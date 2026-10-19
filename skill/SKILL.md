
# drama-studio — 1 分钟 AI 短剧半自动制片工作流

**定位**：不产图、不产视频，只产“可直接复制到文生图 / 图生视频 / TTS 工具的提示词包”。

**来源**：基于 YubAI-DramaFlow 五阶段方法论 + novel-storyboard 段级管线，压缩为 60s 单集流水线。

## 1. 核心约束

| 项 | 约束 |
|---|---|
| 单集总时长 | 60 秒（±3 秒） |
| 段（segment） | 一次视频生成 = 15 秒，全片 4 段 |
| 段内镜头数 | 5–6 个（2–4 秒/镜） |
| 总镜头数 | 4 段 × 5–6 镜 = 20–24 镜 |
| 画面比例 | 默认 9:16 竖屏 |
| 工具调用 | 本 Skill 不调任何图像/视频/TTS 工具，只产出提示词文档 |

## 2. 流水线

```text
P1 故事层 ──► P2 风格层 ──► P3 资产层 ──► P4 段级分镜与音频一体
大纲/剧本      风格锚定词      人物/场景卡      每段一条：镜头表 + H3提示词 + 豆包提示词 + 声景 + 配乐 + 配音
│             │             │             │
Gate1         Gate2         Gate3         Gate4
```

关键变化：P4 不再是“分镜表”，而是“段卡”——以段为单位，把镜头表、双视频提示词、声景、配乐、配音对齐全部打包。因为段才是视频模型一次生成的单位。

3. 入口路由

用户说 进入
“我要做一个 1 分钟短剧，题材是 X” P1，从 templates/project-brief.md 开始
“我已经有剧本了” 跳过 P1，直接进 P2
“风格定过了，下一步呢” 读 project.json，定位 current_phase
“继续上次的项目” 读 project.json 续作

4. 目录结构

```text
projects/<项目名>/
├── project.json              # 状态机
├── 01_故事/
│   ├── 大纲.md
│   ├── 剧本.md
│   └── 可行性评估.md
├── 02_风格/
│   └── 风格定义.md          # 含 global_anchor
├── 03_资产/
│   ├── manifest.md          # 中文编码 → 文件路径
│   ├── 人物/<角色名>.md
│   └── 场景/<场景名>.md
└── 04_段卡/
├── 总览.md              # 全片索引 + 配音对齐总表
└── 第一集/
├── E01-01.md        # 0-15s：元数据+镜头表+H3提示词+豆包提示词+TTS
├── E01-02.md        # 15-30s
├── E01-03.md        # 30-45s
└── E01-04.md        # 45-60s
```

5. project.json

```json
{
  "project_name": "<项目名>",
  "total_duration_sec": 60,
  "ratio": "9:16",
  "current_phase": "p4_segment",
  "phases": {
    "p1_story": {"status": "done"},
    "p2_style": {"status": "done"},
    "p3_assets": {"status": "done"},
    "p4_segment": {"status": "in_progress", "segments_done": 0}
  },
  "global_anchor": {"zh": "...", "en": "...", "negative": "..."}
}
```

6. 视频提示词模板

每段各出一条提示词，不是每镜一条：

模板 参考文档 语法特征
豆包 / Seedance reference/豆包视频提示词模板.md 段级：参考官方模版
MiniMax H3 reference/minimax-h3-多参考模板.md 段级：官方多参考模式六段

H3 六段式语言规则与 Gate4 自检以 phases/p4-segment.md 为准：

· 六段字段顺序不可变：subject_definitions → summary → retention_analysis → detailed_description → overall_soundscape → non_diegetic_music
· 六段主体全英文；仅 <d> 内台词/歌词和英文双引号内画面可见文字可保留中文
· 画内拟声词（如门铃“叮”）在六段主体内必须写英语，如 ding
· [Shot 1] 不写时间戳；后续镜头用 At MM:SS.mmm, the camera cuts to ...
· retention_analysis 只使用 fully_preserved / partially_preserved / attribute_transfer / weak_reference

7. 工作流

· 读用户输入 → 判定入口
· 读 / 初始化 project.json
· 进入对应 phases/p*.md
· 每完成一阶段，更新 project.json.current_phase
· 遇到 Gate 不过，停下来问用户

8. 与原 YubAI-DramaFlow 的差异

原 repo 本 Skill
五阶段自由时长 4 段 × 15 秒固定
分镜表驱动 段卡驱动
H3 用旧版对齐指令 H3 用 Ref2VA 六段式

```
```