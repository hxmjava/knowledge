---
title: Ingest Query Lint Loop
type: concept
status: active
updated: 2026-04-22
source_count: 1
---

# Concept: Ingest Query Lint Loop

## Definition

以 ingest、query、lint 三种循环操作驱动知识库持续增长与结构修复。

## Why It Matters

把“输入-使用-维护”统一为闭环流程，避免知识库只增不修导致失真和可用性下降。

## Core Components

- Ingest：录入新 source，并更新相关页面、index、log
- Query：从 wiki 作答，并把高价值结论沉淀为 analysis
- Lint：系统检查矛盾、陈旧、孤儿页和覆盖缺口

## Supporting Sources

- [[sources/llm-wiki-pattern]]

## Related Pages

- [[concepts/persistent-wiki-compilation]]
- [[concepts/schema-driven-maintenance]]
- [[entities/llm-agent]]

## Contradictions / Nuance

- 自动化程度越高越省时，但人类参与审阅可提高方向正确性和结论质量。
