---
title: "CLAUDE.md 错误率从 41% 到 3%：到底改对了什么？"
type: source
status: active
updated: 2026-05-12
source_count: 1
---

# Source: CLAUDE.md 错误率从 41% 到 3%：到底改对了什么？

## Metadata

- Raw file: `raw/sources/claude-md-error-rate-reduction.md`
- Author: 若飞
- Date: 2026-05-11
- URL / Publisher: [微信公众号「架构师」](https://mp.weixin.qq.com/s/nAqv-0xAeoalLHS-nCt0TQ)

## Summary

- Karpathy 提出 4 条 CLAUDE.md 规则（静默假设、过度复杂、无关改动、未验证完成），Forrest Chang 整理为开源模板，Mnimiy 在 30 个代码库上扩展到 12 条并声称错误率从 41% 降到 3%。
- 12 条规则可重组为 4 类工程问题：控制改动半径、把确定性交还给代码、长任务留检查点、失败显性化。
- 作者提出 CLAUDE.md 本质上是"轻量行为契约"而非提示词技巧——仓库级别的工作约定，目标是让每次会话都少走弯路。
- 关键张力：CLAUDE.md 是上下文而非硬约束（消耗 token、可能互相冲突），需要配合 hooks/权限/CI/测试等确定性反馈层才能真正兜底。
- 推荐三层文件结构：根目录 CLAUDE.md（80-120 行高频行为）→ 项目事实文件（docs/agent/project.md）→ 任务流程文件（按场景索引），避免大杂烩。
- 好规则来自真实失败现场而非设计——先翻 Agent 最近翻车记录，把每类偏差写成可执行约定。

## Key Claims

- "41% 到 3%"是经验样本，非独立复现论文，不同代码库/任务/模型/评判标准结果会变。
- Karpathy 4 条规则的有效性源于 Agent 无法稳定继承项目工作习惯——CLAUDE.md 把习惯固定到仓库。
- CLAUDE.md ≠ 提示词技巧：提示词控制单次对话，行为契约是仓库级别的跨会话约束。
- 规则越长越容易把简单任务拖复杂；12 条不应整包复制，应按仓库失败模式裁剪。
- CLAUDE.md 是 Harness 最轻的一层（事前引导），真正的兜底靠 formatter/lint/tests/hooks/CI/review。
- Mitchell Hashimoto 原则：Agent 犯错后不能只修一次，要顺手补一个机制让同类错误更难再犯。

## Evidence Notes

- Mnimiy 实验：30 代码库、6 周、规则从 4 条扩展到 12 条；最终结果 41% → 3%。
- 失败案例丰富：503 重试策略抖动（概率模型做确定性逻辑）、错误处理器翻倍（两套模式混合）、重复函数绕过旧函数（未读周边代码）、auth 测试全绿但只返回常量（浅验证）。
- 提供了 80 行最小 CLAUDE.md 模板，含 Working style / Verification / Project commands / Project conventions / Safety boundaries 五段。
- 四类应避免的写法：身份提示（"你是资深工程师"）、空泛提醒（"保持优雅"）、纯禁止清单、永不过期规则。
- 参考了 Anthropic 官方建议：单文件控制在 200 行以内，指令具体简洁有结构。
- 引用 Tobi Lütke "context engineering" > "prompt engineering" 视角。
- 文中引用 2 篇 AGENTS.md 学术论文作为补充证据：
  - [Evaluating AGENTS.md: Are Repository-Level Context Files Helpful for Coding Agents?](https://arxiv.org/abs/2602.11988)
  - [On the Impact of AGENTS.md Files on the Efficiency of AI Coding Agents](https://arxiv.org/abs/2601.20404)
- 文章包含 3 张配图：12 条规则栈图、CLAUDE.md 加载层级图、Claude hooks 生命周期图。
- 文末附 20 篇「架构师」公众号系列前作链接，覆盖 Harness 方法论、长周期 Agent、上下文工作集、Claude Skills、Cowork 安全架构等主题。

## Contradictions / Tensions

- 本文引用 Anthropic 文档说 CLAUDE.md 是"上下文而非硬约束"，但 [[sources/agents-md-guide]] 强调 AGENTS.md 应有自动化检查配套——两者在"软约束 vs 硬约束"的立场上形成互补张力。
- 作者建议 80-120 行 CLAUDE.md，但 [[concepts/map-not-manual]] 提出 200 行——差异来自定义范围不同（纯行为约定 vs 含项目事实索引）。
- "规则来自翻车记录"与 [[concepts/bad-case-driven-iteration]] 的理念一致，但本文更强调"规则会过期、需要定期删除"这一维护维度。

## Linked Entities

- [[entities/ruofei]] — 文章作者
- [[entities/jiagoux]] — 发布公众号
- [[entities/karpathy]] — 4 条原始规则的提出者
- [[entities/forrest-chang]] — 整理 CLAUDE.md 开源模板
- [[entities/mnimiy]] — 30 代码库实验、规则扩展至 12 条
- [[entities/claude-code]] — 文章讨论的核心工具

## Linked Concepts

- [[concepts/behavioral-contract-vs-prompt]] — CLAUDE.md 作为"轻量行为契约"而非提示词
- [[concepts/reminders-vs-hard-enforcement]] — 提醒层与硬约束层的分工
- [[concepts/bad-case-driven-iteration]] — 好规则从失败现场长出来
- [[concepts/map-not-manual]] — 三层文件结构、精简入口
- [[concepts/context-and-cost-optimization]] — CLAUDE.md 的 token 消耗与注意力稀释
- [[concepts/hooks-as-safety-net]] — 门禁 vs 提醒的分工
- [[concepts/verification-before-completion]] — 验证必须有证据，不能空口宣称
- [[concepts/verification-loop]] — 端到端验证闭环

## Follow-up Questions

- Mnimiy 的 30 代码库实验是否可独立复现？评判标准是什么？
- Karpathy 的 4 条规则是否已正式开源为标准 CLAUDE.md 模板？
- 三层文件结构在不同仓库规模（个人/小团队/大型 monorepo）下的最佳实践是什么？
- Mitchell Hashimoto 的 "从错误到机制" 原则如何量化？规则 vs 工具 vs 自动化检查的投入回报比？
- 本文讨论的"架构师"公众号系列文章（前文提到了 Cursor Harness、长周期 Agent 等）是否值得作为独立来源录入？
- 文末引用的 2 篇 AGENTS.md 学术论文（arxiv 2602.11988 和 2601.20404）对 repo-level context file 的定量评估结果如何？是否支持 CLAUDE.md 的有效性？
- 文末推荐的 20 篇「架构师」系列文章中，哪些与当前 wiki 主题最相关、最值得优先录入？
