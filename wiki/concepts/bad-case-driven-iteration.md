---
title: Bad Case 驱动迭代
type: concept
status: active
updated: 2026-05-11
source_count: 2
---

# Concept: Bad Case 驱动迭代（Bad Case Driven Iteration）

## Definition

通过 AI 在实际使用中犯的错误驱动 AGENTS.md 的持续改进：观察 AI 犯错 → 判断补充规则能否避免 → 决定放全局（AGENTS.md）还是模块级（docs/）。不试图一次写完，而是从真实 bad case 出发逐步完善。

## Why It Matters

AGENTS.md 不是一份写完就锁定的文档——试图一次写完既不现实也容易遗漏关键场景。Bad Case 驱动确保每条规则都有真实的失败案例支撑，避免纸上谈兵式的过度规范。

## Core Sequence

1. AI 犯了一个错误（如用了错误的命名风格、在错误的层级引入了依赖）
2. 思考："如果 AGENTS.md 里多写一条 XX 规则，AI 是不是就不会犯这个错？"
3. 判断改哪里：全局规则 → AGENTS.md，模块细节 → 对应的 `docs/`
4. 补充自动化检查（如适用），形成规则执行力

## Rule Enforcement Priority

规则的优先级层次：**能自动化检查的 > 写在 AGENTS.md 中的 > 口头约定的**

## Team Practice

鼓励团队成员在遇到 AI bad case 时主动补充规则，但遵循"地图"原则（[[concepts/map-not-manual]]）：

| 改动类型 | 维护位置 | 举例 |
|---------|---------|------|
| 全局架构约定或编码规约 | AGENTS.md | 所有 Controller 统一 POST |
| 某个模块的开发规范 | 对应的 docs/ | 某个 Service 的调用约定 |
| 前端组件使用模式 | 组件模式文档 | ProTable 的某个 prop 必须传特定值 |
| 参考项目架构说明 | ref-* 文档 | 某个开源项目的架构分层介绍 |

## Supporting Sources

- [[sources/agents-md-guide]]
- [[sources/superpowers-deep-practice-guide]]

## Related Pages

- [[entities/agents-md]]
- [[concepts/map-not-manual]]
- [[concepts/schema-driven-maintenance]]

## Parallel Pattern: Superpowers 的"合理化防范"

Superpowers 在技能层面实现了类似但更前置的机制：每个技能内置 **Red Flags 表**（代理可自检的违规信号）+ **Common Rationalizations 表**（每个借口对应的反驳）+ Good/Bad 对比示例。这相当于"事前预堵"——在技能文档中预见代理可能的合理化借口并逐一堵死，而非等 bad case 发生后再补规则。两种模式互补：bad case 驱动迭代适用于项目级 AGENTS.md 的持续改进，合理化防范适用于通用技能库的设计。

## Contradictions / Nuance

- Bad Case 驱动本质上是"事后补救"，可能导致规则体系缺乏系统性——需要定期 lint 审查确保规则间的连贯性。
- 对于高频 bad case，应优先投资自动化检查而非仅仅补充文档规则。
