---
title: Verification Before Completion
type: concept
status: active
updated: 2026-05-13
source_count: 2
---

# Concept: Verification Before Completion

## Definition

在 AI 辅助开发中，将"完成声明"与"新鲜验证结果"强制绑定：模型在产出最新验证证据之前，不允许宣称任务完成。这条规则的优先级高于一切口头判断和历史记忆。

## Why It Matters

AI 编程中最伤协作体验的，通常不是 bug 本身，而是**错误的完成声明**。模型太擅长说出"修好了""搞定了""应该没问题"，一旦允许这类无证据的声明进入工作流，人类验证成本会突然飙升。该概念把"完成"从主观判断升级为证据驱动的硬门禁。

## Core Rules

1. **最新验证结果**：必须是本次变更之后运行的测试/构建输出，不能引用历史结果。
2. **不得空口宣称**：任何"修好了""搞定了""应该没问题"的表述，都必须附带验证命令及输出摘要。
3. **优先级最高**：即使 brainstorming、writing-plans 等前置步骤全部完成，没有验证结果仍不许宣称完成。

## Relationship to TDD

verification-before-completion 与 [[concepts/tdd-as-hard-gate]] 互补但不等价：

| 维度 | TDD 硬门禁 | Verification Before Completion |
|------|-----------|-------------------------------|
| 管控时机 | 开发过程中（RED→GREEN→REFACTOR） | 完成声明发出前 |
| 核心约束 | 必须先有失败测试再写实现 | 必须有新鲜验证结果才能宣称完成 |
| 覆盖范围 | 代码变更的生产过程 | 交付验收的最后关口 |

两者可叠加使用：TDD 保证开发过程有测试驱动，verification-before-completion 保证最终交付有验证证据。

## Concrete Signals

- 在调试链路中：`systematic-debugging → test-driven-development → verification-before-completion` 构成最后三步门禁。
- 在功能开发链路中：`finishing-a-development-branch` 隐含了验证要求，但 verification-before-completion 将其从"建议"升级为"硬约束"。
- 与 hooks 系统配合：可在 `Stop` hook 中检查"是否有新鲜验证结果"，对缺失情况发出提醒。

## 泛化：所有规则都需要验证（来自自进化系统）

[[sources/self-evolving-claude-code]] 将 verification-before-completion 的理念从"完成声明需验证"泛化为"**所有规则都需验证**"——每条 learned-rules 中的规则都必须附带 `verify:` 机器可检查行。没有 verify 行的规则被视为技术债。

> "没有验证检查的规则是愿望，有验证检查的规则才是护栏。只有护栏才能存活。"

这将 verification 从"交付关口"扩展到了整个规则生命周期：规则诞生（从纠正/观察）→ 规则验证（verify 行）→ 规则执行（验证扫描）→ 规则晋升（10+ 会话通过后永久化）。

详见 [[concepts/verification-sweep]] 和 [[concepts/rule-promotion-ladder]]。

## Supporting Sources

- [[sources/superpowers-workflow-deconstruction]]
- [[sources/self-evolving-claude-code]]

## Related Pages

- [[entities/superpowers]]
- [[concepts/tdd-as-hard-gate]]
- [[concepts/hooks-as-safety-net]]
- [[concepts/spec-driven-workflow-and-review-discipline]]
- [[concepts/verification-loop]] — "怎么验证"的基础设施层面，与本概念的"什么时候才算完"互补

- 对纯配置变更、一次性脚本等场景，该规则可能过于严格——需要显式例外流程（与 TDD 硬门禁的豁免逻辑一致）。
- "新鲜"的定义存在模糊性：如果变更很小且上一次验证仍在同一会话内，是否算"新鲜"？建议定义一个明确的时间窗口或变更范围阈值。
