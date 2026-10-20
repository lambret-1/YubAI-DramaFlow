# 👤 人物资产卡 Schema（P3 产物）

> 半自动模式：本卡片**不生成图**，只产出可直接粘到文生图工具的提示词包。
> **资产编码规则**：`<角色全名>`，例 `小夜`。编码必须在 `manifest.md` 注册。
> **三视图标准**：每个角色只出 **1 张三视图图**（character sheet），图内同时包含正面全身、侧面全身、背面全身三个视角。

## 产物格式（markdown）

```markdown
# 人物卡：<角色名>

## 基础
- asset_id: <角色编码>
- 年龄：<年龄>
- 身份：<身份>
- 体型：<体型描述，身高体重>

## 外貌
- 脸型：<脸型>
- 眼睛：<眼睛描述>
- 眉毛：<眉毛描述>
- 发型：<发型描述>
- 肤色：<肤色>

## 服装
- <主要服装描述>

## consistency_keywords
- en: "<英文身份证关键词，逗号分隔>"
- zh: "<中文身份证描述>"

## 资产与提示词

### <角色编码>
```
{anchor_en}
{consistency_keywords.en},
character sheet, three views: front view, side view, back view,
full body, white background, standing pose,
masterpiece, best quality, 8K.
```
```

## 规则

1. 每个角色只出 **1 张三视图图**（front + side + back 在同一张图里），不多出
2. 所有提示词**第一行必须是 `{anchor_en}`**（占位符，P4 生成时替换成真实锚定词）
3. `consistency_keywords.en` 是后续每镜图片提示词必须复用的"身份证"
