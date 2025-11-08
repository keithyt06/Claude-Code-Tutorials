# `/compact` 命令示例

## 概述
`/compact` 命令通过总结对话历史来减少 token 使用，同时保留重要的上下文。您可以选择性地提供指令来指导应保留的内容。

## 何时使用
- 当对话变长并消耗太多 token 时
- 当您想继续当前任务但减少上下文大小时
- 在同一项目内开始新的工作阶段之前

## 示例用法

### 基本压缩

```
User: /compact

Claude Code: I've compacted the conversation, summarizing earlier discussions while preserving key context. We can continue from here.
```

### 带特定指令的压缩

```
User: /compact Keep all code examples and error messages

Claude Code: I've compacted the conversation while preserving all code examples and error messages as requested.
```

### 真实场景

```
User: Help me refactor this user authentication module
[讨论不同方法的 15 条消息]

User: Let's implement the JWT approach
[包含代码实现的 10 条消息]

User: /compact Focus on the JWT implementation decisions and final code

Claude Code: Compacted. I've preserved:
- Your decision to use JWT authentication
- The final implementation in auth.ts
- Key security considerations we discussed
- The token refresh strategy

User: Great! Now let's add rate limiting to these endpoints.
[对话以减少的 token 使用继续]
```

## 压缩策略

### 保留什么
```
/compact Keep all function signatures and API contracts
/compact Preserve error messages and debugging steps
/compact Focus on the final implementation and test results
```

### 总结什么
- 导致死胡同的探索性讨论
- 被替换的多次代码迭代
- 一般背景信息

## 优势
- **降低成本**：更低的 token 使用意味着更低的成本
- **保持上下文**：重要信息得以保留
- **提高性能**：更短的上下文意味着更快的响应
- **继续工作**：无中断地继续处理同一任务

## 与其他命令的比较

| 命令 | 效果 | 使用场景 |
|---------|--------|----------|
| `/clear` | 删除所有历史 | 开始全新任务 |
| `/compact` | 总结历史 | 以更少的上下文继续同一任务 |
| `/rewind` | 返回到先前的点 | 撤销最近的更改 |

## 提示
- 具体说明要保留什么以获得最佳结果
- 在压缩之前使用 `/context` 检查上下文使用情况
- 在达到 token 限制之前主动压缩
- 考虑在完成主要里程碑后进行压缩

## 相关命令
- `/context` - 查看当前上下文使用情况
- `/cost` - 检查 token 使用和成本
- `/clear` - 清除所有对话历史
