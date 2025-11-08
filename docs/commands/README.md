# Claude Code 命令参考指南

欢迎使用 Claude Code 命令参考指南！本综合文档涵盖了 Claude Code 中所有可用的命令，Claude Code 是 Anthropic 官方的 Claude CLI 工具。

## 目录

- [入门指南](#入门指南)
- [命令分类](#命令分类)
  - [Session 管理](#session-管理)
  - [项目与配置](#项目与配置)
  - [工作流与开发](#工作流与开发)
  - [AI Agents 与自动化](#ai-agents-与自动化)
  - [Context 与 Memory](#context-与-memory)
  - [账户与隐私](#账户与隐私)
  - [系统与诊断](#系统与诊断)
  - [高级功能](#高级功能)
- [示例](#示例)

---

## 入门指南

Claude Code 是一个交互式 CLI 工具，可帮助您完成软件工程任务。命令以 `/` 为前缀，可以在与 Claude 对话期间的任何时候执行。

查看所有可用命令：
```bash
/help
```

---

## 命令分类

### Session 管理

#### `/clear`
**用途：** 清除对话历史

删除当前对话中的所有消息，让您重新开始，同时保留配置设置。

**用法：**
```bash
/clear
```

**查看示例：** [examples/session-management/clear-example.md](examples/session-management/clear-example.md)

---

#### `/compact [instructions]`
**用途：** 压缩对话，可选择性地提供关注指令

通过总结对话历史来减少 token 使用，同时保留重要上下文。您可以提供可选的指令来指导应保留的内容。

**用法：**
```bash
/compact
/compact Keep all code examples and error messages
```

**查看示例：** [examples/session-management/compact-example.md](examples/session-management/compact-example.md)

---

#### `/exit`
**用途：** 退出 REPL

优雅地关闭 Claude Code session。

**用法：**
```bash
/exit
```

---

#### `/rewind`
**用途：** 回退对话和/或代码

返回到对话或代码状态的先前点。适用于撤销更改或探索替代方法。

**用法：**
```bash
/rewind
```

**查看示例：** [examples/session-management/rewind-example.md](examples/session-management/rewind-example.md)

---

### 项目与配置

#### `/add-dir`
**用途：** 添加额外的工作目录

扩展 Claude Code 对项目中多个目录的访问权限，使其能够跨代码库的不同部分工作。

**用法：**
```bash
/add-dir
```

**查看示例：** [examples/project-config/add-dir-example.md](examples/project-config/add-dir-example.md)

---

#### `/config`
**用途：** 打开 Settings 界面（Config 标签）

通过交互式界面访问和修改 Claude Code 的配置设置。

**用法：**
```bash
/config
```

**查看示例：** [examples/project-config/config-example.md](examples/project-config/config-example.md)

---

#### `/init`
**用途：** 使用 CLAUDE.md 指南初始化项目

在项目中创建一个 CLAUDE.md 文件，其中包含使用 Claude Code 的最佳实践和指南。

**用法：**
```bash
/init
```

**查看示例：** [examples/project-config/init-example.md](examples/project-config/init-example.md)

---

#### `/memory`
**用途：** 编辑 CLAUDE.md memory 文件

管理包含项目特定上下文和 Claude 应记住的指令的 CLAUDE.md 文件。

**用法：**
```bash
/memory
```

**查看示例：** [examples/project-config/memory-example.md](examples/project-config/memory-example.md)

---

#### `/permissions`
**用途：** 查看或更新权限

查看和修改 Claude Code 在项目中被允许做的事情（文件访问、命令执行等）。

**用法：**
```bash
/permissions
```

**查看示例：** [examples/project-config/permissions-example.md](examples/project-config/permissions-example.md)

---

### 工作流与开发

#### `/review`
**用途：** 请求代码审查

要求 Claude 审查您的代码，以发现潜在的改进、bug 或最佳实践违规。

**用法：**
```bash
/review
```

**查看示例：** [examples/workflow/review-example.md](examples/workflow/review-example.md)

---

#### `/pr_comments`
**用途：** 查看 pull request 评论

显示并与来自 GitHub 或其他版本控制平台的 pull request 评论进行交互。

**用法：**
```bash
/pr_comments
```

**查看示例：** [examples/workflow/pr-comments-example.md](examples/workflow/pr-comments-example.md)

---

#### `/todos`
**用途：** 列出当前的 todo 项

显示当前 session 中所有待办、进行中和已完成的任务。

**用法：**
```bash
/todos
```

**查看示例：** [examples/workflow/todos-example.md](examples/workflow/todos-example.md)

---

#### `/export [filename]`
**用途：** 将当前对话导出到文件或剪贴板

保存对话历史以供文档记录、分享或审查。

**用法：**
```bash
/export
/export conversation-2025-01-08.md
```

**查看示例：** [examples/workflow/export-example.md](examples/workflow/export-example.md)

---

### AI Agents 与自动化

#### `/agents`
**用途：** 管理用于专业任务的自定义 AI 子 agent

创建和配置专业的 AI agent，可以自主处理特定类型的任务。

**用法：**
```bash
/agents
```

**查看示例：** [examples/agents/agents-example.md](examples/agents/agents-example.md)

---

#### `/hooks`
**用途：** 管理工具事件的 hook 配置

设置 shell 命令，以响应特定事件（如工具调用或文件更改）自动执行。

**用法：**
```bash
/hooks
```

**查看示例：** [examples/agents/hooks-example.md](examples/agents/hooks-example.md)

---

#### `/mcp`
**用途：** 管理 MCP server 连接和 OAuth 认证

连接到 Model Context Protocol (MCP) server，以使用自定义工具和数据源扩展 Claude Code 的功能。

**用法：**
```bash
/mcp
```

**查看示例：** [examples/agents/mcp-example.md](examples/agents/mcp-example.md)

---

#### `/bashes`
**用途：** 列出和管理后台任务

查看和控制在后台运行的命令，监控其输出，并在需要时终止它们。

**用法：**
```bash
/bashes
```

**查看示例：** [examples/agents/bashes-example.md](examples/agents/bashes-example.md)

---

### Context 与 Memory

#### `/context`
**用途：** 以彩色网格可视化当前 context 使用情况

查看可用 context 窗口的使用情况，帮助您管理对话长度和 token 使用。

**用法：**
```bash
/context
```

**查看示例：** [examples/context/context-example.md](examples/context/context-example.md)

---

#### `/cost`
**用途：** 显示 token 使用统计信息

显示有关 token 消耗和相关成本的详细信息。有关订阅特定的详细信息，请参阅成本跟踪指南。

**用法：**
```bash
/cost
```

**查看示例：** [examples/context/cost-example.md](examples/context/cost-example.md)

---

#### `/usage`
**用途：** 显示计划使用限制和速率限制状态（仅订阅计划）

查看您当前的使用情况与计划限制的对比，并检查速率限制状态。

**用法：**
```bash
/usage
```

**查看示例：** [examples/context/usage-example.md](examples/context/usage-example.md)

---

### 账户与隐私

#### `/login`
**用途：** 切换 Anthropic 账户

更改您在 Claude Code 中使用的 Anthropic 账户。

**用法：**
```bash
/login
```

**查看示例：** [examples/account/login-example.md](examples/account/login-example.md)

---

#### `/logout`
**用途：** 从 Anthropic 账户注销

结束您当前与 Anthropic 的身份验证 session。

**用法：**
```bash
/logout
```

**查看示例：** [examples/account/logout-example.md](examples/account/logout-example.md)

---

#### `/privacy-settings`
**用途：** 查看和更新隐私设置

控制数据的使用方式，包括对话日志记录和遥测。

**用法：**
```bash
/privacy-settings
```

**查看示例：** [examples/account/privacy-settings-example.md](examples/account/privacy-settings-example.md)

---

### 系统与诊断

#### `/status`
**用途：** 打开 Settings 界面（Status 标签）

查看系统状态，包括版本、model、账户和连接信息。

**用法：**
```bash
/status
```

**查看示例：** [examples/system/status-example.md](examples/system/status-example.md)

---

#### `/doctor`
**用途：** 检查 Claude Code 安装的健康状况

运行诊断以识别和修复常见的安装或配置问题。

**用法：**
```bash
/doctor
```

**查看示例：** [examples/system/doctor-example.md](examples/system/doctor-example.md)

---

#### `/bug`
**用途：** 报告 bug（将对话发送给 Anthropic）

提交包含对话上下文的 bug 报告，以帮助 Anthropic 改进 Claude Code。

**用法：**
```bash
/bug
```

**查看示例：** [examples/system/bug-example.md](examples/system/bug-example.md)

---

#### `/model`
**用途：** 选择或更改 AI model

根据需要在可用的 Claude model（例如 Sonnet、Opus、Haiku）之间切换。

**用法：**
```bash
/model
```

**查看示例：** [examples/system/model-example.md](examples/system/model-example.md)

---

### 高级功能

#### `/sandbox`
**用途：** 启用具有文件系统和网络隔离的沙盒 bash 工具

在隔离环境中运行命令，以实现更安全、更自主的执行，而不影响系统。

**用法：**
```bash
/sandbox
```

**查看示例：** [examples/advanced/sandbox-example.md](examples/advanced/sandbox-example.md)

---

#### `/vim`
**用途：** 进入 vim 模式以交替插入和命令模式

在 Claude Code 中使用 vim 风格的键盘导航和编辑。

**用法：**
```bash
/vim
```

**查看示例：** [examples/advanced/vim-example.md](examples/advanced/vim-example.md)

---

#### `/statusline`
**用途：** 设置 Claude Code 的状态行 UI

配置显示当前 model、token 使用情况和连接状态等信息的状态行。

**用法：**
```bash
/statusline
```

**查看示例：** [examples/advanced/statusline-example.md](examples/advanced/statusline-example.md)

---

#### `/terminal-setup`
**用途：** 安装 Shift+Enter 键绑定以换行（仅限 iTerm2 和 VSCode）

配置终端以在支持的终端中使用 Shift+Enter 进行多行输入。

**用法：**
```bash
/terminal-setup
```

**查看示例：** [examples/advanced/terminal-setup-example.md](examples/advanced/terminal-setup-example.md)

---

#### `/output-style [style]`
**用途：** 直接设置输出样式或从选择菜单中选择

自定义 Claude Code 显示响应的方式（格式、详细程度等）。

**用法：**
```bash
/output-style
/output-style concise
```

**查看示例：** [examples/advanced/output-style-example.md](examples/advanced/output-style-example.md)

---

## 示例

每个命令在 `examples/` 目录中都有详细示例。示例按类别组织：

- **session-management/** - Session 控制命令
- **project-config/** - 项目设置和配置
- **workflow/** - 开发工作流工具
- **agents/** - AI agents 和自动化
- **context/** - Context 和使用监控
- **account/** - 账户管理
- **system/** - 系统诊断
- **advanced/** - 高级功能

## 快速参考卡

### Session 管理
| 命令 | 简要描述 |
|---------|-------------------|
| `/clear` | 清除对话历史 |
| `/compact [instructions]` | 压缩对话，可选择性关注 |
| `/exit` | 退出 REPL |
| `/rewind` | 回退对话和/或代码 |

### 项目与配置
| 命令 | 简要描述 |
|---------|-------------------|
| `/add-dir` | 添加额外的工作目录 |
| `/config` | 打开 Settings 界面（Config 标签） |
| `/init` | 使用 CLAUDE.md 初始化项目 |
| `/memory` | 编辑 CLAUDE.md memory 文件 |
| `/permissions` | 查看或更新权限 |

### 工作流与开发
| 命令 | 简要描述 |
|---------|-------------------|
| `/review` | 请求代码审查 |
| `/pr_comments` | 查看 pull request 评论 |
| `/todos` | 列出当前 todo 项 |
| `/export [filename]` | 将对话导出到文件/剪贴板 |

### AI Agents 与自动化
| 命令 | 简要描述 |
|---------|-------------------|
| `/agents` | 管理自定义 AI 子 agent |
| `/hooks` | 管理 hook 配置 |
| `/mcp` | 管理 MCP server 连接 |
| `/bashes` | 列出和管理后台任务 |

### Context 与 Memory
| 命令 | 简要描述 |
|---------|-------------------|
| `/context` | 以网格形式可视化 context 使用 |
| `/cost` | 显示 token 使用统计 |
| `/usage` | 显示计划使用限制（订阅） |

### 账户与隐私
| 命令 | 简要描述 |
|---------|-------------------|
| `/login` | 切换 Anthropic 账户 |
| `/logout` | 从账户注销 |
| `/privacy-settings` | 查看和更新隐私设置 |

### 系统与诊断
| 命令 | 简要描述 |
|---------|-------------------|
| `/status` | 打开 Settings 界面（Status 标签） |
| `/doctor` | 检查安装健康状况 |
| `/bug` | 向 Anthropic 报告 bug |
| `/model` | 选择或更改 AI model |
| `/help` | 获取使用帮助 |

### 高级功能
| 命令 | 简要描述 |
|---------|-------------------|
| `/sandbox` | 启用沙盒 bash 环境 |
| `/vim` | 进入 vim 模式 |
| `/statusline` | 设置状态行 UI |
| `/terminal-setup` | 安装 Shift+Enter 键绑定 |
| `/output-style [style]` | 设置输出样式 |

## 其他资源

- 官方文档：https://docs.claude.com/en/docs/claude-code
- GitHub Repository：https://github.com/anthropics/claude-code
- 报告问题：https://github.com/anthropics/claude-code/issues

---

**使用 Claude Code 生成**
