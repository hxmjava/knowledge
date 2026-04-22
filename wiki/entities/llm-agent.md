---
title: LLM Agent
type: entity
status: active
updated: 2026-04-22
source_count: 1
---

# Entity: LLM Agent

## What It Is

在该模式中，LLM Agent 不是一次性问答器，而是“知识库维护执行者”。

## Relevance

它承担跨页面更新、链接维护、矛盾标注和日志记录，是 wiki 复利增长的核心执行层。

## Key Facts

- 读 `raw/`，写 `wiki/`，并遵守 schema 约束。
- 一次 ingest 常会修改多个页面，而非只生成单页摘要。
- 在 query 阶段也会把高价值答案沉淀回 wiki。

## Relationships

- Related entities: [[entities/obsidian]]
- Related concepts: [[concepts/schema-driven-maintenance]], [[concepts/ingest-query-lint-loop]]

## Evidence

- [[sources/llm-wiki-pattern]]

## Open Questions

- 在多 agent 协作时如何做冲突合并与质量门禁。
