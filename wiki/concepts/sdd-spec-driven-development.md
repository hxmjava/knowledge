---
title: SDD（Spec-Driven Development，规格驱动开发）
type: concept
status: active
updated: 2026-05-13
source_count: 1
---

# Concept: SDD（Spec-Driven Development，规格驱动开发）

## Definition

规格驱动开发（Spec-Driven Development）是一种为 AI 时代量身定制的方法论：将规格（Specification）视为唯一事实来源（Single Source of Truth），代码只是规格的表达。工作流为 Specify → Clarify → Plan → Tasks → Implement。SDD 在 Vibecoding 五大方法论中处于"战略层"——回答"做什么"。

## Why It Matters

纯 Vibecoding 缺乏可追溯性——没有 SSOT，团队协作困难。SDD 通过将规格提升为最高权威，为 AI 编码提供了"战略层说明书"，驱动全生命周期（规格 → 计划 → 任务 → 实现 → 验证）。

## Core Components

- **规格即真理**：spec.md 是系统行为的唯一事实来源，代码必须符合规格。
- **constitution.md**：项目的基本原则和约束，不可被 AI 覆盖。
- **命令化工作流**：`/speckit.specify` → `/speckit.plan` → `/speckit.tasks`，每一步可追溯。
- **与 Superpowers 互补**：Spec Kit 定"规格是真理"，Superpowers 定"工作流是真理"——社区推荐两者结合使用。

## 与 OpenSpec 的关系

SDD（github/spec-kit）与 OpenSpec 理念相近但定位不同：

| 维度 | SDD (Spec Kit) | OpenSpec |
|------|---------------|----------|
| 核心主张 | 规格是唯一事实来源 | 规格先行 + 变更追踪 |
| 工具形态 | 官方 GitHub 工具包 | 独立工具链 |
| 文件结构 | constitution.md + spec.md + plan.md + tasks.md | openspec/ 目录 + proposal/tasks/specs |
| 工作流 | Specify → Clarify → Plan → Tasks → Implement | Propose → Fast-Forward → Verify → Archive |

两者可以叠加使用：SDD 提供战略规格框架，OpenSpec 提供变更追踪和归档纪律。

## Supporting Sources

- [[sources/vibecoding-tdd-atdd-bdd-ddd-sdd]]

## Related Pages

- [[entities/github-spec-kit]]（代表工具）
- [[concepts/spec-driven-workflow-and-review-discipline]]（OpenSpec 实践）
- [[concepts/spec-coding]]（文档先行范式）
- [[concepts/atdd-for-ai-coding]]（执行层互补）
- [[concepts/ddd-domain-driven-design]]（架构层互补）

## Contradictions / Nuance

- SDD 的"规格即真理"与 OpenSpec 的"规格先行 + 变更追踪"在理念上有重叠——两者的实质差异是什么？SDD 是否只是 OpenSpec 的简化包装？
- github/spec-kit 的实际采用率和社区活跃度未知——官方工具包是否已被广泛使用，还是仍处于早期阶段？
- "代码只是规格的表达"这一理念在实践中面临挑战：规格无法覆盖所有实现细节（性能优化、错误处理、边界条件），这些部分的"真理"在哪里？
