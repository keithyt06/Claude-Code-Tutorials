# `/config` 命令示例

## 概述
`/config` 命令打开设置界面，您可以在其中查看和修改 Claude Code 的配置设置。

## 何时使用
- 调整 Claude Code 的行为
- 更改默认设置
- 配置集成
- 设置偏好
- 审查当前配置

## 示例用法

### 打开配置

```
User: /config

Claude Code: 正在打开配置设置...

[设置界面显示标签页：]
- 常规
- Model
- 编辑器
- 隐私
- 集成
- 高级
```

## 配置类别

### 1. 常规设置

```
User: /config

[常规标签页]
- 工作目录：/Users/dev/myproject
- 自动保存：已启用
- 确认提示：已启用
- 输出样式：详细
- 主题：深色
```

**示例自定义：**
```
User: 禁用文件操作的确认提示

Claude Code: 已更新配置：
- 确认提示：已禁用

我现在将在不请求确认的情况下进行文件更改。
```

### 2. Model 设置

```
[Model 标签页]
- 当前 Model: Claude Sonnet 4.5
- Temperature: 0.7
- Max Tokens: 4096
- 备用 Model: Claude Haiku
```

**示例：**
```
User: /config

User: 将复杂重构任务的默认 model 更改为 Opus

Claude Code: 已将默认 model 更新为 Claude Opus
```

### 3. 编辑器偏好

```
[编辑器标签页]
- 首选编辑器：VS Code
- Tab 大小：2
- 插入空格：是
- 行结尾：LF
- 文件编码：UTF-8
```

### 4. 工具行为

```
[工具标签页]
- Bash 超时：120 秒
- 最大并发任务：3
- 自动安装依赖：询问
- Git 自动 commit: 已禁用
```

## 常见配置场景

### 场景 1：速度优化

```
User: /config

[调整设置以加快响应：]
- Model: Claude Haiku（更快、更便宜）
- 输出样式：简洁
- 自动保存：已禁用
- 确认提示：已禁用
```

### 场景 2：最高质量

```
User: /config

[调整为最高质量：]
- Model: Claude Opus
- Temperature: 0.3（更专注）
- 输出样式：详细
- 代码审查：始终开启
```

### 场景 3：成本优化

```
User: /config

[最小化成本：]
- 默认 Model: Claude Haiku
- Context 窗口：减少
- 自动压缩：已启用
- 响应缓存：已启用
```

## 高级配置

### 自定义输出样式

```
User: /config

[输出样式]
创建自定义样式：
- 名称："简要"
- 格式：仅代码，最少解释
- 显示行号：否
- 显示文件路径：是
```

### Hook 配置

```
User: /config

[Hooks 标签页]
- Pre-commit: npm run lint && npm test
- Post-file-change: echo "文件已修改: ${FILE}"
- Pre-bash: echo "运行: ${COMMAND}"
```

### 集成设置

```
User: /config

[集成标签页]
- GitHub: 已连接 (@username)
- MCP Servers: 2 个活跃
- 自定义工具：3 个已加载
```

## 配置文件

Claude Code 将配置存储在：
```
~/.config/claude-code/config.json
```

### 示例 config.json：
```json
{
  "model": {
    "default": "claude-sonnet-4-5",
    "temperature": 0.7
  },
  "editor": {
    "tabSize": 2,
    "insertSpaces": true
  },
  "behavior": {
    "autoSave": true,
    "confirmations": true,
    "outputStyle": "detailed"
  },
  "privacy": {
    "telemetry": true,
    "conversationStorage": true
  }
}
```

## 按项目配置

### 项目级 .claude/config.json

```json
{
  "extends": "~/.config/claude-code/config.json",
  "model": {
    "default": "claude-opus"
  },
  "conventions": {
    "commitFormat": "conventional",
    "testBeforeCommit": true
  }
}
```

### 用法：
```
User: /config

Claude Code: 使用 .claude/config.json 中的项目配置
覆盖：
- Model: Claude Opus（项目设置）
- Commit 前测试：已启用（项目设置）
```

## 交互式配置

### 示例会话：

```
User: /config

Claude Code: 配置菜单
1. 常规设置
2. Model 选择
3. 编辑器偏好
4. 隐私设置
5. 集成
6. 高级选项

User: 2

[Model 选择]
当前：Claude Sonnet 4.5

可用 models：
- Claude Opus（最强大）
- Claude Sonnet 4.5（平衡）
- Claude Haiku（最快）

User: 我想对重构使用 Opus，对简单任务使用 Haiku

Claude Code: 我将使用：
- Opus 用于：重构、架构、复杂问题解决
- Haiku 用于：简单编辑、格式化、运行命令
- Sonnet 用于：其他所有（默认）

已保存更新的配置。
```

## 配置配置文件

### 创建配置文件：

```
User: /config

User: 创建带有安全默认值的"生产"配置文件

Claude Code: 已创建配置文件"生产"：
- 确认：始终
- 自动 commit: 已禁用
- Sandbox mode: 已启用
- 需要审查：是

User: 创建"快速开发"配置文件

Claude Code: 已创建配置文件"快速开发"：
- Model: Haiku
- 确认：已禁用
- 自动保存：已启用
- 简洁输出：是
```

### 切换配置文件：

```
User: 使用生产配置文件

Claude Code: 已切换到"生产"配置文件。
现在使用更安全、更谨慎的设置。

User: 切换到快速开发

Claude Code: 已切换到"快速开发"配置文件。
已优化速度和效率。
```

## 最佳实践

### 1. 从保守开始
```
初始设置：
- 确认：已启用
- 自动 commit: 已禁用
- 审查：始终

随着您变得熟悉而调整。
```

### 2. 项目特定覆盖
```
对项目特定设置使用 .claude/config.json：
- 不同项目使用不同 model
- 项目特定约定
- 每个项目的自定义 hooks
```

### 3. 定期审查
```
每月：
User: /config
审查设置，根据使用模式调整
```

## 故障排除

### 配置未应用

```
User: /config 显示正确的设置但行为不同

Claude Code: 检查配置优先级：
1. 命令行标志（最高）
2. 项目 .claude/config.json
3. 用户 ~/.config/claude-code/config.json
4. 默认值（最低）

您的项目配置正在覆盖用户设置。
```

### 重置为默认值

```
User: /config

User: 将所有设置重置为默认值

Claude Code: 您确定吗？这将删除所有自定义设置。

User: 是

Claude Code: 配置已重置为默认值。
```

## 提示
- 从默认值开始并逐步调整
- 使用项目配置保持团队一致性
- 为不同工作流创建配置文件
- 在 CLAUDE.md 中记录不寻常的配置
- 当行为似乎意外时审查配置

## 相关命令
- `/model` - 快速 model 切换
- `/permissions` - 配置访问权限
- `/privacy-settings` - 隐私特定设置
- `/status` - 查看当前活动配置
