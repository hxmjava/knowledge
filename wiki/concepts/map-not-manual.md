---
title: 地图，而非手册
type: concept
status: active
updated: 2026-05-07
source_count: 2
---

# Concept: 地图，而非手册（Map, not Manual）

## Definition

AI 项目上下文文件（如 AGENTS.md、CLAUDE.md）应充当导航地图而非完整手册：只放"去哪里找什么"的索引和硬性规则，详细内容通过链接指向专项文档。建议控制在 200 行左右。

## Why It Matters

"什么都重要的时候，什么都不重要。" 如果把所有内容塞进上下文文件，AI 的注意力被稀释，真正关键的规则反而被淹没。模型已经足够聪明，知道什么时候该去查阅详细文档和源码——上下文文件只需要告诉它"文档在哪、源码在哪、什么时候该去看"。

## Core Components

- **写入 AGENTS.md 的两类内容**：
  - AI 理解项目全貌的必要信息（技术栈、仓库结构、核心模块、分层架构）
  - 违反会直接导致问题的硬性规则（编码规约、命名约定、禁止项）
- **不写入的内容**：详细文档通过链接指向 `docs/`，按需查阅。
- **判断标准**：AI 不知道就会写出**错误**的代码 → 放 AGENTS.md；只是写出**不够好**的代码 → 放详细文档。
- **渐进式披露**：从 200 行地图出发，链接指向分层文档（架构文档、开发手册、设计文档、参考项目说明）。

## Relationship to Progressive Disclosure

本概念与 [[concepts/progressive-disclosure-context-retrieval]] 在"按层暴露、按需深入"上共享底层理念，但适用层次不同：

| 维度 | Map, not Manual | 渐进式上下文检索 |
|------|----------------|-----------------|
| 适用对象 | 项目上下文文件（AGENTS.md） | Agent 记忆系统（Claude-Mem） |
| 核心操作 | 编写时精简，用链接替代全文 | 检索时按层暴露，先摘要后细节 |
| 设计目标 | 控制注意力稀释 | 控制上下文成本 |

两者可叠加：AGENTS.md 本身遵循"地图"原则，Agent 在执行时通过渐进式检索获取更深层上下文。

## Supporting Sources

- [[sources/agents-md-guide]]
- [[sources/superpowers-workflow-deconstruction]]

## Related Pages

- [[entities/agents-md]]
- [[entities/claude-code]]
- [[concepts/progressive-disclosure-context-retrieval]]
- [[concepts/context-and-cost-optimization]]

## Contradictions / Nuance

- 200 行是经验法则而非硬约束；大型 monorepo（如 OpenAI 的 88 个嵌套 AGENTS.md）可能需要不同的精简策略。
- "地图"原则假设模型足够聪明能自行查阅链接文档——但对于复杂架构，模型可能需要更多内联上下文才能做出正确判断。
