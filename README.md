# 🧠 Code Review Plugin for Claude Code

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
[![Claude Code](https://img.shields.io/badge/Claude%20Code-Plugin-blue)](https://docs.claude.com/claude-code)

> 一个为 **Claude Code** 打造的 AI 代码审查插件。在本地、团队协作或 CI 场景下，自动发现代码中的潜在问题，输出结构化、可执行的审查报告。

**English version**: [README.en.md](README.en.md)

## ✨ 特性

- 🔍 **零配置** — 安装即用，自动识别 git diff
- 🛡 **本地运行** — 不依赖任何外部服务，代码不出本机
- 🌐 **多语言** — TypeScript / JavaScript / Python / Go / Rust / PHP 等主流语言
- 📊 **结构化输出** — 按严重程度分级的 Markdown 表格 + 修复代码片段
- ⚡ **多种触发方式** — 斜杠命令 / 自然语言 / Skill 自动加载

## 📦 插件结构

本插件采用 Claude Code 官方推荐的 Plugin 结构：

```text
code-review-plugin/
├── .claude-plugin/
│   ├── plugin.json           # 插件元信息
│   └── marketplace.json      # 插件市场清单
├── skills/
│   └── code-review/
│       └── SKILL.md          # 代码审查 Skill
├── docs/
│   └── images/               # 使用演示截图
├── CHANGELOG.md
├── LICENSE
└── README.md
```

## 🚀 安装方式

### 方式一：从 GitHub 安装（推荐）

在 Claude Code 会话中执行：

```bash
> /plugin marketplace add 16urls/code-review-plugin
> /plugin install code-review-plugin@16urls
```

> 也可以使用完整 URL：`/plugin marketplace add https://github.com/16urls/code-review-plugin`

### 方式二：本地开发测试

```bash
git clone https://github.com/16urls/code-review-plugin.git
```

在 Claude Code 会话中把本地目录注册为 marketplace 后安装：

```bash
> /plugin marketplace add /absolute/path/to/code-review-plugin
> /plugin install code-review-plugin@16urls
```

> 安装命令格式为 `<插件名>@<marketplace 名>`。本仓库的 marketplace 名为 `16urls`（与 GitHub owner 一致），插件名为 `code-review-plugin`。

## 🛠 使用方法

### 方式一：斜杠命令（推荐）

在 Claude Code 会话中直接输入：

```bash
> /code-review
```

> 若与其他插件命令重名，可使用插件命名空间显式调用：`/code-review-plugin:code-review`

### 方式二：自然语言自动触发

Skill 会根据上下文自动加载。在 Claude Code 会话中直接说：

- "帮我 review 一下刚才的 commit"
- "检查这段代码有没有 security 问题"
- "帮我做一下代码审查"

Claude 会自动加载 `code-review` skill，对当前代码上下文进行审查，并输出结构化报告。如需强制触发，也可以在提示中明确说 "用 code-review skill 审查 …"。

## 🖼 使用演示

调用 `/code-review` 后的实际效果：

![调用 code-review 命令](docs/images/usage-slash-1.png)

Skill 自动加载并分析代码：

![Skill 分析过程](docs/images/usage-slash-2.png)

输出结构化的审查报告：

![审查报告示例](docs/images/usage-slash-3.png)

## 📊 审查维度

插件会从以下三个维度对代码进行分析：

- 🔴 **严重问题**：Bug、安全漏洞（SQL 注入 / XSS）、空指针、数据泄露风险
- 🟡 **风险点**：并发问题、边界条件、性能瓶颈
- 🟢 **改进建议**：代码可读性、命名规范、架构合理性

## 📝 输出格式

输出为 Markdown 表格，包含：

- 级别（🔴 🟡 🟢）
- 文件路径 + 行号
- 问题描述
- 修复建议（含代码示例）

示例：

```markdown
## Code Review Report

| 级别 | 文件:行 | 问题描述 | 修复建议 |
|----|----|----|----|
| 🔴 | `auth.ts:45` | 空指针风险：未校验 token 是否为 null | 增加 `if (!token) throw new Error(...)` |
```

## 📌 注意事项

- 请确保你的项目已初始化 Git（`git init`），以便 skill 能读取 diff。
- 本插件不依赖外部服务，纯本地运行，保障代码隐私。
- 支持 TypeScript、JavaScript、Python、Go、Rust、PHP 等主流语言。

## 🤝 贡献与反馈

欢迎提交 Issue 或 Pull Request：

- 修复误报
- 增加新语言支持
- 优化输出格式

GitHub 仓库：https://github.com/16urls/code-review-plugin

## 📄 License

[MIT License](LICENSE) © 2026 16urls

## ⚠️ 免责声明

- 本插件的 Skill 提示词初始版本由 [腾讯元宝](https://yuanbao.tencent.com/) 协助生成，作者已在多种语言项目中实测可用。
- 代码审查结果**仅供参考**，不能替代人工 review 与专业安全审计。
- 对于因使用本插件而产生的任何直接或间接损失，作者不承担责任，使用前请自行评估风险。
