# 📐 单镜 JSON Schema（P4 机读版）

每镜一个文件 `shots/shot_<NN>.json`。P5 读这个文件，分别生成豆包版和 H3 版提示词。

## 字段定义

```json
{
  "shot_id": "S01_03",
  "segment": 1,
  "segment_name": "教室_开学",

  "duration_sec": 3,
  "framing": "MCU",
  "camera": "slow_push_in",

  "characters": ["林小雨"],
  "scene": "教室_白天",
  "action": "林小雨侧脸靠窗，阳光打在脸上，睫毛轻颤",
  "dialogue": {
    "speaker": "李凡",
    "line": "苏晴，全校公认的女神……",
    "type": "voiceover"
  },

  "difficulty": "green",
  "fallback": null,

  "image_prompt_zh": "[由 P4 生成，已拼 global_anchor]",
  "image_prompt_en": "[...]",
  "image_refs": ["assets/人物/林小雨/校服_正面.png", "assets/场景/教室_白天.png"],

  "video_prompt_doubao": "[由 P5 生成]",
  "video_prompt_minimax_h3": "[由 P5 生成]",

  "sfx": "校园嘈杂底噪",
  "transition_out": "cut"
}
```

## 枚举值

| 字段 | 取值 |
|---|---|
| `framing` | ELS / LS / FS / MS / MCU / CU / ECU |
| `camera` | fixed / slow_push_in / slow_pull_out / slow_pan / slow_orbit / handheld |
| `difficulty` | green / yellow / red / blocked |
| `dialogue.type` | voiceover / diegetic / none |
| `transition_out` | cut / dissolve / fade_to_black / match_cut |

## 硬校验（P4 Gate4 必查）

- [ ] `duration_sec` 在 1.5–4 之间
- [ ] 同 segment 内镜头数 = 5 或 6
- [ ] 同 segment 内 `duration_sec` 求和 ≤ 15
- [ ] 全片 4 个 segment，总时长 57–63 秒
- [ ] 每镜 `image_prompt_zh` 开头都拼了 `global_anchor.zh`
- [ ] `difficulty=red/blocked` 的镜必须有 `fallback` 字段
