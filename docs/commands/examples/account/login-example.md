# `/login` 命令示例

## 概述
`/login` 命令允许您在使用 Claude Code 时在不同的 Anthropic 账户之间切换。

## 何时使用
- 在个人和工作账户之间切换
- 使用不同的订阅套餐
- 访问团队特定配置
- 排查认证问题

## 示例用法

### 场景 1：切换账户

```
User: /login

Claude Code: 正在启动登录流程...

正在打开浏览器进行认证...
请使用您的 Anthropic 账户登录。

[浏览器打开 Anthropic 登录页面]

User: [在浏览器中完成登录]

Claude Code: 已成功登录为 user@example.com

账户详情：
- 邮箱：user@example.com
- 套餐：Professional
- 组织：Acme Corp

User: 太好了！现在我可以访问我的工作项目了。
```

### 场景 2：多账户管理

```
当前账户：personal@email.com（免费套餐）

User: 我需要切换到工作账户用于这个项目

User: /login

Claude Code: 当前会话将登出。
继续登录？(y/n)

User: y

Claude Code: 正在打开认证页面...

[成功登录后]

Claude Code: 已成功切换到 work@company.com

套餐：Team
组织：TechCorp
可用功能：
- 扩展 context 窗口
- 优先支持
- 团队协作工具
```

### 场景 3：重新认证

```
User: /status

Claude Code: 状态：认证 token 已过期

User: /login

Claude Code: 正在重新认证会话...

[浏览器打开]

Claude Code: 认证已成功刷新。
会话已恢复。
```

## 认证流程

### 分步流程

1. **启动登录**
   ```
   User: /login
   ```

2. **浏览器认证**
   ```
   Claude Code: 正在打开浏览器：
   https://claude.ai/login

   等待认证...
   ```

3. **收到 Token**
   ```
   Claude Code: 认证成功！
   Token 已收到并安全存储。
   ```

4. **账户验证**
   ```
   Claude Code: 正在验证账户详情...

   ✓ 账户已验证
   ✓ 订阅活跃
   ✓ 权限已加载
   ```

## 账户切换场景

### 个人到工作账户

```
User: /login

Claude Code: 当前：personal@email.com
正在登出并重新认证...

[完成工作账户登录]

Claude Code: 已切换到 work@company.com

配置更改：
- 工作目录：~/work-projects
- 团队设置已加载
- 共享内存文件可用
```

### 工作到个人账户

```
User: /login

Claude Code: 正在从 work@company.com 切换到个人账户

[认证完成]

Claude Code: 现在使用 personal@email.com

注意：团队特定设置不再可用。
您想加载个人配置吗？
```

## 会话管理

### 检查当前账户

```
User: 我正在使用哪个账户？

Claude Code: 当前账户：user@example.com
套餐：Professional
登录时间：2025-01-08 09:00 AM
```

### 会话持久性

```
User: 我每次都需要登录吗？

Claude Code: 不需要，您的会话会持续到：
- 您明确登出（/logout）
- Token 过期（30 天）
- 您切换账户（/login）

当前会话过期：2025-02-07
```

## 故障排除

### 浏览器未打开

```
User: /login

Claude Code: 错误：无法打开默认浏览器

手动登录 URL：
https://claude.ai/auth?token=abc123...

请在浏览器中打开此 URL 以完成登录。
```

### 认证失败

```
User: /login

Claude Code: 认证失败。

常见问题：
1. 浏览器阻止了认证
2. 网络连接问题
3. 凭据无效

尝试：
- 检查互联网连接
- 临时禁用 VPN
- 清除浏览器 cookies
- 使用 /doctor 诊断问题
```

### Token 过期

```
User: 帮我处理这段代码

Claude Code: 错误：认证 token 已过期

User: /login

Claude Code: 正在重新认证...
[自动 token 刷新]
会话已恢复。我能帮您什么？
```

### 未找到账户

```
User: /login

[认证后]

Claude Code: 错误：此账户未找到活跃订阅

访问 https://claude.ai/subscribe 激活套餐。
```

## 安全考虑

### Token 存储

```
Claude Code 安全存储认证 tokens：
- macOS: Keychain
- Linux: Secret Service API / 加密文件
- Windows: Credential Manager

Tokens 永远不以明文存储。
```

### 账户隔离

```
每个账户维护单独的：
- 对话历史
- 配置设置
- 工作目录
- 权限

切换账户不会暴露之前的会话数据。
```

### 登出提醒

```
User: 我在共享计算机上完成工作了

User: /logout

Claude Code: 已成功登出。
所有本地会话数据已清除。

建议：关闭终端以完全清理。
```

## 多账户工作流

### 每日工作流示例

```
早上（个人项目）：
User: /login
[使用 personal@email.com 登录]
User: 处理我的副项目

下午（工作）：
User: /login
[使用 work@company.com 登录]
User: 为客户实现功能

晚上（个人）：
User: /login
[切换回 personal@email.com]
```

### 项目特定账户

```
~/personal-projects/
User: /login
[使用个人账户]

~/work/client-project/
User: /login
[使用具有客户访问权限的工作账户]

~/opensource/contribution/
User: /login
[使用公共账户]
```

## 相关命令

- `/logout` - 从当前账户登出
- `/status` - 检查当前账户和认证状态
- `/privacy-settings` - 管理数据共享偏好
- `/config` - 查看账户特定配置

## 最佳实践

### 1. 定期认证
```
定期检查 token 状态：
/status

过期前重新认证：
/login
```

### 2. 安全共享计算机
```
在共享机器上始终登出：
/logout

在共享计算机上永远不要在浏览器中保存密码。
```

### 3. 分离工作和个人
```
使用不同账户：
- 个人项目（个人邮箱）
- 工作项目（公司邮箱）
- 开源（公共邮箱）
```

### 4. 团队协作
```
使用组织账户：
- 共享项目
- 团队资源
- 协作开发
```

## 提示

- 使用描述性电子邮件地址保持多个账户有序
- 检查 `/status` 验证哪个账户活跃
- 在共享计算机上使用 `/logout` 以确保安全
- 如果您的组织支持，设置 SSO
- Token 过期警告在过期前 7 天出现

## 常见问题

**问：可以同时使用多个账户吗？**
答：不可以，每个 Claude Code 会话只能激活一个账户。使用 `/login` 切换。

**问：切换账户会丢失我的对话吗？**
答：是的，对话是账户特定的。切换前使用 `/export` 保存。

**问：会话能持续多久？**
答：会话通常持续 30 天后需要重新认证。

**问：我的 token 存储安全吗？**
答：是的，tokens 使用操作系统级安全存储（Keychain/Credential Manager）。
