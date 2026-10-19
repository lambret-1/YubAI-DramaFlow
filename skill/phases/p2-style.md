# P2 风格层 — 生成全局风格锚定词

## 输入

- `01_故事/大纲.md` 的 `tone`（全片基调，P1 产物）
- P1 的剧本（知道题材和故事类型）
- 用户选的风格族（日漫 / 美漫 / 韩漫 / CG / 仿真人 / 国风 / 水彩）

## 做什么

1. 让用户从风格族里选一个。
2. 按 `schemas/style-anchor.schema.md` 生成完整字段：`genre`、`tone`、`visual`（`main_style / color_palette / texture / reference_artist`）、`anchor_zh`、`anchor_en`、`negative`。
3. 给出 **3 条候选锚定词**，每条都是完整的 `anchor_zh` + `anchor_en` + `negative`，让用户挑一条或自己改。
4. **半自动模式**：不生成测试图，只产出“测试图提示词”让用户自己跑，回填选定结果。
5. 定稿时写入 **版本号**（`v1`），后续要改必须升版本号（`v2`），并注明“改锚定词需重出全片”。

## 产物

- `02_风格/风格定义.md`，必须包含以下字段：
  - `project_name`
  - `genre`
  - `tone`（与 P1 大纲一致）
  - `visual.main_style`
  - `visual.color_palette`
  - `visual.texture`
  - `visual.reference_artist`
  - `anchor_zh`（20–50 个汉字）
  - `anchor_en`（20–50 个英文关键词，逗号分隔）
  - `negative`（必须含 `low quality` / `deformed` / `watermark` / `text`）
  - `version`（`v1` / `v2` ...）
  - `test_images`（用户回填的测试图路径，可为空）
- 3 条候选测试图提示词（让用户去外部工具跑）
- `02_风格/候选锚定词.md`（3 条候选，含各自 `anchor_zh` / `anchor_en` / `negative`）

## Gate2

- [ ] 用户已从 3 条候选中确认一条 anchor（或自己改后确认）
- [ ] `anchor_en` 长度 20–50 词
- [ ] `anchor_zh` 长度 20–50 个汉字
- [ ] `negative` 含 `low quality` / `deformed` / `watermark` / `text`
- [ ] `02_风格/风格定义.md` 已包含 schema 全部字段
- [ ] `tone` 与 `01_故事/大纲.md` 一致
- [ ] 已写入 `version` 版本号
- [ ] 3 条候选测试图提示词已产出（不要求用户已跑完；跑完则回填 `test_images`）
