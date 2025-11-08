# `/vim` 命令示例

## 概述
`/vim` 命令在 Claude Code 中启用 vim 模式，允许您使用 vim 风格的键盘导航和编辑，以及交替的插入和命令模式。

## 何时使用
- 您是 vim 用户并且更喜欢 vim 键绑定
- 想要模式编辑以更快地输入命令
- 需要高效的纯键盘导航
- 编辑长或复杂的 prompts
- 更喜欢命令模式进行快速操作

## 示例用法

### 场景 1：启用 Vim 模式

```
User: /vim

Claude Code: Vim 模式已启用
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

模式：NORMAL

Vim 键绑定现在已激活。

常用命令：
- i: 进入 INSERT 模式
- v: 进入 VISUAL 模式
- :: 进入 COMMAND 模式
- ESC: 返回 NORMAL 模式

导航：
- h/j/k/l: 向左/下/上/右移动
- w/b: 下一个/上一个单词
- 0/$: 行首/行尾
- gg/G: 缓冲区开头/结尾

按 'i' 开始输入。

-- NORMAL --
```

### 场景 2：基本 Vim 工作流

```
User: /vim

[Vim 模式已启用 - NORMAL 模式]

User: i [进入 INSERT 模式]

-- INSERT --

User: 帮我将此函数重构为使用 async/await

User: <ESC> [返回 NORMAL 模式]

-- NORMAL --

User: [审查消息]

User: A [在行尾追加]

-- INSERT --

User:  并添加错误处理

User: <ESC>

-- NORMAL --

User: <ENTER> [发送消息]

Claude Code: [处理请求]
```

### 场景 3：编辑和导航

```
-- NORMAL 模式 --

当前 prompt: |帮我修复 login.ts 中的 authentiation bug

User: w [移动到下一个单词]
光标位于：authentiation

User: cw [更改单词]
-- INSERT --

User: authentication [更正拼写错误]

User: <ESC>
-- NORMAL --

User: $ [跳到行尾]
User: a [追加]
-- INSERT --
User:  在第 45 行

User: <ESC><ENTER>

Claude Code: 我将帮助修复 login.ts 中第 45 行的 authentication bug
```

## Vim 模式基础

### 模式指示器

```
-- NORMAL --    准备导航和命令
-- INSERT --    正常输入文本
-- VISUAL --    选择文本
-- COMMAND --   执行 vim 命令
```

### 基本键绑定

#### 导航（NORMAL 模式）

```
字符移动：
h - 左
j - 下
k - 上
l - 右

单词移动：
w - 下一个单词开头
b - 上一个单词开头
e - 下一个单词结尾

行移动：
0 - 行首
$ - 行尾
^ - 第一个非空白字符

缓冲区移动：
gg - 输入顶部
G - 输入底部
<C-u> - 向上滚动
<C-d> - 向下滚动
```

#### 编辑（NORMAL 模式）

```
进入 INSERT 模式：
i - 在光标前插入
a - 在光标后追加
I - 在行首插入
A - 在行尾追加
o - 在下方打开新行
O - 在上方打开新行

删除：
x - 删除字符
dw - 删除单词
dd - 删除行
D - 删除到行尾

更改：
cw - 更改单词
cc - 更改行
C - 更改到行尾

撤销/重做：
u - 撤销
<C-r> - 重做
```

#### Visual 模式

```
进入 VISUAL 模式：
v - 字符选择
V - 行选择

在 VISUAL 中：
[导航以选择]
y - 复制
d - 删除
c - 更改
```

### Command 模式

```
从 NORMAL 模式，按 : 进入 COMMAND 模式

命令：
:w - 发送消息（如按 ENTER）
:q - 清除当前输入
:help - 显示 vim 帮助
:set - 配置 vim 选项
```

## 高级用法

### 多行编辑

```
-- NORMAL --

User: o [在下方打开新行]

-- INSERT --

User: 帮我处理：
1. 修复认证
2. 添加测试
3. 更新文档

User: <ESC>

-- NORMAL --

User: gg [回到顶部]
User: A [追加到第一行]

-- INSERT --

User:  这些任务：

User: <ESC><ENTER>

Claude Code: 我将帮助您处理这些任务：
1. 修复认证
2. 添加测试
3. 更新文档
```

### Visual 选择

```
-- NORMAL --

当前：帮我重构 getUserData 和 updateUserProfile 函数

User: w w [移动到 "重构"]
User: v [进入 VISUAL]

-- VISUAL --

User: w w w [选择 "重构 getUserData 和"]

已选择：重构 getUserData 和

User: c [更改选择]

-- INSERT --

User: 优化这两个

结果：帮我优化这两个 updateUserProfile 函数

User: <ESC><ENTER>
```

### 搜索和替换

```
-- NORMAL --

当前：更新 userService.js 文件

User: /Service [搜索 "Service"]

光标移动到 "Service"

User: cw [更改单词]

-- INSERT --

User: Repository

结果：更新 userRepository.js 文件

User: <ESC>
User: n [下一个匹配]
User: . [重复上次更改]
```

### 宏（高级）

```
-- NORMAL --

User: qa [开始录制宏到寄存器 'a']
User: I# <ESC>j [在行首添加 "# " 并向下移动]
User: q [停止录制]

User: 5@a [重复宏 5 次]

转换：
Task 1
Task 2
Task 3

为：
# Task 1
# Task 2
# Task 3
```

## 配置

### 自定义 Vim 设置

```
User: /vim --configure

Claude Code: Vim 配置：
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

当前设置：

模式指示器：已启用 ✓
行号：已禁用
相对行号：已禁用
搜索高亮：已启用 ✓
增量搜索：已启用 ✓
智能大小写：已启用 ✓
自动缩进：已启用 ✓

修改设置：
[1] 切换行号
[2] 切换相对行号
[3] 配置键映射
[4] 设置 leader 键
[5] 重置为默认值

User: 1

Claude Code: 行号：已启用

  1 | 当前输入显示在这里
    |

-- NORMAL --
```

### 自定义键映射

```
User: /vim --mappings

Claude Code: 自定义键映射：
━━━━━━━━━━━━━━━━━━━━━━━━━━━━

定义自定义映射：

示例：
jk -> <ESC>（按 j 然后 k 退出 INSERT 模式）
<leader>w -> 发送消息
<leader>c -> 清除输入

当前映射：
- jk: <ESC>
- <leader>: <Space>

添加映射：
User: jk <ESC>

Claude Code: 映射已添加：jk -> <ESC>

现在您可以快速按 'jk' 而不是 ESC。
```

## 工作流示例

### 代码审查请求

```
-- NORMAL --

User: i

-- INSERT --

User: 审查此代码：

User: <ESC>

-- NORMAL --

User: o [新行]

-- INSERT --

User: [粘贴代码]

User: <ESC>

-- NORMAL --

User: o [另一行]

-- INSERT --

User: 重点关注错误处理和性能

User: <ESC><ENTER>
```

### 快速命令编辑

```
用户输入：帮我修复 srvc/login.ts 中的 authentiation bug

-- NORMAL --

User: fb [返回到 "authentiation" 中的 "a"]
User: x [删除 "a"]
User: $ [行尾]
User: T/ [返回到 "/" 之前的 "srvc"]
User: cw [更改 "srvc"]

-- INSERT --

User: src

User: <ESC><ENTER>

结果：帮我修复 src/login.ts 中的 authentication bug
```

### 模板扩展

```
用户有一个常见的 prompt 模式：

-- NORMAL --

User: i

-- INSERT --

User: /review

User: <ESC>

-- NORMAL --

User: A [追加]

-- INSERT --

User:  --focus security

User: <ESC>o

-- INSERT --

User: 检查：
- XSS 漏洞
- SQL 注入
- 认证问题

User: <ESC><ENTER>
```

## Vim 模式功能

### 搜索

```
-- NORMAL --

User: /bug [向前搜索 "bug"]

高亮：修复认证中的 bug

User: n [下一个匹配]
User: N [上一个匹配]

User: ?auth [向后搜索 "auth"]
```

### 标记和跳转

```
-- NORMAL --

User: ma [在当前位置设置标记 'a']

User: [导航到其他地方]

User: 'a [跳回标记 'a']

内置标记：
' - 最后跳转位置
'' - 在最后两个位置之间切换
```

### 文本对象

```
-- NORMAL --

当前：帮我修复此（authentication bug）在代码中

光标在 "bug" 上：

User: ci( [更改括号内]

-- INSERT --

User: login issue

结果：帮我修复此（login issue）在代码中

常见文本对象：
ciw - 更改内部单词
ci" - 更改引号内
ci) - 更改括号内
ca{ - 更改大括号周围（包括大括号）
```

## 禁用 Vim 模式

```
User: /vim off

Claude Code: Vim 模式已禁用

返回正常输入模式。
Vim 键绑定不再激活。

使用 /vim 重新启用
```

## 提示 & 技巧

### 1. 肌肉记忆

```
练习常见模式：
- ESC（退出 INSERT）
- i（插入）或 a（追加）
- 0/$（行导航）
- w/b（单词导航）
- dd（删除行）
- u（撤销）

这些覆盖 80% 的使用。
```

### 2. 快速更正

```
在 INSERT 模式中出现拼写错误？

-- INSERT --

User: 帮我处理 authentiacation

User: <ESC> [退出到 NORMAL]
User: b [回退一个单词]
User: cw [更改单词]

-- INSERT --

User: authentication

比退格更快！
```

### 3. 组合动作

```
-- NORMAL --

强大的组合：
d$ - 删除到行尾
c^ - 更改到行首
y5w - 复制 5 个单词
3dd - 删除 3 行
gU2w - 大写 2 个单词
```

### 4. Leader 键快捷方式

```
-- NORMAL --

<leader> = Space（默认）

<Space>w - 发送消息
<Space>q - 清除输入
<Space>h - 显示帮助
<Space>v - 切换 visual 模式

在以下配置：
/vim --mappings
```

### 5. Escape 替代方案

```
如果 ESC 难以触及：

配置：jk -> ESC
或：<C-[>（Ctrl+[）
或：<C-c>（Ctrl+c）

在 INSERT 模式下快速输入 'jk' -> 退出到 NORMAL
```

## 故障排除

### 卡在模式中

```
问题：卡在 INSERT 模式，无法返回 NORMAL

解决方案：
- 按 ESC
- 或按 Ctrl+[
- 或按 Ctrl+c
- 或输入 'jk' 如果已映射

如果全部失败：
/vim off
/vim
```

### 键绑定不工作

```
User: /vim --debug

Claude Code: Vim 调试模式：

最后按下的键：j
当前模式：NORMAL
待处理的键：（无）
映射的键：jk，<leader>w，<leader>q

检查键是否：
1. 有效的 vim 命令
2. 适合当前模式
3. 不与系统键冲突
```

### 意外禁用

```
User: [意外按下 /vim off]

Claude Code: Vim 模式已禁用。

User: /vim

Claude Code: Vim 模式已重新启用。
所有设置已恢复。
```

## 比较：Normal vs Vim 模式

```
Normal 模式：
✓ 简单、熟悉
✓ 鼠标友好
✗ 编辑较慢
✗ 更多按键

Vim 模式：
✓ 快速编辑
✓ 纯键盘
✓ 强大的动作
✗ 学习曲线
✗ 模式复杂性

根据以下选择：
- 您的 vim 经验
- 模式编辑的舒适度
- 速度与简单性的需求
```

## 相关命令

- `/terminal-setup` - 配置终端键绑定
- `/config` - 常规设置
- `/help` - 常规帮助

## 最佳实践

### 1. 从简单开始
```
首先学习这些：
- i（插入）
- ESC（normal）
- hjkl（导航）
- dd（删除行）
- u（撤销）

根据需要添加更多。
```

### 2. 使用您知道的
```
不要一次尝试学习所有 vim 命令。
使用 normal 模式进行导航，INSERT 进行输入。
逐步添加高级功能。
```

### 3. 配置以获得舒适度
```
设置：
- 简单的 ESC 替代方案（jk）
- 舒适的 leader 键
- 常用命令作为映射
```

## 常见问题

**问：需要了解 vim 才能使用此功能吗？**
答：基本熟悉有帮助，但您可以从 i（插入）和 ESC（normal）开始。

**问：可以将 vim 模式与其他命令一起使用吗？**
答：可以，vim 模式仅影响输入编辑，不影响 Claude Code 的响应方式。

**问：如果按错键怎么办？**
答：按 ESC 返回 NORMAL 模式，然后按 u 撤销。

**问：是否支持完整的 vim？**
答：核心功能支持（导航、编辑、visual）。一些高级功能可能受限。

**问：可以暂时禁用 vim 模式吗？**
答：可以，使用 `/vim off` 禁用，`/vim` 重新启用。

**问：这在所有终端中都有效吗？**
答：大多数终端支持 vim 模式，但某些键绑定可能与终端快捷方式冲突。
