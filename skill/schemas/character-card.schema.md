# 👤 人物资产卡 Schema（P3 产物）

> 半自动模式：本卡片**不生成图**，只产出可直接粘到文生图工具的提示词包。
> **资产编码规则**：`<角色全名>`，例 `林小雨`。编码必须在 `manifest.md` 注册。
> **三视图标准**：每个角色只出 **1 张三视图图**（character sheet），图内同时包含正面全身、侧面全身、背面全身三个视角。

## 字段

```yaml
name: 林小雨
asset_id: 林小雨          # 编码即角色名，无变体后缀
role: 女主
age: 16
identity: 高中生

face:
  face_shape: 鹅蛋脸
  eyes: 大圆眼，浅棕色
  eyebrows: 自然平眉
  marks: 左眼下方一颗泪痣

hair:
  color: 黑色
  length: 及肩
  style: 微卷，扎低马尾

body: 纤细，162cm

outfits:
  - name: 校服
    desc: 白色衬衫，蓝白百褶裙，红色领结
  - name: 居家
    desc: 浅粉色卫衣，牛仔裤

consistency_keywords:
  en: "lin xiaoyu, 16yo, oval face, large brown eyes, tear mole under left eye, black shoulder-length hair, fair skin"
  zh: "林小雨，16岁，鹅蛋脸，棕色大眼，左眼泪痣，黑色及肩发，白皙"

# 资产清单（每个角色 1 张三视图图）
assets:
  - code: 林小雨
    file: assets/人物/林小雨/三视图.png
    desc: 校服三视图（正面/侧面/背面全身）

prompts:
  林小雨: |
    {anchor_en}
    {consistency_keywords.en}, school uniform,
    character sheet, three views: front view, side view, back view,
    full body, white background, standing pose,
    masterpiece, best quality, 8K.
```

## 规则

1. 每个角色只出 **1 张三视图图**（front + side + back 在同一张图里），不多出
2. 所有提示词**第一行必须是 `{anchor_en}`**（占位符，P4 生成时替换成真实锚定词）
3. `consistency_keywords.en` 是后续每镜图片提示词必须复用的"身份证"
4. **prompt 的 key 必须是资产编码**，与 `assets[].code` 一一对应
