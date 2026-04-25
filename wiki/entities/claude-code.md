---
title: Claude Code
type: entity
status: active
updated: 2026-04-25
source_count: 3
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

## Relationships

- Related entities: [[entities/github-actions]], [[entities/llm-agent]], [[entities/claude-mem]], [[entities/harness]]
- Related concepts: [[concepts/team-governance-for-ai-coding]], [[concepts/policy-driven-tool-permissions]], [[concepts/context-and-cost-optimization]], [[concepts/persistent-agent-memory]]

## Evidence

- [[sources/claude-code-enterprise-playbook]]
- [[sources/ai-template2-scaffold]]
- [[sources/claude-mem]]

## Open Questions

- 在不同团队规模下，最小可行治理配置应如何分级定义。
