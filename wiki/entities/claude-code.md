---
title: Claude Code
type: entity
status: active
updated: 2026-05-13
source_count: 9
---

# Entity: Claude Code

## What It Is

Claude Code 是面向开发工作流的 AI 编码代理工具，在企业场景中可作为团队级开发基础设施的一部分，也可通过插件、hooks、skills 和项目级约束扩展为更完整的协作环境。

## Relevance

该实体连接本 wiki 中的规范配置、权限治理、CI/CD 自动化与性能成本管理等核心主题。

## Key Facts

- 支持 `CLAUDE.md` 分层配置（全局/项目/子目录）。
- 可与 GitHub Actions 集成，支持 PR 自动审查与评论交互。
- 具备权限控制机制（Allow/Ask/Deny）与工具白名单配置能力。
- 可通过插件安装 [[entities/claude-mem]] 这类跨会话记忆系统。
- 可通过项目 harness 定义斜杠命令、分层 agents、专项检查技能和 lifecycle hooks。
- Superpowers 将其从问答模型约束为守流程的工程协作者：14 个 skill 构成四层架构（流程控制→执行隔离→质量保障→收尾元能力），通过功能开发链和调试链两条主链路驱动工作流。
- 通过 `CLAUDE.md`（即 AGENTS.md 的兼容形式，`ln -s AGENTS.md CLAUDE.md`）注入项目上下文，是"地图，而非手册"理念的原始推动者。
- Skill 生态可扩展到非代码产出领域：如 [[entities/fireworks-tech-graph]] 将技术图生成封装为声明式 Skill（自然语言→SVG/PNG），覆盖 14 种图类型和 7 种视觉风格。
- 可通过 MCP 接入代码结构图谱工具：如 [[entities/code-review-graph]] 通过 MCP Server 暴露影响面查询，Claude Code 在评审时先查图再读代码，平均节省 8.2× token。
- Karpathy 提出 4 条 CLAUDE.md 核心规则（说明假设→简单方案→必要改动→循环验证），Forrest Chang 整理为开源模板，Mnimiy 在 30 个代码库上扩展到 12 条并声称错误率从 41% 降到 3%。CLAUDE.md 定性为"轻量行为契约"而非提示词——仓库级别的跨会话工作约定。
- Superpowers 的主要接入路径之一：通过 `SessionStart` hook + `hooks/hooks.json` 配置注入 `using-superpowers` 引导上下文（路径 A），输出格式为 `hookSpecificOutput.additionalContext`。支持 `/plugin install` 官方市场和 Superpowers 市场两种安装方式。
- 可被改造为**自进化系统**：四层架构（认知核心 + 子智能体 + 路径作用域规则 + 进化引擎），通过 memory/ 目录的 JSONL 文件持久化纠正和观察，每条规则附带 `verify:` 机器可检查行，会话启动时自动执行验证扫描。
- 子智能体模式：architect（规划，只读工具，sonnet 模型）和 reviewer（提交前验证，只读工具）在隔离上下文窗口启动——3+ 文件变更时自动触发 architect。
- 路径作用域规则：`.claude/rules/` 中的 `.md` 文件通过 frontmatter `paths:` 字段限定加载范围（如安全规则只在 `src/api/**/*` 激活），上下文保持精简。
- Hooks 从"安全提醒"升级为"结构性执行"：SessionStart 注入验证扫描指令、PreToolUse 提醒检查路径规则、Stop 提醒记录会话评分——"让一切变成结构性的而非依赖 agent 的自觉性"。
- CLAUDE.md 建议控制在 150 行以内（超过指令遵从度下降），领域特定规则移到 `.claude/rules/`——与 200 行建议的差异来自 Commands/Architecture 是否计入。

## Relationships

- Related entities: [[entities/github-actions]], [[entities/llm-agent]], [[entities/claude-mem]], [[entities/harness]], [[entities/agents-md]], [[entities/harness-creator]], [[entities/fireworks-tech-graph]], [[entities/code-review-graph]], [[entities/meta-alchemist]]
- Related concepts: [[concepts/team-governance-for-ai-coding]], [[concepts/policy-driven-tool-permissions]], [[concepts/context-and-cost-optimization]], [[concepts/persistent-agent-memory]], [[concepts/map-not-manual]], [[concepts/behavioral-contract-vs-prompt]], [[concepts/reminders-vs-hard-enforcement]], [[concepts/self-evolving-agent-system]], [[concepts/verification-sweep]], [[concepts/rule-promotion-ladder]]

## Evidence

- [[sources/claude-code-enterprise-playbook]]
- [[sources/ai-template2-scaffold]]
- [[sources/claude-mem]]
- [[sources/superpowers-workflow-deconstruction]]
- [[sources/agents-md-guide]]
- [[sources/fireworks-tech-graph]]
- [[sources/superpowers-deep-practice-guide]]
- [[sources/code-review-graph]]
- [[sources/claude-md-error-rate-reduction]]
- [[sources/agents-md-cars-guide]]
- [[sources/self-evolving-claude-code]]

## Open Questions

- 在不同团队规模下，最小可行治理配置应如何分级定义。
