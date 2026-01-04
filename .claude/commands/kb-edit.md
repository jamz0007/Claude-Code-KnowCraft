---
argument-hint: <item-id> [--field=title|content|tags|category|all]
description: 编辑知识条目(自动创建版本备份)
allowed-tools: Read, Write, Edit, Bash
---

# /kb-edit - 编辑知识条目

## 功能
编辑现有知识条目,自动创建版本备份,确保不会丢失历史数据。

## 使用方式

### 基本用法
```
/kb-edit 2025-01-04-143052
```
交互式编辑所有字段。

### 编辑特定字段
```
/kb-edit 2025-01-04-143052 --field=title
```
仅编辑标题。

### 编辑内容
```
/kb-edit 2025-01-04-143052 --field=content
```
仅编辑正文内容,保留元数据。

### 编辑标签
```
/kb-edit 2025-01-04-143052 --field=tags
```
编辑标签列表。

### 编辑分类
```
/kb-edit 2025-01-04-143052 --field=category
```
更改分类。

### 编辑所有
```
/kb-edit 2025-01-04-143052 --field=all
```
逐步编辑所有字段。

## 参数说明
- `item-id`: 知识条目 ID (必需)
- `--field`: 要编辑的字段
  - `title`: 标题
  - `content`: 正文内容
  - `tags`: 标签
  - `category`: 分类
  - `all`: 所有字段(默认)

## 工作流程

### 1. 验证条目存在
```
检查 item-id 是否存在于 index.json
```

### 2. 读取当前条目
```
读取 knowledge/items/YYYY/MM-Month/item-id.md
```

### 3. 创建版本备份
```
复制当前文件到 knowledge/.versions/item-id.v{version}.md
例如: 2025-01-04-143052.v1.md
```

### 4. 递增版本号
```yaml
# 版本 1 → 版本 2
version: 1  # 修改前
version: 2  # 修改后
```

### 5. 更新修改时间
```yaml
modified: 2025-01-04T15:30:00Z
```

### 6. 记录变更日志
```yaml
changeLog:
  - { version: 2, date: "2025-01-04T15:30:00Z", summary: "添加代码示例" }
```

### 7. 更新索引
```
更新 index.json 中的元数据:
- modified 时间
- version 版本号
- wordCount 字数
- tags 标签(如果修改)
- category 分类(如果修改)
```

## 版本备份

### 备份文件命名
```
knowledge/.versions/
├── 2025-01-04-143052.v1.md
├── 2025-01-04-143052.v2.md
└── 2025-01-04-143052.v3.md
```

### 备份文件内容
```markdown
---
id: 2025-01-04-143052
title: "原标题"
version: 1
modified: 2025-01-04T14:30:00Z
backupReason: "edit"
backupDate: 2025-01-04T15:30:00Z
---

(原始内容)
```

## 变更日志

### changeLog 字段格式
```yaml
changeLog:
  - version: 2
    date: 2025-01-04T15:30:00Z
    summary: "添加 useState 和 useEffect 示例"
    fields: ["content"]
  - version: 3
    date: 2025-01-04T16:45:00Z
    summary: "更新标签,添加 hooks"
    fields: ["tags"]
```

## 示例

### 编辑标题
```
/kb-edit 2025-01-04-143052 --field=title

当前标题: React Hooks 深入理解
新标题: React Hooks 完全指南

✅ 标题已更新!
版本: 1 → 2
备份已创建: knowledge/.versions/2025-01-04-143052.v1.md
```

### 编辑内容
```
/kb-edit 2025-01-04-143052 --field=content

正在加载内容...
(编辑器打开)

保存后:
✅ 内容已更新!
版本: 2 → 3
新增字数: 156 字
备份已创建: knowledge/.versions/2025-01-04-143052.v2.md
```

### 编辑标签
```
/kb-edit 2025-01-04-143052 --field=tags

当前标签: react, hooks
新标签(逗号分隔): react, hooks, useState, useEffect

✅ 标签已更新!
版本: 3 → 4
新增标签: useState, useEffect
```

### 交互式编辑所有字段
```
/kb-edit 2025-01-04-143052

[1/5] 标题
当前: React Hooks 深入理解
新标题: (直接回车保持不变)

[2/5] 分类
当前: learning
新分类: (learning|code|projects|personal)

[3/5] 标签
当前: react, hooks
新标签: react, hooks, useState

[4/5] 内容
(打开编辑器编辑内容)

[5/5] 变更说明
简要描述本次修改: 添加 useState 示例代码

✅ 编辑完成!
版本: 4 → 5
变更说明: 添加 useState 示例代码
```

## 数据结构

### 编辑后的 frontmatter
```yaml
---
id: 2025-01-04-143052
title: "React Hooks 完全指南"
type: learning-note
category: learning
tags: [react, hooks, useState, useEffect]
created: 2025-01-04T14:30:00Z
modified: 2025-01-04T16:30:00Z
version: 5
links:
  - to: 2025-01-03-102015
    type: references
backlinks: []
changeLog:
  - { version: 2, date: "2025-01-04T15:30:00Z", summary: "更新标题", fields: ["title"] }
  - { version: 3, date: "2025-01-04T16:00:00Z", summary: "添加代码示例", fields: ["content"] }
  - { version: 4, date: "2025-01-04T16:15:00Z", summary: "更新标签", fields: ["tags"] }
  - { version: 5, date: "2025-01-04T16:30:00Z", summary: "添加 useState 示例代码", fields: ["content"] }
---

# React Hooks 完全指南

(内容...)
```

### index.json 更新
```json
{
  "id": "2025-01-04-143052",
  "title": "React Hooks 完全指南",
  "modified": "2025-01-04T16:30:00Z",
  "version": 5,
  "tags": ["react", "hooks", "useState", "useEffect"],
  "category": "learning",
  "wordCount": 342
}
```

## 版本管理

### 查看版本历史
```
/kb-diff 2025-01-04-143052
显示所有版本和变更日志
```

### 恢复到特定版本
```
/kb-restore 2025-01-04-143052 --version=3
恢复到版本 3
```

### 对比两个版本
```
/kb-diff 2025-01-04-143052 --from=2 --to=4
显示版本 2 和 4 的差异
```

## 注意事项

### 版本控制
- 每次编辑都会创建备份,不会丢失历史
- 版本号自动递增
- 变更日志自动记录

### 编辑限制
- ID 字段不能修改(这是条目的唯一标识)
- created 时间不能修改(创建时间不可变)
- links 和 backlinks 应该使用 `/kb-link` 命令管理

### 性能考虑
- 备份文件保存在 `knowledge/.versions/` 目录
- 长期使用可能积累大量备份文件
- 建议定期清理旧版本(保留最近 10 个版本)
- 可以使用 `/kb-cleanup` 命令清理旧版本(待实现)

### 最佳实践
1. **频繁保存**: 每次重要修改都创建版本
2. **清晰的变更说明**: 在 changeLog 中记录修改原因
3. **定期备份**: 考虑将整个知识库备份到外部存储
4. **版本命名**: 使用描述性的变更总结

## 错误处理

### 条目不存在
```
❌ 错误: 条目 2025-01-99-999999 不存在
请使用 /kb-list 查看所有条目
```

### 备份失败
```
❌ 错误: 无法创建版本备份
检查 knowledge/.versions/ 目录权限
```

### 索引更新失败
```
⚠️  警告: 条目已更新,但索引更新失败
请手动运行 /kb-reindex 重建索引
```

## 扩展功能(未来)

### 批量编辑
```
/kb-edit --batch --tag=react --field=category
批量修改所有 react 标签的条目的分类
```

### 模板替换
```
/kb-edit 2025-01-04-143052 --template=code-snippet
使用新模板重新格式化条目
```

### 外部编辑器
```
/kb-edit 2025-01-04-143052 --editor=vscode
使用 VSCode 打开文件进行编辑
```
