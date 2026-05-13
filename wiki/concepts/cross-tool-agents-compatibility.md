---
title: 跨工具 AGENTS.md 兼容
type: concept
status: active
updated: 2026-05-12
source_count: 1
---

# Concept: 跨工具 AGENTS.md 兼容（Cross-Tool AGENTS.md Compatibility）

## Definition

将 AGENTS.md 作为项目指令的**单一事实来源（SSOT）**，通过符号链接或引用机制使 Cursor、Codex、Claude Code 等多个 AI 编码工具共享同一份规则文件，避免多套文档漂移。

## Why It Matters

开发者在不同 AI 编码工具间切换（Cursor ↔ Codex ↔ Claude Code）时，如果每个工具维护独立的规则文件（`.cursorrules`、`CLAUDE.md`、`AGENTS.md`），规则极易漂移——同一项目在不同工具中的行为不一致，团队成员间的行为也可能不一致。统一的 AGENTS.md + 符号链接策略消除了这一问题。

## 跨工具兼容矩阵（2026 年 5 月）

| 工具 | 支持文件 | 推荐集成方式 |
|------|---------|------------|
| Cursor | `AGENTS.md` + `.cursor/rules/*.mdc` | 根目录 `AGENTS.md` + 细粒度 `.cursor/rules` |
| Codex | `AGENTS.md`（支持多层级） | repo-root + `~/.codex/AGENTS.md` 全局 |
| Claude Code | `CLAUDE.md` | `ln -s AGENTS.md CLAUDE.md` |
| 其他工具 | 视情况 | 以 `AGENTS.md` 为 SSOT |

## 分层集成策略

```
AGENTS.md（SSOT）
├── .cursor/rules/*.mdc    ← Cursor 细粒度规则
├── CLAUDE.md → AGENTS.md  ← Claude Code 符号链接
└── ~/.codex/AGENTS.md     ← Codex 全局指令
```

关键原则：
- AGENTS.md 只写**通用的项目级规则**
- 工具特有功能（如 Cursor 的 `.mdc` 规则触发条件、Claude Code 的 skills/hooks）放在各自目录
- 两层内容不应互相矛盾——工具层是对 SSOT 的补充，不是替代

## Supporting Sources

- [[sources/agents-md-cars-guide]]

## Related Pages

- [[entities/agents-md]]
- [[entities/claude-code]]
- [[entities/cursor]]（待创建）
- [[concepts/spec-driven-workflow-and-review-discipline]]

## Contradictions / Nuance

- 符号链接在 Windows 上需要管理员权限或开发者模式——不是所有团队成员都能轻松设置。
- 不同工具对 AGENTS.md 的**解析深度和注入方式**存在差异——Cursor 可能通过 rules 系统部分覆盖 AGENTS.md 内容，Claude Code 则完整注入 CLAUDE.md。这种差异可能导致同一份文件在不同工具中的实际效果不一致。
- Claude Code 除了 CLAUDE.md 外还支持 `.claude/` 目录下的 skills、hooks、settings——这些能力无法通过 AGENTS.md 符号链接覆盖，需要单独配置。
