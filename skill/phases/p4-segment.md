# P4 段级分镜与音频一体 — 每段一个 md 文件

## 核心理念

**段（segment）= 视频模型一次生成 = 15 秒 = 5–6 镜。**

每段一个 md 文件，打开即读完这段的全部内容：镜头表 + H3 提示词 + 豆包提示词 + TTS 配音。

**音频不单独切块**：声景和配乐本来就是 H3（`overall_soundscape` / `non_diegetic_music`）和豆包（“全程声景...配乐...”）提示词的内嵌字段，跟着视频提示词一起复制。TTS 配音脚本最后单列（因为它是后期贴音频用的，不属于视频生成）。

## 输入

- P1 剧本（4 段 × 5–6 beat）
- P2 global_anchor
- P3 manifest + 人物/场景卡

## 落盘结构

```
04_段卡/
├── 总览.md              # 全片索引 + 配音对齐总表
└── 第一集/
    ├── E01-01.md        # 0-15s，一个文件含全部
    ├── E01-02.md        # 15-30s
    ├── E01-03.md        # 30-45s
    └── E01-04.md        # 45-60s
```

多集时自然扩展为 `第二集/E02-01.md`...

## 单个 E01-XX.md 文件结构

```markdown
# E01-01 段卡（0-15s）

## 一、元数据

- 场景 / 光线 / 情绪弧 / 出场角色 / blocking

## 二、镜头表

| Shot | 时刻 | 景别 | 运镜 | 画面 | 引用资产 | 台词 |

## 三、H3 提示词（直接复制到 Hailuo）

subject_definitions:
<Subject 1> is [角色名], whose face and outfit come from <Picture 1>.
<Subject 2> is [角色名], whose face and outfit come from <Picture 2>.
<Subject 3> is [场景名], whose layout and lighting come from <Picture 3>.
[按实际引用资产增删行。仅作身份/风格来源的图片，写进 Subject 定义里，不单独建行。]

summary:
[reference generation] [一句话概括目标视频。]

retention_analysis:
<Subject 1> (appears in [Shot k], [Shot k]): fully_preserved - [保留了什么]。
<Subject 2> (appears in [Shot k]): fully_preserved - [保留了什么]。
[每个标签一行。标记只用：fully_preserved / partially_preserved / attribute_transfer / weak_reference]

detailed_description:
[1–2 句整体风格声明。]

[Shot 1] [画面、主体、环境、动作、运镜、声音。不写时间戳。]
[Shot 2] At 00:03.000, the camera cuts to [内容]。
[Shot 3] At 00:06.000, the camera cuts to [内容]。
[有台词时：<Subject N> (S1) says, <d>[Chinese] 台词。</d>]

overall_soundscape:
[1–4 句英语，只写环境声、物理动作声、非语言人声。]

non_diegetic_music:
[1–3 句英语，只写配乐乐器、速度、节奏、动态。无配乐写 N/A。]

## 四、豆包/Seedance 提示词（直接复制到即梦）

@编码1 @编码2 ...

【镜头1】
焦距：...
机位：...
构图：...
运镜：...
景别：...
画面：...
台词：{}
视线落点：...
焦点：...
稳定性：...

【镜头2】
...

<环境音>
（配乐）

【约束】画面无字幕，不要生成任何文字或字幕

## 五、配音脚本（TTS 用）

| Shot | 说话人 | 台词 | TTS 提示词 |
```

## Gate4

- [ ] 恰好 4 段，每段 15s，总 60s
- [ ] 每段 5–6 镜，每镜 2–4 秒
- [ ] 六段字段齐全且顺序正确：`subject_definitions` → `summary` → `retention_analysis` → `detailed_description` → `overall_soundscape` → `non_diegetic_music`
- [ ] 六段主体除 `<d>` 内台词/歌词和双引号内画面文字外，无中文
- [ ] `[Shot 1]` 无时间戳；后续时间戳递增且不超段长
- [ ] `retention_analysis` 只使用规范标记（`fully_preserved` 等）
- [ ] `overall_soundscape` 未重复对白/音乐
- [ ] `non_diegetic_music` 未写抽象情绪词
- [ ] 豆包提示词末尾含“全程声景……配乐……”
- [ ] 豆包 `@编码` 都在 `manifest.md` 注册
- [ ] 全片配音对齐总表在 `总览.md`
