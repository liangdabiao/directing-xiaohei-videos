# 生产管线

**默认走免费方案（Agnes keyframe + edge-tts，全套 ¥0）。** 付费方案（apiz h3/gemini）仅作兜底：免费政策结束、免费队列长期满、或用户明确要求更稳的输出时使用。

---

## 一、免费方案（默认）

单段 ¥0；单段耗时约 5-6 分钟（含排队）；一条 1 分钟成片约 30-45 分钟。接口细节见 `agnes.md`。

### 流程总览（每场三步）

```
① 生成首帧图（agnes-image，锁小黑风格与开场构图）
→ ② keyframe 模式生成动画（agnes-video，让首帧动起来）
→ ③ edge-tts 生成该场旁白
→ 全部场次完成后 ffmpeg 合成（白场校正+字幕+批注+片尾卡）
```

### ① 首帧图：agnes-image-2.0-flash

- 接口：`POST https://apihub.agnes-ai.com/v1/images/generations`，请求需 `curl -k`（跳过 SSL）。
- 提示词写法：风格 DNA + 该场"开场状态"（即分镜表三拍的第一拍画面）。包含：纯白背景、手绘抖动线、小黑外形（蛋形黑豆、白点眼、细腿）、物件线稿、留白；结尾加 `No text, no letters, no shadows, no gradients, no people, not cute.`
- **下载必须用响应里的完整 URL**（带 `.png` 后缀；URL 截断会下到 XML 报错页）。
- 下载后过白场曲线，并缩放/裁剪到与视频画幅一致（见"已知问题"）。

### ② 动画：agnes-video-2.5-flash 的 keyframe 模式

- 创建：`POST https://apihub.agnes-ai.com/v1/videos`，参数：
  `model=agnes-video-2.5-flash`、`mode=keyframe`、`first_frame=<首帧图公开URL>`、`seconds="4"–"12"`（字符串）、`size="720P"`（固定）、`aspect_ratio="9:16"` 或 `"16:9"`。
- **必须用 keyframe 模式。** `text` 模式会无视风格约束，生成"真人表情包+动画条+英文烧录字幕"格式，直接作废。
- 运动提示词：英文、简短（3-5 句），只描述"谁做什么动作、什么变化"，并写明 `pure white background, no camera shake, no new objects, no text`。
- 轮询：`GET https://apihub.agnes-ai.com/agnesapi?video_id=<ID>&model_name=agnes-video-2.5-flash`，每 1-2 秒；实测 4-5 分钟完成。
- 免费队列可能返回 `video_queue_full`：30-60 秒退避重试即可。

### ③ 旁白：edge-tts

```bash
python -m edge_tts --voice zh-CN-XiaoxiaoNeural --text "<该场解说词>" --write-media audio/vo-N.mp3
```

- 免费、快、中文自然（晓晓音色）。每场时长用 ffprobe 实测后定场景时长。
- 语速调节用 `--rate=+10%` 这类参数。

### ④ 合成（ffmpeg，同付费管线）

- 白场曲线统一校正；视频与图片画幅不一致时用白色 pad 补边（补白比拉伸放大画质损失小）。
- 字幕（≤16 字/条）、批注贴字（STXINGKA 华文行楷）、片尾卡、loudnorm 同付费管线。

### 已知问题（宽松档口径）

- keyframe 模式可能自行添加环境装饰（如树框）——**通过，不重做**；提示词写 `no new objects` 能降低概率。
- 实际输出尺寸偶与文档不符（16:9 档实测 960x704 而非 1280x704）——补白或等比缩放处理。
- 免费政策随时可能取消；量产前先跑 1 段确认仍免费。

### 待验证项

- 竖屏 9:16 的首帧图：图片接口默认出横图（1152x864 / 1024x768）。可尝试 `"size": "768x1024"` 请求竖图（未验证）；不行则先用 16:9 视频或横图裁切。

---

## 二、付费方案（兜底）

前置：`apiz auth login --api-key <key>` 一次即可；查余额 `apiz account balance`；每日 `apiz account checkin` 有免费积分。技能内不得硬编码任何 key。

### 模型选择

| 模型 | 价格 | 时长 | 特点 |
|---|---|---|---|
| `minimax/h3`（付费首选） | 768P 12积分/秒 | **4–15 秒，支持精确时长** | 按旁白时长生成，无需变速；自带音效轨（响度大，垫底需压低） |
| `google/gemini-omni-flash` | 20积分/秒 | 3–10 秒 | 原生音效+语音；风格遵从度高；只能固定 10s，超长旁白靠后期慢放 |

成本估算：60 秒成片 ≈ h3 720 积分 / gemini 1200 积分 + TTS 数积分。

### h3 调用格式（关键差异，踩过的坑）

h3 通道不走 positional prompt，必须用 `--params` 传结构化请求；比例字段名是 **`ratio`**（不是 `aspect_ratio`，传错会报 "ratio 不能为 adaptive"）；时长是整数秒。

提示词控制在 ≤2500 字符（含英文），提交前 `len()` 校验——gemini 通道 2500 是硬限制；h3 实测略超也能提交，但保持 ≤2500 以跨模型通用。超长会被 HTTP 400 拒绝（不计费）。

把生成逻辑写成脚本文件执行，不要在 shell 里内联多行引号：

```python
import json, subprocess
prompt = open(f'prompts/prompt-{i}.txt', encoding='utf-8').read()
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

### 执行纪律

1. **先试点一段**：生成第 1 场 → 下载 → 抽帧确认（白底/小黑形态/线稿/无文字）→ 通了再批量。
2. 宽松档口径下每段失败重试 1 次；连续失败 2 次先查报错，不盲目重提。
3. 下载用返回 JSON 里的 `result.video_url`（`curl -sL -o clip-N.mp4 "<url>"`），`ffprobe` 核对时长与分辨率（h3 为 768×1344）。

### 后期合成（两套管线通用）

完整脚本骨架见 `xiaohei-video-director/production/trust-boundaries/assemble.py`，要点：

1. **白场校正**（所有素材统一过同一曲线）：手绘白底的"纯白"实际是 213–223 的纸灰，用
   `curves=all='0/0 0.5/0.52 0.70/0.78 0.82/1.0'` 提到 255 纯白，且不伤红/绿/彩色饱和度。
2. **时长对齐**：场景时长 = `min(旁白时长+0.7s, 素材时长)`，只 trim 不变速（h3 按精确时长生成时天然对齐）。
3. **混音**：素材音效床 `volume=0.22`（无声素材可省）+ 各场旁白 `adelay` 到场次起点 + `loudnorm=I=-16:TP=-1.5:LRA=11`。
4. **字幕**：中文 ASS，每条 ≤16 字（超宽会裁字），句间按字数比例分配时间；Microsoft YaHei、暗字白描边、底部 MarginV≈118（768×1344 画布），`subtitles` 滤镜 + `fontsdir='C\:/Windows/Fonts'`。
5. **批注贴字**：按 Phase A 批注规划表，用华文行楷（`STXINGKA.TTF`）+ 四色语义淡入；**注意每条批注显式标注所属场次号**（自动推断会错位）。
6. **片尾卡**：白底 + `drawtext` 淡入主口号，2.8-3 秒，静音。
7. **编码**：中间段 mkv crf14 + pcm；成片 mp4 crf18 + aac 192k，`+faststart`。

### 旁白写作细则（TTS 友好）

- 每场 35–50 字；先 TTS 后定场景时长，反过来会返工。
- 数字用汉字（"三十万"比 "300000" 读得稳）；长句先拆短句。
- edge-tts 语速用 `--rate`，minimax 用 `--speed`（≤1.22，宁可剪词）。
