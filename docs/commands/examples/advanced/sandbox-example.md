# `/sandbox` 命令示例

## 概述
`/sandbox` 命令启用带有文件系统和网络隔离的沙盒 bash 环境，允许 Claude Code 更安全、更自主地执行命令，而不会影响您的系统。

## 何时使用
- 运行不受信任或实验性代码
- 测试可能具有破坏性的命令
- 无风险的自动化脚本执行
- 学习/试验新工具
- 持续集成测试
- 隔离依赖项
- 运行安全评估

## 示例用法

### 场景 1：启用 Sandbox 模式

```
User: /sandbox

Claude Code: Sandbox 模式
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

Sandbox 提供：
✓ 隔离的文件系统（更改不影响主机）
✓ 网络隔离（可选）
✓ 资源限制（CPU、内存）
✓ 安全命令执行
✓ 自动清理

启用 sandbox 模式？(y/n)

User: y

Claude Code: 正在初始化 sandbox 环境...

✓ 创建隔离 container
✓ 挂载安全文件系统
✓ 应用资源限制
✓ 配置网络隔离

Sandbox 已激活！

模式：完全隔离
Container ID: sandbox_abc123
资源：2 个 CPU 核心，4GB RAM
网络：隔离（仅 localhost）

您现在可以安全地执行命令。
输入 /sandbox off 以禁用。
```

### 场景 2：测试潜在危险命令

```
User: 我想测试这个脚本，但不确定它是否安全

User: /sandbox

Claude Code: Sandbox 已启用。

User: 对测试数据运行此清理脚本

Claude Code: 在 sandbox 中执行：

```bash
#!/bin/bash
rm -rf /tmp/test-data/*
find /var/logs -name "*.log" -delete
```

[在 sandbox 中 - 安全执行]

✓ 在 sandbox 中成功执行
✓ 主机系统无更改
✓ 测试数据已删除（仅在 sandbox 中）

结果：
- 已删除：156 个文件（仅 sandbox）
- 已释放：2.3 GB（仅 sandbox）

您的实际系统未更改。
要将这些更改应用到主机吗？(y/n)

User: n

Claude Code: 更改已丢弃。主机系统未受影响。
```

### 场景 3：依赖安装测试

```
User: /sandbox

Claude Code: Sandbox 已激活。

User: 安装这些 npm 包并运行测试

Claude Code: 在 sandbox 环境中：

```bash
npm install axios jest supertest
npm test
```

正在在 sandbox 中安装...
✓ axios@1.6.0 已安装（sandbox）
✓ jest@29.7.0 已安装（sandbox）
✓ supertest@6.3.3 已安装（sandbox）

正在运行测试...
✓ 所有 47 个测试通过

Sandbox 环境测试成功。

选项：
[1] 应用到主机（在真实系统上安装包）
[2] 仅保存包列表（添加到 package.json）
[3] 丢弃（仅保留在 sandbox 中）

User: 2

Claude Code: 已使用依赖项更新 package.json。
Sandbox 包未安装在主机上。
```

## Sandbox 功能

### 文件系统隔离

```
User: /sandbox

Claude Code: Sandbox 文件系统：

隔离目录：
├─ /tmp (sandbox 专用临时目录)
├─ /var (隔离的日志/数据)
├─ /opt (sandbox 安装)
└─ ~/sandbox-workspace (隔离工作区)

只读访问：
├─ /usr (系统二进制文件)
├─ /bin (命令)
└─ /lib (库)

主机项目挂载在：
└─ /project (您的实际代码 - 读/写需确认)

/project 之外的任何更改都仅限于 sandbox。
```

### 网络隔离

```
User: /sandbox --network-isolation

Claude Code: 网络隔离模式：

[1] 完全隔离（无网络访问）
[2] 仅 localhost（仅本地服务）
[3] 允许出站（可以获取，无入站）
[4] 自定义规则

User: 2

Claude Code: 网络：仅 Localhost

允许：
✓ localhost:*（本地服务器）
✓ 127.0.0.1:*（回环）

阻止：
✗ 外部 IP
✗ Internet 访问
✗ 入站连接

这可以防止：
- 意外数据泄露
- 恶意网络调用
- 意外的 API 费用
```

### 资源限制

```
User: /sandbox --show-limits

Claude Code: Sandbox 资源限制：
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

CPU:
├─ 核心：2（共 8 个可用）
├─ 使用限制：80%
└─ 优先级：低

内存：
├─ 限制：4 GB（共 16 GB 可用）
├─ Swap: 已禁用
└─ OOM 保护：已启用

磁盘：
├─ 空间：10 GB
├─ Inodes: 1M
└─ I/O 优先级：低

网络：
├─ 带宽：10 Mbps
└─ 连接：最多 100 个

进程：
├─ 最大 PIDs: 512
└─ 执行时间：最长 1 小时

这些限制防止失控进程影响您的系统。
```

## 使用场景

### 1. 试验新工具

```
User: /sandbox

User: 我想尝试这个新的构建工具，但不想搞乱我的系统

Claude Code: 这是 sandbox 的完美用例！

在 sandbox 中安装：
```bash
curl -sf https://example.com/install.sh | bash
```

✓ 工具已安装在 sandbox 中
✓ 主机系统无更改

让我们测试它：

```bash
newtool build --all
```

✓ 在 sandbox 中构建成功完成

工具可以工作！选项：
[1] 在主机系统上安装
[2] 仅在 sandbox 中使用
[3] 从 sandbox 中删除

User: 2

Claude Code: 工具仅保留在 sandbox 中。
可用于未来的 sandbox 会话。
```

### 2. 测试数据库迁移

```
User: /sandbox

Claude Code: Sandbox 已激活。

User: 测试这些数据库迁移

Claude Code: 设置 sandbox 数据库：

✓ PostgreSQL 已启动（sandbox）
✓ 测试数据已加载（10,000 条记录）
✓ 正在运行迁移...

Migration 001_add_users_table: ✓
Migration 002_add_indexes: ✓
Migration 003_alter_schema: ✗ ERROR

错误：列 'email' 不能为空

迁移在 sandbox 中失败（安全！）。
您的生产数据库未受影响。

修复迁移？(y/n)

User: y

Claude Code: [修复迁移]

在 sandbox 中重新运行...
所有迁移成功！

准备应用到生产环境？(y/n)
```

### 3. 安全测试

```
User: /sandbox --full-isolation

Claude Code: 已启用完全隔离模式。

User: 分析这个可疑脚本

Claude Code: 在隔离的 sandbox 中运行安全分析：

脚本：install.sh
风险：高

检测到的行为：
⚠️  尝试从未知来源下载
⚠️  尝试修改 /etc/hosts
⚠️  创建 cron job
⚠️  连接到外部 IP

在 sandbox 中安全执行。
恶意行为已确认并被阻止。

建议：
✗ 不要在主机系统上运行
✗ 不要批准安装
✓ 报告给安全团队
```

### 4. 自动化测试 CI/CD

```
User: /sandbox

User: 运行完整的 CI pipeline

Claude Code: Sandbox 中的 CI Pipeline：
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

阶段 1：安装依赖项
✓ npm install (sandbox)

阶段 2：Lint
✓ eslint 通过

阶段 3：单元测试
✓ 243/243 测试通过

阶段 4：集成测试
✓ 47/47 测试通过

阶段 5：构建
✓ 生产构建成功

阶段 6：Docker 镜像
✓ 镜像已构建：myapp:latest (sandbox)

所有阶段在 sandbox 中通过！

应用到主机：
[✓] 构建产物
[ ] Docker 镜像
[ ] 部署

User: [选择构建产物]

Claude Code: 正在将构建产物复制到主机...
✓ dist/ 已复制到主机
Sandbox containers 已清理。
```

## Sandbox 管理

### 检查 Sandbox 状态

```
User: /sandbox status

Claude Code: Sandbox 状态：
━━━━━━━━━━━━━━━━━━━━━━━━━

状态：活跃
Container ID: sandbox_abc123
运行时间：45 分钟

资源使用：
├─ CPU: 23%（2 个核心）
├─ 内存：1.8 GB / 4 GB (45%)
├─ 磁盘：3.2 GB / 10 GB (32%)
└─ 网络：隔离（仅 localhost）

活跃进程：
├─ node (PID 1234): 12% CPU，420 MB RAM
├─ postgres (PID 1235): 8% CPU，680 MB RAM
└─ nginx (PID 1236): 3% CPU，45 MB RAM

文件系统更改：
├─ /tmp: 234 个文件已添加
├─ /opt: 12 个包已安装
└─ /var: 45 MB 日志

主机影响：无（完全隔离）
```

### 禁用 Sandbox

```
User: /sandbox off

Claude Code: 禁用 Sandbox？
━━━━━━━━━━━━━━━━━━━━━━━━━━

当前 sandbox 有：
- 3 个运行中的进程
- 234 个临时文件
- 12 个已安装的包
- 3.2 GB 磁盘使用

选项：
[1] 清理并禁用（删除所有）
[2] 保留以供以后使用（保留 container）
[3] 导出更改（保存特定文件）
[4] 取消

User: 1

Claude Code: 正在清理 sandbox...

✓ 停止进程
✓ 删除临时文件
✓ 删除 container
✓ 释放 3.2 GB

Sandbox 已禁用。
主机系统未更改。
```

### 多个 Sandboxes

```
User: /sandbox create --name testing

Claude Code: 正在创建命名 sandbox："testing"

✓ Sandbox "testing" 已创建
✓ 隔离环境就绪

活跃的 sandboxes:
1. default（运行中，45 分钟）
2. testing（新）

在它们之间切换：
/sandbox use default
/sandbox use testing
```

## 配置

### 自定义 Sandbox 配置文件

```
User: /sandbox --configure

Claude Code: Sandbox 配置：
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

配置文件：
[1] Development（宽松限制）
[2] Testing（平衡）
[3] Security（严格隔离）
[4] Custom

User: 4 (Custom)

Claude Code: 自定义 Sandbox 配置：

文件系统隔离：[Full | Partial | None]
User: Full

网络访问：[None | Localhost | Outbound | Full]
User: Localhost

资源限制：
├─ CPU 核心：2
├─ 内存 (GB): 4
├─ 磁盘 (GB): 10
└─ 进程：512

在会话之间持久化 sandbox？(y/n)
User: n

配置已保存。
使用：/sandbox --profile custom
```

### Sandbox 预设

```
User: /sandbox --preset security-audit

Claude Code: 正在加载 "security-audit" 预设：

✓ 完全文件系统隔离
✓ 无网络访问
✓ 只读系统目录
✓ 资源限制：最小
✓ 日志记录：详细
✓ 自动清理：已启用

非常适合安全地分析不受信任的代码。
```

## 高级功能

### 快照和恢复

```
User: /sandbox snapshot create before-migration

Claude Code: 正在创建快照 "before-migration"...

✓ 快照已创建

Sandbox 状态已保存：
- 文件系统：3.2 GB
- 运行中的进程：3
- 网络状态：活跃
- 资源使用：45%

恢复使用：
/sandbox snapshot restore before-migration
```

### 导出 Sandbox 结果

```
User: /sandbox export

Claude Code: 导出 Sandbox 内容：
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

选择要导出的内容：
[✓] 构建产物（dist/）
[✓] 测试结果（coverage/）
[✓] 日志文件
[ ] 已安装的包
[ ] 数据库转储
[ ] 整个文件系统

导出到：~/sandbox-export/

[导出] [取消]

User: [点击导出]

Claude Code: 已导出到 ~/sandbox-export/
- dist/（125 MB）
- coverage/（4 MB）
- logs/（12 MB）

总计：141 MB
```

## 故障排除

### Sandbox 无法启动

```
User: /sandbox

Claude Code: 错误：无法启动 sandbox

可能的原因：
1. Docker 未安装/运行
2. 权限不足
3. 资源限制超出

运行诊断：
User: /doctor

Claude Code: [诊断问题]
问题：Docker 守护程序未运行

修复：sudo systemctl start docker

User: [启动 Docker]

User: /sandbox

Claude Code: ✓ Sandbox 启动成功
```

### Sandbox 性能问题

```
User: /sandbox status

Claude Code: 警告：高资源使用

CPU: 95%（2 个核心完全利用）
内存：3.9 GB / 4 GB (98%)

建议：
1. 增加资源限制：/sandbox --configure
2. 停止 sandbox 中未使用的进程
3. 清理临时文件

优化？(y/n)

User: y

Claude Code: 正在优化 sandbox...
✓ 清理了 1.2 GB 临时文件
✓ 停止了 2 个空闲进程
资源使用：45% CPU，2.1 GB RAM
```

## 最佳实践

### 1. 始终用于不受信任的代码

```
运行来自未知来源的代码时：

User: /sandbox --full-isolation
[安全测试代码]
[审查行为]
[决定是否可以安全地在主机上运行]
```

### 2. 生产前测试

```
User: /sandbox
[运行迁移/部署]
[验证成功]
[如果成功则应用到生产环境]
```

### 3. 定期清理

```
User: /sandbox cleanup

Claude Code: 正在清理旧的 sandboxes...
✓ 删除了 3 个停止的 containers
✓ 释放了 8.4 GB 磁盘空间
```

## 相关命令

- `/doctor` - 诊断 sandbox 问题
- `/config` - 配置 sandbox 默认设置
- `/bashes` - 管理 sandbox 中的进程
- `/permissions` - 控制 sandbox 访问

## 提示

- 对任何不受信任或实验性代码使用 sandbox
- 为安全测试启用完全隔离
- 在风险操作前创建快照
- 清理前导出有用的结果
- 根据需要配置资源限制
- 为不同项目使用命名 sandboxes
- 清理旧的 sandboxes 以释放磁盘空间

## 常见问题

**问：Sandbox 需要 Docker 吗？**
答：是的，目前 sandbox 模式需要安装并运行 Docker。

**问：可以在 sandbox 中访问我的项目文件吗？**
答：可以，您的项目默认以只读方式挂载，需确认后可写。

**问：在 sandbox 中创建的文件会发生什么？**
答：它们被隔离，并在清理 sandbox 时删除（除非导出）。

**问：Sandbox 会影响性能吗？**
答：由于资源限制，影响很小。根据需要配置限制。

**问：可以运行多个 sandboxes 吗？**
答：可以，为不同的项目/用途创建命名 sandboxes。

**问：网络是否完全阻止？**
答：取决于配置。可以完全阻止、仅 localhost 或允许出站。
