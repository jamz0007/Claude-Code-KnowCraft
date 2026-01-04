# 🧠 个人知识系统 - Claude Code 智能集成

> 基于本地文件的智能知识管理系统,集成 Claude Code 实现自然语言交互和智能学习

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
[![Claude Code](https://img.shields.io/badge/Claude_Code-Integrated-brightgreen)](https://claude.ai/claude-code)
[![Stage](https://img.shields.io/badge/Stage-7_Complete-blue)]()
[![Version](https://img.shields.io/badge/version-1.0.0-blue.svg)]()

[![Knowledge Items](https://img.shields.io/badge/Knowledge_Items-0+-green)]()
[![Commands](https://img.shields.io/badge/Commands-19-orange)]()
[![AI Agents](https://img.shields.io/badge/AI_Agents-8-purple)]()
[![Platform](https://img.shields.io/badge/Platform-Windows%20%7C%20Linux%20%7C%20macOS-lightgrey)]()

这是一个革命性的个人知识管理系统,完全基于本地文件存储(JSON + Markdown),无需数据库依赖。通过深度集成 Claude Code,支持自然语言交互、智能网络搜索、间隔重复学习、费曼技巧验证等先进功能,让知识管理变得前所未有的智能和高效。

**核心优势**: 本地优先、AI驱动、科学学习、完全掌控你的知识。

---

## 👥 开发团队与社区

| 项目 | 链接/信息 |
|------|-----------|
| 开发团队官网 | https://www.wellally.tech/ |
| 交流群 | ![社群](./public/社群.jpg) |
| 社群介绍 | 使用 Claude Code 替代现有的一切软件,让任何一个人都可以享受到 Claude Code 对一切的改变 |

---

## ✨ 核心特性

### 🎯 智能知识管理
- **📝 多源知识输入**: 支持手动输入、PDF导入、URL抓取、图片OCR、网络搜索
- **🏷️ 智能标签系统**: 自动推荐标签、标签层级管理、相似标签合并建议
- **🔗 知识关联**: 自动识别相关条目、双向链接、关联类型(references/builds-on/related)
- **📊 版本控制**: 自动版本备份、差异对比、一键恢复历史版本

### 🧠 AI驱动的学习系统
- **🔄 间隔重复 (SuperMemo SM-2算法)**: 科学计算复习间隔,提高记忆效率
- **👨‍🏫 费曼技巧**: 通过教学验证理解,发现知识盲区
- **📝 智能测验**: 自动生成测试题(选择题/填空题/应用题),评估掌握程度
- **📅 复习提醒**: 基于遗忘曲线的智能复习提醒

### 🗣️ 自然语言交互
- **💬 对话式操作**: 用自然语言管理知识(如"记一条React笔记"、"修改第一条")
- **🎯 意图识别**: 自动理解用户意图,6大意图类型(添加/搜索/编辑/学习/导入/网络搜索)
- **🧠 上下文理解**: 记住对话历史,解析代词("它"、"这个"、"第一条")
- **⚡ 智能建议**: 主动推荐关联、学习路径、优化建议

### 🔍 智能网络搜索
- **🌐 Google集成**: 使用Google Custom Search API搜索最新资料
- **🤖 AI整理**: 自动抓取、提取、摘要、评分搜索结果
- **⭐ 多维度评分**: 内容质量(40%) + 权威性(30%) + 时效性(15%) + 相关性(15%)
- **🎯 对话式筛选**: 支持多轮搜索优化("太泛了,专注于useMemo")

### 🏗️ 8个专业AI Agent
1. **Knowledge Architect** - 知识架构师,分析知识结构
2. **Knowledge Enricher** - 知识增强师,完善内容质量
3. **Quiz Master** - 测验大师,生成智能测试
4. **Research Assistant** - 研究助手,深度研究主题
5. **Search Assistant** - 搜索助手,整理网络资源
6. **Student** - 学生Agent,模拟学习过程
7. **Tutor** - 导师Agent,提供个性化指导
8. **Version Keeper** - 版本管理员,追踪知识演化

### 💾 本地优先设计
- **📁 纯文本存储**: JSON + Markdown,无数据库依赖,数据永久可控
- **🔒 隐私保护**: 所有数据存储在本地,不上传云端
- **📂 时间组织**: 按日期自动分层存储(年/月/日)
- **🔍 可搜索**: 纯文本格式,支持任何文本搜索工具

---

## 🚀 快速开始

### 前置要求
- [Claude Code CLI](https://claude.ai/claude-code) - Anthropic官方AI命令行工具
- [Node.js](https://nodejs.org/) (v16+) - 可选

### 安装
```bash
# 克隆仓库
git clone https://github.com/huifer/Claude-Code-KnowCraft.git
cd Claude-Code-KnowCraft

# 启动 Claude Code
claude

# 测试功能
claude> /kb-add --type=learning-note
claude> /kb-list
```

### 更多文档
📖 [完整快速开始指南](docs/GETTING_STARTED.md)

---

## 📚 文档导航

### 使用指南
- 📖 [快速开始](docs/GETTING_STARTED.md) - 安装、配置、首次使用
- 📖 [使用指南](docs/USER_GUIDE.md) - 自然语言交互、命令参考、学习系统
- 📖 [配置说明](docs/CONFIGURATION.md) - 用户偏好、API配置、自定义模板

### 技术文档
- 📖 [系统架构](docs/ARCHITECTURE.md) - 架构图、目录结构、核心组件
- 📖 [命令参考](docs/COMMAND_REFERENCE.md) - 完整命令列表、Agent文档、Skill文档
- 📖 [开发指南](docs/DEVELOPMENT.md) - 贡献指南、添加命令、测试调试

### 项目信息
- 📖 [更新日志](docs/CHANGELOG.md) - 版本历史、新功能
- 📖 [发展路线](docs/ROADMAP.md) - 已完成功能、未来计划

---

## 🆚 功能对比

| 功能特性 | 本系统 | Obsidian | Notion | Logseq | Roam Research |
|---------|--------|----------|--------|--------|---------------|
| **存储方式** | 本地JSON+MD | 本地MD | 云端 | 本地MD | 云端 |
| **自然语言交互** | ✅ 支持 | ❌ | ❌ | ❌ | ❌ |
| **AI智能学习** | ✅ 间隔重复+费曼技巧 | ❌ | ❌ | 部分插件 | ❌ |
| **智能搜索** | ✅ AI整理结果 | 基础搜索 | 全文搜索 | 全文搜索 | 全文搜索 |
| **网络搜索集成** | ✅ Google+AI整理 | ❌ | ❌ | ❌ | ❌ |
| **版本控制** | ✅ 自动备份 | Git集成 | 历史版本 | Git集成 | 历史版本 |
| **知识关联** | ✅ 智能推荐+双向链接 | 双向链接 | 关联数据库 | 双向链接 | 双向链接 |
| **学习系统** | ✅ SM-2算法+测验 | 插件支持 | ❌ | 插件支持 | ❌ |
| **AI Agent** | ✅ 8个专业Agent | ❌ | ❌ | ❌ | ❌ |
| **PDF导入** | ✅ 自动提取 | 插件支持 | ✅ | 插件支持 | ❌ |
| **图片OCR** | ✅ 支持 | 插件支持 | ❌ | ❌ | ❌ |
| **数据库依赖** | ❌ 无依赖 | ❌ | ✅ 需要 | ❌ | ✅ 需要 |
| **离线使用** | ✅ 完全离线 | ✅ | ❌ | ✅ | ❌ |
| **隐私保护** | ✅ 完全本地 | ✅ | ⚠️ 云端 | ✅ | ⚠️ 云端 |
| **学习曲线** | 🟢 低(自然语言) | 🟡 中 | 🟢 低 | 🟡 中 | 🟡 中 |
| **定制化** | ✅ 高度可定制 | 插件生态 | 模板系统 | 插件生态 | 模板系统 |
| **价格** | ✅ 免费(MIT) | ✅ 免费 | 💰 付费 | ✅ 免费 | 💰 付费 |

---

## 🤝 常见问题

**Q: 如何配置Google搜索API？**
A: 查看 [配置说明](docs/CONFIGURATION.md#网络搜索api配置) 的详细指南。

**Q: 知识库可以迁移到其他设备吗？**
A: 可以！整个项目都是纯文本文件，可以直接复制或使用Git同步。

**Q: 支持中文搜索吗？**
A: 完全支持！所有功能都针对中文优化。

更多问题请查看 [使用指南](docs/USER_GUIDE.md)。

---

## 📄 许可证

本项目采用 **MIT License** 开源。

详见 [LICENSE](LICENSE) 文件。

---

## 🙏 致谢

感谢您选择本系统！如果您觉得这个项目对您有帮助,请给个⭐️Star支持一下！

**让我们一起,用AI改变知识管理！** 🚀
