---
argument-hint: [query] [--tag=tag1,tag2] [--category=code|projects|learning|personal] [--after=DATE] [--before=DATE] [--type=type] [--limit=N] [--sort=relevance|newest|oldest|modified] [--format=short|detailed] [--exact] [--regex]
description: 在知识库中搜索内容(支持全文搜索和高级过滤)
allowed-tools: Read, Grep, Glob, Bash
---

# /kb-search - 搜索知识库

## 功能
在个人知识库中搜索相关内容,支持全文搜索、元数据过滤、正则表达式和多种排序方式。

## 使用方式

### 基本搜索
```
/kb-search react hooks
```
在所有知识条目中搜索 "react hooks"。

### 按标签过滤
```
/kb-search --tag=react 性能优化
```
只在标签包含 "react" 的条目中搜索。

### 按分类过滤
```
/kb-search --category=learning javascript
```
只在 "learning" 分类中搜索。

### 按日期范围过滤
```
/kb-search --after=2025-01-01 --before=2025-01-31 react
```
只搜索 2025 年 1 月创建的条目。

### 组合过滤
```
/kb-search --tag=react --category=learning --limit=10 hooks
```
多个条件组合搜索,最多显示 10 条结果。

### 按相关性排序
```
/kb-search --sort=relevance react
```
按相关性排序结果(默认)。

### 按时间排序
```
/kb-search --sort=newest react
```
按创建时间排序。

### 按修改时间排序
```
/kb-search --sort=modified react
```
按最后修改时间排序。

### 按类型过滤
```
/kb-search --type=learning-note hooks
```
只搜索学习笔记类型的条目。

### 精确匹配
```
/kb-search --exact "React Hooks"
```
精确匹配 "React Hooks",不区分大小写。

### 正则表达式搜索
```
/kb-search --regex "use[A-Z][a-z]+"
```
使用正则表达式搜索,匹配 useState、useEffect 等。

### 详细格式输出
```
/kb-search --format=detailed --limit=5 react
```
显示详细信息,包括链接、反向链接等。

### 组合高级搜索
```
/kb-search --tag=react,frontend --category=learning --after=2025-01-01 --sort=relevance --limit=10 --format=detailed hooks
```
多个条件组合搜索。

### 无参数搜索(列出所有)
```
/kb-search
```
显示所有知识条目(按创建时间排序)。

## 参数说明
- `query`: 搜索关键词(可选,未提供时列出所有条目)
- `--tag`: 按标签过滤,多个标签用逗号分隔 (OR 逻辑)
- `--tag-all`: 所有标签都必须匹配 (AND 逻辑)
- `--category`: 按分类过滤
- `--type`: 按条目类型过滤
- `--after`: 起始日期 (YYYY-MM-DD)
- `--before`: 结束日期 (YYYY-MM-DD)
- `--limit`: 最大结果数量 (默认 20)
- `--sort`: 排序方式
  - `relevance`: 相关性 (默认)
  - `newest`: 最新创建
  - `oldest`: 最旧创建
  - `modified`: 最近修改
  - `links`: 链接数量
  - `backlinks`: 反向链接数量
- `--format`: 输出格式
  - `short`: 简短格式 (默认)
  - `detailed`: 详细格式
  - `id-only`: 仅显示 ID
- `--exact`: 精确匹配(禁用模糊搜索)
- `--regex`: 使用正则表达式
- `--case-sensitive`: 区分大小写

## 搜索策略

### 相关性评分(增强版)
- **标题精确匹配**: 15 分
- **标题部分匹配**: 10 分
- **标签匹配**: 5 分/标签
- **分类匹配**: 3 分
- **ID 匹配**: 20 分
- **正文匹配**: 每次 1 分(最多 10 分)
- **链接数量**: 每个链接 +0.5 分

### 搜索流程
1. 使用 ripgrep 进行全文搜索
2. 使用 jq 查询 index.json 进行元数据过滤
3. 应用高级过滤条件(标签、分类、日期等)
4. 合并结果并计算相关性评分
5. 按指定方式排序
6. 格式化输出前 N 条结果

### 高级过滤逻辑

#### 标签过滤
```
--tag=react,hooks     → 匹配 react OR hooks
--tag-all=react,hooks → 匹配 react AND hooks
```

#### 日期过滤
```
--after=2025-01-01  → created >= 2025-01-01
--before=2025-01-31 → created <= 2025-01-31
```

#### 类型过滤
```
--type=learning-note  → 仅学习笔记
--type=code-snippet   → 仅代码片段
```

#### 链接过滤
```
--has-links     → 有前向链接的条目
--has-backlinks → 有反向链接的条目
--isolated      → 孤立条目(无链接)
```

## 输出格式

### 简短格式 (默认)
```
[2026-01-04-105815] React Hooks 深入理解
标签: react, hooks, frontend | 分类: learning
创建: 2026-01-04 10:58 | 修改: 2026-01-04 11:00
相关度: ⭐⭐⭐⭐⭐ (98分)

useState 是 React 提供的最基础的 Hook,用于在函数组件中添加状态...
```

### 详细格式
```
[2026-01-04-105815] React Hooks 深入理解
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
类型: learning-note
分类: learning
标签: react, hooks, frontend
创建: 2026-01-04 10:58
修改: 2026-01-04 11:00
版本: 1
字数: 210

链接 (2 个):
  → references: 2026-01-04-105644 (React 基础概念)
  → builds-on: 2026-01-04-105900 (函数组件最佳实践)

反向链接 (0 个)

摘要:
React Hooks 是 React 16.8 引入的新特性,让函数组件拥有状态和其他 React 特性。

常用 Hooks:
- useState: 状态管理
- useEffect: 副作用处理
- useContext: 上下文共享

文件: knowledge/items/2026/01-January/2026-01-04-105815.md
```

### 仅 ID 格式
```
2026-01-04-105815
2026-01-04-105644
2026-01-04-105730
```

### 统计信息
```
搜索完成!找到 3 个结果 (0.05 秒)

应用过滤:
  标签: react, hooks
  分类: learning
  日期: 2025-01-01 ~ 2025-01-31

结果排序: 相关性
搜索范围: 5 个条目
匹配率: 60% (3/5)
```

## 示例

### 搜索 React 相关内容
```
/kb-search react hooks useState

[2025-01-04-143052] React Hooks 深入理解
类型: learning-note | 分类: learning | 标签: react, hooks, useState
创建: 2025-01-04 14:30

useState 是 React 提供的最基础的 Hook,用于在函数组件中添加状态...
```

### 按标签和日期过滤
```
/kb-search --tag=javascript --after=2025-01-01 异步编程
```

### 搜索孤立条目
```
/kb-search --isolated

找到没有链接的条目,帮助发现需要关联的知识。
```

### 搜索高链接条目
```
/kb-search --has-links --sort=links --limit=10

查找链接最多的条目(核心知识)。
```

### 正则表达式搜索
```
/kb-search --regex "use[A-Z][a-z]+"

搜索结果:
[2026-01-04-105815] React Hooks 深入理解
匹配: useState, useEffect, useContext

[2026-01-04-105900] 函数组件最佳实践
匹配: useMemo, useCallback
```

### 组合搜索示例
```
/kb-search --tag=react --type=learning-note --sort=links --format=detailed --limit=5

查找:
- 包含 react 标签
- 类型为学习笔记
- 按链接数量排序
- 显示详细信息
- 最多 5 条结果
```

### 搜索特定版本
```
/kb-search --min-version=3 --sort=version

查找至少编辑过 3 次的条目(成熟的知识)。
```

### 搜索长内容
```
/kb-search --min-words=200 --sort=words

查找详细的知识条目(字数 >= 200)。
```

## 性能说明

### 搜索性能
- 使用 ripgrep 进行快速全文搜索(毫秒级)
- 使用 jq 进行 JSON 查询(毫秒级)
- 适合中小规模知识库 (< 1000 条)
- 大规模知识库建议使用搜索引擎

### 性能优化技巧

#### 1. 使用精确过滤
```
慢: /kb-search react (全文搜索)
快: /kb-search --tag=react (仅元数据查询)
```

#### 2. 限制结果数量
```
/kb-search --limit=10 react
```

#### 3. 使用日期范围
```
/kb-search --after=2025-01-01 react
缩小搜索范围
```

#### 4. 避免复杂正则
```
慢: /kb-search --regex ".*?(react|hooks|useState).*?"
快: /kb-search react hooks useState
```

## 搜索技巧

### 1. 从宽泛到精确
```
第一步: /kb-search react
第二步: /kb-search --tag=react hooks
第三步: /kb-search --tag=react --exact "useState"
```

### 2. 发现孤立知识
```
/kb-search --isolated --format=detailed

找到没有链接的条目,然后使用 /kb-link 创建关联
```

### 3. 追踪知识演化
```
/kb-search --sort=modified --limit=10

查看最近修改的条目
```

### 4. 查找核心知识
```
/kb-search --has-links --sort=links --limit=10

链接最多的条目通常是核心概念
```

### 5. 按学习路径查找
```
/kb-search --tag-all=basic,react --sort=newest

查找既包含 basic 又包含 react 标签的条目
```

### 6. 发现相关主题
```
/kb-search --regex "(React|Vue|Angular)"

查找所有前端框架相关内容
```

### 7. 查找高质量内容
```
/kb-search --min-version=3 --min-words=300 --sort=links

查找编辑次数多、内容长、链接多的条目
```

### 8. 按类型浏览
```
/kb-search --type=code-snippet

浏览所有代码片段
```

## 高级用法

### 搜索并导出
```
/kb-search --format=id-only react > react-ids.txt
批量导出搜索结果
```

### 搜索后批量操作
```
/kb-search --format=id-only --tag=react | xargs -I {} /kb-link {} current
为搜索结果批量创建链接
```

### 搜索并统计
```
/kb-search --tag=react --format=id-only | wc -l
统计 react 标签的条目数量
```

### 搜索并可视化
```
/kb-search --tag=react --format=id-only | xargs -I {} echo "Node: {}"
用于生成自定义可视化
```

## 常见搜索模式

### 查找学习资料
```
/kb-search --type=learning-note --tag-all=tutorial,beginner
```

### 查找代码示例
```
/kb-search --type=code-snippet --min-words=100
```

### 查找项目文档
```
/kb-search --category=projects --sort=modified
```

### 查找个人思考
```
/kb-search --category=personal --format=detailed
```

### 查找待整理内容
```
/kb-search --isolated --tag=temp
```

## 搜索结果操作

### 查看搜索结果
```
/kb-search react
# 找到 [2026-01-04-105815]

/kb-read 2026-01-04-105815
# 读取完整内容(需要实现 /kb-read 命令)
```

### 编辑搜索结果
```
/kb-search react
# 找到 [2026-01-04-105815]

/kb-edit 2026-01-04-105815 --field=tags
```

### 创建关联
```
/kb-search react hooks
# 找到相关条目后

/kb-link id1 id2 --type=related
```

## 注意事项

### 1. 搜索词大小写
- 默认不区分大小写
- 使用 --case-sensitive 区分大小写

### 2. 特殊字符
- 正则表达式模式需要转义特殊字符
- 精确模式自动转义

### 3. 空结果处理
- 检查搜索词拼写
- 尝试放宽过滤条件
- 使用 --list 查看所有条目

### 4. 性能警告
- 复杂正则表达式可能较慢
- 大量结果建议使用 --limit
- 全文扫描在大型知识库中较慢

## 搜索快捷方式

### 快速查找
```
alias kbs='/kb-search'
kbs react hooks
```

### 查找并打开
```
/kb-search-and-open react
搜索并直接打开第一个结果
```

### 保存搜索
```
/kb-search --tag=react --save=daily-react-search
保存常用搜索查询
```
