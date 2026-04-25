---
title: Persistent Wiki Compilation
type: concept
status: active
updated: 2026-04-25
source_count: 2
---

# Concept: Persistent Wiki Compilation

## Definition

将新资料增量“编译”进持久化 wiki，使综合结论和链接关系可复用、可演化，而非每次问答重新拼装。

## Why It Matters

减少重复检索与重复推理成本，提升复杂问题回答的一致性与累积质量。

Claude-Mem 这类系统补充了另一条路径：先自动保留跨会话工作记忆，再由人工或 agent 将高价值片段编译为稳定 wiki 页面。

## Core Components

- 原始资料不可变层（`raw/`）
- 可持续更新的结构化 wiki 层（`wiki/`）
- 约束流程与规范的 schema 层（`AGENTS.md`）

## Supporting Sources

- [[sources/llm-wiki-pattern]]
- [[sources/claude-mem]]

## Related Pages

- [[concepts/schema-driven-maintenance]]
- [[concepts/persistent-agent-memory]]
- [[entities/llm-agent]]
- [[entities/obsidian]]

## Contradictions / Nuance

- 小规模可仅靠 index 导航；规模上升后可逐步引入搜索工具，不必一开始就复杂化。
- 自动记忆不是自动知识库；wiki 仍负责稳定命名、来源追踪和综合判断。
