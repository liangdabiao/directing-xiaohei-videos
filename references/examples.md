# Complete Example（端到端示例）

Load only when a concrete example resolves ambiguity. Reuse the workflow and level of detail — never the topic, metaphors, or wording. 本示例的「融化的钱冰淇淋」构图已列入反复刻清单。

## User source

“通货膨胀到底是什么？为什么你什么都没买，钱却变少了？”

## Setup gate

Assistant: “请选择画幅（16:9 或 9:16）与旁白语言（默认中文）。”
User: “9:16，中文。”

## Phase A — 导演提案

**中文标题：**《你什么都没买，钱却变小了》
**英文标题：** *Inflation: Your Money Is Melting*

**核心信息：** 通货膨胀不是东西涨价，是你手里钱的购买力在慢慢蒸发；只拿着现金的人，每年都在变小。

**Hook：** 一根冰淇淋放在桌上，没人碰它，它自己在变小。

**规格：** 9:16 竖屏，白底黑小黑，中文旁白，约 252 字 ≈ 58 秒。

**旁白声线：** 清晰亲和女声（shaonv），语速 1.15。

**四色语义规划：** 黑=小黑与柜台/冰淇淋线稿；橙=钱的流向（工资→柜台）；红=缩水/警告（本片的情绪色，留给第 4、6 场）；蓝=脑内想法（第 3 场一处）。

**BGM/情绪弧：** 极简节拍，第 4 场变紧，第 6 场收束明亮。好奇 → 发现 → 惊 → 焦虑 → 理解 → 行动。

| # | 时间 | 叙事职责 | 小黑场景 | 运动/镜头/转场 | 旁白 | 批注规划 | 音效 |
|---|---|---|---|---|---|---|---|
| 1 | 10s | 钩子 | 小黑端着托盘，把一根标着"钱"的冰淇淋放在柜台中央，退后一步立正看着它 | 0-3 放下+立正；3-7 缓慢推近冰淇淋；7-10 冰淇淋表面出现第一个小凹坑，小黑歪头 | 想象你手里有一根冰淇淋。你没吃它，没人碰它，它就放在桌上。可是它，正在自己变小。 | 「钱？」黑，0-2s，托盘上方 | 放盘轻响、安静环境音 |
| 2 | 10s | 机制命名 | 凹坑扩大，一滴奶油滴落；小黑掏出小本子记录，抬头看蒸发的水汽 | 0-3 滴落特写；3-7 小黑记录+抬头；7-10 蒸汽线条上升，冰淇淋矮了一截 | 这就是通货膨胀。东西还是那些东西，是钱自己的购买力，在一滴一滴地蒸发。 | 「购买力↓」红，7s，冰淇淋旁 | 滴落声、翻本子声 |
| 3 | 10s | 时间放大 | 画面分屏：左边一年，小黑打盹；右边冰淇淋缩成一半，头顶冒出蓝色想法泡（更小的冰淇淋+问号） | 0-3 分屏拉开；3-7 右侧缩水动画加速；7-10 想法泡亮起 | 你什么都没做错，没有乱花钱，只是把现金放在那里。一年之后，它能买到的东西，就少了这么多。 | 「一年后」蓝，0s 分屏上方 | 时钟轻响、缩小音效 |
| 4 | 10s | 后果（红） | 柜台上冰淇淋只剩一张糖纸；小黑举起糖纸对光看，糖纸是半透明的，红色"缩水 10 年"进度条从满格掉到底 | 0-3 举纸对光；3-7 进度条快速下降；7-10 红色进度条清空闪两下 | 如果每年蒸发百分之三，十年之后，这一百块的实际购买力，只剩七十多。你什么都没买，但你已经付过钱了。 | 「-30%」红，8s，进度条尾 | 低频紧张、进度条滴答 |
| 5 | 10s | 实践 | 小黑把冰淇淋插进一台怪机器的投币口，机器嗡嗡转动，吐出一支更大的冰淇淋，小黑扶稳机器继续投喂 | 0-3 投币入机；3-7 机器运转吐出新冰淇淋；7-10 小黑拍机器，新的更大 | 所以现金会化，就要让它变成会生长的东西：能收租的资产、能分红的公司、能增值的本事。让增长跑赢蒸发。 | 「会生长的」橙，7s，机器上方 | 机器嗡嗡、吐出叮当 |
| 6 | 10s | 收束 | 小黑举起新冰淇淋对镜头立正，头顶蒸汽换成了向上的橙色箭头；箭头带光点飘向镜头渐白 | 0-3 举起立正；3-7 蒸汽变橙箭头上升；7-10 箭头光点充满画面渐白 | 记住：钱不会自己变多，它只会安静地变小。别让它一直躺在桌上——让它去生长。 | 「别让它躺着」红，8s，顶部 | 明亮收束音、渐白风声 |

**场间交接：** 1→2 凹坑出现↔凹坑扩大滴落；2→3 蒸汽上升↔分屏右侧蒸汽延续；3→4 缩小的冰淇淋↔只剩糖纸；4→5 红进度条清空↔小黑转身面向机器；5→6 新冰淇淋举起↔举高对镜头；6→片尾 渐白↔白底文字卡。

## Phase B — 六场提示词

### 默认免费管线交付（每场 = 首帧图提示词 + 运动提示词），以第 1、4 场为例

**场景 1 · 首帧图提示词**

```text
Minimalist black hand-drawn illustration on a pure white background. Slightly wobbly pen strokes, uniform line weight. Lots of empty white space.

小黑, a small solid-black creature with two round white dot eyes facing the viewer, tiny thin legs, short thin arms, a blank serious expression, and a bumpy, slightly uneven hand-drawn outline. The black fill is flat and matte, with no glow, no highlights, no gradients. 小黑 is a simple egg-shaped black blob, NOT furry, NOT spiky, NOT hairy; its eyes are two small plain white dots, NOT large cartoon eyes. In this first frame 小黑 sits on a small stool at the center of a tiny outline-drawn hut, holding a tea cup, while two plain vertical pillars hold up the roof, one on the left and one on the right. The whole hut fills the upper two thirds; the bottom third is empty white space.

No text, no letters, no numbers, no shadows, no gradients, no paper texture, no people, not cute.
```

**场景 1 · 运动提示词（keyframe）**

```text
小黑 takes one slow sip of tea, then lowers the cup and looks up at the roof. A short orange stroke traces the left pillar, then the right pillar. A thin red crack line appears on the left pillar and the roof tilts slightly. Simple 2D hand-drawn motion on pure white background, no camera shake, no new objects, no text.
```

**场景 4 · 首帧图提示词**

```text
Minimalist black hand-drawn illustration on a pure white background. Slightly wobbly pen strokes, uniform line weight. Lots of empty white space.

小黑, a small solid-black creature with two round white dot eyes facing the viewer, tiny thin legs, short thin arms, a blank serious expression, and a bumpy, slightly uneven hand-drawn outline. The black fill is flat and matte. 小黑 is a simple egg-shaped black blob, NOT furry, NOT spiky, NOT hairy; its eyes are two small plain white dots, NOT large cartoon eyes. In this first frame 小黑 walks along a ground line carrying an empty simple back rack, with one thin line straw already resting on the rack.

No text, no letters, no numbers, no shadows, no gradients, no paper texture, no people, not cute.
```

**场景 4 · 运动提示词（keyframe）**

```text
More thin straws keep falling from above onto the rack, one by one, and the stack grows taller. 小黑 slows down, knees bending, body leaning forward under the growing load. Then one last tiny straw floats down gently; the moment it lands, 小黑 collapses flat on the ground and the straws scatter around, tinted red. Simple 2D hand-drawn motion on pure white background, no camera shake, no new objects, no text.
```

（其余四场按同一格式从分镜表展开；场景参数：seconds 取旁白时长+0.5s 取整，size "720P"，aspect_ratio "9:16"。）

### 付费备选：12 项完整文本提示词（节选两条，h3/gemini 用）

## Phase B — 六条提示词（节选两条，其余按同合同展开）

### Prompt 1

```text
Output: one continuous 2D motion-graphics clip, exactly 10 seconds, 9:16 vertical, 768p, whiteboard cartoon style.

Background: a completely flat, uniform, digitally pure-white canvas — no tint, no paper texture, no grain, no gradients, no vignette, no shadows, no 3D depth.

Line art: minimalist black hand-drawn strokes, slightly wobbly, uniform line weight.

Character lock: 小黑, a small solid-black creature with round white dot eyes, tiny thin legs, short thin arms, a blank serious expression, and a slightly uneven hand-drawn body outline. The black fill is flat and matte. 小黑 stays serious, deadpan, and slightly bizarre — never cute. In this scene 小黑 carries a small round tray, places one simple ice-cream cone at the center of a plain counter, then steps back and stands at attention like a careful clerk.

Palette: black for 小黑, the counter and the ice cream; orange unused; red reserved for one tiny dent line; blue unused. No other colors.

Composition: 9:16 — the counter is a single horizontal line in the middle band, the ice cream at center, 小黑 to its right, generous white space above for overlays.

First frame: an empty white canvas.

[0-3s] 小黑 walks in from the right holding the tray, places the ice cream on the counter, steps back, stands at attention.
[3-7s] Slow camera push-in on the ice cream cone; 小黑's dot eyes track it; a faint wobble line above the cone hints at warmth.
[7-10s] A tiny dent appears on the ice cream's side, drawn as one short red line; 小黑 tilts its head slightly; the frame holds on the dented cone.

Audio: synchronized sound effects only — a soft tray clink, quiet room tone, one subtle squish as the dent appears. No narration, no speech, no words in the audio.

Final frame: the dented ice cream cone at center, 小黑 head-tilted beside it.

Style: rapid scene changes, kinetic motion-graphic transformations, and frequent visual events, while preserving an identical character design, constant line weight, and strict temporal consistency; a visible change every 2-3 seconds.

Negatives: no photorealism, no 3D rendering, no facial expressions beyond blank dot eyes, no cute mascot look, no children's cartoon style, no clothing on 小黑, no extra limbs, no changed proportions, no varying line weight, no theme inversion, no unexplained colors, no extra characters, no irrelevant spectacle, no visible words, letters, numbers, captions, subtitles, labels, interface copy, logos, watermarks, or technical color notation anywhere.
```

### Prompt 4

```text
Output: one continuous 2D motion-graphics clip, exactly 10 seconds, 9:16 vertical, 768p, whiteboard cartoon style.

Background: a completely flat, uniform, digitally pure-white canvas — no tint, no paper texture, no grain, no gradients, no vignette, no shadows, no 3D depth.

Line art: minimalist black hand-drawn strokes, slightly wobbly, uniform line weight.

Character lock: 小黑, a small solid-black creature with round white dot eyes, tiny thin legs, short thin arms, a blank serious expression, and a slightly uneven hand-drawn body outline. The black fill is flat and matte. 小黑 stays serious, deadpan, and slightly bizarre — never cute. In this scene 小黑 lifts the last wrapper of the melted ice cream and holds it up against the light to inspect it.

Palette: black for 小黑, the wrapper and the meter; orange unused; red only for the draining meter and its final blink; blue unused. No other colors.

Composition: 9:16 — the wrapper held high at center, a vertical battery-style meter beside it, 小黑 small below the wrapper, white space at the bottom for subtitles.

First frame: a completely melted puddle on the counter with only the wrapper left, inherited from the previous clip.

[0-3s] 小黑 picks up the translucent wrapper and raises it toward the camera; light passes through as simple hatching lines.
[3-7s] A vertical red meter beside the wrapper drains from full to nearly empty, tick by tick, each tick shrinking the wrapper slightly.
[7-10s] The meter hits empty and blinks red twice; the wrapper crumples; 小黑 stares at it, motionless, deadpan.

Audio: synchronized sound effects only — a low tense hum, meter ticks, two soft alarm blinks. No narration, no speech, no words in the audio.

Final frame: the crumpled wrapper in 小黑's hand with the empty red meter beside it.

Style: rapid scene changes, kinetic motion-graphic transformations, and frequent visual events, while preserving an identical character design, constant line weight, and strict temporal consistency; a visible change every 2-3 seconds.

Negatives: no photorealism, no 3D rendering, no facial expressions beyond blank dot eyes, no cute mascot look, no children's cartoon style, no clothing on 小黑, no extra limbs, no changed proportions, no varying line weight, no theme inversion, no unexplained colors, no extra characters, no irrelevant spectacle, no visible words, letters, numbers, captions, subtitles, labels, interface copy, logos, watermarks, or technical color notation anywhere.
```

（Prompt 2/3/5/6 按同一 12 项合同从分镜表展开，此处略。）

## 拼接指南

1→2 硬切（凹坑特写延续）；2→3 硬切（蒸汽升入分屏）；3→4 硬切（缩小的冰淇淋接只剩糖纸）；4→5 硬切（小黑转身方向一致）；5→6 硬切（新冰淇淋位置居中一致）；6→片尾 渐白接白底文字卡「别让它一直躺着」。旁白起点 = 每场起点 +0.1s；批注按分镜表时机以手写体淡入。

## 音频与后期批注说明

生成仅音效；旁白外部 TTS（shaonv，1.15）；批注六处（钱？/购买力↓/一年后/-30%/会生长的/别让它躺着）按上表颜色与时机贴字，全片 ≤12 处。混音 loudnorm -16 LUFS，音效床 0.22 倍。
