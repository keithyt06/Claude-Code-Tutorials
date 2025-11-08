# `/init` 命令示例

## 概述
`/init` 命令在您的项目中创建 CLAUDE.md 文件，包含使用 Claude Code 的最佳实践和指南。

## 何时使用
- 使用 Claude Code 开始新项目
- 希望向 Claude 提供项目特定 context
- 为 AI 辅助设置团队指南
- 记录项目约定和偏好

## 示例用法

### 基本初始化

```
User: /init

Claude Code: 我将为您的项目创建 CLAUDE.md 文件。

已创建：/Users/dev/myproject/CLAUDE.md

此文件将帮助我更好地理解您的项目。您可以自定义以下内容：
- 项目概览和目标
- 编码标准和约定
- 架构决策
- 首选工具和框架
- 测试要求

User: 很好！你能添加关于我们测试策略的信息吗？

Claude Code: 我将使用您的测试偏好更新 CLAUDE.md。
```

## 创建的内容

### CLAUDE.md 示例结构

```markdown
# Claude Code 项目指南

## 项目概览
[项目简要描述]

## 架构
[关键架构决策]

## 编码标准
- 语言：[例如，TypeScript]
- 风格指南：[例如，Airbnb, Standard]
- 格式化：[例如，Prettier 配置]

## 测试
- 框架：[例如，Jest, Vitest]
- 覆盖率要求：[例如，80%]
- 测试位置：[例如，__tests__ 文件夹]

## Git 工作流
- 分支命名：[例如，feature/, bugfix/]
- Commit 消息格式：[例如，Conventional Commits]

## 依赖
- 包管理器：[例如，npm, yarn, pnpm]
- Node 版本：[例如，18.x]

## 关键约定
[项目特定的模式和实践]
```

## 实际示例

### 示例 1：React + TypeScript 项目

```
User: /init

User: 使用我们的 React 项目约定更新 CLAUDE.md

Claude Code: 我将为您的 React 项目自定义它。

[更新 CLAUDE.md，包含：]
- TypeScript strict mode 要求
- React 18+ 最佳实践
- 组件结构（hooks, 函数组件）
- 状态管理（Redux Toolkit）
- 样式方法（Tailwind CSS）
- 使用 React Testing Library 测试
```

### 示例 2：Python API 项目

```
User: /init

User: 这是一个 FastAPI 项目。添加我们的 Python 约定。

Claude Code: 已更新 CLAUDE.md，包含：
- Python 3.11+ 要求
- FastAPI 最佳实践
- Type hints 要求
- SQLAlchemy ORM 模式
- Pytest 配置
- Docker 设置偏好
```

## 自定义示例

### 添加编码标准

```
User: 将我们的 TypeScript 约定添加到 CLAUDE.md

Claude Code: 我将添加：
```typescript
## TypeScript 约定
- 使用 strict mode
- 避免 'any' 类型
- 对象优先使用 interfaces 而非 types
- 适当使用 const assertions
- 利用 discriminated unions 处理复杂状态
```

### 添加架构决策

```
User: 在 CLAUDE.md 中记录我们的微服务架构

Claude Code: 已添加架构部分：
```markdown
## 架构
- 微服务模式
- 事件驱动通信（RabbitMQ）
- 每个服务有自己的数据库
- 外部访问的 API Gateway 模式
- 单独包中的共享类型
```

### 添加测试要求

```
User: 包含我们的测试要求

Claude Code: 已添加：
```markdown
## 测试要求
- 单元测试：所有业务逻辑
- 集成测试：所有 API endpoints
- E2E 测试：关键用户流程
- 最低覆盖率：80%
- Commit 前运行测试（pre-commit hook）
```

## CLAUDE.md 的好处

### 一致的行为
```
没有 CLAUDE.md：
User: 添加新组件

Claude Code: [使用通用 React 模式]

有 CLAUDE.md：
User: 添加新组件

Claude Code: [使用您的特定结构、样式和测试模式]
```

### 项目 Context
```
CLAUDE.md 包括：
- "我们使用 Zustand 进行状态管理"
- "API 调用放在 src/api/"
- "组件应该是默认导出"

Claude Code 自动遵循这些约定。
```

### 团队对齐
所有团队成员获得一致的 AI 辅助，遵循相同的指南。

## 示例：完整设置工作流

```
# 新项目设置
User: 我正在开始一个新的 Next.js 项目

User: /init

Claude Code: 已创建默认结构的 CLAUDE.md。

User: 为 Next.js 14 with App Router 更新它

Claude Code: 已更新 CLAUDE.md：
```markdown
## 框架
- Next.js 14 with App Router
- 默认使用 React Server Components
- 需要时使用 Client Components ('use client')

## 项目结构
- app/ - App Router 页面
- components/ - 共享组件
- lib/ - 工具和辅助函数
- public/ - 静态资源

## 约定
- 使用 Server Actions 进行变更
- 在 Server Components 中获取数据
- 使用 loading.tsx 和 error.tsx
- 使用 next/image 优化图片
```

User: 完美！现在当我让你创建组件时，你会遵循这些模式。
```

## 更新 CLAUDE.md

### 手动更新
```
User: /memory
[打开 CLAUDE.md 进行编辑]
[进行更改]
[保存]
```

### AI 辅助更新
```
User: 将我们的 ESLint 规则添加到 CLAUDE.md

Claude Code: 我将添加您的 ESLint 配置详情。
```

## 示例：多环境设置

```markdown
## 环境
- 开发环境：http://localhost:3000
- 预发布：https://staging.myapp.com
- 生产环境：https://myapp.com

## 环境变量
- NEXT_PUBLIC_API_URL
- DATABASE_URL
- AUTH_SECRET

## 部署
- Vercel 用于前端
- Railway 用于后端
- PRs 的自动预览部署
```

## 最佳实践

### 1. 从简单开始
```
User: /init
[从基本结构开始]
[随着项目增长添加详情]
```

### 2. 保持更新
```
当架构决策变化时：
User: 更新 CLAUDE.md - 我们从 REST 切换到 GraphQL
```

### 3. 具体明确
```
不要写："使用良好的命名"
而要写："变量使用 camelCase，组件使用 PascalCase"
```

### 4. 包含示例
```markdown
## 组件结构
```typescript
// 好的示例
export default function UserProfile({ userId }: Props) {
  const user = useUser(userId);
  return <div>{user.name}</div>;
}
```

## 提示
- 首先包含最重要的约定
- 引用外部文档（风格指南、架构文档）
- 随项目演进而更新
- 与团队成员分享以保持一致性
- 包含常见陷阱或注意事项

## 相关命令
- `/memory` - 直接编辑 CLAUDE.md
- `/config` - 查看当前配置
- `/permissions` - 管理文件访问
