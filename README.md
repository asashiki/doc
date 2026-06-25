<div align="center">

<img src="https://cdn.jsdelivr.net/gh/asashiki/asashiki-design@main/assets/brand/asashiki-mark-color-t.png" alt="Asashiki" width="84" />

# doc — 项目展示与文档站点

一个纯静态的项目展示中心。首页用卡片列出各项目，每个项目有自己的展示页（在线演示 + 说明），全站共享一套设计系统。

[![Live](https://img.shields.io/badge/Live-doc.asashiki.com-6b6570?style=flat-square&labelColor=221f26)](https://doc.asashiki.com)
![Deploy](https://img.shields.io/badge/Deploy-Cloudflare_Pages-6b6570?style=flat-square&labelColor=221f26)
![Build](https://img.shields.io/badge/Build-zero--config-6b6570?style=flat-square&labelColor=221f26)
[![Asashiki Design](https://img.shields.io/badge/Asashiki-Design_System-e85d97?style=flat-square&labelColor=221f26)](https://github.com/asashiki/asashiki-design)

</div>

首页用卡片列出各个项目，每个项目有自己的展示页（在线演示 + 说明）。
全站共享一套设计系统，新增项目只需复制模板、填内容、加一张卡片。

> 这个仓库是「地基」：模板、设计系统和文档已经搭好。
> 具体每个项目的展示页内容，由后续的协作者（人或 AI）按 [`AGENTS.md`](./AGENTS.md) 填充。

## 目录结构

```
doc/
├── index.html              # 门户首页：用卡片列出所有项目
├── 404.html                # 找不到页面时的回退页
├── assets/
│   └── base.css            # 共享设计系统（颜色 token、按钮、卡片等）
├── templates/
│   └── project.html        # 单个项目展示页的可复制模板
├── projects/               # 各项目展示页：projects/<项目名>/index.html
│   └── .gitkeep
├── README.md               # 本文件
└── AGENTS.md               # 给后续协作者 / AI 的操作指南
```

## 设计原则

- **静态优先**：纯 HTML + CSS，无构建步骤，推送即部署。
- **单一设计系统**：所有页面引用同一个 [`assets/base.css`](./assets/base.css)，
  避免风格漂移。改全站外观只改这一个文件。
- **绝对路径引用**：页面里用 `/assets/base.css`（而非相对路径），
  这样不论页面放在哪一层目录都能正确加载样式。
- **暗色模式自动适配**：`base.css` 通过 `prefers-color-scheme` 跟随系统，无需 JS。
- **复制即用的模板**：新项目从 [`templates/project.html`](./templates/project.html) 起步。

## 新增一个项目（速览）

1. 复制 `templates/project.html` 到 `projects/<项目名>/index.html`。
2. 搜索文件里的 `TODO`，逐项替换为真实内容。
3. 编辑根目录 `index.html`，在「项目卡片」区复制一张卡片，
   `href` 指向 `/projects/<项目名>/`。

完整规范与约定见 [`AGENTS.md`](./AGENTS.md)。

## 本地预览

无需依赖，任选其一在仓库根目录启动一个静态服务器：

```bash
python3 -m http.server 8000
# 然后浏览器打开 http://localhost:8000
```

> 直接双击打开 HTML 文件也能看，但 `/assets/base.css` 这类绝对路径
> 在 `file://` 协议下会失效，所以建议用上面的本地服务器预览。

## 部署（Cloudflare Pages）

本仓库就是站点根目录，无构建步骤：

- **Build command**：留空
- **Build output directory**：`/`（仓库根目录）

连接到 GitHub 后，推送到生产分支即自动部署。

---

<div align="center">
<sub>界面与文档遵循 <a href="https://github.com/asashiki/asashiki-design">Asashiki Design</a> · 墨と桜 —— 暖中性灰打底，樱粉作克制点缀。</sub>
</div>
