# 👤 人物资产卡 Schema（P3 产物）

> 半自动模式：本卡片**不生成图**，只产出可直接粘到文生图工具的提示词包。

## 字段

```yaml
name: 林小雨
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

prompts:
  front_view: |
    {global_anchor_en}
    {consistency_keywords.en}, school uniform, front view, facing camera,
    white background, character sheet, masterpiece, best quality, 8K.
  side_view: |
    {global_anchor_en}
    {consistency_keywords.en}, school uniform, side view, profile,
    white background, character sheet.
  back_view: |
    ...
  expression_smile: |
    {global_anchor_en}
    {consistency_keywords.en}, gentle smile, looking at viewer.
  expression_cry: |
    ...
```

## 规则

1. 每个主角至少出 `front_view / side_view / expression_smile` 三个提示词
2. 所有提示词**第一行必须是 `{global_anchor_en}`**（占位符，P4 生成时替换成真实锚定词）
3. `consistency_keywords.en` 是后续每镜图片提示词必须复用的"身份证"
4. 配角只需要 `front_view` 一条
