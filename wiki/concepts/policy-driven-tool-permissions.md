---
title: Policy Driven Tool Permissions
type: concept
status: active
updated: 2026-04-22
source_count: 1
---

# Concept: Policy Driven Tool Permissions

## Definition

以策略方式管理 AI 工具调用权限，包括 Allow/Ask/Deny 级别、白名单/黑名单、环境隔离与审计追踪。

## Why It Matters

企业场景中的核心风险不在“模型会不会写代码”，而在“代理能做什么、是否可控、是否可追责”。

## Core Components

- 权限模型（Allow/Ask/Deny）
- `allowedTools` 与 `disallowedTools` 细粒度匹配
- 开发/生产分环境策略
- MCP 服务信任分级与超时、沙箱策略

## Supporting Sources

- [[sources/claude-code-enterprise-playbook]]

## Related Pages

- [[concepts/team-governance-for-ai-coding]]
- [[entities/claude-code]]
- [[entities/github-actions]]

## Contradictions / Nuance

- 过宽权限提升效率但扩大风险；过严权限增强安全但可能压低交付速度。
