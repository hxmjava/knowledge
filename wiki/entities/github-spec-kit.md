---
title: GitHub Spec Kit
type: entity
status: active
updated: 2026-05-13
source_count: 1
---

# Entity: GitHub Spec Kit

## What It Is

github/spec-kit 是 GitHub 官方推出的 SDD（Spec-Driven Development）工具包，旨在为 AI 辅助开发提供规格驱动的工作流基础设施。明确针对"Vibe Coding 的混乱"提出系统性解决方案。

## Relevance

在 Vibecoding 五大方法论中代表 SDD 的具体实现——将"规格作为唯一事实来源"从理念落地为可操作的工具链。

## Key Facts

- 包含四个核心文件：`constitution.md`（项目原则和约束）、`spec.md`（系统行为规格）、`plan.md`（实施计划）、`tasks.md`（可执行任务列表）。
- 命令化工作流：`/speckit.specify` → `/speckit.plan` → `/speckit.tasks`。
- 设计理念："规格是真理"——代码只是规格的表达。
- 与 Superpowers 互补：Spec Kit 定"做什么"，Superpowers 定"怎么执行"。社区推荐两者结合使用。
- GitHub: https://github.com/github/spec-kit

## Relationships

- Related entities: [[entities/superpowers]]（互补：规格 vs 工作流纪律）
- Related concepts: [[concepts/sdd-spec-driven-development]], [[concepts/spec-driven-workflow-and-review-discipline]], [[concepts/spec-coding]]

## Evidence

- [[sources/vibecoding-tdd-atdd-bdd-ddd-sdd]]

## Open Questions

- github/spec-kit 的实际采用率和社区活跃度如何？
- constitution.md 的约束如何被 AI 编码工具强制执行？
- Spec Kit 的命令（`/speckit.specify` 等）是 Claude Code 原生支持还是需要插件？
- 与 OpenSpec 的文件结构和工作流是否存在互操作性？
