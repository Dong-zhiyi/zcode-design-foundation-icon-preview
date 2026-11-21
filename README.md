# 图标预览页 · design-foundation

一个自包含的静态页面，用来在浏览器里**跨库对比 design-foundation 推荐的 11 个图标库**：同一个图标概念在 11 个库里的形状并排看，看清了再选，选定后再落地。

- **在线地址（GitHub Pages）**：https://dong-zhiyi.github.io/zcode-design-foundation-icon-preview/
- **所属项目**：design-foundation（设计基座）· 平台 / 技术栈 / 风格 / 架构 / 字体 / 图标的选型工作流
- **插件集成**：ZCode 插件 `design-foundation` 的配置项 `icon_preview_url` 填上面那个地址即可

> 页面是单文件的：内联 CSS 与 JS，无构建步骤，`index.html` 一个文件（约 200KB，含 372 个预置图标的 SVG 本体）即可部署。
> 预置图标零网络、断网可用；搜索和未预置图标运行时来自 Iconify API（api.iconify.design），有 localStorage 跨会话缓存。

---

## 页面能力

| 能力 | 说明 |
|---|---|
| **35 组常用图标跨库对比** | home / search / user / ticket / cart / bell / settings 等 35 个概念 × 11 个库 = 372 个图标位，构建期已逐一核实命名；**SVG 本体已内嵌进页面（142KB），预置区零网络、断网可用、秒开** |
| **关键词搜索** | 支持中文（内置 70+ 词映射：票→ticket、会员→vip member…）和英文，调 Iconify search API 跨库搜索，按选中库过滤；**搜过的图标进 localStorage 跨会话缓存，下次离线也能看** |
| **弱网自愈** | 非预置图标受控并发拉取（4 路，防触发限流）+ 三域名自动轮换 + 进视口才加载；连续失败自动熔断（不再挂转圈），后台每 8s 探测网络，**恢复后自动重载全部失败图标**；失败卡片有 ↻ 可手动重试，顶部横幅可一键重试全部 |
| **库筛选** | 11 个库 chip 开关，只看关心的库 |
| **尺寸滑块** | 16–64px 实时切换（CSS 变量驱动，零重新请求） |
| **颜色切换** | 墨黑 / 剧院红 / 金 / Linear 紫 / 绿 / 蓝 + 自定义取色器 |
| **详情弹层** | 点任意卡片：96px 大图 + 16/20/24/32/48 五档尺寸 + **复制 SVG 源码**（IconPark 品牌蓝已在构建期归一为 currentColor）+ 复制图标名 + 官方页跳转 |
| **库信息卡** | 11 个库的图标数、许可证、风格适配建议、官网链接、Iconify 前缀 |

## 覆盖的 11 个库

| 库 | Iconify 前缀 | 数量 | 许可 |
|---|---|---|---|
| Lucide | `lucide` | ~2,092 | ISC |
| Tabler Icons | `tabler` | ~6,545 | MIT |
| Phosphor | `ph` ⚠️ | ~9,072 | MIT |
| Heroicons | `heroicons` | ~1,288 | MIT |
| Bootstrap Icons | `bi` | ~2,078 | MIT |
| Remix Icon | `ri` | ~3,188 | Apache-2.0 |
| IconPark | `icon-park` | ~2,658 | Apache-2.0 |
| Octicons | `octicon` | ~986 | MIT |
| Fluent UI Icons | `fluent` | ~20,894 | MIT |
| Iconoir | `iconoir` | ~2,020 | MIT |
| Radix Icons | `radix-icons` | ~345 | MIT |

全部免费可商用。

## 快速开始

### 本地预览

**方式一：直接双击 `index.html`** —— 页面、预置对比网格（SVG 已内嵌，零网络）、详情、库信息全部可用且**断网也能用**；搜索新关键词需要网络（Iconify API），搜过的会缓存。部署到任意静态服务器也一样用。

**方式二：起个本地服务（推荐）**

```bash
cd zcode-design-foundation-icon-preview
python -m http.server 8902
# 打开 http://localhost:8902/
```

### 部署

整个目录上传到任意静态服务器即可（GitHub Pages / Vercel / 自有服务器）。部署后把地址填进插件配置项 `icon_preview_url`。

### GitHub Pages

仓库推到 GitHub 后，Settings → Pages → 选分支根目录即可。

---

## 数据来源与 API 说明

- **API**：`https://api.iconify.design`（Cloudflare，国内可达，2026-11 实测）
- **备用域名**：`api.simplesvg.com`、`api.unisvg.com`（页面内置自动回退）
- **搜索端点**：`GET /search?query={kw}&limit=64`
- **SVG 端点**：`GET /{prefix}/{name}.svg?height={n}&color={hex}`
- **元数据端点**：`GET /collections?prefixes={...}`

### 已知的三个坑（页面与文档均已标注）

1. **Phosphor 前缀是 `ph` 不是 `phosphor`**，图标名小写 + 权重后缀（`ticket-bold`、`ticket-fill`…）
2. **同一名词各库名字不同**：ticket / ticket-2-line / ticket-perforated / ticket-24-regular
3. **搜索索引不全**：phosphor、icon-park、fluent 对部分关键词搜不到（预置区已用全量图标名列表核实，不受影响）；Octicons / Radix / Iconoir 集合小，缺图常见

### IconPark 的品牌蓝

IconPark 的 SVG 自带硬编码填充色 `fill="#2F88FF"`（不受 color 参数影响），所以网格里它显示蓝色。详情弹层里**复制 SVG 时会自动替换为 `currentColor`**，落地到 Figma 后可正常绑定语义色。

---

## 与插件的关系

- `design-foundation` 插件的 `references/libraries/icon-search.md` 定义了完整的「搜索 → 预览 → 选定 → 落地」工作流；本页是该工作流的**图形化预览端**。
- 插件配置项：
  - `icon_preview_url`：本页部署地址（选图标时 ZCode 会展示）
  - `font_preview_url`：字体样张页地址（姊妹工具，见 `zcode-design-foundation-font-preview/`）

## 更新预置数据

预置的 35 组 × 11 库图标命名映射来自构建期核实（每个库的完整图标名列表逐一比对）。库升级后如需刷新：

1. 重新拉各库图标名列表（Iconify API `/collection?prefix=` 或 npm `@iconify-json/{prefix}` 的 icons.json）
2. 跑 `_work/icon-preview-build/match_presets.py` 重新匹配
3. 把输出的 `presets.json` 内容替换进 `index.html` 的 `const PRESETS = ...`
