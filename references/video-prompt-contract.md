# Phase B · 生产提示词合同

仅在当前 Phase A 获得明确批准后使用。

## 生产包顺序

1. 全局连续性块（复审摘要）
2. 六条独立提示词
3. 拼接指南
4. 音频与后期批注说明

全局块只作复审摘要；每条提示词仍必须自包含、重复全部关键锁。

## 单条提示词的 12 项顺序

1. **输出规格**：one continuous 2D motion-graphics clip, exactly N seconds（按该场时长写死整数，模型支持 4–15s 时用旁白时长 +0.7s）, 9:16（或 16:9）vertical/horizontal, 768p, whiteboard cartoon style。
2. **画布锁**：a completely flat, uniform, digitally pure-white canvas — no tint, no paper texture, no grain, no gradients, no vignette, no shadows, no 3D depth。
3. **线稿锁**：minimalist black hand-drawn line art, slightly wobbly pen strokes, uniform line weight。
4. **小黑角色锁**（原文照抄，不得改写）：
   > 小黑, a small solid-black creature with two round white dot eyes facing the viewer, tiny thin legs, short thin arms, a blank serious expression, and a bumpy, slightly uneven hand-drawn outline. The black fill is flat and matte, with no glow, no highlights, no gradients. 小黑 stays serious, deadpan, and slightly bizarre — never cute.
   并写明本场小黑的位置、动作、是否变形；物件按"白底黑线稿、只有小黑实心黑"的填充规则描述（outline-drawn machines/objects, only 小黑 solid black）。
5. **四色语义**：exactly three accent colors on the white canvas（黑为底色不计入）：orange only for main flow/arrows, red only for warning/problem/result, blue only for secondary notes/system state（本场用不到的颜色写 unused）。No other colors.
6. **构图策略**：按画幅写明主要元素的空间关系与留白区（含叠字安全区）。
7. **首帧状态**：从上一场结尾继承的可见状态。
8. **三拍时间轴**：`[0–⅓s] [⅓–⅔s] [⅔–Ns]` 三段，写清每拍：小黑动作、物件状态变化、镜头运动、哪种颜色承担语义、结束时画面被什么填满或退出。
9. **音频**：synchronized sound effects only（或无声）——absolutely no narration, no speech, no words in the audio。旁白由外部 TTS 在合成阶段叠加。
10. **末帧状态**：交给下一场的可见交接物。
11. **风格密度句**（照抄）：rapid scene changes, kinetic motion-graphic transformations, and frequent visual events, while preserving an identical character design, constant line weight, and strict temporal consistency; a visible change every 2-3 seconds。
12. **负向锁**：no photorealism, no 3D rendering, no facial expressions beyond blank dot eyes, no cute mascot look, no children's cartoon style, no clothing on 小黑, no extra limbs, no changed proportions, no varying line weight, no theme inversion, no unexplained colors, no extra characters, no irrelevant spectacle, no visible words, letters, numbers, captions, subtitles, labels, interface copy, logos, watermarks, or technical color notation anywhere.

## 硬约束

- 提示词主体用英文；总长 ≤2500 字符（生成通道的硬限制，提交前数一遍）。
- 批注词绝不进入提示词（画面禁文字）。
- 不引入 Phase A 之外的新叙事主张。
- 时长数字必须写"exactly N seconds"并在生成参数中传同一数值。

## 拼接指南

按顺序列出六段；每个剪辑点重复"上一段结尾状态 ↔ 下一段开头状态"；标注硬切/4–8 帧溶解；说明字幕与批注的入场时机。

## 音频与后期批注说明

1. 画面生成仅含音效（或无声），避免分段生成导致音色漂移。
2. 旁白用外部统一 TTS（同 voice、同语速）逐场生成，合成时按场次时间轴叠加。
3. 批注按 Phase A 的批注规划表，在剪辑阶段以手写风字体贴字：词、颜色、入场时机、位置逐条列出。
4. 混音：旁白为主（峰值约 -1 dBFS 呼叫 loudnorm -16 LUFS），素材音效床以低电平（约 0.2–0.3 倍）垫底，杂乱则弃用。

## Phase B 检查

- 六条提示词齐全，均 ≤2500 字符。
- 每条重复：规格、白底、线稿、小黑锁、四色、构图、首帧、三拍、音频、末帧、密度句、负向锁。
- 每个结尾与下一个开头逐字对应。
- 生成画面零文字；批注全部列在后期层。
- 无技术色号；无新叙事主张。
