# Wiki Log

Append-only operational timeline.

## [2026-05-07] ingest | AGENTS.md 实践指南

### Scope

- 保存 raw 来源: `raw/sources/agents-md-guide.md`
- 新增来源页面: `wiki/sources/agents-md-guide.md`
- 新增实体页面: `wiki/entities/agents-md.md`, `wiki/entities/harness-creator.md`
- 新增概念页面: `wiki/concepts/map-not-manual.md`, `wiki/concepts/verification-loop.md`, `wiki/concepts/bad-case-driven-iteration.md`, `wiki/concepts/reference-projects-as-context.md`
- 更新实体页面: `wiki/entities/claude-code.md`, `wiki/entities/harness.md`
- 更新概念页面: `wiki/concepts/progressive-disclosure-context-retrieval.md`, `wiki/concepts/context-and-cost-optimization.md`, `wiki/concepts/spec-driven-workflow-and-review-discipline.md`, `wiki/concepts/verification-before-completion.md`
- 更新 hub 页面: `wiki/overview.md`, `wiki/index.md`

### Outcomes

- 完成微信文章「一个文件让 AI Coding 效率翻倍：AGENTS.md 实践指南」（Kirito的技术分享，2026-04-20）的录入。
- 新增 AGENTS.md 实体——记录其作为事实标准的前世今生（Anthropic CLAUDE.md → 工具碎片化 → AMP+OpenAI 推动统一 → Agentic AI Foundation 托管）。
- 提炼"地图，而非手册"概念：与既有渐进式上下文检索共享底层理念，但适用层次不同（项目上下文文件 vs 记忆系统）。
- 新增"验证闭环"概念：「改→构建→启动→验证」端到端循环，包含 curl 规范、Agent Browser 验证和自动化检查，与 verification-before-completion 互补。
- 新增"Bad Case 驱动迭代"和"参考项目引入"两个实践概念。
- 新增 harness-creator 实体，记录其作为 AGENTS.md 一键脚手架工具的角色。
- 标注了本文与 [[sources/ai-template2-scaffold]] 在 AGENTS.md 丰富度上的张力（200 行精简地图 vs 多层 harness 配置）。

### Open Questions / Next Actions

- AGENTS.md 的 200 行建议在大型 monorepo 中的适用性——OpenAI 88 个嵌套 AGENTS.md 的模式是否可复制。
- harness-creator 生成质量和技术栈覆盖范围待评估。
- "源码即文档"策略在上下文窗口有限的模型中的检索效率问题。
- 验证闭环基础设施的最小可行子集——哪些是必选项、哪些是增强项。

## [2026-05-07] ingest | Superpowers 工作流拆解

### Scope

- 保存 raw 来源: `raw/sources/superpowers-workflow-deconstruction.md`
- 新增来源页面: `wiki/sources/superpowers-workflow-deconstruction.md`
- 新增概念页面: `wiki/concepts/verification-before-completion.md`
- 更新实体页面: `wiki/entities/superpowers.md`, `wiki/entities/claude-code.md`
- 更新概念页面: `wiki/concepts/spec-driven-workflow-and-review-discipline.md`, `wiki/concepts/tdd-as-hard-gate.md`
- 更新 hub 页面: `wiki/overview.md`, `wiki/index.md`

### Outcomes

- 完成微信文章「我把 Claude Code 的 Superpowers 全拆了一遍，终于看懂它真正厉害的地方」（地瓜老爸，2026-03-27）的录入。
- 将 Superpowers 的 14 个 skill 解析为四层架构（总入口/流程控制、实施执行/环境隔离、质量保障/问题处理、收尾/元能力），补充到实体页。
- 提炼两条主链路：功能开发链（brainstorming → plan → worktree → execute → finish）和调试链（systematic-debugging → TDD → verification）。
- 新增 "verification-before-completion" 概念：完成声明必须绑定新鲜验证结果，与 TDD 硬门禁互补但不等价（TDD 管开发过程，此概念管交付关口）。
- 标注了本文与 [[sources/ai-template2-scaffold]] 在"最该默认启用的底线规则"上的优先级差异（本文偏完成纪律，脚手架偏开发纪律）。

### Open Questions / Next Actions

- 14 个 skill 是否全部默认安装，还是按需加载？文章未做说明。
- 功能开发链路中发现 bug 需要切换到调试链路时，切换机制是什么？
- "新鲜"验证结果的精确定义（时间窗口/变更范围阈值）待明确。
- 是否值得将四层架构映射到 harness 的命令分层，形成"配置即文档"。

## [2026-05-06] ingest | Claudian Obsidian 插件

### Scope

- 新增来源页面: `wiki/sources/claudian-obsidian-plugin.md`
- 新增实体页面: `wiki/entities/claudian.md`, `wiki/entities/brat.md`
- 新增概念页面: `wiki/concepts/vault-native-ai-assistant.md`, `wiki/concepts/structured-tag-system-for-ai.md`
- 更新实体页面: `wiki/entities/obsidian.md`
- 更新 hub 页面: `wiki/overview.md`, `wiki/index.md`
- 保存 raw 来源: `raw/sources/claudian-obsidian-plugin.md`

### Outcomes

- 完成微信文章 "Claudian：让 AI 直接长在 Obsidian 里的插件" 的录入。
- 引入 "vault-native AI 助手"概念，与既有 LLM wiki 编译、上下文成本优化等主题形成连接。
- 引入"面向 AI 的结构化标签体系"概念，标记了与 MOC 多标签实践的张力。
- Obsidian 实体页更新，反映插件生态扩展（BRAT 分发、AI 集成场景）。

### Open Questions / Next Actions

- Claudian 对大型 vault（1000+ 笔记）的上下文处理策略是什么？是否支持 RAG？
- 对比 Claudian vs Obsidian Copilot vs Smart Connections 的架构差异。
- 是否值得将标签体系设计模板化，作为 vault 维护的可复用 checklist。
- BRAT 安装的 beta 插件的安全模型和更新策略待调研。

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

## [2026-04-25] ingest | OpenSpec + Superpowers 深度教程

### Scope

- Added source page: `wiki/sources/ai-coding-advanced-openspec-superpowers-deep-guide.md`
- Updated entity pages: `wiki/entities/openspec.md`, `wiki/entities/superpowers.md`
- Updated concept pages: `wiki/concepts/spec-driven-workflow-and-review-discipline.md`, `wiki/concepts/tdd-as-hard-gate.md`
- Updated hub pages: `wiki/overview.md`, `wiki/index.md`
- Updated task page: `wiki/tasks/backlog.md`

### Outcomes

- Ingested the WeChat article `AI 编程进阶：OpenSpec + Superpowers 组合方案深度使用教程` from `https://mp.weixin.qq.com/s/092HGb6sEfz2Q-Pr-jEX2w`.
- Captured its distinct contribution relative to the earlier OpenSpec + Superpowers guide: a more tutorialized, end-to-end path centered on `/opsx:ff → verify → archive`, a shopping-cart example, and a failure-recovery playbook.
- Strengthened existing OpenSpec / Superpowers / spec-driven workflow / TDD pages with practical signals: fast-forward onboarding, minimal core skills, and boundary-condition checks before verification.

### Open Questions / Next Actions

- Verify whether `/opsx:ff` and `verify` are default OpenSpec commands or profile/scaffold-level wrappers.
- Decide whether the shopping-cart edge-case checklist should become a reusable DoD template for stateful features.

## [2026-04-29] refactor | 补录微信文章备用网址并去重校验

### Scope

- 更新来源页面: `wiki/sources/ai-coding-advanced-openspec-superpowers-deep-guide.md`
- 更新导航页: `wiki/index.md`
- 更新操作日志: `wiki/log.md`

### Outcomes

- 复核用户提供的微信链接 `https://mp.weixin.qq.com/s/HJi8n8t5RXFCevn0ezmLNg`，确认 vault 中已存在同标题来源页 `[[sources/ai-coding-advanced-openspec-superpowers-deep-guide]]`，未新建重复页面。
- 在来源页中补记既有 URL 与本次 Alternate URL，保留“同文多链接”痕迹，便于后续追溯。
- 记录本次复核的限制：直连抓取命中 `secitptpage/verify`，因此未从该备用网址重新抽取正文。

### Open Questions / Next Actions

- 如需更强校验，可把文章原文保存到 `raw/sources/`，以便后续脱离微信验证页做稳定比对。
- 若后续再次出现同标题多链接，可考虑给 source 页面增加固定的 “Known URLs” 字段规范。

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
