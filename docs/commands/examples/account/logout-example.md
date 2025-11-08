# `/logout` 命令示例

## 概述
`/logout` 命令使您从 Claude Code 中的当前 Anthropic 账户会话登出，清除认证 tokens 和会话数据。

## 何时使用
- 在共享/公共计算机上结束工作会话
- 切换到不同账户
- 排查认证问题
- 离开工作站时的安全最佳实践
- 卸载 Claude Code 前

## 示例用法

### 场景 1：基本登出

```
User: /logout

Claude Code: 您确定要登出吗？(y/n)
当前账户：user@example.com

User: y

Claude Code: 正在登出...

✓ 认证 token 已清除
✓ 会话数据已删除
✓ 对话历史已从内存清除

成功登出。

要再次使用 Claude Code，请运行：/login
```

### 场景 2：快速登出（无确认）

```
User: /logout --force

Claude Code: 已成功登出。
认证 token 已清除。
```

### 场景 3：共享计算机安全

```
User: 我在这台图书馆计算机上完成工作了

User: /logout

Claude Code: 正在从 work@company.com 登出

✓ 所有会话数据已清除
✓ 认证 tokens 已删除
✓ 对话历史已删除
✓ 缓存文件已清除

安全提示：关闭此终端窗口以确保完全清理。

User: [关闭终端]
```

## 清除的内容

### 会话数据
```
当您登出时，Claude Code 删除：

✓ 认证 tokens
✓ 活跃会话数据
✓ 对话历史（在内存中）
✓ 缓存的 API 响应
✓ 临时工作文件
```

### 保留的内容
```
以下内容保留在磁盘上：

✓ 配置文件（~/.config/claude/）
✓ CLAUDE.md 内存文件（项目特定）
✓ 本地代码更改
✓ Git commits
✓ 项目文件
✓ 自定义设置
```

## 登出场景

### 1. 工作会话结束

```
User: 我已完成认证功能的实现

User: 让我先 commit 这个
[进行 git commit]

User: /logout

Claude Code: 已从 work@company.com 登出

会话摘要：
- 持续时间：3 小时 24 分钟
- 执行命令：47
- 修改文件：12
- 使用 tokens: 45,230

再见！
```

### 2. 安全协议

```
公司安全政策：离开办公桌时登出

User: /logout

Claude Code: 公司账户（team@company.com）已登出。

安全检查清单：
✓ 认证已清除
✓ 会话已终止
✓ 本地 cache 已清理
✓ 网络连接已关闭

提醒：锁定您的计算机（Ctrl+Cmd+Q）
```

### 3. 认证问题排查

```
User: 我遇到认证错误

User: /logout

Claude Code: 正在清除认证状态...

已成功登出。

现在尝试：
1. /login（重新认证）
2. /doctor（诊断问题）

User: /login

Claude Code: [重新开始认证流程]
```

### 4. 账户切换前

```
User: 我需要切换到个人账户

User: /logout

Claude Code: 已从 work@company.com 登出

User: /login

Claude Code: [不同账户的登录流程]
```

## 带数据导出的登出

### 登出前保存

```
User: /export session-2025-01-08.md

Claude Code: 对话已导出到 session-2025-01-08.md

User: /logout

Claude Code: 已登出。
您导出的对话保存在：
/Users/dev/session-2025-01-08.md
```

### 完整会话归档

```
User: 登出前保存所有内容

Claude Code: 正在导出会话数据...

已保存：
- 对话：~/claude-sessions/2025-01-08-auth-feature.md
- Todos: todos-backup.json
- 修改文件列表：changes.txt

User: /logout

Claude Code: 所有数据已导出。可以安全登出。
已成功登出。
```

## 自动登出场景

### Token 过期

```
Claude Code: 警告：您的会话 token 已过期。

正在自动登出...

请运行 /login 重新认证。
```

### 强制登出（组织策略）

```
Claude Code: 触发组织安全策略。

原因：超过最大会话时长（8 小时）

正在自动登出...

✓ 已登出
✓ 会话数据已清除

请使用 /login 重新认证
```

### 网络断开

```
Claude Code: 无法验证认证 token。
网络连接丢失。

60 秒后自动登出...
如果连接恢复，按 Ctrl+C 取消。

[60 秒后]
由于长时间网络故障已登出。
```

## 安全最佳实践

### 1. 在共享系统上始终登出

```
公共计算机工作流：
1. /login（开始会话）
2. [进行工作]
3. /export（如需保存）
4. /logout（始终！）
5. 关闭终端
```

### 2. 自动登出配置

```
User: 可以设置不活动后自动登出吗？

User: /config

[在配置文件中]
security:
  auto_logout_minutes: 30
  require_confirmation: true
  clear_history_on_logout: true
```

### 3. 公司环境

```
公司政策合规：

User: /logout

Claude Code: 根据安全政策启动登出。

合规检查：
✓ 剪贴板中无敏感数据
✓ 所有 API 连接已关闭
✓ 本地 cache 已加密
✓ 审计日志已更新

登出完成。审计 ID: 20250108-1425
```

## 登出后验证

### 检查登出状态

```
User: [登出后] /status

Claude Code: 状态：未认证

要使用 Claude Code，请登录：
/login

未找到活跃会话。
```

### 验证 Token 删除

```
Terminal: cat ~/.config/claude/auth.json

输出：文件未找到（或空/null token）

这确认成功登出。
```

## 故障排除

### 登出失败

```
User: /logout

Claude Code: 错误：无法完成登出

活跃进程：
- 后台任务（bash_id: abc123）

选项：
1. 终止后台任务：/bashes --kill-all
2. 强制登出：/logout --force
3. 取消：Ctrl+C

User: /bashes --kill-all

User: /logout

Claude Code: 已成功登出。
```

### 登出后会话持续

```
User: /logout
[登出似乎成功]

User: [重新打开 Claude Code]

Claude Code: 欢迎回来，user@example.com

问题：Token 未正确清除

解决方案：
User: /doctor

Claude Code: 正在运行诊断...
发现问题：内存中的缓存会话

修复：重启终端
或：/logout --clear-cache --force
```

### 无法登出

```
User: /logout

Claude Code: 错误：登出被阻止

原因：对话中有未 commit 的更改

选项：
1. 导出对话：/export
2. 无论如何强制登出：/logout --force
3. 取消：Ctrl+C

User: /export conversation-backup.md

User: /logout

Claude Code: 已成功登出。
```

## 登出 vs 清除 vs 退出

### 对比

```
/logout
- 清除认证
- 删除会话数据
- 需要重新登录
- 安全导向

/clear
- 保持认证
- 仅清除对话
- 无需重新登录
- 工作流导向

/exit
- 关闭 Claude Code
- 会话可能持续
- 重启时自动登录
- 便利导向
```

### 何时使用各个命令

```
使用 /logout 当：
- 共享计算机
- 切换账户
- 安全要求
- 工作日结束（公司）

使用 /clear 当：
- 开始新任务
- 减少 context
- 同一账户，重新开始

使用 /exit 当：
- 完成 Claude Code
- 保持同一账户
- 很快会返回
```

## 推荐工作流

### 每日工作会话

```
早上：
User: /login
[全天工作]

每日结束：
User: /export daily-summary.md
User: /logout
```

### 快速会话

```
User: /login
[快速任务 - 10 分钟]
User: /logout
```

### 共享环境

```
始终：
1. /login（开始）
2. [工作]
3. /logout（结束）
4. 关闭终端
5. 锁定计算机
```

## 相关命令

- `/login` - 使用 Anthropic 账户认证
- `/status` - 检查认证状态
- `/exit` - 关闭 Claude Code（可能保持会话）
- `/export` - 登出前保存对话
- `/privacy-settings` - 控制数据保留

## 提示

- 登出前使用 `/export` 保存重要对话
- 在共享或公共计算机上始终 `/logout`
- 配置自动登出以确保安全（在 `/config` 中）
- `/logout` 不会删除本地项目文件
- 不使用 `/logout` 关闭终端可能保持会话活跃
- 使用 `/logout --force` 跳过确认提示

## 常见问题

**问：登出会删除我的代码更改吗？**
答：不会，仅清除认证和会话数据。您的代码保持不变。

**问：可以登出而不丢失对话吗？**
答：在 `/logout` 前使用 `/export` 保存对话历史。

**问：/logout 和 /exit 有什么区别？**
答：`/logout` 清除认证；`/exit` 只是关闭 Claude Code 但可能保持会话。

**问：我每次都需要登出吗？**
答：仅在安全需要时（共享计算机）或切换账户时。否则，会话会持续。

**问：如何验证我已登出？**
答：运行 `/status` - 如果登出成功，它将显示"未认证"。
