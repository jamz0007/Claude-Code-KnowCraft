# 💡 使用指南

> 全面了解如何使用个人知识系统进行高效学习和知识管理

## 📑 目录

- [自然语言交互](#️-自然语言交互)
- [斜杠命令快速参考](#-斜杠命令快速参考)
- [智能学习系统](#-智能学习系统)
- [智能网络搜索](#-智能网络搜索)
- [典型使用场景](#-典型使用场景)
- [效率技巧](#-效率技巧)

---

## 🗣️ 自然语言交互

**核心优势**: 无需记忆命令,用日常语言管理知识

### 基础操作示例

#### 添加知识

```bash
# 多种表达方式都可以
"记一条React笔记"
"添加一条JavaScript学习记录"
"新建一个项目文档"
"写一篇关于Vue的学习笔记"
```

#### 搜索知识

```bash
# 按关键词搜索
"找useState相关的笔记"
"搜索所有React Hooks"
"查找昨天的笔记"

# 按标签搜索
"显示所有前端相关的笔记"
"找带javascript标签的条目"
```

#### 编辑知识

```bash
# 代词引用
"修改第一条"
"编辑刚才那条"
"把React基础概念更新一下"

# 明确指定
"编辑useState的笔记"
"修改标题为Redux的条目"
```

#### 删除知识

```bash
# 简单直接
"删除测试笔记"
"移除最后一条"

# 确认操作
"删除刚才那条笔记"
```

#### 学习相关

```bash
# 学习计划
"开始学习React"
"制定Python学习计划"

# 测试和复习
"测试我的React知识"
"复习昨天的内容"
"检查我的学习进度"
```

### 上下文理解示例

系统具有对话历史记忆能力，可以理解上下文和代词。

#### 对话历史记忆

```bash
用户: "找useState"
系统: [返回3条结果，例如：2026-01-04-120000, 2026-01-03-150000, 2026-01-02-100000]

用户: "修改它"
系统: 📝 编辑知识 - 2026-01-04-120000 (useState)
      # "它"自动解析为最新搜索的useState ID
```

#### 代词解析

```bash
用户: "搜索React Hooks"
系统: [返回5条结果]

用户: "这个怎么用"
系统: 📖 React Hooks 使用指南
      # "这个"指React Hooks主题

用户: "第三条呢"
系统: 📖 第三条: useEffect详解
      # "第三条"直接引用搜索结果中的第3条
```

#### 多轮对话

```bash
用户: "添加一条Redux笔记"
系统: [创建笔记，返回ID: 2026-01-04-150000]

用户: "给刚才那条加个状态管理的标签"
系统: ✅ 已添加标签: state-management
      # "刚才那条"自动引用最新创建的笔记ID
```

### 智能建议交互

系统会在操作后主动推荐相关操作。

#### 添加知识后的智能建议

```bash
用户: "记一条Redux笔记"
系统: ✅ 已添加: [2026-01-04-150000]

      💡 智能建议
        [92%] 创建关联
          发现3个React相关条目
          操作: /kb-link 2026-01-04-150000 <other-id>

        [85%] 开始学习
          建议创建学习计划掌握Redux
          操作: /kb-learn "Redux"

        [70%] 测试理解
          检验对Redux的掌握程度
          操作: /kb-quiz "Redux"

      选择操作(输入序号或跳过): 1

系统: ✅ 已创建关联！
      Redux ←→ React (related)
```

#### 搜索后的智能建议

```bash
用户: "搜索性能优化"
系统: [返回10条结果]

      💡 搜索建议
        - 结果过多，建议添加标签过滤: "搜索react性能优化"
        - 或按时间筛选: /kb-search "性能优化" --after=2025-01-01
```

---

## ⚡ 斜杠命令快速参考

19个核心命令速查表：

### 知识管理

| 命令 | 功能 | 常用示例 |
|------|------|----------|
| `/kb-add` | 添加知识 | `/kb-add --type=learning-note` |
| `/kb-edit` | 编辑知识 | `/kb-edit [id]` |
| `/kb-delete` | 删除知识 | `/kb-delete [id]` |
| `/kb-list` | 列出知识 | `/kb-list --by=recent` |
| `/kb-search` | 搜索知识 | `/kb-search "React" --tag=hooks` |

### 知识导入

| 命令 | 功能 | 常用示例 |
|------|------|----------|
| `/kb-from-pdf` | PDF导入 | `/kb-from-pdf document.pdf` |
| `/kb-from-url` | URL抓取 | `/kb-from-url https://example.com` |
| `/kb-from-image` | 图片OCR | `/kb-from-image screenshot.png` |
| `/kb-import` | 批量导入 | `/kb-import --source=obsidian` |
| `/kb-export` | 导出知识 | `/kb-export --format=markdown` |

### 知识关联

| 命令 | 功能 | 常用示例 |
|------|------|----------|
| `/kb-link` | 创建关联 | `/kb-link id1 id2 --type=related` |
| `/kb-graph` | 知识图谱 | `/kb-graph --format=mermaid` |
| `/kb-diff` | 版本对比 | `/kb-diff id1 --version=2` |
| `/kb-restore` | 恢复版本 | `/kb-restore id --version=1` |

### 学习系统

| 命令 | 功能 | 常用示例 |
|------|------|----------|
| `/kb-learn` | 学习计划 | `/kb-learn "React" --duration=2weeks` |
| `/kb-quiz` | 智能测验 | `/kb-quiz "React" --difficulty=medium` |
| `/kb-review` | 间隔复习 | `/kb-review --today` |
| `/kb-teach` | 费曼技巧 | `/kb-teach "useState" --role=teacher` |

### 网络搜索

| 命令 | 功能 | 常用示例 |
|------|------|----------|
| `/kb-search-web` | 智能搜索 | `/kb-search-web "React性能优化"` |

---

## 🧠 智能学习系统

### 1. 间隔重复 (SuperMemo SM-2算法)

基于科学的遗忘曲线，智能安排复习时间，最大化记忆效率。

#### 查看今日复习

```bash
/kb-review --today
```

#### 复习流程

```bash
用户: "开始复习"

系统: 📝 今日复习 (5条)

      1. [2026-01-03-105822] useEffect依赖项
         上次评分: 4/5 | 复习间隔: 3天
         下次复习: 2026-01-10

         [内容预览...]
         useEffect是React的Hook，用于处理副作用...

         评分 (1-5): 4

系统: ✅ 已记录
      下次复习: 2026-01-10 (7天后)

      2. [2026-01-02-100000] React生命周期
         ...
```

#### 评分标准

- **1分**: 完全不记得，重置间隔为1天
- **2分**: 有印象但不清楚，重置间隔为1天
- **3分**: 基本记得，间隔保持不变
- **4分**: 记得清楚，间隔 × 1.5
- **5分**: 完全掌握，间隔 × 2.0

#### 算法原理

SuperMemo SM-2算法：

- 评分 < 3: 重置间隔为1天（重新学习）
- 评分 ≥ 3: 间隔 = 间隔 × 难度系数
- 难度系数: 1.3 ~ 2.5（根据评分动态调整）

### 2. 费曼技巧

通过"教学"来验证理解，发现知识盲区。

#### 启动费曼学习

```bash
/kb-teach "useState" --role=teacher
```

#### 学习流程

```bash
系统: 👨‍🏫 费曼学习 - useState

      你现在是老师,请向初学者解释useState

      要求:
        1. 用简单语言(避免术语)
        2. 使用类比和例子
        3. 发现理解盲区

      [你的解释...]
      useState就像是React给函数组件的一个"魔法盒子"，
      你可以在里面放一个值，然后React会记住它...
```

#### AI评估反馈

```bash
系统: 📊 理解评估
        ✅ 概念清晰
        ✅ 类比恰当
        ⚠️ 缺少实际例子
        💡 建议: 补充一个实际应用场景

      想要改进解释吗？(y/n)
```

#### 费曼技巧的优势

- **主动回忆**: 强调主动输出而非被动输入
- **简化理解**: 用简单语言解释复杂概念
- **发现盲区**: AI分析找出理解不完整的地方
- **加深记忆**: 教学过程本身就是最好的复习

### 3. 智能测验

自动生成测试题，评估掌握程度，发现薄弱环节。

#### 生成测验

```bash
/kb-quiz "React Hooks" --difficulty=medium --count=5
```

#### 测验示例

```bash
系统: 📝 React Hooks 测验 (5题)

      Q1. useState的返回值是什么？
          A. (state, setState)
          B. [state, setState]
          C. {state, setState}
          D. state & setState

      你的答案: B

系统: ✅ 正确！
      解释: useState返回数组,第一个元素是状态值,
            第二个是更新函数,通过数组解构获取。

      Q2. useEffect的依赖数组为空时，效果是什么？
      ...
```

#### 难度级别

- **easy**: 基础概念和定义
- **medium**: 应用场景和最佳实践
- **hard**: 高级特性和边界情况

#### 测验报告

```bash
系统: 📊 测验报告

      总分: 4/5 (80%)

      掌握良好:
        ✅ useState
        ✅ useEffect
        ✅ useContext

      需要加强:
        ⚠️ useMemo (答错了)
        💡 建议: 复习 useMemo 的使用场景

      下次复习建议:
        - useMemo相关笔记 (2026-01-05)
```

---

## 🔍 智能网络搜索

集成Google Custom Search API，AI智能整理搜索结果。

### 基本搜索

```bash
/kb-search-web "React性能优化"
```

### 搜索流程

#### 1. 搜索中

```bash
系统: 🔍 搜索Google...
      找到10个结果,AI整理后推荐Top 3:
```

#### 2. 结果展示

```bash
系统: 1. ⭐⭐⭐⭐⭐ [98分] React性能优化完全指南

         核心要点:
         • React.memo避免不必要的重渲染
         • useMemo和useCallback优化计算
         • 虚拟列表处理大量数据

         摘要: 这篇文章系统介绍了React性能优化的核心技巧，
               包含大量实例代码和性能对比数据。适合中高级
               开发者深入学习。

         链接: https://react.dev/learn/render-and-commit
         作者: React团队
         发布: 2024-12-15

      2. ⭐⭐⭐⭐☆ [85分] React Hooks性能陷阱
      3. ⭐⭐⭐⭐☆ [82分] 大型React应用性能优化实战
```

#### 3. 选择保存

```bash
选择保存哪些？(输入序号,如1,3): 1,3

系统: 确认保存？
      1. React性能优化完全指南
         建议标签: react, performance, optimization

      要修改标签吗？(回车确认): [回车]
```

#### 4. 智能关联

```bash
系统: ✅ 正在保存...
      ✅ 已保存2个条目！

      💡 这2个条目都讨论性能优化,是否创建关联？(y/n): y

系统: ✅ 已创建关联！
      [2026-01-04-150000] ←→ [2026-01-04-150100] (related)
```

### 多维度评分系统

搜索结果综合评分（满分100分）：

- **内容质量** (40%): 内容完整性、准确性、深度
- **权威性** (30%): 来源可信度、作者专业度
- **时效性** (15%): 发布时间、更新频率
- **相关性** (15%): 与搜索查询的匹配度

### 对话式筛选

支持多轮搜索优化：

```bash
用户: "搜索React性能优化"
系统: [返回15条结果]

用户: "结果太多了，专注于useMemo"
系统: 🔍 优化搜索: React useMemo 性能优化
      [返回5条更精确的结果]

用户: "只要2024年的"
系统: 🔍 筛选: React useMemo 性能优化 2024
      [返回3条最新结果]
```

---

## 🎯 典型使用场景

### 场景1: 学习新技术栈

系统化学习一个完整的技术栈。

#### 步骤1: 创建学习计划

```bash
/kb-learn "React生态" --duration=4weeks
```

系统会生成阶段性学习目标和每日任务。

#### 步骤2: 逐步添加知识

```bash
# 每天学习时添加笔记
"记一条React基础笔记"
"添加Redux学习记录"
"记下React Router用法"
"学习React Suspense"
```

系统会自动推荐标签，并发现相关条目。

#### 步骤3: 系统自动建议关联

```bash
系统: 💡 智能建议
      发现5个React相关条目,建议创建关联
```

接受建议，系统自动构建知识网络。

#### 步骤4: 定期复习

```bash
# 每天复习
/kb-review --today
```

基于遗忘曲线智能安排复习。

#### 步骤5: 测试掌握程度

```bash
# 每周测试
/kb-quiz "React生态" --difficulty=hard
```

发现薄弱环节，有针对性复习。

#### 步骤6: 用费曼技巧验证

```bash
# 深度理解核心概念
/kb-teach "React状态管理" --role=teacher
```

通过教学验证理解深度。

### 场景2: 整理项目文档

将现有项目文档导入并结构化。

#### 步骤1: 导入现有文档

```bash
/kb-import --source=markdown --path=./project-docs
```

系统会自动解析文档并创建索引。

#### 步骤2: 创建项目关联

```bash
# 建立文档间的引用关系
/kb-link id1 id2 --type=references
/kb-link id3 id1 --type=builds-on
```

- `references`: 引用关系
- `builds-on`: 依赖关系
- `related`: 相关关系

#### 步骤3: 生成知识图谱

```bash
/kb-graph --format=mermaid --output=project-graph.png
```

可视化项目知识结构，发现关键节点。

#### 步骤4: 分析架构

```bash
@knowledge-architect "分析项目知识结构"
```

AI Agent会分析知识架构，识别空白和冗余。

### 场景3: 研究特定主题

深入研究一个技术主题。

#### 步骤1: 网络搜索最新资料

```bash
/kb-search-web "微前端架构2025最新实践"
```

AI自动整理并评分搜索结果。

#### 步骤2: AI自动整理并保存

```bash
# 选择保存2-3个高质量资源
# 系统自动提取核心内容
```

#### 步骤3: 深入研究

```bash
@research-assistant "深入研究微前端的状态管理方案"
```

Research Agent会综合多个来源，生成深度研究报告。

#### 步骤4: 整理成笔记

```bash
/kb-add --type=research-note
# 整合研究结果
```

#### 步骤5: 创建主题集群

```bash
/kb-link research-id implementation-id --type=related
```

建立主题内部的关联网络。

---

## 📊 效率技巧

### 快捷方式（自定义别名）

在 `config/user-preferences.json` 中定义快捷方式：

```json
{
  "shortcuts": {
    "笔记": "--type=learning-note",
    "代码": "--type=code-snippet",
    "项目": "--category=projects"
  }
}
```

使用时自动展开：

```bash
"记一条笔记" → 自动展开为 --type=learning-note
"记一段代码" → 自动展开为 --type=code-snippet
"新建项目文档" → 自动展开为 --category=projects
```

### 批量操作

#### 批量导入

```bash
# 从Obsidian导入
/kb-import --source=obsidian --path=./vault

# 从Markdown导入
/kb-import --source=markdown --path=./notes

# 从Notion导出后导入
/kb-import --source=markdown --path=./notion-export
```

#### 批量导出

```bash
# 导出为Markdown
/kb-export --format=markdown --output=./backup

# 导出特定标签
/kb-export --tag=react --output=./react-notes
```

#### 批量复习

```bash
# 批量复习10条
/kb-review --batch --count=10

# 复习特定主题
/kb-review --tag=react --batch
```

### 智能过滤

#### 组合过滤条件

```bash
# 多条件搜索
/kb-search "React" --tag=hooks --after=2026-01-01 --category=learning

# 按时间范围
/kb-list --after=2026-01-01 --before=2026-01-31

# 按分类和标签
/kb-list --category=learning --tag=frontend
```

#### 排除特定标签

```bash
/kb-list --exclude=archive --exclude=draft

# 只看活跃条目
/kb-list --exclude=archived --exclude=deprecated
```

#### 排序选项

```bash
# 按时间排序
/kb-list --by=recent

# 按相关性排序
/kb-search "React" --sort=relevance

# 按复习时间排序
/kb-list --by=review-date
```

---

## 📚 相关文档

- [快速开始](GETTING_STARTED.md) - 安装和配置
- [配置说明](CONFIGURATION.md) - 自定义系统行为
- [命令参考](COMMAND_REFERENCE.md) - 完整命令文档

---

**祝您使用愉快！用AI改变知识管理！** 🚀
