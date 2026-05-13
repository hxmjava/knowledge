---
title: Code Structure Graph for AI Context
type: concept
status: active
updated: 2026-05-11
source_count: 1
---

# Concept: Code Structure Graph for AI Context

## Definition

在本地维护一张代码结构图谱（函数、类、导入、调用、测试关系），AI 助手通过查询图谱获取结构化上下文，而不是将整个仓库或大段文件作为上下文喂入模型。

核心公式：**先查图，再读代码**。

## Why It Matters

AI 编程助手在代码评审中面临一个结构性困境：上下文窗口有限，但代码仓库可能很大。将大量无关文件注入上下文不仅浪费 token，还会稀释模型的判断能力。结构图谱通过只提供"模型该读什么"的精确答案，将上下文使用从"全量灌入"转变为"按需检索"。

## Core Mechanism

```
代码仓库
  → Tree-sitter（增量解析器）解析为 AST
    → 提取结构信息（函数、类、导入、调用、测试关系）
      → 存入本地 SQLite 图谱（节点 + 边）
        → AI 助手通过 MCP 查询影响面
          → 只读取真正相关的代码子集
```

### 关键组件

| 组件 | 作用 |
|------|------|
| Tree-sitter | 增量代码解析器，识别多种语言的语法结构 |
| AST | 抽象语法树，将代码从文本转为树状结构 |
| SQLite 图谱 | 本地存储结构信息，节点=函数/类，边=调用/导入/测试关系 |
| BFS 遍历 | 从变更点向外逐层扩散，找到受影响的文件和函数 |
| MCP Server | 将查询能力暴露给 AI 助手，无需 AI 理解图谱实现细节 |

### 效果数据

- 平均 token 节省 8.2×（6 仓库 13 commits）
- 2,900 文件项目增量索引 < 2 秒
- 支持 23 种语言 + Jupyter/Databricks notebook
- 影响面 recall 100%，F1 0.54

### 局限

- 图谱有固定开销（节点、边、提示词模板占 token），小项目/孤立改动可能不如直接读文件
- precision 0.38 表示会"多报"，适合评审（不漏检）但不等于每个命中都有问题
- Tree-sitter 对某些边缘语法的支持可能不完整

## 实例

- [[entities/code-review-graph]]：目前最完整的开源实现，Tree-sitter + SQLite + MCP 全链路

## 与其他概念的关系

- [[concepts/context-and-cost-optimization]] — 结构图谱是上下文优化的一种具体手段，从"少喂文件"升级到"先查结构再决定喂什么"
- [[concepts/map-not-manual]] — 代码图谱充当"代码地图"，与 AGENTS.md 的"地图而非手册"理念共享结构化导航思维
- [[concepts/blast-radius-impact-analysis]] — 影响面分析是图谱的核心查询场景
- [[concepts/persistent-wiki-compilation]] — 两者都是将隐性知识（代码结构/阅读笔记）编译为可查询的结构化存储

## Supporting Sources

- [[sources/code-review-graph]]

## Related Pages

- [[entities/code-review-graph]]
- [[concepts/context-and-cost-optimization]]
- [[concepts/map-not-manual]]
