---
argument-hint: [--by=recent|category|tags|date] [--category=code|projects|learning|personal] [--tag=tag] [--limit=N] [--format=short|detailed]
description: 列出知识库中的条目
allowed-tools: Read, Bash, jq
---

# /kb-list - 列出知识条目

## 功能
浏览个人知识库中的条目,支持多种排序和过滤方式。

## 使用方式

### 列出最近的条目
```
/kb-list --by=recent --limit=10
```
显示最近创建的 10 条知识。

### 按分类浏览
```
/kb-list --by=category
```
按分类统计并显示所有分类的条目数量。

### 按分类过滤
```
/kb-list --category=learning
```
只显示 learning 分类的条目。

### 按标签浏览
```
/kb-list --by=tags
```
显示所有标签及其使用次数。

### 按标签过滤
```
/kb-list --tag=react
```
只显示包含 "react" 标签的条目。

### 详细格式
```
/kb-list --by=recent --limit=5 --format=detailed
```
使用详细格式显示,包含更多元数据。

## 参数说明
- `--by`: 排序/分组方式
  - `recent`: 按创建时间(默认)
  - `category`: 按分类
  - `tags`: 按标签
  - `date`: 按日期
- `--category`: 过滤分类
- `--tag`: 过滤标签
- `--limit`: 显示数量 (默认 20)
- `--format`: 输出格式
  - `short`: 简短格式(默认)
  - `detailed`: 详细格式

## 输出格式

### 简短格式
```
最近的知识条目 (共 5 条):

1. [2025-01-04-143052] React Hooks 深入理解
   创建: 2025-01-04 14:30 | 标签: react, hooks

2. [2025-01-03-102015] JavaScript 异步编程
   创建: 2025-01-03 10:20 | 标签: javascript, async
```

### 详细格式
```
最近的知识条目 (共 5 条):

1. [2025-01-04-143052] React Hooks 深入理解
   类型: learning-note
   分类: learning
   标签: react, hooks, useState
   创建: 2025-01-04 14:30
   修改: 2025-01-04 15:07
   版本: 2
   链接: 2 个

   摘要: useState 是 React 提供的最基础的 Hook...
```

### 按分类统计
```
知识库分类统计:

code (代码片段): 15 条
  - react: 8 条
  - javascript: 5 条
  - python: 2 条

projects (项目文档): 12 条
learning (学习笔记): 23 条
personal (个人思考): 8 条

总计: 58 条
```

### 按标签统计
```
标签使用统计 (前 20 个):

react (15 次)
javascript (12 次)
hooks (10 次)
async (8 次)
...
```

## 示例

### 查看今天添加的知识
```
/kb-list --by=date --limit=50 | rg "2025-01-04"
```

### 查看 React 相关的所有知识
```
/kb-list --tag=react --format=detailed
```

### 按分类浏览
```
/kb-list --by=category

知识库概览:
- code: 15 条
- projects: 12 条
- learning: 23 条
- personal: 8 条

总计: 58 条知识条目
```

## 注意事项
- 如果没有指定过滤条件,显示所有条目
- 标签和分类过滤可以组合使用
- 使用 jq 从 index.json 读取数据
- 结果按创建时间降序排列
