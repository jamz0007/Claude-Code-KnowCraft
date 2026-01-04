# 📚 命令参考

> 完整的命令、Agent和Skill文档索引

## 📑 目录

- [命令列表](#命令列表)
- [Agent列表](#agent列表)
- [Skill列表](#skill列表)

---

## 命令列表

### 知识管理

| 命令 | 文档路径 | 说明 |
|------|---------|------|
| `/kb-add` | [`.claude/commands/kb-add.md`](../.claude/commands/kb-add.md) | 添加知识条目 |
| `/kb-edit` | [`.claude/commands/kb-edit.md`](../.claude/commands/kb-edit.md) | 编辑知识条目 |
| `/kb-delete` | [`.claude/commands/kb-delete.md`](../.claude/commands/kb-delete.md) | 删除知识条目 |
| `/kb-search` | [`.claude/commands/kb-search.md`](../.claude/commands/kb-search.md) | 搜索知识 |
| `/kb-list` | [`.claude/commands/kb-list.md`](../.claude/commands/kb-list.md) | 列出知识 |

### 知识导入

| 命令 | 文档路径 | 说明 |
|------|---------|------|
| `/kb-from-pdf` | [`.claude/commands/kb-from-pdf.md`](../.claude/commands/kb-from-pdf.md) | PDF导入 |
| `/kb-from-url` | [`.claude/commands/kb-from-url.md`](../.claude/commands/kb-from-url.md) | URL抓取 |
| `/kb-from-image` | [`.claude/commands/kb-from-image.md`](../.claude/commands/kb-from-image.md) | 图片OCR |
| `/kb-import` | [`.claude/commands/kb-import.md`](../.claude/commands/kb-import.md) | 批量导入 |
| `/kb-export` | [`.claude/commands/kb-export.md`](../.claude/commands/kb-export.md) | 导出知识 |

### 知识关联

| 命令 | 文档路径 | 说明 |
|------|---------|------|
| `/kb-link` | [`.claude/commands/kb-link.md`](../.claude/commands/kb-link.md) | 创建关联 |
| `/kb-graph` | [`.claude/commands/kb-graph.md`](../.claude/commands/kb-graph.md) | 知识图谱 |
| `/kb-diff` | [`.claude/commands/kb-diff.md`](../.claude/commands/kb-diff.md) | 版本对比 |
| `/kb-restore` | [`.claude/commands/kb-restore.md`](../.claude/commands/kb-restore.md) | 恢复版本 |

### 学习系统

| 命令 | 文档路径 | 说明 |
|------|---------|------|
| `/kb-learn` | [`.claude/commands/kb-learn.md`](../.claude/commands/kb-learn.md) | 学习计划 |
| `/kb-quiz` | [`.claude/commands/kb-quiz.md`](../.claude/commands/kb-quiz.md) | 智能测验 |
| `/kb-review` | [`.claude/commands/kb-review.md`](../.claude/commands/kb-review.md) | 间隔复习 |
| `/kb-teach` | [`.claude/commands/kb-teach.md`](../.claude/commands/kb-teach.md) | 费曼技巧 |

### 网络搜索

| 命令 | 文档路径 | 说明 |
|------|---------|------|
| `/kb-search-web` | [`.claude/commands/kb-search-web.md`](../.claude/commands/kb-search-web.md) | 智能搜索 |

---

## Agent列表

### 分析类

| Agent | 文档路径 | 核心功能 |
|-------|---------|---------|
| **Knowledge Architect** | [`.claude/agents/knowledge-architect/AGENT.md`](../.claude/agents/knowledge-architect/AGENT.md) | 知识架构分析、结构优化、空白识别 |

### 内容类

| Agent | 文档路径 | 核心功能 |
|-------|---------|---------|
| **Knowledge Enricher** | [`.claude/agents/knowledge-enricher/AGENT.md`](../.claude/agents/knowledge-enricher/AGENT.md) | 内容增强、质量提升、信息补充 |

### 学习类

| Agent | 文档路径 | 核心功能 |
|-------|---------|---------|
| **Quiz Master** | [`.claude/agents/quiz-master/AGENT.md`](../.claude/agents/quiz-master/AGENT.md) | 生成测验、评估理解、难度自适应 |
| **Student** | [`.claude/agents/student/AGENT.md`](../.claude/agents/student/AGENT.md) | 模拟学习、提问互动、理解验证 |
| **Tutor** | [`.claude/agents/tutor/AGENT.md`](../.claude/agents/tutor/AGENT.md) | 个性化指导、学习建议、进度跟踪 |

### 研究类

| Agent | 文档路径 | 核心功能 |
|-------|---------|---------|
| **Research Assistant** | [`.claude/agents/research-assistant/AGENT.md`](../.claude/agents/research-assistant/AGENT.md) | 深度研究、资料整理、观点综合 |
| **Search Assistant** | [`.claude/agents/search-assistant/AGENT.md`](../.claude/agents/search-assistant/AGENT.md) | 网页抓取、内容提取、质量评分 |

### 版本类

| Agent | 文档路径 | 核心功能 |
|-------|---------|---------|
| **Version Keeper** | [`.claude/agents/version-keeper/AGENT.md`](../.claude/agents/version-keeper/AGENT.md) | 版本追踪、演化分析、历史对比 |

---

## Skill列表

### 核心技能

| Skill | 文档路径 | 功能描述 |
|-------|---------|---------|
| **Knowledge Manager** | [`.claude/skills/knowledge-manager/skill.md`](../.claude/skills/knowledge-manager/skill.md) | 智能知识管理、自动标签推荐、关联建议 |
| **NLP Interface** | [`.claude/skills/nlp-interface/skill.md`](../.claude/skills/nlp-interface/skill.md) | 自然语言接口、意图识别、上下文理解 |
| **Suggestion Engine** | [`.claude/skills/suggestion-engine/skill.md`](../.claude/skills/suggestion-engine/skill.md) | 智能建议引擎、主动推荐、个性化排序 |

---

## 使用说明

### 查看命令帮助

```bash
# 查看命令用法
claude> /kb-add --help

# 查看命令示例
claude> /kb-add --example
```

### 调用Agent

```bash
# 使用@符号调用Agent
claude> @knowledge-architect "分析我的知识结构"
claude> @research-assistant "研究微前端架构"
```

### 自然语言

```bash
# 使用自然语言操作
"记一条笔记"
"搜索React"
"编辑第一条"
```

---

## 📚 相关文档

- [使用指南](USER_GUIDE.md) - 详细使用说明
- [开发指南](DEVELOPMENT.md) - 添加新命令
- [系统架构](ARCHITECTURE.md) - 了解系统结构

---

**快速查找命令，高效使用系统！** 🚀
