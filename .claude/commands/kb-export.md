---
argument-hint: <output> [--type=markdown|json|html|pdf] [--filter=...] [--include-versions] [--standalone]
description: 导出知识库内容
allowed-tools: Read, Write, Bash
---

# /kb-export - 导出知识库

## 功能
将知识库内容导出为各种格式，支持 Markdown bundle、完整 JSON、静态网站和 PDF。

## 使用方式

### 导出为 Markdown Bundle
```
/kb-export my-knowledge.zip --type=markdown

打包所有知识条目为 Markdown 文件。
```

### 导出为 JSON
```
/kb-export knowledge-dump.json --type=json

导出完整的 JSON 数据(包括元数据)。
```

### 导出为静态网站
```
/kb-export website/ --type=html

生成可浏览的静态网站。
```

### 导出为 PDF
```
/kb-export react-guide.pdf --type=pdf --filter="tag:react"

导出 React 相关内容为 PDF。
```

### 过滤导出
```
/kb-export learning-notes.zip --type=markdown --filter="category:learning"

仅导出 learning 分类的条目。
```

### 包含版本历史
```
/kb-export full-export.zip --type=markdown --include-versions

导出所有内容，包括版本历史。
```

## 参数说明

- `output`: 输出文件或目录路径 (必需)
- `--type`: 导出类型
  - `markdown`: Markdown bundle (默认)
  - `json`: 完整 JSON 导出
  - `html`: 静态网站
  - `pdf`: PDF 文档
- `--filter`: 过滤条件
  - `tag:xxx`: 按标签
  - `category:xxx`: 按分类
  - `after:DATE`: 按日期
  - `id:xxx1,xxx2`: 指定 ID
- `--include-versions`: 包含版本历史
- `--standalone`: 独立文档(包含所有依赖)
- `--pretty`: JSON 格式化输出
- `--theme`: 主题(html/pdf)

## 导出类型详解

### 1. Markdown Bundle

#### 基本导出
```
/kb-export backup-2025-01-04.zip --type=markdown

输出结构:
backup-2025-01-04.zip
├── index.json
├── tags.json
├── relationships.json
├── items/
│   ├── 2025-01-04-104800.md
│   ├── 2026-01-04-105644.md
│   ├── 2026-01-04-105730.md
│   ├── 2026-01-04-105815.md
│   └── 2026-01-04-105900.md
└── versions/ (可选)
    └── 2026-01-04-105815.v1.md
```

#### 保留目录结构
```
/kb-export backup.zip --type=markdown --preserve-structure

保留原始的 YYYY/MM-Month/ 目录结构
```

#### 仅导出特定内容
```
/kb-export react-notes.zip --type=markdown --filter="tag:react"

仅导出包含 react 标签的条目
```

#### 元数据包含
```yaml
每个 Markdown 文件包含完整的 frontmatter:
---
id: 2026-01-04-105815
title: "React Hooks 深入理解"
type: learning-note
category: learning
tags: [react, hooks, frontend]
created: 2026-01-04T10:58:15Z
modified: 2026-01-04T11:00:00Z
version: 1
links:
  - to: 2026-01-04-105644
    type: references
backlinks: []
---

# React Hooks 深入理解

(内容...)
```

### 2. JSON 导出

#### 完整导出
```
/kb-export full-dump.json --type=json --pretty

导出所有数据为单个 JSON 文件:

{
  "version": "1.0",
  "exportDate": "2025-01-04T12:00:00Z",
  "stats": {
    "totalItems": 5,
    "totalTags": 12,
    "totalLinks": 3
  },
  "index": { ... },
  "tags": { ... },
  "relationships": { ... },
  "items": [
    {
      "id": "2026-01-04-105815",
      "title": "React Hooks 深入理解",
      "content": "# React Hooks 深入理解\n\n...",
      "metadata": { ... }
    },
    ...
  ]
}
```

#### 仅导出元数据
```
/kb-export metadata.json --type=json --metadata-only

仅导出 index.json，不包含内容
```

#### 分离导出
```
/kb-export export/ --type=json --separate

导出为多个文件:
export/
├── index.json
├── tags.json
├── relationships.json
├── items/
│   ├── 2026-01-04-105815.json
│   └── ...
```

### 3. 静态网站导出

#### 基本网站
```
/kb-export website/ --type=html

生成独立的静态网站:

website/
├── index.html
├── styles.css
├── app.js
├── data/
│   ├── knowledge.json
│   └── search-index.json
└── assets/
    └── ...
```

#### 网站特性
- ✅ 响应式设计
- ✅ 内置搜索功能
- ✅ 标签过滤
- ✅ 分类浏览
- ✅ 知识图谱可视化
- ✅ 代码高亮
- ✅ 深色模式支持

#### 自定义主题
```
/kb-export website/ --type=html --theme=dark

使用深色主题
```

#### 包含搜索
```
/kb-export website/ --type=html --with-search

启用客户端搜索功能
```

#### 示例页面结构
```
<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>个人知识库</title>
    <link rel="stylesheet" href="styles.css">
</head>
<body>
    <header>
        <h1>我的知识库</h1>
        <div class="search">
            <input type="text" id="search-input" placeholder="搜索...">
        </div>
    </header>

    <nav class="filters">
        <button class="tag-filter" data-tag="all">全部</button>
        <button class="tag-filter" data-tag="react">React</button>
        <button class="tag-filter" data-tag="javascript">JavaScript</button>
    </nav>

    <main class="knowledge-grid">
        <article class="knowledge-item" data-id="2026-01-04-105815">
            <h2>React Hooks 深入理解</h2>
            <div class="metadata">
                <span class="tags">react, hooks, frontend</span>
                <span class="date">2026-01-04</span>
            </div>
            <div class="summary">
                React Hooks 是 React 16.8 引入的新特性...
            </div>
            <a href="#detail-2026-01-04-105815">查看详情</a>
        </article>
        ...
    </main>

    <div id="detail-modal" class="modal">
        <div class="modal-content">
            <span class="close">&times;</span>
            <div id="detail-content"></div>
        </div>
    </div>

    <script src="app.js"></script>
</body>
</html>
```

### 4. PDF 导出

#### 基本 PDF
```
/kb-export knowledge-base.pdf --type=pdf

所有内容导出为单个 PDF
```

#### 按主题导出
```
/kb-export react-guide.pdf --type=pdf --filter="tag:react"

导出 React 相关内容
```

#### 分章节导出
```
/kb-export knowledge-base.pdf --type=pdf --toc

生成目录和章节
```

#### PDF 样式
```
/kb-export knowledge-base.pdf --type=pdf --style=academic

学术风格 PDF:
- 封面
- 目录
- 章节分隔
- 页码
- 页眉页脚
```

#### PDF 选项
- `--toc`: 包含目录
- `--style`: 样式主题(academic/simple/colorful)
- `--font`: 字体设置
- `--margin`: 页边距
- `--page-number`: 页码格式

## 过滤选项

### 按标签
```
/kb-export react.zip --filter="tag:react,hooks"
```

### 按分类
```
/kb-export code.zip --filter="category:code"
```

### 按日期
```
/kb-export recent.zip --filter="after:2025-01-01"
```

### 按组合条件
```
/kb-export export.zip --filter="tag:react & category:learning"
```

### 按指定 ID
```
/kb-export selected.zip --filter="id:2026-01-04-105815,2026-01-04-105644"
```

## 导出报告

### 成功导出
```
✅ 导出完成!

类型: markdown
输出: backup-2025-01-04.zip
大小: 2.3 MB

导出统计:
  条目: 5 个
  标签: 12 个
  链接: 3 个
  版本: 4 个

文件列表:
  ✅ index.json
  ✅ tags.json
  ✅ relationships.json
  ✅ items/2025-01-04-104800.md
  ✅ items/2026-01-04-105644.md
  ✅ items/2026-01-04-105730.md
  ✅ items/2026-01-04-105815.md
  ✅ items/2026-01-04-105900.md

导出时间: 1.2 秒
```

### HTML 导出报告
```
✅ 网站生成完成!

输出: website/
大小: 3.5 MB

生成文件:
  ✅ index.html (首页)
  ✅ styles.css (样式)
  ✅ app.js (交互)
  ✅ data/knowledge.json (数据)
  ✅ data/search-index.json (搜索索引)

功能:
  ✅ 响应式设计
  ✅ 搜索功能
  ✅ 标签过滤
  ✅ 知识图谱
  ✅ 代码高亮

访问方式:
  直接打开 website/index.html
  或使用本地服务器: python -m http.server 8000
```

## 高级功能

### 定期备份
```
/kb-export "backup-$(date +%Y%m%d).zip" --type=markdown --include-versions

自动生成带日期的备份文件
```

### 增量导出
```
/kb-export incremental.zip --type=markdown --after="last-export"

仅导出上次导出后的新增/修改内容
```

### 加密导出
```
/kb-export secret.zip --type=markdown --encrypt

使用密码加密导出文件
```

### 压缩选项
```
/kb-export backup.zip --type=markdown --compression=maximum

最大压缩率
```

## 与其他命令的配合

### 导出前验证
```
/kb-list --by=recent --limit=10
/kb-export latest.zip --type=markdown
```

### 导出后分享
```
/kb-export website/ --type=html
# 上传到 GitHub Pages 或 Netlify
```

### 迁移数据
```
/kb-export full-export.zip --type=markdown --include-versions
# 在另一台机器上导入
/kb-import full-export.zip
```

## 注意事项

### 1. 文件大小
- 大量内容导出可能产生大文件
- 建议使用压缩
- 考虑分批导出

### 2. 依赖项
- HTML 导出需要浏览器支持
- PDF 导出需要相应工具
- Markdown 是最通用的格式

### 3. 隐私保护
- 导出的内容可能包含敏感信息
- 谨慎分享
- 考虑使用加密

### 4. 链接处理
- 导出时保留内部链接
- 外部链接保持原样
- 可能需要手动检查

### 5. 图片处理
- Markdown: 相对路径
- HTML: 复制到 assets/
- PDF: 嵌入图片

## 最佳实践

### 1. 定期备份
```
每月导出一次完整备份
/kb-export "backup-$(date +%Y%m).zip" --type=markdown --include-versions
```

### 2. 主题备份
```
按主题导出便于分享
/kb-export react-guide.zip --filter="tag:react"
```

### 3. 网站发布
```
生成静态网站发布到网上
/kb-publish website/ --type=html
```

### 4. 离线访问
```
导出为 HTML 便于离线查看
/kb-export offline/ --type=html
```

### 5. 数据迁移
```
导出完整数据用于迁移
/kb-export migration.zip --type=json --include-versions
```

## 扩展功能(未来)

### 1. 更多导出格式
```
- EPUB 电子书
- Word 文档
- PowerPoint 演示文稿
```

### 2. 自定义模板
```
使用自定义模板导出 HTML/PDF
```

### 3. 自动发布
```
直接发布到 GitHub Pages/Netlify
```

### 4. 增量备份
```
自动同步到云存储
```

### 5. 协作导出
```
导出为团队共享格式
```
