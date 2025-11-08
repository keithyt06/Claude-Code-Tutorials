# `/agents` 命令示例

## 概述
`/agents` 命令允许您管理专门任务的自定义 AI subagents。Subagents 是可以独立处理特定类型工作的自主 AI 助手，例如代码审查、测试、文档编写或研究。

## 何时使用
- 将专门任务委托给专注的 agents
- 并行运行多个任务
- 创建可重用的 workflows
- 自动化重复性任务
- 设置自定义审查流程
- 构建项目特定的助手

## 示例用法

### 场景1：查看可用的 Agents

```
User: /agents

Claude Code: AI Agents 管理
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

内置 Agents：
┌────────────────┬─────────────────────────────────────┐
│ 名称           │ 描述                                │
├────────────────┼─────────────────────────────────────┤
│ code-reviewer  │ 审查代码问题和质量                   │
│ test-writer    │ 生成单元测试                         │
│ doc-generator  │ 创建文档                            │
│ bug-hunter     │ 查找和分析 bugs                      │
│ refactorer     │ 建议代码改进                         │
│ security-audit │ 安全漏洞扫描                         │
└────────────────┴─────────────────────────────────────┘

自定义 Agents（在 .claude/agents/ 中）：
┌────────────────┬─────────────────────────────────────┐
│ api-designer   │ 设计 REST API endpoints              │
│ db-optimizer   │ 优化数据库查询                       │
└────────────────┴─────────────────────────────────────┘

选项：
[1] 启动一个 agent
[2] 创建自定义 agent
[3] 管理 agents
[4] 查看 agent 历史记录

选择选项（1-4）：
```

### 场景2：启动内置 Agent

```
User: /agents code-reviewer

Claude Code: 正在启动 code-reviewer agent...
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

Agent：code-reviewer
任务：审查最近的代码更改
范围：当前目录中的已修改文件

开始审查...

[Agent 自主运行]

Agent 报告：
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

已审查文件：5
发现问题：8（3个高，3个中，2个低）

高优先级问题：
1. src/auth.ts:45 - SQL injection 漏洞
   风险：高安全风险
   修复：使用参数化查询

2. src/api/users.ts:67 - 缺少错误处理
   风险：应用程序在无效输入时崩溃
   修复：添加 try-catch block

3. src/utils/validation.ts:23 - Regex DoS 漏洞
   风险：性能下降
   修复：使用更简单的验证

中优先级问题：
4. useEffect 中的内存泄漏（UserForm.tsx:89）
5. 命名约定不一致（3个文件）
6. 缺少 TypeScript 类型（2个函数）

低优先级问题：
7. 代码中遗留 Console.log 语句
8. 未使用的 imports

建议：
- 在部署前修复高优先级问题
- 考虑添加 pre-commit hooks
- 更新 ESLint 配置

您想让我修复这些问题吗？（y/n）

User: y

Claude Code: [自动修复问题]

Agent 成功完成。
所有高优先级问题已解决。
```

### 场景3：创建自定义 Agent

```
User: /agents create

Claude Code: 创建自定义 Agent
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

Agent 名称：api-designer

描述：设计 RESTful API endpoints

专业领域（此 agent 擅长什么）：
User: 遵循最佳实践设计 REST APIs、OpenAPI specs 和正确的 HTTP 语义

Agent 可以使用的工具：
[✓] Read（读取文件）
[✓] Write（创建文件）
[✓] Grep（搜索代码）
[✓] Bash（运行命令）
[ ] WebFetch（获取外部数据）

Agent 行为：
( ) Autonomous - 无需询问即完成任务
(•) Interactive - 在关键决策时询问确认
( ) Report-only - 仅提供分析，不做更改

触发条件（可选）：
[ ] 在文件更改时运行，匹配：*.api.ts
[ ] 在 git commit 时运行
[ ] 按计划运行

保存 agent 到：.claude/agents/api-designer.json

创建 agent？（y/n）

User: y

Claude Code: ✓ 自定义 agent 已创建！

Agent：api-designer
位置：.claude/agents/api-designer.json

使用以下命令启动：
/agents api-designer

或在命令中使用：
Claude，使用 api-designer agent 创建用户 endpoint
```

## 内置 Agents

### 1. Code Reviewer Agent

```
User: /agents code-reviewer

Agent 专业领域：
- 识别 bugs 和代码异味
- 检查安全漏洞
- 建议性能改进
- 执行编码标准
- 审查测试覆盖率

配置：
{
  "name": "code-reviewer",
  "focus": ["security", "performance", "quality"],
  "severity_threshold": "medium",
  "auto_fix": false
}
```

### 2. Test Writer Agent

```
User: /agents test-writer

Agent 专业领域：
- 生成单元测试
- 创建集成测试
- 编写测试用例
- 确保覆盖率
- 遵循测试最佳实践

示例：

User: /agents test-writer --file src/utils/calculator.ts

Agent 报告：
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

已分析：src/utils/calculator.ts
发现函数：4（add、subtract、multiply、divide）

生成的测试：
✓ calculator.test.ts 已创建
✓ 编写了12个测试用例
✓ 覆盖了边缘情况
✓ 覆盖率：100%

测试：
- 基本操作（4个测试）
- 边缘情况（4个测试）
- 错误处理（4个测试）

运行测试：
npm test calculator.test.ts
```

### 3. Doc Generator Agent

```
User: /agents doc-generator

Agent 专业领域：
- 创建 JSDoc 注释
- 生成 README 文件
- 编写 API 文档
- 创建使用示例
- 维护文档一致性

示例：

User: /agents doc-generator --type api

Agent：正在生成 API 文档...

✓ 扫描了23个 API endpoints
✓ 生成了 OpenAPI 3.0 spec
✓ 创建了带示例的 API.md
✓ 为45个函数添加了 JSDoc 注释

已创建文件：
- docs/API.md（完整 API 参考）
- openapi.yaml（OpenAPI 规范）
- docs/examples/（使用示例）
```

### 4. Bug Hunter Agent

```
User: /agents bug-hunter

Agent 专业领域：
- 查找潜在 bugs
- 分析错误模式
- 追踪执行路径
- 识别边缘情况
- 建议修复

示例：

User: 我的应用程序随机崩溃

User: /agents bug-hunter

Agent：正在分析代码库以查找潜在 bugs...

发现5个潜在问题：
1. 数据获取中的竞态条件（高）
2. 空指针解引用（高）
3. 循环中的差一错误（中）
4. 缺少 error boundary（中）
5. 未处理的 promise rejection（低）

最可能导致崩溃的原因：
→ 问题#1：UserContext.tsx 中的竞态条件

详细分析：
[显示代码，解释问题，建议修复]
```

### 5. Refactorer Agent

```
User: /agents refactorer

Agent 专业领域：
- 识别代码重复
- 建议设计模式
- 改进代码结构
- 提取可重用组件
- 现代化遗留代码

示例：

User: /agents refactorer --focus duplication

Agent：正在扫描代码重复...

发现8处重复代码：

1. 错误处理（3个文件，45行）
   建议：提取到 errorHandler 工具
   影响：-35行，+1个可重用函数

2. API 调用（5个文件，120行）
   建议：创建 apiClient service
   影响：-80行，+1个 service 类

3. 表单验证（4个文件，67行）
   建议：使用验证库（Zod）
   影响：-50行，+类型安全

总潜在减少：165行

继续重构？（y/n）
```

### 6. Security Audit Agent

```
User: /agents security-audit

Agent 专业领域：
- 扫描漏洞
- 检查依赖项安全性
- 审查认证/授权
- 识别数据泄露风险
- 检查常见漏洞

示例：

User: /agents security-audit

Agent：正在运行安全审计...

安全评估：
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

严重问题：2
高优先级：5
中优先级：8
低优先级：12

严重问题：
1. 登录 endpoint 中的 SQL Injection
   文件：src/api/auth.ts:34
   风险：数据库泄露

2. 代码中的硬编码 API keys
   文件：src/config/keys.ts:12
   风险：repository 中的 key 泄露

建议：
- 将 secrets 移至环境变量
- 使用参数化查询
- 启用 HTTPS
- 添加速率限制
- 实施 CSRF 保护

生成安全报告？（y/n）
```

## 自定义 Agent 示例

### 示例1：API Designer Agent

```
.claude/agents/api-designer.json:

{
  "name": "api-designer",
  "description": "设计 REST API endpoints",
  "specialization": "REST API 设计、OpenAPI specs、HTTP 语义",
  "tools": ["Read", "Write", "Grep"],
  "behavior": "interactive",
  "prompt": "您是 API 设计专家。根据需求设计遵循最佳实践的 RESTful endpoints：正确的 HTTP 方法、状态码、资源命名、分页、过滤、版本控制和错误处理。生成 OpenAPI 规范。"
}

用法：

User: /agents api-designer

Claude Code: 正在启动 api-designer agent...

User: 设计一个具有 CRUD 操作的 posts API

Agent：正在设计 posts API...

Endpoints：
GET    /api/v1/posts           （列出 posts，分页）
GET    /api/v1/posts/:id       （获取单个 post）
POST   /api/v1/posts           （创建 post）
PUT    /api/v1/posts/:id       （更新 post）
DELETE /api/v1/posts/:id       （删除 post）
GET    /api/v1/posts/:id/comments （列出 comments）

功能：
✓ 分页（page、limit）
✓ 过滤（status、author）
✓ 排序（createdAt、title）
✓ 字段选择（fields 参数）
✓ 速率限制 headers
✓ HATEOAS links

已创建文件：
- api/posts.routes.ts（Express routes）
- api/posts.controller.ts（Controllers）
- docs/posts-api.md（文档）
- openapi-posts.yaml（OpenAPI spec）
```

### 示例2：DB Optimizer Agent

```
.claude/agents/db-optimizer.json:

{
  "name": "db-optimizer",
  "description": "优化数据库查询和 schema",
  "specialization": "SQL 优化、索引、查询分析",
  "tools": ["Read", "Grep", "Bash"],
  "behavior": "report-only"
}

用法：

User: /agents db-optimizer

Agent：正在分析数据库查询...

发现15个要优化的查询：

1. getUserPosts 查询（users.service.ts:45）
   当前：N+1 查询（慢）
   优化后：JOIN 查询（快10倍）

   之前：
   SELECT * FROM users WHERE id = ?
   [对每个用户：SELECT * FROM posts WHERE user_id = ?]

   之后：
   SELECT u.*, p.* FROM users u
   LEFT JOIN posts p ON u.id = p.user_id
   WHERE u.id = ?

2. 搜索查询（search.service.ts:67）
   问题：全表扫描
   修复：在（title、content）上添加索引

   CREATE INDEX idx_posts_search ON posts(title, content);

性能改进：
- 查询1：450ms → 45ms（快90%）
- 查询2：2.3s → 0.1s（快95%）

应用优化？（y/n）
```

### 示例3：Deployment Agent

```
.claude/agents/deployer.json:

{
  "name": "deployer",
  "description": "处理部署任务",
  "specialization": "CI/CD、Docker、部署 workflows",
  "tools": ["Read", "Write", "Bash"],
  "behavior": "autonomous"
}

用法：

User: /agents deployer --env production

Agent：部署检查清单
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

部署前检查：
✓ 所有测试通过
✓ 代码审查已批准
✓ 无安全漏洞
✓ 环境变量已设置
✓ 数据库迁移准备就绪
✓ 回滚计划已准备

开始部署...

步骤：
1. 构建 Docker image... ✓
2. 在容器中运行测试... ✓
3. 推送到 registry... ✓
4. 更新 Kubernetes manifests... ✓
5. 应用部署... ✓
6. 等待 rollout... ✓
7. 运行冒烟测试... ✓

部署成功！

应用 URL：https://myapp.com
版本：v2.3.1
回滚：kubectl rollout undo deployment/myapp
```

## 并行运行多个 Agents

```
User: 并行运行代码审查、测试和安全审计

Claude Code: 正在并行启动3个 agents...

┌─────────────────┬─────────────┬──────────────────┐
│ Agent           │ 状态        │ 进度             │
├─────────────────┼─────────────┼──────────────────┤
│ code-reviewer   │ 运行中      │ ████████░░ 80%  │
│ test-writer     │ 运行中      │ ██████░░░░ 60%  │
│ security-audit  │ 已完成      │ ██████████ 100% │
└─────────────────┴─────────────┴──────────────────┘

[所有 agents 完成]

综合报告：
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

代码审查：
- 发现8个问题（3个高优先级）
- 建议：12

测试：
- 编写了45个新测试
- 覆盖率：87% → 94%

安全性：
- 2个严重漏洞
- 7个中等问题

需要采取的行动：
1. 修复2个严重安全问题（阻塞）
2. 解决3个高优先级代码问题
3. 审查并运行新测试

继续修复？（y/n）
```

## Agent 配置

### 配置 Agent 行为

```
User: /agents config code-reviewer

Claude Code: 配置 code-reviewer Agent
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

当前设置：

关注领域：
[✓] Security
[✓] Performance
[✓] Code quality
[ ] Accessibility
[✓] Best practices

严重性阈值：
( ) 所有问题
(•) 中等及以上
( ) 仅高
( ) 仅严重

自动修复：
(•) 修复前询问
( ) 自动修复
( ) 从不修复（仅报告）

代码风格：
[✓] 遵循 ESLint config
[✓] 遵循 Prettier config
[✓] 检查 TypeScript 类型

最多审查文件数：
当前：50个文件
新：[___]

[保存] [取消]
```

### 查看 Agent 历史记录

```
User: /agents history

Claude Code: Agent 执行历史记录
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

最近的 agent 运行：

2025-01-08 14:30 | code-reviewer    | ✓ 成功 | 8个问题
2025-01-08 14:15 | test-writer      | ✓ 成功 | 45个测试
2025-01-08 14:10 | security-audit   | ⚠ 警告 | 2个严重
2025-01-08 13:45 | doc-generator    | ✓ 成功 | 5个文件
2025-01-08 13:20 | refactorer       | ✓ 成功 | 165行

过滤条件：
[1] Agent 名称
[2] 日期范围
[3] 状态
[4] 查看详情

选择选项或按 Enter 查看全部：

User: 3

Agent 运行：security-audit（2025-01-08 14:10）
持续时间：2分34秒
状态：完成但有警告

详情：
- 扫描文件：89
- 发现问题：9
- 严重：2
- 高：0
- 中：7

问题：
1. SQL injection（auth.ts:34）
   状态：已修复

2. 代码中的 API keys（config.ts:12）
   状态：未修复（需要手动操作）

完整报告：.claude/reports/security-audit-20250108.md
```

## Agent Templates

### 从 Template 创建 Agent

```
User: /agents create --from-template

Claude Code: Agent Templates
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

可用 templates：

[1] Code Quality Checker
    - 审查代码风格
    - 检查复杂度
    - 建议重构

[2] Test Generator
    - 编写单元测试
    - 创建测试 fixtures
    - 确保覆盖率

[3] Documentation Writer
    - 生成文档
    - 创建示例
    - 维护 README

[4] Security Scanner
    - 查找漏洞
    - 检查依赖项
    - 审查认证/授权

[5] Performance Analyzer
    - 识别瓶颈
    - 建议优化
    - benchmark 代码

[6] Blank Template
    - 从头开始

选择 template（1-6）：

User: 1

Claude Code: 自定义 Code Quality Checker

名称：code-quality-checker

关注：
[✓] Cyclomatic complexity
[✓] 代码重复
[✓] 函数长度
[✓] 命名约定
[ ] 注释质量

阈值：
- 最大复杂度：10
- 最大函数长度：50行
- 重复容忍度：3%

保存 agent？（y/n）

User: y

Agent 已创建：code-quality-checker
```

## 故障排除

### Agent 失败

```
User: /agents code-reviewer

Agent：开始代码审查...

错误：Agent 在30秒后失败

原因：超时（文件太多）

解决方案：
[1] 增加超时：/agents config --timeout 300
[2] 减少范围：/agents code-reviewer --files src/
[3] 分成更小的任务
[4] 查看日志：.claude/logs/agent-error.log

User: 2

User: /agents code-reviewer --files src/auth/

Agent：仅审查 src/auth/...
✓ 成功（审查了5个文件）
```

### 找不到 Agent

```
User: /agents my-custom-agent

错误：未找到 Agent 'my-custom-agent'

可用 agents：
- 内置：code-reviewer、test-writer、doc-generator
- 自定义：api-designer、db-optimizer

您是否想要：
[1] api-designer
[2] 创建新 agent 'my-custom-agent'

User: 2

[启动 agent 创建向导]
```

## 最佳实践

### 1. 对重复性任务使用 Agents

```
而不是：
User: 审查这段代码
User: 编写测试
User: 生成文档

使用 agents：
User: /agents code-reviewer
User: /agents test-writer
User: /agents doc-generator

或并行：
User: 并行运行 code-reviewer、test-writer 和 doc-generator
```

### 2. 创建项目特定的 Agents

```
针对您项目的需求：
.claude/agents/
├── api-reviewer.json      （审查 API endpoints）
├── schema-validator.json  （验证 GraphQL schemas）
└── changelog-generator.json（生成 changelogs）
```

### 3. 为您的工作流配置

```
设置适当的：
- Behavior（autonomous vs interactive）
- Tools（所需的最少工具）
- Triggers（何时自动运行）
- Thresholds（严重性级别）
```

## 相关命令

- `/hooks` - 自动化 agent 触发器
- `/bashes` - 监控 agent 后台任务
- `/todos` - 跟踪 agent 建议
- `/review` - 快速代码审查（使用 code-reviewer agent）

## 提示

- 在创建自定义 agents 之前先使用内置 agents
- 使用并行 agents 进行综合分析
- 为项目的特定需求配置 agents
- 在应用更改之前仔细审查 agent 报告
- 为重复性项目任务创建自定义 agents
- 使用 agent 历史记录跟踪随时间的改进
- 设置 hooks 以自动触发 agents

## 常见问题

**Q：agents 会使用额外的 API tokens 吗？**
A：是的，agents 独立运行并消耗 tokens。使用 `/cost` 监控。

**Q：agents 可以在不询问的情况下修改代码吗？**
A：取决于配置。将 behavior 设置为 "interactive" 以获得确认。

**Q：可以并行运行多少个 agents？**
A：最多同时5个 agents（可在 `/config` 中配置）。

**Q：我可以与团队共享自定义 agents 吗？**
A：可以，将 `.claude/agents/*.json` 文件 commit 到您的 repository。

**Q：agents 可以访问所有文件吗？**
A：它们遵守您的 `/permissions` 设置。

**Q：我可以停止正在运行的 agent 吗？**
A：可以，使用 Ctrl+C 或通过 `/bashes` kill 进程。
