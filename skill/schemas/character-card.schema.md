# 👤 人物资产卡 Schema（P3 产物）

> 半自动模式：本卡片**不生成图**，只产出可直接粘到文生图工具的提示词包。
> **资产编码规则**：`<角色全名>_<变体>`，例 `林小雨_正`。编码必须在 `manifest.md` 注册。

## 字段

```yaml
name: 林小雨
asset_id: 林小雨          # 编码前缀，变体拼在后面
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

# 资产清单（每条对应 manifest.md 一行）
assets:
  - code: 林小雨_正
    file: assets/人物/林小雨/正.png
    desc: 校服正面
  - code: 林小雨_侧
    file: assets/人物/林小雨/侧.png
    desc: 校服侧面
  - code: 林小雨_笑
    file: assets/人物/林小雨/笑.png
    desc: 微笑表情
  - code: 林小雨_哭
    file: assets/人物/林小雨/哭.png
    desc: 哭泣表情

prompts:
  林小雨_正: |
    {global_anchor_en}
    {consistency_keywords.en}, school uniform, front view, facing camera,
    white background, character sheet, masterpiece, best quality, 8K.
  林小雨_侧: |
    {global_anchor_en}
    {consistency_keywords.en}, school uniform, side view, profile,
    white background, character sheet.
  林小雨_笑: |
    {global_anchor_en}
    {consistency_keywords.en}, gentle smile, looking at viewer.
  林小雨_哭: |
    {global_anchor_en}
    {consistency_keywords.en}, teary eyes, trembling lips, looking down.
```

## 规则

1. 每个主角至少出 `林小雨_正 / 林小雨_侧 / 林小雨_笑` 三条
2. 所有提示词**第一行必须是 `{global_anchor_en}`**（占位符，P4 生成时替换成真实锚定词）
3. `consistency_keywords.en` 是后续每镜图片提示词必须复用的"身份证"
4. 配角只需要 `<角色>_正` 一条
5. **每条 prompt 的 key 必须是资产编码**，与 `assets[].code` 一一对应
