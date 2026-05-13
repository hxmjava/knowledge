---
title: 行为契约 vs 提示词
type: concept
status: active
updated: 2026-05-13
source_count: 2
---

# Concept: 行为契约 vs 提示词（Behavioral Contract vs Prompt）

## Definition

将 CLAUDE.md / AGENTS.md 定性为"轻量行为契约"而非提示词技巧：提示词控制当前一次对话的行为，行为契约放在仓库级别，目标是让每一次会话都少走弯路。两者的区别不在形式（都是文本指令），而在持久性、范围和意图。

## Why It Matters

大多数人将 CLAUDE.md 当作"更好的提示词"来写，导致两类常见问题：(1) 写得太泛，充满无法执行的抽象建议；(2) 写得太多，把每次任务的上下文窗口塞满。理解它是"行为契约"而非"提示词"，能改变编写策略——从"告诉模型怎么思考"转向"告诉模型在这个仓库里什么是允许的、什么是必须的、什么是禁止的"。

## Core Distinctions

| 维度 | 提示词 | 行为契约 |
|------|--------|---------|
| 作用范围 | 当前对话 | 仓库内所有会话 |
| 持久性 | 用完即丢 | 签入版本控制 |
| 内容风格 | 引导推理过程 | 约束输入/输出行为 |
| 典型内容 | "请一步步分析" | "只改必要范围，不顺手重构" |
| 变更触发 | 任务需求变化 | 项目失败模式变化 |

## Tobi Lütke 的 "Context Engineering" 视角

Shopify CEO Tobi Lütke 提出用 "context engineering" 替代 "prompt engineering"——核心技能是"给模型足够的上下文，让任务变得可解"。CLAUDE.md 属于这层最薄、也最稳定的上下文：不像动态提示词那样随任务变化，也不像 RAG 检索那样依赖检索质量。

## Relationship to Map, not Manual

本概念与 [[concepts/map-not-manual]] 互补：
- Map, not Manual 解决"CLAUDE.md 里放什么"（导航地图 vs 百科全书）
- 行为契约 vs 提示词解决"CLAUDE.md 是什么"（仓库级约束 vs 单次引导）

两者叠加：行为契约应以地图形式呈现——精简、结构化、通过链接延伸。

## "行为编程"视角（来自自进化系统）

[[sources/self-evolving-claude-code]] 进一步强化了这一概念，用"行为编程"（behavior programming）替代"行为契约"：

> "CLAUDE.md 不是文档，而是行为编程。里面的每一行都会直接加载到 Claude 的系统提示词中，塑造它在整个会话期间的思维方式。"

关键增量：
- **决策框架前置**：CLAUDE.md 不只列出"不能做什么"（契约式），还编程了"怎么做决策"（先 grep → 评估影响 → 最小改动 → 验证计划）——从约束行为升级为塑造认知。
- **进化协议内置**：CLAUDE.md 包含 Self-Evolution Protocol 段落——要求 agent 在每次会话中观察、记录纠正、查阅记忆、不重复犯错——行为契约本身包含了自我改进的指令。
- **150 行硬上限**：超过这个长度 Claude 的指令遵从度下降——这比 200 行建议更保守。
- **Things You Must Never Do**：明确禁止清单（不直接 commit main、不读 .env、不静默吞错、不未经 /evolve 修改 learned-rules），比"行为契约"更像"行为编程中的断言"。

## Supporting Sources

- [[sources/claude-md-error-rate-reduction]]
- [[sources/self-evolving-claude-code]]

## Related Pages

- [[concepts/map-not-manual]]
- [[concepts/context-and-cost-optimization]]
- [[concepts/bad-case-driven-iteration]]
- [[entities/karpathy]]
- [[entities/claude-code]]

## Contradictions / Nuance

- 在实践中，CLAUDE.md 的内容往往既包含行为契约（"不要重构相邻代码"）也包含提示词元素（"先说假设再写代码"）——两者界限并非泾渭分明。
- Agent 的会话隔离特性意味着行为契约也需要"每次开工前重新注入"——这与传统版本控制中的"签入一次、永远生效"不同。
