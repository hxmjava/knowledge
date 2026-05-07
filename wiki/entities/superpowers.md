---
title: Superpowers
type: entity
status: active
updated: 2026-05-07
source_count: 3
---

# Entity: Superpowers

## What It Is

Superpowers 是一套强调可组合工作流与纪律化执行的 AI 开发方法/能力集合，用于提升任务分解和交付可靠性。目标是把最佳实践变成 Agent 的默认行为，而不是"想起来再提醒"。

## Relevance

本文将其定位为"执行与工程纪律层"，与 OpenSpec 的规格层互补。OpenSpec 定方向，Superpowers 定计划与纪律。

## Key Facts

- 推荐七步工作流：
  1. **brainstorming** — 需求澄清（苏格拉底式提问）
  2. **using-git-worktrees** — 隔离工作区
  3. **writing-plans** — 拆成可执行的小步任务
  4. **subagent-driven-development** — 子代理执行 + 审查
  5. **test-driven-development** — 强制 TDD（RED → GREEN → REFACTOR）
  6. **requesting-code-review** — 代码审查，关键问题可阻塞
  7. **finishing-a-development-branch** — 收尾与合并选项
- 对"长任务 / 核心模块"默认走完整链路；对"一行 hotfix"可裁剪，但要在 PR/记录里写明例外原因。
- 要求在验证阶段逐任务产出可复核证据，避免"checkbox 即完成"的误判。
- 借助技能（skills）与 hooks 对流程自动化，减少"临时提醒式"规范执行。
- 新教程进一步强调”按需加载”而非”全量上技能”：先围绕 planning、Git Worktree、TDD、review 等核心能力形成最小组合，再逐步扩展。
- 14 个 skill 的四层架构（来自工作流拆解分析）：
  1. **总入口/流程控制**：`using-superpowers`、`brainstorming`、`writing-plans`
  2. **实施执行/环境隔离**：`using-git-worktrees`、`subagent-driven-development`、`executing-plans`、`dispatching-parallel-agents`
  3. **质量保障/问题处理**：`test-driven-development`、`systematic-debugging`、`requesting-code-review`、`receiving-code-review`、`verification-before-completion`
  4. **收尾/元能力**：`finishing-a-development-branch`、`writing-skills`
- 两条主链路：
  - **功能开发链**：`using-superpowers → brainstorming → writing-plans → worktrees → executing → finishing`
  - **调试链**：`using-superpowers → systematic-debugging → TDD → verification-before-completion`
- 目录结构：`plugins/superpowers/skills/<capability>/SKILL.md` 为核心，配合 `docs/superpowers/plans/` 和 `docs/superpowers/specs/`。
- 安装方式因编辑器而异：Cursor (`/add-plugin superpowers`)、Claude Code (`/plugin marketplace add obra/superpowers-marketplace`)、Codex（参考安装文档）。
- GitHub: https://github.com/obra/superpowers

## Relationships

- Related entities: [[entities/openspec]], [[entities/claude-code]]
- Related concepts: [[concepts/spec-driven-workflow-and-review-discipline]], [[concepts/team-governance-for-ai-coding]]

## Evidence

- [[sources/openspec-superpowers-practice-guide]]
- [[sources/ai-coding-advanced-openspec-superpowers-deep-guide]]
- [[sources/superpowers-workflow-deconstruction]]

## Open Questions

- 团队是否已定义”默认启用的核心技能集合”，避免安装后无人维护的大而全栈？
- subagent-driven-development 在你们仓库中的实际并行批次策略是什么？
- 四层架构是否可映射到 harness 的命令分层，实现配置即文档？
- 功能开发链路中发现 bug 需要切换到调试链路时，切换机制是什么？
