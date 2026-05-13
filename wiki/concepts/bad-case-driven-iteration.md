---
title: Bad Case 驱动迭代
type: concept
status: active
updated: 2026-05-13
source_count: 5
---

# Concept: Bad Case 驱动迭代（Bad Case Driven Iteration）

## Definition

通过 AI 在实际使用中犯的错误驱动 AGENTS.md 的持续改进：观察 AI 犯错 → 判断补充规则能否避免 → 决定放全局（AGENTS.md）还是模块级（docs/）。不试图一次写完，而是从真实 bad case 出发逐步完善。[[sources/agents-md-cars-guide]] 进一步强调：先从 Commands 和 Restrictions 两部分开始写最实用，后面再慢慢补 Architecture 和知识索引——"演进式更新，而非一次性编写"。

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

## 行为契约视角：从翻车记录到工程约定

[[sources/claude-md-error-rate-reduction]] 将这一模式提升为"行为契约"框架：好规则不是写出来的，是摔出来的。若飞提出的操作方法是——先翻 Agent 最近几次翻车记录，再把每类偏差（猜、扩、混、忘、装作完成）写成可执行的具体约定，而非抽象提醒。

关键增量：
- **规则会过期**：模型升级、框架迁移后，旧规则可能反而误导 Agent。每隔一段时间删一轮，比不断追加更重要。
- **四类应避免的写法**：身份提示（"你是资深工程师"）、空泛提醒（"保持优雅"）、纯禁止清单、永不过期规则。
- **最小可行版本**：先写 80 行高频行为约定 + 5 条项目命令 + 5 条项目边界，根据真实失败逐步迭代。

## Supporting Sources

- [[sources/agents-md-guide]]
- [[sources/superpowers-deep-practice-guide]]
- [[sources/claude-md-error-rate-reduction]]
- [[sources/agents-md-cars-guide]]
- [[sources/self-evolving-claude-code]]

## Related Pages

- [[entities/agents-md]]
- [[entities/karpathy]]
- [[concepts/map-not-manual]]
- [[concepts/behavioral-contract-vs-prompt]]
- [[concepts/reminders-vs-hard-enforcement]]
- [[concepts/schema-driven-maintenance]]

## Parallel Pattern: Superpowers 的"合理化防范"

Superpowers 在技能层面实现了类似但更前置的机制：每个技能内置 **Red Flags 表**（代理可自检的违规信号）+ **Common Rationalizations 表**（每个借口对应的反驳）+ Good/Bad 对比示例。这相当于"事前预堵"——在技能文档中预见代理可能的合理化借口并逐一堵死，而非等 bad case 发生后再补规则。两种模式互补：bad case 驱动迭代适用于项目级 AGENTS.md 的持续改进，合理化防范适用于通用技能库的设计。

## 自动化变体：免疫系统方法（来自自进化系统）

[[sources/self-evolving-claude-code]] 将 bad case 驱动迭代从"人工判断补充规则"升级为"系统自动验证 + 自动晋升"：

| 维度 | Bad Case 驱动迭代 | 免疫系统方法 |
|------|-----------------|------------|
| 发现方式 | 人工观察 AI 犯错 | 系统自动捕获纠正模式 |
| 补充决策 | 人工判断放全局还是模块级 | 量化触发：2 次同模式纠正 → 自动晋升 |
| 验证方式 | 补充自动化检查（可选） | 每条规则强制附带 `verify:` 行（必须） |
| 淘汰机制 | 定期 lint 审查 | 容量上限（50 行）+ `/evolve` 审计 |
| 风险 | 规则体系缺乏系统性 | 可能误晋升低质量规则 |

核心原则：**"Never log a guess. Verify it immediately or don't log it."**——观察必须先 grep 验证后才记录，confirmed + 0 反例直接晋升为规则。

两种方法互补：免疫系统方法适合高频、可机器检查的纠正模式；bad case 驱动迭代适合需要人工判断的架构级决策。

详见 [[concepts/self-evolving-agent-system]] 和 [[concepts/rule-promotion-ladder]]。

## Contradictions / Nuance

- Bad Case 驱动本质上是"事后补救"，可能导致规则体系缺乏系统性——需要定期 lint 审查确保规则间的连贯性。
- 对于高频 bad case，应优先投资自动化检查而非仅仅补充文档规则。
