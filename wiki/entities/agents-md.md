---
title: AGENTS.md
type: entity
status: active
updated: 2026-05-07
source_count: 2
---

# Entity: AGENTS.md

## What It Is

AGENTS.md 是一个开放格式的标准文件，用于指导 AI Coding Agent 在项目中工作——相当于"给 AI 看的 README"。它包含构建命令、编码规范、测试要求、安全注意事项等 AI 需要的项目上下文。由 Linux Foundation 下属 Agentic AI Foundation 托管，截至 2026 年初已有超 6 万 GitHub 项目采用。

## Relevance

该实体是 AI 编码协作的项目级上下文入口，连接仓库结构、验证闭环、自动化检查和团队治理等 wiki 核心主题。

## Key Facts

- 各工具一度各自为政（CLAUDE.md / .cursorrules / GEMINI.md 等），2025 年 5 月经 AMP + OpenAI 推动统一为 AGENTS.md。
- Claude Code 虽仍用 CLAUDE.md，但内容完全通用，`ln -s AGENTS.md CLAUDE.md` 即可兼容。
- 大型 monorepo 支持子目录嵌套 AGENTS.md，Agent 读最近的那个。
- 建议控制在 200 行左右，遵循"地图，而非手册"原则（[[concepts/map-not-manual]]）。
- 核心价值：把项目知识和规范从人的脑子里转移到 AI 能读到的地方。
- 不是写完就锁定的文档，需要通过 Bad Case 驱动持续迭代（[[concepts/bad-case-driven-iteration]]）。
- 可用 **C.A.R.S 结构**组织内容：Commands、Architecture、Restrictions、Standards（[[concepts/cars-agents-structure]]）。Restrictions（不能做什么）被认为是最有价值的区块。
- **跨工具兼容**：作为单一事实来源（SSOT），Claude Code 通过 `ln -s AGENTS.md CLAUDE.md` 接入，Cursor 配合 `.cursor/rules/*.mdc` 细粒度规则，Codex 支持 repo-root + `~/.codex/AGENTS.md` 多层级（[[concepts/cross-tool-agents-compatibility]]）。
- **大项目索引模式**：超过 300 行时切换为 100-120 行的"目录索引"，详细内容下放到 `docs/` 子目录（adr/、conventions/、workflows/、patterns/、gotchas.md）。

## Relationships

- Related entities: [[entities/claude-code]], [[entities/harness-creator]], [[entities/openspec]], [[entities/superpowers]], [[entities/miao]]
- Related concepts: [[concepts/map-not-manual]], [[concepts/progressive-disclosure-context-retrieval]], [[concepts/bad-case-driven-iteration]], [[concepts/verification-loop]], [[concepts/reference-projects-as-context]], [[concepts/cars-agents-structure]], [[concepts/cross-tool-agents-compatibility]]

## Evidence

- [[sources/agents-md-guide]]
- [[sources/agents-md-cars-guide]]

## Open Questions

- 200 行建议在不同项目类型（前端/后端/全栈/数据）的适用性差异。
- 嵌套 AGENTS.md 的层级深度限制和优先级规则是否标准化。
- AGENTS.md 与 `CLAUDE.md` 在长期是否可能完全合并，还是保持软链接兼容。
- C.A.R.S 结构在非 Web 项目（移动端、数据工程、ML pipeline）中的适用性。
- 索引模式切换的触发条件——"超过 300 行"是硬规则还是经验法则？
