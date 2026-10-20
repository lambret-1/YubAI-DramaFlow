# 单镜头 Schema（P4 段卡内机读版）

> 每镜是段卡 `E01-XX.md` 中镜头表的一行，以及豆包提示词里一个【镜头N】块。
> 不再单独生成 `shots/shot_<id>.json` 文件。

## 字段定义

```json
{
  "shot_id": "E01-01_S03",
  "segment": 1,
  "segment_name": "教室_白天",
  "duration_sec": 3,
  "framing": "MCU",
  "camera": "fixed",
  "characters": ["尚哥"],
  "scene": "教室_白天",
  "action": "尚哥站在教室后排，眼神瞟向前排",
  "dialogue": {
    "speaker": "尚哥",
    "line": "",
    "type": "none"
  },
  "difficulty": "green",
  "fallback": null,
  "image_prompt_zh": "[由 P4 生成，已拼 anchor_zh]",
  "image_prompt_en": "[由 P4 生成，已拼 anchor_en]",
  "image_refs": ["尚哥", "教室_白天"],
  "video_prompt_doubao": "[由 P4 生成，写入段卡【镜头N】块]",
  "video_prompt_minimax_h3": "[由 P4 生成，写入段卡 H3 detailed_description]",
  "sfx": "教室安静底噪",
  "transition_out": "cut"
}
```

## 枚举值

| 字段 | 取值 |
|---|---|
| framing | ELS 大远景 / LS 远景 / MS 中景 / MCU 近景 / CU 特写 / ECU 大特写 |
| camera | fixed 固定 / slow_push_in 缓慢推镜 / slow_pull_out 缓慢拉镜 / handheld 手持跟拍 |
| difficulty | green / yellow / red / blocked |
| dialogue.type | voiceover 旁白 / diegetic 对白 / none 无台词 |
| transition_out | cut 硬切 / dissolve 叠化 / fade_to_black 黑场 / match_cut 匹配剪 |

## image_refs 编码规则

- 人物：直接 `<角色全名>`，例 `尚哥`、`女神`（每个角色对应 1 张三视图图）
- 场景：`<场景名>_<时段>`，例 `教室_白天`、`天台_黄昏`
- 道具：直接 `<道具名>`，例 `信封`
- 每个编码必须在 `03_资产/manifest.md` 注册过

## 硬校验（P4 Gate4 必查）

- [ ] `duration_sec` 在 2–4 之间
- [ ] 同 segment 内镜头数 = 5 或 6
- [ ] 同 segment 内 `duration_sec` 求和 ≤ 15
- [ ] 全片 4 个 segment，总时长 57–63 秒
- [ ] 每镜 `image_prompt_zh` 开头都拼了 `anchor_zh`
- [ ] 每镜 `image_prompt_en` 开头都拼了 `anchor_en`
- [ ] `difficulty` = red / blocked 的镜必须有 `fallback` 字段
- [ ] `image_refs` 中每个编码都在 `manifest.md` 注册
- [ ] `video_prompt_doubao` 和 `video_prompt_minimax_h3` 由 P4 生成，写入段卡对应块，不单独出文件
