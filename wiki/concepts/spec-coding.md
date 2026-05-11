---
title: Spec Coding（文档先行范式）
type: concept
status: active
updated: 2026-05-11
source_count: 1
---

# Concept: Spec Coding（文档先行范式）

## Definition

一种AI Coding研发范式：先编写完整的需求文档和设计规范（Spec），再严格按照文档进行代码实现。切入点是需求分析+Reference代码，核心关注需求明确性和可追溯性。

## Why It Matters

大型企业项目（如618促销）需求复杂、涉及多方协作，文档先行能有效减少歧义、降低返工成本。与 [[concepts/spec-driven-workflow-and-review-discipline]] 中的 OpenSpec 规格纪律互补——Spec Coding 更偏"需求规格驱动"，OpenSpec 更偏"变更追踪和规格纪律"。

## Core Components

- **需求文档体系**：从写作总则到追踪矩阵的完整文档链（14份Spec文档）
- **Reference 代码识别**：结合现有代码资产明确复用边界
- **可追溯性**：每个功能点都能追溯到对应的Spec文档
- **团队协作规范**：文档作为多方（PM、架构师、开发）的沟通桥梁

## 适用场景

- 大型企业级系统、金融核心系统
- 需求稳定、团队规模大、协作需求高
- 不适用：快速原型、频繁需求变更

## 量化指标

- 开发周期：3-4周（较慢）
- 代码复用率：中等（30%）
- 测试覆盖率：中（60%）
- 人力成本：高
- 维护成本：低

## Supporting Sources

- [[sources/ai-coding-paradigms-618-practice]]

## Related Pages

- [[concepts/spec-driven-workflow-and-review-discipline]]（规格纪律的系统化方法论）
- [[concepts/glue-coding]]（互补范式：复用优先）
- [[concepts/paradigm-composition]]（组合策略）

## Contradictions / Nuance

- 本文的 Spec Coding 与 OpenSpec 的规格驱动理念一脉相承，但侧重点不同：Spec Coding 面向需求分析阶段，OpenSpec 面向变更执行阶段。两者可以叠加使用。
- Spec Coding 声称"代码质量高（设计驱动）"，但量化表中测试覆盖率仅60%——如果"高"质量主要依赖设计而非测试，其可靠性保障机制是否足够？
