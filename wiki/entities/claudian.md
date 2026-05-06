---
title: Claudian
type: entity
status: active
updated: 2026-05-06
source_count: 1
---

# Entity: Claudian

## What It Is

Claudian 是一个 Obsidian 插件，将 Claude Code 和 Codex 等 AI Agent 接入笔记库，使 AI 能够读取、理解和操作保险库内容，成为 vault-native 的协作助手，而非独立的聊天窗口。

GitHub 仓库：https://github.com/YishenTu/claudian

## Relevance

Claudian 代表了一种 vault-native AI 的实现路径：将 AI 嵌入笔记工作区，让笔记库直接作为 AI 的工作上下文。这与本 wiki 关注的 LLM 辅助知识编译主题高度相关——从"人工编译"走向"AI 辅助编译"。

## Key Facts

- 通过 BRAT 安装，尚未正式上架 Obsidian 社区市场。
- 支持两种 AI 提供方：Claude CLI（Anthropic）和 Codex（OpenAI），可在设置中切换。
- 核心交互模式：
  - **vault 问答**：AI 读取笔记库作为上下文回答问题，支持 @ 精准指定文件。
  - **选中润色**：选中文字后快捷键（Ctrl+Shift+E）触发 AI 优化，带词级 diff 预览。
  - **侧边栏对话**：Cmd+Shift+C / Ctrl+Shift+C 调出。
  - **斜杠命令 / 技能模板**：`/` 或 `$` 触发预设提示词，支持用户级和保险库级两种模板范围。
- 界面语言支持中文。
- 接入 Claude 时需本机已安装 Claude Code 并完成 `claude` 登录授权。
- 接入 Codex 时需本机已安装 Codex 桌面 app。

## Relationships

- Related entities: [[entities/obsidian]], [[entities/brat]], [[entities/claude-code]]
- Related concepts: [[concepts/vault-native-ai-assistant]], [[concepts/structured-tag-system-for-ai]]

## Evidence

- [[sources/claudian-obsidian-plugin]]

## Open Questions

- 大型 vault 的上下文处理策略（是否支持 RAG/检索增强）。
- 与 Obsidian Copilot、Smart Connections 等同类插件的架构对比。
- 插件成熟度：BRAT 分发意味着仍处于 beta 阶段，稳定性和安全性待验证。
