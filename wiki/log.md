# Wiki Log

Append-only operational timeline.

## [2026-04-25] refactor | 默认中文输出规则

### Scope

- 更新规则文件: `AGENTS.md`
- 中文化本次 Claude-Mem 录入相关页面: `wiki/sources/claude-mem.md`, `wiki/entities/claude-mem.md`, `wiki/concepts/persistent-agent-memory.md`, `wiki/concepts/progressive-disclosure-context-retrieval.md`
- 中文化相关 hub/任务/日志摘要: `wiki/index.md`, `wiki/overview.md`, `wiki/tasks/backlog.md`, `wiki/log.md`

### Outcomes

- 明确 agent 回复、wiki 页面、index 摘要、overview 综合、tasks 和 log 默认使用简体中文。
- 保留工具名、命令、项目名、路径、来源标题和会降低精度的技术术语原文。
- 将刚录入的 Claude-Mem 相关内容调整为中文表达，保持链接和证据关系不变。

### Open Questions / Next Actions

- 后续 lint 可逐步中文化更早的英文模板与历史页面。

## [2026-04-25] ingest | Claude-Mem 持久化记忆

### Scope

- 新增来源页面: `wiki/sources/claude-mem.md`
- 新增实体页面: `wiki/entities/claude-mem.md`
- 新增概念页面: `wiki/concepts/persistent-agent-memory.md`, `wiki/concepts/progressive-disclosure-context-retrieval.md`
- 更新相关页面: `wiki/entities/claude-code.md`, `wiki/concepts/context-and-cost-optimization.md`, `wiki/concepts/hooks-as-safety-net.md`, `wiki/concepts/persistent-wiki-compilation.md`
- 更新 hub/任务页面: `wiki/overview.md`, `wiki/index.md`, `wiki/tasks/backlog.md`

### Outcomes

- 完成 `raw/sources/claude-mem.md` 的录入。
- 将 Claude-Mem 记录为一个具体的 Claude Code 持久化记忆系统，包含 hooks、worker 服务、SQLite、Chroma、Web 查看器和 `mem-search`。
- 新增“持久化 agent 记忆”和“渐进式上下文检索”两个可复用概念，并接入既有的上下文成本与 wiki 编译主题。
- 标出自动记忆捕获与可审计、经整理 wiki 综合之间的张力。

### Open Questions / Next Actions

- 定义自动捕获 agent 记忆的隐私、保留和修剪规则。
- 判断何时 Claude-Mem 式记忆搜索已经足够，何时应提升为整理后的 wiki 页面。
- 评估个人 vault 和小团队可接受的本地基础设施成本。

## [2026-04-24] ingest | ai_template2 Multi-Module AI Collaboration Scaffold

### Scope

- Added raw source: `raw/sources/ai-template2-scaffold.md`
- Added source page: `wiki/sources/ai-template2-scaffold.md`
- Added entity page: `wiki/entities/harness.md`
- Added concept pages: `wiki/concepts/layered-project-harness.md`, `wiki/concepts/specialized-agent-pattern.md`, `wiki/concepts/tdd-as-hard-gate.md`, `wiki/concepts/hooks-as-safety-net.md`
- Updated hub pages: `wiki/index.md`, `wiki/overview.md`

### Outcomes

- Completed ingest from ai_template2 scaffold (`D:/Users/Administrator/Desktop/AI/ai_template2`).
- Captured the concrete integration of OpenSpec + Superpowers + Claude Code Harness into a single project template.
- Added new entity (Harness) and 4 concepts: layered harness organization, specialized agent routing, TDD hard gates, and lifecycle hooks as safety net.
- Expanded the wiki from theoretical workflow patterns to a concrete, deployable scaffold reference.

### Open Questions / Next Actions

- Decide whether to adapt this scaffold for an actual project (replacing placeholders).
- Explore whether hooks should be fail-closed for security-sensitive projects.
- Define a minimum viable subset of the 9 commands + 6 skills + 4 agents for small teams.

## [2026-04-24] ingest | OpenSpec + Superpowers 源文件完整入库

### Scope

- 更新源页面: `wiki/sources/openspec-superpowers-practice-guide.md`（补充五阶段流水线、场景决策表、FAQ、dlabel-cloud-mall 实战案例、常见问题与改进建议）
- 更新实体页面: `wiki/entities/openspec.md`（补充目录结构、核心命令、安装方式），`wiki/entities/superpowers.md`（补充七步流程、TDD 纪律、安装方式、目录结构）
- 更新概念页面: `wiki/concepts/spec-driven-workflow-and-review-discipline.md`（补充场景决策表、常见坑模式）
- 更新合成页面: `wiki/overview.md`

### Outcomes

- Raw 源文件全部关键内容已录入 wiki：OpenSpec/Superpowers 工作流、五阶段流水线、场景分级、实战案例、经验教训。
- 实体页面现在包含可操作的目录结构和命令参考。
- 概念页面新增常见坑模式，便于后续项目参考。

### Open Questions / Next Actions

- 沉淀统一的 DoD（Definition of Done）模板供 AI 开发使用。
- 明确任务规模触发完整 Superpowers 链路的阈值。

## [2026-04-24] ingest | OpenSpec + Superpowers 规范开发指南

### Scope

- Added source page: `wiki/sources/openspec-superpowers-practice-guide.md`
- Added entity pages: `wiki/entities/openspec.md`, `wiki/entities/superpowers.md`
- Added concept page: `wiki/concepts/spec-driven-workflow-and-review-discipline.md`
- Updated hub pages: `wiki/index.md`, `wiki/overview.md`

### Outcomes

- Completed ingest from `raw/sources/OpenSpec + Superpowers规范开发指南.md`.
- Added the OpenSpec + Superpowers operational layer and its key entities/concept links.
- Connected spec-driven governance concepts into the existing enterprise + personal workflow graph.

### Open Questions / Next Actions

- Define explicit thresholds for when full Superpowers chain is mandatory vs. minimal-flow exceptions.
- Decide whether to add a task-level minimum evidence rubric and make it a shared checklist.

## [2026-04-22] refactor | Initialize LLM wiki scaffold

### Scope

- Created schema: `AGENTS.md`
- Created base directories under `raw/` and `wiki/`
- Added starter pages: `wiki/index.md`, `wiki/overview.md`, `wiki/tasks/backlog.md`
- Added workflow templates in `wiki/templates/`

### Outcomes

- Vault is now structured for ingest/query/lint operations.
- Index and log conventions are defined and ready for first source ingest.

### Open Questions / Next Actions

- Add first source into `raw/sources/`.
- Run first ingest to create the initial source + concept/entity graph.

## [2026-04-22] ingest | LLM Wiki

### Scope

- Added source page: `wiki/sources/llm-wiki-pattern.md`
- Added entity pages: `wiki/entities/llm-agent.md`, `wiki/entities/obsidian.md`
- Added concept pages: `wiki/concepts/persistent-wiki-compilation.md`, `wiki/concepts/ingest-query-lint-loop.md`, `wiki/concepts/schema-driven-maintenance.md`
- Updated hub pages: `wiki/overview.md`, `wiki/index.md`

### Outcomes

- Completed first source ingest from `raw/sources/llm-wiki.md`.
- Established initial cross-linked graph across source, entities, and concepts.
- Captured key operating loop (ingest/query/lint) and schema governance concept.

### Open Questions / Next Actions

- Ingest at least 2-3 external examples to test contradictions and refine concepts.
- Decide whether to create an initial analysis page comparing this pattern vs classic RAG workflows.

## [2026-04-22] ingest | Claude Code 综合实战完整指南

### Scope

- Added source page: `wiki/sources/claude-code-enterprise-playbook.md`
- Added entity pages: `wiki/entities/claude-code.md`, `wiki/entities/github-actions.md`
- Added concept pages: `wiki/concepts/team-governance-for-ai-coding.md`, `wiki/concepts/policy-driven-tool-permissions.md`, `wiki/concepts/ai-ci-cd-automation.md`, `wiki/concepts/context-and-cost-optimization.md`
- Updated hub pages: `wiki/overview.md`, `wiki/index.md`

### Outcomes

- Completed ingest from `raw/sources/综合实战完整指南.md`.
- Expanded wiki from conceptual pattern layer to enterprise execution layer.
- Captured actionable governance dimensions: team standards, permission policy, CI/CD automation, and performance-cost controls.

### Open Questions / Next Actions

- Create a durable comparison analysis between personal LLM wiki workflows and enterprise Claude Code governance workflows.
- Add a task page for “minimum secure baseline” templates (`CLAUDE.md`, permissions, and GitHub Actions) for small teams.

## [2026-04-22] query | Personal vs Enterprise LLM Workflows

### Scope

- Added analysis page: `wiki/analyses/personal-vs-enterprise-llm-workflows.md`
- Updated navigation: `wiki/index.md`

### Outcomes

- Produced a durable comparison between personal knowledge-compilation workflows and enterprise AI engineering governance.
- Added a migration path from lightweight personal usage to policy-driven CI/CD operations.

### Open Questions / Next Actions

- Convert the decision framework into a checklist template for team onboarding.
- Define a “minimum secure baseline” starter pack for 1-10 person teams.
