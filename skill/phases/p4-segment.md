# P4 段级分镜与音频一体 — 每段一张段卡

## 核心理念
**段（segment）= 视频模型一次生成 = 15 秒 = 5–6 镜。**
不再"每镜一个视频提示词"，而是"每段一条提示词"，内含多镜切点、台词、声景、配乐。

## 输入
- P1 剧本（4 段 × 5–6 beat）
- P2 global_anchor
- P3 manifest + 人物/场景卡

## 做什么

对每一段（E01-01 ~ E01-04），生成一份段卡目录：

### 4.1 段卡.md（元数据 + 镜头表）
```yaml
segment_id: E01-01
time_range: 0-15s
scene: 便利店_夜
lighting: 冷白顶光 + 暖黄货架灯
emotion_arc: 安静 → 微怔
characters_in_shot: [小夜_正, 阿雾_正]

blocking:
  小夜在柜台后（画面左侧）
  阿雾从右侧门口进入
  间距：柜台宽度

shots:
  - shot: 1
    time: 0.0-3.0s
    framing: ELS
    camera: fixed
    action: 雨夜空荡街道，远处便利店暖光透出
    refs: [街道_雨]
    dialogue: null
  - shot: 2
    time: 3.0-6.0s
    framing: MS
    camera: fixed
    action: 小夜在柜台后擦杯子
    refs: [小夜_正, 便利店_夜]
    dialogue: null
  # ... 5-6 镜
```

### 4.2 h3_prompt.md（MiniMax H3 完整提示词）
按 `reference/minimax-h3-多参考模板.md` 段级结构写：
- 首行：对齐指令（参考图编号 = 资产编码）
- `integrated_multimodal_description:` 后逐镜一行 `[Shot k] 时刻: 画面描述`
- 台词逐字进 `<d>[Chinese] …</d>` 块
- `overall_soundscape:` 段级声景
- `non_diegetic_music:` 段级配乐

### 4.3 doubao_prompt.md（豆包/Seedance 提示词）
按 `reference/豆包视频提示词模板.md` 段级结构写：
- 一段连续描述，镜与镜之间用"切："分隔
- 末尾 `@编码` 引用所有参考图
- 注明总时长 15s

### 4.4 audio.md（段级音频）
```yaml
soundscape:
  - 全程雨声底噪
  - 冰箱嗡嗡声（室内段）
  - 门铃"叮"（Shot 3）

music:
  style: 钢琴单音，稀疏，混响大
  volume: 压低，不抢戏
  entry: 淡入
  exit: 持续

voiceover:
  - shot: 8
    speaker: 阿雾
    line: "老样子。"
    tts_prompt: "用20岁女生的气声，偏轻偏慢，念：老样子。"
```

## 产物
- `04_段卡/总览.md`（4 段索引 + 全片配音对齐总表）
- `04_段卡/E01-01/段卡.md`
- `04_段卡/E01-01/h3_prompt.md`
- `04_段卡/E01-01/doubao_prompt.md`
- `04_段卡/E01-01/audio.md`
- （E01-02 ~ E01-04 同结构）

## Gate4
- [ ] 恰好 4 段，每段 15s，总 60s
- [ ] 每段 5–6 镜，每镜 2–4 秒
- [ ] 每段 H3 提示词含 `[Shot k]` 切点时刻，时刻与镜头表对齐
- [ ] 每段台词逐字进 `<d>` 块
- [ ] 每段有 `overall_soundscape` 和 `non_diegetic_music`
- [ ] 每段豆包提示词含 `@编码`，编码都在 manifest 注册
- [ ] 每段 audio.md 有 TTS 提示词（本段无台词则标"无"）
- [ ] 全片配音对齐总表在 `总览.md`
