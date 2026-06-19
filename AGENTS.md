# AGENTS.md — 给协作者 / AI 的操作指南

本仓库是一个纯静态项目展示站点的「地基」。本文件说明在这个地基上
**如何新增一个项目展示页**，以及需要遵守的约定。先读完再动手。

## 这个仓库是什么

- 静态站点，托管在 Cloudflare Pages，**无构建步骤**，推送即部署。
- 仓库根目录 = 站点根目录。
- 全站共享一套设计系统：[`assets/base.css`](./assets/base.css)。

目录结构与设计原则见 [`README.md`](./README.md)。

## 添加一个项目展示页

### 1. 从模板创建页面

把模板复制到项目目录（每个项目一个子目录）：

```bash
mkdir -p projects/<项目名>
cp templates/project.html projects/<项目名>/index.html
```

`<项目名>` 用小写英文 + 连字符（kebab-case），例如 `image-tool`。
它会成为访问路径的一部分：`/projects/<项目名>/`。

### 2. 填充内容

打开 `projects/<项目名>/index.html`，**全文搜索 `TODO`**，逐项替换：

- `<title>` 与 `<meta name="description">`
- 标题 `<h1>` 与简介 `.subtitle`
- 按钮里的 GitHub 仓库链接
- 特性卡片（可增删）
- 演示区 `#demo`（嵌入 iframe / 动图 / 截图等）

### 3. 在首页登记这个项目

编辑根目录 `index.html`，在 `<section class="grid" id="projects">` 里
**复制一张 `<a class="card">`**，改成你的项目，`href` 指向 `/projects/<项目名>/`：

```html
<a class="card" href="/projects/<项目名>/">
    <h3>🔧 项目标题</h3>
    <p>一句话简介。</p>
    <span class="card-link">查看演示 →</span>
</a>
```

> 首次添加项目后，可删除首页里那张「示例项目（占位）」卡片，
> 以及 `projects/.gitkeep`。

## 约定（请遵守）

- **样式走共享系统**：优先使用 `base.css` 里已有的类
  （`.container` `.card` `.grid` `.btn` `.btn-primary` `.btn-outline`
  `.badge` `.panel` `.placeholder` `.subtitle` 等）。
  需要新外观时，先考虑把它加进 `base.css` 让全站复用；
  只有**本页特有**的小调整才写进该页 `<head>` 的 `<style>`。
- **用绝对路径引用资源**：`/assets/base.css`、`/`（首页），
  不要用 `../../`，避免目录层级变化时失效。
- **不要新增构建工具 / 框架 / 依赖**：保持纯静态、零构建。
- **每个项目自成一目录**，资源（图片等）放在该目录内，互不干扰。
- **可访问性**：图标 `<svg>` 加 `aria-hidden="true"`，
  链接按钮文字要有意义，保持语义化标签。
- **中文为主、可中英混排**，与现有页面风格一致。

## 本地预览

```bash
python3 -m http.server 8000   # 打开 http://localhost:8000
```

改完自查清单：

- [ ] 页面里已没有残留的 `TODO`
- [ ] 首页新增了对应卡片，点击能跳到项目页
- [ ] 项目页能正确加载 `base.css`（用本地服务器预览，不要用 `file://`）
- [ ] 亮色 / 暗色模式下都正常（切换系统主题查看）
- [ ] 手机窄屏下布局正常
