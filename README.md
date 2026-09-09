# CodeVault Official — 官网

纯静态多页官网（零构建、零依赖），参考 ZPad-official 的站点结构。

> 定位对照：`PRD/` 是产品规范（面向开发），`docs/` 是技术文档（同步协议 / UI spec），**本目录是面向用户的官网**。

## 页面结构

```
CodeVault-official/
├── README.md     ← 本文件
├── index.html    ← 官网首页（Hero、功能、四类型、同步、FAQ 预览）
├── docs.html     ← 使用指南：单页完整手册（侧边目录 + 编号章节 1-9）
├── faq.html      ← 常见问题（基础 / 快捷键与面板 / 数据与安全 / 同步）
└── .nojekyll     ← GitHub Pages 直发标记
```

`docs.html` 章节锚点：`#install` `#first-item` `#quick-panel` `#types` `#clipboard` `#sync` `#self-hosting` `#settings` `#troubleshooting`

## 本地预览

无需构建，直接打开或起本地服务：

```bash
cd CodeVault-official && python3 -m http.server 8000
# http://localhost:8000
```

## 部署

- **GitHub Pages**：Settings → Pages → 选分支与目录（`/CodeVault-official`）。`.nojekyll` 已就位
- **Cloudflare Pages / Vercel / Netlify**：直接指向本目录

## 维护约定

1. **事实以代码为准**，写前先核对源码入口：
   - 快捷键默认值：`CodeVault/Preferences.swift`（快捷面板 `⌘1`）、`Modules/Clipboard/Core/ClipboardConfig.swift`（剪贴板 `⌘2`）
   - 同步行为：`CodeVault/Modules/Sync/SyncService.swift` + `sync-worker/README.md`
   - 功能命名：`CodeVault/Resources/{zh-Hans,en}.lproj/Localizable.strings`
2. **双语规则**：每个页面中英内容成对维护（`data-l="zh"` / `data-l="en"`，CSS 按 `html[data-lang]` 切显隐）。语言初始化：`localStorage('cv-lang')` > 系统语言（`zh*` → 中文，否则英文），头部有切换按钮。改了一处文案必须同步另一语言
3. **英文锚点后缀 `-en`**：docs/faq 的英文区块 id 与 TOC 均带 `-en`（如 `#sync-en`）；中文区块用裸 id。跨语言链接时注意目标区块的锚点
2. **描述当前产品，不描述规划**：PRD 里的 V1.2+ 路线图（五类型体系等）落地前不要写进对外内容
3. **视觉对齐 App**：三页共用同一套 token（accent `#0A84FF`，类型色 code `#4C9FFE` / prompt `#A78BFA` / text `#34D3BE` / key `#F5A623`；暗色 `#1E1E22` / 亮色 `#F5F5F7`，`[data-theme]` 切换，localStorage 键 `cv-theme`）
4. **零依赖**：不引入 CDN 字体/脚本/框架；图标用内联 SVG，无 emoji
5. **页面互链用相对路径 + 锚点**（`docs.html#sync`），指向仓库文件用 GitHub 绝对 URL

## 相关仓库资源

| 资源 | 位置 | 用途 |
|---|---|---|
| 产品规范（PRD） | [`PRD/`](../PRD/README.md) | 产品定义、路线图 |
| 技术文档 | [`docs/`](../docs/) | 同步协议、UI spec |
| 自部署后端 | [`sync-worker/`](../sync-worker/README.md) | Cloudflare Worker 源码与部署手册 |
| 工程规范 | [`AGENTS.md`](../AGENTS.md) | 开发规则（面向贡献者） |
