---
title: 持久化 Agent 记忆
type: concept
status: active
updated: 2026-05-13
source_count: 2
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

## 结构化记忆变体（来自自进化系统）

[[sources/self-evolving-claude-code]] 提出比 Claude-Mem 更结构化的记忆方案：

| 维度 | Claude-Mem | 自进化系统 |
|------|-----------|----------|
| 存储格式 | SQLite + Chroma 向量库 | JSONL 追加文件 + Markdown |
| 检索方式 | 语义搜索（渐进式披露） | 文件读取（验证扫描时全量） |
| 验证机制 | 无 | 每条规则附带 `verify:` 行，会话启动自动执行 |
| 晋升机制 | 无（便签式记录） | 量化阶梯：纠正 → learned-rules → 永久配置 |
| 容量治理 | 无明确上限 | `learned-rules.md` 50 行硬上限 |

核心差异：Claude-Mem 强调**检索便利性**（语义搜索、渐进披露），自进化系统强调**规则执行性**（验证检查、自动晋升）。前者是便签本，后者是免疫系统。

## 支持来源

- [[sources/claude-mem]]
- [[sources/self-evolving-claude-code]]

## 相关页面

- [[entities/claude-mem]]
- [[entities/claude-code]]
- [[concepts/persistent-wiki-compilation]]
- [[concepts/progressive-disclosure-context-retrieval]]
- [[concepts/self-evolving-agent-system]]
- [[concepts/verification-sweep]]
- [[concepts/rule-promotion-ladder]]

## 矛盾 / 细节

- 持久记忆不等于已整理知识。它改善连续性，但稳定结论仍需要综合、来源追踪和矛盾处理。
- 如果缺少明确的检索和保留策略，更多记忆也可能意味着更多过时或敏感上下文。
