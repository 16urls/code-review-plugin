# 🧠 Code Review Plugin for Claude Code

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
[![Claude Code](https://img.shields.io/badge/Claude%20Code-Plugin-blue)](https://docs.claude.com/claude-code)

> An AI-powered code review plugin for **Claude Code**. Automatically surfaces potential issues in local development, team collaboration, and CI workflows — and emits a structured, actionable review report.

**中文版**: [README.md](README.md)

## ✨ Features

- 🔍 **Zero-config** — Works out of the box, auto-detects `git diff`
- 🛡 **Runs locally** — No external services, your code never leaves your machine
- 🌐 **Multi-language** — TypeScript / JavaScript / Python / Go / Rust / PHP and more
- 📊 **Structured output** — Markdown table grouped by severity, with fix snippets
- ⚡ **Multiple triggers** — Slash command / natural language / auto-loaded skill

## 📦 Plugin Layout

This plugin follows the recommended Claude Code plugin structure:

```text
code-review-plugin/
├── .claude-plugin/
│   ├── plugin.json           # Plugin manifest
│   └── marketplace.json      # Marketplace manifest
├── skills/
│   └── code-review/
│       └── SKILL.md          # Code review skill
├── docs/
│   └── images/               # Screenshots
├── CHANGELOG.md
├── LICENSE
└── README.md
```

## 🚀 Installation

### Option 1: Install from GitHub (recommended)

In a Claude Code session:

```bash
> /plugin marketplace add 16urls/code-review-plugin
> /plugin install code-review-plugin@16urls
```

> Full URL form also works: `/plugin marketplace add https://github.com/16urls/code-review-plugin`

### Option 2: Local development

```bash
git clone https://github.com/16urls/code-review-plugin.git
```

Then register the local directory as a marketplace and install:

```bash
# Note: `marketplace add` expects the absolute path of the repo you just cloned
# i.e. the code-review-plugin/ subdirectory under wherever you ran `git clone`
# Example (macOS/Linux): /Users/alice/code-review-plugin
# Example (Windows):     C:\Users\Alice\code-review-plugin
> /plugin marketplace add <absolute path of the cloned repo>
> /plugin install code-review-plugin@16urls
```

> The install command follows `<plugin>@<marketplace>`. This repo's marketplace is named `16urls` (matching the GitHub owner) and the plugin name is `code-review-plugin`.

## 🛠 Usage

### Option 1: Slash command (recommended)

```bash
> /code-review
```

> If the command name collides with another plugin, use the namespaced form: `/code-review-plugin:code-review`

### Option 2: Natural language

The skill auto-loads from context. Just say:

- "Review my last commit"
- "Audit this file for security issues"
- "Do a code review on the staged changes"

Claude will load the `code-review` skill and produce a structured report. To force the skill, mention it explicitly: "use the code-review skill to review …".

## 🖼 Demo

Invoking `/code-review`:

![Invoke /code-review](docs/images/usage-slash-1.png)

Skill auto-loaded and analysis in progress:

![Skill analyzing](docs/images/usage-slash-2.png)

The structured review report:

![Review report](docs/images/usage-slash-3.png)

## 📊 Review Dimensions

The plugin reviews code along three dimensions:

- 🔴 **Critical** — Bugs, security vulnerabilities (SQLi / XSS), null dereferences, data leak risks
- 🟡 **Warning** — Concurrency, edge cases, performance bottlenecks
- 🟢 **Suggestion** — Readability, naming, architecture

## 📝 Output Format

A Markdown table containing:

- Severity (🔴 🟡 🟢)
- File:line
- Issue description
- Fix suggestion (with code snippet)

Example:

```markdown
## Code Review Report

| Severity | File:Line | Issue | Fix |
|----|----|----|----|
| 🔴 | `auth.ts:45` | Null deref risk: token not checked | Add `if (!token) throw new Error(...)` |
```

## 📌 Notes

- Make sure the project is a git repo (`git init`) so the skill can read the diff.
- The plugin makes no external network calls — code stays on your machine.
- Supports TypeScript, JavaScript, Python, Go, Rust, PHP, and other mainstream languages.

## 🤝 Contributing

Issues and Pull Requests are welcome:

- False-positive fixes
- New language support
- Output format improvements

GitHub: https://github.com/16urls/code-review-plugin

## 📄 License

[MIT License](LICENSE) © 2026 16urls

## ⚠️ Disclaimer

- The initial version of the skill prompt was drafted with the help of [Tencent Yuanbao](https://yuanbao.tencent.com/) and has been validated by the author across multiple language projects.
- Review results are **advisory only** and do not replace human review or professional security audits.
- The author accepts no liability for any direct or indirect loss arising from the use of this plugin; please assess the risk before use.
