# Phase B · 生产提示词合同

仅在当前 Phase A 获得明确批准后使用。

**默认按"免费管线"交付：每场两条提示词——① 首帧图提示词 ② 运动提示词（keyframe 模式）。**
仅当用户指定付费管线（h3/gemini 文生视频）时，才按文末"付费备选"写出 12 项完整提示词。

## 生产包顺序

1. 全局连续性块（复审摘要）
2. 六场的【首帧图提示词 + 运动提示词】
3. 拼接指南
4. 音频与后期批注说明

## ① 首帧图提示词（免费管线，每场一条）

作用：锁定该场的风格与开场构图，作为 keyframe 视频的首帧。

按顺序包含：

1. **画布与线稿**：Minimalist black hand-drawn illustration on a pure white background. Slightly wobbly pen strokes, uniform line weight. Lots of empty white space.
2. **小黑角色锁**（原文照抄）：
   > 小黑, a small solid-black creature with two round white dot eyes facing the viewer, tiny thin legs, short thin arms, a blank serious expression, and a bumpy, slightly uneven hand-drawn outline. The black fill is flat and matte, with no glow, no highlights, no gradients. 小黑 is a simple egg-shaped black blob, NOT furry, NOT spiky, NOT hairy; its eyes are two small plain white dots, NOT large cartoon eyes.
   并写明该场开场时小黑的位置、姿势、动作。
3. **物件与构图**：物件一律 black outlines on white（只有小黑实心黑）；写清主要物件、空间关系、留白区（含底部字幕安全区）。
4. **首帧状态**：分镜表第一拍的开场画面（什么在哪里、什么颜色点缀）。
5. **收尾禁则**：No text, no letters, no numbers, no shadows, no gradients, no paper texture, no people, not cute.

长度控制在 ~1200 字符内。

## ② 运动提示词（keyframe 视频，每场一条）

作用：告诉视频模型"从首帧开始发生什么"。

- 英文，3–5 句，只描述**动作与变化**：小黑做什么、物件如何变化、哪种颜色承担语义、镜头如何动。
- 必须写：`simple 2D hand-drawn motion on pure white background, no camera shake, no new objects, no text.`
- 不重复角色外形描述（首帧已锁定）；不写字幕词。
- 对应分镜表的三拍，压成一句连续的动作链。

## ③ 场次参数（免费管线）

- `seconds`：字符串 `"4"`–`"12"`，按该场旁白时长 +0.5s 取整。
- `aspect_ratio`：与成片一致（`"9:16"` 或 `"16:9"`）；`size` 固定 `"720P"`。
- 首帧图下载后过白场曲线并匹配视频画幅（补白优先于拉伸）。

## 付费备选：12 项完整文本提示词（h3/gemini 文生视频）

仅付费管线使用。每条按此顺序写全：

1. **输出规格**：one continuous 2D whiteboard-cartoon clip, exactly N seconds（整数）, 9:16（或 16:9）vertical, 768p。
2. **画布锁**：a flat, uniform, digitally pure-white canvas — no tint, texture, grain, gradients, vignette, shadows, or 3D depth。
3. **线稿锁**：minimalist black hand-drawn strokes, slightly wobbly, uniform line weight。
4. **小黑角色锁**：同上角色锁原文 + 本场位置、动作、变形；物件按白底黑线稿规则描述。
5. **四色语义**：exactly three accent colors——orange only for main flow/arrows, red only for warning/problem/result, blue only for secondary notes（本场用不到的写 unused）。No other colors.
6. **构图策略**：画幅内主要元素空间关系 + 留白区。
7. **首帧状态**：继承上一场结尾。
8. **三拍时间轴**：`[0–⅓] [⅓–⅔] [⅔–N]` 三段。
9. **音频**：synchronized sound effects only — no narration, no speech, no words in the audio。
10. **末帧状态**：交给下一场的交接物。
11. **风格密度句**（照抄）：rapid scene changes, kinetic motion-graphic transformations, and frequent visual events, while preserving an identical character design, constant line weight, and strict temporal consistency; a visible change every 2-3 seconds.
12. **负向锁**：no photorealism, no 3D rendering, no facial expressions beyond blank dot eyes, no cute mascot look, no children's cartoon style, no extra limbs, no changed proportions, no varying line weight, no theme inversion, no extra characters, no visible words, letters, numbers, captions, subtitles, labels, logos, watermarks, or technical color notation anywhere.

长度 ≤2500 字符；时长数字与生成参数一致。

## 通用硬约束

- 提示词主体用英文；批注词绝不进入任何提示词（画面禁文字，批注走后期）。
- 不引入 Phase A 之外的新叙事主张。
- 每场首帧 = 上一场末帧（写清交接物），拼接指南里逐字对应。

## 拼接指南

按顺序列出六段；每个剪辑点重复"上一段结尾状态 ↔ 下一段开头状态"；标注硬切/溶解；说明字幕与批注入场时机。

## 音频与后期批注说明

1. 免费管线素材无音轨、旁白用 edge-tts 统一音色逐场生成；付费管线素材音效以低电平垫底。
2. 旁白时长实测后定为各场时长；混音 loudnorm -16 LUFS。
3. 批注按 Phase A 批注规划表，后期以华文行楷贴字：词、颜色、场次、时机逐条列出（合成时每条批注必须显式标注场次号，防错位）。

## Phase B 检查

- 六场齐全：免费管线=每场两条提示词（图+运动）；付费管线=每场一条 12 项提示词。
- 首帧图提示词含角色锁原文与开场状态；运动提示词含 no new objects / no text。
- 每场时长参数在通道支持范围内（免费 4–12s；h3 4–15s；gemini 3–10s）。
- 每个结尾与下一个开头逐字对应；生成画面零文字；批注全部在后期层。
- 无技术色号；无新叙事主张。
