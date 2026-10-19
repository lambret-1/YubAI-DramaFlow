# P4 分镜层 — 分镜表 + 每镜 JSON

## 输入
- P1 剧本（4 段 × 5–6 beat）
- P2 global_anchor
- P3 人物/场景卡

## 做什么
1. 把剧本 beat 表转成 shot 表。**每段必须 5–6 镜，每镜 1.5–4 秒，段总时长 ≤ 15 秒。**
2. 每镜生成：
   - `image_prompt_zh/en`（拼 anchor + consistency_keywords + 场景）
   - `difficulty` 评级
   - `video_prompt_doubao` 草稿（P5 精修）
   - `video_prompt_minimax_h3` 草稿（P5 精修）
3. 对 🔴/⛔ 镜头强制写 `fallback`（例：打斗 → 拔剑特写 + 音效）。
4. 同时输出人读版 `分镜表.md` 和机读版 `shots/shot_XX.json`。

## 产物
- `04_分镜/分镜表.md`
- `04_分镜/shots/shot_01.json … shot_22.json`（见 `schemas/shot.schema.md`）

## Gate4（硬校验）
- [ ] 4 个 segment，每段 5–6 镜
- [ ] 每段时长和 ≤ 15s，总时长 57–63s
- [ ] 每镜 image_prompt 已拼 global_anchor
- [ ] 所有 red/blocked 镜有 fallback
- [ ] 景别分布：特写 40% / 中景 30% / 全景 30%（±10%）
