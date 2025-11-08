# `/hooks` 命令示例

## 概述
`/hooks` 命令允许您管理 hook 配置，这些配置可以在 Claude Code 中响应特定事件（如文件更改、工具调用或 git 操作）自动执行 shell 命令。

## 何时使用
- 在文件更改时自动化 workflows
- 自动运行 linters/formatters
- 在代码修改后触发构建
- 在 git commits 前验证更改
- 与外部工具集成
- 创建自定义自动化 pipelines

## 示例用法

### 场景1：查看当前 Hooks

```
User: /hooks

Claude Code: Hooks 配置
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

活动 Hooks：

post-file-write:
├─ Script: .claude/hooks/format-on-save.sh
├─ Action: 在保存文件时运行 Prettier
└─ Status: Enabled ✓

pre-tool-use:
├─ Script: .claude/hooks/check-permissions.sh
├─ Action: 在工具使用前验证权限
└─ Status: Enabled ✓

未配置其他 hooks。

可用的 hook 类型：
- pre-tool-use（在任何工具执行之前）
- post-tool-use（在任何工具执行之后）
- post-file-write（在文件写入后）
- post-file-edit（在文件编辑后）
- pre-bash（在 bash 命令之前）
- post-bash（在 bash 命令之后）
- user-prompt-submit（当用户提交消息时）

选项：
[1] 创建新 hook
[2] 编辑现有 hook
[3] 禁用/启用 hook
[4] 删除 hook
[5] 测试 hook

选择选项（1-5）：
```

### 场景2：创建 Hook

```
User: /hooks create

Claude Code: 创建新 Hook
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

Hook 类型：
[1] pre-tool-use       （工具执行前）
[2] post-tool-use      （工具执行后）
[3] post-file-write    （文件写入后）
[4] post-file-edit     （文件编辑后）
[5] pre-bash           （bash 命令前）
[6] post-bash          （bash 命令后）
[7] user-prompt-submit （用户消息时）

选择类型（1-7）：

User: 3

Claude Code: 创建 post-file-write Hook

名称：lint-on-save

操作（shell 命令或脚本路径）：
User: eslint $FILE --fix

描述：
User: 在文件保存时自动修复 ESLint 错误

文件模式（可选，例如 "*.ts"）：
User: *.{ts,tsx,js,jsx}

条件：
[ ] 仅在 git repositories 中运行
[✓] 仅对特定文件模式运行
[ ] 仅在特定目录中运行
[ ] 运行前需要确认

预览：
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Hook: post-file-write
名称：lint-on-save
命令：eslint $FILE --fix
模式：*.{ts,tsx,js,jsx}
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

创建 hook？（y/n）

User: y

Claude Code: ✓ Hook 已创建！

位置：.claude/hooks/post-file-write-lint-on-save.sh

Hook 现在将在以下情况自动运行：
- 任何 .ts、.tsx、.js 或 .jsx 文件被写入时
- ESLint 将自动修复问题

测试 hook：
/hooks test lint-on-save
```

### 场景3：Hook 实际应用

```
User: 修复 login.ts 中的身份验证 bug

Claude Code: [分析并修复 bug]

正在将更改写入 login.ts...

[Hook 触发：post-file-write]
运行 hook：lint-on-save
命令：eslint login.ts --fix

Hook 输出：
✓ login.ts 已修复（自动纠正了3个问题）
  - 删除了未使用的 imports
  - 修复了缩进
  - 添加了缺失的分号

✓ 文件已保存：src/auth/login.ts

更改已应用并格式化！
```

## 常见 Hook 类型

### 1. Post-File-Write Hook（保存时格式化）

```
.claude/hooks/post-file-write-format.sh:

#!/bin/bash
FILE=$1

# 在保存的文件上运行 Prettier
if [[ $FILE =~ \.(ts|tsx|js|jsx)$ ]]; then
    prettier --write "$FILE"
    echo "✓ 已格式化 $FILE"
fi

用法：

User: 更新 UserForm 组件

Claude Code: [进行更改]

正在写入 src/components/UserForm.tsx...

[Hook 触发]
运行：prettier --write src/components/UserForm.tsx
✓ 已格式化 src/components/UserForm.tsx

完成！
```

### 2. Pre-Bash Hook（命令验证）

```
.claude/hooks/pre-bash-validate.sh:

#!/bin/bash
COMMAND=$1

# 防止危险命令
if [[ $COMMAND =~ rm\ -rf\ / ]]; then
    echo "❌ 已阻止：检测到危险命令"
    exit 1
fi

# 对 sudo 使用发出警告
if [[ $COMMAND =~ ^sudo ]]; then
    echo "⚠️  警告：命令需要 sudo 权限"
    read -p "继续？（y/n）" -n 1 -r
    echo
    if [[ ! $REPLY =~ ^[Yy]$ ]]; then
        exit 1
    fi
fi

exit 0

用法：

User: 运行 rm -rf /tmp/*

Claude Code: [Hook 拦截]

Pre-bash hook：validate
命令：rm -rf /tmp/*

✓ 验证通过
执行：rm -rf /tmp/*
```

### 3. Post-File-Edit Hook（运行测试）

```
.claude/hooks/post-file-edit-test.sh:

#!/bin/bash
FILE=$1

# 如果编辑了测试文件，运行测试
if [[ $FILE =~ \.test\.(ts|js)$ ]]; then
    echo "正在为 $FILE 运行测试..."
    npm test "$FILE"
fi

# 如果编辑了源文件，运行相关测试
if [[ $FILE =~ src/.*\.(ts|js)$ ]] && [[ ! $FILE =~ \.test\. ]]; then
    TEST_FILE="${FILE%.ts}.test.ts"
    if [ -f "$TEST_FILE" ]; then
        echo "正在运行相关测试：$TEST_FILE"
        npm test "$TEST_FILE"
    fi
fi

用法：

User: 更新 calculateTotal 函数

Claude Code: [编辑 src/utils/calculator.ts]

[Hook 触发]
正在运行相关测试：src/utils/calculator.test.ts

测试结果：
✓ calculateTotal 正确相加
✓ calculateTotal 处理空数组
✓ calculateTotal 处理负数

所有测试通过！
```

### 4. User-Prompt-Submit Hook（上下文检查）

```
.claude/hooks/user-prompt-submit-check.sh:

#!/bin/bash
PROMPT=$1

# 检查提示是否太长
WORD_COUNT=$(echo "$PROMPT" | wc -w)
if [ $WORD_COUNT -gt 500 ]; then
    echo "⚠️  警告：提示过长（$WORD_COUNT 个词）"
    echo "考虑使用 /compact 减少上下文"
fi

# 提醒敏感数据
if [[ $PROMPT =~ (password|secret|key|token) ]]; then
    echo "⚠️  警告：提示可能包含敏感数据"
    echo "确保不共享真实凭据"
fi

用法：

User: 帮我调试这个。API password 是 abc123 并且...

[Hook 触发]
⚠️  警告：提示可能包含敏感数据
确保不共享真实凭据

继续？（y/n）
```

### 5. Post-Bash Hook（完成通知）

```
.claude/hooks/post-bash-notify.sh:

#!/bin/bash
COMMAND=$1
EXIT_CODE=$2
DURATION=$3

# 如果命令耗时 > 10 秒则通知
if [ $DURATION -gt 10 ]; then
    ICON="✓"
    MESSAGE="命令已完成"

    if [ $EXIT_CODE -ne 0 ]; then
        ICON="✗"
        MESSAGE="命令失败"
    fi

    # macOS 通知
    osascript -e "display notification \"$COMMAND\" with title \"$MESSAGE\" sound name \"Glass\""

    echo "$ICON $MESSAGE (${DURATION}s)"
fi

用法：

User: 运行完整测试套件

Claude Code: 运行：npm test

[测试运行45秒]

[Hook 触发]
✓ 命令已完成（45s）
[出现桌面通知]
```

## Hook 配置

### 启用/禁用 Hooks

```
User: /hooks disable lint-on-save

Claude Code: Hook 'lint-on-save' 已禁用。

Hook 仍然存在，但不会自动运行。

重新启用：
/hooks enable lint-on-save

User: /hooks enable lint-on-save

Claude Code: ✓ Hook 'lint-on-save' 已启用。
```

### 编辑 Hook

```
User: /hooks edit lint-on-save

Claude Code: 编辑 Hook：lint-on-save
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

当前配置：
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
#!/bin/bash
FILE=$1
eslint "$FILE" --fix
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

选项：
[1] 在 $EDITOR 中编辑脚本
[2] 内联更改命令
[3] 修改文件模式
[4] 更改条件
[5] 取消

User: 2

新命令：
User: eslint "$FILE" --fix && prettier --write "$FILE"

Claude Code: ✓ Hook 已更新！

现在运行：保存时 ESLint + Prettier
```

### 测试 Hook

```
User: /hooks test lint-on-save

Claude Code: 测试 Hook：lint-on-save
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

选择测试文件：
[1] 使用现有文件
[2] 创建临时测试文件

User: 2

Claude Code: 创建测试文件：/tmp/test-hook.ts

内容：
const x=1;const y=2;const z=x+y;console.log(z)

运行 hook...

Hook 输出：
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
✓ /tmp/test-hook.ts 已修复
  - 在运算符周围添加空格
  - 添加分号
  - 格式化代码
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

结果：
const x = 1;
const y = 2;
const z = x + y;
console.log(z);

✓ Hook 执行成功！
```

## 高级 Hook 模式

### 条件执行

```
.claude/hooks/post-file-write-conditional.sh:

#!/bin/bash
FILE=$1

# 仅在 git repositories 中运行
if ! git rev-parse --git-dir > /dev/null 2>&1; then
    exit 0
fi

# 仅对暂存文件运行
if git diff --cached --name-only | grep -q "$FILE"; then
    echo "正在对 $FILE 运行 pre-commit 检查"
    npm run lint-staged "$FILE"
fi

# 仅在工作时间运行（上午9点 - 下午6点）
HOUR=$(date +%H)
if [ $HOUR -ge 9 ] && [ $HOUR -lt 18 ]; then
    echo "运行仅工作时间 hook"
    ./scripts/notify-team.sh "$FILE updated"
fi
```

### 链接多个命令

```
.claude/hooks/post-file-write-pipeline.sh:

#!/bin/bash
FILE=$1

echo "正在为 $FILE 运行文件处理 pipeline"

# 步骤1：格式化
prettier --write "$FILE" || exit 1
echo "✓ 已格式化"

# 步骤2：Lint
eslint "$FILE" --fix || exit 1
echo "✓ 已 Lint"

# 步骤3：类型检查
tsc --noEmit "$FILE" || exit 1
echo "✓ 类型检查完成"

# 步骤4：运行测试
if [[ $FILE =~ src/.*\.ts$ ]]; then
    TEST_FILE="${FILE%.ts}.test.ts"
    if [ -f "$TEST_FILE" ]; then
        npm test "$TEST_FILE" || exit 1
        echo "✓ 测试通过"
    fi
fi

echo "✓ Pipeline 完成！"
```

### 异步 Hooks（后台任务）

```
.claude/hooks/post-file-write-async.sh:

#!/bin/bash
FILE=$1

# 在后台运行以不阻塞 Claude Code
(
    # 重量级操作：重建
    echo "正在后台构建项目..."
    npm run build > /tmp/build.log 2>&1

    if [ $? -eq 0 ]; then
        echo "✓ 构建成功"
    else
        echo "✗ 构建失败。查看 /tmp/build.log"
    fi
) &

echo "构建已在后台启动（PID：$!）"
```

## Hook 管理

### 列出所有 Hooks

```
User: /hooks list

Claude Code: 所有 Hooks
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

Post-File-Write Hooks：
✓ format-on-save         （Prettier 格式化）
✓ lint-on-save           （ESLint 自动修复）
✓ run-tests              （自动运行测试）

Pre-Bash Hooks：
✓ validate-command       （防止危险命令）

Post-Bash Hooks：
✓ notify-completion      （桌面通知）

User-Prompt-Submit Hooks：
✓ check-sensitive-data   （警告 secrets）

总计：6个 hooks（全部启用）
```

### 导出/导入 Hooks

```
User: /hooks export

Claude Code: 导出 Hooks
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

导出位置：
/Users/dev/project/.claude/hooks-backup.tar.gz

包含：
- 所有 hook 脚本
- 配置文件
- 带设置说明的 README

✓ Hooks 已导出！

与团队共享：
git add .claude/hooks-backup.tar.gz
git commit -m "Add Claude Code hooks"

User: /hooks import ~/Downloads/hooks-backup.tar.gz

Claude Code: 导入 Hooks
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

发现 hooks：
- format-on-save
- lint-on-save
- run-tests
- validate-command

导入全部？（y/n）

User: y

✓ 已导入4个 hooks
✓ 脚本已设为可执行
✓ 配置已应用
```

### 删除 Hook

```
User: /hooks delete lint-on-save

Claude Code: 删除 Hook：lint-on-save
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

这将永久删除：
- 脚本：.claude/hooks/post-file-write-lint-on-save.sh
- 配置

删除？（y/n）

User: y

Claude Code: ✓ Hook 已删除

重新创建，使用：
/hooks create
```

## Hook 变量

### 可用变量

```
所有 hooks 通过环境变量接收上下文：

$FILE               - 文件路径（文件相关 hooks）
$TOOL              - 工具名称（工具相关 hooks）
$COMMAND           - Bash 命令（bash hooks）
$EXIT_CODE         - 退出代码（post-bash hooks）
$DURATION          - 持续时间（秒）
$CLAUDE_PROJECT    - 项目根目录
$CLAUDE_SESSION_ID - 当前会话 ID
$USER_PROMPT       - 用户消息（prompt-submit hooks）

示例用法：

#!/bin/bash
echo "工具：$TOOL"
echo "文件：$FILE"
echo "项目：$CLAUDE_PROJECT"
echo "持续时间：${DURATION}s"
```

## 故障排除

### Hook 未运行

```
User: /hooks debug lint-on-save

Claude Code: Hook 调试：lint-on-save
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

检查：
✓ Hook 存在
✓ 脚本可执行
✗ 文件模式匹配：否

问题：文件模式 "*.{ts,tsx}" 与当前文件 "config.json" 不匹配

解决方案：
1. 更新文件模式以包括 .json 文件
2. Hook 将仅对 .ts/.tsx 文件运行

最近运行：
- 无最近执行（模式不匹配）
```

### Hook 失败

```
User: 我的 format-on-save hook 一直失败

User: /hooks logs format-on-save

Claude Code: Hook 日志：format-on-save
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

最近执行：

2025-01-08 14:30:45 | ✗ 失败
文件：src/utils/helper.ts
命令：prettier --write src/utils/helper.ts
退出代码：1
错误：解析错误：意外 token
持续时间：0.3s

2025-01-08 14:25:12 | ✓ 成功
文件：src/components/Button.tsx
持续时间：0.5s

最后错误输出：
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
[error] src/utils/helper.ts: SyntaxError: Unexpected token (15:10)
  13 | function test() {
  14 |   return {
> 15 |     value:
  16 | }
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

问题：文件中的语法错误阻止格式化。
首先修复语法错误，然后 Prettier 将正常工作。
```

### 临时禁用

```
User: /hooks pause

Claude Code: 暂停所有 Hooks
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

本会话所有 hooks 临时禁用。

Hooks 将：
- 不自动执行
- 在下次 Claude Code 会话时恢复
- 可以使用以下命令重新启用：/hooks resume

已暂停：6个 hooks

User: [在没有 hooks 的情况下工作]

User: /hooks resume

Claude Code: ✓ 所有 hooks 已恢复
6个 hooks 现在处于活动状态
```

## 最佳实践

### 1. 保持 Hooks 快速

```
❌ 慢 hook：
npm run build  # 耗时2分钟

✓ 更好：
npm run lint   # 耗时2秒

✓ 或异步运行：
(npm run build &)  # 不阻塞
```

### 2. 优雅地处理错误

```
#!/bin/bash
FILE=$1

# 如果未安装 prettier 不要失败
if command -v prettier &> /dev/null; then
    prettier --write "$FILE" || echo "⚠️  Prettier 失败，继续"
else
    echo "ℹ️  未安装 Prettier，跳过格式化"
fi

exit 0  # 始终成功以不阻塞 Claude Code
```

### 3. 使用文件模式

```
✓ 具体：
模式：src/**/*.ts

✓ 多个：
模式：*.{ts,tsx,js,jsx}

❌ 太宽泛：
模式：*  （在所有文件上运行）
```

### 4. 提供反馈

```
#!/bin/bash
echo "🔍 正在运行安全扫描..."
bandit -r . > /tmp/security-report.txt
if [ $? -eq 0 ]; then
    echo "✓ 安全扫描通过"
else
    echo "⚠️  发现安全问题。查看 /tmp/security-report.txt"
fi
```

## 相关命令

- `/agents` - 对复杂任务使用 agents 而不是 hooks
- `/bashes` - 监控 hook 后台进程
- `/config` - 配置全局 hook 设置
- `/permissions` - 控制 hooks 可以访问的内容

## 提示

- 从简单 hooks 开始（format、lint）
- 启用前测试 hooks：`/hooks test`
- 使用文件模式限制范围
- 保持 hooks 快速（< 5秒）
- 在后台运行重量级任务
- 提供清晰的输出消息
- 优雅地处理错误（不阻塞）
- 通过 git 与团队共享 hooks

## 常见问题

**Q：hooks 在所有 terminals 中都有效吗？**
A：是的，hooks 是在您的 terminal 环境中运行的 shell 脚本。

**Q：hooks 可以修改文件吗？**
A：可以，如果它们有写权限。对自动修复 hooks 要小心。

**Q：如果 hook 失败会发生什么？**
A：取决于退出代码。退出1会阻塞操作，退出0会继续。

**Q：我可以在 hooks 中运行 Claude Code 命令吗？**
A：不可以，hooks 是 shell 脚本。使用它们调用外部工具（linters、tests 等）。

**Q：Claude Code 未运行时 hooks 会运行吗？**
A：不会，hooks 仅在 Claude Code 会话期间触发。

**Q：如何与团队共享 hooks？**
A：将 `.claude/hooks/` 目录 commit 到您的 repository。

**Q：hooks 可以访问环境变量吗？**
A：可以，hooks 在您的 shell 中运行并继承所有环境变量。
