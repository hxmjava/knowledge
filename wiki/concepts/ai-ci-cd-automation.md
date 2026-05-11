---
title: AI CI CD Automation
type: concept
status: active
updated: 2026-05-11
source_count: 2
---

# Concept: AI CI CD Automation

## Definition

把 AI 审查、安全扫描与文档生成嵌入 CI/CD 流水线，实现持续、可复现、可追踪的质量保障流程。

## Why It Matters

将 AI 从“开发者临时助手”升级为“流程内质量控制节点”，可提高审查覆盖率并降低人工遗漏。

## Core Components

- PR 自动代码审查
- 安全扫描与风险分级输出
- 评论触发的交互式命令处理
- 主分支 push 后的文档生成

## Supporting Sources

- [[sources/claude-code-enterprise-playbook]]
- [[sources/ai-coding-paradigms-618-practice]]

## Related Pages

- [[entities/github-actions]]
- [[entities/claude-code]]
- [[concepts/policy-driven-tool-permissions]]

## Contradictions / Nuance

- 自动化结果并不等于合规结论；关键业务与高风险变更仍需人工复核。
- [[sources/ai-coding-paradigms-618-practice]] 将 CI/CD 自动化提升为独立的"Harness 范式"（自动化先行，交付驱动），主张 Harness 不仅做 CI/CD，更是"限制交付边界的框架"——比本概念定义的"流水线内质量控制节点"更宽泛。两者有交集但视角不同。
