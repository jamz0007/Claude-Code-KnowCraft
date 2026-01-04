---
argument-hint: <topic|id|tag> [--difficulty=beginner|intermediate|advanced] [--type=recall|understanding|application|analysis] [--count=N] [--analyze] [--comprehensive]
description: 知识测验系统 - 生成测试并评估理解程度
allowed-tools: Read, Task
---

# /kb-quiz - 知识测验系统

## 功能
基于知识条目自动生成针对性测验,评估知识掌握程度,识别理解盲区。

## 核心理念

### 布鲁姆分类法
测验覆盖不同认知层次:
1. **记忆** (Remember) - 回忆型问题
2. **理解** (Understand) - 解释型问题
3. **应用** (Apply) - 应用型问题
4. **分析** (Analyze) - 分析型问题
5. **评价** (Evaluate) - 评价型问题
6. **创造** (Create) - 创造型问题

### 自适应难度
- 根据答题情况调整难度
- 识别薄弱知识点
- 推荐针对性学习

## 使用方式

### 基本测验
```
/kb-quiz "React Hooks"

基于相关知识条目生成测验
```

### 指定难度
```
/kb-quiz "React Hooks" --difficulty=intermediate

生成中级难度测验
```

### 指定题目类型
```
/kb-quiz "JavaScript" --type=application

仅生成应用型题目(实践题)
```

### 基于知识条目
```
/kb-quiz --id=2026-01-04-105815

基于特定条目生成测验
```

### 基于标签
```
/kb-quiz --tag=react,hooks

测试所有包含这些标签的条目
```

### 指定题目数量
```
/kb-quiz "React" --count=10

生成 10 道题目
```

### 综合测试
```
/kb-quiz --comprehensive

覆盖整个知识库的综合测试
```

### 分析模式
```
/kb-quiz --analyze

分析答题情况,识别知识盲区
```

## 参数说明

- `topic|id|tag`: 测验主题、条目 ID 或标签 (必需)
- `--difficulty`: 难度级别
  - `beginner`: 初级(基础概念)
  - `intermediate`: 中级(理解应用)
  - `advanced`: 高级(深入分析)
- `--type`: 题目类型
  - `recall`: 记忆型(填空、选择)
  - `understanding`: 理解型(解释、说明)
  - `application`: 应用型(代码、场景)
  - `analysis`: 分析型(对比、评价)
  - `mixed`: 混合(默认)
- `--count=N`: 题目数量 (默认: 5)
- `--analyze`: 答题后分析结果
- `--comprehensive`: 综合测试
- `--timed`: 计时模式(每题限时)
- `--practice`: 练习模式(显示答案和解析)

## 题目类型详解

### 1. 记忆型 (Recall)

**选择题**:
```
问题: React useState Hook 的主要作用是什么?

A) 管理组件的生命周期
B) 在函数组件中添加状态
C) 处理副作用
D) 优化组件性能

正确答案: B

你的答案: [输入 A/B/C/D]

✅/❌ 正确/错误

解析: useState 用于在函数组件中添加状态管理功能。
     useEffect 用于处理副作用,生命周期由 useEffect 处理。
```

**填空题**:
```
问题: React Hooks 必须在函数组件的____层调用,不能在循环、
     条件或嵌套函数中调用。

正确答案: 顶层

你的答案: [输入]

✅/❌ 正确/错误

解析: Hooks 的规则要求必须在顶层调用,这样 React 才能正确
     追踪 Hook 的调用顺序。
```

**判断题**:
```
问题: useState 可以在 Class 组件中使用吗? (是/否)

正确答案: 否

你的答案: [输入是/否]

✅/❌ 正确/错误

解析: Hooks 只能在函数组件中使用,不能在 Class 组件中使用。
```

### 2. 理解型 (Understanding)

**解释题**:
```
问题: 请用自己的话解释什么是"副作用"(Side Effect)?

参考答案:
  副作用是指在函数外部产生影响的操作,如:
  - 数据获取(API 请求)
  - 手动修改 DOM
  - 定时器设置
  - 订阅事件

你的答案: [输入]

评分: [1-5 分]

AI 评价:
  - 提到了"外部影响": ✓
  - 举例说明: ✓
  - 准确性: 良好

得分: 4/5

反馈: 很好!还可以补充"与渲染无关的操作"这个特点。
```

**对比题**:
```
问题: 对比 useState 和 useReducer 的适用场景?

参考要点:
  useState:
    - 简单状态(单一值)
    - 状态更新逻辑简单
    - 适合基本类型状态

  useReducer:
    - 复杂状态(对象或数组)
    - 状态更新逻辑复杂
    - 下一个状态依赖前一个状态
    - 需要多个相关状态

你的答案: [输入]

评分: [1-5 分]

AI 评价: [具体分析]
```

### 3. 应用型 (Application)

**代码题**:
```
问题: 使用 useState 重构以下 Class 组件为函数组件:

class Counter extends React.Component {
  constructor(props) {
    super(props);
    this.state = { count: 0 };
  }

  increment = () => {
    this.setState({ count: this.state.count + 1 });
  };

  render() {
    return (
      <div>
        <p>Count: {this.state.count}</p>
        <button onClick={this.increment}>Increment</button>
      </div>
    );
  }
}

你的代码:
[输入代码]

AI 评分: [1-5 分]

代码评价:
  ✓ 正确使用 useState
  ✓ 保持了相同的功能
  ✓ 代码结构清晰
  ⚠️ 可以改进: [具体建议]

最终得分: 4.5/5
```

**场景题**:
```
问题: 场景: 一个表单组件有以下状态:
  - 用户名(username)
  - 邮箱(email)
  - 密码(password)
  - 表单提交状态(isSubmitting)
  - 错误信息(error)

  问题:
  1) 你会用一个状态对象还是多个 useState?
  2) 为什么这样选择?

你的答案: [输入]

AI 评价:
  方案合理性: ✓/✗
  理由充分性: [评分]
  最佳实践: [建议]

得分: [分数]
```

### 4. 分析型 (Analysis)

**代码分析题**:
```
问题: 分析以下代码有什么问题,如何改进?

function UserProfile({ userId }) {
  const [user, setUser] = useState(null);

  useEffect(() => {
    fetch(`/api/users/${userId}`)
      .then(res => res.json())
      .then(data => setUser(data));
  });

  return <div>{user?.name}</div>;
}

你的分析:
[输入]

参考分析:
  问题:
    1. 缺少依赖数组,每次渲染都会请求
    2. 没有错误处理
    3. 没有加载状态
    4. userId 变化时不会重新请求

  改进:
    1. 添加依赖数组 [userId]
    2. 添加 loading 和 error 状态
    3. 使用 async/await 或 Promise 链
    4. 清理函数处理组件卸载

AI 评价:
  发现问题数量: X/4
  分析深度: [评分]
  改进方案: [评分]

总得分: [分数]
```

**性能分析题**:
```
问题: 以下组件在频繁更新时可能遇到性能问题,分析原因并提出优化方案:

function TodoList({ todos, onToggle, onDelete }) {
  return (
    <ul>
      {todos.map(todo => (
        <TodoItem
          key={todo.id}
          todo={todo}
          onToggle={() => onToggle(todo.id)}
          onDelete={() => onDelete(todo.id)}
        />
      ))}
    </ul>
  );
}

你的分析:
[输入]

AI 评价:
  - 识别的性能问题: [列出]
  - 提出的优化方案: [评估]
  - 方案的权衡: [讨论]

得分: [分数]
```

## 测验流程

### 开始测验
```
/kb-quiz "React Hooks" --difficulty=intermediate --count=5

🎯 知识测验: React Hooks

难度: 中级
题目数量: 5 题
预计时间: 10 分钟

题目类型分布:
  - 记忆型: 1 题
  - 理解型: 1 题
  - 应用型: 2 题
  - 分析型: 1 题

准备好了吗? 开始...

────────────────────────────────────────
```

### 答题过程
```
第 1 题 / 共 5 题 (记忆型)

问题: 以下哪个 Hook 用于处理副作用?

A) useState
B) useEffect
C) useContext
D) useReducer

计时: 0:15 / 1:00

你的答案: [输入]

下一题 →
```

### 逐题反馈
```
你的答案: B

✅ 正确!

用时: 18 秒

解析:
  useEffect 用于处理副作用,包括:
  - 数据获取
  - 订阅
  - 手动修改 DOM
  - 定时器

继续 →
```

### 测验总结
```
────────────────────────────────────────
📊 测验完成报告

主题: React Hooks
难度: 中级
完成时间: 8 分 32 秒

得分: 4/5 (80%)

详细得分:
  第 1 题: ✅ 正确 (18秒)
  第 2 题: ✅ 正确 (45秒)
  第 3 题: ❌ 错误 (2分15秒)
  第 4 题: ✅ 正确 (1分30秒)
  第 5 题: ✅ 正确 (3分44秒)

题目类型分析:
  记忆型: 1/1 (100%) ⭐⭐⭐⭐⭐
  理解型: 1/1 (100%) ⭐⭐⭐⭐⭐
  应用型: 1/2 (50%)  ⭐⭐⭐☆☆
  分析型: 1/1 (100%) ⭐⭐⭐⭐⭐

平均答题速度: 1分 42 秒/题

错题回顾:

第 3 题 (应用型 - 代码题):
题目: [题目内容]
你的答案: [你的代码]
问题: [指出问题]
正确答案: [参考代码]

学习建议:
  - 复习 useEffect 依赖数组
  - 练习清理函数的使用
  - 理解闭包陷阱

下一步:
  - 查看详细分析: /kb-quiz --analyze
  - 复习薄弱知识: /kb-review --tag=react,hooks
  - 练习类似题目: /kb-quiz "useEffect" --type=application

保存测验记录? (yes/no)
```

## 分析模式

### 答题分析
```
/kb-quiz --analyze

📈 知识分析报告

基于最近 5 次测验结果

总体表现:
  平均得分: 82%
  平均用时: 1分 45秒/题
  进步趋势: ↗ +5%

按题型分析:
  记忆型:   95% ⭐⭐⭐⭐⭐
  理解型:   88% ⭐⭐⭐⭐☆
  应用型:   75% ⭐⭐⭐⭐☆
  分析型:   70% ⭐⭐⭐☆☆

按主题分析:
  React 基础:    90% ⭐⭐⭐⭐⭐
  React Hooks:   82% ⭐⭐⭐⭐☆
  React 性能优化: 65% ⭐⭐⭐☆☆  ⚠️ 需加强
  React 状态管理: 70% ⭐⭐⭐☆☆

知识盲区识别:

⚠️ 薄弱知识点:
  1. React 性能优化 (65%)
     - 常见错误: 忘记使用 React.memo
     - 建议: 学习 useMemo 和 useCallback

  2. useEffect 依赖 (70%)
     - 常见错误: 依赖数组不完整
     - 建议: 复习 ESLint 插件的警告

  3. 自定义 Hooks (75%)
     - 常见错误: 规则不清晰
     - 建议: 练习创建自定义 Hook

✅ 掌握良好的知识点:
  1. useState 使用 (95%)
  2. Hooks 基本规则 (90%)
  3. 组件渲染原理 (88%)

学习建议:

优先级 1 (立即加强):
  /kb-learn "React 性能优化" --duration="1 week"
  /kb-review --tag=performance

优先级 2 (本周复习):
  /kb-quiz "useEffect" --type=application
  /kb-teach "自定义 Hooks" --role=student

优先级 3 (保持巩固):
  /kb-review --tag=react,basics
  /kb-quiz "React 基础" --difficulty=advanced

遗忘曲线预测:
  基于答题质量,预计:
  - React 基础: 30 天后保持率 85%
  - React Hooks: 30 天后保持率 70%
  - 性能优化: 30 天后保持率 45% ⚠️

  建议复习计划:
  - 性能优化: 3 天后复习
  - Hooks: 7 天后复习
  - 基础: 14 天后复习
```

## 综合测试

### 全知识库测试
```
/kb-quiz --comprehensive

🎯 综合知识测试

覆盖范围: 全部知识库 (45 个条目)

题目分布:
  React:       15 题 (33%)
  JavaScript:  12 题 (27%)
  CSS:         8 题 (18%)
  TypeScript:  6 题 (13%)
  其他:        4 题 (9%)

难度分布:
  初级: 30%
  中级: 50%
  高级: 20%

题目总数: 45 题
预计时间: 90 分钟

开始前建议:
  - 确保有充足时间
  - 准备纸笔记录思考
  - 保持安静环境

开始测试? (yes/no)
```

### 综合测试报告
```
────────────────────────────────────────
📊 综合测试报告

测试时间: 2026-01-04
总用时: 87 分 12 秒

总分: 38/45 (84%)

各领域得分:
  React:       13/15 (87%) ⭐⭐⭐⭐⭐
  JavaScript:  10/12 (83%) ⭐⭐⭐⭐☆
  CSS:         7/8  (88%) ⭐⭐⭐⭐⭐
  TypeScript:  5/6  (83%) ⭐⭐⭐⭐☆
  其他:        3/4  (75%) ⭐⭐⭐⭐☆

能力雷达图:
       React (87%)
         /|\
        / | \
       /  |  \
 TS (83%)  |  CSS (88%)
       \  |  /
        \ | /
         \|/
  JS (83%)  Other (75%)

认知层次分析:
  记忆 (Remember):    95% ⭐⭐⭐⭐⭐
  理解 (Understand):  88% ⭐⭐⭐⭐⭐
  应用 (Apply):       78% ⭐⭐⭐⭐☆
  分析 (Analyze):     72% ⭐⭐⭐⭐☆
  评价 (Evaluate):    65% ⭐⭐⭐☆☆
  创造 (Create):      60% ⭐⭐⭐☆☆

优势能力:
  ✓ 理论知识扎实
  ✓ 基础概念清晰
  ✓ 代码应用熟练

提升空间:
  - 深度分析能力 (65% → 75%)
  - 创造性思维 (60% → 70%)
  - 性能优化实践 (70% → 85%)

知识结构评估:
  整体性: ⭐⭐⭐⭐☆
    - 知识点之间关联良好
    - 能够跨领域应用

  深度: ⭐⭐⭐⭐☆
    - 核心概念理解深入
    - 部分高级概念需要加强

  广度: ⭐⭐⭐⭐☆
    - 覆盖主要技术栈
    - 可以扩展学习领域

建议学习计划:

阶段 1 (1-2 周) - 加强薄弱:
  重点: 性能优化、深度分析
  行动:
    - /kb-learn "React 性能优化"
    - /kb-quiz "performance" --type=analysis

阶段 2 (2-4 周) - 深化理解:
  重点: 高级特性、设计模式
  行动:
    - /kb-learn "React 高级模式"
    - /kb-teach "HOC vs Hooks" --mode=mckinsey

阶段 3 (4-8 周) - 创造应用:
  重点: 项目实践、架构设计
  行动:
    - 完成综合项目
    - /kb-quiz --comprehensive (复测)

与历史测试对比:
  上次 (2025-12-01): 76% → 本次: 84% (+8%) ↗
  进步显著,继续保持!

保存完整报告? (yes/no)
```

## 练习模式

### 带解析的练习
```
/kb-quiz "React Hooks" --practice

练习模式: 显示答案和详细解析

────────────────────────────────────────
第 1 题

问题: useEffect 的依赖数组为空 [] 时, behavior 是什么?

A) 每次渲染后都执行
B) 只在组件挂载时执行一次
C) 只在组件卸载时执行
D) 永远不执行

思考时间...

[按任意键显示答案]

正确答案: B) 只在组件挂载时执行一次

详细解析:
  useEffect(() => {
    // 这个 effect 只在组件挂载时运行一次
    // 类似于 componentDidMount
  }, []);

  依赖数组为空表示 effect 不依赖任何值,
  因此只在挂载时执行一次,不会在更新时重新执行。

  对比:
  - 无依赖数组: 每次渲染后执行
  - 空数组 []: 只执行一次
  - 有依赖 [x, y]: 依赖变化时执行

  易混淆点:
  记住:[] = "我什么都不依赖,只需要初始化"

[按任意键继续]
────────────────────────────────────────
```

## 测验数据保存

### 测验记录
```json
learning/quizzes/quiz-id.json

{
  "id": "2026-01-04-quiz-001",
  "date": "2026-01-04T14:30:00Z",
  "type": "topic-based",
  "topic": "React Hooks",
  "difficulty": "intermediate",
  "questionCount": 5,
  "duration": "8m 32s",

  "score": {
    "total": 5,
    "correct": 4,
    "percentage": 80,
    "byType": {
      "recall": 100,
      "understanding": 100,
      "application": 50,
      "analysis": 100
    }
  },

  "questions": [
    {
      "id": 1,
      "type": "recall",
      "correct": true,
      "timeSpent": "18s",
      "difficulty": "easy"
    },
    ...
  ],

  "weaknesses": [
    "useEffect 依赖数组",
    "自定义 Hooks 规则"
  ],

  "recommendations": [
    "复习 useEffect 完整文档",
    "练习创建自定义 Hook"
  ]
}
```

## 高级功能

### 自适应难度
```
/kb-quiz "React" --adaptive

根据答题情况自动调整难度:
- 答对 → 提高难度
- 答错 → 降低难度
- 找到合适的学习区间
```

### 限时挑战
```
/kb-quiz "JavaScript" --timed --limit=30

30 秒限时挑战模式
```

### 错题重做
```
/kb-quiz --mistakes

仅重做之前答错的题目
```

### 对比测试
```
/kb-quiz --compare 2026-01-01

与指定日期的测验结果对比
```

## 与其他系统配合

### 测验 + 复习
```
/kb-quiz "React"
/kb-review --tag=weak-topics  # 复习薄弱知识
```

### 测验 + 学习计划
```
/kb-quiz --comprehensive  # 综合测试
/kb-learn "加强薄弱" --items=[分析结果中的薄弱条目]
```

### 测验 + 费曼技巧
```
/kb-quiz "Hooks" --analyze
/kb-teach "薄弱知识点" --role=teacher  # 费曼技巧加强
```

## 最佳实践

### 1. 定期测试
```
频率建议:
  - 每日: 5-10 题快速测试
  - 每周: 针对性主题测试
  - 每月: 综合测试
```

### 2. 分析结果
```
每次测试后:
  - 查看详细分析
  - 识别薄弱点
  - 制定复习计划
```

### 3. 循环加强
```
测试 → 复习 → 再测试
  ↓
识别盲点 → 重点学习 → 验证提升
```

### 4. 多角度练习
```
不同类型题目:
  - 记忆型: 巩固基础
  - 理解型: 深化认识
  - 应用型: 实践能力
  - 分析型: 批判思维
```

### 5. 记录进步
```
长期跟踪:
  - 保存所有测验记录
  - 观察进步趋势
  - 调整学习策略
```

## 注意事项

### 1. 真实测试
- 不要查看资料
- 独立完成
- 诚实记录

### 2. 质量优先
- 理解题意再作答
- 应用题写出完整过程
- 不要追求速度

### 3. 错误反思
- 分析错误原因
- 理解正确答案
- 总结经验教训

### 4. 持续改进
- 根据分析调整学习
- 针对性加强
- 定期复测

### 5. 积极心态
- 错误是学习机会
- 不要怕犯错
- 从错误中成长

## 扩展功能(未来)

### 1. 语音答题
```
支持语音输入答案
```

### 2. 代码运行
```
在线运行和测试代码
```

### 3. 排行榜
```
与其他学习者对比
```

### 4. AI 出题
```
根据学习历史定制题目
```

### 5. 团队测试
```
多人协作答题
```
