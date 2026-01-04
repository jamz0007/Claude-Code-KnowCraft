# 🚀 快速开始指南

> 本指南将帮助您安装、配置并首次使用个人知识系统

## 📋 前置要求

### 必需软件

- **[Claude Code CLI](https://claude.ai/claude-code)** - Anthropic官方AI命令行工具

  这是本系统的核心引擎，提供自然语言交互和AI能力。

- **[Node.js](https://nodejs.org/) (v16+)** - 可选

  如果需要使用扩展功能（如自定义脚本），需要安装Node.js。

### 可选服务（用于网络搜索）

- **[Google Custom Search API](https://developers.google.com/custom-search/v1/overview)** - 用于智能网络搜索
- **Google Account** - 创建搜索引擎

### 检查环境

在开始之前，请验证您的环境：

```bash
# 检查Claude Code是否安装
claude --version

# 检查Node.js(可选)
node --version
```

如果 `claude --version` 返回版本号，说明已安装。如果没有，请访问 [Claude Code 官网](https://claude.ai/claude-code) 下载安装。

---

## 📥 安装步骤

### 方式1: Git克隆（推荐）

使用Git克隆可以获得完整的版本历史和后续更新能力。

```bash
# 克隆仓库
git clone https://github.com/huifer/Claude-Code-KnowCraft.git
cd Claude-Code-KnowCraft

# 验证文件结构
ls -la
# 应该看到: .claude/, knowledge/, config/, templates/ 等目录
```

### 方式2: 下载压缩包

如果不熟悉Git，可以直接下载压缩包。

```bash
# 下载并解压
unzip my-know-main.zip
cd my-know-main
```

---

## ⚙️ 首次配置

### 1. 配置Claude Code

在项目根目录启动Claude Code：

```bash
claude
```

**首次启动会引导配置：**
- 选择编辑器（VS Code / Vim / 其他）
- 配置API密钥
- 选择工作目录

按照屏幕提示完成配置即可。

### 2. 验证系统功能

配置完成后，测试基本功能是否正常。

#### 测试基本命令

```bash
claude> /kb-add --type=learning-note
# 输入标题: 测试笔记
# 输入内容: 这是一条测试笔记
# 应该成功创建并返回ID，例如: 2026-01-04-120000
```

#### 测试列表命令

```bash
claude> /kb-list
# 应该显示刚才创建的笔记
```

#### 测试自然语言

```bash
claude> "搜索测试"
# 应该找到刚才的笔记
```

如果以上测试都通过，说明系统运行正常！

### 3. 配置网络搜索（可选）

网络搜索功能可以帮您从Google搜索并自动整理最新资料。这是可选功能，但强烈推荐配置。

#### 创建配置文件

```bash
# 创建搜索API配置
vim config/search-api.json
```

#### 添加配置内容

```json
{
  "google": {
    "enabled": true,
    "apiKey": "YOUR_GOOGLE_API_KEY",
    "cx": "YOUR_SEARCH_ENGINE_ID"
  }
}
```

#### 获取Google API密钥

**步骤1：创建Google Cloud项目**

1. 访问 [Google Cloud Console](https://console.cloud.google.com/)
2. 创建新项目或选择现有项目
3. 在"API和服务"中启用"Custom Search API"

**步骤2：创建API密钥**

1. 进入"凭据"页面
2. 点击"创建凭据" → "API密钥"
3. 复制生成的API密钥

**步骤3：创建搜索引擎**

1. 访问 [Programmable Search Engine](https://programmablesearchengine.google.com/)
2. 点击"添加"
3. 设置搜索引擎：
   - 要搜索的网站：留空（全网搜索）
   - 语言：选择您的偏好语言
4. 创建后，进入"设置"
5. 在"基本信息"中找到"搜索引擎ID (CX)"
6. 复制CX值

**步骤4：配置到系统**

将API Key和CX填入 `config/search-api.json` 文件。

#### 测试网络搜索

```bash
claude> /kb-search-web "React性能优化"
# 应该返回搜索结果并AI整理
```

### 4. 自定义用户偏好（可选）

系统会学习您的使用习惯，但您也可以预设偏好。

```bash
# 编辑用户偏好
vim config/user-preferences.json
```

**可配置项：**

- `learningStyle`: 学习风格 (visual/auditory/reading/kinesthetic)
- `defaults.category`: 默认分类
- `defaults.tags`: 默认标签
- `ui.mode`: 界面模式 (command/hybrid/natural)
- `recommendations.enabled`: 是否启用智能建议

详细配置说明请参考 [配置文档](CONFIGURATION.md)。

---

## 🎉 第一个知识条目

配置完成后，让我们创建第一个知识条目。

### 使用自然语言（推荐）

```bash
claude> "记一条React学习笔记"
```

系统会自动：
1. **识别意图** → 识别为"添加知识"
2. **推荐标签** → 基于偏好学习推荐 `react`, `frontend`
3. **提示输入** → 请求标题和内容
4. **创建条目** → 生成唯一ID并保存
5. **智能建议** → 提示创建关联、开始学习等

示例对话：
```
claude> "记一条React学习笔记"

📝 添加知识笔记

推荐标签: react, frontend
标题: useState Hook详解

内容: useState是React提供的Hook，用于在函数组件中添加状态...
...

✅ 已创建: 2026-01-04-120000

💡 智能建议
  发现您有3条React相关笔记，是否创建关联？
  [92%] 创建关联: /kb-link 2026-01-04-120000 <other-id>
```

### 使用斜杠命令（传统方式）

如果您更喜欢传统命令行方式：

```bash
claude> /kb-add --type=learning-note --tags=react,hooks
```

按提示输入：
- 标题: React useState Hook详解
- 内容: useState是React提供的Hook...

效果与自然语言方式完全相同。

---

## ✅ 验证安装

最后，运行完整的系统验证：

### 查看系统状态

```bash
claude> /kb-list --stats
```

**预期输出：**
```
📊 知识库统计

总条目: 2+
总标签: 5+
总链接: 0
系统状态: ✅ 正常

分类分布:
  learning: 70%
  code: 20%
  projects: 8%
  personal: 2%

最近更新:
  2026-01-04-120000: React useState Hook详解
  2026-01-04-115500: 测试笔记
```

### 测试学习系统

```bash
claude> /kb-quiz "React" --difficulty=easy
```

系统会生成关于React的测验题，评估您的掌握程度。

### 测试网络搜索（如已配置）

```bash
claude> /kb-search-web "React性能优化"
```

应该返回搜索结果并AI整理后的摘要。

---

## 🆘 遇到问题？

### 常见问题

**Q: Claude Code命令找不到？**

A: 请确认：
1. 已完成Claude Code安装
2. 已重启终端或重新加载环境变量
3. 如果使用Windows，可能需要以管理员身份运行

**Q: 知识条目创建失败？**

A: 检查：
1. 项目目录权限是否正确
2. `knowledge/` 目录是否存在
3. 查看错误日志：`cat .claude/debug.log`

**Q: 网络搜索不工作？**

A: 确认：
1. API密钥和CX配置正确
2. Google Cloud账户有配额
3. Custom Search API已启用

**Q: 中文显示乱码？**

A: 设置终端编码：
- Windows: `chcp 65001`
- Linux/Mac: 确保终端使用UTF-8编码

---

## 📚 下一步

恭喜！您已经成功安装并配置了个人知识系统。

**推荐下一步：**

1. 📖 阅读 [使用指南](USER_GUIDE.md) - 了解自然语言交互、命令参考等
2. 📖 阅读 [配置说明](CONFIGURATION.md) - 深度自定义系统行为
3. 🎯 创建您的第一条学习笔记 - 开始积累知识！

**快速命令参考：**

| 命令 | 功能 |
|------|------|
| `/kb-add` | 添加知识 |
| `/kb-list` | 列出知识 |
| `/kb-search` | 搜索知识 |
| `/kb-quiz` | 智能测验 |
| `/kb-review` | 间隔复习 |

更多命令请查看 [命令参考](COMMAND_REFERENCE.md)。

---

**祝您使用愉快！用AI改变知识管理！** 🚀
