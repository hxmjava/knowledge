# Wiki Index

本页是 wiki 的主要导航层。
深入阅读前优先查看本页。

## Overview

- [[overview]] - 所有已处理来源的当前高层综合。
- [[quickstart]] - ingest/query/lint 操作的可复用提示词。

## Sources

- [[sources/llm-wiki-pattern]] - 构建持久化、由 LLM 维护的个人 wiki 的模式提案。
- [[sources/claude-code-enterprise-playbook]] - Claude Code 企业治理、CI/CD、安全与性能实施指南。
- [[sources/openspec-superpowers-practice-guide]] - 面向 AI 团队开发的“规格优先 + 执行纪律”工作流模式。
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
