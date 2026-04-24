---
title: Spec-Driven Workflow and Review Discipline
type: concept
status: active
updated: 2026-04-24
source_count: 2
---

# Concept: Spec-Driven Workflow and Review Discipline

## Definition

在 AI 辅助开发中，把"规格先行（OpenSpec）"与"执行纪律（Superpowers）"串成一个闭环：先对齐目标，再按可验证任务推进，并持续留痕审计。二者不是互斥替代，而是"先对齐规范 → 再按流程执行"。

## Why It Matters

它减少了"文档先写了、代码后写了，最后谁也说不清改了什么"的失真问题；尤其在多人协作和长期模块里，能显著降低回归成本。

## Core Components

- **规范层**：`openspec/` 组织、proposal/tasks/specs、change 与 archive。
- **执行层**：计划化分解、子任务并行、TDD、代码审查。
- **交付层**：任务完成有可验证证据，代码合并后执行文档回写与归档。
- **复盘层**：异常路径和过程调整要有痕迹（评审结论、修订任务、归档说明）。

## Core Sequence

1. **提案** (OpenSpec)：`/opsx:explore` / `/opsx:propose` → `proposal.md` + `tasks.md` + 规范增量
2. **纠偏** (Superpowers Plan)：技术栈或约束与初稿不一致时，重写任务分层与依赖（如 Wave 并行批次）
3. **实现** (Superpowers)：`tasks.md` 驱动 + TDD + 子代理协作
4. **验证** (测试/CI)：编译/测试 + 证据留存（命令、接口返回、截图或日志摘要）
5. **归档** (OpenSpec)：评审与 `/opsx:archive`，规范与实现可追溯
6. **维护**：关键事实回写 wiki 或后续检索页

> `tasks.md` 可能是初稿；执行中允许由 Plan/评审调整为更合理的 Wave/依赖，但**变更要有记录**。

## Scenario-Based Usage

| 场景 | 推荐 | 原因 |
|------|------|------|
| 核心业务、长期维护模块 | Superpowers（+ 测试/评审） | 质量与可维护性 |
| 多人协作、需对外/对内说明 | OpenSpec | 规范统一、可归档追溯 |
| 生产级功能迭代 | 二者协同 | 规范 + 纪律 |
| 极小范围 bugfix | 原生 Agent / 最小流程 | 避免流程成本大于收益 |

## Common Pitfalls

- **计划完整但执行闭环不足**：设计很充分，代码落地与验证进度不可见 → 固定执行顺序，每 task 必须附可验证证据。
- **文档分散，版本漂移风险**：`docs/`、`openspec/`、`.cursor/doc/ai-context/` 语义重叠 → 规定单一事实源（SSOT）。
- **跨模块联调成本高**：契约未先落定就写实现 → 先落 API 契约，再落 Controller。
- **数据口径未确认就写分支**：先完成数据源定稿，再写业务分支，禁止默认长期使用临时方案。

## Supporting Sources

- [[sources/openspec-superpowers-practice-guide]]
- [[sources/claude-code-enterprise-playbook]]

## Related Pages

- [[entities/openspec]]
- [[entities/superpowers]]
- [[concepts/team-governance-for-ai-coding]]
- [[concepts/ingest-query-lint-loop]]

## Contradictions / Nuance

- 纪律越重，初期执行成本越高；建议先定义分级触发条件，避免把每个小修复都走完整链路。
- 文档鼓励流程强制化，却也给了 `hotfix` 的裁剪口径；最终取舍依赖团队成熟度与风险容忍。
