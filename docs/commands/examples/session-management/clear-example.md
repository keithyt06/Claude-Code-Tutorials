# `/clear` 命令示例

## 概述
`/clear` 命令会删除当前对话中的所有消息，让您重新开始，同时保留配置设置。

## 何时使用
- 当您想开始一个与当前对话无关的全新任务时
- 当对话变得太长并且您想减少上下文时
- 当您在完成任务后需要一个干净的起点时

## 示例用法

### 场景：开始新任务

```
User: Help me debug this authentication issue...
[关于多次代码更改的长对话]

User: Thanks! That's resolved. Now I want to start working on a completely different feature.

User: /clear

Claude Code: Conversation cleared. How can I help you?

User: I need to implement a new payment gateway integration.
```

## 清除的内容
- 对话中的所有先前消息
- 先前代码讨论的上下文
- 任务历史（todo 将被重置）

## 保留的内容
- 您的配置设置
- 工作目录
- Model 选择
- 权限
- CLAUDE.md memory 文件

## 提示
- 在切换无关任务时使用 `/clear` 以避免混淆
- 如果您想保留一些上下文，请考虑使用 `/compact`
- 如果您想保存对话历史，请在 `/clear` 之前使用 `/export`

## 相关命令
- `/compact` - 减少对话长度同时保留关键上下文
- `/rewind` - 返回到先前的点而不清除所有内容
- `/export` - 在清除之前保存对话
