+++
date = '2026-04-12T14:00:59+08:00'
draft = false
title = '“屿”SKU设计概念图与品牌宣传视频：AI工具与方法指南'
tags = ["屿"]
categories = ["奥德赛拾光"]
summary = "日常生活中的一座孤岛，5分钟的绝对自我时刻。" 
+++

# “屿”SKU设计概念图与品牌宣传视频：AI工具与方法指南

以下是针对“屿”品牌需求，从图像生成到视频制作的完整AI工具链和方法论。


## 一、SKU设计概念图生成

### 1.1 核心工具对比

| 工具 | 适合场景 | 优势 | 劣势 | 费用 |
| :--- | :--- | :--- | :--- | :--- |
| **Midjourney** | 氛围图、产品渲染、场景图 | 审美最好，光影质感强 | 需Discord操作，对中文不友好 | $10-60/月 |
| **DALL·E 3**（ChatGPT Plus） | 精准控制、文字渲染 | 理解复杂指令，可生成中文 | 艺术感略弱 | $20/月 |
| **Stable Diffusion** | 高精度控制、批量生成 | 开源免费，可本地运行 | 学习曲线陡峭 | 免费 |
| **Leonardo.ai** | 产品图、电商图 | 免费额度大，有产品模板 | 质感不如Midjourney | 有免费版 |
| **Playground v2** | 快速迭代 | 完全免费，界面友好 | 细节控制弱 | 免费 |

### 1.2 推荐工作流：Midjourney + DALL·E 3 组合

```
草稿阶段（DALL·E 3）→ 快速出图，验证构图和色彩
精修阶段（Midjourney）→ 出最终图，提升质感和光影
局部修改（Photoshop AI）→ 微调细节
```

### 1.3 具体操作指南

#### 方法一：Midjourney生成SKU概念图

**步骤1：编写提示词（Prompt）**

以“雨林与海”为例，这是经过优化的提示词：

```
/imagine a handcrafted artisan soap bar, 8cm x 6cm x 3cm, rounded square shape with slightly uneven hand-cut edges, color is deep muted green (60%) mixed with off-white (30%) marble pattern, tiny dark green seaweed flakes visible on surface, placed on a wet dark grey coastal rock, background is blurred ocean waves and mist, cold natural lighting, moody atmosphere, cinematic, photorealistic, 8K, product photography style, no text, no logo --ar 4:3 --style raw --stylize 250
```

**参数说明**：
| 参数 | 作用 |
| :--- | :--- |
| `--ar 4:3` | 宽高比，适合电商详情页 |
| `--style raw` | 减少Midjourney的默认美化，更真实 |
| `--stylize 250` | 控制风格强度（0-1000），数值越低越写实 |

**步骤2：迭代优化**

| 问题 | 解决方法 |
| :--- | :--- |
| 颜色不对 | 添加参考色值，如“color #5C6B4A” |
| 纹理不对 | 添加参考词，如“like waves washing over rocks” |
| 皂体太完美 | 添加“imperfect, handmade, organic shape” |
| 背景太乱 | 添加“minimalist, clean background” |

**步骤3：变体与放大**

- `V1/V2/V3/V4` → 生成当前图的变体
- `U1/U2/U3/U4` → 放大当前图
- `Remix Mode` → 开启后修改提示词生成变体

---

#### 方法二：DALL·E 3生成（ChatGPT Plus）

**提示词示例**（可直接复制）：

```
请生成一张产品摄影图：一块手工香皂，尺寸8×6×3厘米，圆角方形，边缘有不规则的手工切割痕迹。颜色是墨绿色和灰白色的大理石纹，表面有细小的深绿色海藻碎颗粒。放在一块湿漉漉的深灰色岩石上。背景是虚化的海浪和雾气。冷调自然光，电影感，写实风格。不要有文字和logo。比例4:3。
```

**优势**：
- 支持中文，理解自然语言
- 可对话式修改：“把墨绿色调浅一点”、“把海藻碎颗粒放大一点”
- 可生成四宫格进行对比

---

#### 方法三：Stable Diffusion（高精度控制）

**适合场景**：需要精确控制产品形态、批量生成多个角度

**推荐模型**：
- Realistic Vision V5.0（写实产品）
- Product Shot（专门的产品摄影模型）

**工作流**：

```
1. 安装 Automatic1111 WebUI 或 ComfyUI
2. 下载写实模型（Realistic Vision）
3. 使用 ControlNet 控制皂体形状
   - Canny Edge：控制边缘轮廓
   - Depth：控制立体感
4. 生成后使用 Inpainting 修图
```

**ControlNet设置示例**：
```
预处理器：canny
模型：control_v11p_sd15_canny
权重：0.8
起始步：0
结束步：0.8
```

---

### 1.4 三款SKU提示词库（可直接使用）

#### 雨林与海

```
# Midjourney版本
/imagine handcrafted soap bar, 8x6x3cm, rounded square, slightly uneven edges, deep muted green and off-white marble pattern, tiny seaweed flakes, on wet dark grey coastal rock, blurred ocean waves and mist background, cold natural lighting, moody, cinematic, photorealistic, 8K --ar 4:3 --style raw

# DALL·E 3版本
一块手工香皂，8×6×3厘米，圆角方形，边缘不规则。墨绿色和灰白色大理石纹，表面有细小深绿色海藻碎颗粒。放在湿漉漉的深灰色岩石上，背景是虚化的海浪和雾气。冷调自然光，电影感，写实。4:3比例。
```

#### 地衣与火

```
# Midjourney版本
/imagine handcrafted soap bar, 8x6x3cm, rounded square, slightly uneven edges, muted grey-green base with scattered burnt orange speckles, tiny dark grey volcanic rock particles, on dark weathered wood plank next to ash and charcoal, warm low-key lighting, autumn evening mood, cinematic, photorealistic --ar 4:3 --style raw

# DALL·E 3版本
一块手工香皂，8×6×3厘米，圆角方形。灰绿色基底上散落着暗橙色斑点，表面有细小深灰色火山石颗粒。放在深色旧木板上，旁边有灰烬和焦炭。暖调暗光，深秋夜晚氛围，电影感，写实。4:3比例。
```

#### 融雪

```
# Midjourney版本
/imagine handcrafted soap bar, 8x6x3cm, rounded square, slightly melted-looking edges, semi-translucent white base with subtle light grey marbling, tiny dark brown particles and light beige oat flakes visible, in shallow puddle of meltwater on wet earth, cold morning light, melancholic, late winter atmosphere, cinematic, photorealistic --ar 4:3 --style raw

# DALL·E 3版本
一块手工香皂，8×6×3厘米，圆角方形，边缘略薄像融化过。半透明白色基底，有浅灰色细纹，内部可见深褐色细小颗粒和浅米色燕麦片。放在融雪水洼中的湿泥土上。冷调晨光，冬日将尽氛围，电影感，写实。4:3比例。
```

---

### 1.5 从概念图到3D模型（如需多角度展示）

| 工具 | 功能 | 费用 |
| :--- | :--- | :--- |
| **Meshy** | 文字/图片生成3D模型 | 有免费版 |
| **CSM** | 单张图片转3D模型 | 有免费版 |
| **Tripo** | 文字/图片生成3D模型 | 有免费版 |

**工作流**：
```
生成2D概念图（Midjourney）→ 上传到Meshy → 生成3D模型 → 导入Blender渲染多角度
```


## 二、品牌宣传视频生成

### 2.1 核心工具对比

| 工具 | 适合场景 | 优势 | 劣势 | 费用 |
| :--- | :--- | :--- | :--- | :--- |
| **Runway Gen-2/Gen-3** | 图生视频、产品动态 | 画质好，运动自然 | 时长有限（4-10秒） | 有免费版 |
| **Pika Labs** | 产品动画、特效 | 可控性强，有画笔功能 | 画质略弱 | 有免费版 |
| **Kling（可灵）** | 写实视频、人物动作 | 国内可用，中文友好 | 需排队 | 有免费版 |
| **Luma Dream Machine** | 场景视频、运镜 | 运镜流畅 | 生成慢 | 有免费版 |
| **Stable Video Diffusion** | 开源、可本地 | 免费，可训练 | 需GPU | 免费 |
| **HeyGen** | 数字人讲解 | 口型同步好 | 产品展示弱 | 有免费版 |

### 2.2 推荐工作流：组合使用

```
方案A（低成本快速）：
Midjourney生成关键帧 → Runway图生视频 → CapCut剪辑配音

方案B（高质量精细）：
Midjourney生成分镜图 → Runway/Pika生成视频片段 → 
后期拼接（Premiere/DaVinci）→ 调色配音

方案C（纯AI生成）：
Pika文字生成视频片段 → Runway超分 → HeyGen配音
```

### 2.3 具体操作指南

#### 方法一：Runway Gen-2/Gen-3 图生视频

**步骤1：准备关键帧图片**（用Midjourney生成）

以“双手搓揉起泡”为例：

```
/imagine close-up of two hands holding a dark green soap bar, rubbing together, white creamy foam starting to appear between fingers, dark background, cinematic lighting, photorealistic --ar 16:9
```

**步骤2：上传到Runway，设置运动参数**

| 参数 | 设置 | 说明 |
| :--- | :--- | :--- |
| Motion | 3-5（中低） | 运动幅度，太大容易变形 |
| Scale | 2-4 | 缩放幅度 |
| 帧数 | 自动 | 生成4秒视频 |

**步骤3：生成并下载**

**提示**：Runway对静态图的效果最好，动态图容易变形。建议把复杂的动作拆成多个静帧分别生成。

---

#### 方法二：Pika Labs（更适合产品展示）

**优势**：有“画板”功能，可指定运动方向

**操作步骤**：
1. 进入Pika Discord或网页版
2. 上传产品图
3. 输入提示词：
```
slow rotation of the soap bar, water droplets sliding down, soft lighting, cinematic 4k
```
4. 使用“Motion Brush”指定哪些区域运动

---

#### 方法三：Kling（可灵）- 国内用户首选

**优势**：国内可用，中文提示词，生成速度快

**操作步骤**：
1. 访问 kling.kuaishou.com
2. 上传参考图（Midjourney生成的产品图）
3. 输入提示词：
```
一块墨绿色手工香皂放在岩石上，水珠从表面滑落，雾气缓慢飘动，海浪声背景，电影感，4K
```
4. 选择生成时长（5秒或10秒）
5. 等待1-3分钟

---

### 2.4 品牌形象片生成方案（30秒版）

将30秒视频拆解为8-10个独立片段，分别生成后拼接：

| 镜号 | 内容 | 生成工具 | 提示词关键词 |
| :--- | :--- | :--- | :--- |
| 01 | 雾中岛屿 | Runway/ Kling | misty island in the ocean, slow push in |
| 02 | 冷杉枝叶 | Runway | fir branch with dew drops, macro |
| 03 | 岩石上的皂 | Pika | soap on wet rock, water droplets |
| 04 | 双手合握 | Runway | hands holding soap, slow motion |
| 05 | 搓揉起泡 | Runway/Pika | hands rubbing, white foam appearing |
| 06 | 泡沫溢出 | Runway | creamy foam between fingers |
| 07 | 冲洗 | Pika | water washing over hands |
| 08 | 擦干后皮肤 | Runway | dry hand touching skin, subtle shine |
| 09 | 窗边背影 | Kling | person silhouette by window, rain outside |
| 10 | 文字卡 | 后期剪辑 | — |

**成本估算**：
- 免费版额度：约可生成50-100个短视频片段
- 付费版（$15-30/月）：可生成高质量版本

---

### 2.5 配音与音乐生成

| 工具 | 功能 | 费用 |
| :--- | :--- | :--- |
| **ElevenLabs** | AI配音（最自然） | 有免费版 |
| **剪映/CapCut** | 配音+音乐库 | 免费 |
| **Suno** | AI生成背景音乐 | 有免费版 |
| **Udio** | AI生成音乐 | 有免费版 |
| **Artlist** | 版权音乐库 | $199/年 |

**配音生成（ElevenLabs）**：
1. 选择声音：女性，中性，自然（推荐“Rachel”或“Bella”）
2. 输入文案：
```
城市是海。我们是船。屿。不是目的地。是可以抛锚的地方。冷杉和海盐。十秒激活。乳霜泡沫。每日五分钟，回到你的屿。
```
3. 调整语速：0.9x，停顿添加

**背景音乐生成（Suno）**：
```
Prompt: cinematic ambient, slow piano and ocean waves, melancholic, minimal, 60 BPM, key of D minor, no drums
```

---

### 2.6 后期剪辑与调色

| 工具 | 适合 | 费用 |
| :--- | :--- | :--- |
| **剪映/CapCut** | 快速剪辑，有AI功能 | 免费 |
| **DaVinci Resolve** | 专业调色 | 免费版足够 |
| **Premiere Pro** | 专业剪辑 | 订阅制 |

**AI辅助剪辑功能**：
- 剪映：自动踩点、AI字幕、智能调色
- CapCut：文本转语音、自动生成字幕


## 三、低成本快速方案（预算 < 1000元）

### 方案：纯AI生成品牌物料

| 步骤 | 工具 | 费用 | 产出 |
| :--- | :--- | :--- | :--- |
| 1 | ChatGPT Plus | $20 | 生成提示词、脚本 |
| 2 | Midjourney | $10（基础版） | 10张概念图 |
| 3 | Kling（可灵） | 免费 | 5段产品视频 |
| 4 | 剪映 | 免费 | 30秒宣传片 |
| 5 | Suno | 免费 | 背景音乐 |
| **合计** | | **约¥220** | 全套物料 |

**时间估算**：2-3天


## 四、高质量专业方案（预算 5000-10000元）

### 方案：AI辅助 + 人工精修

| 步骤 | 工具 | 费用 | 说明 |
| :--- | :--- | :--- | :--- |
| 1 | Midjourney Pro | $60 | 大量生成筛选 |
| 2 | Runway Gen-3 | $15 | 高质量视频片段 |
| 3 | ElevenLabs | $22 | 专业配音 |
| 4 | Artlist | $199/年 | 版权音乐 |
| 5 | 剪辑师 | ¥2000 | 人工精剪调色 |
| 6 | 设计师 | ¥1000 | 文字卡、Logo动画 |
| **合计** | | **约¥4500** | — |


## 五、快速上手指南（今日可执行）

### 第1步：注册免费工具（30分钟）

| 工具 | 注册地址 | 免费额度 |
| :--- | :--- | :--- |
| Midjourney | midjourney.com | 无免费（需付费$10起） |
| **替代：Leonardo.ai** | leonardo.ai | 每日150积分（约50张图） |
| **替代：Playground** | playground.com | 每日500张免费 |
| Kling | kling.kuaishou.com | 每日66积分 |
| 剪映 | capcut.com | 完全免费 |
| Suno | suno.com | 每日50积分 |

### 第2步：生成第一张概念图（5分钟）

用**Leonardo.ai**（免费）：
1. 注册登录
2. 选择“Image Generation”
3. 粘贴提示词：
```
a handcrafted dark green soap bar on a wet rock, ocean background, moody lighting, product photography, 4K
```
4. 点击生成

### 第3步：生成第一段视频（10分钟）

用**Kling（可灵）**：
1. 访问 kling.kuaishou.com
2. 上传刚才生成的图
3. 点击“图生视频”
4. 等待1分钟

### 第4步：剪辑成片（30分钟）

用**剪映**：
1. 导入生成的视频片段
2. 添加文字：“屿 · 每日五分钟，回到你的屿”
3. 添加音乐（剪映内置）
4. 导出

**30分钟后，你就有了第一版品牌宣传视频。**


## 六、常见问题与解决

| 问题 | 解决方法 |
| :--- | :--- |
| AI生成的皂体形状不对 | 添加“8cm x 6cm x 3cm, rounded square”精确描述 |
| 颜色不够准确 | 使用色值描述如“color #5C6B4A”或上传参考图 |
| 视频中物体变形 | 降低运动幅度，使用更稳定的工具（Runway优于Pika） |
| 生成太慢 | 使用国内工具（Kling、即梦）速度更快 |
| 没有合适的提示词 | 使用ChatGPT生成英文提示词 |
| 视频时长不够 | 多个片段拼接，或使用“extend”功能 |

---

**文档结束**

如需我帮你：
1. **写一套完整的Midjourney提示词库**（针对屿的每个SKU和场景）
2. **制作一个可复用的视频剪辑模板**（剪映/CapCut）
3. **写一个AI视频生成自动化脚本**（批量处理）

请告诉我。