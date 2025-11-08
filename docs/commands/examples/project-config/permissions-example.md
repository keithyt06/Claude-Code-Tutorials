# `/permissions` 命令示例

## 概述
`/permissions` 命令允许您查看和修改 Claude Code 在项目中允许执行的操作，包括文件访问、命令执行和网络操作。

## 何时使用
- 初始项目设置
- 限制对敏感文件的访问
- 启用/禁用特定功能
- 审查 Claude 可以访问的内容
- 调试权限相关问题

## 示例用法

### 查看当前权限

```
User: /permissions

Claude Code: 当前权限

文件系统：
  ✓ 读取：/Users/dev/myproject
  ✓ 写入：/Users/dev/myproject
  ✗ 读取：/Users/dev/.env
  ✗ 写入：/Users/dev/config/

命令：
  ✓ npm, yarn, pnpm
  ✓ git
  ✓ node, python3
  ✗ rm, sudo
  ✗ curl, wget (使用 WebFetch 代替)

网络：
  ✓ WebFetch（受控）
  ✗ 直接网络访问
```

## 权限类别

### 1. 文件系统权限

```
User: /permissions

[文件系统标签页]

读取权限：
✓ /Users/dev/myproject/src
✓ /Users/dev/myproject/tests
✗ /Users/dev/myproject/.env
✗ /Users/dev/myproject/secrets/

写入权限：
✓ /Users/dev/myproject/src
✓ /Users/dev/myproject/tests
✗ /Users/dev/myproject/package.json（受保护）
✗ /Users/dev/myproject/.git/config（受保护）
```

**示例：保护敏感文件**
```
User: /permissions

User: 阻止访问 .env 文件和凭据

Claude Code: 已添加限制：
- .env*（所有 env 文件）
- **/credentials/**
- **/secrets/**
- **/.aws/**

我不会读取或修改这些文件。
```

### 2. 命令执行权限

```
User: /permissions

[命令标签页]

允许：
✓ npm install, npm run, npm test
✓ git add, git commit, git push
✓ node, python3, go run
✓ make, cmake
✓ docker（只读）

受限：
⚠ rm, rmdir（需要确认）
⚠ chmod, chown（需要确认）

阻止：
✗ sudo, su
✗ dd, mkfs
✗ iptables, netstat
```

**示例：启用 Docker 命令**
```
User: /permissions

User: 允许完整的 docker 命令

Claude Code: 已更新权限：
✓ docker build
✓ docker run
✓ docker compose up
✓ docker exec

Docker 命令现在已完全启用。
```

### 3. 网络权限

```
User: /permissions

[网络标签页]

允许：
✓ WebFetch（沙盒化的 HTTP/HTTPS）
✓ npm/yarn 包下载
✓ git clone/pull/push

阻止：
✗ 直接 socket 连接
✗ 原始 curl/wget
✗ netcat, telnet
```

## 常见权限场景

### 场景 1：安全生产项目

```
User: /permissions

User: 为生产代码库设置严格权限

Claude Code: 已应用安全配置文件：

只读：
✓ src/（可读取，不可修改）
✓ tests/
✓ docs/

读写：
✓ /tmp/claude-workspace

阻止：
✗ .env, .env.*
✗ config/production.json
✗ secrets/
✗ .aws/
✗ .ssh/

命令：
✓ git status, git diff（只读）
✗ git push, git commit
✗ npm install（不允许依赖更改）
✓ npm test

这确保我可以分析代码但不进行破坏性更改。
```

### 场景 2：开放开发环境

```
User: /permissions

User: 为我的个人项目启用完全访问

Claude Code: 已应用开发配置文件：

文件访问：完全
✓ 读写整个项目
⚠ 确认：.env, package.json

命令：大多数允许
✓ 所有 git 命令
✓ 所有 npm/yarn 命令
✓ 构建和测试命令
⚠ 确认：rm -rf, chmod

网络：受控
✓ WebFetch 用于文档
✓ 包管理器下载
```

### 场景 3：仅代码审查

```
User: /permissions

User: 我只想要代码审查，不要修改

Claude Code: 已应用只读配置文件：

文件访问：
✓ 读取所有项目文件
✗ 无写入访问

命令：
✓ git diff, git log
✓ npm test（在 sandbox 中）
✗ 无文件修改
✗ 无 git commits

我可以审查和分析但不能进行更改。
```

## 权限规则

### 文件模式

```
User: /permissions

User: 添加自定义文件规则

模式：
- *.env → 阻止
- package*.json → 需要确认
- src/**/*.ts → 完全访问
- test/**/* → 完全访问
- node_modules/** → 只读
```

### 命令白名单

```
User: /permissions

User: 仅允许特定命令

白名单：
- git status
- git diff
- git log
- npm test
- npm run lint

所有其他命令将需要明确批准。
```

## 交互式权限管理

```
User: /permissions

Claude Code: 权限管理器

当前配置文件：开发（中等）

快速操作：
1. 切换到安全（限制性）
2. 切换到开放（宽松）
3. 自定义权限
4. 审查最近的权限请求

User: 3

[自定义权限]

文件系统：
- 允许：src/, tests/, docs/
- 确认：package.json, tsconfig.json
- 阻止：.env*, secrets/, .aws/

命令：
- 允许：git, npm, node
- 确认：rm, chmod
- 阻止：sudo, curl

应用更改？(y/n)

User: y

Claude Code: 权限已更新。
```

## 权限请求

### 运行时权限请求

```
User: 安装新包 'lodash'

Claude Code: 我需要权限运行：npm install lodash

这将：
- 修改 package.json
- 修改 package-lock.json
- 添加到 node_modules/

允许？(yes/no/always/never)

User: always

Claude Code: 已将 npm install 添加到允许的命令。
正在安装 lodash...
```

### 临时权限授予

```
User: /permissions

User: 临时允许此会话使用 curl

Claude Code: 已授予临时权限：
✓ curl（仅限会话）

这将在您重启 Claude Code 时被撤销。
```

## 权限配置文件

### 预定义配置文件

```
1. 最高安全
   - 只读访问
   - 无命令执行
   - 无网络访问

2. 安全生产
   - 有限写入访问
   - 确认的命令
   - 审计日志

3. 标准开发
   - 正常文件访问
   - 大多数命令允许
   - 破坏性操作需确认

4. 完全访问
   - 完整文件系统访问
   - 所有命令允许
   - 最少确认
```

### 创建自定义配置文件

```
User: /permissions

User: 创建自定义配置文件 "frontend-only"

配置文件：frontend-only
- 访问：src/components/, src/pages/, src/styles/
- 阻止：backend/, api/, database/
- 命令：npm, git（无 docker, 无 python）
- 用于：前端专注开发

Claude Code: 已创建自定义配置文件 "frontend-only"。
```

## 最佳实践

### 1. 从限制性开始
```
开始时：
- 敏感操作需确认
- 阻止 .env 和 secrets
- 破坏性命令需确认

根据需要放宽。
```

### 2. 使用模式
```
不要单独阻止文件：
**/*.env
**/*secret*
**/*credential*
**/.*rc（shell 配置文件）
```

### 3. 定期审计
```
每周：
User: /permissions
User: 显示最近的权限请求

审查并相应调整。
```

### 4. 项目特定权限
```
存储在 .claude/permissions.json：
{
  "read": ["src/", "tests/"],
  "write": ["src/", "tests/"],
  "block": [".env*", "secrets/"],
  "commands": {
    "allow": ["npm", "git"],
    "confirm": ["rm"],
    "block": ["sudo"]
  }
}
```

## 故障排除

### 权限被拒绝错误

```
Claude Code: 错误：权限被拒绝 - 无法写入 package.json

User: /permissions

[检查权限]
问题：package.json 在受保护列表中

解决方案：
User: 允许修改 package.json

Claude Code: 已更新。现在可以修改 package.json。
```

### 过度限制的权限

```
User: 为什么你不能运行测试？

Claude Code: /permissions 显示 npm test 被阻止

User: /permissions
User: 允许 npm test

Claude Code: npm test 现在已允许。
```

## 安全考虑

### 敏感数据保护
```
始终阻止：
- .env, .env.*
- *secret*, *credential*
- .ssh/, .aws/, .gcp/
- 私钥
```

### 命令安全
```
需要确认：
- rm -rf
- chmod
- chown
- 数据库操作
- 生产部署
```

### 网络安全
```
优先选择：
- WebFetch 而不是 curl
- 包管理器而不是手动下载
- 沙盒化操作
```

## 提示
- 在项目设置期间审查权限
- 不确定时使用确认模式
- 为不同工作流创建配置文件
- 在 CLAUDE.md 中记录自定义权限
- 定期审计权限请求
- 使用有效的最严格权限

## 相关命令
- `/config` - 常规配置
- `/sandbox` - 隔离命令执行
- `/status` - 查看活动权限
- `/privacy-settings` - 隐私相关权限
