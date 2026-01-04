---
argument-hint: <title> --tags=TAGS [--duration=TIME] [--goal=TEXT] [--items=IDS]
description: 创建学习计划和路径
allowed-tools: Read, Write, Edit, Bash
---

# /kb-learn - 创建学习计划

## 功能
创建结构化的学习计划，定义学习目标，追踪学习进度，基于知识图谱生成学习路径。

## 使用方式

### 创建学习计划
```
/kb-learn "深入掌握 React Hooks" --tags=react,hooks --duration="4 weeks" --goal="能够熟练使用 Hooks 开发复杂应用"
```

### 基于现有条目创建计划
```
/kb-learn "React 完整学习路径" --items="2026-01-04-105644,2026-01-04-105815,2026-01-04-105900"

自动包含指定条目到学习计划
```

### 快速创建
```
/kb-learn "JavaScript 异步编程"

交互式创建学习计划
```

### 查看学习计划
```
/kb-learn --list

显示所有学习计划
```

### 查看计划进度
```
/kb-learn --progress "learn-react-hooks"

显示学习进度
```

## 参数说明

- `title`: 学习计划标题 (必需)
- `--tags`: 相关标签 (用于筛选知识条目)
- `--duration`: 预计学习时长 (例如: "2 weeks", "30 days", "4 weeks")
- `--goal`: 学习目标描述
- `--items`: 包含的知识条目 ID (逗号分隔)
- `--milestones`: 里程碑 (JSON 格式)
- `--daily`: 每日学习时间 (例如: "2 hours")
- `--priority`: 优先级 (high|medium|low)
- `--list`: 列出所有计划
- `--progress`: 查看进度
- `--complete`: 标记计划完成

## 学习计划结构

### 基本信息
```
计划 ID: learn-react-hooks
标题: 深入掌握 React Hooks
创建时间: 2026-01-04
状态: in-progress
优先级: high
```

### 学习目标
```
总体目标: 能够熟练使用 Hooks 开发复杂应用

具体目标:
1. 理解 Hooks 原理
2. 掌握常用 Hooks
3. 能够自定义 Hooks
4. 性能优化实践
```

### 时间规划
```
总时长: 4 weeks
每日学习: 2 小时
总学习时间: 56 小时

开始时间: 2026-01-04
预计完成: 2026-01-28
```

### 知识条目
```
包含的条目:
- [2026-01-04-105644] React 基础概念
- [2026-01-04-105815] React Hooks 深入理解
- [2026-01-04-105900] 函数组件最佳实践

推荐阅读顺序:
1. React 基础概念 →
2. React Hooks 深入理解 →
3. 函数组件最佳实践
```

### 里程碑
```
Week 1 (2026-01-04 - 2026-01-10):
  目标: 掌握基础 Hooks (useState, useEffect)
  条目: React 基础概念, React Hooks 深入理解
  状态: 未开始

Week 2 (2026-01-11 - 2026-01-17):
  目标: 理解 Hooks 规则和原理
  条目: React Hooks 深入理解
  状态: 未开始

Week 3 (2026-01-18 - 2026-01-24):
  目标: 实践项目和自定义 Hooks
  条目: 函数组件最佳实践
  状态: 未开始

Week 4 (2026-01-25 - 2026-01-31):
  目标: 性能优化和最佳实践
  条目: 函数组件最佳实践, React Hooks 深入理解
  状态: 未开始
```

## 输出示例

### 创建学习计划
```
/kb-learn "深入掌握 React Hooks" --tags=react,hooks --duration="4 weeks" --goal="能够熟练使用 Hooks 开发复杂应用" --items="2026-01-04-105644,2026-01-04-105815,2026-01-04-105900"

⏳ 正在分析知识库...

找到 3 个相关条目:
- [2026-01-04-105644] React 基础概念
- [2026-01-04-105815] React Hooks 深入理解
- [2026-01-04-105900] 函数组件最佳实践

分析关联:
→ React Hooks 深入理解 引用了 React 基础概念
→ React Hooks 深入理解 构建于 函数组件最佳实践

✅ 学习计划创建完成!

计划 ID: learn-react-hooks
标题: 深入掌握 React Hooks
状态: in-progress
优先级: high

学习目标:
能够熟练使用 Hooks 开发复杂应用

时间规划:
总时长: 4 weeks
每日学习: 2 小时 (建议)
开始时间: 2026-01-04
预计完成: 2026-01-28

包含条目: 3 个
推荐学习顺序:
1. React 基础概念
2. React Hooks 深入理解
3. 函数组件最佳实践

里程碑:
Week 1 (1月4日-10日): 掌握基础 Hooks
  - 理解 useState 和 useEffect
  - 学习 Hooks 规则
  ✅ 已完成: 0/3

Week 2 (1月11日-17日): 深入理解
  - 自定义 Hooks
  - 性能考虑
  ✅ 已完成: 0/2

Week 3 (1月18日-24日): 实践应用
  - 实际项目
  - 代码重构
  ✅ 已完成: 0/1

Week 4 (1月25日-31日): 巩固提升
  - 最佳实践
  - 常见陷阱
  ✅ 已完成: 0/2

学习进度: 0% (0/8 任务完成)

下次复习: 2026-01-11 (Week 1 结束后)

保存位置: learning/plans/learn-react-hooks.json

下一步:
1. 开始学习第一周内容
2. 标记已完成的任务
3. 记录学习笔记

相关命令:
/kb-learn --progress "learn-react-hooks"  # 查看进度
/kb-learn --complete "learn-react-hooks"  # 标记完成
```

### 查看所有计划
```
/kb-learn --list

📚 学习计划列表

进行中 (2 个):
1. learn-react-hooks
   标题: 深入掌握 React Hooks
   进度: 0% (0/8)
   截止: 2026-01-28
   优先级: high

2. learn-javascript-async
   标题: JavaScript 异步编程精通
   进度: 25% (2/8)
   截止: 2026-01-15
   优先级: medium

已完成 (5 个):
- learn-python-basics (2025-12-01 完成)
- learn-git-workflow (2025-12-10 完成)
...

计划中 (1 个):
- learn-type-script (未开始)
```

### 查看进度
```
/kb-learn --progress "learn-react-hooks"

📊 学习进度报告: 深入掌握 React Hooks

总体进度: 12.5% (1/8 任务完成)

时间进度:
  已用: 3 天
  剩余: 25 天
  进度: 正常 (预计按时完成)

里程碑进度:

Week 1 (1月4日-10日): 掌握基础 Hooks
  ✅ 已完成: 2/3
  ✅ 理解 useState 和 useEffect
  ✅ 学习 Hooks 规则
  ⬜ 待完成: 实践练习

Week 2 (1月11日-17日): 深入理解
  ⬜ 未开始: 0/2

Week 3 (1月18日-24日): 实践应用
  ⬜ 未开始: 0/1

Week 4 (1月25日-31日): 巩固提升
  ⬜ 未开始: 0/2

知识掌握度:
  React 基础概念: ⭐⭐⭐⭐⭐ (5/5)
  React Hooks 深入理解: ⭐⭐⭐☆☆ (3/5)
  函数组件最佳实践: ⭐⭐☆☆☆ (2/5)

学习建议:
  - 当前进度正常
  - 继续保持每日学习
  - 下周进入 Week 2
  - 记得做练习题

下次复习: 2026-01-11
```

## 学习路径生成

### 基于知识图谱
```
系统自动分析:
1. 查找指定标签的所有条目
2. 分析条目之间的依赖关系
3. 识别前置知识
4. 生成学习顺序

例如:
标签: react,hooks

前置知识:
→ JavaScript 基础
→ HTML/CSS 基础

核心知识:
1. React 基础概念 (必须)
2. React Hooks 深入理解 (核心)
3. 函数组件最佳实践 (实践)

扩展知识:
→ React 性能优化
→ React 状态管理
→ React 测试
```

### 智能推荐
```
基于您的学习计划推荐:

1. 补充知识
   建议: 先学习 JavaScript 异步编程
   原因: React Hooks 涉及异步操作

2. 实践项目
   建议: 完成一个 Todo List 项目
   原因: 综合运用所学知识

3. 相关资源
   推荐: React 官方文档
   推荐: React Hooks 深度教程
```

## 进度追踪

### 任务标记
```
标记任务完成:
/kb-learn --task-complete "learn-react-hooks" --task=1

标记整个里程碑完成:
/kb-learn --milestone-complete "learn-react-hooks" --week=1
```

### 记录学习时间
```
/kb-learn --log-time "learn-react-hooks" --hours=2

记录今天学习了 2 小时
```

### 添加学习笔记
```
/kb-learn --note "learn-react-hooks" "今天学会了自定义 Hooks，感觉很实用！"
```

### 调整计划
```
/kb-learn --adjust "learn-react-hooks" --duration="6 weeks"

延长学习时间
```

## 学习数据模型

### learning/plans/plan-id.json
```json
{
  "id": "learn-react-hooks",
  "title": "深入掌握 React Hooks",
  "goal": "能够熟练使用 Hooks 开发复杂应用",
  "status": "in-progress",
  "priority": "high",
  "created": "2026-01-04T16:00:00Z",

  "timing": {
    "duration": "4 weeks",
    "dailyGoal": "2 hours",
    "totalHours": 56,
    "startDate": "2026-01-04",
    "endDate": "2026-01-28",
    "actualHours": 14
  },

  "items": [
    "2026-01-04-105644",
    "2026-01-04-105815",
    "2026-01-04-105900"
  ],

  "order": [
    "2026-01-04-105644",
    "2026-01-04-105815",
    "2026-01-04-105900"
  ],

  "milestones": [
    {
      "week": 1,
      "period": "2026-01-04 - 2026-01-10",
      "goal": "掌握基础 Hooks",
      "tasks": [
        {
          "id": 1,
          "title": "理解 useState 和 useEffect",
          "completed": true,
          "completedAt": "2026-01-05T10:00:00Z"
        },
        {
          "id": 2,
          "title": "学习 Hooks 规则",
          "completed": true,
          "completedAt": "2026-01-06T14:00:00Z"
        },
        {
          "id": 3,
          "title": "实践练习",
          "completed": false
        }
      ]
    }
  ],

  "progress": {
    "totalTasks": 8,
    "completedTasks": 1,
    "percentage": 12.5,
    "lastUpdated": "2026-01-06T14:00:00Z"
  },

  "mastery": {
    "2026-01-04-105644": 5,
    "2026-01-04-105815": 3,
    "2026-01-04-105900": 2
  },

  "notes": [
    {
      "date": "2026-01-05",
      "content": "useState 比 class state 更直观",
      "type": "insight"
    }
  ],

  "nextReview": "2026-01-11"
}
```

## 高级功能

### 自动生成路径
```
/kb-learn "React 全栈" --tags=react --auto-generate

自动分析知识库，生成完整学习路径
```

### 难度分级
```
/kb-learn "React 进阶" --difficulty=advanced

仅包含高级内容
```

### 个性化推荐
```
基于您的学习历史推荐计划
```

### 学习提醒
```
每日提醒:
/kb-learn --remind --daily

每周总结:
/kb-learn --summary --weekly
```

## 与其他命令配合

### 学习 + 复习
```
/kb-learn "React Hooks"
/kb-review --today
```

### 学习 + 测试
```
/kb-learn "React Hooks"
/kb-quiz "React Hooks" --difficulty=medium
```

### 学习 + 费曼技巧
```
/kb-learn "React Hooks"
/kb-teach "React Hooks" --role=teacher
```

## 注意事项

1. **合理规划**: 设置现实可行的目标和时间
2. **每日坚持**: 保持每日学习习惯
3. **主动复习**: 利用间隔重复巩固记忆
4. **实践应用**: 结合实际项目加深理解
5. **灵活调整**: 根据进度调整计划

## 最佳实践

### 1. SMART 目标
- Specific: 具体明确
- Measurable: 可量化
- Achievable: 可实现
- Relevant: 相关性
- Time-bound: 有时限

### 2. 分阶段学习
- 每周一个主题
- 每个主题有明确目标
- 循序渐进

### 3. 理论与实践
- 学习理论知识
- 完成练习题
- 做实践项目

### 4. 定期回顾
- 每周总结
- 每月回顾
- 调整计划

### 5. 记录心得
- 学习笔记
- 个人理解
- 经验总结
