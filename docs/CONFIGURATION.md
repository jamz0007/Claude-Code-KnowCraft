# ⚙️ 配置说明

> 详细说明如何配置和自定义个人知识系统

## 📑 目录

- [配置文件概览](#配置文件概览)
- [用户偏好配置](#用户偏好配置)
- [网络搜索API配置](#网络搜索api配置)
- [自定义模板](#自定义模板)
- [配置最佳实践](#配置最佳实践)

---

## 配置文件概览

| 配置文件 | 位置 | 用途 | 必需 |
|---------|------|------|------|
| `user-preferences.json` | `config/` | 用户偏好和行为模式 | ✅ |
| `search-api.json` | `config/` | 网络搜索API密钥 | ⚠️ 可选 |
| `settings.local.json` | `.claude/` | Claude Code本地设置 | ✅ |
| `conversation-history/index.json` | `.claude/config/` | 对话历史记录 | ✅ |

---

## 用户偏好配置

**文件**: `config/user-preferences.json`

### 完整配置示例

```json
{
  "version": "1.0",
  "lastUpdated": "2026-01-04T14:30:00Z",

  // 用户画像
  "profile": {
    "name": "用户",
    "learningStyle": "visual",
    "expertiseLevel": "intermediate",
    "primaryInterests": ["frontend", "react", "javascript"]
  },

  // 默认设置
  "defaults": {
    "category": "learning",
    "tags": ["frontend"],
    "template": "learning-note",
    "searchSort": "relevance",
    "searchFormat": "short",
    "editor": "vscode"
  },

  // 行为模式(系统自动学习)
  "patterns": {
    "commonTopics": [
      {"topic": "React", "frequency": 45, "lastUsed": "2026-01-04"},
      {"topic": "JavaScript", "frequency": 32, "lastUsed": "2026-01-03"}
    ],
    "commonTags": [
      {"tag": "react", "frequency": 50, "accuracy": 0.95},
      {"tag": "hooks", "frequency": 28, "accuracy": 0.92}
    ],
    "categoryDistribution": {
      "learning": 0.70,
      "code": 0.20,
      "projects": 0.08,
      "personal": 0.02
    }
  },

  // 智能建议设置
  "recommendations": {
    "enabled": true,
    "aggressiveness": "moderate",
    "showAfter": ["kb-add", "kb-search", "kb-quiz", "kb-review"],
    "maxSuggestions": 3
  },

  // 界面设置
  "ui": {
    "mode": "hybrid",
    "naturalLanguage": {
      "enabled": true,
      "confirmThreshold": 0.7
    }
  }
}
```

### 配置项详解

#### 用户画像 (profile)

```json
"profile": {
  "name": "用户",                      // 显示名称
  "learningStyle": "visual",          // 学习风格
  "expertiseLevel": "intermediate",   // 专业水平
  "primaryInterests": ["frontend", "react", "javascript"]
}
```

**learningStyle 选项**:
- `visual`: 视觉学习者（推荐图表、代码示例）
- `auditory`: 听觉学习者（推荐语音讲解）
- `reading`: 阅读学习者（推荐文字文档）
- `kinesthetic`: 动觉学习者（推荐实践练习）

**expertiseLevel 选项**:
- `beginner`: 初学者（更多基础解释）
- `intermediate`: 中级（平衡深度和广度）
- `advanced`: 高级（深入技术细节）

#### 默认设置 (defaults)

```json
"defaults": {
  "category": "learning",              // 默认分类
  "tags": ["frontend"],                // 默认标签
  "template": "learning-note",         // 默认模板
  "searchSort": "relevance",           // 默认排序方式
  "searchFormat": "short",             // 默认显示格式
  "editor": "vscode"                   // 默认编辑器
}
```

**searchSort 选项**:
- `relevance`: 相关性排序
- `recent`: 最近创建
- `review-date`: 复习时间
- `alpha`: 字母顺序

**searchFormat 选项**:
- `short`: 简短格式（标题+标签）
- `medium`: 中等格式（+摘要）
- `long`: 完整格式（+全文）

#### 行为模式 (patterns)

系统自动学习，记录使用习惯：

```json
"patterns": {
  "commonTopics": [
    {"topic": "React", "frequency": 45, "lastUsed": "2026-01-04"}
  ],
  "commonTags": [
    {"tag": "react", "frequency": 50, "accuracy": 0.95}
  ],
  "categoryDistribution": {
    "learning": 0.70,
    "code": 0.20,
    "projects": 0.08,
    "personal": 0.02
  }
}
```

**说明**:
- 此部分由系统自动维护，手动编辑可能影响准确性
- `frequency`: 使用频率
- `accuracy`: 推荐准确度（0-1）
- `categoryDistribution`: 各类别的使用比例

#### 智能建议设置 (recommendations)

```json
"recommendations": {
  "enabled": true,                     // 是否启用智能建议
  "aggressiveness": "moderate",        // 建议激进程度
  "showAfter": ["kb-add", "kb-search"], // 触发建议的命令
  "maxSuggestions": 3                  // 最大建议数量
}
```

**aggressiveness 选项**:
- `conservative`: 保守（只给高置信度建议）
- `moderate`: 适中（平衡准确性和覆盖面）
- `aggressive`: 激进（给更多建议）

#### 界面设置 (ui)

```json
"ui": {
  "mode": "hybrid",                     // 界面模式
  "naturalLanguage": {
    "enabled": true,                    // 启用自然语言
    "confirmThreshold": 0.7             // 置信度阈值
  }
}
```

**mode 选项**:
- `command`: 纯命令模式（只用斜杠命令）
- `natural`: 纯自然语言模式
- `hybrid`: 混合模式（两者都可以）

**confirmThreshold 说明**:
- 当自然语言识别置信度 >= 此值时，直接执行
- 0.7 = 70%置信度直接执行
- 降低此值会更频繁地执行，但可能误判

---

## 网络搜索API配置

**文件**: `config/search-api.json` (需创建)

### 基本配置

```json
{
  "google": {
    "enabled": true,
    "apiKey": "YOUR_GOOGLE_API_KEY",
    "cx": "YOUR_SEARCH_ENGINE_ID"
  }
}
```

### 获取Google API密钥

#### 步骤1: 创建Google Cloud项目

1. 访问 [Google Cloud Console](https://console.cloud.google.com/)
2. 点击"选择项目" → "新建项目"
3. 输入项目名称，例如"My Knowledge System"
4. 点击"创建"

#### 步骤2: 启用Custom Search API

1. 在左侧菜单选择"API和服务" → "库"
2. 搜索"Custom Search API"
3. 点击"Custom Search API"
4. 点击"启用"

#### 步骤3: 创建API密钥

1. 在左侧菜单选择"API和服务" → "凭据"
2. 点击"创建凭据" → "API密钥"
3. 复制生成的API密钥
4. （可选）点击"编辑API密钥"，设置限制：
   - **应用限制**: IP地址或Referer
   - **API限制**: 只选择Custom Search API
   - **配额**: 设置每日请求限制

#### 步骤4: 创建搜索引擎

1. 访问 [Programmable Search Engine](https://programmablesearchengine.google.com/)
2. 点击"添加"
3. 填写搜索引擎信息：
   - **要搜索的网站**: 留空（全网搜索）
   - **语言**: 选择您的偏好语言（如"中文"）
4. 点击"创建"
5. 在搜索引擎列表中，找到刚创建的搜索引擎
6. 点击"控制面板"
7. 在"设置"标签页找到"搜索引擎ID (CX)"
8. 复制CX值

#### 步骤5: 配置到系统

编辑 `config/search-api.json`:

```json
{
  "google": {
    "enabled": true,
    "apiKey": "AIzaSyXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX",
    "cx": "012345678901234567890:abcdefg_hijk"
  }
}
```

### 测试配置

```bash
claude> /kb-search-web "测试"
```

如果返回搜索结果，说明配置成功！

### 配额说明

**免费配额**（每天）:
- Custom Search API: 100次查询
- 超出后需要付费升级

**监控使用量**:
1. 访问 [Google Cloud Console](https://console.cloud.google.com/)
2. 选择项目
3. "API和服务" → "仪表板"
4. 查看Custom Search API的使用情况

### 成本控制

**降低API使用**:
```json
{
  "google": {
    "enabled": false,  // 关闭网络搜索
    // 或设置缓存
    "cache": {
      "enabled": true,
      "ttl": 86400  // 缓存24小时
    }
  }
}
```

---

## 自定义模板

**模板位置**: `templates/`

### 创建自定义模板

#### 步骤1: 创建模板文件

```bash
vim templates/my-custom-template.md
```

#### 步骤2: 编写模板内容

```markdown
---
id: {{id}}
title: {{title}}
type: custom-type
category: custom
tags: {{tags}}
created: {{created}}
modified: {{modified}}
version: 1
---

# {{title}}

## 概述


## 详细内容


## 关键点


## 代码示例


## 参考资料

- [链接描述](url)


## 相关笔记

- [相关主题](../path/to/note.md)
```

### 模板变量

系统会自动替换以下变量：

| 变量 | 说明 | 示例 |
|------|------|------|
| `{{id}}` | 唯一标识 | 2026-01-04-120000 |
| `{{title}}` | 标题 | React Hooks详解 |
| `{{tags}}` | 标签列表 | react, hooks |
| `{{created}}` | 创建时间 | 2026-01-04T12:00:00Z |
| `{{modified}}` | 修改时间 | 2026-01-04T12:00:00Z |

### 使用自定义模板

```bash
# 指定模板
/kb-add --template=my-custom-template

# 或通过自然语言
"用my-custom-template模板创建笔记"
```

### 预置模板

系统提供4个预置模板：

1. **learning-note.md**: 学习笔记模板
2. **code-snippet.md**: 代码片段模板
3. **project-doc.md**: 项目文档模板
4. **research-note.md**: 研究笔记模板

---

## 配置最佳实践

### 1. 渐进式配置

```bash
# 第一周: 使用默认配置
# 观察系统自动学习的行为模式

# 第二周: 调整基础设置
# - 修改默认分类和标签
# - 设置学习风格

# 第三周: 启用高级功能
# - 配置网络搜索API
# - 调整建议激进程度
```

### 2. 备份配置

```bash
# 定期备份配置文件
cp config/user-preferences.json config/user-preferences.json.backup

# 或使用Git
git add config/
git commit -m "Backup configuration"
```

### 3. 隐私保护

```json
{
  "privacy": {
    "saveHistory": true,   // 保存历史以支持上下文理解
    "analytics": true,     // 允许分析以改进建议
    "shareData": false     // 始终设为false,不分享到云端
  }
}
```

**重要提示**:
- 所有数据存储在本地
- 不上传任何内容到云端
- 完全掌控你的知识

### 4. 性能优化

```json
{
  "performance": {
    "cacheSize": 100,        // 缓存条目数量
    "indexRefresh": "auto",  // 索引刷新策略
    "parallelSearch": true   // 并行搜索
  }
}
```

### 5. 团队协作

如果需要团队协作：

```bash
# 使用Git同步配置
git init
git remote add origin <your-repo>
git push

# 共享配置（排除敏感信息）
echo "config/search-api.json" >> .gitignore
```

---

## 📚 相关文档

- [快速开始](GETTING_STARTED.md) - 首次配置
- [系统架构](ARCHITECTURE.md) - 理解配置的作用
- [使用指南](USER_GUIDE.md) - 如何使用系统功能

---

**合理配置，让系统更懂你！** 🚀
