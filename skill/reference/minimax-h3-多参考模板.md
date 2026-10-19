
# MiniMax H3 Ref2VA 六段式提示词模板

## 上传清单

| 编号 | 资产编码 | 文件路径 | 对应标签 |
|---|---|---|---|
| 图1 | 小夜_正 | `assets/人物/小夜/正.png` | `<Subject 1>` |
| 图2 | 阿雾_正 | `assets/人物/阿雾/正.png` | `<Subject 2>` |
| 图3 | 便利店_夜 | `assets/场景/便利店/夜.png` | `<Subject 3>` |
| 图4 | 便利店门口_夜 | `assets/场景/便利店门口/夜.png` | `<Subject 4>` |
| 图5 | 街道_雨 | `assets/场景/街道/雨.png` | `<Subject 5>` |

## 标准结构（可直接复制）

```
subject_definitions:
<Subject 1> is Xiaoye, whose face and outfit come from <Picture 1>.
<Subject 2> is Awu, whose face and outfit come from <Picture 2>.
<Subject 3> is the convenience store interior at night, whose layout and warm lighting come from <Picture 3>.
<Subject 4> is the convenience store entrance at night, whose glass door and exterior come from <Picture 4>.
<Subject 5> is the rainy street at night, whose wet pavement and distant glow come from <Picture 5>.

summary:
[reference generation] A 15-second rainy-night scene in and around a convenience store, featuring Xiaoye and Awu. The target video uses the character references for facial and outfit consistency, and the environment references for the store interior, the entrance, and the rainy street.

retention_analysis:
<Subject 1> (appears in [Shot 2], [Shot 5]): fully_preserved - Xiaoye retains her facial identity and outfit from <Picture 1>.
<Subject 2> (appears in [Shot 4]): fully_preserved - Awu retains her facial identity, wet black hair, and outfit from <Picture 2>.
<Subject 3> (appears in [Shot 2], [Shot 3]): fully_preserved - the store interior layout and warm lighting are retained.
<Subject 4> (appears in [Shot 3], [Shot 4]): fully_preserved - the glass door and entrance area are retained.
<Subject 5> (appears in [Shot 1]): fully_preserved - the rainy street surface and distant store glow are retained.

detailed_description:
The target video uses a cinematic live-action style with soft warm interior lighting and a cool rainy exterior palette.

[Shot 1] An empty rainy street at night; warm light from a distant convenience store glows through the glass. Static shot.
[Shot 2] At 00:03.000, the camera cuts to the inside of the convenience store, where Xiaoye stands behind the counter wiping a cup. Static shot.
[Shot 3] At 00:06.000, the camera cuts to the glass door of the convenience store being pushed open, and the door chime rings. Static shot.
[Shot 4] At 00:08.000, the camera cuts to Awu standing at the doorway, rainwater dripping from the tips of her wet black hair. Static shot.
[Shot 5] At 00:12.000, the camera cuts to Xiaoye looking up, her eyes slightly stunned; the camera pushes in at slow speed with small amplitude to a close-up. Warm yellow light falls on Xiaoye's face.

overall_soundscape:
Rain falls throughout as a continuous ambient bed. During the interior shots, a refrigerator hum is audible. At Shot 3, the door chime rings once.

non_diegetic_music:
Sparse single piano notes, with large reverb and low volume.
```

##关键规则

字段 规则
六段顺序 subject_definitions → summary → retention_analysis → detailed_description → overall_soundscape → non_diegetic_music，不可变
六段主体语言 全英语；仅 <d> 内台词/歌词、双引号内画面可见文字可保留中文
subject_definitions 每个引用主体一行；场景/道具用 whose layout/lighting/material comes from ...，不要套用角色的 face and outfit
summary 以 [reference generation] 开头
retention_analysis 每个标签一行；标记只用 fully_preserved / partially_preserved / attribute_transfer / weak_reference
[Shot 1] 不写时间戳
后续镜头 At MM:SS.mmm, the camera cuts to ...，严格递增且不超段长
台词 <Subject N> (S1) says, <d>[Chinese] 逐字台词。</d>
画面文字 英文双引号包裹原文，如 "营业中"
overall_soundscape 1–4 句英语；只写环境声、物理动作声、非语言人声；不重复对白/音乐
non_diegetic_music 1–3 句英语；只写乐器、速度、节奏、动态；不写抽象情绪词；无配乐写 N/A
画内拟声词 不是画面文字，六段内必须写英语，如 door chime ding

