---
title: Claude-Mem 持久化记忆系统
type: source
status: active
updated: 2026-04-25
source_count: 1
---

# Source: Claude-Mem 持久化记忆系统

## 元数据

- Raw 文件: `raw/sources/claude-mem.md`
- 作者: Alex Newman / thedotmack
- URL / 发布方: `https://github.com/thedotmack/claude-mem`
- 来源标注版本: 6.5.0
- 来源标注许可证: AGPL-3.0；`ragtime/` 单独使用 PolyForm Noncommercial License 1.0.0

## 摘要

- Claude-Mem 是面向 [[entities/claude-code]] 的持久化记忆压缩系统，用于跨会话保留项目上下文。
- 它会自动捕获工具使用观察、生成语义摘要，并通过 `mem-search` 技能暴露历史工作。
- 架构组合了生命周期 hooks、由 Bun 管理的 worker 服务、SQLite 存储、Chroma 向量搜索，以及运行在 `37777` 端口的本地 Web 查看器。
- 搜索能力是多维度的：观察、会话、提示词、概念、文件、类型、最近上下文、时间线，以及围绕查询结果的时间线上下文。
- 它强调 [[concepts/progressive-disclosure-context-retrieval]]，让 agent 按层检索记忆，并看到 token 成本。
- 隐私控制包括用 `<private>` 标签排除敏感内容存储，但具体执行策略仍需用户或团队制定。

## 关键主张

- 持久化记忆让 Claude Code 在会话结束或重连后仍能保留有用的项目知识。
- 相比手写笔记，自动捕获降低了维护上下文的人工负担。
- 基于 SQLite/全文记录与 Chroma 向量检索的混合搜索，可以同时改善关键词查询和语义查询的召回。
- Web 查看器让记忆流可被审计，而不是变成不可见的后台状态。
- 无尽模式等测试版功能显示其方向是更长时间运行的类生物记忆架构。

## 证据笔记

- 安装流程使用 Claude Code 插件命令：先 `/plugin marketplace add thedotmack/claude-mem`，再 `/plugin install claude-mem`。
- 来源列出的核心组件包括：5 个生命周期 hooks、6 个 hook 脚本、依赖预检查 hook、worker 服务、SQLite 数据库、`mem-search` 技能和 Chroma 向量数据库。
- 系统要求包括 Node.js 18+、支持插件的 Claude Code、Bun、uv 和 SQLite 3。
- 配置存放在 `~/.claude-mem/settings.json`，覆盖模型、worker 端口、数据目录、日志和上下文注入设置。

## 矛盾 / 张力

- 本 wiki 将 `wiki/` 页面视为显式、可人工审阅的编译知识；Claude-Mem 更偏向自动记忆捕获。两者互补，但如果缺少策略，自动记忆可能积累低价值或敏感观察。
- 持久化记忆改善连续性，但也会增加隐私、许可与合规负担，尤其是在 AGPL-3.0 约束和本地保留项目数据的情况下。
- 上下文注入很有用，但若缺少检索纪律，可能重新引入 [[concepts/context-and-cost-optimization]] 想避免的上下文膨胀。

## 关联实体

- [[entities/claude-mem]]
- [[entities/claude-code]]
- [[entities/llm-agent]]

## 关联概念

- [[concepts/persistent-agent-memory]]
- [[concepts/progressive-disclosure-context-retrieval]]
- [[concepts/context-and-cost-optimization]]
- [[concepts/hooks-as-safety-net]]

## 后续问题

- 自动捕获项目记忆时，最低限度的隐私策略应该是什么？
- 什么时候应优先做持久 wiki 综合，而不是只依赖原始记忆搜索？
- 对个人 vault 或小团队而言，多少本地基础设施是可接受的？
