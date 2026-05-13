---
title: code-review-graph
type: entity
status: active
updated: 2026-05-11
source_count: 1
---

# Entity: code-review-graph

## What It Is

`code-review-graph` 是一个开源的本地代码结构图工具，用 Tree-sitter 解析代码仓库，将函数、类、导入、调用和测试关系存成 SQLite 图谱，并通过 MCP（Model Context Protocol）向 AI 编程助手暴露影响面查询能力。

## Relevance

该实体展示了 AI 编程基础设施从"让模型自己读代码"向"先给模型一张结构化地图"的演进方向，直接关联上下文成本优化和 MCP 生态扩展两个核心主题。

## Key Facts

- **包名**：`code-review-graph`（PyPI）
- **版本**：2.3.2（截至归档）
- **许可**：MIT
- **语言**：Python（主语言），要求 Python 3.10+
- **GitHub**：[tirth8205/code-review-graph](https://github.com/tirth8205/code-review-graph)（~15.3k Stars）
- **本地存储**：`.code-review-graph/` 目录（SQLite 文件）
- **核心流水线**：Tree-sitter 解析 → AST → SQLite 图谱（节点+边）→ BFS 影响面分析 → MCP 查询接口
- **增量更新**：基于文件变更 + SHA-256 校验，2,900 文件项目重索引 < 2 秒
- **语言覆盖**：23 种语言 + Jupyter/Databricks notebook（Python, TypeScript, Go, Rust, Java, C/C++, Swift, Kotlin, Svelte 等）
- **MCP 集成**：通过 MCP Server 暴露查询能力，支持 Claude Code、Cursor、Windsurf、Zed、Codex 等工具
- **Benchmark**：6 仓库 13 commits，平均 token 节省 8.2×；小型单文件变更可能开销更大（0.7×）
- **影响面准确率**：recall 100%，F1 0.54，precision 0.38——倾向"宁可多报，不漏"

## CLI 命令

```
pip install code-review-graph
code-review-graph install    # 检测本机 AI 工具，写入 MCP 配置
code-review-graph build      # 解析当前项目，构建图谱
code-review-graph update     # 增量更新图谱
code-review-graph watch      # 文件监听模式
code-review-graph detect-changes  # 检测变更
code-review-graph visualize  # 可视化图谱
```

## Relationships

- Related entities: [[entities/claude-code]], [[entities/ai-cheatcode]]
- Related concepts: [[concepts/code-structure-graph-for-ai]], [[concepts/blast-radius-impact-analysis]], [[concepts/context-and-cost-optimization]]
- 工具对比: [[entities/fireworks-tech-graph]]（同为领域特化工具，但定位不同：图查询 vs 图生成）

## Evidence

- [[sources/code-review-graph]]

## Open Questions

- Tree-sitter 解析失败时的降级策略
- 大型 monorepo 的图谱文件大小和查询延迟
- 是否支持自定义关系类型（数据流、依赖注入等）
- 与 GitNexus 的能力差异
