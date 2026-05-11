---
title: Claude Code
type: entity
status: active
updated: 2026-05-11
source_count: 6
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
- Superpowers 的主要接入路径之一：通过 `SessionStart` hook + `hooks/hooks.json` 配置注入 `using-superpowers` 引导上下文（路径 A），输出格式为 `hookSpecificOutput.additionalContext`。支持 `/plugin install` 官方市场和 Superpowers 市场两种安装方式。

## Relationships

- Related entities: [[entities/github-actions]], [[entities/llm-agent]], [[entities/claude-mem]], [[entities/harness]], [[entities/agents-md]], [[entities/harness-creator]], [[entities/fireworks-tech-graph]]
- Related concepts: [[concepts/team-governance-for-ai-coding]], [[concepts/policy-driven-tool-permissions]], [[concepts/context-and-cost-optimization]], [[concepts/persistent-agent-memory]], [[concepts/map-not-manual]]

## Evidence

- [[sources/claude-code-enterprise-playbook]]
- [[sources/ai-template2-scaffold]]
- [[sources/claude-mem]]
- [[sources/superpowers-workflow-deconstruction]]
- [[sources/agents-md-guide]]
- [[sources/fireworks-tech-graph]]
- [[sources/superpowers-deep-practice-guide]]

## Open Questions

- 在不同团队规模下，最小可行治理配置应如何分级定义。
