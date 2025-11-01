---
title: "Hello Hugo"
date: 2024-10-31
draft: false
---

欢迎来到我使用 **Hugo + PaperMod** 重建的博客！这篇文章留作站点初始化的笔记，也方便以后回顾整个构建流程。

## 本地预览

```bash
hugo server --buildDrafts --buildFuture
```

访问 `http://localhost:1313` 就能实时查看文章效果。若需要预览草稿或未来日期的文章，记得带上 `--buildDrafts` 与 `--buildFuture`。

## 撰写新文章

Hugo 默认支持页面包结构：

```bash
hugo new posts/my-first-hugo-post/index.md
```

命令会创建一个目录 `content/posts/my-first-hugo-post/`，其中的 `index.md` 用来写正文，图片等静态资源直接放在同级目录即可引用。

## 构建与部署

```bash
hugo --minify
```

构建结果会生成到 `public/`。在当前仓库中，GitHub Actions 会自动运行这一步并部署到 GitHub Pages，我们只需要把源码推送到 `main`。

感谢你来到这里，也欢迎你和我一样继续记录、分享和交流。
