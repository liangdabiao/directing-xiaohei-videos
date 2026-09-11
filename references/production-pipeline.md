# 生产管线（apiz 实战参数，2026-09 实测）

前置：`apiz auth login --api-key <key>` 一次即可；查余额 `apiz account balance`；每日 `apiz account checkin` 有免费积分。技能内不得硬编码任何 key。

## 模型选择

| 模型 | 价格 | 时长 | 特点 |
|---|---|---|---|
| `minimax/h3`（默认） | 768P 12积分/秒 | **4–15 秒，支持精确时长** | 按旁白时长生成，无需变速；自带音效轨（响度大，垫底需压低） |
| `google/gemini-omni-flash` | 20积分/秒 | 3–10 秒 | 原生音效+语音；风格遵从度高；只能固定 10s，超长旁白靠后期慢放 |

成本估算：60 秒成片 ≈ h3 720 积分 / gemini 1200 积分 + TTS 数积分。

## h3 调用格式（关键差异，踩过的坑）

h3 通道不走 positional prompt，必须用 `--params` 传结构化请求；比例字段名是 **`ratio`**（不是 `aspect_ratio`，传错会报 "ratio 不能为 adaptive"）；时长是整数秒。

提示词控制在 ≤2500 字符（含英文），提交前 `len()` 校验——gemini 通道 2500 是硬限制；h3 实测略超也能提交，但保持 ≤2500 以跨模型通用。超长会被 HTTP 400 拒绝（不计费）。

把生成逻辑写成脚本文件执行，不要在 shell 里内联多行引号：

```python
import json, subprocess
prompt = open(f'prompts/prompt-{i}.txt', encoding='utf-8').read()
assert len(prompt) <= 2500
params = {
    "content": [{"type": "text", "text": prompt}],   # h3 要求 content 数组
    "duration": dur,                                  # 整数秒 4-15
    "resolution": "768P",                             # 最低档 12积分/秒
    "ratio": "9:16",                                  # 注意字段名
}
subprocess.run(["apiz", "generate", "", "--model", "minimax/h3",
                "--params", json.dumps(params),
                "--wait", "--wait-timeout", "10m", "--json"],
               capture_output=True, text=True, encoding='utf-8')
```

gemini-omni-flash 对照：`apiz generate "<prompt>" --model google/gemini-omni-flash --aspect-ratio "9:16" --params '{"duration":10}' --wait --json`（positional prompt，字段名是 `duration`）。

## 执行纪律

1. **先试点一段**：生成第 1 场 → 下载 → 抽帧检查（白底/小黑形态/线稿/无文字）→ 全链路通了再批量。
2. 每段失败自动重试 1 次；连续失败 2 次先查报错，不盲目重提。
3. 下载用返回 JSON 里的 `result.video_url`（`curl -sL -o clip-N.mp4 "<url>"`），`ffprobe` 核对时长与分辨率（768×1344）。

## 后期合成（实测参数）

按场次时间轴组装，完整脚本骨架见项目 `video/rich-dad-poor-dad/ep2/assemble2.py`，要点：

1. **白场校正**（所有素材统一过同一曲线）：h3/gemini 的"纯白"实际是 213–223 的纸灰，用
   `curves=all='0/0 0.5/0.52 0.70/0.78 0.82/1.0'` 提到 255 纯白，且不伤红/绿/金色饱和度。
2. **时长对齐**：h3 按精确时长生成，场景时长 = `min(旁白时长+0.7s, 素材时长)`，只 trim 不变速。
3. **旁白 TTS**：`apiz speak "<文案>" --voice female-shaonv --speed 1.15 --output-file vo-N.mp3`；
   用 `ffprobe` 测时长，>10s 的段落改 speed 1.18–1.22 重生成（最多两轮，仍超长则该场时长迁就旁白）。
4. **混音**：素材音效床 `volume=0.22` + 六段旁白 `adelay` 到各场起点 + `loudnorm=I=-16:TP=-1.5:LRA=11`。
5. **字幕**：中文 ASS，每条 ≤16 字（超宽会裁字），句间按字数比例分配时间；样式 Microsoft YaHei、暗字白描边、底部 MarginV≈118（768×1344 画布），`subtitles` 滤镜 + `fontsdir='C\:/Windows/Fonts'`。
6. **片尾卡**：白底 + `drawtext` 淡入主口号（如「让钱为你工作」），2.8 秒，静音。
7. **编码**：中间段 mkv crf14 + pcm；成片 mp4 crf18 + aac 192k，`+faststart`。

## 旁白写作细则（TTS 友好）

- 每场 35–50 字；先 TTS 后定场景时长，反过来会返工。
- 数字用汉字（"三十万"比 "300000" 读得稳）；长句先拆短句。
- 同一段 speed 不超过 1.25，宁可剪词。
