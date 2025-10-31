# ABigRookie GitHub Pages Blog

这个仓库使用 [Hexo](https://hexo.io/) + [hexo-theme-next](https://github.com/next-theme/hexo-theme-next) 构建，用于部署在 GitHub Pages 上。

## 本地开发

1. 安装 Node.js（建议 18 LTS+）与 Git。如果刚安装完 Node.js 仍然提示找不到 `node`/`npm`，重新打开终端或把 `C:\Program Files\nodejs` 添加到 `PATH`。
2. 在仓库根目录执行 `npm install` 安装依赖。
3. 常用脚本：

   ```bash
   npm run serve   # 启动本地预览，默认 http://localhost:4000
   npm run build   # 生成静态文件到 public/
   npm run clean   # 清理缓存与 public/
   ```

4. 在 `source/_posts/` 中新增 Markdown 文件撰写文章，例如：

   ```bash
   npx hexo new post "My New Post"
   ```

   Hexo 会自动为文章创建同名资源目录，方便放置图片等素材。

## 部署到 GitHub Pages

- `_config.yml` 中已经配置 `hexo-deployer-git`，默认推送到 `gh-pages` 分支。
- 修改为你自己的 SSH/HTTPS 仓库地址后，执行：

  ```bash
  npm run deploy
  ```

  Hexo 会自动执行 `hexo clean && hexo generate && hexo deploy`，并将静态文件推送到配置的分支。

如果你希望使用 GitHub Actions 自动部署，可以参考 Hexo 官方文档或在仓库中新增 workflow（例如 `peaceiris/actions-gh-pages`）。

## 目录结构说明

```
.
├── _config.yml           # Hexo 全局配置
├── _config.next.yml      # NexT 主题配置
├── package.json          # 依赖与脚本
├── scaffolds/            # 新建内容模板
├── source/
│   ├── _posts/           # 文章目录
│   ├── about/            # 关于页
│   ├── categories/       # 分类页
│   └── tags/             # 标签页
└── themes/
    └── next/             # NexT 主题（已拉取最新版源码）
```

## 下一步可选操作

- 在 `_config.yml` 中补充 `title`、`subtitle`、`description` 等元信息。
- 编辑 `_config.next.yml` 自定义菜单、社交链接、配色、评论等主题功能。
- 将原 Gridea 导出的 Markdown 文章迁移至 `source/_posts/`，调整 Front Matter 即可。
