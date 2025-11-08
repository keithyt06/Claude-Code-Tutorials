# `/memory` 命令示例

## 概述
`/memory` 命令允许您编辑 CLAUDE.md 文件，该文件包含 Claude 在所有对话中应记住的项目特定 context 和指令。

## 何时使用
- 添加项目特定约定
- 记录架构决策
- 记录代码风格偏好
- 记录 Claude 应始终记住的重要 context
- 随项目演进更新指南

## 示例用法

### 基本 Memory 管理

```
User: /memory

Claude Code: 正在打开 CLAUDE.md 进行编辑...

[编辑器打开当前 CLAUDE.md 内容]
[用户进行更改]
[用户保存]

Claude Code: Memory 已更新。我将在后续操作中应用这些指南。
```

## 在 Memory 中存储什么

### 1. 编码约定

```markdown
## 编码标准

### TypeScript
- 始终使用 strict mode
- 没有显式注释不使用 'any' 类型
- 对象形状优先使用 interfaces
- 字面类型使用 const assertions

### React
- 仅使用函数组件
- Hooks 用于所有状态管理
- Props interface 必须导出
- 每个文件一个组件
```

### 2. 项目架构

```markdown
## 架构决策

- **状态管理**：Zustand（不是 Redux）
- **样式**：Tailwind CSS 配合自定义设计 tokens
- **API**：tRPC 用于类型安全 API
- **数据库**：Prisma 配合 PostgreSQL
- **认证**：NextAuth.js 配合 JWT 策略
```

### 3. 文件组织

```markdown
## 文件结构

components/
├── ui/           # Shadcn UI 组件
├── features/     # 功能特定组件
└── layouts/      # 布局组件

lib/
├── api/          # API client 函数
├── utils/        # 工具函数
└── hooks/        # 自定义 React hooks
```

### 4. 测试偏好

```markdown
## 测试

- Jest + React Testing Library
- 最低 80% 覆盖率
- 测试文件：源文件旁的 `*.test.tsx`
- 在测试中 mock 外部 API
- 使用 `data-testid` 作为测试选择器
```

## 实际示例

### 示例 1：添加 API 约定

```
User: /memory

[添加到 CLAUDE.md：]
```markdown
## API 约定

### Endpoint 结构
- GET /api/[resource] - 列表
- GET /api/[resource]/[id] - 单个项目
- POST /api/[resource] - 创建
- PUT /api/[resource]/[id] - 更新
- DELETE /api/[resource]/[id] - 删除

### 响应格式
```typescript
{
  success: boolean;
  data?: T;
  error?: { message: string; code: string };
  meta?: { total: number; page: number };
}
```

现在当 Claude 创建 API endpoints 时，会自动遵循此模式。
```

### 示例 2：记录设计决策

```
User: /memory

[添加：]
```markdown
## 设计决策

### 为什么用 Monorepo？
我们使用 monorepo 在 web、mobile 和 backend 之间共享代码。
每个包都是独立的，但可以从 `shared/` 导入。

### 为什么不用 Redux？
我们选择 Zustand 因为：
- 更简单的 API
- 更少的样板代码
- 更好的 TypeScript 支持
- 更容易测试
```

### 示例 3：记录注意事项

```
User: /memory

[添加：]
```markdown
## 重要说明

### 数据库迁移
- 永远不要编辑现有迁移
- 始终为 schema 更改创建新迁移
- 先在预发布环境测试迁移

### 环境变量
- 所有公共变量必须以 NEXT_PUBLIC_ 开头
- 永远不要 commit .env 文件
- 使用 .env.example 作为模板

### 性能
- 图片必须使用 next/image
- 延迟加载折叠下方的组件
- 防抖搜索输入（300ms）
```

## Memory 最佳实践

### 保持可操作性

```
不好：
"编写好的代码"

好：
"使用描述性变量名（getUserById，而不是 gd）"
```

### 具体明确

```
不好：
"遵循 React 最佳实践"

好：
"对昂贵渲染使用 React.memo，对计算值使用 useMemo，对传递给子组件的事件处理器使用 useCallback"
```

### 包含示例

```markdown
## 组件模式

```typescript
// ✅ 好
export default function UserCard({ user }: UserCardProps) {
  return (
    <Card>
      <CardHeader>{user.name}</CardHeader>
      <CardContent>{user.email}</CardContent>
    </Card>
  );
}

// ❌ 不好
export default function UserCard(props: any) {
  return <div>{props.user.name}</div>;
}
```

## 示例：完整 Memory 文件

```markdown
# Claude Code 项目 Memory

## 项目：TaskMaster Pro
使用 Next.js 14 构建的项目管理 SaaS 应用。

## 技术栈
- Next.js 14 (App Router)
- TypeScript (strict mode)
- Tailwind CSS + Shadcn UI
- Prisma + PostgreSQL
- NextAuth.js
- Zustand 状态管理

## 编码约定

### TypeScript
- 始终使用 strict mode
- Props 使用 interfaces，unions 使用 types
- 无隐式 any
- 导出所有 prop interfaces

### React
- 仅函数组件
- Hooks 状态管理
- 默认使用 Server Components
- 仅在必要时使用 'use client'

### 样式
- Tailwind 工具类
- components/ui/ 中的自定义组件
- 需要暗色模式支持
- 移动优先响应式设计

## 文件结构
```
app/
  (auth)/           # 认证页面
  (dashboard)/      # 受保护页面
  api/              # API routes
components/
  ui/               # Shadcn 组件
  features/         # 功能组件
lib/
  db.ts             # Prisma client
  auth.ts           # NextAuth 配置
  utils.ts          # 辅助函数
```

## API 约定
- tRPC 用于类型安全 API
- Server Actions 用于变更
- try/catch 错误处理
- 返回类型化响应

## 测试
- Vitest + React Testing Library
- 测试就近：*.test.tsx
- 最低 80% 覆盖率
- Mock API 调用

## Git 工作流
- 分支：feature/description
- Commits: Conventional Commits 格式
- 需要 PR 模板
- Squash merge 到 main

## 重要说明
- 永远不要暴露 API keys
- 始终验证用户输入
- 使用 Zod 进行 schema 验证
- Cache 昂贵的操作
- 错误记录到 Sentry

## 偏好
- 我偏好函数式编程风格
- 保持函数小（< 20 行）
- 单一职责原则
- DRY 但不以牺牲清晰度为代价
```

## 开发期间更新 Memory

```
User: 我们决定从 REST 切换到 GraphQL

User: /memory

[更新：]
```markdown
## API 层
~~- REST API with fetch~~
- GraphQL with Apollo Client
- graphql/ 文件夹中的查询
- 从 schema 生成的类型
```

User: 另外，添加我们正在使用 Codegen

[更新：]
```markdown
- GraphQL Code Generator 用于类型安全
- Schema 更改后运行 `npm run codegen`
```

## Memory 生命周期

### 初始设置
```
1. 创建项目
2. /init (创建基本 CLAUDE.md)
3. /memory (为项目自定义)
```

### 持续更新
```
做出架构决策时：
User: /memory
[记录决策]

建立新模式时：
User: /memory
[将模式添加到约定]

遇到常见问题时：
User: /memory
[在"注意事项"部分记录解决方案]
```

### 团队协作
```
- 在版本控制中共享 CLAUDE.md
- 团队成员随项目演进更新
- 在代码审查中审查更改
- 保持简洁但全面
```

## 提示
- 发现自己重复指令时更新 memory
- 包含决策背后的"为什么"，而不仅仅是"是什么"
- 链接到外部文档以获取详细信息
- 定期审查和修剪
- 使用 markdown 格式提高可读性
- 包含代码示例以提高清晰度

## 相关命令
- `/init` - 创建初始 CLAUDE.md
- `/config` - 查看当前设置
- `/context` - 查看 memory 是否影响 context 使用
