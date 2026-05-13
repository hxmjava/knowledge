---
title: 提醒 vs 硬约束
type: concept
status: active
updated: 2026-05-12
source_count: 1
---

# Concept: 提醒 vs 硬约束（Reminders vs Hard Enforcement）

## Definition

在 AI 编码系统中区分两个层次的行为控制：CLAUDE.md 等上下文文件提供"事前提醒"（告诉 Agent 怎么做），而 hooks、权限、lint、测试、CI 和 review 提供"硬约束"（决定危险动作能不能发生）。前者解决"应该怎么做"，后者解决"能不能这么做"——两者不可混淆，也不能互相替代。

## Why It Matters

过度依赖 CLAUDE.md 的提醒能力会导致虚假安全感。典型失败场景：
- CLAUDE.md 写"不要读 .env"，但 Agent 仍然可以读——真正拦住它的是 settings.json 的 deny 规则。
- CLAUDE.md 写"测试必须通过"，但 Agent 可以跑一个浅测试就宣称通过——真正拦住它的是 CI 里的覆盖率门禁。
- CLAUDE.md 写"不要改危险文件"，但 Agent 可以在上下文压力下忽略——真正拦住它的是 hook 的 PreToolUse 检查。

把提醒和硬约束混在一起，"文章看着完整，系统并不会因此更稳"。

## Layered Control Model

| 层次 | 工具 | 性质 | 示例 |
|------|------|------|------|
| 事前提醒 | CLAUDE.md / AGENTS.md | 软约束，可被忽略 | "只改必要范围" |
| 格式与静态检查 | formatter / lint / 类型检查 | 硬约束，自动执行 | ESLint 规则、TypeScript 类型 |
| 行为验证 | 单元测试 / 集成测试 | 硬约束，回归检测 | `pnpm test` |
| 动作边界 | hooks / 权限 (settings.json) | 硬约束，阻断执行 | deny list、PreToolUse hook |
| 合并前检查 | CI / review | 硬约束，流程门禁 | GitHub Actions、PR review |
| 合并后信号 | 日志 / 指标 / 线上监控 | 反馈回路 | 错误率、延迟指标 |

## Mitchell Hashimoto 原则

Mitchell Hashimoto 在《My AI Adoption Journey》中提出：Agent 犯错后，不能只修这一次，还要顺手补一个机制，让同类错误以后更难再发生。

机制的层次：
- 最轻：一条 AGENTS.md 规则（提醒）
- 中等：一个 lint 规则或测试用例（自动化检查）
- 最重：一个 hook 或权限配置（硬阻断）

选择哪个层次，取决于错误的严重性和频率。

## Relationship to Hooks as Safety Net

本概念与 [[concepts/hooks-as-safety-net]] 形成理论框架与实践工具的关系：
- Hooks as Safety Net 描述了 hooks 的具体配置和生命周期
- 本概念提供了选择"提醒 vs 硬约束"的决策框架

## Supporting Sources

- [[sources/claude-md-error-rate-reduction]]

## Related Pages

- [[concepts/hooks-as-safety-net]]
- [[concepts/bad-case-driven-iteration]]
- [[concepts/verification-before-completion]]
- [[concepts/tdd-as-hard-gate]]
- [[concepts/policy-driven-tool-permissions]]
- [[entities/mitchell-hashimoto]]

## Contradictions / Nuance

- 硬约束的搭建成本远高于写一条提醒——小型项目可能无法负担完整的 hooks + CI + review 链路。
- 提醒的价值在于"低成本启动"——项目初期可以先靠 CLAUDE.md，但应逐步投资自动化。
- 有些规则难以硬编码为自动化检查（如"先说假设"），只能通过提醒实现——这不是缺陷，而是提醒层的独特价值。
