---
argument-hint: <item-id> --version=N [--backup] [--reason=text]
description: 从历史版本恢复知识条目
allowed-tools: Read, Write, Edit, Bash
---

# /kb-restore - 版本恢复

## 功能
从历史版本恢复知识条目,支持备份当前版本和递增版本号。

## 使用方式

### 基本用法
```
/kb-restore 2026-01-04-105815 --version=3

从版本 3 恢复,当前版本自动备份
```

### 恢复并指定原因
```
/kb-restore 2026-01-04-105815 --version=2 --reason="误删重要内容"

恢复并记录恢复原因
```

### 恢复前不备份
```
/kb-restore 2026-01-04-105815 --version=3 --no-backup

直接恢复,不备份当前版本(谨慎使用)
```

### 查看可用版本
```
/kb-restore 2026-01-04-105815 --list

列出所有可用的历史版本
```

## 参数说明

- `item-id`: 知识条目 ID (必需)
- `--version`: 要恢复的版本号 (必需)
- `--backup`: 是否备份当前版本 (默认: true)
- `--no-backup`: 不备份当前版本
- `--reason`: 恢复原因 (记录到变更日志)
- `--list`: 列出可用版本而不执行恢复

## 工作流程

### 1. 验证请求
```
检查条目是否存在
检查目标版本是否存在
确认当前版本与目标版本不同
```

### 2. 可选:备份当前版本
```
如果使用 --backup (默认):
复制当前文件到 .versions/
命名为 item-id.v{current+1}.md
标记为恢复前备份
```

### 3. 读取历史版本
```
从 .versions/ 目录读取:
knowledge/.versions/item-id.v{version}.md
```

### 4. 更新元数据
```
修改 frontmatter:
- version: 递增到新版本号
- modified: 更新为当前时间
- changeLog: 添加恢复记录
```

### 5. 写入主文件
```
将历史版本内容写入:
knowledge/items/YYYY/MM-Month/item-id.md
```

### 6. 更新索引
```
更新 index.json:
- 更新 modified 时间
- 更新 version 号
- 更新字数统计
```

## 输出示例

### 基本恢复
```
/kb-restore 2026-01-04-105815 --version=3

正在恢复...
  条目: React Hooks 深入理解
  从版本: 5
  到版本: 3

✅ 恢复完成!

详细信息:
  当前版本: 5 → 3
  新版本号: 6
  备份文件: knowledge/.versions/2026-01-04-105815.v5.md
  恢复时间: 2025-01-04 18:00

变更内容:
  - 字数: 225 → 195 (-30 字)
  - 段落: 12 → 9 (-3 段)
  - 标签: 6 → 4 (移除了 useEffect, best-practices)

注意事项:
  - 版本 5 已备份,可以再次恢复
  - 链接和反向链接保持不变
```

### 带原因的恢复
```
/kb-restore 2026-01-04-105815 --version=2 --reason="误删重要示例代码"

正在恢复...
  条目: React Hooks 深入理解
  从版本: 5
  到版本: 2
  原因: 误删重要示例代码

✅ 恢复完成!

新版本信息:
  版本号: 6
  恢复原因: 误删重要示例代码
  恢复时间: 2025-01-04 18:05
```

### 列出可用版本
```
/kb-restore 2026-01-04-105815 --list

可用版本历史:

版本 1 (2025-01-04 14:30)
  字数: 156
  标签: react, hooks
  变更: 初始创建

版本 2 (2025-01-04 15:30)
  字数: 180
  标签: react, hooks, frontend
  变更: 添加 useContext 说明

版本 3 (2025-01-04 16:00)
  字数: 195
  标签: react, hooks, frontend, useState
  变更: 添加 useState 示例 ⭐ 推荐版本

版本 4 (2025-01-04 16:45)
  字数: 210
  标签: react, hooks, frontend, useState, useEffect
  变更: 添加 useEffect 详细说明

版本 5 (2025-01-04 17:30) [当前]
  字数: 225
  标签: react, hooks, frontend, useState, useEffect, best-practices
  变更: 添加最佳实践

使用示例:
  /kb-restore 2026-01-04-105815 --version=3
```

## 恢复后的 frontmatter

### 恢复前 (版本 5)
```yaml
---
id: 2026-01-04-105815
title: "React Hooks 深入理解"
version: 5
modified: 2025-01-04T17:30:00Z
changeLog:
  - { version: 2, date: "...", summary: "添加 useContext" }
  - { version: 3, date: "...", summary: "添加 useState" }
  - { version: 4, date: "...", summary: "添加 useEffect" }
  - { version: 5, date: "...", summary: "添加最佳实践" }
---
```

### 恢复后 (新版本 6)
```yaml
---
id: 2026-01-04-105815
title: "React Hooks 深入理解"
version: 6
modified: 2025-01-04T18:00:00Z
changeLog:
  - { version: 2, date: "...", summary: "添加 useContext" }
  - { version: 3, date: "...", summary: "添加 useState" }
  - { version: 4, date: "...", summary: "添加 useEffect" }
  - { version: 5, date: "...", summary: "添加最佳实践" }
  - { version: 6, date: "2025-01-04T18:00:00Z", summary: "从版本 3 恢复", restoreFrom: 3, reason: "误删重要内容" }
---
```

## 版本历史管理

### 版本编号规则
```
原始版本: 1, 2, 3, 4, 5
恢复后: 6 (版本 3 的内容,但版本号继续递增)

这样保证了:
- 版本号单调递增
- 时间顺序清晰
- 不会造成混淆
```

### 备份文件命名
```
恢复前自动备份当前版本:
2026-01-04-105815.v5.md → 恢复前版本 5 的备份

如果再次恢复:
2026-01-04-105815.v6.md → 恢复前版本 6 的备份
```

## 高级功能

### 批量恢复
```
/kb-restore --batch --tag=react --version=1

恢复所有 react 标签的条目到版本 1
```

### 条件恢复
```
/kb-restore 2026-01-04-105815 --condition="before:2025-01-04"

恢复到 2025-01-04 之前的最新版本
```

### 交互式恢复
```
/kb-restore 2026-01-04-105815 --interactive

显示版本历史,交互式选择:
[1] 版本 1 - 初始创建
[2] 版本 2 - 添加 useContext
[3] 版本 3 - 添加 useState ⭐
[4] 版本 4 - 添加 useEffect
[5] 版本 5 - 添加最佳实践 [当前]

选择要恢复的版本 (1-5): 3
确认恢复到版本 3? (yes/no): yes
```

### 预览恢复
```
/kb-restore 2026-01-04-105815 --version=3 --preview

预览恢复内容,不实际执行:

将会发生的变化:
  - 字数: 225 → 195 (-30 字, -13.3%)
  - 段落: 12 → 9 (-3 段)
  - 标签: react, hooks, frontend, useState, useEffect, best-practices
       → react, hooks, frontend, useState

将删除的内容:
  - useEffect 详细说明章节
  - 最佳实践章节
  - 2 个标签

将恢复的内容:
  + 原始的 useState 说明
  + 原始的结构

继续恢复? (yes/no):
```

## 注意事项

### 数据安全
1. **默认备份**: 恢复前自动备份当前版本
2. **版本保护**: 版本历史不会丢失
3. **可逆操作**: 可以再次恢复回之前的版本

### 链接处理
```
恢复操作不会影响:
- links 字段 (前向链接)
- backlinks 字段 (反向链接)
- relationships.json 中的边

如果需要更新链接,手动使用 /kb-link 管理
```

### 索引更新
```
恢复后自动更新:
- index.json 中的元数据
- 字数统计
- 标签列表
- 分类信息
```

### 性能考虑
- 恢复操作很快 (< 1 秒)
- 版本历史文件占用空间很小
- 建议定期清理旧版本 (保留最近 10-20 个)

## 错误处理

### 版本不存在
```
❌ 错误: 版本 10 不存在
可用版本: 1, 2, 3, 4, 5
使用 /kb-restore 2026-01-04-105815 --list 查看所有版本
```

### 条目不存在
```
❌ 错误: 条目 2026-01-99-999999 不存在
请使用 /kb-list 查看所有条目
```

### 目标版本与当前相同
```
⚠️  警告: 当前已经是版本 3
无需恢复
```

### 权限错误
```
❌ 错误: 无法写入文件
检查文件权限: knowledge/items/2026/01-January/2026-01-04-105815.md
```

## 实用场景

### 1. 撤销错误编辑
```
不小心删除了重要内容:
/kb-diff item-id  # 查看变化
/kb-restore item-id --version=5 --reason="撤销错误编辑"
```

### 2. 回退到简洁版本
```
内容变得过于冗长:
/kb-restore item-id --version=2 --reason="简化内容"
```

### 3. 恢复早期思路
```
想回到早期的理解方式:
/kb-restore item-id --version=1
```

### 4. 对比后恢复
```
/kb-diff item-id --format=timeline
# 发现版本 3 最好
/kb-restore item-id --version=3
```

## 与其他命令的配合

### 查看差异后恢复
```
/kb-diff 2026-01-04-105815 --from=3 --to=5
# 发现版本 5 不如版本 3
/kb-restore 2026-01-04-105815 --version=3
```

### 恢复后继续编辑
```
/kb-restore 2026-01-04-105815 --version=3
/kb-edit 2026-01-04-105815 --field=content
# 在版本 3 的基础上继续改进
```

### 查看恢复效果
```
/kb-restore 2026-01-04-105815 --version=3
/kb-diff 2026-01-04-105815 --from=5 --to=6
# 查看恢复前后的差异
```

## 最佳实践

### 1. 定期创建重要版本
```
完成重要修改后:
/kb-edit item-id --field=content
# 自动创建版本备份
```

### 2. 使用有意义的变更说明
```
/kb-restore item-id --version=3 --reason="恢复到添加 useState 之前的版本"
```

### 3. 预览后再恢复
```
/kb-restore item-id --version=3 --preview
# 先看预览,确认无误后再实际恢复
```

### 4. 定期清理旧版本
```
/kb-cleanup --versions --keep=10
保留最近 10 个版本,删除更早的版本
```

## 版本清理建议

### 保留策略
```
重要条目: 保留所有版本
普通条目: 保留最近 10-20 个版本
测试条目: 保留最近 5 个版本
```

### 清理频率
```
每月清理一次
或手动触发清理
```

### 归档旧版本
```
/kb-archive --versions --older-than=90

将 90 天前的版本移归档存储
```

## 扩展功能(未来)

### 智能恢复
```
/kb-restore item-id --smart

AI 分析历史版本,推荐最佳版本
```

### 部分恢复
```
/kb-restore item-id --version=3 --section="最佳实践"

只恢复特定章节,其他内容保持不变
```

### 合并版本
```
/kb-restore item-id --merge=2,3,5

合并多个版本的内容
```

### 恢复历史
```
/kb-restore --history item-id

显示该条目的恢复历史
```
