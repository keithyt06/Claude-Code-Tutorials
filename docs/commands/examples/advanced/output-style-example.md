# `/output-style` 命令示例

## 概述
`/output-style` 命令允许您自定义 Claude Code 显示响应的方式，包括格式化、详细程度和呈现风格。

## 何时使用
- 自定义 Claude 的响应格式
- 调整详细程度（简洁 vs 详细）
- 为不同任务更改输出
- 屏幕阅读器兼容性
- 终端宽度限制
- 可读性的个人偏好

## 示例用法

### 场景 1：查看当前样式

```
User: /output-style

Claude Code: 输出样式配置
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

当前样式：Default

可用样式：
[1] Default - 平衡的格式化和详细程度
[2] Concise - 简短、直接的响应
[3] Detailed - 全面的解释
[4] Minimal - 纯文本，无格式化
[5] Technical - 以代码为中心，较少散文
[6] Beginner - 额外的解释和示例
[7] Custom - 配置您自己的样式

当前设置：
├─ 格式化：Markdown 已启用
├─ 代码块：语法高亮开启
├─ 详细程度：中等
├─ 解释：标准
└─ 示例：已包含

选择样式 (1-7) 或按 Enter 保持当前：
```

### 场景 2：切换到 Concise 样式

```
User: /output-style concise

Claude Code: 样式：Concise ✓

响应将会：
- 简短直接
- 最少解释
- 专注于解决方案
- 较少冗长

示例对比：

Default 样式：
"我将帮助您修复认证 bug。此问题通常
由不正确的 token 处理引起。让我检查代码并
提供带解释的解决方案..."

Concise 样式：
"修复认证 bug。问题：token 处理。解决方案："

User: 修复登录 bug

Claude Code: Bug: 异步认证调用缺少 await。

修复（第 42 行）：
- const user = authenticateUser(token);
+ const user = await authenticateUser(token);

完成。
```

### 场景 3：切换到 Detailed 样式

```
User: /output-style detailed

Claude Code: 样式：Detailed ✓

响应将包括：
- 全面的解释
- 逐步分解
- 额外的 context
- 多个示例
- 最佳实践
- 相关概念

User: 如何使用 async/await？

Claude Code: 理解 JavaScript 中的 async/await
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

## 什么是 async/await？

Async/await 是构建在 Promises 之上的现代 JavaScript 功能，
允许您编写看起来和行为更像同步代码的异步代码，
使其更易于阅读和维护。

## 背景

在 async/await 之前，开发者使用：
1. Callbacks（早期，导致"callback hell"）
2. Promises（ES6，更好但仍然复杂）
3. async/await（ES2017，最简洁的语法）

## 基本语法

### 声明 async 函数

```javascript
async function fetchData() {
  // 函数体
}
```

函数前的 'async' 关键字意味着：
- 函数自动返回 Promise
- 您可以在其中使用 'await'
- 任何返回值都包装在 Promise.resolve() 中

### 使用 await

```javascript
async function fetchUserData() {
  const response = await fetch('/api/user');
  const data = await response.json();
  return data;
}
```

'await' 关键字：
- 暂停执行直到 Promise resolve
- 只能在 async 函数内使用
- 返回 resolved 值
- 如果 Promise reject 则抛出

[... 继续广泛的示例、边缘情况、最佳实践 ...]
```

## 可用样式

### 1. Default 样式

```
User: /output-style default

Claude Code: 平衡样式，具有：
- 标准格式化（markdown）
- 中等详细程度
- 有用时的代码示例
- 清晰的解释
- 结构化的响应

最适合：一般使用
```

### 2. Concise 样式

```
User: /output-style concise

Claude Code: 简短样式，具有：
- 短响应
- 最少散文
- 快速解决方案
- 较少解释
- 紧凑格式化

最适合：快速任务、有经验的开发者
```

### 3. Detailed 样式

```
User: /output-style detailed

Claude Code: 全面样式，具有：
- 深入解释
- 多个示例
- 逐步指南
- Context 和背景
- 包含最佳实践

最适合：学习、复杂主题、彻底审查
```

### 4. Minimal 样式

```
User: /output-style minimal

Claude Code: 纯文本样式，具有：
- 无 markdown 格式化
- 无语法高亮
- 仅基本文本
- 干净的输出
- 终端友好

最适合：屏幕阅读器、文本处理、简单终端

示例输出（minimal）：

User: 显示一个函数

Claude Code:
function add(a, b) {
  return a + b;
}

此函数将两个数字相加并返回结果。
```

### 5. Technical 样式

```
User: /output-style technical

Claude Code: 以代码为中心的样式，具有：
- 强调代码
- 较少散文
- 技术精确性
- 假设有经验
- 实现细节

最适合：高级开发者、以实现为中心的任务

示例：

User: 优化此查询

Claude Code:
查询优化：

原始（N+1）：
```sql
SELECT * FROM users;
-- 然后对每个：SELECT * FROM posts WHERE user_id = ?
```

优化（JOIN）：
```sql
SELECT u.*, p.*
FROM users u
LEFT JOIN posts p ON u.id = p.user_id;
```

性能：O(n) -> O(log n)，带索引的 user_id。
结果：快 10 倍，单次 DB 往返。
```

### 6. Beginner 样式

```
User: /output-style beginner

Claude Code: 初学者友好样式，具有：
- 额外解释
- 词汇定义
- 简单示例优先
- 注明常见陷阱
- 鼓励性的语气

最适合：学习、新开发者、不熟悉的主题

示例：

User: 什么是 Promise？

Claude Code: 理解 Promises（初学者友好）
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

Promise 就像编程中的"欠条"。

现实世界的类比：
想象您订购外卖：
1. 您下订单（Promise 创建）
2. 您继续做其他事情（async）
3. 食物稍后到达（Promise resolve）
4. 或订单失败（Promise reject）

您不会在门口等待 - 您做其他事情，
外卖在"后台"发生！

简单的代码示例：

```javascript
// 订购食物（创建 Promise）
const foodPromise = orderFood("pizza");

// 等待时做其他事情
watchTV();

// 当食物到达时，吃它（处理 Promise）
foodPromise.then(food => {
  eat(food);
});
```

解释的关键术语：
- "async" = 异步 = 不阻塞/等待
- "Promise" = 代表未来的值
- "then" = Promise 完成时要做什么
- "catch" = Promise 失败时要做什么

[... 继续温和、彻底的解释 ...]
```

### 7. Custom 样式

```
User: /output-style custom

Claude Code: 自定义输出样式配置
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

自定义您的输出偏好：

详细程度：
( ) Minimal - 仅必要内容
( ) Low - 简短响应
(•) Medium - 平衡
( ) High - 彻底
( ) Maximum - 所有内容

格式化：
[✓] Markdown 格式化
[✓] 语法高亮
[✓] Emoji 指示器
[ ] ASCII 艺术/图表
[✓] 节标题
[✓] 项目符号

代码呈现：
[✓] 语言标签
[✓] 行号
[✓] 代码中的注释
[✓] 多个示例
[ ] 可执行片段

解释：
[✓] 内联注释
[✓] 单独的解释
[✓] 概念背景
[ ] 历史 context
[✓] 最佳实践
[✓] 常见陷阱

语气：
( ) 正式
(•) 专业
( ) 随意
( ) 友好

应用自定义样式？(y/n)

User: y

Claude Code: ✓ 自定义样式已应用！
您的偏好已保存到 ~/.config/claude/output-style.json
```

## 样式比较

### 相同问题，不同样式

问题："如何在 JavaScript 中反转字符串？"

#### Concise:
```
User: 反转字符串

Claude Code:
```javascript
str.split('').reverse().join('')
```
分割 → 反转数组 → 连接。
```

#### Default:
```
User: 反转字符串

Claude Code: 这是如何在 JavaScript 中反转字符串：

```javascript
const reversed = str.split('').reverse().join('');
```

这通过以下工作：
1. `split('')` - 将字符串转换为字符数组
2. `reverse()` - 反转数组
3. `join('')` - 组合回字符串

示例：
```javascript
const str = "hello";
const reversed = str.split('').reverse().join('');
console.log(reversed); // "olleh"
```
```

#### Detailed:
```
User: 反转字符串

Claude Code: JavaScript 中的字符串反转 - 完整指南
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

## 方法 1：split-reverse-join（最常见）

```javascript
const reversed = str.split('').reverse().join('');
```

工作原理：
1. split('') 将字符串分解为单个字符数组
2. reverse() 就地反转数组
3. join('') 将数组连接回字符串

优点：
- ✓ 简单易读
- ✓ 适用于大多数情况
- ✓ 单行

缺点：
- ✗ 不能正确处理 Unicode（emoji、代理对）
- ✗ 创建中间数组（内存）

## 方法 2：循环（更好的性能）

```javascript
function reverseString(str) {
  let reversed = '';
  for (let i = str.length - 1; i >= 0; i--) {
    reversed += str[i];
  }
  return reversed;
}
```

优点：
- ✓ 长字符串更好的性能
- ✓ 无中间数组

缺点：
- ✗ 更冗长
- ✗ 字符串连接可能很慢

## 方法 3：Reduce（函数式）

```javascript
const reversed = str.split('').reduce((rev, char) => char + rev, '');
```

## 方法 4：Unicode 安全（最适合 emoji）

```javascript
const reversed = [...str].reverse().join('');
```

使用展开运算符正确处理 Unicode：
- "hello👋" → "👋olleh" ✓
- 不是："hello👋" → "�olleh" ✗

[... 继续性能比较、边缘情况等 ...]
```

#### Beginner:
```
User: 反转字符串

Claude Code: 反转字符串 - 初学者指南
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

## 什么是"反转字符串"的意思？

它意味着取一个单词或句子并将其向后翻转。

示例：
- "hello" 变成 "olleh"
- "cat" 变成 "tac"
- "abc123" 变成 "321cba"

## JavaScript 中最简单的方法

```javascript
const word = "hello";
const backwards = word.split('').reverse().join('');
console.log(backwards); // 显示："olleh"
```

让我解释每个部分：

1. **split('')**
   - 将字符串分成片段
   - "hello" 变成 ["h", "e", "l", "l", "o"]
   - 想象它就像分离拼字游戏字母

2. **reverse()**
   - 翻转顺序
   - ["h", "e", "l", "l", "o"] 变成 ["o", "l", "l", "e", "h"]
   - 就像翻转一叠卡片

3. **join('')**
   - 将字母粘回一起
   - ["o", "l", "l", "e", "h"] 变成 "olleh"
   - 就像用拼字游戏字母拼写单词

自己尝试！
[包括交互式示例、常见错误、练习题...]
```

## Context 感知样式

### 自动样式调整

```
Claude Code 可以根据 context 自动调整：

User: 快速问题：箭头函数的语法是什么？

Claude Code: [自动使用 concise 样式]

箭头函数语法：
```javascript
const func = (param) => param * 2;
```

User: 我正在学习 JavaScript。你能解释箭头函数吗？

Claude Code: [自动使用 beginner 样式]

箭头函数解释（初学者）
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

箭头函数是在 JavaScript 中编写函数的更短方法。
它们看起来像一个箭头 (=>)，这就是为什么它们被称为"箭头函数"！

[详细的初学者友好解释如下...]
```

## 高级配置

### 每个项目的样式

```
User: /output-style --save-project

Claude Code: 为此项目保存样式？

当前目录：~/dev/my-app
当前样式：Technical

将 technical 样式保存为 ~/dev/my-app 的默认值？(y/n)

User: y

Claude Code: ✓ 已保存

项目样式配置：
~/.claude/projects/my-app/output-style.json

在 ~/dev/my-app 中工作时：
- 自动使用 Technical 样式
- 使用 /output-style [style] 覆盖

其他项目：使用全局默认值
```

### 样式配置文件

```
User: /output-style --profiles

Claude Code: 输出样式配置文件
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

已保存的配置文件：
[1] work - Technical, concise, 无 emoji
[2] learning - Beginner, detailed, 示例
[3] quick - Minimal, 快速响应

创建新配置文件：
[4] 新配置文件

选择 (1-4):

User: 1

Claude Code: ✓ 已加载 "work" 配置文件

设置：
- 样式：Technical
- 详细程度：Low
- 格式化：以代码为中心
- Emoji: 已禁用
```

### 切换设置

```
User: /output-style --toggle emoji

Claude Code: Emoji 指示器：关闭

响应将使用文本代替：
- ✓ → [OK]
- ✗ → [FAILED]
- ⚠️ → [WARNING]

User: /output-style --toggle syntax-highlighting

Claude Code: 语法高亮：关闭

代码块现在是纯文本（更好地复制粘贴）。
```

## 故障排除

### 样式未应用

```
User: /output-style --diagnose

Claude Code: 输出样式诊断
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

正在检查配置...

✓ 样式配置文件存在
✓ 样式设置：concise
✗ 项目覆盖活跃：detailed（来自 ~/project/.claude/style.json）

当前有效样式：detailed（项目覆盖）

项目覆盖优先于全局设置。

修复：
[1] 删除项目覆盖
[2] 更新项目覆盖
[3] 保持项目覆盖

User: 1

Claude Code: ✓ 项目覆盖已删除
现在使用全局样式：concise
```

### 重置为默认值

```
User: /output-style --reset

Claude Code: 将输出样式重置为默认值？

这将：
- 清除自定义配置
- 删除项目覆盖
- 重置为 Default 样式
- 清除已保存的配置文件

继续？(y/n)

User: y

Claude Code: ✓ 输出样式已重置为默认值

所有自定义已清除。
使用：Default 样式
```

## 最佳实践

### 根据任务选择样式

```
代码审查：Default 或 Technical
学习：Detailed 或 Beginner
快速修复：Concise
文档：Detailed
探索：Default
调试：Technical
```

### 根据需要调整

```
从 Default 开始，然后：
- 太冗长？→ Concise
- 需要更多细节？→ Detailed
- 新话题？→ Beginner
- 只想要代码？→ Technical
```

### 使用项目样式

```
为了一致性：
/output-style --save-project

团队成员可以共享样式配置。
```

## 相关命令

- `/config` - 常规配置
- `/help` - 查看可用命令
- `/compact` - 减少对话长度

## 提示

- 尝试不同的样式以找到您的偏好
- 学习新主题时使用 Beginner 样式
- 快速任务切换到 Concise
- 以实现为重的工作使用 Technical 样式
- 保存项目样式以保持一致性
- 为不同工作流创建配置文件

## 常见问题

**问：样式会影响 Claude 的能力吗？**
答：不会，仅影响呈现。同样的智能，不同的格式。

**问：可以在对话中更改样式吗？**
答：可以，随时使用 `/output-style [style]`。

**问：Concise 样式会遗漏重要细节吗？**
答：不会，它更简短但仍然准确。如果需要，询问详情。

**问：可以与团队成员共享我的自定义样式吗？**
答：可以，共享 ~/.config/claude/output-style.json 文件。

**问：样式在会话间持久存在吗？**
答：可以，您的选择会保存，直到您更改它。

**问：可以在选择前预览样式吗？**
答：使用 `/output-style` 查看每种样式的描述和示例。
