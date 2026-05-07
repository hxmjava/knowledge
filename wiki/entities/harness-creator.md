---
title: harness-creator
type: entity
status: active
updated: 2026-05-07
source_count: 1
---

# Entity: harness-creator

## What It Is

harness-creator 是一个 AI Coding Skill（可在 hiclaw 市场下载），用于一键生成 AGENTS.md 及配套的 lint 脚本、Makefile、验证脚本、参考文档等项目基础设施。它把"AGENTS.md + 文档体系 + lint 脚本 + 启动脚本 + 验证规范"打包为一键生成工具。

## Relevance

该实体是 AGENTS.md 生态中的自动化脚手架，降低了从零开始写 AGENTS.md 的门槛，与 [[entities/harness]] 在理念上一脉相承。

## Key Facts

- 下载地址：https://market.hiclaw.io/skills/product-69e4ee23e4b0491b51db30bd
- 生成物包括：AGENTS.md、分层架构 lint 脚本、Makefile、验证脚本、参考文档模板。
- 与 `/init` 命令互补：`/init` 生成初始 AGENTS.md，harness-creator 生成完整配套基础设施。
- 建议用作起点，后续通过 Bad Case 驱动迭代优化。

## Relationships

- Related entities: [[entities/agents-md]], [[entities/harness]], [[entities/claude-code]]
- Related concepts: [[concepts/bad-case-driven-iteration]], [[concepts/verification-loop]]

## Evidence

- [[sources/agents-md-guide]]

## Open Questions

- harness-creator 生成质量如何？是否需要人工大幅修正？
- 支持哪些技术栈和项目类型？
- 与 ai_template2 脚手架的关系——是互补还是替代？
