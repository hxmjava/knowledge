---
title: 持久化 Agent 记忆
type: concept
status: active
updated: 2026-04-25
source_count: 1
---

# Concept: 持久化 Agent 记忆

## 定义

持久化 agent 记忆把有用的项目上下文存放在当前聊天窗口之外，让 AI 编码 agent 可以跨会话回忆之前的工作、决策、失败记录和文件级观察。

## 为什么重要

长期开发工作往往跨越许多次对话。没有持久记忆时，用户需要反复解释项目历史；有了记忆后，agent 可以更接近真实工作状态地开始。

## 核心组成

- 捕获层：通过 hooks 或工具记录 agent 活动中的观察。
- 存储层：持久保存会话、提示词、观察和摘要。
- 检索层：通过搜索工具按需暴露相关记忆。
- 治理层：用隐私过滤、修剪和可审计性，防止记忆变成失控的上下文堆积。

## 支持来源

- [[sources/claude-mem]]

## 相关页面

- [[entities/claude-mem]]
- [[entities/claude-code]]
- [[concepts/persistent-wiki-compilation]]
- [[concepts/progressive-disclosure-context-retrieval]]

## 矛盾 / 细节

- 持久记忆不等于已整理知识。它改善连续性，但稳定结论仍需要综合、来源追踪和矛盾处理。
- 如果缺少明确的检索和保留策略，更多记忆也可能意味着更多过时或敏感上下文。
