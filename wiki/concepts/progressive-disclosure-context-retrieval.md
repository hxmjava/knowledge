---
title: 渐进式上下文检索
type: concept
status: active
updated: 2026-04-25
source_count: 1
---

# Concept: 渐进式上下文检索

## 定义

渐进式上下文检索按层暴露记忆：先使用紧凑摘要或最近上下文，只有在需要时才继续获取更深层的观察、时间线、文件或原始记录。

## 为什么重要

AI agent 需要足够上下文才能做好事，但过多上下文会增加成本、延迟和噪声。渐进式披露让记忆检索变成可调节过程，而不是一次性全量灌入。

## 核心组成

- 摘要优先的检索，用于快速定位。
- 按观察、会话、提示词、概念、文件、类型或时间线限定搜索范围。
- 暴露 token 成本，让 agent 判断是否需要继续深入。
- 从高层上下文逐步升级到精确历史记录的路径。

## 支持来源

- [[sources/claude-mem]]

## 相关页面

- [[entities/claude-mem]]
- [[concepts/persistent-agent-memory]]
- [[concepts/context-and-cost-optimization]]
- [[concepts/ingest-query-lint-loop]]

## 矛盾 / 细节

- 分层检索只有在 agent 真正停在“最小足够层”时，才能减少上下文膨胀。
- 可搜索记忆能回答“过去发生了什么”，但不会自动判断哪些历史上下文仍然有效。
