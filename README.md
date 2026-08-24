# FDE-Wiki

## 🌐 在线访问

| 站点 | 地址 |
|---|---|
| 根站点 | <https://fde-wiki.github.io/> |
| 项目页 | <https://zhyese.github.io/fde-wiki/> |

两者内容一致,任选其一。

## ✨ 功能特性

- **中文全文搜索** — 本地搜索内置 CJK 分词(单字 + 双字 bigram),中文精准可搜
- **分章节 Wiki** — 4 篇 → 23 章 → 62 深度专题(按 技术 / 方法 / 能力 三类折叠)+ 附录
- **标签系统** — 每页顶部 `#标签` 五色徽章(行业 / 技术 / 方法 / 能力 / 视角),`/tags` 标签云一键跳转
- **公司索引** — `/companies` 公司云彩色徽章(海外 / 国内双色),点击直达该公司相关章节
- **交叉链接** — 正文「第 N 章 / 专题 X」自动转站内链接(490+ 处)
- **阅读增强** — 顶部阅读进度条、字号记忆、面包屑、阅读时间估算、返回顶部、上一篇 / 下一篇
- **术语悬浮** — 正文术语 hover 显示附录术语表释义
- **四篇导语页**(`/part1`…`/part4`),侧边栏组标题可点
- **暗色模式** + 每页右侧本页目录(H2/H3)

## 🚀 快速开始

```bash
corepack enable  # 首次使用时启用 package.json 固定的 pnpm 10.34.5
pnpm install --frozen-lockfile
pnpm split       # 从 source/ 拆分生成 docs/*.md + 侧边栏/导航/索引(改内容后重跑)
pnpm dev         # 本地预览 http://localhost:5173
```

构建生产版本:

```bash
pnpm build       # 产物在 docs/.vitepress/dist(纯静态)
pnpm preview     # 本地预览构建产物
```

## 📚 内容结构

```
第一篇 · 范式与市场全景         第 1–4 章
第二篇 · 工作方法论与最新方式    第 5–10 章
第三篇 · 全行业落地             第 11–19 章
第四篇 · 能力、商业与未来        第 20–23 章
第五部分 · 62 个深度专题         技术 / 方法 / 能力 纵深
附录                           术语表 · 工具框架清单 · 参考资料
```

## 🔄 内容更新

1. 替换 `source/FDE全球市场与全行业落地调研报告_2026.md`(原文,只读)
2. (可选)维护 `docs/.meta/tags.json` 标签数据
3. 运行 `pnpm split` — 自动重新生成全部页面、交叉链接、侧边栏、导语页、标签索引、公司索引、术语表
4. `pnpm build` 部署

## 📦 部署

纯静态产物 `docs/.vitepress/dist`,可托管到任意静态平台。

### GitHub Pages(已配置,推送即部署)

仓库含 `.github/workflows/deploy.yml`,推送到 `master` 自动构建部署。本仓库同时部署到两个 Pages 站点:

- **根站点** `fde-wiki.github.io/` — 组织 `FDE-Wiki` 的 `FDE-Wiki.github.io` 仓库,`base = /`
- **项目页** `zhyese.github.io/fde-wiki/` — `zhyese/fde-wiki` 仓库,`base = /fde-wiki/`

`base` 由 workflow 的 `VITEPRESS_BASE` 控制(根站点为 `/`,项目页为 `/<repo>/`)。仓库 Settings → Pages → Source = GitHub Actions。

### Vercel（仓库已配置）

```bash
pnpm dlx vercel
```

根目录 `vercel.json` 已固定 VitePress 框架、`pnpm build` 构建命令与 `docs/.vitepress/dist` 输出目录；首次执行命令时按提示关联或新建 Vercel Project。`base` 默认 `/`，适用于 Vercel。

### LLM 文档索引

构建已接入 `vitepress-plugin-llms`，会生成 `/llms.txt`、`/llms-full.txt` 与逐页的 LLM 友好 Markdown，供 AI 工具读取站点内容。GitHub Pages 项目页会写入上游绝对链接，Vercel 保持根路径链接。

### Netlify

- Build command: `pnpm split && pnpm build`
- Publish directory: `docs/.vitepress/dist`

## 🗂 项目结构

```
fde-wiki/
├─ source/                       # 原始报告(只读,自包含)
├─ scripts/split.mjs             # 拆分 + 交叉链接 + 标签 + 导语页 + 公司索引 + 术语表
├─ vercel.json                    # Vercel：VitePress 构建命令与静态产物目录
├─ docs/
│  ├─ index.md ch01–ch23.md topic01–62.md part1–4.md tags.md companies.md appendix.md
│  ├─ .meta/tags.json            # 标签数据
│  ├─ public/favicon.svg          # 浏览器图标（Wiki + 工程落地路径）
│  └─ .vitepress/
│     ├─ config.ts               # 站点配置(中文搜索分词 / base / 主题)
│     ├─ generated.ts            # 自动生成的 sidebar + nav
│     └─ theme/{index.ts,custom.css}  # 阅读增强组件 + 标签/公司徽章样式
└─ .github/workflows/deploy.yml  # GitHub Pages：构建并部署 docs/.vitepress/dist
```

## 🛠 技术栈

- [VitePress](https://vitepress.dev) 1.6 — 静态站点生成
- MiniSearch — 本地全文搜索(CJK 分词定制)
- @nolebase/vitepress-plugin-enhanced-readabilities — 阅读布局与聚光灯增强
- vitepress-plugin-llms — LLM 友好文档索引与聚合产物
- 纯前端,无后端、无数据库

---

> 本站由原始 Markdown 调研报告自动构建 · 原文未改动
