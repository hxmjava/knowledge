---
title: DDD（领域驱动设计）
type: concept
status: active
updated: 2026-05-13
source_count: 1
---

# Concept: DDD（领域驱动设计）

## Definition

领域驱动设计（Domain-Driven Design）在 AI 辅助开发中的应用：通过统一语言（Ubiquitous Language）和限界上下文（Bounded Context）帮助 AI 理解系统边界，生成高内聚低耦合的代码。DDD 为 AI 编码提供"架构护栏"——告诉 AI "如何组织领域逻辑"。

## Why It Matters

AI 编码工具在大型复杂系统中容易产生架构混乱的代码——类名不一致、模块边界模糊、跨域耦合。DDD 的限界上下文和统一语言为 AI 提供明确的架构边界，减少"意大利面条式代码"的风险。

## Core Components

- **统一语言**（Ubiquitous Language）：业务和技术团队使用同一套术语描述领域概念，确保 AI 生成的代码与业务语义一致。
- **限界上下文**（Bounded Context）：将系统划分为独立的领域模块，每个模块有明确的边界和职责——AI 在特定上下文内生成代码时不会越界。
- **领域模型**：在限界上下文内的核心业务实体和行为建模，为 AI 提供代码生成的架构骨架。

## 在 Vibecoding 中的定位

DDD 在五大方法论中处于"架构层"：

- SDD 回答"做什么"（战略层）
- **DDD 回答"怎么组织"（架构层）**
- ATDD + TDD 回答"怎么验证"（执行层）
- BDD 回答"谁来协作"（协作层）

适合复杂业务系统，常与 SDD 结合使用。

## Supporting Sources

- [[sources/vibecoding-tdd-atdd-bdd-ddd-sdd]]

## Related Pages

- [[concepts/sdd-spec-driven-development]]（战略层互补）
- [[concepts/bdd-for-ai-coding]]（共享统一语言理念）
- [[concepts/layered-project-harness]]（分层项目组织）
- [[concepts/spec-driven-workflow-and-review-discipline]]

## Contradictions / Nuance

- 文章中 DDD 部分仅两行概述，缺乏具体的 AI Coding 实践案例——DDD 如何与 Claude Code 等 AI 编码工具结合？AI 是否能自动识别和遵守限界上下文？
- 限界上下文的划分本身就是架构决策中最困难的部分之一——期望 AI 理解并遵守限界上下文，前提是人类已经正确划分了边界。
- DDD 与 SDD 的结合方式未在文章中展开——规格如何编码限界上下文信息？
