# Portfolio 设计上下文 · Chloe

> 供 AI 协作时参考，记录审美偏好、踩坑经验、设计决策。
> 最后更新：2026-04-20

---

## 🎨 审美偏好

### 整体风格
- **克制优雅**，不堆砌，留白要到位
- 参照系：Kinfolk、aristidebenoist.com 风格
- 不喜欢"太商务感"或"太设计感强"的东西，要有一点点**杂志内页感**

### 配色体系
| 角色 | 色值 | 说明 |
|---|---|---|
| 主背景 | `#F7F3ED` | 米色，温暖不刺眼 |
| 主题粉 | `#D4A5A5` | 淡粉，点缀色 |
| 深茄紫 | `#1E1118` | 舞蹈板块底色 |
| 近黑 | `#111111` | 摄影板块底色 |
| 深墨蓝 | `#0F1318` | 旅行板块底色 |
| 旅行蓝字 | `#A8B8C4` | 淡蓝灰，旅行板块强调色 |
| 摄影米白 | `#E8E0D5` | 摄影板块文字色 |

- **不要纯黑**（`#000000`），用带色彩倾向的深色代替
- 深色模块的颜色要来自整体 palette，不要突兀
- 标签字体用深色（`#2E3A42`），背景用半透明色块+细边框

### 字体
- **英文大标题**：Bodoni Moda，斜体（`font-style: italic`），字重 900
- **英文正文/说明**：Cormorant Garamond，字重 300，斜体
- **中文**：系统默认衬线或无衬线
- 字号要**优雅小巧**，不要撑满，宁可小一点

### 组件偏好
- **三扇门**：flex 布局（非 grid），hover 时伸缩动效（`flex: 1.35`），卡片有 `border-radius: 6px`，有 `gap: 0.8rem`
- **标签胶囊**：`border-radius: 20px`，半透明背景 + 细边框，字体深色，国旗 emoji + 地名
- **瀑布流**：CSS `columns: 2`，图片保持原比例不裁剪
- **摄影画廊**：左大图（黑底 contain）+ 右竖向缩略图轨道（90px 宽）

---

## ⚠️ 踩坑记录（必看）

### 1. CSS 选择器太宽泛 → 全页样式污染
**问题**：写 `.gallery-v2-main img { ... }` 没有加父级限制，导致页面所有 `img` 都受影响，首页文字消失。  
**教训**：所有组件内的元素选择器必须加父级前缀，例如 `.photo-gallery-v2 .gallery-v2-main img`。

### 2. grid 布局无法做 hover 伸缩动效
**问题**：三扇门用 `display: grid; grid-template-columns: 1fr 1fr 1fr` 无法实现 hover 展开效果。  
**教训**：需要伸缩动效的并排卡片一律用 `display: flex`，每个子项 `flex: 1`，hover 时改 `flex` 值。

### 3. 预览和正文代码不同步
**问题**：在独立预览文件（`door-preview-v2.html`）里调好的样式，合并回主文件时漏掉关键属性（如 flex 布局、gap、border-radius），导致效果完全不同。  
**教训**：合并前必须逐项核对：布局方式、尺寸、颜色、动效，不能只改颜色忽略结构。

### 4. 图片 URL 特殊字符编码
**问题**：中文文件名需要 URL encode，例如 `摄影.JPG` → `%E6%91%84%E5%BD%B1.JPG`。  
**教训**：上传图片用英文/拼音命名更稳妥；中文名必须手动或脚本编码后再写入 HTML。

### 5. 背景图片和纯色底冲突
**问题**：三扇门同时设置了背景图片和背景色，图片的暖黄色和整体米色系风格不搭。  
**解决**：去掉背景图片，改用纯深色背景，文字颜色从主 palette 取色，反而更统一。

### 6. 高度单位用 vh 导致内容截断
**问题**：摄影画廊用 `height: 100vh` 没减去导航栏高度，内容被遮住。  
**教训**：固定高度容器要用 `calc(100vh - Npx)` 减去所有固定层（nav + inner-tab + header）。

---

## 📁 仓库结构

| 仓库 | 用途 | Pages URL |
|---|---|---|
| `chengsiyu-web/Portfolio` | 主 portfolio 网页 + 图片资源 | `https://chengsiyu-web.github.io/Portfolio/` |
| `chengsiyu-web/Chloe-s-demo` | 各项目展示页 | `https://chengsiyu-web.github.io/Chloe-s-demo/` |

**项目链接：**
- StageShare: `https://chengsiyu-web.github.io/Chloe-s-demo/stageshare/index.html`
- JoyOps: `https://chengsiyu-web.github.io/Chloe-s-demo/JoyOps/index.html`
- 微信读书AI: `https://chengsiyu-web.github.io/Chloe-s-demo/Weread/index.html`

**本地工作文件：**
- 主文件：`/home/node/.openclaw/workspace/portfolio-index-clean.html`

---

## 🖼 图片资源清单（Portfolio 仓库）

| 文件名 | 用途 | 状态 |
|---|---|---|
| `IMG_5125 2.JPG` | About 页个人照 | ✅ |
| `IMG_2594.JPG` | 舞蹈瀑布流 | ✅ |
| `路演1.JPG` / `路演2.JPG` / `路演3.JPG` | 舞蹈瀑布流 | ✅ |
| `摄影.JPG` | 摄影画廊 | ✅ |
| `摄影:日本-大阪.JPG` | 摄影画廊 | ✅ |
| `IMG_4759.JPG` | 摄影画廊/旅行（意大利罗马） | ✅ |
| `威尼斯.JPG` / `威尼斯3.JPG` / `威尼斯4.JPG` | 旅行瀑布流 | ✅ |
| `西班牙.JPG` / `西班牙1.jpg` / `西班牙2.jpg` | 旅行瀑布流 | ✅ |
| `米兰.JPG` | 旅行瀑布流 | ✅ |
| `匈牙利.JPG` / `匈牙利2.JPG` | 旅行瀑布流 | ✅ |
| `香港-中环.JPG` / `香港-兰桂坊.JPG` / `香港-坚尼地城.JPG` / `香港1.JPG` | 旅行瀑布流 | ✅ |
| `冰岛.JPG` | ❌ 无法加载，已从旅行删除 | 跳过 |
| `日本.JPG` | ❌ 无法加载，已从旅行删除 | 跳过 |

---

## ✅ 已完成功能

- [x] About 页个人照
- [x] 三扇门：flex 布局 + hover 伸缩 + 三色深色配色（无背景图）
- [x] 舞蹈板块：瀑布流（IMG_2594 + 路演1/2/3）
- [x] 旅行板块：瀑布流 + 国旗胶囊标签（蓝色底+深色字）
- [x] 摄影板块：左大图 + 右缩略图轨道分栏画廊
- [x] Lightbox 全屏放大
- [x] 三个项目链接修复（404 → 200）

## 🔜 待完善

- [ ] 摄影板块：继续上传更多摄影作品
- [ ] About 页：替换照片占位符为真实照片（用户自行操作）
- [ ] Portfolio 页面整体移动端适配
