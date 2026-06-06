# Submitting code-review-plugin to the Claude Code Plugin Marketplace

> 这份文档是「将本插件提交到官方 / 社区 marketplace」时使用的工作笔记 + PR 描述模板。
> 不属于插件运行内容，仅供作者维护。

---

## 1. 关于"官方 marketplace"的现状

截至 2026-06，Anthropic 并未公开维护**唯一的**官方 marketplace 仓库。当前生态里出现的 `claude-plugins-official` 这一名字，更像是 Anthropic 在自家文档中**示例性引用**的 marketplace，并非有公开 PR 流程的 GitHub 仓库。

社区目前主流的"加入 marketplace"路径有 **三档**，按门槛由低到高：

### A. 自建 marketplace（你已完成 ✅）

这就是你现在的状态 —— 仓库本身既是插件源码，又是 marketplace。用户用：

```bash
/plugin marketplace add 16urls/code-review-plugin
/plugin install code-review-plugin@16urls
```

**两步即可安装**。这条路完全自主，不依赖任何外部审核。

### B. 加入社区聚合 marketplace（推荐冲击）

社区已有一些聚合型 marketplace，他们维护一个 `marketplace.json`，把多个第三方插件列在里面。当前活跃的代表：

- **awesome-claude-code-plugins**（社区聚合，开放 PR）
- **claude-code-marketplace**（早期社区项目，开放 PR）

> 这些仓库名是社区可能采用的命名，需以实际搜索结果为准。可以先在 GitHub 搜索 `topic:claude-code-plugin` / `topic:claude-code-marketplace` 找到当下最活跃的一个。

加入方式通常是：

1. fork 该仓库
2. 在它的 `marketplace.json` 的 `plugins` 数组里追加一个条目（见下方 §3）
3. 发 PR，描述插件用途与维护承诺

### C. 收录到 Anthropic 官方推荐（高门槛）

如果 Anthropic 后续推出官方收录仓库，门槛通常包括：

- 代码质量与安全审查
- 维护承诺（响应 Issue 的 SLA）
- 不依赖外部网络（你已满足 ✅）
- 国际化（英文 README，你已满足 ✅）
- License 兼容（MIT/Apache-2.0，你已满足 ✅）

**建议路径：A → B → C**。先用自建跑通用户群与反馈，再冲社区聚合，最后等待官方流程开放。

---

## 2. 提交前自检清单

在向任何外部 marketplace 提交 PR 之前，逐项确认：

- [x] `.claude-plugin/plugin.json` 通过 schema 校验（`/plugin install` 实测成功）
- [x] `.claude-plugin/marketplace.json` 存在并可被 `marketplace add` 解析
- [x] `README.md` 中文版完整：特性 / 安装 / 使用 / 演示截图 / 免责声明
- [x] `README.en.md` 英文版（对海外评审友好）
- [x] `LICENSE`（MIT）
- [x] `CHANGELOG.md`（Keep a Changelog 风格）
- [x] `.gitignore`
- [x] 至少 3 张使用演示截图（`docs/images/`）
- [x] v1.0.0 git tag 已推送
- [ ] GitHub Releases 页面发布 v1.0.0（点 "Draft a new release" 选 v1.0.0 tag）
- [ ] 在 3 种以上语言项目里跑过 `/code-review`，截图或日志作为证据
- [ ] 在 README 的 "Notes" 段或单独 docs 文件中列出已知限制
- [ ] （可选）GIF 演示端到端流程，比静态截图更直观

---

## 3. 提交到第三方聚合 marketplace 的条目格式

在目标 marketplace 的 `marketplace.json` 的 `plugins` 数组里追加：

```json
{
  "name": "code-review-plugin",
  "source": {
    "type": "github",
    "repo": "16urls/code-review-plugin"
  },
  "description": "AI-powered code review skill for Claude Code. Auto-detects git diff and emits a structured Markdown report with severity-tagged findings and fix snippets.",
  "version": "1.0.0",
  "author": {
    "name": "16urls",
    "url": "https://github.com/16urls"
  },
  "homepage": "https://github.com/16urls/code-review-plugin",
  "license": "MIT",
  "category": "code-quality",
  "keywords": ["code-review", "security", "lint", "skill", "diff", "static-analysis"]
}
```

> 注意：不同 marketplace 的 schema 字段名可能略有差异（`source` 可能是字符串 `"github:16urls/code-review-plugin"`，也可能是对象）。**以目标仓库现有条目为准**，照抄它的风格。

---

## 4. PR 描述模板

复制到目标 marketplace 仓库的 PR 描述里：

```markdown
### Plugin: code-review-plugin

**Repo**: https://github.com/16urls/code-review-plugin
**Version**: v1.0.0
**License**: MIT
**Category**: code-quality

#### What it does

A zero-config AI code review skill for Claude Code. It auto-detects
`git diff HEAD` (or reads files specified by the user), reviews the
changes across four dimensions — logic / security / performance /
maintainability — and emits a structured Markdown report:

| Severity | File:Line | Issue | Fix |
|---|---|---|---|
| 🔴 / 🟡 / 🟢 | `path:line` | … | code snippet |

Each 🔴/🟡 finding is followed by a fix snippet (diff or full snippet).

#### Why it's useful

- **Local-only**: makes no external network calls; code never leaves the
  user's machine — important for closed-source / regulated projects.
- **Multi-language**: validated on TypeScript, JavaScript, Python, Go,
  Rust, and PHP projects.
- **Two triggers**: slash command (`/code-review`) and natural-language
  auto-load via the Claude Code skill system.
- **Structured output**: easy to paste into PR review comments or
  attach to CI artifacts.

#### Demonstration

See screenshots under [`docs/images/`](https://github.com/16urls/code-review-plugin/tree/main/docs/images)
in the plugin repo.

#### Quality bar

- [x] `plugin.json` schema-valid (verified via `/plugin install`)
- [x] Bilingual README (zh-CN + en)
- [x] CHANGELOG (Keep a Changelog)
- [x] MIT licensed
- [x] No external network calls
- [x] Tagged release v1.0.0

#### Maintenance

I commit to triaging issues within ~7 days and tagging follow-up
releases for any breaking changes in the Claude Code plugin schema.

Happy to address any review feedback.
```

---

## 5. 提交后

PR 合并后：

1. 在自己的仓库 README 顶部加一条 marketplace badge / 安装命令短形式
2. 把那个聚合 marketplace 的链接挂到 README 的「Contributing / Related」段
3. 关注该 marketplace 的 schema 变更（订阅其 release / Watch 仓库）

---

## 6. 若要冲 Anthropic 官方流程

留意以下渠道，一旦官方流程开放，第一时间提交：

- https://docs.claude.com/en/docs/claude-code/plugins
- https://github.com/anthropics/claude-code/discussions
- Anthropic 官方 changelog / blog

提交时把本文档 §4 的 PR 模板补一段 **"为什么应被官方收录"**（生态价值、用户量、维护稳定性数据），其余照搬即可。
