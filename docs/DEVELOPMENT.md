# 🛠️ 开发指南

> 贡献代码、添加新功能、扩展系统的完整指南

## 📑 目录

- [贡献指南](#贡献指南)
- [添加新命令](#添加新命令)
- [测试指南](#测试指南)
- [调试技巧](#调试技巧)
- [发布流程](#发布流程)

---

## 贡献指南

我们欢迎所有形式的贡献！

### 贡献方式

- 🐛 **报告Bug**: 发现问题请提Issue
- 💡 **功能建议**: 有好想法请告诉我们
- 📖 **改进文档**: 帮助完善文档
- 🔧 **代码修复**: 修复已知问题
- ✨ **新功能**: 添加新的功能特性

### 开发流程

#### 1. Fork并克隆仓库

```bash
git clone https://github.com/yourusername/my-know.git
cd my-know
```

#### 2. 创建功能分支

```bash
git checkout -b feature/your-feature-name
```

**分支命名规范**:
- `feature/xxx`: 新功能
- `fix/xxx`: Bug修复
- `docs/xxx`: 文档更新
- `refactor/xxx`: 代码重构

#### 3. 进行开发

```bash
# 编辑文件
vim .claude/commands/kb-new-command.md

# 测试功能
claude> /kb-new-command --test
```

#### 4. 提交更改

```bash
git add .
git commit -m "feat: add new command for X"
```

**提交信息规范**:
- `feat`: 新功能
- `fix`: Bug修复
- `docs`: 文档更新
- `style`: 代码格式
- `refactor`: 重构
- `test`: 测试
- `chore`: 构建/工具

#### 5. 推送并创建PR

```bash
git push origin feature/your-feature-name
# 在GitHub上创建Pull Request
```

**PR模板**:
```markdown
## 功能描述
简要描述这个PR做什么

## 变更类型
- [ ] 新功能
- [ ] Bug修复
- [ ] 文档更新
- [ ] 代码重构

## 测试
- [ ] 已测试功能
- [ ] 已更新文档

## 截图
如有UI变更，请提供截图
```

---

## 添加新命令

### 步骤1: 创建命令文件

```bash
# 创建新命令
vim .claude/commands/kb-mycommand.md
```

### 步骤2: 编写命令内容

```markdown
---
argument-hint: [--type=value] [--option]
description: 我的新命令
allowed-tools: Read, Write, Bash
---

# /kb-mycommand - 我的新命令

## 功能
这个命令做什么...

## 使用方式
### 基本用法
```
/kb-mycommand
```

## 参数说明
- `--type`: 参数描述

## 工作流程
1. 读取配置
2. 处理数据
3. 输出结果

## 示例
```
/kb-mycommand --type=example
```
```

### 步骤3: 测试命令

```bash
claude> /kb-mycommand --test
```

### 步骤4: 更新文档

在相关文档中添加新命令的说明：
- [COMMAND_REFERENCE.md](COMMAND_REFERENCE.md)
- [USER_GUIDE.md](USER_GUIDE.md)

---

## 测试指南

### 单元测试

```bash
# 测试每个命令
claude> /kb-add --test
claude> /kb-search --test
claude> /kb-edit --test

# 验证输出
# - 检查文件是否创建
# - 验证索引是否更新
# - 确认数据一致性
```

### 集成测试

```bash
# 测试完整工作流
claude> "记一条测试笔记"
claude> "搜索测试"
claude> "编辑第一条"
claude> "删除第一条"

# 验证:
# - 意图识别准确
# - 上下文正确
# - 数据一致
```

### 测试清单

- [ ] 命令功能正常
- [ ] 错误处理完善
- [ ] 索引更新正确
- [ ] 文件创建成功
- [ ] 文档已更新
- [ ] 向后兼容

---

## 调试技巧

### 启用调试模式

在 `config/user-preferences.json` 中添加：

```json
{
  "debug": {
    "enabled": true,
    "logLevel": "verbose",
    "logFile": ".claude/debug.log"
  }
}
```

**日志级别**:
- `error`: 只记录错误
- `warn`: 警告和错误
- `info`: 一般信息
- `debug`: 调试信息
- `verbose`: 详细信息

### 查看日志

```bash
# 查看最新日志
tail -f .claude/debug.log

# 搜索错误
grep "ERROR" .claude/debug.log

# 统计错误数量
grep -c "ERROR" .claude/debug.log
```

### 常见问题

**Q: 命令无法识别？**

A: 检查：
1. 文件名格式：`kb-xxx.md`
2. frontmatter格式是否正确
3. description字段是否存在

**Q: 索引未更新？**

A: 验证：
1. JSON文件格式是否正确
2. 文件权限是否正常
3. 检查日志中的错误信息

**Q: 工具调用失败？**

A: 确认：
1. `allowed-tools`字段包含所需工具
2. 工具参数格式正确
3. 文件路径是否存在

---

## 发布流程

### 版本号规范

遵循语义化版本 (Semantic Versioning):
- `MAJOR.MINOR.PATCH`
- MAJOR: 不兼容的API变更
- MINOR: 向后兼容的功能新增
- PATCH: 向后兼容的bug修复

### 发布清单

- [ ] 更新版本号
- [ ] 更新CHANGELOG.md
- [ ] 运行完整测试
- [ ] 更新文档
- [ ] 创建Git标签
- [ ] 发布Release

### 创建Release

```bash
# 1. 更新版本号
# 2. 提交更改
git add .
git commit -m "chore: release v1.0.0"

# 3. 创建标签
git tag -a v1.0.0 -m "Release v1.0.0"

# 4. 推送标签
git push origin v1.0.0

# 5. 在GitHub创建Release
```

---

## 📚 相关文档

- [系统架构](ARCHITECTURE.md) - 了解系统结构
- [命令参考](COMMAND_REFERENCE.md) - 现有命令列表
- [配置说明](CONFIGURATION.md) - 配置系统行为

---

**感谢您的贡献！** 🚀
