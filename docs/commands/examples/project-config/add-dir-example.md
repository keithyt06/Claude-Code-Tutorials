# `/add-dir` 命令示例

## 概述
`/add-dir` 命令扩展 Claude Code 对项目中多个目录的访问权限，使其能够跨代码库的不同部分工作。

## 何时使用
- 使用 monorepo 结构
- 需要访问独立的 frontend/backend 目录
- 开发微服务架构
- 访问不同位置的共享库或实用程序

## 示例用法

### 场景：Monorepo 开发

```
User: I'm working on a monorepo with separate packages

User: /add-dir

Claude Code: Current working directory: /Users/dev/monorepo/packages/api

Add additional directory:
[目录选择器打开]

User: [选择 /Users/dev/monorepo/packages/web]

Claude Code: Added /Users/dev/monorepo/packages/web to working directories.

I now have access to both:
- /Users/dev/monorepo/packages/api
- /Users/dev/monorepo/packages/web

User: Great! Update the API endpoint in the backend and the corresponding fetch call in the frontend.

Claude Code: [跨两个目录进行协调更改]
```

### 场景：Frontend + Backend 分离

```
Initial directory: /Users/dev/myproject/backend

User: /add-dir
[添加 /Users/dev/myproject/frontend]

User: When I change this API response format, update the frontend types too.

Claude Code: I'll update:
- backend/src/api/users.ts (response format)
- frontend/src/types/user.ts (TypeScript types)
- frontend/src/api/userService.ts (API client)
```

## 常见的多目录设置

### 1. Monorepo 结构
```
/myproject
├── packages/
│   ├── api/        (working dir 1)
│   ├── web/        (working dir 2)
│   ├── mobile/     (working dir 3)
│   └── shared/     (working dir 4)
```

```
User: /add-dir
[根据需要添加每个 package 目录]
```

### 2. Frontend/Backend 分离
```
/myproject
├── backend/        (working dir 1)
├── frontend/       (working dir 2)
└── shared/         (working dir 3)
```

### 3. 微服务
```
/services
├── auth-service/       (working dir 1)
├── payment-service/    (working dir 2)
├── notification-service/ (working dir 3)
└── shared-lib/         (working dir 4)
```

## 优势

### 跨目录协调
```
User: Update the user schema in the backend and the corresponding GraphQL types in the frontend

Claude Code:
Updated backend/src/models/user.ts:
- Added 'phoneNumber' field

Updated frontend/src/graphql/types.ts:
- Added 'phoneNumber' to UserType
- Updated UserInput interface
```

### 一致性更改
```
User: Rename the 'getUserData' function across all services

Claude Code: Renamed in:
- api/src/services/userService.ts
- web/src/api/client.ts
- mobile/src/services/api.ts
- shared/src/types/api.ts
```

## 管理多个目录

### 查看当前目录
```
User: What directories do you have access to?

Claude Code: I have access to:
1. /Users/dev/project/backend (primary)
2. /Users/dev/project/frontend
3. /Users/dev/project/shared
```

### 删除目录
```
User: Remove access to the mobile directory

Claude Code: I'll focus on the backend and web directories only.
[注意：目前您需要重启才能删除目录]
```

## 最佳实践

### 1. 按需添加目录
不要一次性添加所有目录 - 在需要跨目录工作时再添加。

```
User: /add-dir
[仅添加当前任务相关的目录]
```

### 2. 将相关代码放在一起
添加需要频繁协调更改的目录：
```
- API + 对应的 frontend
- Service + 它的测试
- Core lib + 依赖的 package
```

### 3. 注意 Context
更多目录 = 需要考虑更多文件 = 更多 context 使用

```
User: /context
[检查添加更多目录是否会导致问题]
```

## 示例：完整工作流

```
# 从 backend 目录开始
Current: /Users/dev/app/backend

User: I need to implement a new feature that touches both backend and frontend

User: /add-dir
[添加 /Users/dev/app/frontend]

User: Add a new 'tags' field to blog posts:
1. Add to database schema
2. Update API endpoints
3. Update frontend form
4. Update display components

Claude Code:
I'll implement this across both directories:

Backend changes:
- backend/src/models/post.ts (add tags field)
- backend/src/api/posts.ts (update endpoints)
- backend/migrations/xxx-add-tags.ts (migration)

Frontend changes:
- frontend/src/types/post.ts (add tags type)
- frontend/src/components/PostForm.tsx (add tags input)
- frontend/src/components/PostCard.tsx (display tags)

[进行所有协调更改]
```

## 故障排除

### 权限问题
```
User: /add-dir
Claude Code: I don't have permission to access that directory.

Solution: Check with /permissions and grant necessary access
```

### 找不到目录
```
User: /add-dir
[目录未出现在选择器中]

Solution: Ensure directory exists and you have read permissions
```

## 提示
- 从一个目录开始，根据需要添加更多
- 用于跨代码库的协调更改
- 对于复杂的设置，考虑使用符号链接
- 记住更多目录会增加 context 大小

## 相关命令
- `/permissions` - 管理目录访问权限
- `/config` - 查看当前工作目录配置
- `/context` - 检查多个目录是否影响 context
