---
title: 范式组合策略
type: concept
status: active
updated: 2026-05-11
source_count: 1
---

# Concept: 范式组合策略

## Definition

在企业级AI Coding项目中，不同项目阶段灵活组合使用多种研发范式（Spec Coding、TDD、Glue Coding、Harness、Vibe Coding），而非固守单一范式。核心理念：范式无优劣，场景定选择。

## Why It Matters

单一范式难以满足复杂项目的全流程需求。618促销项目的实战表明，组合使用五种范式可实现：需求清晰（Spec）、核心质量（TDD）、开发效率（Glue）、自动化交付（Harness）、用户体验（Vibe）的全面覆盖。

## Core Components

| 阶段 | 推荐范式 | 说明 |
|------|---------|------|
| 项目启动 | - | 加载Reference代码、参考AGENTS.md规范 |
| 需求分析 | Spec Coding | 编写需求文档，识别可复用资产 |
| 设计阶段 | Spec Coding + Vibe Coding | 架构设计用Spec，交互体验用Vibe |
| 开发阶段 | TDD + Glue Coding | 核心逻辑用TDD，辅助功能用Glue |
| 体验优化 | Vibe Coding | A/B测试验证最优方案 |
| 测试阶段 | Harness | 自动化测试、持续验证 |
| 上线阶段 | Harness | 自动化部署、灰度发布 |

## PM角色随范式调整

- Spec Coding中PM主导需求
- TDD中PM关注验收标准
- Glue Coding中PM识别可复用资产
- Harness中PM定义发布节奏
- Vibe Coding中PM聚焦用户体验和A/B测试方案

## 实战关键数据

| 指标 | 数值 |
|------|------|
| 代码复用率 | 70% |
| 开发周期 | 2周 |
| 测试覆盖率 | 85% |
| 部署时间 | <10分钟 |
| 系统可用性 | 99.95% |

## Supporting Sources

- [[sources/ai-coding-paradigms-618-practice]]

## Related Pages

- [[concepts/spec-coding]]
- [[concepts/tdd-as-hard-gate]]
- [[concepts/glue-coding]]
- [[concepts/vibe-coding]]
- [[concepts/ai-ci-cd-automation]]（Harness范式的CI/CD实现）

## Contradictions / Nuance

- 文章主张"范式无优劣"，但量化数据实际上隐含了优先级：Glue Coding（效率最高、成本最低）和 Harness（部署最快、可靠性最强）的量化指标明显优于 Spec Coding。"无优劣"是否过于理想化？
- 组合策略增加了心智负担和切换成本——团队如何判断当前阶段应该切换范式？缺少明确的切换触发条件。
- 组合策略假设PM能灵活适应每种范式的角色要求，但实际组织中PM的专业背景可能只偏向其中一两种。
