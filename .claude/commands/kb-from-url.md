---
argument-hint: <url> [--title=TITLE] [--tags=TAGS] [--category=CAT] [--full-content] [--readability]
description: 从网页 URL 抓取内容并创建知识条目
allowed-tools: Read, mcp__web_reader__webReader
---

# /kb-from-url - 网页知识抓取

## 功能
从网页 URL 抓取内容，自动提取正文，识别元数据，生成知识条目。

## 使用方式

### 基本用法
```
/kb-from-url https://react.dev/learn

从 URL 提取内容并创建知识条目。
```

### 指定标题和标签
```
/kb-from-url https://blog.example.com/react-hooks --title="React Hooks 教程" --tags=react,hooks
```

### 提取完整内容
```
/kb-from-url https://example.com/long-article --full-content

提取完整内容，包括评论区等。
```

### 使用阅读模式
```
/kb-from-url https://news.example.com/article --readability

使用阅读模式，提取干净的正文内容。
```

### 批量导入
```
/kb-from-url urls.txt --batch

从文本文件批量导入多个 URL。
```

## 参数说明

- `url`: 网页 URL 或包含 URL 的文件 (必需)
- `--title`: 自定义标题 (默认: 从网页提取)
- `--tags`: 指定标签 (逗号分隔)
- `--category`: 指定分类
- `--full-content`: 提取完整内容(包括侧边栏、评论区等)
- `--readability`: 使用阅读模式(仅正文)
- `--include-images`: 保留图片链接
- `--convert-links`: 转换相对链接为绝对链接
- `--batch`: 批量模式(从文件读取 URL)
- `--delay`: 批量模式下的请求延迟(秒)

## 工作流程

### 1. URL 验证
```
检查 URL 格式:
- 必须是有效的 HTTP/HTTPS URL
- 检查可访问性
- 获取重定向链
```

### 2. 内容抓取
```
使用 MCP web reader 或内置工具:
- 获取网页 HTML
- 转换为 Markdown
- 提取正文内容
- 识别元数据
```

### 3. 内容清理
```
智能清理:
- 移除广告
- 移除导航栏
- 移除页脚
- 移除脚本和样式
- 保留主要内容
```

### 4. 元数据提取
```
自动提取:
- 标题: <title> 或 <h1>
- 作者: meta author 或 byline
- 发布时间: meta date 或 time
- 描述: meta description
- 关键词: meta keywords
- 域名: 用作标签
```

### 5. 生成条目
```
创建知识条目:
- 生成时间戳 ID
- 添加 frontmatter
- 保存内容
- 更新索引
```

## 输出示例

### 成功导入
```
/kb-from-url https://react.dev/learn

⏳ 正在抓取内容...
URL: https://react.dev/learn
重定向: 无

✅ 网页内容导入完成!

来源信息:
  URL: https://react.dev/learn
  域名: react.dev
  作者: React Team
  发布时间: 2024-12-01

内容统计:
  字数: 5,234 字
  段落: 45 个
  代码块: 8 个
  图片: 12 个

生成的条目:
[2026-01-04-140001] React 官方教程 - Learn React
类型: learning-note
分类: learning
标签: [react, tutorial, official, frontend]

自动摘要:
本文档是 React 官方教程，介绍了 React 的基础概念，
包括组件、Props、State 等核心内容，并提供实例演示。

元数据:
  来源类型: website
  原始 URL: https://react.dev/learn
  域名标签: react.dev
  作者: React Team
  抓取时间: 2026-01-04 14:00

文件位置: knowledge/items/2026/01-January/2026-01-04-140001.md
```

### 阅读模式
```
/kb-from-url https://blog.example.com/article --readability

✅ 网页内容导入完成!(阅读模式)

清理统计:
  移除广告: 15 个
  移除导航: 3 个
  移除脚本: 8 个
  移除样式: 12 个

正文内容:
  纯净的 Markdown 内容
  保留图片和代码
  结构清晰
```

### 批量导入
```
/kb-from-url urls.txt --batch

读取文件: urls.txt (5 个 URL)

⏳ 批量抓取中...
[1/5] https://example.com/article1 ✅
[2/5] https://example.com/article2 ✅
[3/5] https://example.com/article3 ❌ (404 Not Found)
[4/5] https://example.com/article4 ✅
[5/5] https://example.com/article5 ✅

批量导入完成!
成功: 4 个
失败: 1 个

生成的条目:
1. [2026-01-04-140001] Article 1
2. [2026-01-04-140002] Article 2
3. [2026-01-04-140004] Article 4
4. [2026-01-04-140005] Article 5

失败列表:
- https://example.com/article3 (404 Not Found)
```

## 内容提取

### 网页结构识别
```
识别常见结构:
├─ 头部 (Header)
│  ├─ 导航 (移除)
│  └─ 标题 (保留)
├─ 主体 (Main)
│  ├─ 文章 (保留)
│  ├─ 侧边栏 (移除)
│  └─ 评论区 (可选)
└─ 页脚 (Footer) (移除)
```

### Markdown 转换

#### 标题
```html
<h1>主标题</h1>
<h2>二级标题</h2>
<h3>三级标题</h3>

↓ 转换为 ↓

# 主标题
## 二级标题
### 三级标题
```

#### 链接
```html
<a href="https://example.com">链接文本</a>

↓ 转换为 ↓

[链接文本](https://example.com)
```

#### 代码块
```html
<pre><code class="language-javascript">
function example() {
  return true;
}
</code></pre>

↓ 转换为 ↓

\```javascript
function example() {
  return true;
}
\```
```

#### 图片
```html
<img src="image.jpg" alt="图片描述">

↓ 转换为 ↓

![图片描述](image.jpg)

或 (使用 --include-images)
![图片描述](https://example.com/image.jpg)
```

#### 表格
```html
<table>
  <tr>
    <th>标题1</th>
    <th>标题2</th>
  </tr>
  <tr>
    <td>数据1</td>
    <td>数据2</td>
  </tr>
</table>

↓ 转换为 ↓

| 标题1 | 标题2 |
|-------|-------|
| 数据1 | 数据2 |
```

### 元数据提取

#### HTML Meta 标签
```html
<meta name="author" content="张三">
<meta name="description" content="文章描述">
<meta name="keywords" content="react, hooks, frontend">
<meta name="date" content="2024-12-01">

↓ 提取为 ↓

author: "张三"
description: "文章描述"
tags: ["react", "hooks", "frontend"]
published: "2024-12-01"
```

#### Open Graph
```html
<meta property="og:title" content="分享标题">
<meta property="og:description" content="分享描述">
<meta property="og:image" content="分享图片">

↓ 提取为 ↓

备用标题: "分享标题"
备用描述: "分享描述"
缩略图: "分享图片"
```

#### 结构化数据
```html
<script type="application/ld+json">
{
  "@type": "Article",
  "headline": "文章标题",
  "author": {
    "@type": "Person",
    "name": "作者名"
  },
  "datePublished": "2024-12-01"
}
</script>

↓ 提取为 ↓

结构化元数据
```

## 高级功能

### 阅读模式
```
/kb-from-url https://news.example.com/article --readability

启用 Readability 算法:
- 识别正文区域
- 移除干扰元素
- 提取主要内容
- 清理格式
```

### 完整内容
```
/kb-from-url https://blog.example.com/post --full-content

提取包括:
- 正文
- 侧边栏
- 评论区
- 相关文章
```

### 延迟加载
```
/kb-from-url https://example.com/article --wait-for-content

等待动态内容加载:
- 等待 JavaScript 执行
- 等待 AJAX 请求
- 等待图片加载
```

### 自定义清理
```
/kb-from-url url --remove=".ad,.sidebar,.comments"

移除指定 CSS 选择器的内容
```

### 批量导入配置
```
URLs 文件格式:
https://example.com/article1
https://example.com/article2
https://example.com/article3

每行一个 URL
支持注释(以 # 开头)
支持空行
```

## 支持的网站类型

### 技术博客
```
示例: dev.to, medium.com, css-tricks.com

特点:
- 代码块清晰
- Markdown 友好
- 结构良好
```

### 新闻网站
```
示例: news.ycombinator.com, techcrunch.com

建议使用 --readability:
移除广告和导航，仅保留正文
```

### 文档网站
```
示例: docs.rs, developer.mozilla.org

特点:
- 结构化强
- 有目录导航
- 代码示例多
```

### 教程网站
```
示例: tutorialspoint.com, w3schools.com

特点:
- 章节清晰
- 示例丰富
- 适合学习
```

## 生成的 Frontmatter

### 完整示例
```yaml
---
id: 2026-01-04-140001
title: "React 官方教程 - Learn React"
type: learning-note
category: learning
tags: [react, tutorial, official, frontend, basics]

source:
  type: website
  url: "https://react.dev/learn"
  domain: "react.dev"
  author: "React Team"
  published: "2024-12-01T00:00:00Z"
  accessed: "2026-01-04T14:00:00Z"

  # 提取的元数据
  description: "React 官方学习教程"
  keywords: ["react", "learn", "tutorial"]
  language: "en"

  # 统计信息
  wordCount: 5234
  readingTime: "21 分钟"

created: 2026-01-04T14:00:00Z
modified: 2026-01-04T14:00:00Z
version: 1
links: []
backlinks: []
---

# React 官方教程 - Learn React

[正文内容...]
```

## 错误处理

### URL 无效
```
❌ 错误: 无效的 URL
URL: htttp://example.com
建议: 检查 URL 拼写，确保以 http:// 或 https:// 开头
```

### 网站无法访问
```
❌ 错误: 无法访问网站
URL: https://example.com
状态码: 404 Not Found
建议: 检查 URL 是否正确，网站是否在线
```

### 内容提取失败
```
⚠️  警告: 内容提取不完整
URL: https://example.com/article
问题: 网页结构复杂
建议: 手动检查提取的内容，可能需要编辑
```

### 编码问题
```
⚠️  警告: 检测到编码问题
已尝试: UTF-8, GBK
结果: 部分字符可能显示不正确
```

### 超时错误
```
❌ 错误: 请求超时
URL: https://slow-website.com
超时时间: 30 秒
建议: 网站响应过慢，稍后重试
```

## 导入后处理

### 清理内容
```
检查:
- 格式是否正确
- 代码块是否完整
- 图片链接是否有效
- 表格是否正确
```

### 补充信息
```
/kb-edit id --field=tags
添加更具体的标签
```

### 创建关联
```
/kb-link new-id related-id --type=related
与其他知识建立关联
```

### 添加笔记
```
在导入的内容后添加:
- 个人理解
- 学习笔记
- 实践经验
```

## 最佳实践

### 1. 使用阅读模式
```
大多数情况使用 --readability:
/kb-from-url url --readability
获得更干净的内容
```

### 2. 批量导入
```
创建 URLs 文件，批量导入:
echo "
https://example.com/article1
https://example.com/article2
" > urls.txt

/kb-from-url urls.txt --batch
```

### 3. 添加合理延迟
```
批量导入时添加延迟:
/kb-from-url urls.txt --batch --delay=2
避免请求过快被限制
```

### 4. 检查导入结果
```
导入后验证:
- 检查格式
- 验证图片
- 测试代码
- 阅读全文
```

### 5. 补充上下文
```
导入后添加:
- 阅读时间
- 重要程度
- 个人评价
- 相关资源
```

## 与其他命令配合

### 导入后增强
```
/kb-from-url url
@knowledge-enricher "自动摘要和要点提取"
```

### 导入后分析
```
/kb-from-url research-paper-url
@research-assistant "总结研究发现"
```

### 导入后组织
```
/kb-from-url tutorial-url
@knowledge-architect "组织学习路径"
```

## 注意事项

### 1. 版权尊重
- 仅用于个人学习
- 不要商业使用
- 保留来源链接
- 注明原作者

### 2. 内容时效
- 网页内容可能变化
- 建议及时导入
- 定期更新
- 检查过时内容

### 3. 网站限制
- 某些网站有反爬虫
- 可能需要设置延迟
- 尊重 robots.txt
- 遵守网站条款

### 4. 内容质量
- 检查提取质量
- 手动清理格式
- 验证代码示例
- 确认图片链接

### 5. 隐私保护
- 不要导入敏感信息
- 注意个人信息
- 遵守隐私政策
- 本地存储安全

## 扩展功能(未来)

### 1. 订阅源
```
/kb-from-url --subscribe https://blog.example.com/rss.xml
自动抓取 RSS 更新
```

### 2. 定时抓取
```
/kb-from-url --schedule="daily" https://news.example.com
每天自动抓取更新
```

### 3. 智能去重
```
自动检测相似内容，避免重复导入
```

### 4. 内容更新
```
/kb-from-url --update id https://example.com/article
更新已导入的条目
```

### 5. 转发链
```
自动跟踪重定向链，获取最终 URL
```
