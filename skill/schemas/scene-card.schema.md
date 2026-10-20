# 🏞️ 场景资产卡 Schema（P3 产物）

> 半自动模式：本卡片**不生成图**，只产出可直接粘到文生图工具的提示词包。
> **资产编码规则**：`<场景名>_<时段>`，例 `便利店_夜晚`。编码必须在 `manifest.md` 注册。

## 字段

```yaml
name: 便利店
asset_id: 便利店          # 编码前缀，时段拼在后面
location: 街角
indoor: true

layout:
  - 进门左手是货架，右手是收银台
  - 深处有冷藏柜，天花板贴满促销海报

lighting:
  main: 日光灯冷白，收银台区域暖黄
  atmosphere: 夜晚店内外温差玻璃起雾

color_palette: 冷白主调 + 暖黄点缀

texture: 真实材质，塑料货架 + 玻璃门 + 瓷砖地面

# 资产清单（每条对应 manifest.md 一行）
assets:
  - code: 便利店_夜晚
    file: assets/场景/便利店/夜晚.png
    desc: 夜间便利店全景，暖光从玻璃门透出
  - code: 便利店_白天
    file: assets/场景/便利店/白天.png
    desc: 白天店内自然光，顾客稀少
  - code: 便利店_黄昏
    file: assets/场景/便利店/黄昏.png
    desc: 黄昏时分，夕阳从门外斜射进来

prompts:
  便利店_夜晚: |
    {anchor_en}
    convenience store interior at night, rows of shelves, glass door entrance,
    fluorescent ceiling lights, warm yellow counter light, tiled floor,
    wide establishing shot, no people, empty scene, masterpiece, best quality, 8K.
  便利店_白天: |
    {anchor_en}
    convenience store interior in daytime, natural light from glass windows,
    shelves fully stocked, clean floor, wide shot, no people, masterpiece, 8K.
  便利店_黄昏: |
    {anchor_en}
    convenience store interior at dusk, sunset light streaming through glass door,
    warm golden rays across tiled floor, shelves on both sides, wide shot, no people, masterpiece, 8K.
```

## 规则

1. 每个场景至少出 **1 个主时段**（该场景在全片中实际出现的时段）；可选出 2–3 个时段变体
2. 所有提示词**第一行必须是 `{anchor_en}`**（占位符，P4 生成时替换成真实锚定词）
3. 场景提示词默认 **no people**，人物在 P4 视频生成时单独叠加
4. **每条 prompt 的 key 必须是资产编码**，与 `assets[].code` 一一对应
5. `layout` 和 `lighting` 是给 H3 `subject_definitions` 里 `whose layout/lighting comes from <Picture N>` 用的描述依据
