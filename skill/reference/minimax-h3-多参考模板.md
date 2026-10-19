---

MiniMax H3 Ref2VA 六段式提示词模板

标准结构（可直接复制）

```text
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

关键规则

1. 输出契约

只输出六个字段，字段名小写、带冒号，无前言、无解释、无 Markdown 代码围栏。六段主体全部英语，唯一例外：<d>内的对白/歌词、画面可见文字保留原语言。

2. subject_definitions

每行定义一个引用单位。图片仅用于定义角色/场景/风格时，不单独建<Picture N>行，而是写进<Subject N>定义里，注明来源。上例中<Picture 1>到<Picture 5>均为“来源图片”，因此只作为<Subject N>的出处引用，不单独成行。

3. summary

以方括号任务类型开头。本模板为角色/场景参考，用[reference generation]；若同时复用音频，用+组合[audio reuse]。

4. retention_analysis

每个标签一行，只能用固定标记：视觉内容用fully_preserved、partially_preserved、attribute_transfer、weak_reference；音频用fully_copy、partially_copy、reference、weak_reference。格式为<Subject N> (appears in [Shot k]): marker - 保留了什么。

5. detailed_description

· 先写1–2句整体风格，再进入[Shot 1]，风格声明不放进首镜。
· [Shot 1]无时间戳；后续镜头用[Shot N] At MM:SS.mmm, the camera cuts to ...，时间严格递增。
· 每镜按构图、主体外貌与位置、环境与光线、动作与状态变化、运镜、当前声音、引用内容生效点来写，不写成剧情梗概。
· 运镜写自然英语动作 + 幅度 + 速度，如pushes in at slow speed with small amplitude，不堆标签。
· 台词格式：<Subject 2> (S1) says, <d>[Chinese] 老样子。</d>，台词外写说话人和语气，<d>内只放语言标签和逐字台词。

6. overall_soundscape

1–4句英语，只写环境声、物理动作声、非语言人声。不重复对白、歌唱或画内音乐；完全静音才写N/A。

7. non_diegetic_music

1–3句英语，只写角色听不到的配乐：乐器、速度、节奏、动态。不写抽象情绪词；无配乐写N/A。

上传清单（六段外，中文备注可自留）

编号 资产编码 文件路径 对应标签
图1 小夜_正 assets/人物/小夜/正.png <Subject 1>
图2 阿雾_正 assets/人物/阿雾/正.png <Subject 2>
图3 便利店_夜 assets/场景/便利店/夜.png <Subject 3>
图4 便利店门口_夜 assets/场景/便利店门口/夜.png <Subject 4>
图5 街道_雨 assets/场景/街道/雨.png <Subject 5>

提交前自检

检查项 标准
字段名 六个，全小写，全英文，顺序不可变
六段主体语言 除<d>和画面文字外，全英文
首镜时间戳 [Shot 1]不写时间戳
后续时间戳 At MM:SS.mmm，递增，不超时长
保留标记 只用规范词，不自己发明
overall_soundscape 不重复对白/音乐
non_diegetic_music 不写情绪，只写乐器/速度/动态