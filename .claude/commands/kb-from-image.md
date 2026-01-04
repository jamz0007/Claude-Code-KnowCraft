---
argument-hint: <image-file> [--title=TITLE] [--tags=TAGS] [--category=CAT] [--ocr-engine=auto|google|tesseract]
description: 从图片提取文字并创建知识条目
allowed-tools: Read, mcp__4_5v_mcp__analyze_image
---

# /kb-from-image - 图片 OCR 和知识提取

## 功能
从图片中提取文字，使用 Claude 视觉能力理解内容，生成描述性知识条目。

## 使用方式

### 基本用法
```
/kb-from-image screenshot.png

从图片提取文字并创建知识条目。
```

### 指定标题
```
/kb-from-image whiteboard.jpg --title="团队讨论记录 - React 架构"
```

### 代码截图
```
/kb-from-image code-screenshot.png --tags=code,javascript

识别并提取代码。
```

### 手写笔记
```
/kb-from-image handwritten-notes.jpg

识别手写文字。
```

### 批量处理
```
/kb-from-image *.jpg --batch

批量处理多张图片。
```

## 参数说明

- `image-file`: 图片文件路径 (必需)
- `--title`: 自定义标题 (默认: 从图片内容提取)
- `--tags`: 指定标签 (逗号分隔)
- `--category`: 指定分类
- `--ocr-engine`: OCR 引擎选择 (auto|google|tesseract)
- `--language`: 语言代码 (zh-CN, en-US)
- `--batch`: 批量模式
- `--detect-code`: 检测并提取代码
- `--enhance`: 增强图片质量(预处理)

## 工作流程

### 1. 图片读取
```
使用 Claude 视觉能力:
- 读取图片文件
- 识别图片类型
- 检测图片质量
- 分析图片内容
```

### 2. 内容识别
```
识别图片中的内容:
- 文字内容(OCR)
- 代码片段
- 图表结构
- 布局信息
```

### 3. 文字提取
```
使用 OCR 技术:
- 提取所有文字
- 保留布局结构
- 识别标题层级
- 提取列表和表格
```

### 4. 内容理解
```
使用 AI 分析:
- 理解图片主题
- 识别关键信息
- 提取核心概念
- 生成描述
```

### 5. 生成条目
```
创建知识条目:
- 生成时间戳 ID
- 添加描述
- 提取内容
- 保存图片
```

## 输出示例

### 代码截图
```
/kb-from-image react-code.png --detect-code

✅ 图片内容提取完成!

文件: react-code.png
大小: 256 KB
类型: PNG

识别内容类型: 代码截图

提取的代码:
\```javascript
function UserProfile({ name, email }) {
  return (
    <div>
      <h1>{name}</h1>
      <p>{email}</p>
    </div>
  );
}
\```

语言: JavaScript (React)
组件名: UserProfile
Props: name, email

生成的条目:
[2026-01-04-150001] React 函数组件示例 - UserProfile
类型: code-snippet
分类: code
标签: [react, component, functional, props, screenshot]

描述:
React 函数组件示例，展示了如何定义一个简单的
用户配置文件组件，接收 name 和 email 作为 props。

附件:
- 原图: knowledge/assets/2026-01-04-150001.png
```

### 手写笔记
```
/kb-from-image handwritten-notes.jpg

✅ 图片内容提取完成!

文件: handwritten-notes.jpg
类型: 手写笔记

识别文字:
React Hooks 学习笔记
==================

1. useState
   - 用于状态管理
   - const [state, setState] = useState(initial)

2. useEffect
   - 用于副作用
   - 类似 componentDidMount

3. 规则
   - 只在顶层调用
   - 不能在条件语句中

置信度: 85%

生成的条目:
[2026-01-04-150002] React Hooks 手写笔记
类型: learning-note
分类: learning
标签: [react, hooks, handwritten, notes]

提取的内容:
# React Hooks 学习笔记

## 1. useState
- 用于状态管理
- const [state, setState] = useState(initial)

## 2. useEffect
- 用于副作用
- 类似 componentDidMount

## 3. 规则
- 只在顶层调用
- 不能在条件语句中

附件:
- 原图: knowledge/assets/2026-01-04-150002.jpg
```

### 白板照片
```
/kb-from-image whiteboard.jpg

✅ 图片内容提取完成!

文件: whiteboard.jpg
场景: 白板讨论

识别内容:
=============
系统架构讨论
=============

架构方案: 微服务
技术栈:
  - 前端: React + TypeScript
  - 后端: Node.js + Express
  - 数据库: PostgreSQL
  - 缓存: Redis

模块划分:
  - 用户服务
  - 订单服务
  - 支付服务

待讨论:
  1. 消息队列选型
  2. 监控方案
  3. 部署流程

参与者: 团队 A
日期: 2025-01-03

生成的条目:
[2026-01-04-150003] 微服务架构讨论 - 白板记录
类型: project-doc
分类: projects
标签: [architecture, microservices, whiteboard, meeting]

描述:
团队关于微服务架构的白板讨论记录，
包含技术栈选择、模块划分和待讨论事项。

附件:
- 原图: knowledge/assets/2026-01-04-150003.jpg
```

### 书籍页面
```
/kb-from-image book-page.jpg

✅ 图片内容提取完成!

文件: book-page.jpg
类型: 书籍页面

识别章节:
第3章: JavaScript 异步编程

内容摘要:
JavaScript 是单线程语言，通过事件循环处理异步操作。
主要方式包括回调函数、Promise 和 async/await。

代码示例:
\```javascript
fetch('/api/data')
  .then(response => response.json())
  .then(data => console.log(data))
  .catch(error => console.error(error));
\```

关键概念:
- Event Loop
- Callback Queue
- Promise
- async/await

生成的条目:
[2026-01-04-150004] JavaScript 异步编程 - 读书笔记
类型: learning-note
分类: learning
标签: [javascript, async, book, notes]

附件:
- 原图: knowledge/assets/2026-01-04-150004.jpg
```

## 内容识别

### 图片类型识别

#### 代码截图
```
特征:
- 等宽字体
- 语法高亮
- 行号
- IDE 界面

处理:
- 提取代码
- 识别语言
- 保留缩进
- 提取注释
```

#### 手写笔记
```
特征:
- 不规则字体
- 手绘图形
- 箭头和线条
- 涂改痕迹

处理:
- OCR 识别
- 理解布局
- 重构结构
- 补充格式
```

#### 白板照片
```
特征:
- 大面积文字
- 手绘图形
- 组织结构图
- 流程图

处理:
- 提取文字
- 描述图表
- 识别关系
- 梳理逻辑
```

#### 书籍页面
```
特征:
- 排版规整
- 章节标题
- 段落清晰
- 页眉页脚

处理:
- 识别章节
- 提取正文
- 去除页眉页脚
- 保留结构
```

### 智能提取

#### 文字提取 (OCR)
```
使用多种 OCR 引擎:
- Google Cloud Vision API
- Tesseract
- Azure Computer Vision

自动选择最佳引擎
```

#### 代码检测
```
检测代码特征:
- 关键字识别
- 语法结构
- 缩进模式
- 配对符号

自动识别语言:
- JavaScript
- Python
- Java
- CSS
- SQL
- 等等...
```

#### 结构识别
```
识别文档结构:
- 标题层级
- 列表(有序/无序)
- 表格
- 代码块
- 引用块
```

#### 内容理解
```
AI 分析:
- 主题识别
- 关键点提取
- 概念关联
- 摘要生成
```

## 高级功能

### 批量处理
```
/kb-from-image *.jpg --batch

处理所有匹配的图片:
- screenshot-1.jpg ✅
- screenshot-2.jpg ✅
- photo.jpg ✅

生成批量报告
```

### 代码优先模式
```
/kb-from-image code.png --detect-code

优先识别和提取代码:
- 检测代码块
- 保留语法高亮
- 提取注释
- 识别函数/类名
```

### 语言指定
```
/kb-from-image chinese-text.jpg --language=zh-CN

指定 OCR 语言以提高准确度
```

### 图片预处理
```
/kb-from-image dark-photo.jpg --enhance

自动增强:
- 调整亮度
- 提高对比度
- 去除噪点
- 锐化图像
```

### 多页文档
```
/kb-from-image page-*.jpg --merge

合并多页图片:
- page-01.jpg
- page-02.jpg
- page-03.jpg

→ 生成单个知识条目
```

## 生成的 Frontmatter

### 完整示例
```yaml
---
id: 2026-01-04-150001
title: "React 函数组件示例"
type: code-snippet
category: code
tags: [react, component, screenshot, code]

source:
  type: image
  file: "react-code.png"
  ocr_confidence: 0.95
  detected_language: "javascript"
  image_type: "code-screenshot"

  # 提取的信息
  code_language: "javascript"
  component_type: "functional"
  props: ["name", "email"]

  # 统计信息
  lines_of_code: 8
  complexity: "low"

created: 2026-01-04T15:00:00Z
modified: 2026-01-04T15:00:00Z
version: 1
links: []
backlinks: []
---

# React 函数组件示例

从截图提取的 React 函数组件代码：

\```javascript
function UserProfile({ name, email }) {
  return (
    <div>
      <h1>{name}</h1>
      <p>{email}</p>
    </div>
  );
}
\```

## 说明
这是一个简单的 React 函数组件示例...

![原图](knowledge/assets/2026-01-04-150001.png)
```

## 错误处理

### 图片格式不支持
```
❌ 错误: 不支持的图片格式
文件: document.pdf
支持格式: PNG, JPG, JPEG, GIF, BMP, WebP
建议: 转换为支持的格式
```

### OCR 识别失败
```
⚠️  警告: OCR 识别置信度低
文件: blurry-photo.jpg
置信度: 45%
建议: 图片质量较低，可能需要手动输入
```

### 无法识别文字
```
❌ 错误: 无法识别文字
文件: abstract-art.jpg
原因: 图片中没有清晰的文字
建议: 确认图片包含文字内容
```

### 文件过大
```
❌ 错误: 图片文件过大
文件: large-image.png
大小: 15 MB
限制: 10 MB
建议: 压缩图片后再导入
```

## 导入后处理

### 验证识别结果
```
检查:
- 文字是否正确
- 代码是否完整
- 格式是否保留
- 是否有遗漏
```

### 补充信息
```
添加:
- 来源说明
- 背景信息
- 个人理解
- 相关资源
```

### 编辑内容
```
/kb-edit id --field=content
修正识别错误
```

### 创建关联
```
/kb-link image-note related-concept --type=example-of
建立知识点关联
```

## 最佳实践

### 1. 保证图片质量
```
使用高质量图片:
- 分辨率足够高
- 文字清晰可见
- 光线均匀
- 避免模糊
```

### 2. 适当裁剪
```
裁剪掉无关内容:
- 移除空白区域
- 聚焦主要内容
- 减少干扰元素
```

### 3. 使用代码模式
```
代码截图使用:
/kb-from-image code.png --detect-code

更好的代码识别和格式化
```

### 4. 添加上下文
```
导入后补充:
- 什么时候拍的
- 在哪里拍的
- 为什么重要
- 相关背景
```

### 5. 组织图片
```
按主题组织:
- 同一主题的图片
- 创建合集
- 建立关联
```

## 应用场景

### 1. 代码片段保存
```
看到好的代码示例:
截图保存 → 导入知识库
自动提取代码并格式化
```

### 2. 会议记录
```
拍白板照片:
记录讨论内容 → 保存为知识条目
自动提取文字和结构
```

### 3. 学习笔记
```
纸质笔记数字化:
拍照 → OCR 识别 → 保存
自动整理结构
```

### 4. 书籍摘录
```
重要页面拍照:
保存 → 提取内容 → 建立读书笔记
自动识别章节和段落
```

### 5. 灵感捕捉
```
随时记录想法:
白板、便利贴、草稿纸
拍照保存 → 永久保留
```

## 与其他命令配合

### 导入后增强
```
/kb-from-image notes.jpg
@knowledge-enricher "整理和格式化笔记"
```

### 导入后总结
```
/kb-from-image whiteboard.jpg
@research-assistant "总结讨论要点"
```

### 导入后关联
```
/kb-from-image concept.jpg
@knowledge-manager "创建关联"
```

## 注意事项

### 1. 图片质量
- 高质量图片识别更准确
- 避免模糊和反光
- 确保文字清晰

### 2. 版权问题
- 尊重原图版权
- 仅个人学习使用
- 标注来源

### 3. 存储空间
- 图片占用空间较大
- 考虑压缩或删除原图
- 定期清理

### 4. 隐私保护
- 注意敏感信息
- 避免拍私人内容
- 本地存储

### 5. 识别准确度
- OCR 不是 100% 准确
- 需要人工检查
- 及时修正错误

## 扩展功能(未来)

### 1. 手写文字识别增强
```
更好的手写体识别
```

### 2. 表格识别
```
自动识别并提取表格数据
```

### 3. 公式识别
```
提取数学公式和 LaTeX 代码
```

### 4. 图表理解
```
理解图表含义并生成描述
```

### 5. 智能分类
```
自动识别图片类型并分类
```
