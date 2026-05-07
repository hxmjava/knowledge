---
title: AGENTS.md 实践指南
type: source
status: active
updated: 2026-05-07
source_count: 1
---

# Source: AGENTS.md 实践指南

## Metadata

- Raw file: `raw/sources/agents-md-guide.md`
- Author: Kirito的技术分享
- Date: 2026-04-20
- URL: https://mp.weixin.qq.com/s/m-v7GTbksdhWZuHxGD7BaA
- Series: "AI Coding 实践"系列第六篇

## Summary

- AGENTS.md 是给 AI Agent 看的项目指令文件（"给 AI 看的 README"），已成为事实标准，由 Linux Foundation 下属 Agentic AI Foundation 托管，截至 2026 年初 GitHub 上超 6 万项目采用。
- 核心理念是"地图，而非手册"：约 200 行导航地图，告诉 Agent 去哪里找什么，详细内容通过链接指向 `docs/` 文档。
- 五大实践：仓库聚合（monorepo）、统一环境配置（`~/.<project>_env` + 一键启动脚本）、验证闭环（改→构建→启动→验证，含 curl 规范和 Agent Browser）、自动化检查（分层依赖 lint + Makefile 命令矩阵）、参考项目引入（git submodule 源码 + ref 架构文档）。
- Bad Case 驱动迭代：不要一次写完，从 AI 实际犯错的地方逐条补充规则。
- 规则执行力优先级：自动化检查 > AGENTS.md 写规则 > 口头约定。

## Key Claims

- AGENTS.md 的本质是用最小上下文成本让 AI 获得最大项目理解——写得准比写得多重要。
- "源码永远不会过时，它就是最准确的文档"——对闭源/私域组件，引入源码比维护使用文档更可靠。
- 验证闭环是夜间 Agent 自主执行的前提：改完代码不算完，跑通接口才算完。
- 错误信息格式 WHAT+WHY+HOW 同时服务人类和 AI——AI 读到后能直接按指引修复。
- 为 AI 写 AGENTS.md 的过程也是为团队做知识梳理——把散落在 Wiki/聊天/口头的"潜规则"结构化。

## Evidence Notes

- 作者半年实践于管控系统（Spring Boot + React 前后端分离），经历了从三仓分离到 monorepo 的演进。
- 引用 OpenAI Harness Engineering "Map, not Manual" 原则和 Anthropic 官方博客关于渐进式披露的论述。
- 提到 Boris Cherny（Claude Code 主创）关于端到端验证的经验分享。
- AGENTS.md 历史脉络：Anthropic CLAUDE.md → 各工具各自为政 → 2025 年 5 月 AMP 提议统一 → OpenAI 买下 agents.md → 最终成为事实标准。
- harness-creator 是一个配套 Skill，可一键生成 AGENTS.md 及 lint 脚本、Makefile、验证基础设施。

## Contradictions / Tensions

- 与 [[sources/ai-template2-scaffold]] 对比：本文的 AGENTS.md 模板是 9 章节约 200 行的精简地图；脚手架方案的 CLAUDE.md + harness 配置则更丰富（含 agents、skills、hooks），两者在"多丰富才够"上存在张力。
- "源码即文档"策略在仓库体积和 submodule 管理上有成本，对小型项目未必适用。
- "200 行上限"是经验法则而非硬约束——实际的管控系统 AGENTS.md 摘要暗示接近该上限时仍需多层文档支撑。

## Linked Entities

- [[entities/agents-md]]
- [[entities/claude-code]]
- [[entities/harness-creator]]

## Linked Concepts

- [[concepts/progressive-disclosure-context-retrieval]]
- [[concepts/map-not-manual]]
- [[concepts/verification-loop]]
- [[concepts/bad-case-driven-iteration]]
- [[concepts/reference-projects-as-context]]
- [[concepts/context-and-cost-optimization]]

## Follow-up Questions

- AGENTS.md 的 200 行建议是否适用于大型 monorepo（88 个嵌套 AGENTS.md 的 OpenAI 模式）？
- harness-creator 的生成质量和覆盖范围如何？是否需要人工大幅修正？
- "源码即文档"在 AI 上下文窗口有限的情况下，是否会导致检索效率问题？
- 不同 AI 工具对 AGENTS.md 的解析和注入方式是否存在差异，导致实际效果不一致？
