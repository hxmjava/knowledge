---
title: swingerman/atdd
type: entity
status: active
updated: 2026-05-13
source_count: 1
---

# Entity: swingerman/atdd

## What It Is

swingerman/atdd 是一个面向 Claude Code（支持 Cursor 等编辑器）的 ATDD（验收测试驱动开发）插件，灵感来源于 Uncle Bob 的 empire-2025 项目。它实现了 Uncle Bob 风格的纯领域语言验收测试工作流，包含泄露检查和变异测试能力。

## Relevance

在 Vibecoding 五大方法论中代表 ATDD 的具体实现——通过 Claude Code 插件形式将"纯领域语言验收规格"落地为可操作的 AI 编码约束。

## Key Facts

- 插件类型：Claude Code 插件（同时支持 Cursor 等编辑器）。
- 核心命令：
  - `/atdd:atdd` — 启动 ATDD 流程
  - `/atdd:spec-check` — 检查规格中的实现细节泄露
  - `/atdd:mutate` — 运行变异测试
- 工作模式：纯领域语言的 Given-When-Then 规格，禁止任何实现细节（类名、API、数据库表）。
- 双流测试架构：验收测试（WHAT）+ 单元测试（HOW）必须同时通过。
- 多代理团队编排：Spec Writer（编写规格）、Implementer（实现代码）、Spec Guardian（守护规格纯度）。
- 灵感来源：Uncle Bob 的 empire-2025 项目。
- GitHub: https://github.com/swingerman/atdd

## Relationships

- Related concepts: [[concepts/atdd-for-ai-coding]], [[concepts/bdd-for-ai-coding]]
- Related entities: [[entities/github-spec-kit]], [[entities/superpowers]]

## Evidence

- [[sources/vibecoding-tdd-atdd-bdd-ddd-sdd]]

## Open Questions

- swingerman/atdd 的多代理团队编排对个人开发者是否过度？
- 变异测试（Mutation Testing）在 AI 生成代码上的实际效果和性能开销如何？
- `/atdd:spec-check` 的泄露检查规则是否可自定义？
- 插件在 Cursor 等编辑器中的功能完整度是否与 Claude Code 一致？
