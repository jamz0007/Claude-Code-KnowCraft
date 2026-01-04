---
argument-hint: <source-id> <target-id> [--type=references|builds-on|related|contradicts|example-of|application]
description: 在两个知识条目之间创建关联
allowed-tools: Read, Write, Edit, Bash
---

# /kb-link - 创建知识关联

## 功能
在两个知识条目之间创建双向关联,建立知识网络。

## 使用方式

### 基本用法
```
/kb-link 2025-01-04-143052 2025-01-03-102015
```
在两个条目之间创建默认的"相关"关联。

### 指定关联类型
```
/kb-link 2025-01-04-143052 2025-01-03-102015 --type=references
```
创建"引用"类型的关联。

### 使用"current"引用当前工作
```
/kb-link current 2025-01-03-102015 --type=builds-on
```
将当前工作内容与指定条目关联。

## 参数说明
- `source-id`: 源条目 ID(或 "current")
- `target-id`: 目标条目 ID
- `--type`: 关联类型
  - `references`: 引用或提及(默认)
  - `builds-on`: 基于或扩展
  - `related`: 主题相关
  - `contradicts`: 对立观点
  - `example-of`: 示例
  - `application`: 应用

## 关联类型说明

### references (引用)
一个条目引用或提及另一个条目:
- 引用某个概念
- 提到某项研究
- 参考某个实现

### builds-on (基于)
一个条目基于另一个条目扩展:
- 在基础上添加新内容
- 改进或优化
- 补充细节

### related (相关)
两个条目主题相关:
- 讨论相似话题
- 使用相似技术
- 解决相似问题

### contradicts (对立)
两个条目观点对立:
- 不同解决方案
- 相反观点
- 对比讨论

### example-of (示例)
一个条目是另一个概念的应用示例:
- 实际案例
- 代码示例
- 实践应用

### application (应用)
一个条目应用了另一个条目的理论:
- 理论到实践
- 方法应用
- 技术落地

## 工作流程

1. **验证条目存在**:
   - 检查源条目 ID 是否有效
   - 检查目标条目 ID 是否有效

2. **读取源条目**:
   - 读取源条目的 frontmatter
   - 检查是否已存在该链接
   - 避免重复链接

3. **更新源条目**:
   - 在 `links` 数组中添加新链接
   - 格式: `{ to: "target-id", type: "link-type" }`

4. **更新目标条目**:
   - 在目标条目的 `backlinks` 数组中添加反向链接
   - 格式: `{ from: "source-id", type: "link-type" }`

5. **更新索引**:
   - 更新 index.json 中的链接计数
   - 更新 relationships.json 图数据

6. **更新关系图谱**:
   - 在 relationships.json 中添加边
   - 格式: `{ from: "source", to: "target", type: "link-type", strength: "normal" }`

## 示例

### 创建引用关联
```
/kb-link 2025-01-04-143052 2025-01-03-102015 --type=references

✅ 成功创建关联!
源: 2025-01-04-143052 (React Hooks 深入理解)
目标: 2025-01-03-102015 (React 基础概念)
类型: references

源条目现在引用了目标条目。
目标条目的 backlinks 已自动更新。
```

### 查看条目的所有关联
```bash
/kb-list --format=detailed | rg "2025-01-04-143052"

[2025-01-04-143052] React Hooks 深入理解
  链接: 2 个
  反向链接: 1 个

  链接:
  → references: 2025-01-03-102015 (React 基础概念)
  → builds-on: 2025-01-02-084530 (函数组件)

  反向链接:
  ← from: 2025-01-05-091234 (自定义 Hook)
```

### 链接当前工作
```
# 你正在编辑一段代码
/kb-link current 2025-01-04-143052 --type=application

✅ 成功!
当前内容已链接到: React Hooks 深入理解
```

## 数据结构

### 源条目的 links 字段
```yaml
---
links:
  - to: 2025-01-03-102015
    type: references
    created: 2025-01-04T14:30:00Z
  - to: 2025-01-02-084530
    type: builds-on
    created: 2025-01-04T14:35:00Z
---
```

### 目标条目的 backlinks 字段
```yaml
---
backlinks:
  - from: 2025-01-04-143052
    type: references
    context: "在讨论 Hooks 时引用"
    created: 2025-01-04T14:30:00Z
  - from: 2025-01-05-091234
    type: application
    context: "应用了 useState"
    created: 2025-01-05T10:20:00Z
---
```

### relationships.json 边数据
```json
{
  "from": "2025-01-04-143052",
  "to": "2025-01-03-102015",
  "type": "references",
  "strength": "normal",
  "created": "2025-01-04T14:30:00Z"
}
```

## 注意事项
- 不能创建自链接(同一个条目链接到自己)
- 避免重复链接(同一对条目同一种类型)
- 链接应该有意义,避免过度链接
- 定期检查和清理断开的链接
