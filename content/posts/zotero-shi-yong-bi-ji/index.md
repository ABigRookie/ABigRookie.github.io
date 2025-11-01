---
title: "Zotero 使用笔记"
date: 2022-11-21 16:13:02
draft: false
---

记录一下自己在使用 Zotero 管理文献时常用的插件和技巧，方便以后查阅。

## 推荐插件

### DOI Manager
- 功能：补全或批量更新条目的 DOI，与 Sci-Hub 等工具配合可以迅速获取全文；
- 地址：<https://github.com/bwiernik/zotero-shortdoi>；
- 使用：在条目上右键选择 `Manage DOIs → Get Long DOIs`。

### Zotero PDF Translate
- 功能：在 PDF 阅读器中直接翻译选中的段落；
- 地址：<https://github.com/windingwind/zotero-pdf-translate>；
- 使用：安装后，在 PDF 里选中英文段落即可看到翻译面板。

### Zotero Scholar Rank & Zotero updateifsE
- 功能：显示期刊 CCF/SCI 分区、影响因子等信息，适合快速了解文献档次；
- 地址：
  - Scholar Rank: <https://github.com/SiriusXT/Zotero-Scholar-Rank>
  - updateifsE: <https://github.com/redleafnew/zotero-updateifsE>

## 使用技巧

### Zotero Connector
- Chrome/Edge 插件，可将网页上的文献信息一键保存到指定库；
- 遇到无法直接下载 PDF 时，可先保存条目，再结合 DOI Manager 与 Sci-Hub 获取全文。

### 自定义 PDF 获取路径
在 `首选项 → 高级 → 高级设置 → 配置编辑器` 中搜索 `findPDF`，将以下内容写入即可：

```json
{ 
  "name": "sci-hub", 
  "method": "GET",    
  "url": "https://sci-hub.st/{doi}",    
  "mode": "html", "selector": "#pdf",    
  "attribute": "src",
  "automatic": true
}
```

之后在没有 PDF 的条目上右键选择“查找可用 PDF”，Zotero 会尝试通过 Sci-Hub 获取。

希望这些设置能让文献整理更高效。如果你还有好用的插件，欢迎告诉我！
