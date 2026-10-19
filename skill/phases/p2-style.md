# P2 风格层 — 生成全局风格锚定词

## 输入
- P1 的剧本（知道题材和基调）

## 做什么
1. 让用户从风格族里选：日漫 / 美漫 / 韩漫 / CG / 仿真人 / 国风 / 水彩
2. 生成 `anchor_zh` / `anchor_en` / `negative`（结构见 `schemas/style-anchor.schema.md`）
3. 给出 3 条候选锚定词，让用户挑一条或自己改。
4. **半自动模式**：不生成测试图，只产出"测试图提示词"让用户自己跑，回填选定结果。

## 产物
- `02_风格/风格定义.md`（含 global_anchor 三件套）
- 3 条候选测试图提示词（让用户去外部工具跑）

## Gate2
- [ ] 用户已确认一条 anchor
- [ ] anchor_en 长度 20–50 词
- [ ] negative 含 `low quality / deformed / watermark / text`
- [ ] 用户已在外部跑出满意的测试图（或明确说"先跳过，后面再说"）
