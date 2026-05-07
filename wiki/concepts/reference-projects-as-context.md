---
title: 参考项目引入
type: concept
status: active
updated: 2026-05-07
source_count: 1
---

# Concept: 参考项目引入（Reference Projects as Context）

## Definition

通过 git submodule 将闭源组件、开源依赖或其他产品的源码引入项目仓库的 `reference-projects/` 目录，为 AI 提供训练数据中不存在的上下文。核心信条："源码永远不会过时，它就是最准确的文档。"

## Why It Matters

AI 工具的训练数据无法覆盖闭源组件库、内部产品、特定开源项目的对接细节。维护使用文档总是滞后于实现且覆盖不全，而源码永远准确。引入源码后，AI 可以直接读取 TypeScript 定义和实现，写代码质量有质的提升。

## Core Components

- **目录结构**：`reference-projects/` 下按项目划分，通过 git submodule 引入。
- **CI/CD 隔离**：`ignore = all` 避免干扰主流水线，本地按需拉取。
- **架构文档**：每个参考项目配 `docs/design-docs/ref-*.md`，帮助 AI 快速理解参考代码结构。
- **ref 文档与源码的关系**：ref 文档是"地图"（整体结构和关键模块），源码是"细节"（需要时直接去读）。
- **渐进式获取**：AGENTS.md 中通过项目结构树标注每个目录用途，ref 文档提供架构概览，参考优先级规则明确何时看哪个项目。

## Trade-offs

| 方式 | 优点 | 缺点 |
|------|------|------|
| 只写使用文档 | 轻量、聚焦 | 滞后于实现、覆盖不全、边界情况缺失 |
| 引入源码 + 架构说明 | 永远准确、覆盖完整 | 仓库体积增大、需要管理 submodule |

## Supporting Sources

- [[sources/agents-md-guide]]

## Related Pages

- [[entities/agents-md]]
- [[concepts/map-not-manual]]
- [[concepts/context-and-cost-optimization]]

## Contradictions / Nuance

- 引入大量参考仓库可能增加 AI 的上下文检索负担——依赖 AGENTS.md 的渐进式披露设计来避免迷失。
- git submodule 的管理成本（版本锁定、按需拉取）在实际团队协作中可能成为摩擦点。
- 对小型项目或纯前端项目，此模式的投入产出比可能不高。
