---
title: Schema Driven Maintenance
type: concept
status: active
updated: 2026-04-22
source_count: 1
---

# Concept: Schema Driven Maintenance

## Definition

通过 `AGENTS.md` 之类的 schema 文档，把 LLM 的行为从“通用聊天”约束为“可执行的知识维护流程”。

## Why It Matters

没有 schema 时，输出容易漂移；有 schema 后，结构、命名、日志和质量检查可持续一致。

## Core Components

- 目录与页面类型约定
- ingest/query/lint 的步骤定义
- index/log 更新义务
- 质量门槛与人机分工

## Supporting Sources

- [[sources/llm-wiki-pattern]]

## Related Pages

- [[concepts/persistent-wiki-compilation]]
- [[concepts/ingest-query-lint-loop]]
- [[entities/llm-agent]]

## Contradictions / Nuance

- schema 过严会降低灵活性，过松会牺牲一致性；应随领域实践迭代。
