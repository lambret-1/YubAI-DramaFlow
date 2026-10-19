# 🎨 风格锚定词 Schema（P2 产物，全局唯一）

> 这是整个项目的"视觉身份证"。所有图片提示词**开头必须拼接**这段。

## 结构

```yaml
project_name: <项目名>
genre: 青春校园 | 古风 | 都市 | 科幻 | 搞笑 | 悬疑
tone: 轻松 | 治愈 | 热血 | 悬疑 | 悲伤

visual:
  main_style: 日漫 | 美漫 | 韩漫 | CG | 仿真人 | 国风 | 水彩
  color_palette: 明亮温暖 | 暗沉压抑 | 高饱和 | 低饱和
  texture: 平涂 | 厚涂 | 水彩 | 油画
  reference_artist: 新海诚 | 吉卜力 | 皮克斯 | 其他__

anchor_zh: "<20-50 个汉字风格描述>"
anchor_en: "<20-50 个英文风格关键词逗号分隔>"
negative: "blurry, low quality, deformed, 3d render, western cartoon, watermark, text"

test_images:
  - 用户选定的风格测试图路径（用户在外部跑图后回填）
```

## 范例（青春校园日漫）

```yaml
anchor_zh: 日漫风格，青春校园题材，明亮暖色调，细腻人物刻画，柔和逆光，清新氛围，新海诚光影
anchor_en: anime style, high school slice of life, bright warm palette, detailed character, soft rim light, fresh atmosphere, Makoto Shinkai inspired, clean line art, masterpiece
negative: dark, horror, realistic photo, 3D render, western cartoon, rough sketch, low quality, blurry, deformed, ugly face
```

## 规则

1. `anchor_zh/en` 长度控制在 **20–50 词**（太短不稳，太长稀释主体）
2. `negative` 必须包含 `low quality / deformed / watermark / text`
3. 一旦定稿，**禁止在 P3/P4 改写**；要改必须重出全片（锚定词带版本号 v1/v2）
