# `/export` 命令示例

## 概述
`/export` 命令将您的对话历史保存到文件或剪贴板，用于文档、分享或审查目的。

## 何时使用
- 记录问题解决会话
- 与团队成员分享解决方案
- 从对话创建教程
- 归档重要决策
- 生成进度报告

## 示例用法

### 基本导出

```
User: /export

Claude Code: 导出选项：
1. 保存到文件
2. 复制到剪贴板
3. 导出为 markdown
4. 导出为 JSON

User: 1

Claude Code: 文件名？(默认：conversation-2025-01-08.md)

User: [Enter]

Claude Code: 已导出对话到 conversation-2025-01-08.md
位置：/Users/dev/myproject/conversation-2025-01-08.md
```

### 使用自定义文件名导出

```
User: /export auth-implementation-session.md

Claude Code: 已导出对话到 auth-implementation-session.md
包括：
- 47 条消息
- 12 次代码更改
- 3 个修改的文件
- 已完成的 todos
```

## 导出格式

### Markdown 格式（默认）

```
User: /export session.md

# Claude Code 会话
日期：2025-01-08
持续时间：45 分钟

## 总结
使用 JWT tokens 实现用户认证

## 对话

### User
我需要实现 JWT 认证

### Claude Code
我将帮助实现 JWT 认证。让我分解一下：
1. 安装依赖
2. 创建认证 middleware
3. 实现登录/登出
4. 添加 token 刷新

[完整对话继续...]

## 代码更改

### src/auth/jwt.ts（新文件）
```typescript
[代码内容]
```

## 已完成的 Todos
✅ 安装 jsonwebtoken 包
✅ 创建 JWT 签名函数
✅ 实现认证 middleware
✅ 添加登录 endpoint
✅ 添加登出 endpoint
✅ 实现 token 刷新
✅ 编写测试

## 修改的文件
- src/auth/jwt.ts（已创建）
- src/middleware/auth.ts（已修改）
- src/api/auth.ts（已修改）
- tests/auth.test.ts（已创建）
```

### JSON 格式

```
User: /export session.json

{
  "date": "2025-01-08T10:30:00Z",
  "duration_minutes": 45,
  "messages": [
    {
      "role": "user",
      "content": "我需要实现 JWT 认证",
      "timestamp": "2025-01-08T10:30:00Z"
    },
    {
      "role": "assistant",
      "content": "我将帮助实现 JWT 认证...",
      "timestamp": "2025-01-08T10:30:15Z"
    }
  ],
  "files_modified": [
    {
      "path": "src/auth/jwt.ts",
      "action": "created",
      "lines_added": 87
    }
  ],
  "todos": {
    "completed": 7,
    "pending": 0
  }
}
```

### 纯文本格式

```
User: /export session.txt

Claude Code 会话 - 2025-01-08
================================

实现了 JWT 认证

USER：我需要实现 JWT 认证

CLAUDE：我将帮助实现 JWT 认证...

[对话以纯文本继续...]
```

## 导出选项

### 导出特定部分

```
User: /export --only-code code-changes.md

Claude Code: 仅导出代码更改到 code-changes.md

包含：
- 4 个修改的文件
- 完整文件内容
- 更改摘要
```

### 不导出代码

```
User: /export --no-code discussion.md

Claude Code: 已导出对话（不包含代码）到 discussion.md

包括：
- 消息交换
- 所做决策
- Todo 列表
- 排除：代码片段和文件内容
```

### 仅导出摘要

```
User: /export --summary-only summary.md

# 会话摘要

**日期：** 2025-01-08
**主题：** JWT 认证实现
**持续时间：** 45 分钟
**更改文件：** 4
**添加行数：** 247
**删除行数：** 12

## 成就
- 实现了 JWT token 生成
- 创建了认证 middleware
- 添加了登录/登出 endpoints
- 实现了 token 刷新
- 添加了全面的测试（95% 覆盖率）

## 关键决策
- 使用 HS256 算法用于 JWT
- 15 分钟访问 token 生命周期
- 7 天刷新 token 生命周期
- Tokens 存储在 httpOnly cookies
```

## 实际示例

### 示例 1：文档

```
User: 我们刚刚实现了一个复杂功能。让我导出这个用于文档。

User: /export feature-auth-implementation.md

Claude Code: 已导出到 feature-auth-implementation.md

[稍后，用作文档：]

# 用户认证功能
[从 Claude Code 会话自动生成]

## 实现步骤
[从对话中捕获]

## 代码
[包含所有代码更改]

## 测试
[讨论的测试用例]
```

### 示例 2：团队分享

```
User: /export --format team

Claude Code: 优化用于团队分享的导出

# 团队更新：认证实现

## 已构建内容
- 基于 JWT 的认证
- 登录/登出 endpoints
- Token 刷新机制
- 认证 middleware

## 更改的文件
- src/auth/（新）
- src/middleware/auth.ts
- tests/auth.test.ts

## 如何使用
[对话中的使用示例]

## 下一步
[待处理的 todos]

准备通过电子邮件、Slack 或 PR 描述分享！
```

### 示例 3：进度报告

```
User: /export --format report progress-report.md

# 进度报告
**周：** 2025 年 1 月 8-12 日
**开发者：** [User]
**AI 伙伴：** Claude Code

## 本周完成

### 认证系统（8 小时）
- 实现了 JWT 认证
- 添加了 OAuth 集成
- 创建了用户会话管理
- 全面的测试覆盖

### Bug 修复（3 小时）
- 修复了 UserList 中的内存泄漏
- 解决了 SQL 注入漏洞
- 纠正了日期格式问题

### 代码质量（2 小时）
- 重构了支付模块
- 改进了错误处理
- 添加了 TypeScript strict mode

## 指标
- 创建文件：12
- 修改文件：28
- 添加行数：1,847
- 删除行数：432
- 测试覆盖率：78% → 92%
- 修复 Bugs：8

[本周所有会话的详细信息]
```

## 导出过滤

### 日期范围

```
User: /export --date-range "2025-01-08" session.md

Claude Code: 仅导出 2025 年 1 月 8 日的消息
```

### 按主题

```
User: /export --filter "authentication" auth-only.md

Claude Code: 仅导出与认证相关的消息
已排除 23 条不相关消息
已包含 18 条相关消息
```

### 按文件

```
User: /export --files "src/auth/*" auth-changes.md

Claude Code: 仅导出 src/auth/ 中文件的更改
```

## 导出模板

### 自定义模板

```
.claude/export-templates/bug-fix.md:

# Bug 修复报告

## Bug 描述
{{first_user_message}}

## 根本原因
{{analysis}}

## 解决方案
{{code_changes}}

## 测试
{{test_results}}

## 预防
{{recommendations}}
```

用法：
```
User: /export --template bug-fix bug-report.md

Claude Code: 使用 bug-fix 模板...
已导出到 bug-report.md
```

## 剪贴板导出

### 到剪贴板

```
User: /export --clipboard

Claude Code: 对话已复制到剪贴板！
准备粘贴到：
- 电子邮件
- Slack
- GitHub issue
- 文档
```

### 分享链接

```
User: /export --share-link

Claude Code: 已创建可分享链接：
https://claude.ai/share/abc123xyz

链接过期时间：7 天
密码保护：是
```

## 自动导出

### 会话结束时自动导出

```
.claude/config.json:
{
  "export": {
    "onExit": true,
    "format": "markdown",
    "location": "./sessions/"
  }
}
```

### 导出 Hooks

```
.claude/hooks/post-session.sh:
#!/bin/bash
# 自动导出并 commit 到 repo
claude export "sessions/$(date +%Y-%m-%d).md"
git add sessions/
git commit -m "Session: $(date +%Y-%m-%d)"
```

## 导出分析

### 带统计信息

```
User: /export --with-stats session-stats.md

# 会话统计

## 概览
- 持续时间：45 分钟
- 消息数：47
- 用户消息：24
- Claude 消息：23

## 代码更改
- 创建文件：3
- 修改文件：4
- 删除文件：0
- 添加行数：387
- 删除行数：45

## 生产力指标
- 完成 Todos：12
- 修复 Bugs：3
- 添加测试：8
- 覆盖率提升：+15%

## 使用的命令
- Bash: 15 次
- Read: 23 次
- Edit: 18 次
- Write: 3 次

[完整对话如下...]
```

## 导出最佳实践

### 1. 导出重要会话

```
完成主要功能后：
User: /export feature-name-DATE.md

解决困难 bugs 后：
User: /export bug-fix-DATE.md
```

### 2. 定期备份

```
每日或每周：
User: /export backup/session-$(date +%Y-%m-%d).md
```

### 3. 团队沟通

```
在 PR 或站会前：
User: /export --summary-only update.md
```

### 4. 学习存档

```
学习新概念时：
User: /export learning/how-to-X.md
```

## 提示
- `/clear` 前导出以保留历史
- 使用带日期的描述性文件名
- 在导出中包含代码以获得完整 context
- 导出摘要以便快速分享
- 归档重要会话
- 使用 JSON 格式进行程序化处理
- 模板可以节省重复导出的时间

## 相关命令
- `/clear` - 清除对话（先导出！）
- `/compact` - 减少对话大小
- `/rewind` - 回到之前的时间点
- `/todos` - 查看导出中包含的 todos
