---
title: Claude-Mem
type: entity
status: active
updated: 2026-04-25
source_count: 1
---

# Entity: Claude-Mem

## 是什么

Claude-Mem 是一个 Claude Code 插件，用于增加跨会话、可搜索的项目记忆。它捕获 agent 活动中的观察，生成摘要，存储到本地，并通过搜索工具和 Web 查看器暴露出来。

## 相关性

Claude-Mem 是 [[concepts/persistent-agent-memory]] 的具体实现。它位于短期聊天上下文与持久 wiki 综合之间：比本 vault 的手动 ingest 流程更自动，但不如 [[concepts/persistent-wiki-compilation]] 那样经过整理和审阅。

## 关键事实

- 通过 Claude Code 插件市场安装。
- 提供 `mem-search` 技能，用自然语言查询项目历史。
- 在本地 `37777` 端口运行 worker 服务，提供 API 端点和 Web 查看器。
- 使用 SQLite 存储会话、观察和摘要。
- 使用 Chroma 做语义 + 关键词混合检索。
- 支持 `<private>` 标签，将敏感内容排除在存储之外。

## 关系

- 相关实体: [[entities/claude-code]], [[entities/llm-agent]]
- 相关概念: [[concepts/persistent-agent-memory]], [[concepts/progressive-disclosure-context-retrieval]], [[concepts/context-and-cost-optimization]]

## 证据

- [[sources/claude-mem]]

## 开放问题

- 自动捕获的记忆应被视为证据、工作记忆，还是两者兼有？
- 团队应如何长期审计和修剪记忆存储？
