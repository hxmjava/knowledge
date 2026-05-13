---
title: Code Review Graph：给 AI 代码评审装一张本地图谱
type: source
status: active
updated: 2026-05-11
source_count: 0
known_urls:
  - https://mp.weixin.qq.com/s/-AzJNiWtO5G_Lbv8xl4BVQ
---

# Source: Code Review Graph：给 AI 代码评审装一张本地图谱

## 来源信息

| 字段 | 值 |
|------|-----|
| 来源 | 微信公众号「AI作弊码」 |
| 日期 | 2026-05-05 |
| 原始链接 | [微信文章](https://mp.weixin.qq.com/s/-AzJNiWtO5G_Lbv8xl4BVQ) |
| 归档路径 | `raw/sources/code-review-graph-weixin.md` |
| 图片目录 | `raw/assets/code-review-graph-*.png` |

## 核心主张

`code-review-graph` 用 Tree-sitter 解析代码结构，将函数、类、调用、导入和测试关系存成本地 SQLite 图谱，再通过 MCP 让 AI 助手查询影响面。评审时 AI 先查图再读代码，减少无关上下文的 token 消耗。

## 关键数据

| 指标 | 数值 | 备注 |
|------|------|------|
| 平均 token 节省 | 8.2× | 6 仓库 13 commits，相比全量读法 |
| 小型单文件变更（express） | 0.7× | 图谱有固定开销，小改动不如直接读文件 |
| 影响面 recall | 100% | 倾向多报，不漏 |
| 影响面 F1 | 0.54 | precision 0.38 |
| 支持语言数 | 23 种 + Jupyter/Databricks | Python, TypeScript, Go, Rust, Java, C/C++, Swift, Kotlin, Svelte 等 |
| 增量索引速度（2,900 文件） | < 2 秒 | 基于 SHA-256 校验 |
| 包版本 | 2.3.2 | MIT License, Python 3.10+ |
| GitHub Stars | ~15.3k | 截至归档日期 |

## 文章结构摘要

1. **为什么 AI 评审会浪费上下文**：无关文件注入导致 token 浪费和判断稀释
2. **代码先变成图**：Tree-sitter → AST → SQLite 图谱，核心概念解读
3. **只读可能被波及的部分**：blast-radius analysis（影响面分析），沿调用/导入/测试关系扩散
4. **把图查询交给 AI 助手**：通过 MCP 暴露查询能力，Claude Code/Cursor/Windsurf/Zed/Codex 等工具可调用
5. **很省 Token，但不是银弹**：8.2× 节省是平均值，小项目开销可能更高
6. **本地、增量、多语言**：`.code-review-graph/` 本地存储、SHA-256 增量更新、23 种语言
7. **快速上手**：`pip install → install → build` 三步
8. **适合谁，不适合谁**：适合大仓库/跨文件 PR/本地隐私优先；不适合小项目偶尔使用

## 连接到 wiki 知识图谱

本文引入的核心概念：
- [[concepts/code-structure-graph-for-ai]] — 用代码结构图谱替代全文喂入，给 AI 提供精准上下文
- [[concepts/blast-radius-impact-analysis]] — 从变更点沿调用链扩散的影响面分析
- [[concepts/context-and-cost-optimization]] — 通过图谱裁剪实现 token 节省（8.2× 平均）
- [[entities/code-review-graph]] — 工具实体
- [[entities/ai-cheatcode]] — 发布平台实体

相关现有 wiki 页面：
- [[entities/claude-code]] — MCP 接入的 AI 助手之一
- [[concepts/map-not-manual]] — 图谱充当"代码地图"，与 AGENTS.md "地图而非手册"理念共享结构化上下文思维
- [[sources/fireworks-tech-graph]] — 同为 Claude Code Skill 生态的领域特化工具（对比：技术图生成 vs 代码结构图查询）

## 与其他来源的张力

- **与 [fireworks-tech-graph](fireworks-tech-graph) 的定位差异**：fireworks-tech-graph 是 Skill 层的非代码产出工具，code-review-graph 是 MCP 层的代码上下文基础设施——两者在 Skill 生态中占据不同位置。
- **token 节省数据的适用边界**：8.2× 平均值来自 6 个仓库的有限样本；express 反例（0.7×）说明小型项目不适用，但文章未披露仓库规模与节省比的相关性曲线。

## 开放问题

- Tree-sitter 解析失败时的降级策略是什么？未解析的文件如何处理？
- 图谱文件大小与仓库规模的关系——大型 monorepo 的 `.code-review-graph/` 目录可能有多大？
- 是否支持自定义关系类型（如数据流、依赖注入）？
- MCP 工具的查询延迟——大型图谱的 BFS 遍历速度如何？
- 与 GitNexus（文章中提到的关联项目）在能力上有什么区别？
