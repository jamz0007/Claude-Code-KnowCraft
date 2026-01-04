---
argument-hint: <query> [--time=today|week|month|year|all] [--quality=high|medium|all] [--depth=beginner|intermediate|advanced] [--count=N] [--save] [--interactive]
description: 网络智能搜索 - 搜索Google并AI整理结果
allowed-tools: WebSearch, mcp__web_reader__webReader, Read, Write, Bash
---

# /kb-search-web - 网络智能搜索

## 功能
集成Google搜索API，智能搜索网络资源，AI自动提取和整理内容，支持对话式确认存储到知识库。

## 使用方式

### 基本搜索
```
/kb-search-web "React性能优化"

搜索Google，AI整理结果，交互式确认是否保存。
```

### 时间筛选
```
/kb-search-web "React Hooks" --time=month

只搜索最近一个月的内容。
选项: today, week, month, year, all
```

### 质量筛选
```
/kb-search-web "JavaScript闭包" --quality=high

只返回高质量资源（权威网站、官方文档）。
选项: high, medium, all
```

### 深度筛选
```
/kb-search-web "React状态管理" --depth=advanced

筛选内容的深度级别。
选项: beginner, intermediate, advanced
```

### 限制数量
```
/kb-search-web "TypeScript泛型" --count=5

只返回Top 5个最佳结果。
```

### 多轮搜索
```
用户: "搜索React性能优化"
系统: [显示结果]

用户: "太泛了，专注于useMemo"
系统:
  理解: 缩小搜索范围
  执行: 搜索"useMemo 性能优化 React"
  显示: 更精准的结果
```

### 自动保存模式
```
/kb-search-web "Vue3新特性" --save

搜索完成后自动保存所有结果，无需确认。
```

## 工作流程

### Step 1: 接收搜索请求
```
用户: "搜索React性能优化最新资料"

系统解析:
  - 查询词: "React性能优化"
  - 时间约束: "最新" → 最近1个月
  - 意图: 学习资料
```

### Step 2: 调用Google Search API
```
使用WebSearch工具搜索:

参数:
  query: "React性能优化"
  num: 10  # 返回10个结果
  dateRestrict: "m1"  # 最近1个月

返回: 10个搜索结果
```

### Step 3: AI智能整理
```
对每个搜索结果:

1. 获取URL
2. 使用mcp__web_reader__webReader抓取全文
3. AI提取关键信息:
   - 核心观点 (3-5个要点)
   - 代码示例 (如有)
   - 最佳实践
   - 注意事项
   - 适用场景
4. 生成摘要 (150-200字)
5. 评分相关性 (0-100)
```

### Step 4: 输出整理结果
```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
🔍 React性能优化 - 搜索结果整理
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

搜索到 10 个结果，AI整理后推荐 3 个:

1. ⭐⭐⭐⭐⭐ [98分] React性能优化完全指南
   发布: 2024-12-15
   链接: https://example.com/react-performance

   核心要点:
   • 使用React.memo避免不必要的重渲染
   • useMemo和useCallback优化计算和函数
   • 虚拟列表处理大量数据（react-window）
   • 代码分割和懒加载减少初始加载

   最佳实践:
   - 性能测量先行（React Profiler API）
   - 避免过早优化
   - 关注真实用户体验指标（Core Web Vitals）

   摘要:
   这篇文章系统介绍了React性能优化的全流程，
   从测量工具的使用到具体的优化技巧。
   作者通过实际案例演示了如何识别性能瓶颈，
   并提供了详细的优化方案和代码示例。
   特别强调了"测量优先"的原则，
   建议在优化前先用Profiler分析，
   避免盲目优化。文章还覆盖了服务端渲染、
   图片优化、缓存策略等高级主题。

2. ⭐⭐⭐⭐☆ [85分] React Hooks性能陷阱
   发布: 2024-11-20
   ...

3. ⭐⭐⭐⭐☆ [82分] 大型React应用性能优化实战
   发布: 2024-12-01
   ...

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
💡 下一步操作
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

选择操作:
1. 保存条目 - 输入序号（如: 1,3 或 1-3）
2. 继续搜索 - 输入更多关键词
3. 查看原文 - open 序号
4. 结束搜索 - done 或 exit

你的选择:
```

### Step 5: 对话式保存
```
用户: "1,3"

系统:
  确认要保存以下2个条目吗？

  1. React性能优化完全指南
     来源: https://example.com/react-performance
     建议标签: react, performance, optimization
     建议分类: learning

  3. 大型React应用性能优化实战
     来源: https://example.com/react-performance-large
     建议标签: react, performance, scaling
     建议分类: learning

  是否修改标签？(回车使用建议 / 输入新标签)

用户: [回车]

系统:
  ✅ 正在保存...

  [1/2] 抓取内容: React性能优化完全指南
  [2/2] 抓取内容: 大型React应用性能优化实战

  ✅ 已保存2个条目！
    [2026-01-04-150001] React性能优化完全指南
    [2026-01-04-150002] 大型React应用性能优化实战

  💡 这2个条目都讨论性能优化，是否创建关联？
  输入: y(是) / n(否) / done

用户: "y"

系统:
  ✅ 已创建关联！
    2026-01-04-150001 ←→ 2026-01-04-150002 (type: related)

  还需要其他帮助吗？
```

## 高级功能

### 多轮搜索

```
第1轮:
用户: "搜索React状态管理"
系统: [显示结果]

第2轮 (细化):
用户: "专注于Redux"
系统: [搜索"React Redux状态管理"，显示更精准结果]

第3轮 (对比):
用户: "加上Zustand的对比"
系统: [搜索"Redux vs Zustand"，显示对比文章]
```

### 智能筛选

**时间筛选**:
```
--time=today     # 今天
--time=week      # 本周
--time=month     # 本月（默认）
--time=year      # 今年
--time=all       # 不限时间
```

**质量筛选**:
```
--quality=high   # 只显示权威网站
--quality=medium # 中等质量以上
--quality=all    # 所有结果（默认）
```

权威网站包括:
- 官方文档 (react.dev, developer.mozilla.org)
- 知名博客 (overreacted.io, danabramov.com)
- GitHub官方仓库
- 技术社区 (dev.to, css-tricks.com)

**深度筛选**:
```
--depth=beginner     # 入门教程
--depth=intermediate # 中级文章
--depth=advanced     # 深度分析
```

判断标准:
- beginner: 包含"入门"、"教程"、"快速开始"
- intermediate: 包含"实践"、"应用"、"案例"
- advanced: 包含"原理"、"源码"、"底层"、"深度"

### 批量操作

```
保存序号范围:
  "1-3"     → 保存1,2,3
  "1,3,5"   → 保存1,3,5
  "all"     → 保存所有推荐结果
  "none"    → 不保存，继续搜索
```

## 搜索结果质量评估

### 评分标准 (0-100)

```python
评分维度:

1. 内容质量 (40分)
   - 内容完整性: 15分
   - 代码示例质量: 15分
   - 解释清晰度: 10分

2. 权威性 (30分)
   - 来源权威度: 20分
   - 作者知名度: 10分

3. 时效性 (15分)
   - 发布时间: 10分 (越新分数越高)
   - 内容更新频率: 5分

4. 相关性 (15分)
   - 主题匹配度: 10分
   - 关键词覆盖: 5分

总分 = 质量分 + 权威分 + 时效分 + 相关分
```

### 筛选条件

```
高质量 (--quality=high):
  - 总分 > 80
  - 权威网站
  - 最近1年发布

中质量 (--quality=medium):
  - 总分 > 60
  - 相对权威
  - 最近2年发布

所有质量 (--quality=all):
  - 总分 > 40
  - 任何来源
  - 任何时间
```

## 交互式命令

### 搜索中的命令

```
搜索结果页可用命令:

"1" 或 "保存1"     → 保存第1个
"1,3" 或 "保存1,3"  → 保存第1和第3个
"1-3"             → 保存第1到第3个
"all"             → 保存所有结果

"open 1"          → 在浏览器打开第1个
"open all"        → 打开所有结果链接

"more 1"          → 展开第1个的详细内容
"detail 1"        → 显示第1个的完整摘要

"search 关键词"    → 继续搜索新关键词
"refine 约束"     → 细化当前搜索

"clear"           → 清空搜索历史
"help"            → 显示帮助

"done" 或 "exit"   → 结束搜索
```

## API配置

### Google Custom Search API

```json
{
  "google": {
    "apiKey": "YOUR_API_KEY",
    "cx": "YOUR_SEARCH_ENGINE_ID",
    "freeQuota": 100,
    "usedToday": 0,
    "quotaReset": "00:00:00"
  }
}
```

### 获取API密钥

1. 访问 [Google Custom Search API](https://developers.google.com/custom-search/v1/overview)
2. 创建项目并获取API Key
3. 创建Search Engine (Programmable Search Engine)
4. 配置搜索引擎:
   - 要搜索的网站: 全网或特定域名
   - 语言: 中文和英文
   - 安全搜索: 关闭

### 备选API: Bing Search API

```json
{
  "bing": {
    "apiKey": "YOUR_BING_KEY",
    "asBackup": true,
    "freeQuota": 1000,
    "quotaPeriod": "month"
  }
}
```

## 配置文件

创建 `d:/my-know/config/search-api.json`:

```json
{
  "version": "1.0",
  "primary": "google",
  "google": {
    "enabled": true,
    "apiKey": "",
    "cx": "",
    "quota": {
      "daily": 100,
      "used": 0,
      "reset": "2026-01-05T00:00:00Z"
    }
  },
  "bing": {
    "enabled": false,
    "apiKey": "",
    "asBackup": true
  },
  "defaults": {
    "numResults": 10,
    "timeRange": "month",
    "quality": "medium",
    "depth": "intermediate",
    "language": "zh-CN,en"
  },
  "cache": {
    "enabled": true,
    "ttl": 86400,
    "maxSize": 100
  }
}
```

## 输出格式

### 保存的内容格式

保存到知识库的条目格式:

```yaml
---
id: 2026-01-04-150001
title: "React性能优化完全指南"
type: learning-note
category: learning
tags: [react, performance, optimization]

source:
  type: web-search
  url: "https://example.com/react-performance"
  domain: "example.com"
  author: "作者名"
  published: "2024-12-15T00:00:00Z"
  accessed: "2026-01-04T14:30:00Z"
  searched: "React性能优化"

  # AI整理
  summary: "..."
  keyPoints:
    - "使用React.memo避免不必要的重渲染"
    - "useMemo和useCallback优化计算和函数"
    - "虚拟列表处理大量数据"

  bestPractices:
    - "性能测量先行（React Profiler API）"
    - "避免过早优化"
    - "关注真实用户体验指标"

  score: 98

created: 2026-01-04T14:30:00Z
version: 1
links: []
backlinks: []
---

# React性能优化完全指南

## 核心要点

### 1. 使用React.memo避免不必要的重渲染

...

## 最佳实践

...

## 代码示例

...

[完整内容...]
```

## 使用示例

### 示例1: 基础搜索
```
/kb-search-web "React Hooks教程"

输出:
  🔍 搜索到 10 个结果
  整理后推荐 3 个

  1. ⭐⭐⭐⭐⭐ [95分] React Hooks完整指南
  2. ⭐⭐⭐⭐☆ [88分] Hooks实战案例
  3. ⭐⭐⭐⭐☆ [82分] Hooks常见错误

  选择: _
```

### 示例2: 多轮搜索
```
第1轮:
/kb-search-web "React性能"
→ [显示10个结果]

第2轮:
"太泛了，专注于useMemo"
→ 搜索"useMemo 性能优化"
→ [显示5个精准结果]

第3轮:
"加上代码示例"
→ 搜索"useMemo 代码示例 性能"
→ [显示带代码示例的文章]
```

### 示例3: 保存流程
```
/kb-search-web "Vue3组合式API"
→ [显示结果]

"1,2"
→ 保存第1和第2个

"y"
→ 确认标签

"y"
→ 创建关联

✅ 完成！
```

## 注意事项

### API配额

```
Google Custom Search API:
  - 免费额度: 每天100次
  - 超额后: $5 per 1000次
  - 建议: 缓存搜索结果，避免重复搜索

Bing Search API (备选):
  - 免费额度: 每月1000次
  - 超额后: 按使用量计费
  - 适合: 作为备用方案
```

### 内容抓取

```
注意事项:
- 尊重网站版权
- 仅用于个人学习
- 不要商业使用
- 保留来源链接

抓取策略:
- 使用Readability算法提取正文
- 移除广告和导航
- 保留代码和图片
- 标注内容来源
```

### 隐私保护

```
数据安全:
- 对话历史仅本地存储
- 搜索查询不上传个人信息
- 保存的内容加密存储

建议:
- 定期清理搜索历史
- 不要搜索敏感信息
- 遵守网站服务条款
```

## 与其他命令配合

### 搜索后学习
```
/kb-search-web "React Hooks"
→ 保存结果

/kb-learn "React Hooks" --items=[保存的ID]
→ 创建学习计划
```

### 搜索后测试
```
/kb-search-web "JavaScript闭包"
→ 保存结果

/kb-quiz "JavaScript闭包"
→ 测试掌握程度
```

### 搜索后整理
```
/kb-search-web "TypeScript泛型"
→ 保存多个结果

/kb-link [id1] [id2]
→ 创建关联

@knowledge-architect "整理TypeScript知识"
→ 优化知识结构
```

## 最佳实践

### 1. 精确搜索
```
好的搜索词:
✅ "React Hooks性能优化"
✅ "useState vs useReducer"
✅ "JavaScript闭包实际应用"

不好的搜索词:
❌ "React" (太泛)
❌ "学习" (不明确)
❌ "怎么" (模糊)
```

### 2. 逐步细化
```
从宽泛到精确:
1. "React性能"       → 宽泛搜索
2. "专注于useMemo"   → 细化搜索
3. "加上代码示例"    → 进一步细化
4. "中级难度"        → 最终精准结果
```

### 3. 理解筛选
```
根据需求选择:
- 学习新知识: --depth=beginner
- 解决问题: --quality=high
- 最近资料: --time=month
- 深入研究: --depth=advanced
```

### 4. 有效保存
```
保存策略:
- 只保存真正需要的
- 及时添加笔记和标注
- 创建相关条目的关联
- 定期复习和整理
```

## 故障排除

### API错误
```
问题: "API quota exceeded"
解决:
  1. 检查配额使用情况
  2. 等待配额重置（每天0点）
  3. 切换到备用API（Bing）
  4. 使用缓存结果
```

### 抓取失败
```
问题: "无法抓取网页内容"
解决:
  1. 检查URL是否有效
  2. 网站可能有反爬虫
  3. 手动复制URL到浏览器
  4. 使用 /kb-from-url 手动抓取
```

### 整理质量差
```
问题: "AI摘要不准确"
解决:
  1. 查看原文确认
  2. 手动编辑摘要
  3. 提供反馈优化
  4. 调整筛选条件
```

## 扩展功能（未来）

### 1. 语音搜索
```
/kb-search-web --voice "React性能优化"
使用语音输入搜索
```

### 2. 图像搜索
```
/kb-search-web --image screenshot.png
使用图片搜索相关内容
```

### 3. 学术搜索
```
/kb-search-web --scholar "React performance"
搜索学术论文（Google Scholar）
```

### 4. 视频搜索
```
/kb-search-web --video "React Hooks教程"
搜索视频教程
```
