# `/doctor` 命令示例

## 概述
`/doctor` 命令对您的 Claude Code 安装运行全面的健康诊断，自动识别和修复常见问题。

## 何时使用
- 排查安装问题
- 调试配置问题
- 检查系统要求
- 验证 API 连接
- 更新或重新安装后
- 遇到意外行为时

## 示例用法

### 基本诊断

```
User: /doctor

Claude Code: 正在运行系统诊断...
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

检查 Claude Code 安装...

✓ Claude Code 已安装 (v1.2.3)
✓ 安装路径有效
✓ 依赖已安装
✓ 找到配置文件
✓ 权限正确

检查系统要求...

✓ Node.js v20.10.0 (需要 >= 18.0.0)
✓ npm v10.2.3
✓ 操作系统受支持 (macOS 14.2)
✓ 磁盘空间：512 GB 可用
✓ 内存：16 GB 可用

检查 API 连接...

✓ 互联网连接活动
✓ 可以访问 api.anthropic.com
✓ API key 已配置
✓ 认证成功
✓ Model 访问已验证

检查配置...

✓ 配置文件有效
✓ 工作目录可访问
✓ 权限已配置
✓ 未检测到冲突

所有检查通过！✓

Claude Code 健康且可使用。
```

## 常见已修复问题

### 问题 1：API Key 未设置

```
User: /doctor

检查 API 连接...
✗ API key 未配置

修复：/doctor 自动提示输入 API key

输入您的 Anthropic API key：
User: sk-ant-...

✓ API key 已保存
✓ 认证成功

问题已解决！
```

### 问题 2：权限问题

```
检查权限...
✗ 无法写入配置目录

/doctor 尝试自动修复：

正在修复权限...
✓ 已更新目录权限
✓ 配置现在可写

问题已解决！
```

### 问题 3：过时的依赖

```
检查依赖...
⚠ 发现 3 个过时的依赖

要更新的依赖：
- axios: 1.5.0 → 1.6.2
- chalk: 5.2.0 → 5.3.0
- inquirer: 9.2.0 → 9.2.12

现在更新？(y/n)
User: y

正在更新...
✓ 依赖已更新
✓ 所有依赖都是最新的

问题已解决！
```

## 详细诊断

```
User: /doctor --detailed

运行全面诊断...

1. 安装检查
   ✓ Binary: /usr/local/bin/claude
   ✓ Modules: /usr/local/lib/node_modules/@anthropic/claude-code
   ✓ Symlinks: 有效
   ✓ 版本：1.2.3

2. 系统要求
   ✓ Node.js: 20.10.0 (✓)
   ✓ npm: 10.2.3 (✓)
   ✓ OS: macOS 14.2.1 (支持)
   ✓ 架构：arm64 (✓)
   ✓ CPU: 8 核可用
   ✓ RAM: 16 GB (最低 4 GB)
   ✓ 磁盘：512 GB 可用 (最低 1 GB)

3. API 连接
   ✓ DNS 解析：api.anthropic.com
   ✓ HTTPS 连接：成功
   ✓ SSL 证书：有效
   ✓ API endpoint: 可访问
   ✓ 认证：有效 token
   ✓ 速率限制：正常
   ✓ 响应时间：234ms (良好)

4. 配置文件
   ✓ 主配置：~/.config/claude/config.json
   ✓ Hooks: 4 个文件，全部可执行
   ✓ MCP servers: 3 个已配置
   ✓ 权限：正确
   ✓ 语法：有效 JSON

5. 环境变量
   ✓ ANTHROPIC_API_KEY: 已设置
   ✓ HOME: 已设置
   ✓ PATH: 包含 claude
   ✓ NODE_ENV: production
   ✗ HTTP_PROXY: 未设置 (可选)

6. 依赖
   ✓ 所有依赖已安装
   ✓ 无版本冲突
   ✓ 无缺失模块

7. 功能支持
   ✓ Sandbox: Docker 可用
   ✓ Git: 已安装 (v2.42.0)
   ✓ Terminal: 支持
   ✓ MCP: 已启用

8. 最近错误
   ✓ 最近 24 小时无错误
   ✓ 日志文件干净

诊断完成：所有系统健康 ✓
```

## 修复特定问题

```
User: /doctor --fix connectivity

诊断连接问题...

测试：
1. 互联网连接... ✓
2. DNS 解析... ✓
3. 防火墙... ⚠ 端口 443 可能被阻止
4. API endpoint... ✗ 超时

发现问题：无法访问 API

尝试自动修复：

[1] 测试备用 DNS
[2] 检查防火墙规则
[3] 测试 proxy 设置
[4] 验证 API 状态

运行修复...
✓ DNS 工作
⚠ 防火墙阻止 HTTPS
✓ 已添加防火墙例外
✓ API 现在可访问

连接已恢复！
```

## 诊断报告

```
User: /doctor --report

生成诊断报告...

已保存到：claude-diagnostic-2025-01-08.txt

系统诊断报告
日期：2025-01-08 14:45:23

安装：通过
系统要求：通过
API 连接：通过
配置：通过
依赖：通过
功能：通过

发现问题：0
警告：0
错误：0

状态：健康 ✓

[将此文件附加到支持工单]
```

## 相关命令

- `/status` - 快速状态检查
- `/config` - 配置管理
- `/help` - 命令帮助

## 提示

- 安装后运行 `/doctor`
- 报告问题前使用
- 系统更新后检查
- 在支持工单中包含报告
- 使用 --detailed 进行全面检查

## 常见问题

**问：/doctor 需要多长时间？**
答：通常所有检查需要 10-30 秒。

**问：会自动修复问题吗？**
答：是的，它会尝试自动修复常见问题。

**问：会消耗 tokens 吗？**
答：不会，这是本地诊断工具。

**问：应该定期运行吗？**
答：仅在遇到问题或更新后运行。
