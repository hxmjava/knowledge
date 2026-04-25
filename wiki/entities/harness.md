---
name: Harness
description: Multi-agent collaboration layer that orchestrates layer-specific agents, specialized skills, and lifecycle hooks for AI-assisted development.
type: entity
status: draft
updated: 2026-04-24
source_count: 1
---

# Entity: Harness

## What It Is

Harness 是多 Agent 协作层，负责将「分层专用 Agent + 专项检查技能 + 生命周期 Hooks + 斜杠命令编排」整合为一套可操作的项目工作流。它不替代 OpenSpec（规范）或 Superpowers（纪律），而是负责「谁来做、如何并行、如何兜底」。

## Relevance

在 ai_template2 脚手架中，Harness 是连接 OpenSpec 规格与 Superpowers 纪律的中间层：读取 OpenSpec 变更 → 按 AGENTS.md 划定模块与风险 → 用 Superpowers 约束实现过程 → 用构建工具做硬门禁 → 回到 OpenSpec 做验收或归档。

## Key Facts

- 提供 4 个分层 Agent：proj-app-agent、proj-common-agent、proj-service-agent、proj-message-agent，各负责对应层内的改动。
- 提供 6 个专项检查技能：api-change-checker、orm-change-checker、xml-config-checker、message-consumer-checker、build-module-verifier、test-bootstrap。
- 提供 9 个斜杠命令作为编排入口，其中 `/proj-dev` 是日常开发主流程。
- 提供 4 个生命周期 Hooks（PreToolUse / PostToolUse / PostToolUseFailure / Stop），通过 Python 脚本实现轻量提醒，默认 fail-open 不阻断。
- 不同业务域无共享表/实体耦合时可并行；触及 common 层或根构建文件应串行。
- 高风险区域变更必须写明执行的构建命令及结果。

## Relationships

- Related entities: [[entities/openspec]], [[entities/superpowers]], [[entities/claude-code]]
- Related concepts: [[concepts/layered-project-harness]], [[concepts/specialized-agent-pattern]], [[concepts/hooks-as-safety-net]], [[concepts/team-governance-for-ai-coding]]

## Evidence

- [[sources/ai-template2-scaffold]]

## Open Questions

- 在不同编辑器（Cursor / Codex / Claude Code）之间，Harness 命令如何统一？
- Hooks fail-open 是否适合安全敏感项目？是否应在特定场景改为 fail-closed？
