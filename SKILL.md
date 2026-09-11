---
name: directing-xiaohei-videos
description: Use when turning copy, notes, articles, or topics into approximately one-minute Chinese-narrated "Xiao Hei" (小黑) motion videos — deadpan absurd white-canvas explainer clips with the solid-black character, for generation via the apiz pipeline (minimax/h3 or google/gemini-omni-flash). Covers storyboard proposals, shot-level prompt packages, production pipeline, and frame-level QA.
---

# Directing Xiaohei Videos（小黑动态视频导演）

## Core contract

Turn one source into a confirmed director's proposal (Phase A) and then six standalone production prompts (Phase B) for roughly ten-second clips starring 小黑 — the solid-black deadpan creature — preserving the source's meaning while strengthening its hook, progression, and closing callback.

小黑视频 = 火柴人视频的骨架 + 小黑配图的灵魂：

- 骨架（来自 directing-stickman-videos，已验证）：Setup gate → Phase A 提案 → 批准门 → Phase B 六段提示词包 → 生成 → 合成。三拍节奏、场间交接、负向锁、旁白 audio-only 全部保留。
- 灵魂（来自 ian-xiaohei-illustrations，必须移植）：实心小黑 IP、纯白手绘、四色批注语义、低科技怪机器隐喻发明法、"小黑是动作主体不是装饰"。

## Setup gate

Require these before planning:

- source material（文案、文章、笔记或主题）
- aspect ratio：`16:9` 或 `9:16`（小黑视频默认建议 `9:16`；`1:1` 不支持）
- narration language：默认中文（小黑内容的批注天然是中文语境）；英文需用户显式指定
- theme 固定为白底黑小黑。黑色背景会让实心黑色小黑隐形，v1 不提供暗色主题；如用户坚持暗色，解释后改用"反白小黑"（白色实心+黑点眼）并按全局变更重新提案

If anything required is missing, ask for all missing items in one concise message and stop. Do not re-ask choices already supplied.

## Workflow

1. Read `references/metaphor-invention.md` and `references/xiaohei-ip.md`：先为每个场景发明新隐喻（物理动作 + 低科技物件 + 小黑动作），禁止复刻任何旧构图。
2. Read `references/storyboard-template.md` and produce Phase A in Chinese. 旁白默认中文（240–270 汉字 ≈ 55–65 秒）；每场附"批注规划"（后期手写批注的词/颜色/时机/位置）。
3. Stop after the director's proposal and request explicit approval.
4. If the user changes ratio, narration, scene structure, or global style, recompose Phase A and request approval again.
5. Only after approval of the current Phase A, read `references/video-prompt-contract.md` and produce Phase B.
6. When the user asks to actually produce the video, read `references/production-pipeline.md`（apiz 生成 + TTS + 字幕合成的实战参数）。
7. After generation, apply `references/qa-checklist.md`（抽帧 QA，默认宽松档：快速出片、少重做，仅灾难级失败重做）。
8. Use `references/examples.md` only when a concrete end-to-end example resolves ambiguity.

Topic approval, schedule pressure, or approval of an older draft is not approval of the current Phase A.

## Output rules

- 旁白 240–270 汉字，六场，每场 35–50 字 ≈ 8–12 秒。
- 每场三拍（开场继承/中段转化/结尾高潮+交接），至少四个相关视觉设备，每 2–3 秒一次可感知变化。
- 四色语义固定：黑色=小黑与结构线稿（画布主体）；橙色=主流向/路径/箭头；红色=警示/问题/结果；蓝色=补充说明/脑内/系统状态。宁少勿多，不出现其他颜色。
- 小黑必须是每场的动作主体；去掉小黑后隐喻不成立才算合格。
- 生成画面内禁止任何文字、字母、数字、界面、标注（中文手写批注是风格的一部分，但渲染易错，全部下沉到后期叠字层；Phase A 的批注规划表就是给后期的施工图）。
- 旁白是 audio-only；禁止在提示词中要求模型朗读、显示或转写旁白。
- 每条生成提示词自包含，重复所有关键锁（白底、手绘线、小黑外形、四色、禁文字）。
- 不虚构数据、引语、统计和产品主张。

## Revision rules

Recompose rather than rename：

- `16:9`：左中右调度、横向跟踪、负空间留叠字安全区。
- `9:16`：上下分层、纵深、垂直揭示、底部字幕安全区。
- 全局变更（比例、旁白语言、四色语义、语气）作废旧批准，重出 Phase A。

## Final check

Apply the checklist in `references/qa-checklist.md`. Repair any failed condition before responding.
