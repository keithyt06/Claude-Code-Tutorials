# `/pr_comments` 命令示例

## 概述
`/pr_comments` 命令显示并允许与来自 GitHub 和其他版本控制平台的 pull request 评论进行交互。

## 何时使用
- 审查 PR 反馈
- 处理审查者评论
- 实现请求的更改
- 理解审查 context
- 响应代码审查讨论

## 示例用法

### 查看 PR 评论

```
User: /pr_comments

Claude Code: 正在获取 PR 评论...

## Pull Request #234：添加用户认证
**状态：** 开放 | **评论：** 8 | **批准：** 1/2

### 审查评论

**@sarah_dev** (src/auth/jwt.ts:45)
💬 考虑添加速率限制以防止暴力攻击

**@john_lead** (src/auth/jwt.ts:67)
⚠️ Token 过期时间应通过环境变量配置

**@sarah_dev** (tests/auth.test.ts:23)
✅ 很好的测试覆盖率！

**@security_bot**
🔴 发现潜在安全问题：硬编码的 JWT secret

**@john_lead**（一般）
📝 请使用认证设置说明更新 README
```

## 与评论交互

### 处理评论

```
User: /pr_comments

Claude Code: 显示 4 条未解决的评论

User: 处理所有安全评论

Claude Code: 我将修复安全问题：

1. **硬编码的 JWT secret**
   - 将 secret 移至环境变量
   - 更新了 src/auth/jwt.ts:67
   - 添加了 JWT_SECRET 到 .env.example

2. **速率限制**
   - 添加了 express-rate-limit middleware
   - 为认证 endpoints 配置
   - 添加了测试

所做更改：
✅ src/auth/jwt.ts（从 env 获取 JWT_SECRET）
✅ src/middleware/rateLimit.ts（新）
✅ src/api/auth.ts（应用了速率限制）
✅ .env.example（添加了 JWT_SECRET）
✅ tests/auth.test.ts（速率限制测试）

准备好 push 并响应审查者。
```

### 响应特定评论

```
User: /pr_comments

User: 响应 sarah_dev 的速率限制评论

Claude Code: 我将实现速率限制并回复：

[实现更改]

准备的回复：
---
@sarah_dev 好发现！我已添加速率限制：
- 登录尝试每分钟 5 个请求
- Token 刷新每分钟 10 个请求
- 通过环境变量可配置

查看 commits: abc123f, def456g
---

发布此回复？(yes/no)

User: yes

Claude Code: 已发布回复到 PR 评论。
```

## PR 评论工作流

### 完整审查周期

```
User: /pr_comments

Claude Code: PR #234 有新评论 (4)

User: 显示所有行动项

Claude Code: PR 审查的行动项：

🔴 必须修复 (2)：
1. 安全：将 JWT secret 移至 env var
2. Bug：token 刷新中的竞争条件

🟡 应该修复 (3)：
3. 为过期 tokens 添加错误处理
4. 提高测试覆盖率（当前 78%）
5. 将常量提取到配置文件

💚 最好有 (1)：
6. 为公共 API 添加 JSDoc 注释

User: 修复所有"必须修复"项

Claude Code: 正在修复关键项...

1. ✅ 将 JWT secret 移至环境变量
2. ✅ 使用互斥锁修复竞争条件

准备好重新审查。
```

### 增量更新

```
User: /pr_comments

[显示 8 条评论]

User: 先修复来自 john_lead 的项目

Claude Code: John 的评论：

1. 使 token 过期时间可配置
2. 添加 README 文档
3. 将魔法数字提取到常量

实现中：

1. Token 过期：
```typescript
const TOKEN_EXPIRATION = process.env.JWT_EXPIRATION || '15m';
```

2. README 已更新，包含：
   - 设置说明
   - 环境变量
   - 使用示例

3. 提取的常量：
```typescript
const MAX_LOGIN_ATTEMPTS = 5;
const RATE_LIMIT_WINDOW = 60 * 1000; // 1 分钟
```

John 的所有评论已处理。您想要：
1. Push 更改
2. 将评论标记为已解决
3. 请求重新审查
```

## 高级功能

### 评论线程

```
User: /pr_comments --thread

Claude Code: PR #234 - 线程评论

📍 src/auth/jwt.ts:45-52（3 条评论）
  @sarah_dev: 考虑添加速率限制
  └─ @you: 好主意，将实现
      └─ @sarah_dev: 也检查常见密码
          └─ (未解决)

📍 src/auth/jwt.ts:67（2 条评论）
  @john_lead: Token 过期应该可配置
  └─ @you: 同意，使其基于环境
      └─ (已解决 ✓)

📍 tests/auth.test.ts:23（1 条评论）
  @sarah_dev: 很好的测试覆盖率！
  └─ (不需要操作)
```

### 过滤评论

```
User: /pr_comments --filter unresolved

Claude Code: 仅显示未解决的评论 (3)：

1. @sarah_dev: 添加常见密码检查
2. @security_bot: 验证密码复杂性
3. @john_lead: 更新文档

User: /pr_comments --filter "security"

Claude Code: 安全相关评论 (4)：

[仅显示安全评论]
```

### 评论统计

```
User: /pr_comments --stats

Claude Code: PR #234 统计

评论：12 条总计
├─ 已解决：7
├─ 未解决：5
└─ 待处理：0

按审查者：
├─ @sarah_dev: 5 条评论
├─ @john_lead: 4 条评论
├─ @security_bot: 2 条评论
└─ @ci_bot: 1 条评论

按类型：
├─ 安全：3
├─ Bug: 2
├─ 样式：4
└─ 文档：3

按优先级：
├─ 严重：2
├─ 重要：3
└─ 次要：7
```

## 实际示例

### 示例 1：安全审查

```
User: /pr_comments

Claude Code: 来自 @security_team 的安全审查：

❌ 严重问题 (2)：
1. SQL 注入漏洞（第 234 行）
2. 用户输入渲染中的 XSS 风险（第 456 行）

⚠️ 警告 (3)：
3. 缺少输入验证
4. 弱密码要求
5. 无速率限制

User: 立即修复所有严重问题

Claude Code: 修复严重安全问题：

1. SQL 注入（第 234 行）：
```typescript
// 之前
db.query(`SELECT * FROM users WHERE id = ${userId}`);

// 之后
db.query('SELECT * FROM users WHERE id = ?', [userId]);
```

2. XSS 风险（第 456 行）：
```tsx
// 之前
<div dangerouslySetInnerHTML={{__html: userInput}} />

// 之后
<div>{sanitize(userInput)}</div>
```

所有严重问题已修复。准备好重新请求安全审查。
```

### 示例 2：代码质量审查

```
User: /pr_comments

@tech_lead 评论：

1. "此函数太复杂（复杂度：25）"
   → 行：src/services/payment.ts:145

2. "考虑将此逻辑提取到单独的函数中"
   → 行：src/services/payment.ts:200-350

3. "API 调用缺少错误处理"
   → 行：src/api/client.ts:89

User: 根据这些评论进行重构

Claude Code: 重构以处理反馈：

1. 降低复杂度：
   - 将 processPayment 拆分为 4 个较小的函数
   - 复杂度：25 → 8

2. 提取逻辑：
   - 创建了 validatePaymentData()
   - 创建了 processTransaction()
   - 创建了 sendConfirmation()

3. 添加错误处理：
   - 所有 API 调用的 Try-catch 块
   - 适当的错误消息
   - 瞬态失败的重试逻辑

更新的文件：
✅ src/services/payment.ts（已重构）
✅ src/services/payment/validator.ts（新）
✅ src/services/payment/processor.ts（新）
✅ src/api/client.ts（错误处理）
```

### 示例 3：设计讨论

```
User: /pr_comments

@architect: "我对这里的方法有顾虑。让我们讨论设计。"

线程（5 条消息）：
1. @architect: 当前设计耦合了支付和通知
2. @you: 同意，但对于即时 MVP 需要
3. @architect: 考虑改用事件驱动方法
4. @architect: 这也会使测试更容易
5. [需要您的响应]

User: 按建议实现事件驱动方法

Claude Code: 重构为事件驱动架构：

之前：直接耦合
```typescript
function processPayment(payment) {
  // 处理支付
  sendNotification(payment); // 耦合！
}
```

之后：事件驱动
```typescript
function processPayment(payment) {
  // 处理支付
  eventBus.emit('payment.processed', payment);
}

// 单独的通知处理器
eventBus.on('payment.processed', (payment) => {
  sendNotification(payment);
});
```

好处：
- 解耦组件
- 更容易测试
- 灵活的通知策略
- 可以轻松添加更多监听器

响应线程：
"很好的建议！实现了事件驱动方法。这使得
代码更易于维护和测试。如果这解决了您的
顾虑，请告诉我。"

发布响应？(yes/no)
```

## 与 Git 集成

### 更改时自动获取

```
User: git push

Claude Code: 已 push 更改到 PR #234

[自动检查新评论]

检测到新评论 (2)：
1. @reviewer: "看起来不错，一个小事情..."
2. @ci_bot: "测试通过 ✅"

User: /pr_comments

[显示最新评论]
```

### 从评论生成 Commit 消息

```
User: /pr_comments

User: 生成处理这些评论的 commit 消息

Claude Code: 建议的 commit 消息：

---
fix: 处理 PR 审查反馈

- 将 JWT secret 移至环境变量
- 为认证 endpoints 添加速率限制
- 将常量提取到配置文件
- 使用设置说明更新 README

处理 PR #234 中来自 @sarah_dev 和 @john_lead 的评论

Co-authored-by: Claude <noreply@anthropic.com>
---

使用此消息？(yes/no)
```

## 评论通知

### 实时更新

```
[Claude Code 正在运行]

🔔 来自 @tech_lead 对 PR #234 的新 PR 评论
"整体实现看起来不错，但是..."

User: /pr_comments

[在 context 中显示最新评论]
```

## 最佳实践

### 1. 定期检查

```
全天：
User: /pr_comments

检查新反馈并及时处理
```

### 2. 优先处理关键评论

```
User: /pr_comments --priority critical

首先处理阻塞问题
```

### 3. 分组相关更改

```
修复一个文件的所有评论：
User: /pr_comments --file src/auth/jwt.ts

一起处理以获得更清晰的 commits
```

### 4. 保持沟通

```
修复后：
User: 回复评论解释更改

让审查者了解情况
```

## 提示
- 开始新工作前检查评论
- 立即处理严重/阻塞问题
- 在单个 commit 中分组相关修复
- 让审查者了解进度
- 需要时提出澄清问题
- 使用评论提高代码质量
- 从审查反馈中学习

## 相关命令
- `/review` - push 前自我审查
- `/export` - 导出 PR 讨论
- `/todos` - 跟踪评论行动项
- 通过 Bash 工具使用 `gh pr` 命令
