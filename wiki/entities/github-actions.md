---
title: GitHub Actions
type: entity
status: active
updated: 2026-04-22
source_count: 1
---

# Entity: GitHub Actions

## What It Is

GitHub Actions 是 GitHub 提供的自动化工作流平台，可将 AI 审查、安全检查和文档生成纳入 CI/CD 流水线。

## Relevance

在本模式里，它是将“LLM 能力”从聊天界面迁移到工程流程中的关键执行层。

## Key Facts

- 可按事件触发（PR、评论、push）执行不同作业。
- 可与 `anthropics/claude-code-action` 配合实现自动审查与安全扫描。
- 通过 `permissions`、secrets 与 job 拆分实现最小权限和可追踪审查流程。

## Relationships

- Related entities: [[entities/claude-code]]
- Related concepts: [[concepts/ai-ci-cd-automation]], [[concepts/policy-driven-tool-permissions]]

## Evidence

- [[sources/claude-code-enterprise-playbook]]

## Open Questions

- 当前团队应优先启用哪些最小工作流以平衡收益与维护成本。
