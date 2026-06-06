# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

### Added

- 英文版 README（`README.en.md`），便于海外用户与官方 marketplace 收录评审
- `CHANGELOG.md`，按 Keep a Changelog 规范记录版本变更
- `.gitignore`，忽略 IDE 与系统生成文件

### Changed

- README 重构：新增「特性」徽章，免责声明独立成节
- README 的 marketplace 注册示例与 `marketplace.json` 中的 `name: "16urls"` 对齐

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

[Unreleased]: https://github.com/16urls/code-review-plugin/compare/v1.0.0...HEAD
[1.0.0]: https://github.com/16urls/code-review-plugin/releases/tag/v1.0.0
