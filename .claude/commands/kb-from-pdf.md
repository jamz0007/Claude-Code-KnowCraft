---
argument-hint: <pdf-file> [--title=TITLE] [--tags=TAGS] [--category=CAT] [--split] [--ocr]
description: 从 PDF 文件提取知识并创建条目
allowed-tools: Read, Bash
---

# /kb-from-pdf - PDF 知识提取

## 功能
从 PDF 文件中提取内容，自动识别结构，生成知识条目。

## 使用方式

### 基本用法
```
/kb-from-pdf research-paper.pdf

自动从 PDF 提取内容并创建知识条目。
```

### 指定标题和标签
```
/kb-from-pdf document.pdf --title="React 深度解析" --tags=react,frontend
```

### 分长文档为多个条目
```
/kb-from-pdf book.pdf --split

按章节自动拆分为多个知识条目。
```

### 使用 OCR
```
/kb-from-pdf scanned.pdf --ocr

对扫描版 PDF 使用 OCR 提取文字。
```

### 指定分类
```
/kb-from-pdf tutorial.pdf --category=learning --tags=tutorial,beginner
```

## 参数说明

- `pdf-file`: PDF 文件路径 (必需)
- `--title`: 自定义标题 (默认: 从 PDF 提取)
- `--tags`: 指定标签 (逗号分隔)
- `--category`: 指定分类 (code|projects|learning|personal)
- `--split`: 拆分长文档为多个条目
- `--ocr`: 使用 OCR 处理扫描版 PDF
- `--chapters`: 按章节拆分
- `--pages`: 指定页面范围 (例如: 1-50)
- `--language`: 文档语言 (默认: auto)

## 工作流程

### 1. 读取 PDF
```
使用 Claude 的 PDF 阅读能力:
- 读取 PDF 内容
- 识别文档结构
- 提取文本和图片
```

### 2. 内容分析
```
分析 PDF 内容:
- 识别标题层级
- 提取章节结构
- 识别代码块
- 提取关键概念
```

### 3. 智能拆分
```
如果使用 --split:
- 按章节拆分
- 每个章节一个条目
- 自动建立关联
```

### 4. 元数据提取
```
自动提取:
- 标题(文档标题)
- 作者(如果有)
- 出版日期(如果有)
- 关键词(从内容识别)
```

### 5. 生成条目
```
创建知识条目:
- 生成时间戳 ID
- 添加 frontmatter
- 保存到对应目录
- 更新索引
```

## 输出格式

### 短文档(单条目)
```
/kb-from-pdf short-tutorial.pdf

✅ PDF 导入完成!

文件: short-tutorial.pdf
提取页数: 15 页
字数: 3,245 字

生成的条目:
[2026-01-04-130001] React Hooks 快速入门
类型: learning-note
分类: learning
标签: [react, hooks, tutorial, frontend]

摘要:
本文档介绍了 React Hooks 的基础知识，
包括 useState、useEffect 等常用 Hooks 的使用方法...

文件位置: knowledge/items/2026/01-January/2026-01-04-130001.md
```

### 长文档(拆分为多条目)
```
/kb-from-pdf complete-guide.pdf --split

✅ PDF 导入完成!

文件: complete-guide.pdf
总页数: 250 页
章节数: 12 个

生成的条目 (12 个):
1. [2026-01-04-130001] 第1章: React 基础概念
2. [2026-01-04-130002] 第2章: 组件与 Props
3. [2026-01-04-130003] 第3章: State 和 Lifecycle
4. [2026-01-04-130004] 第4章: 事件处理
...
12. [2026-01-04-130012] 第12章: 最佳实践

建立的关联:
→ 自动建立章节关联(前一章节 → 后一章节)
→ 主条目标记为 "complete-guide"

标签:
所有条目自动添加: [react, guide, book]
```

## 内容提取

### 文档结构识别
```
PDF 结构分析:
├─ 封面
│  └─ 标题: "React 完全指南"
│  └─ 作者: "张三"
│  └─ 年份: "2024"
├─ 目录
│  └─ 识别章节结构
├─ 正文
│  ├─ 第1章 (1-20页)
│  ├─ 第2章 (21-45页)
│  └─ ...
└─ 附录
```

### 智能内容提取

#### 标题提取
```markdown
# React 完全指南
## 第一章 基础概念
### 1.1 什么是 React
#### 1.1.1 React 的起源

自动识别标题层级并生成结构化内容
```

#### 代码块提取
```
识别代码块:
```javascript
function Example() {
  return <div>Hello</div>;
}
```

保留格式和语法高亮标记
```

#### 列表提取
```
有序列表:
1. 第一步
2. 第二步
3. 第三步

无序列表:
- 要点一
- 要点二
- 要点三
```

#### 表格提取
```
| 概念 | 描述 |
|------|------|
| Hook | 函数组件的特性 |
| Props | 组件的输入 |

转换为 Markdown 表格
```

### 元数据提取

#### 自动识别
```
从 PDF 内容提取:
- 标题: 文档标题或第一级标题
- 作者: 封面或版权页
- 日期: 版权页或发布信息
- 关键词: 章节标题或关键词
```

#### 生成的 frontmatter
```yaml
---
id: 2026-01-04-130001
title: "React 完全指南 - 第1章"
type: learning-note
category: learning
tags: [react, guide, frontend, basics]
source:
  type: pdf
  file: complete-guide.pdf
  author: "张三"
  year: 2024
  pages: "1-20"
created: 2026-01-04T13:00:00Z
modified: 2026-01-04T13:00:00Z
version: 1
links: []
backlinks: []
---
```

## 高级功能

### 按章节拆分
```
/kb-from-pdf book.pdf --split --chapters

按章节自动拆分:
- 识别章节标题
- 提取章节范围
- 每章创建一个条目
- 自动建立关联
```

### 页面范围
```
/kb-from-pdf document.pdf --pages=1-50

只导入前 50 页
```

### 语言检测
```
/kb-from-pdf chinese-doc.pdf --language=zh

指定文档语言以优化提取
```

### OCR 处理
```
/kb-from-pdf scanned.pdf --ocr

对扫描版 PDF:
1. 使用 OCR 提取文字
2. 自动检测语言
3. 识别布局
4. 提取内容
```

### 批量导入
```
/kb-from-pdf *.pdf --recursive

批量导入目录中的所有 PDF
```

## 内容增强

### 自动摘要
```
提取时自动生成摘要:
本文档介绍了 React 的核心概念，
包括组件、Props、State 等基础知识，
并通过实例说明了如何使用 React 构建用户界面。
```

### 关键词提取
```
从内容中提取关键词:
- React
- 组件
- Props
- State
- JSX
- 虚拟 DOM
```

### 标签建议
```
基于内容建议标签:
核心标签: react, frontend
类型标签: guide, tutorial
具体标签: components, state, props
```

## 处理不同类型 PDF

### 学术论文
```
/kb-from-pdf research-paper.pdf

特殊处理:
- 提取摘要(Abstract)
- 提取关键词(Keywords)
- 识别章节结构
- 提取引用(References)
```

### 技术文档
```
/kb-from-pdf api-reference.pdf

特殊处理:
- 识别 API 签名
- 提取代码示例
- 保留参数说明
- 提取返回值
```

### 电子书
```
/kb-from-pdf ebook.pdf --split

特殊处理:
- 按章节拆分
- 保留目录结构
- 提取侧边栏内容
- 处理双栏排版
```

### 扫描文档
```
/kb-from-pdf scanned.pdf --ocr

特殊处理:
- OCR 文字识别
- 版面分析
- 图片提取
- 去除噪点
```

## 错误处理

### 文件读取失败
```
❌ 错误: 无法读取 PDF 文件
原因: 文件损坏或格式不支持
建议: 检查文件是否为有效 PDF
```

### OCR 失败
```
⚠️  警告: OCR 处理遇到问题
页面: 15-20
建议: 这些页面可能需要手动检查
```

### 编码问题
```
⚠️  警告: 检测到编码问题
已尝试: UTF-8, GBK, Big5
结果: 部分字符可能显示不正确
```

### 内容为空
```
❌ 错误: PDF 内容为空
可能原因:
- PDF 是扫描版且未使用 OCR
- PDF 是图片格式
- PDF 加密

建议: 使用 --ocr 选项
```

## 导入后操作

### 检查导入结果
```
/kb-list --by=recent --limit=5
```

### 查看导入的内容
```
/kb-search --tag=pdf-imported
```

### 建立关联
```
/kb-link chapter1 chapter2 --type=builds-on
```

### 补充标签
```
/kb-edit id --field=tags
```

### 清理内容
```
检查格式:
- 代码块是否正确
- 表格是否完整
- 图片是否提取
```

## 最佳实践

### 1. 先预览
```
使用 --dry-run 预览提取结果
```

### 2. 分批处理
```
大型书籍分章节导入:
/kb-from-pdf book.pdf --pages=1-100
/kb-from-pdf book.pdf --pages=101-200
```

### 3. 使用拆分
```
长文档使用 --split:
/kb-from-pdf guide.pdf --split
每章一个条目，便于管理
```

### 4. 补充元数据
```
导入后补充:
- 作者信息
- 出版年份
- 来源链接
- 阅读笔记
```

### 5. 创建关联
```
为相关章节建立关联:
- 前后章节
- 相关概念
- 引用文献
```

## 与其他命令配合

### 导入后增强
```
/kb-from-pdf document.pdf
@knowledge-enricher "增强导入的内容"
```

### 导入后分析
```
/kb-from-pdf research.pdf
@research-assistant "总结研究发现"
```

### 导入后组织
```
/kb-from-pdf chapter.pdf
@knowledge-architect "组织章节结构"
```

## 注意事项

### 1. PDF 质量
- 高质量 PDF 提取效果更好
- 扫描版需要 OCR
- 加密 PDF 需要先解密

### 2. 文件大小
- 大型 PDF 处理时间较长
- 建议分批处理
- 考虑按页面范围导入

### 3. 版权问题
- 尊重 PDF 版权
- 个人学习使用
- 不得商业分发

### 4. 内容准确性
- 检查 OCR 结果
- 验证代码示例
- 确认公式转换

### 5. 图片处理
- 图片需要单独保存
- 考虑图片大小
- 手动检查图片链接

## 扩展功能(未来)

### 1. 批量导入
```
/kb-from-pdf --batch *.pdf
```

### 2. 智能分页
```
自动识别最佳拆分点
```

### 3. 图表提取
```
提取和转换 PDF 中的图表
```

### 4. 公式识别
```
提取 LaTeX/MathML 公式
```

### 5. 双语处理
```
处理中英混排 PDF
```
