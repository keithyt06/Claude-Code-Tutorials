# `/rewind` 命令示例

## 概述
`/rewind` 命令允许您返回到对话或代码状态的先前点，使您能够撤销更改或探索替代方法。

## 何时使用
- 当您想撤销最近的代码更改时
- 当您想尝试不同的方法时
- 当最近的更改引入 bug 时
- 当您想返回到先前的讨论点时

## 示例用法

### 场景：回退代码更改

```
User: Add error handling to all database operations

Claude Code: [对 5 个文件进行更改]

User: Actually, this is too aggressive. Let me rewind and try a lighter approach.

User: /rewind

[出现交互式选择]
Claude Code: Select a point to rewind to:
1. Before adding error handling (2 minutes ago)
2. After initial database setup (10 minutes ago)
3. Start of conversation (15 minutes ago)

User: 1

Claude Code: Rewound to before adding error handling. Your files have been restored.

User: Instead, just add error handling to the user authentication queries.
```

### 场景：探索替代解决方案

```
User: Implement caching using Redis

Claude Code: [实现 Redis 缓存]

User: /rewind

[返回到 Redis 实现之前]

User: Actually, let's use in-memory caching instead for simplicity.

Claude Code: [实现 in-memory 缓存作为替代方案]
```

## Rewind 的工作原理

### 被回退的内容
- **对话状态**：返回到选定的消息
- **文件更改**：回退回退点之后所做的代码修改
- **任务状态**：将 todo 列表恢复到先前状态

### 保持不变的内容
- 配置设置
- Model 选择
- 工作目录
- CLAUDE.md memory

## 交互式 Rewind 过程

```
1. 用户执行 /rewind
2. Claude Code 呈现检查点选项
3. 用户选择回退点
4. 系统回退更改
5. 对话从该点继续
```

## 最佳实践

### 创建自然的检查点
- 在开始另一个更改之前完成一个逻辑更改
- 使用描述性消息使回退点清晰
- 考虑在主要重构之前进行回退

### 何时不回退
- 如果您只需要撤销一个小更改（只需要求 Claude 撤销它）
- 如果您想保留某些更改但不保留其他更改（明确说明要更改什么）
- 如果您已将更改推送到版本控制（请使用 git revert）

## 示例：复杂的重构决策

```
User: Refactor the payment processing module to use a strategy pattern

Claude Code: [跨多个文件实现策略模式]

User: Hmm, this seems over-engineered for our use case. /rewind

[回退到重构之前]

User: Let's just extract the common logic into helper functions instead.

Claude Code: [使用辅助函数进行更简单的重构]

User: Much better!
```

## Rewind 与其他命令的对比

| 命令 | 目的 | 影响 |
|---------|---------|--------|
| `/rewind` | 回到过去 | 回退代码和对话 |
| `/clear` | 重新开始 | 删除所有历史 |
| `git revert` | 撤销 commit | 仅影响版本控制 |
| Manual edit | 修复特定问题 | 精确更改 |

## 提示
- Rewind 是非破坏性的 - 您始终可以再次向前移动
- 如果您想保存当前状态，请在回退之前使用 `/export`
- Rewind 非常适合尝试不同的方法
- 非常适合"假设"场景，而不会丢失工作

## 相关命令
- `/clear` - 清除整个对话
- `/export` - 在回退之前保存当前状态
- `/todos` - 检查哪些任务将受到回退的影响
