---
title: Glue Coding（复用先行范式）
type: concept
status: active
updated: 2026-05-11
source_count: 1
---

# Concept: Glue Coding（复用先行范式）

## Definition

一种AI Coding研发范式：优先复用现有代码和组件，快速拼接实现新功能。切入点是Reference代码，核心关注开发效率和代码一致性。其核心哲学是"天下文章一大抄"——项目中已有稳定代码时，没必要让AI重新生成。

## Why It Matters

在促销活动等"高相似度迭代"场景中，Glue Coding 是效率最高的范式。618促销项目中复用率达70%，核心功能开发时间缩短60%。与 [[concepts/reference-projects-as-context]] 形成互补——Glue Coding 侧重代码级复用（直接注入 Service），reference-projects-as-context 侧重知识级复用（submodule 引入源码供 AI 阅读）。

## Core Components

- **资产扫描**：识别可复用组件（Service、配置、工具类）
- **参数化配置**：可变参数外部化（如满减阈值、活动时间）
- **组合拼接**：将多个已有组件组合成新功能
- **风格一致性**：复用已有代码风格，保持团队代码统一

## 适用场景

- 促销活动、快速迭代功能
- 中小型项目，代码复用率高
- 不适用：复杂架构设计、首次开发从零开始

## 量化指标

- 开发周期：1-2周（快）
- 代码复用率：高（70%）
- 测试覆盖率：中（60%）
- 人力成本：低
- 维护成本：中（技术债务风险）

## Supporting Sources

- [[sources/ai-coding-paradigms-618-practice]]

## Related Pages

- [[concepts/reference-projects-as-context]]（知识级复用的互补模式）
- [[concepts/spec-coding]]（互补范式：文档先行）
- [[concepts/paradigm-composition]]（组合策略）

## Contradictions / Nuance

- Glue Coding 强调"代码质量有保障（经过验证的代码）"，但同时承认"可能引入不必要的依赖"和"技术债务"——复用不是零成本的，需要定期重构清理。
- 在 AI 编码语境下，Glue Coding 的"抄"与"让 AI 重新生成"之间的决策标准未明确——什么情况下应该复用、什么情况下应该让 AI 从零写？缺少判断阈值。
