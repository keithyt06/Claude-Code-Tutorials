# `/terminal-setup` 命令示例

## 概述
`/terminal-setup` 命令在支持的终端（iTerm2 和 VSCode）中安装 Shift+Enter 键绑定以输入换行符，允许您轻松插入多行输入而不发送消息。

## 何时使用
- Claude Code 的首次设置
- 编写多行 prompts 或代码
- 需要使用换行符格式化消息
- iTerm2 或 VSCode 集成终端用户
- 改进消息格式化工作流

## 支持的终端
- ✅ iTerm2 (macOS)
- ✅ VSCode 集成终端
- ⚠️ 其他终端：需要手动配置

## 示例用法

### 场景 1：初始设置 (iTerm2)

```
User: /terminal-setup

Claude Code: 终端设置向导
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

检测到的终端：iTerm2

当前键绑定：
- Enter: 发送消息
- Shift+Enter: [未配置]

此命令将配置：
✓ Shift+Enter → 插入换行符
✓ Enter → 发送消息（不变）

这允许您轻松编写多行 prompts。

继续设置？(y/n)

User: y

Claude Code: 正在设置 iTerm2...

✓ 备份当前 iTerm2 首选项
✓ 添加 Shift+Enter 键绑定
✓ 绑定操作：发送文本 "\n"
✓ iTerm2 首选项已更新

设置完成！

重启 iTerm2 以使更改生效。

重启后，您可以使用：
- Shift+Enter: 新行
- Enter: 发送消息
```

### 场景 2：在 VSCode 中设置

```
User: /terminal-setup

Claude Code: 终端设置向导
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

检测到的终端：VSCode 集成终端

VSCode 键绑定配置：

选项 1：自动设置
- 修改 keybindings.json
- 推荐给大多数用户

选项 2：手动设置
- 显示要复制/粘贴的说明
- 适用于高级用户

选择选项 (1/2):

User: 1

Claude Code: 正在设置 VSCode 键绑定...

✓ 找到 keybindings.json:
  ~/.config/Code/User/keybindings.json

✓ 备份现有键绑定
✓ 添加 Shift+Enter 绑定：

  {
    "key": "shift+enter",
    "command": "workbench.action.terminal.sendSequence",
    "args": { "text": "\n" },
    "when": "terminalFocus"
  }

✓ 键绑定已更新

设置完成！

更改立即生效（无需重启）。

测试它：
1. 按 Shift+Enter → 创建新行
2. 按 Enter → 发送消息
```

## 使用 Shift+Enter

### 设置前

```
User: 帮我处理：
[按 Enter - 消息过早发送]

Claude Code: [响应不完整的消息]

User: 抱歉，我想写更多...
```

### 设置后

```
User: 帮我处理：
[按 Shift+Enter - 创建新行]
1. 修复认证 bug
[按 Shift+Enter]
2. 添加单元测试
[按 Shift+Enter]
3. 更新文档
[按 Enter - 发送完整消息]

Claude Code: 我将帮助您处理所有三个任务：
1. 修复认证 bug
2. 添加单元测试
3. 更新文档

让我们从认证 bug 开始...
```

## 使用场景

### 多行代码片段

```
User: 审查此函数：
[Shift+Enter]
[Shift+Enter]
function calculateTotal(items) {
[Shift+Enter]
  return items.reduce((sum, item) => {
[Shift+Enter]
    return sum + item.price * item.quantity;
[Shift+Enter]
  }, 0);
[Shift+Enter]
}
[Shift+Enter]
[Shift+Enter]
重点关注性能和可读性。
[Enter]

Claude Code: [审查多行函数]
```

### 结构化 Prompts

```
User: 我需要帮助完成一个复杂的任务：
[Shift+Enter]
[Shift+Enter]
Context:
[Shift+Enter]
- 正在开发电子商务应用
[Shift+Enter]
- 使用 React 和 Node.js
[Shift+Enter]
- 数据库：PostgreSQL
[Shift+Enter]
[Shift+Enter]
任务：
[Shift+Enter]
- 实现购物车
[Shift+Enter]
- 添加持久存储
[Shift+Enter]
- 处理边缘情况
[Shift+Enter]
[Shift+Enter]
要求：
[Shift+Enter]
- 必须快速
[Shift+Enter]
- 处理 1000+ 项
[Shift+Enter]
- 支持访客用户
[Enter]

Claude Code: [响应结构良好、详细的 prompt]
```

### 列表和格式化

```
User: 修复这些问题：
[Shift+Enter]
[Shift+Enter]
高优先级：
[Shift+Enter]
- login.ts 中的 SQL 注入
[Shift+Enter]
- 评论中的 XSS 漏洞
[Shift+Enter]
[Shift+Enter]
中等优先级：
[Shift+Enter]
- 缺少输入验证
[Shift+Enter]
- 弱错误处理
[Shift+Enter]
[Shift+Enter]
低优先级：
[Shift+Enter]
- 代码格式化
[Shift+Enter]
- 更新依赖项
[Enter]

Claude Code: [正确处理优先级列表]
```

## 手动设置（其他终端）

### 其他 macOS 终端

```
User: /terminal-setup

Claude Code: 终端：不自动支持

手动设置说明：

Terminal.app:
1. 打开终端首选项
2. 转到配置文件 > 键盘
3. 点击 "+"
4. 设置键：Shift+Enter
5. 操作：发送文本
6. 值：\n

Alacritty:
添加到 ~/.config/alacritty/alacritty.yml:

key_bindings:
  - { key: Return, mods: Shift, chars: "\n" }

Kitty:
添加到 ~/.config/kitty/kitty.conf:

map shift+enter send_text all \n
```

### Linux 终端

```
User: /terminal-setup

Claude Code: 手动设置 - Linux

GNOME Terminal:
1. 编辑 > 首选项 > 快捷方式
2. 找到 "发送文本" 或自定义快捷方式
3. 分配 Shift+Enter → \n

Konsole:
1. 设置 > 配置键盘快捷方式
2. 添加自定义绑定
3. Shift+Enter → 发送文本 "\n"

Terminator:
添加到 ~/.config/terminator/config:

[keybindings]
  insert_newline = <Shift>Return

tmux (在 ~/.tmux.conf 中):
bind -n S-Enter send-keys "\n"
```

### Windows Terminal

```
User: /terminal-setup

Claude Code: 手动设置 - Windows Terminal

添加到 settings.json:

{
  "actions": [
    {
      "command": {
        "action": "sendInput",
        "input": "\r\n"
      },
      "keys": "shift+enter"
    }
  ]
}

访问 settings.json:
1. 打开 Windows Terminal
2. 按 Ctrl+Shift+,
3. 添加上述绑定
4. 保存并重启
```

## 验证

### 测试设置

```
User: /terminal-setup --test

Claude Code: 正在测试终端键绑定...

测试 1：基本换行符
输入一些文本并按 Shift+Enter

User: 第一行
[按 Shift+Enter]
第二行
[按 Enter]

Claude Code: ✓ 测试通过！

收到：
"第一行
第二行"

Shift+Enter 工作正常！

测试 2：多个换行符
尝试多个 Shift+Enters

User: 第 1 行
[Shift+Enter]
[Shift+Enter]
第 3 行
[Enter]

Claude Code: ✓ 测试通过！

收到：
"第 1 行

第 3 行"

所有键绑定工作正常！
```

### 常见问题

```
User: /terminal-setup --diagnose

Claude Code: 正在诊断键绑定问题...

检查：
✓ 检测到终端：iTerm2
✓ 备份存在：~/.config/claude/backups/iterm2-backup.plist
✗ Shift+Enter 绑定：未找到

问题：键绑定未配置

可能的原因：
1. 设置后 iTerm2 未重启
2. 键绑定被其他设置覆盖
3. 设置被中断

解决方案：
[1] 重新运行设置：/terminal-setup --force
[2] 手动配置
[3] 检查 iTerm2 首选项

User: 1

Claude Code: 使用 --force 标志重新运行设置...
[重复设置过程]
✓ 设置完成！请重启 iTerm2。
```

## 高级配置

### 自定义换行符序列

```
User: /terminal-setup --custom

Claude Code: 自定义终端配置

默认换行符：\n (Unix/Mac)
Windows 换行符：\r\n (CRLF)

自定义序列：
[1] \n (LF) - Unix/Mac
[2] \r\n (CRLF) - Windows
[3] \r (CR) - Old Mac
[4] Custom

选择 (1-4):

User: 1

Claude Code: 使用 Unix 换行符 (\n)
✓ 配置已保存
```

### 多个键绑定

```
User: /terminal-setup --add-bindings

Claude Code: 额外的键绑定

您想添加：

[1] Ctrl+Enter → 发送消息（替代）
[2] Alt+Enter → 插入换行符（替代）
[3] Cmd+Return → 发送消息（Mac）
[4] 自定义绑定

选择选项或 'done':

User: 2

Claude Code: 正在添加 Alt+Enter → 插入换行符

✓ 绑定已添加
现在 Shift+Enter 和 Alt+Enter 都插入换行符。

添加另一个？(y/n)
```

## 备份和恢复

### 备份配置

```
User: /terminal-setup --backup

Claude Code: 正在备份终端配置...

终端：iTerm2

备份位置：
~/.config/claude/backups/iterm2-2025-01-08.plist

✓ 当前 iTerm2 首选项已备份
✓ 键绑定已保存
✓ 备份已验证

恢复使用：
/terminal-setup --restore 2025-01-08
```

### 恢复配置

```
User: /terminal-setup --restore

Claude Code: 可用的备份：

[1] 2025-01-08（当前 - Shift+Enter 设置前）
[2] 2025-01-05（vim 模式设置前）
[3] 2024-12-28（初始备份）

选择要恢复的备份 (1-3):

User: 1

Claude Code: 正在从 2025-01-08 恢复备份...

✓ 备份已加载
✓ iTerm2 首选项已恢复
✓ 先前的键绑定已恢复

重启 iTerm2 以使更改生效。
```

## 卸载

```
User: /terminal-setup --uninstall

Claude Code: 卸载终端设置

这将删除：
- Shift+Enter 键绑定
- 自定义换行符配置
- 恢复原始终端设置

为安全起见，备份将保留。

继续？(y/n)

User: y

Claude Code: 正在卸载...

✓ 已删除 Shift+Enter 绑定
✓ 已恢复原始键绑定
✓ 备份保留在：
  ~/.config/claude/backups/

卸载完成。
重启终端以使更改生效。
```

## 提示 & 最佳实践

### 1. 设置后测试

```
始终验证：
User: 测试第 1 行
[Shift+Enter]
测试第 2 行
[Enter]

确保它创建多行消息，而不是两条消息。
```

### 2. 肌肉记忆

```
练习使用：
- Shift+Enter 用于换行符
- Enter 用于发送

使用几次后变得自然。
```

### 3. 与代码块一起使用

```
粘贴代码时：
User: 这是函数：
[Shift+Enter]
[Shift+Enter]
[粘贴多行代码]
[Shift+Enter]
[Shift+Enter]
请审查它。
[Enter]

创建适当的格式。
```

### 4. 与 /vim 模式结合

```
在 vim 模式下：
- 'o' 打开新行（与 Shift+Enter 相同）
- Shift+Enter 在 INSERT 模式下仍然有效

两种方法都可用于灵活性。
```

## 故障排除

### Shift+Enter 发送消息而不是换行

```
问题：Shift+Enter 发送消息而不是换行符

诊断：
/terminal-setup --diagnose

解决方案：
1. 检查终端配置
2. 验证终端首选项中的绑定
3. 重新运行设置：/terminal-setup --force
4. 重启终端应用程序
```

### 按 Shift+Enter 无效果

```
问题：Shift+Enter 什么也不做

可能的原因：
1. 绑定未保存
2. 终端未重启
3. 冲突的键绑定

解决方案：
1. /terminal-setup --diagnose
2. 检查终端首选项中的冲突
3. 如果自动失败则手动设置
```

### 在 iTerm 中有效但在 VSCode 中无效

```
问题：配置了 iTerm，但 VSCode 不同

解释：
iTerm 和 VSCode 有单独的配置。

解决方案：
在 VSCode 终端中运行 /terminal-setup:
User: /terminal-setup

选择 VSCode 特定的设置。
```

## 相关命令

- `/vim` - 使用 vim 模式的替代多行编辑
- `/config` - 常规 Claude Code 配置
- `/help` - 常规帮助

## 常见问题

**问：需要为每个项目运行此操作吗？**
答：不需要，终端设置是系统范围的，在项目间持久存在。

**问：如果我使用多个终端怎么办？**
答：在您使用的每种终端类型（iTerm、VSCode 等）中运行 `/terminal-setup`。

**问：可以撤销设置吗？**
答：可以，使用 `/terminal-setup --uninstall` 或从备份恢复。

**问：在 tmux/screen 中有效吗？**
答：需要手动 tmux/screen 配置。请参见手动设置说明。

**问：如果 Shift+Enter 在我的终端中已经做了其他事情怎么办？**
答：现有绑定将被覆盖。自动创建备份。

**问：可以使用不同的键组合吗？**
答：可以，使用 `/terminal-setup --custom` 配置替代键。

**问：这是使用 Claude Code 所必需的吗？**
答：不是，但它显著改善了多行输入体验。
