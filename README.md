<div align="center">
    <h1>🚀 Claude Code 从入门到精通</h1>
    <h3><em>完整的 AI 辅助编程学习资源库</em></h3>
</div>

<p align="center">
    <strong>从零基础到高级应用，系统学习 Claude Code，掌握 AI 辅助编程技能，提升开发效率 10 倍</strong>
</p>

<p align="center">
    <a href="https://github.com/0xfnzero/AI-Code-Tutorials">
        <img src="https://img.shields.io/github/stars/0xfnzero/AI-Code-Tutorials?style=social" alt="GitHub stars">
    </a>
    <a href="https://github.com/0xfnzero/AI-Code-Tutorials/network">
        <img src="https://img.shields.io/github/forks/0xfnzero/AI-Code-Tutorials?style=social" alt="GitHub forks">
    </a>
    <a href="https://github.com/0xfnzero/AI-Code-Tutorials/blob/main/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-blue.svg" alt="License">
    </a>
    <a href="https://github.com/0xfnzero/AI-Code-Tutorials/issues">
        <img src="https://img.shields.io/github/issues/0xfnzero/AI-Code-Tutorials" alt="GitHub issues">
    </a>
</p>

<p align="center">
    <img src="https://img.shields.io/badge/Claude-000000?style=for-the-badge&logo=anthropic&logoColor=white" alt="Claude">
    <img src="https://img.shields.io/badge/AI-FF6B6B?style=for-the-badge&logo=openai&logoColor=white" alt="AI">
    <img src="https://img.shields.io/badge/Tutorial-4B8BBE?style=for-the-badge&logo=read-the-docs&logoColor=white" alt="Tutorial">
</p>

<p align="center">
    <a href="#-快速开始">快速开始</a> •
    <a href="#-学习路线建议">学习路线</a> •
    <a href="#-内容导航">内容导航</a> •
    <a href="#-扩展资源">扩展资源</a>
</p>

<p align="center">
    <a href="./README.md">中文</a> |
    <a href="./README_EN.md">English</a> |
    <a href="https://fnzero.dev/">Website</a> |
    <a href="https://t.me/fnzero_group">Telegram</a> |
    <a href="https://discord.gg/vuazbGkqQE">Discord</a>
</p>

---

## 📖 快速开始

### 新手入门
如果你是第一次接触 Claude Code，建议从这里开始：

1. 📚 阅读 [第一课：什么是 Claude Code？](./docs/tutorials/zh/01-基础概念.md)
2. ⚙️ 跟随 [第二课：安装和配置](./docs/tutorials/zh/02-安装和配置.md) 完成环境搭建
3. 💬 尝试 [第三课：第一次对话](./docs/tutorials/zh/03-第一次对话.md) 开始实践

### 快速查询
- 🔍 查找命令？访问 [命令参考指南](./docs/commands/README_CN.md)
- 📋 寻找示例？浏览 [命令使用示例](./docs/commands/examples/)
- 🎯 高级技巧？查看 [最佳实践](./docs/tutorials/zh/12-最佳实践.md)

---

## 🗂️ 项目结构

```
Claude-Code-Tutorials/
│
├── 📚 docs/
│   ├── 📖 tutorials/          # 系统教程（第 1-14 课）
│   │   ├── zh/               # 中文教程
│   │   └── en/               # 英文教程
│   │
│   └── 📝 commands/           # 命令参考指南
│       ├── README_CN.md      # 命令索引（中文）
│       ├── README.md         # 命令索引（英文）
│       └── examples/         # 命令使用示例
│           ├── session-management/   # 会话管理
│           ├── project-config/       # 项目配置
│           ├── workflow/             # 工作流
│           ├── agents/               # AI 代理
│           ├── context/              # 上下文管理
│           ├── account/              # 账户管理
│           ├── system/               # 系统诊断
│           └── advanced/             # 高级功能
│
├── 📦 assets/                 # 图片、资源文件
├── 💡 examples/               # 完整项目示例代码
├── README.md                  # 项目主文档（中文）
├── README_EN.md              # 项目主文档（英文）
└── LICENSE                    # MIT 许可证
```

---

## 🎯 内容导航

### 📚 系统教程（循序渐进）

#### 📘 入门篇（零基础友好）

| 课程 | 标题 | 描述 | 链接 |
|:---:|:---|:---|:---:|
| 1 | 什么是 Claude Code？ | 基础概念、特点、适用场景 | [查看](./docs/tutorials/zh/01-基础概念.md) |
| 2 | 安装和配置 | 环境搭建、API 配置、常见问题 | [查看](./docs/tutorials/zh/02-安装和配置.md) |
| 3 | 第一次对话 | 有效沟通、创建第一个项目 | [查看](./docs/tutorials/zh/03-第一次对话.md) |
| 4 | 基本命令和操作 | 内置命令、文件操作、Git 基础 | [查看](./docs/tutorials/zh/04-基本命令和操作.md) |

#### 📗 进阶篇（提升技能）

| 课程 | 标题 | 描述 | 链接 |
|:---:|:---|:---|:---:|
| 5 | 文件操作进阶 | 复杂项目管理、代码重构技巧 | [查看](./docs/tutorials/zh/05-文件操作进阶.md) |
| 6 | 项目实战 - Web 应用 | 从零构建完整的任务管理应用 | [查看](./docs/tutorials/zh/06-项目实战-Web应用.md) |
| 7 | 进阶技巧和最佳实践 | 提示词、代码审查、调试、设计模式 | [查看](./docs/tutorials/zh/07-进阶技巧.md) |

**第六课详细模块：**
- [1.1 项目规划](./docs/tutorials/zh/06-项目实战-Web应用/01-项目规划.md) - 需求分析、技术栈选择
- [1.2 项目结构搭建](./docs/tutorials/zh/06-项目实战-Web应用/02-项目结构.md) - 目录结构、版本控制
- [1.3 静态页面设计](./docs/tutorials/zh/06-项目实战-Web应用/03-静态页面.md) - HTML/CSS、响应式布局
- [1.4 前端功能实现](./docs/tutorials/zh/06-项目实战-Web应用/04-前端功能.md) - CRUD 操作、本地存储
- [1.5 后端服务器搭建](./docs/tutorials/zh/06-项目实战-Web应用/05-后端搭建.md) - Express、SQLite、API
- [1.6 用户认证系统](./docs/tutorials/zh/06-项目实战-Web应用/06-用户认证.md) - 注册登录、JWT、密码加密
- [1.7 功能增强](./docs/tutorials/zh/06-项目实战-Web应用/07-功能增强.md) - 搜索筛选、拖拽排序
- [1.8 部署上线](./docs/tutorials/zh/06-项目实战-Web应用/08-部署上线.md) - Heroku 部署、环境配置

**第七课详细模块：**
- [1.1 提示词基础](./docs/tutorials/zh/07-进阶技巧/01-提示词基础.md) - 精确描述、上下文、示例引用
- [1.2 代码审查](./docs/tutorials/zh/07-进阶技巧/02-代码审查.md) - 性能优化、重构建议
- [1.3 调试技巧](./docs/tutorials/zh/07-进阶技巧/03-调试技巧.md) - 系统化调试、断点、日志
- [1.4 设计模式](./docs/tutorials/zh/07-进阶技巧/04-设计模式.md) - 单例、观察者、工厂模式
- [1.5 错误处理](./docs/tutorials/zh/07-进阶技巧/05-错误处理.md) - 统一处理、友好提示
- [1.6 安全最佳实践](./docs/tutorials/zh/07-进阶技巧/06-安全实践.md) - 输入验证、XSS/CSRF 防护

#### 📕 高级篇（专业开发）

| 课程 | 标题 | 描述 | 链接 |
|:---:|:---|:---|:---:|
| 8 | Claude Code 高级应用 | AI 结对编程、复杂架构、自动化测试 | [查看](./docs/tutorials/zh/08-高级应用.md) |
| 9 | ⭐ 提示词优化技巧 | **效率提升 10 倍的秘诀** | [查看](./docs/tutorials/zh/09-提示词优化技巧.md) |
| 10 | ⭐ AI 子代理系统 | **打造你的专家团队** | [查看](./docs/tutorials/zh/10-AI子代理系统.md) |
| 11 | 实用技巧集锦 | 34 条实战技巧（CLI、图像、集成等） | [查看](./docs/tutorials/zh/11-实用技巧集锦.md) |
| 12 | ⭐ 最佳实践 | **Anthropic 官方推荐** | [查看](./docs/tutorials/zh/12-最佳实践.md) |
| 13 | ⭐ MCP 服务器指南 | **从入门到精通的 MCP 配置** | [查看](./docs/tutorials/zh/13-MCP服务器指南.md) |
| 14 | ⭐ 完整使用指南 | **百科全书和日常参考手册** | [查看](./docs/tutorials/zh/14-完整使用指南.md) |

**第九课详细模块：**
- [1.1 六大黄金原则](./docs/tutorials/zh/09-提示词优化技巧/01-六大原则.md)
- [1.2 高级技巧](./docs/tutorials/zh/09-提示词优化技巧/02-高级技巧.md)
- [1.3 模板库](./docs/tutorials/zh/09-提示词优化技巧/03-模板库.md)
- [1.4 最佳实践](./docs/tutorials/zh/09-提示词优化技巧/04-最佳实践.md)
- [1.5 案例研究](./docs/tutorials/zh/09-提示词优化技巧/05-案例研究.md)
- [1.6 练习项目](./docs/tutorials/zh/09-提示词优化技巧/06-练习项目.md)

**第十课详细模块：**
- [1.1 核心概念](./docs/tutorials/zh/10-AI子代理系统/01-核心概念.md)
- [1.2 开发类代理](./docs/tutorials/zh/10-AI子代理系统/02-开发类代理.md)
- [1.3 架构类代理](./docs/tutorials/zh/10-AI子代理系统/03-架构类代理.md)
- [1.4 测试类代理](./docs/tutorials/zh/10-AI子代理系统/04-测试类代理.md)
- [1.5 运维类代理](./docs/tutorials/zh/10-AI子代理系统/05-运维类代理.md)
- [1.6 协作模式](./docs/tutorials/zh/10-AI子代理系统/06-协作模式.md)
- [1.7 实战项目](./docs/tutorials/zh/10-AI子代理系统/07-实战项目.md)

### 📝 命令参考指南

完整的 Claude Code 命令文档，包含所有内置命令的详细说明和使用示例：

| 类别 | 说明 | 链接 |
|:---|:---|:---:|
| 📋 命令索引 | 所有命令的完整列表和快速参考 | [查看](./docs/commands/README_CN.md) |
| 💼 会话管理 | clear, compact, exit, rewind | [示例](./docs/commands/examples/session-management/) |
| ⚙️ 项目配置 | config, init, memory, permissions | [示例](./docs/commands/examples/project-config/) |
| 🔄 工作流 | review, todos, export, pr_comments | [示例](./docs/commands/examples/workflow/) |
| 🤖 AI 代理 | agents, hooks, mcp, bashes | [示例](./docs/commands/examples/agents/) |
| 📊 上下文 | context, cost, usage | [示例](./docs/commands/examples/context/) |
| 👤 账户 | login, logout, privacy-settings | [示例](./docs/commands/examples/account/) |
| 🔧 系统 | status, doctor, bug, model | [示例](./docs/commands/examples/system/) |
| 🚀 高级 | sandbox, vim, statusline, terminal-setup | [示例](./docs/commands/examples/advanced/) |

---

## 🎓 学习路线建议

### 零基础用户
```
第1课 → 第2课 → 第3课 → 第4课 → 第6课（实战）
预计学习时间：2-3 周
```

**学习重点：**
- 理解基本概念和工作原理
- 掌握基础命令和文件操作
- 完成一个完整的实战项目
- 建立 AI 辅助编程的思维模式

### 有编程基础用户
```
第1课（快速浏览）→ 第2课 → 第4课 → 第5课 → 第6课 → 第7课 → 第8课 → 第9课 → 第10课
预计学习时间：1-2 周
```

**学习重点：**
- 快速上手基础操作
- 深入学习进阶技巧
- 掌握提示词优化
- 配置 AI 子代理系统

### 专业开发者
```
第2课（安装）→ 第5课 → 第7课 → 第8课 → 第9课（必学）→ 第10课（必学）→ 第12课 → 第13课 → 第14课
预计学习时间：3-5 天
```

**学习重点：**
- 高级特性和最佳实践
- 提示词优化技巧（效率关键）
- AI 子代理系统（团队协作）
- MCP 服务器集成
- 生产环境实践

---

## 💡 学习建议

### 基本原则
1. ✅ **按顺序学习** - 后面的课程会用到前面的知识
2. ✅ **动手实践** - 每课都有练习任务，一定要自己做
3. ✅ **不要跳过** - 即使觉得简单，也要过一遍
4. ✅ **多提问** - 遇到不懂的，直接问 Claude Code
5. ✅ **做笔记** - 记录常用命令和技巧
6. ✅ **创建项目** - 学完每个阶段，做一个小项目巩固

### 高效技巧
- 📌 **使用命令参考** - 随时查阅 [命令索引](./docs/commands/README_CN.md)
- 📌 **参考示例** - 遇到问题先看 [命令示例](./docs/commands/examples/)
- 📌 **建立工作流** - 参考 [最佳实践](./docs/tutorials/zh/12-最佳实践.md)
- 📌 **优化提示词** - 学习 [提示词技巧](./docs/tutorials/zh/09-提示词优化技巧.md)

---

## 🎯 学习目标

完成本教程后，你将能够：

- ✅ 熟练使用 Claude Code 进行日常开发
- ✅ 独立完成前端和后端项目
- ✅ 运用最佳实践编写高质量代码
- ✅ 设计和实现复杂的应用架构
- ✅ 配置和使用 MCP 服务器扩展功能
- ✅ 创建专业的 AI 子代理团队
- ✅ 建立完整的开发工作流
- ✅ **使用 AI 提升 10 倍开发效率**

---

## 📚 扩展资源

### 官方资源
- 📖 [Claude Code 官方文档](https://docs.claude.com/en/docs/claude-code)
- 🐙 [GitHub 仓库](https://github.com/anthropics/claude-code)
- 🐛 [问题反馈](https://github.com/anthropics/claude-code/issues)

### 推荐文章

#### 1. Claude Code 优化指南
别再瞎写提示词了！这份 Claude Code 优化指南让你效率提升 10 倍

🔗 [查看文章](https://juejin.cn/post/7539544124669870115)

#### 2. Claude Code AI 子代理集合
为 Claude Code 提供 83 个专业 AI 子代理的综合集合，涵盖软件开发、基础设施和业务运营领域的专业知识

🔗 [GitHub 仓库](https://github.com/wshobson/agents)

#### 3. AI 工作流实战
耗时 1 年，终于拥有属于自己的 AI 工作流

🔗 [查看文章](https://aicoding.juejin.cn/post/7551359585900331060)

#### 4. AI 编程出海实践
AI 编程出海不知道做什么？通过这个方法，有人月入 10 万

🔗 [查看文章](https://aicoding.juejin.cn/post/7553598949196021812)

### 社区资源
- 💬 [Telegram 群组](https://t.me/fnzero_group)
- 💬 [Discord 服务器](https://discord.gg/vuazbGkqQE)
- 🌐 [官方网站](https://fnzero.dev/)

---

## 🚀 开始学习

准备好了吗？选择适合你的学习路线：

| 经验水平 | 推荐起点 | 预计时间 |
|:---:|:---|:---:|
| 零基础 | [第一课：什么是 Claude Code？](./docs/tutorials/zh/01-基础概念.md) | 2-3 周 |
| 有基础 | [第二课：安装和配置](./docs/tutorials/zh/02-安装和配置.md) | 1-2 周 |
| 专业级 | [第九课：提示词优化技巧](./docs/tutorials/zh/09-提示词优化技巧.md) | 3-5 天 |

或者直接查看：
- 📋 [命令参考指南](./docs/commands/README_CN.md) - 快速查找命令
- 💡 [命令使用示例](./docs/commands/examples/) - 学习实际用法
- 🎯 [最佳实践](./docs/tutorials/zh/12-最佳实践.md) - 官方推荐方法

---

## 📞 获取帮助

### 遇到问题？
- 💬 直接在项目中问 Claude Code
- 🔍 搜索 [命令参考指南](./docs/commands/README_CN.md)
- 📖 查看 [完整使用指南](./docs/tutorials/zh/14-完整使用指南.md)
- 🐛 提交 [Issue](https://github.com/0xfnzero/AI-Code-Tutorials/issues)

### 想要贡献？
- 💡 有建议？欢迎 Pull Request
- 📝 发现错误？提交 Issue
- 🌟 觉得有用？给个 Star 支持

---

## 🤝 贡献指南

我们欢迎所有形式的贡献！

### 如何贡献
1. Fork 本仓库
2. 创建你的特性分支 (`git checkout -b feature/AmazingFeature`)
3. 提交你的更改 (`git commit -m 'Add some AmazingFeature'`)
4. 推送到分支 (`git push origin feature/AmazingFeature`)
5. 开启一个 Pull Request

### 贡献类型
- 📝 改进文档和教程
- 🐛 修复错误和问题
- 💡 添加新的示例和技巧
- 🌍 翻译成其他语言
- ✨ 提出新功能建议

---

## 📊 项目统计

- ✅ **14 节完整课程** - 从入门到精通
- ✅ **40+ 个子模块** - 详细的专题讲解
- ✅ **30+ 个命令** - 完整的命令参考
- ✅ **8 个命令类别** - 系统化的命令分类
- ✅ **中英双语** - 支持中文和英文
- ✅ **持续更新** - 跟进最新版本

---

## 📄 许可证

本教程遵循 [MIT 许可证](./LICENSE)，欢迎自由使用和分享。

---

## 🌟 Star History

如果这个教程对你有帮助，请给个 Star 支持一下！

[![Star History Chart](https://api.star-history.com/svg?repos=0xfnzero/AI-Code-Tutorials&type=Date)](https://star-history.com/#0xfnzero/AI-Code-Tutorials&Date)

---

<div align="center">
    <p><strong>Made with ❤️ by the Claude Code Community</strong></p>
    <p>
        <a href="https://fnzero.dev/">Website</a> •
        <a href="https://t.me/fnzero_group">Telegram</a> •
        <a href="https://discord.gg/vuazbGkqQE">Discord</a>
    </p>
</div>

---

⭐ **如果这个教程对你有帮助，请给个 Star 支持一下！**
