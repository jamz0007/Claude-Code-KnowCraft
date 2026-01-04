# 个人知识系统 - Claude Code 集成

基于 Claude Code 的个人知识管理系统,使用本地文件存储(JSON + Markdown)。

## 🎯 系统特性

- ✅ **纯文本存储**: JSON + Markdown,无数据库依赖
- ✅ **时间组织**: 按日期自动分层组织
- ✅ **灵活标签**: 多标签分类系统
- ✅ **版本控制**: 内置版本追踪
- ✅ **多源输入**: PDF、URL、图片支持
- ✅ **主动学习**: 间隔重复、费曼技巧、麦肯锡学习法

## 📁 目录结构

```
d:/my-know/
├── .claude/
│   └── commands/          # 斜杠命令定义
├── knowledge/             # 知识存储
│   ├── index.json        # 全局索引
│   ├── items/            # 知识条目(按日期组织)
│   └── .versions/        # 版本历史
├── learning/             # 学习系统
├── templates/            # 知识条目模板
├── exports/              # 导出内容
└── config/               # 配置文件
```

## 🚀 快速开始

### 第一阶段功能(已实现 ✅)

#### 1. 添加知识
```bash
/kb-add
```
系统会提示你输入标题和内容,自动创建知识条目。

#### 2. 搜索知识
```bash
/kb-search 关键词
```

高级搜索:
```bash
/kb-search --tag=react --category=learning hooks
```

#### 3. 浏览知识
```bash
/kb-list --by=recent --limit=10
```

### 第二阶段功能(已实现 ✅)

#### 1. 创建知识关联
```bash
/kb-link 2026-01-04-105815 2026-01-04-105644 --type=references
```
在两个知识条目之间创建双向关联。

#### 2. 编辑知识
```bash
/kb-edit 2026-01-04-105815 --field=content
```
编辑知识条目,自动创建版本备份。

#### 3. 删除知识
```bash
/kb-delete 2026-01-04-105730 --archive
```
删除或归档知识条目,自动清理关联。

#### 4. 知识图谱
```bash
/kb-graph --format=mermaid
```
生成知识图谱可视化(支持 Mermaid、HTML、ASCII 三种格式)。

#### 5. 智能辅助
Knowledge Manager Skill 会自动:
- 建议标签
- 建议分类
- 推荐关联
- 优化组织

### 第三阶段功能(已实现 ✅)

#### 1. 版本对比
```bash
/kb-diff 2026-01-04-105815 --format=timeline
```
对比不同版本,追踪知识演化过程。

#### 2. 版本恢复
```bash
/kb-restore 2026-01-04-105815 --version=3
```
从历史版本恢复知识条目。

#### 3. 高级搜索
```bash
/kb-search --tag=react --type=learning-note --sort=links --format=detailed
```
支持多种过滤、排序和格式选项。

#### 4. Version Keeper Agent
```
@version-keeper "分析 React Hooks 的知识演化"
```
分析知识演化过程,追踪认知变化。

### 第四阶段功能(已实现 ✅)

#### 1. 智能代理
```
@research-assistant "深入研究 React 性能优化"
```
深度研究,综合多个知识来源,生成研究报告。

```
@knowledge-architect "分析我的知识库结构"
```
分析知识结构,优化组织方式,识别知识空白。

```
@knowledge-enricher "增强这个条目: 2026-01-04-105815"
```
自动生成摘要,提取要点,创建术语表。

#### 2. 导入外部知识
```bash
/kb-import ~/Documents/notes --type=markdown
```
导入 Markdown 文件、浏览器书签、Notion、Obsidian。

#### 3. 导出知识库
```bash
/kb-export backup.zip --type=markdown
```
导出为 Markdown、JSON、静态网站或 PDF。

### 第五阶段功能(已实现 ✅)

#### 1. PDF 知识提取
```bash
/kb-from-pdf research-paper.pdf
```
从 PDF 文件提取内容,自动识别结构,支持 OCR 和章节拆分。

#### 2. 网页内容抓取
```bash
/kb-from-url https://react.dev/learn
```
从网页 URL 抓取内容,智能清理,提取正文和元数据。

#### 3. 图片 OCR
```bash
/kb-from-image screenshot.png
```
从图片提取文字,支持代码截图、手写笔记、白板照片。

#### 浏览知识
```bash
/kb-list --by=recent --limit=10
```

## 📊 当前状态

### ✅ 已完成(第一 + 第二 + 第三 + 第四 + 第五阶段)

#### 第一阶段:核心基础
- [x] 目录结构创建
- [x] JSON 索引系统
- [x] 知识条目模板
  - default.md (默认模板)
  - code-snippet.md (代码片段)
  - learning-note.md (学习笔记)
  - project-doc.md (项目文档)
- [x] 核心命令
  - /kb-add - 添加知识
  - /kb-search - 搜索知识
  - /kb-list - 浏览列表
- [x] 测试验证

#### 第二阶段:组织和关联
- [x] /kb-link - 创建知识关联
- [x] /kb-edit - 编辑知识(带版本控制)
- [x] /kb-delete - 删除知识(支持归档)
- [x] /kb-graph - 知识图谱可视化
- [x] Knowledge Manager Skill - 智能辅助
- [x] 双向链接系统
- [x] 关系图谱数据(relationships.json)
- [x] 测试验证(创建 4 个测试条目并建立关联)

#### 第三阶段:版本控制和搜索增强
- [x] /kb-diff - 版本对比(unified/side-by-side/timeline)
- [x] /kb-restore - 版本恢复(支持备份和预览)
- [x] /kb-search 增强 - 高级过滤和排序
- [x] Version Keeper Agent - 知识演化分析
- [x] 版本历史测试数据(4 个版本)

#### 第四阶段:高级特性和智能代理
- [x] Research Assistant Agent - 深度研究和知识综合
- [x] Knowledge Architect Agent - 结构分析和优化
- [x] Knowledge Enricher Agent - 内容增强和质量提升
- [x] /kb-import - 导入外部知识(Markdown/书签/Notion/Obsidian)
- [x] /kb-export - 导出知识库(Markdown/JSON/HTML/PDF)

#### 第五阶段:多源输入系统
- [x] /kb-from-pdf - PDF 知识提取(支持 OCR 和章节拆分)
- [x] /kb-from-url - 网页内容抓取(支持阅读模式和批量导入)
- [x] /kb-from-image - 图片 OCR 和知识提取(支持代码截图、手写笔记、白板)

### 📝 待实现

#### 第三阶段:版本控制
- /kb-diff - 版本对比
- /kb-restore - 版本恢复
- Version Keeper Agent

#### 第四阶段:高级特性
- Sub-agents (研究助手、知识架构师)
- 导入导出功能
- 知识图谱可视化

#### 第五阶段:多源输入
- /kb-from-pdf - PDF 知识提取
- /kb-from-url - 网页内容抓取
- /kb-from-image - 图片 OCR

#### 第六阶段:主动学习
- /kb-learn - 学习计划
- /kb-review - 智能复习
- /kb-teach - 费曼技巧
- /kb-quiz - 测验系统
- Tutor/Student/Quiz-master Agents

## 💡 使用示例

### 添加学习笔记
```bash
/kb-add --type=learning-note --tags=react,hooks
```

### 搜索 React 相关内容
```bash
/kb-search react hooks
```

### 查看最近的知识
```bash
/kb-list --by=recent --limit=10
```

## 📖 详细文档

完整的设计文档和实施计划,请查看:
- [Claude Code 计划文档](C:\Users\zhangsan\.claude\plans\giggly-drifting-milner.md)

## 🔧 技术栈

- **存储**: JSON + Markdown
- **搜索**: ripgrep + jq
- **平台**: Claude Code
- **操作系统**: Windows/Linux/macOS

## 📝 许可

个人知识管理系统,仅供个人使用。

---

**创建时间**: 2025-01-04
**当前版本**: v0.5.0 (第五阶段完成)
**状态**: ✅ 核心功能、组织关联、版本控制、高级特性、多源输入全部完成

## 📝 测试数据

### 第二阶段测试
创建了 4 个测试条目:
1. [2026-01-04-105644] React 基础概念
2. [2026-01-04-105730] JavaScript 异步编程
3. [2026-01-04-105815] React Hooks 深入理解
4. [2026-01-04-105900] 函数组件最佳实践

建立了 3 个关联:
- React Hooks → React 基础 (引用)
- React Hooks → 函数组件最佳实践 (构建于)
- 函数组件最佳实践 → React 基础 (相关)

### 第三阶段测试
创建了 4 个历史版本:
- 2026-01-04-105815.v1.md (初始版本,基础概念)
- 2026-01-04-105815.v2.md (添加细节)
- 2026-01-04-105815.v3.md (添加代码示例)
- 2026-01-04-105815.v4.md (深化理解,添加链接)

可用于测试:
- `/kb-diff` 命令的版本对比功能
- `/kb-restore` 命令的版本恢复功能
- Version Keeper Agent 的演化分析
