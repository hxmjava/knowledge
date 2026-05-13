# Wiki Index

本页是 wiki 的主要导航层。
深入阅读前优先查看本页。

## Overview

- [[overview]] - 所有已处理来源的当前高层综合。
- [[quickstart]] - ingest/query/lint 操作的可复用提示词。

## Sources

- [[sources/llm-wiki-pattern]] - 构建持久化、由 LLM 维护的个人 wiki 的模式提案。
- [[sources/claude-code-enterprise-playbook]] - Claude Code 企业治理、CI/CD、安全与性能实施指南。
- [[sources/openspec-superpowers-practice-guide]] - “规格优先 + 执行纪律”工作流模式，含五阶段流水线、工程化目录详解、TDD-driven schema、AI 编码技巧、上下文管理策略与 Obsidian 软链接集成。
- [[sources/ai-coding-advanced-openspec-superpowers-deep-guide]] - OpenSpec + Superpowers 的深度教程化落地：fast-forward 入口、购物车案例、失败修复路径与备用网址补记。
- [[sources/ai-template2-scaffold]] - 整合 OpenSpec、Superpowers 和 Claude Code Harness 的多模块 AI 协作脚手架。
- [[sources/claude-mem]] - 面向 Claude Code 的持久化记忆压缩系统，使用 hooks、本地存储、搜索和渐进式披露。
- [[sources/claudian-obsidian-plugin]] - Claudian 插件：将 Claude/Codex 接入 Obsidian 笔记库，实现 vault-native AI 问答、润色和模板触发。
- [[sources/superpowers-workflow-deconstruction]] - Superpowers 14-skill 四层架构拆解与两条主链路（功能开发链、调试链），强调工程纪律而非功能堆叠。
- [[sources/agents-md-guide]] - AGENTS.md 实践指南：地图而非手册原则、五大实践（仓库聚合、统一环境、验证闭环、自动化检查、参考项目引入）、Bad Case 驱动迭代。
- [[sources/figma-personal-access-tokens]] - Figma 官方 PAT 管理指南：全量访问令牌的生成、撤销与安全限制。
- [[sources/fireworks-tech-graph]] - 声明式技术图生成 Skill：自然语言→SVG/PNG，14 种图类型 × 7 种视觉风格，五层架构含语义表达。
- [[sources/superpowers-deep-practice-guide]] - Superpowers 全面深度实战指南：架构全景、8 平台安装、14 skill 深度解析、插件系统技术细节、技能设计哲学与 React Todo List 实战示例。
- [[sources/ai-coding-paradigms-618-practice]] - 企业级AI Coding五范式组合实战：618促销场景下Spec/TDD/Glue/Harness/Vibe的系统化对比、量化指标与PM角色协作。
- [[sources/code-review-graph]] - 代码结构图谱工具：Tree-sitter + SQLite 本地图谱 + MCP 查询，将 AI 评审上下文从全量灌入转为按结构关系检索，平均 token 节省 8.2×。
- [[sources/claude-md-error-rate-reduction]] - CLAUDE.md 行为契约深度分析：Karpathy 4 规则→12 规则扩展（41%→3%）、三层文件结构、提醒 vs 硬约束分工、规则来自翻车记录的迭代方法论。
- [[sources/agents-md-cars-guide]] - AGENTS.md C.A.R.S 组织框架：Commands/Architecture/Restrictions/Standards 四区块、跨工具兼容矩阵、大项目索引模式、30-40 行紧凑模板。
- [[sources/vibecoding-tdd-atdd-bdd-ddd-sdd]] - Vibecoding 五大方法论工程化护栏：TDD/ATDD/BDD/DDD/SDD 协同实践，分层定位模型，BDD vs ATDD 深度对比，github/spec-kit、swingerman/atdd、obra/superpowers 工具实践。
- [[sources/self-evolving-claude-code]] - Claude Code 自进化系统完整指南：四层架构（认知核心+子智能体+路径作用域规则+进化引擎）、验证扫描、规则晋升阶梯、hooks 结构化执行、免疫系统隐喻。

## Entities

- [[entities/llm-agent]] - 作为持续 wiki 维护者的 agent，而不是一次性聊天机器人。
- [[entities/obsidian]] - wiki 的 Markdown 工作区与可视化界面。
- [[entities/openspec]] - AI 辅助开发中的规格驱动层与变更追踪机制。
- [[entities/superpowers]] - AI 开发中的执行纪律与任务编排层，并强调按需加载核心 skills。
- [[entities/claude-code]] - 面向团队工作流的核心 AI 编码平台实体。
- [[entities/github-actions]] - 将 AI 审查落地到 CI/CD 的自动化平台。
- [[entities/harness]] - 编排分层 agents、专项技能和生命周期 hooks 的多 agent 协作层。
- [[entities/claude-mem]] - Claude Code 插件，用于持久、可搜索的跨会话项目记忆。
- [[entities/claudian]] - Obsidian 插件，将 Claude Code 和 Codex 接入笔记库，提供 vault-native AI 协作。
- [[entities/brat]] - Obsidian 测试版插件安装工具，用于安装未上架社区市场的 beta 插件。
- [[entities/cc-switch]] - 跨平台桌面 All-in-One 管理工具，统一管理 Claude Code、Codex、Gemini CLI 等 AI 编码 CLI 的 Provider、MCP、Prompts 与 Skills。
- [[entities/agents-md]] - AI Coding 项目指令的开放标准文件（"给 AI 看的 README"），由 Agentic AI Foundation 托管。
- [[entities/harness-creator]] - 一键生成 AGENTS.md 及配套 lint 脚本、Makefile、验证基础设施的 Skill。
- [[entities/figma]] - 基于浏览器的协作设计平台，通过 PAT 授权 API 访问，是设计-to-code 管道的上游数据源。
- [[entities/fireworks-tech-graph]] - Claude Code Skill，将自然语言描述转成可发布的 SVG+PNG 技术图，覆盖 14 种图类型和 7 种视觉风格。
- [[entities/lv-zhaobo]] - 企业级AI Coding实践者，「沐然云计算」公众号作者，提出五范式分类与组合策略。
- [[entities/muran-cloud]] - 微信公众号，聚焦企业级AI Coding实践和研发效能提升。
- [[entities/code-review-graph]] - 开源本地代码结构图工具，Tree-sitter + SQLite 图谱 + MCP 接口，通过影响面分析优化 AI 代码评审的上下文效率。
- [[entities/ai-cheatcode]] - 微信公众号，聚焦 AI 编程工具的技术深度评测（代码评审、上下文优化、MCP 生态）。
- [[entities/ruofei]] - 微信公众号「架构师」运营者，聚焦 AI 编程、Agent Harness、上下文工程与软件架构。
- [[entities/jiagoux]] - 微信公众号「架构师」（JiaGouX），由若飞运营，关注软件架构与 AI 编程实践。
- [[entities/karpathy]] - AI 领域知名研究者，提出 CLAUDE.md 4 条核心规则（假设→简单→必要→验证）。
- [[entities/forrest-chang]] - 将 Karpathy 4 条规则整理为开源 CLAUDE.md 模板。
- [[entities/mnimiy]] - AI 编程实践者，30 代码库 6 周扩展 Karpathy 规则至 12 条，声称错误率 41%→3%。
- [[entities/mitchell-hashimoto]] - HashiCorp 联合创始人，提出"Agent 犯错后要补机制"原则。
- [[entities/miao]] - 微信公众号「肥喵学AI」运营者，聚焦 AI 编码工具实践，提出 AGENTS.md 的 C.A.R.S 结构。
- [[entities/fatcat-learn-ai]] - 微信公众号，由米奥运营，关注 AI 编码工具使用体验和最佳实践。
- [[entities/github-spec-kit]] - GitHub 官方 SDD 工具包，constitution.md + spec.md + plan.md + tasks.md，将规格提升为唯一事实来源。
- [[entities/swingerman-atdd]] - Claude Code ATDD 插件，Uncle Bob 风格纯领域语言验收测试、双流测试、变异测试、多代理团队编排。
- [[entities/gis-in-frontend]] - 微信公众号「GIS人在前端」，聚焦 AI 编程方法论与工程化实践。
- [[entities/meta-alchemist]] - AI 工程实践博主（一天天的），提出 Claude Code 四层自进化系统方案。
- [[entities/engineer-juggling]] - 微信公众号「工程师耍杂技」，聚焦 AI 编程工具深度实践教程。

## Concepts

- [[concepts/persistent-wiki-compilation]] - 将知识增量编译为持久页面。
- [[concepts/ingest-query-lint-loop]] - 支撑增长、检索和维护的操作循环。
- [[concepts/schema-driven-maintenance]] - 用 schema 约束保持行为一致。
- [[concepts/team-governance-for-ai-coding]] - 标准化团队 AI 编码实践。
- [[concepts/policy-driven-tool-permissions]] - 用明确策略和信任边界控制工具执行（覆盖 Claude Code 细粒度权限与 Figma 全量 PAT 两种模型）。
- [[concepts/ai-ci-cd-automation]] - 将 AI 审查和安全检查集成进自动化流水线。
- [[concepts/context-and-cost-optimization]] - 优化上下文使用、延迟和成本。
- [[concepts/spec-driven-workflow-and-review-discipline]] - 将 OpenSpec 规格纪律、fast-forward 起步与 Superpowers 执行治理结合。
- [[concepts/layered-project-harness]] - 围绕明确项目层、专属 agents 和验证策略组织 AI 辅助开发。
- [[concepts/specialized-agent-pattern]] - 使用分层 agents 和领域检查技能，而不是单一通用 agent。
- [[concepts/tdd-as-hard-gate]] - 将测试驱动开发视为所有生产代码变更的不可协商门禁，并补充边界/异常/并发校验。
- [[concepts/hooks-as-safety-net]] - 将生命周期 hooks 作为 AI agent 决策旁路的轻量安全提醒。
- [[concepts/persistent-agent-memory]] - 跨 AI agent 会话存储和检索有用项目上下文。
- [[concepts/progressive-disclosure-context-retrieval]] - 按层检索记忆，在连续性、成本和噪声之间取得平衡。
- [[concepts/vault-native-ai-assistant]] - 将 AI 嵌入笔记工作区，笔记库直接作为上下文，消除切换摩擦。
- [[concepts/structured-tag-system-for-ai]] - 为 AI 设计的结构化标签体系，标签质量决定 AI 回答质量。
- [[concepts/verification-before-completion]] - 完成声明必须绑定新鲜验证结果，比 TDD 管控更靠后的交付关口。
- [[concepts/map-not-manual]] - 项目上下文文件应充当导航地图而非完整手册，约 200 行，详细内容通过链接指向专项文档。
- [[concepts/verification-loop]] - 「改→构建→启动→验证」端到端验证闭环，AI 自主执行的前提。
- [[concepts/bad-case-driven-iteration]] - 从 AI 实际犯错出发逐条补充 AGENTS.md 规则，不一次写完。
- [[concepts/reference-projects-as-context]] - 通过 git submodule 引入源码作为 AI 上下文，"源码即文档"。
- [[concepts/diagram-generation-as-skill]] - 声明式技术图生成：自然语言描述→图类型识别→风格渲染→发布级输出的工程化 Skill 能力。
- [[concepts/spec-coding]] - 文档先行范式：先写Spec再编码，适合大型项目需求明确、多方协作场景。
- [[concepts/glue-coding]] - 复用先行范式：优先复用Reference代码快速拼接，适合促销活动等高相似度迭代场景。
- [[concepts/vibe-coding]] - 体验先行范式：A/B测试驱动的UI优化，适合活动页面和交互设计。
- [[concepts/paradigm-composition]] - 范式组合策略：不同项目阶段灵活切换多种研发范式，而非固守单一范式。
- [[concepts/obsidian-project-symlink]] - 通过 Windows 软链接将项目目录映射到 Obsidian vault，一套文件双端管理，消除手动同步。
- [[concepts/code-structure-graph-for-ai]] - 用本地代码结构图谱（Tree-sitter + SQLite）替代全文喂入，AI 先查结构关系再读代码，实现精准上下文供给。
- [[concepts/blast-radius-impact-analysis]] - 从变更点沿调用/导入/测试链逐层扩散的影响面分析，recall 100%、precision 0.38 的安全侧取舍。
- [[concepts/behavioral-contract-vs-prompt]] - CLAUDE.md 是"轻量行为契约"（仓库级跨会话约束）而非提示词技巧（单次对话引导），两者在持久性、范围和意图上根本不同。
- [[concepts/reminders-vs-hard-enforcement]] - CLAUDE.md 是事前提醒（软约束），hooks/权限/CI 是硬约束——前者告诉 Agent 怎么做，后者决定能不能做。
- [[concepts/cars-agents-structure]] - AGENTS.md 的 C.A.R.S 组织框架：Commands/Architecture/Restrictions/Standards，Restrictions（不能做什么）为最高价值区块。
- [[concepts/cross-tool-agents-compatibility]] - 跨工具 AGENTS.md 兼容策略：以 AGENTS.md 为 SSOT，Claude Code 符号链接接入、Cursor `.cursor/rules` 补充、Codex 多层级支持。
- [[concepts/atdd-for-ai-coding]] - ATDD 在 AI 编码中的应用：纯领域语言的 Given-When-Then 验收规格作为最高层行为约束，双流测试 + 变异测试三层验证。
- [[concepts/bdd-for-ai-coding]] - BDD 在 AI 编码中的应用：活文档 + 统一语言 + 跨角色协作，与 ATDD 互补（协作性 vs AI 约束强度）。
- [[concepts/ddd-domain-driven-design]] - DDD 在 AI 编码中的应用：统一语言 + 限界上下文为 AI 提供架构护栏，防止"意大利面条式代码"。
- [[concepts/sdd-spec-driven-development]] - SDD 规格驱动开发：规格作为唯一事实来源，Specify → Clarify → Plan → Tasks → Implement，与 OpenSpec 互补。
- [[concepts/self-evolving-agent-system]] - 自进化 Agent 系统：四层架构（认知核心+子智能体+路径作用域规则+进化引擎），免疫系统隐喻，将静态配置改造为持续自我改进系统。
- [[concepts/verification-sweep]] - 验证扫描机制：会话启动时自动运行所有规则的 verify: 检查，全通过时静默，违规则报告——"没有验证的规则是愿望，有验证的规则才是护栏"。
- [[concepts/rule-promotion-ladder]] - 规则晋升阶梯：纠正→learned-rules→永久配置的量化晋升路径，50 行上限强制晋升或淘汰，/evolve 审计命令。

## Analyses

- [[analyses/personal-vs-enterprise-llm-workflows]] - 对比个人 wiki 编译与企业治理工作流的决策框架。

## Tasks

- [[tasks/backlog]] - 开放研究与维护任务。

## Templates

- [[templates/source-template]] - 标准来源页面结构。
- [[templates/entity-template]] - 标准实体页面结构。
- [[templates/concept-template]] - 标准概念页面结构。
- [[templates/analysis-template]] - 标准分析输出结构。
- [[templates/lint-checklist]] - 周期性维护检查清单。
