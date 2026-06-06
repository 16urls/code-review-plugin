# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

## [1.1.0] - 2026-06-06

### Added

- **SKILL.md 步骤 0：git 环境检查**
  - 先检测 `git --version`，未安装时输出中文提示 + git 官网下载地址，并立即终止
  - 当前目录不是 git 仓库时（`git rev-parse --is-inside-work-tree` 返回非真），输出中文提示要求 `git init`，并立即终止
  - 用户在请求中显式指定文件路径时，可跳过 git 检查
- 步骤 1 新增回退：`git diff HEAD` 为空时尝试 `git diff HEAD~1 HEAD` 审查最近一次 commit
- 两个 manifest 增加 `$schema` 引用，IDE 提供字段补全与实时校验
- 英文版 README（`README.en.md`），便于海外用户与官方 marketplace 收录评审
- `CHANGELOG.md`，按 Keep a Changelog 规范记录版本变更
- `.gitignore`，忽略 IDE 与系统生成文件
- `docs/SUBMIT.md`，记录 marketplace 投稿流程与 PR 模板

### Changed

- README 重构：新增「特性」徽章，免责声明独立成节
- README 的 marketplace 注册示例与 `marketplace.json` 中的 `name: "16urls"` 对齐
- `plugin.json`：补充 `homepage` / `bugs` / `author.url`，`category` 字段从 marketplace 条目迁移到 plugin 本体，`description` 与 `keywords` 扩充
- `marketplace.json`：marketplace `name` 由 `code-review-plugin` 改为 `16urls`，与 GitHub owner 一致；安装命令变为 `code-review-plugin@16urls`

### Fixed

- 移除 `plugin.json` 中无效的 `skills` 字段（skills 由 Claude Code 从 `skills/*/SKILL.md` 自动发现）

## [1.0.0] - 2026-06-06

### Added

- 首个公开版本
- `code-review` Skill：
  - 自动读取 `git diff HEAD` 作为审查范围
  - 三档严重度（🔴 严重 / 🟡 警告 / 🟢 建议）
  - 输出 Markdown 表格 + 针对性修复代码片段
  - 覆盖 TypeScript / JavaScript / Python / Go / Rust / PHP 等主流语言
- 插件 manifest：`.claude-plugin/plugin.json`
- Marketplace 清单：`.claude-plugin/marketplace.json`（marketplace name: `16urls`）
- `docs/images/` 使用演示截图

[Unreleased]: https://github.com/16urls/code-review-plugin/compare/v1.1.0...HEAD
[1.1.0]: https://github.com/16urls/code-review-plugin/releases/tag/v1.1.0
[1.0.0]: https://github.com/16urls/code-review-plugin/releases/tag/v1.0.0
