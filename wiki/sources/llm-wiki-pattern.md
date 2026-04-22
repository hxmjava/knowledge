---
title: LLM Wiki
type: source
status: active
updated: 2026-04-22
source_count: 1
---

# Source: LLM Wiki

## Metadata

- Raw file: `raw/sources/llm-wiki.md`
- Author: unknown (idea note)
- Date: unknown
- Format: markdown idea document

## Summary

- 提出一种区别于传统 RAG 的模式：通过 LLM 持续维护“持久化 wiki”，而非每次问答都从原始文档重新检索与拼接。
- 知识库由三层组成：不可变原始资料层、LLM 维护的 wiki 层、约束行为的 schema 层（如 `AGENTS.md`）。
- 工作流分为 ingest/query/lint，强调每次操作都更新 `index.md` 与 `log.md`，实现可导航与可审计。
- 用户负责选材与提问，LLM 负责总结、交叉链接、矛盾标注和多页维护，从而降低知识管理维护成本。

## Key Claims

- “编译式知识库”优于“每次重算式回答”，因为跨文档综合会沉淀到 wiki 中并持续复用。
- 维护负担是知识库失败主因之一，LLM 可显著降低该负担并保持结构一致性。
- 在中等规模下，内容型索引（`index.md`）可替代复杂 RAG 基础设施。

## Practical Workflow Notes

- Ingest 单次常触达 5-15 个页面，优先一篇篇处理并保持人类在回路中。
- Query 结果如果有长期价值，应回写为 `wiki/analyses/` 页面以形成复利。
- Lint 定期检查矛盾、陈旧结论、孤儿页、缺失概念页和交叉链接机会。

## Contradictions / Tensions

- 文档主张“可不依赖检索基础设施”，但同时建议规模增长后可引入搜索引擎（如 qmd）；两者并非冲突，而是规模阶段差异。
- 文档强调抽象通用性，因此具体实现细节（命名、字段、工具）需要在本地实践中逐步收敛。

## Linked Entities

- [[entities/llm-agent]]
- [[entities/obsidian]]

## Linked Concepts

- [[concepts/persistent-wiki-compilation]]
- [[concepts/ingest-query-lint-loop]]
- [[concepts/schema-driven-maintenance]]
