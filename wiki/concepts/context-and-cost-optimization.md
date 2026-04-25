---
title: Context and Cost Optimization
type: concept
status: active
updated: 2026-04-25
source_count: 2
---

# Concept: Context and Cost Optimization

## Definition

通过上下文精简、任务拆分、调试可观测与模型选型，控制 AI 编码系统的响应性能与调用成本。

## Why It Matters

在企业长期使用中，性能与成本不是附属指标，而是系统能否持续运行的约束条件。

## Core Components

- 精简 `CLAUDE.md` 与分层配置
- 控制会话上下文规模（清理历史、拆分大任务）
- 使用 `--verbose` 定位瓶颈
- 按任务复杂度选择模型并设置预算阈值
- 使用渐进式披露检索历史上下文，先取摘要和最近上下文，再按需深入观察、文件或时间线

## Supporting Sources

- [[sources/claude-code-enterprise-playbook]]
- [[sources/claude-mem]]

## Related Pages

- [[entities/claude-code]]
- [[concepts/team-governance-for-ai-coding]]
- [[concepts/ingest-query-lint-loop]]
- [[concepts/progressive-disclosure-context-retrieval]]

## Contradictions / Nuance

- 追求极致低成本可能牺牲复杂问题质量；需按任务价值匹配模型与预算。
