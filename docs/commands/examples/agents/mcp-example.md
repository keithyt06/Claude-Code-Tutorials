# `/mcp` 命令示例

## 概述
`/mcp` 命令管理 Model Context Protocol (MCP) server 连接，允许 Claude Code 通过标准化协议与外部工具、数据源和服务集成。MCP servers 扩展了 Claude 的功能，超越了内置功能。

## 何时使用
- 连接到外部数据库
- 与 APIs 和 web 服务集成
- 访问云服务（AWS、GCP、Azure）
- 使用专用工具（Slack、Jira、GitHub）
- 创建自定义工具集成
- 管理服务的 OAuth 身份验证

## 示例用法

### 场景1：查看 MCP Servers

```
User: /mcp

Claude Code: Model Context Protocol (MCP) Servers
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

已连接的 Servers：

┌──────────────┬──────────────┬─────────────────────────┐
│ Server       │ Status       │ Tools Available         │
├──────────────┼──────────────┼─────────────────────────┤
│ filesystem   │ ● Connected  │ 5 tools                 │
│ github       │ ● Connected  │ 12 tools                │
│ postgres     │ ○ Disconn'd  │ 8 tools (unavailable)   │
└──────────────┴──────────────┴─────────────────────────┘

可用但未连接：
- slack-mcp (Slack 集成)
- aws-mcp (AWS 服务)
- jira-mcp (Jira 项目管理)

选项：
[1] 连接到 server
[2] 从 server 断开连接
[3] 添加新 server
[4] 配置 server
[5] 查看 server 详情

选择选项（1-5）：
```

### 场景2：连接到 MCP Server

```
User: /mcp connect github

Claude Code: 连接到 GitHub MCP Server
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

Server：github-mcp
类型：需要 OAuth

此 server 提供：
- Repository 管理
- Issue 跟踪
- Pull request 操作
- 代码搜索
- GitHub Actions

需要身份验证：
[1] OAuth 登录（推荐）
[2] Personal Access Token
[3] GitHub App

选择身份验证方法（1-3）：

User: 1

Claude Code: 打开 GitHub OAuth 流程...

[浏览器打开]

请授权 Claude Code 访问：
✓ 读取 repositories
✓ 创建/更新 issues
✓ 管理 pull requests
✓ 读/写代码

[用户授权]

Claude Code: ✓ GitHub MCP 已连接！

可用工具：
- github_create_issue
- github_list_repos
- github_create_pr
- github_search_code
- github_get_file
- github_list_issues
- github_update_issue
- github_merge_pr
- github_create_branch
- github_list_prs
- github_get_pr_diff
- github_review_pr

您现在可以在对话中直接使用 GitHub：

示例：
"列出我的开放 pull requests"
"为这个 bug 创建一个 issue"
"在 repo 中搜索类似代码"
```

### 场景3：在对话中使用 MCP Tools

```
User: 列出我当前 repository 中的所有开放 issues

Claude Code: 使用 GitHub MCP server...

调用：github_list_issues
Repository：myuser/myproject
过滤：state=open

结果：
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

#45：登录流程中的身份验证 bug
     打开时间：2天前 由 john
     标签：bug、high-priority
     分配者：无

#42：添加深色模式支持
     打开时间：5天前 由 sarah
     标签：enhancement
     分配者：mike

#38：更新依赖项
     打开时间：1周前 由 bot
     标签：maintenance
     分配者：无

总计：3个开放 issues

您想让我处理其中任何一个吗？
```

## 内置 MCP Servers

### 1. Filesystem MCP

```
User: /mcp details filesystem

Claude Code: Filesystem MCP Server
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

Status：● Connected（内置）
描述：扩展文件系统操作

可用工具：
1. fs_watch         - 监控文件更改
2. fs_find          - 按模式搜索文件
3. fs_tree          - 显示目录树
4. fs_permissions   - 管理文件权限
5. fs_metadata      - 获取文件元数据

使用示例：

监控更改：
"监控 src/ 目录的更改"

查找文件：
"在项目中查找所有 .env 文件"

显示树：
"显示项目结构"
```

### 2. Git MCP

```
User: /mcp details git

Claude Code: Git MCP Server
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

Status：● Connected（内置）
描述：高级 git 操作

可用工具：
1. git_history      - 查看 commit 历史
2. git_blame        - 显示文件 blame
3. git_diff_branch  - 比较分支
4. git_cherry_pick  - Cherry-pick commits
5. git_rebase       - Rebase 分支
6. git_stash        - 管理 stashes
7. git_tag          - Tag 管理
8. git_remote       - Remote 操作

用法：

"显示 login.ts 的 git 历史"
"谁最后修改了这个函数？"
"比较 main 和 dev 分支"
```

### 3. Web MCP

```
User: /mcp details web

Claude Code: Web MCP Server
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

Status：● Connected（内置）
描述：Web 抓取和 API 调用

可用工具：
1. web_fetch        - 获取网页内容
2. web_api_call     - 进行 HTTP 请求
3. web_parse_html   - 解析 HTML 文档
4. web_screenshot   - 捕获截图
5. web_monitor      - 监控 URLs 的更改

用法：

"从 example.com 获取最新文档"
"向此 API endpoint 发送 POST 请求"
"解析此 HTML 页面的表格"
```

## 第三方 MCP Servers

### GitHub MCP

```
User: /mcp add github

Claude Code: 添加 GitHub MCP Server
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

安装：
npm install -g @modelcontextprotocol/server-github

配置：
Server 路径：@modelcontextprotocol/server-github
身份验证：OAuth 或 PAT

您想要：
[1] 现在安装和配置
[2] 配置现有安装
[3] 手动设置说明

User: 1

Claude Code: 正在安装 GitHub MCP...

✓ Package 已安装
✓ 配置已创建

使用 GitHub 进行身份验证：
[打开 OAuth 流程]

✓ 已连接到 GitHub MCP！

可用命令：
- 列出 repositories
- 创建/管理 issues
- 处理 pull requests
- 搜索代码
- 查看 GitHub Actions
```

### Slack MCP

```
User: /mcp add slack

Claude Code: 添加 Slack MCP Server
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

Slack MCP server 提供：
- 向 channels 发送消息
- 读取 channel 历史记录
- 管理 threads
- 上传文件
- 搜索消息

安装：
npm install -g @modelcontextprotocol/server-slack

需要配置：
1. Slack OAuth token
2. Workspace 选择
3. Channel 权限

[设置向导引导配置]

✓ Slack MCP 已配置！

示例用法：
"向 #dev-team channel 发送消息"
"在 Slack 中搜索有关身份验证的消息"
"将此错误日志发布到 #bugs"
```

### Database MCP (PostgreSQL)

```
User: /mcp add postgres

Claude Code: 添加 PostgreSQL MCP Server
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

连接详情：

Host：localhost
Port：5432
Database：myapp_db
Username：postgres
Password：[隐藏]

SSL：[✓] 启用
Pool size：10

测试连接...
✓ 连接成功！

可用工具：
- postgres_query       （运行 SQL 查询）
- postgres_schema      （查看 schema）
- postgres_explain     （解释查询计划）
- postgres_migrate     （运行 migrations）
- postgres_backup      （创建备份）

用法：

"显示 users 表 schema"
"查询数据库中的活跃用户"
"解释此慢查询的执行计划"
```

### AWS MCP

```
User: /mcp add aws

Claude Code: 添加 AWS MCP Server
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

AWS MCP 提供访问：
- S3（存储）
- Lambda（函数）
- DynamoDB（数据库）
- EC2（计算）
- CloudWatch（监控）

身份验证：
[1] AWS CLI 凭据（~/.aws/credentials）
[2] IAM role
[3] Access key + Secret

User: 1

Claude Code: 使用 AWS CLI 凭据...

✓ 认证为：user@example.com
✓ Region：us-east-1
✓ Account：123456789012

可用工具：
- s3_list_buckets
- s3_get_object
- s3_put_object
- lambda_invoke
- dynamodb_query
- ec2_list_instances
- cloudwatch_get_metrics

示例：
"列出所有 S3 buckets"
"调用 processData Lambda 函数"
"查询 users DynamoDB 表"
```

## 自定义 MCP Servers

### 创建自定义 Server

```
User: /mcp create

Claude Code: 创建自定义 MCP Server
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

Server 名称：company-api

描述：内部公司 API 集成

Base URL：https://api.company.internal

身份验证：
[1] API Key
[2] OAuth
[3] Basic Auth
[4] Custom

User: 1

API Key 位置：
( ) Header
(•) Query parameter
( ) Custom

Header 名称：X-API-Key
API Key：[输入 key]

定义工具（endpoints）：

工具1：
名称：get_employee
Endpoint：/api/employees/{id}
方法：GET
描述：按 ID 获取员工

工具2：
名称：create_ticket
Endpoint：/api/tickets
方法：POST
描述：创建支持票证

添加更多工具？（y/n）

User: n

Claude Code: ✓ 自定义 MCP server 已创建！

配置已保存：
.claude/mcp-servers/company-api.json

Server 可以使用：
"获取 ID 12345 的员工信息"
"为此 bug 创建支持票证"
```

### 自定义 Server 配置

```
.claude/mcp-servers/company-api.json:

{
  "name": "company-api",
  "type": "http",
  "baseUrl": "https://api.company.internal",
  "authentication": {
    "type": "apiKey",
    "location": "header",
    "name": "X-API-Key",
    "value": "${COMPANY_API_KEY}"
  },
  "tools": [
    {
      "name": "get_employee",
      "description": "按 ID 获取员工",
      "endpoint": "/api/employees/{id}",
      "method": "GET",
      "parameters": {
        "id": {
          "type": "string",
          "required": true,
          "description": "员工 ID"
        }
      }
    },
    {
      "name": "create_ticket",
      "description": "创建支持票证",
      "endpoint": "/api/tickets",
      "method": "POST",
      "body": {
        "title": "string",
        "description": "string",
        "priority": "enum[low,medium,high]"
      }
    }
  ]
}
```

## OAuth 管理

### 连接 OAuth 服务

```
User: /mcp oauth github

Claude Code: GitHub OAuth 身份验证
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

打开授权页面...

[浏览器打开：github.com/login/oauth/authorize]

请求的权限：
✓ 读取 repositories
✓ 写入 issues
✓ 管理 pull requests
✓ 读取组织成员资格

授权 Claude Code？[用户批准]

Claude Code: ✓ 收到 OAuth token
✓ Token 已安全存储
✓ GitHub MCP 已认证

Token 过期：2025-02-08（30天）
在到期前刷新：/mcp oauth refresh github
```

### 刷新 OAuth Token

```
User: /mcp oauth refresh github

Claude Code: 正在刷新 GitHub OAuth token...

旧 token 过期：2025-01-10（2天后）

[自动刷新流程]

✓ 收到新 token
✓ Token 过期：2025-02-09（30天）

GitHub MCP 保持连接。
```

### 撤销 OAuth

```
User: /mcp oauth revoke slack

Claude Code: 撤销 Slack OAuth Token
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

这将：
- 断开 Slack MCP server
- 撤销 access token
- 删除存储的凭据

继续？（y/n）

User: y

Claude Code: ✓ OAuth token 已撤销
✓ Slack MCP 已断开连接

重新连接：
/mcp connect slack
```

## Server 配置

### 配置 Server 设置

```
User: /mcp config postgres

Claude Code: 配置 PostgreSQL MCP
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

连接设置：

Host：localhost
Port：5432
Database：myapp_db
Username：postgres
SSL：启用

性能设置：

连接池大小：10
查询超时：30s
最大查询结果：1000
启用查询缓存：是

安全设置：

[✓] DELETE 需要确认
[✓] DROP 需要确认
[✓] TRUNCATE 需要确认
[ ] 只读模式
[✓] 记录所有查询

保存更改？（y/n）

User: y

✓ 配置已更新
正在重新连接到 server...
✓ 使用新设置连接
```

### Server 健康检查

```
User: /mcp health

Claude Code: MCP Servers 健康检查
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

检查所有已连接的 servers...

filesystem MCP：
✓ Status：健康
✓ 响应时间：5ms
✓ Tools：5/5 工作中

github MCP：
✓ Status：健康
✓ 响应时间：234ms
✓ 身份验证：有效
✓ 速率限制：4850/5000 剩余
✓ Tools：12/12 工作中

postgres MCP：
⚠ Status：警告
⚠ 响应时间：1234ms（慢）
✓ 连接：活动
⚠ Pool：9/10 连接已使用
✓ Tools：8/8 工作中

建议：
- postgres：考虑增加池大小
- postgres：检测到慢查询
```

## 故障排除

### 连接失败

```
User: /mcp connect postgres

Claude Code: 错误：连接失败

原因：无法连接到 localhost:5432

诊断：
✗ PostgreSQL 未运行
✓ 网络可访问
✓ 凭据有效

解决方案：
[1] 启动 PostgreSQL server
[2] 检查连接设置
[3] 验证防火墙规则
[4] 手动测试连接

User: 1

Claude Code: 启动 PostgreSQL？

命令：brew services start postgresql

运行命令？（y/n）

User: y

[PostgreSQL 启动]

重试连接...
✓ 连接成功！
```

### 身份验证过期

```
Claude Code: ⚠️ GitHub MCP 身份验证已过期

您的 OAuth token 在3天前过期。

选项：
[1] 刷新 token（推荐）
[2] 重新认证
[3] 断开 server 连接

User: 1

Claude Code: 正在刷新 OAuth token...

[OAuth 流程打开]

✓ 身份验证已刷新
✓ Token 有效期30天
✓ GitHub MCP 已重新连接
```

### 工具不工作

```
User: 列出我的 GitHub repositories

Claude Code: 使用 github_list_repos 工具时出错

原因：权限不足

当前权限：
✓ 读取 repositories
✗ 列出组织（必需）

修复：
/mcp oauth github --update-permissions

User: /mcp oauth github --update-permissions

[带有额外权限的重新授权流程]

✓ 权限已更新
✓ 工具现在可用

User: 列出我的 GitHub repositories

Claude Code: [成功列出 repositories]
```

## 最佳实践

### 1. 安全性

```
❌ 不要硬编码凭据：
{
  "apiKey": "sk_live_abc123..."
}

✓ 使用环境变量：
{
  "apiKey": "${API_KEY}"
}

✓ 可用时使用 OAuth：
{
  "authentication": "oauth"
}
```

### 2. 连接管理

```
✓ 仅连接需要的 servers
✓ 断开未使用的 servers
✓ 定期监控健康状况
✓ 保持身份验证最新
```

### 3. 速率限制

```
监控 API 使用：

User: /mcp stats github

GitHub MCP 统计：
- 今天的请求：234
- 速率限制：4766/5000
- 在以下时间后重置：42分钟

通过以下方式避免速率限制：
- 缓存结果
- 批处理请求
- 使用 webhooks
```

## MCP Server 开发

### 创建 MCP Server (Node.js)

```
MCP server 实现示例：

// my-mcp-server.js
const { MCPServer } = require('@modelcontextprotocol/sdk');

const server = new MCPServer({
  name: 'my-custom-server',
  version: '1.0.0',
  description: '自定义 MCP server'
});

// 注册工具
server.registerTool({
  name: 'my_tool',
  description: '执行有用的操作',
  parameters: {
    param1: {
      type: 'string',
      required: true
    }
  },
  handler: async (params) => {
    // 工具实现
    return {
      success: true,
      result: `已处理：${params.param1}`
    };
  }
});

server.start();

// 使用 Claude Code 注册：
User: /mcp add --path ./my-mcp-server.js
```

## 相关命令

- `/agents` - 使用 agents 与 MCP tools
- `/hooks` - 自动触发 MCP 操作
- `/permissions` - 控制 MCP server 访问
- `/config` - 配置 MCP 设置

## 提示

- 从内置 MCP servers 开始
- 使用 OAuth 以获得更好的安全性
- 监控速率限制
- 保持 servers 更新
- 记录自定义 servers
- 定期测试连接
- 使用环境变量存储 secrets

## 常见问题

**Q：什么是 MCP？**
A：Model Context Protocol - 将 AI 连接到外部工具/数据的标准。

**Q：MCP servers 安全吗？**
A：内置 servers 是安全的。使用前审查第三方 servers。

**Q：MCP 调用使用 tokens 吗？**
A：是的，使用工具会消耗 API tokens。

**Q：我可以创建自己的 MCP server 吗？**
A：可以，使用 MCP SDK 构建自定义 servers。

**Q：可以连接多少个 servers？**
A：没有硬限制，但更多 servers = 更复杂。

**Q：MCP servers 可以离线工作吗？**
A：只有不需要网络访问的才可以（例如 filesystem MCP）。

**Q：如何与团队共享 MCP 配置？**
A：将 `.claude/mcp-servers/` 配置 commit 到 git（排除 secrets）。
