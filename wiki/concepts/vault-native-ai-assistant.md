---
title: Vault-Native AI 助手
type: concept
status: active
updated: 2026-05-06
source_count: 1
---

# Concept: Vault-Native AI 助手

## Definition

将 AI agent 直接嵌入笔记工作区（如 Obsidian），使整个笔记库成为 AI 的工作上下文，而非通过外部聊天窗口手动复制粘贴笔记内容。AI 与笔记作者共处同一编辑环境，可在不切屏的情况下完成问答、润色、总结等操作。

## Why It Matters

传统的 AI 使用模式要求用户在笔记工具和 AI 聊天窗口之间来回切换，割裂了写作和知识整理的思维流。Vault-native 模式消除了这个摩擦：AI 就在光标旁边，笔记直接是上下文。这对知识密集型工作（研究、写作、项目复盘）效率提升显著。

这也与本 wiki 的核心工作流——LLM 辅助增量知识编译——直接相关：vault-native AI 可以更低成本地实现 ingest、query 和 lint 操作。

## Core Components

- **上下文注入**：AI 直接读取 vault 文件作为上下文源，无需手动复制。
- **精准指定**：通过 @ 提及或选中文字，限定 AI 的阅读范围，控制噪声和成本。
- **就地操作**：润色结果可直接替换选中文字，diff 预览确保可控。
- **模板触发**：斜杠命令（/）或自定义前缀（$）提供结构化 prompt，降低使用门槛。
- **多模型切换**：支持多个 AI 提供方（如 Claude 和 Codex），按场景选择。

## Supporting Sources

- [[sources/claudian-obsidian-plugin]]

## Related Pages

- [[entities/claudian]]
- [[entities/obsidian]]
- [[concepts/persistent-wiki-compilation]]
- [[concepts/context-and-cost-optimization]]

## Contradictions / Nuance

- "Vault-native" 的粒度值得区分：是将整个 vault 作为上下文（可能超 token 限制），还是通过检索机制选取相关片段？前者简单但有规模瓶颈，后者更复杂但可扩展。
- 与 RAG（检索增强生成）模式的关系：vault-native 可以是纯上下文注入，也可以结合向量检索，两者在成本和精度上存在权衡。
