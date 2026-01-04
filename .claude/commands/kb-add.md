---
argument-hint: [--type=code-snippet|project-doc|learning-note|research-note] [--category=code|projects|learning|personal] [--tags=tag1,tag2] [--template=template-name]
description: 添加知识条目到知识库
allowed-tools: Read, Write, Bash, Glob
---

# /kb-add - 添加知识条目

## 功能
快速添加新的知识条目到个人知识库。

## 使用方式

### 基本用法
```
/kb-add
```
系统会提示你输入标题和内容。

### 指定参数
```
/kb-add --type=learning-note --category=learning --tags=react,hooks
```

### 使用模板
```
/kb-add --template=code-snippet
```

## 参数说明
- `--type`: 知识类型 (code-snippet, project-doc, learning-note, research-note)
- `--category`: 分类 (code, projects, learning, personal)
- `--tags`: 标签列表,用逗号分隔
- `--template`: 使用的模板名称

## 工作流程

1. **收集信息**:
   - 提示用户输入标题
   - 提示用户输入内容
   - 可以选择指定类型、分类、标签

2. **生成 ID**:
   - 使用当前时间戳生成唯一 ID
   - 格式: YYYY-MM-DD-HHMMSS

3. **确定路径**:
   - 根据当前日期确定存储路径
   - 格式: knowledge/items/YYYY/MM-Month/YYYY-MM-DD-HHMMSS.md

4. **创建文件**:
   - 使用指定的模板或默认模板
   - 填充 YAML frontmatter
   - 写入用户输入的内容

5. **更新索引**:
   - 读取 knowledge/index.json
   - 添加新条目的元数据
   - 更新统计数据

## 示例

### 添加学习笔记
```
/kb-add --type=learning-note --tags=react,useState

请输入标题: React useState Hook 详解
请输入内容: useState 是 React 提供的 Hook...
```

### 添加代码片段
```
/kb-add --template=code-snippet

请输入标题: React Hooks 使用示例
请输入代码: ```javascript
const [count, setCount] = useState(0);
```
```

## 注意事项
- 如果不指定类型,默认使用 "default"
- 如果不指定分类,默认使用 "personal"
- 标签会自动去重
- 标题不能为空
