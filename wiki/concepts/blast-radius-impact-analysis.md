---
title: Blast Radius / Impact Analysis
type: concept
status: active
updated: 2026-05-11
source_count: 1
---

# Concept: Blast Radius / Impact Analysis（影响面分析）

## Definition

从代码变更点出发，沿调用关系、导入关系和测试覆盖关系逐层向外扩散，系统化识别所有可能受影响的文件、函数和测试。目标是让 AI 在评审时优先读取这些"波及区域"，而不是盲目扫描整个仓库。

术语 "blast radius"（爆炸半径）源自工程语境，中文更适合称为"影响面分析"。

## Why It Matters

传统的代码评审依赖开发者的经验来判断"这次改动会影响哪里"。在大型仓库中，这个问题很容易被低估——一个函数的修改可能通过多层调用链影响到看起来不相关的模块。影响面分析将这个判断从人脑记忆转移到结构化查询，确保不遗漏。

## Core Components

影响面分析的扩散维度：

| 维度 | 说明 |
|------|------|
| 直接调用 | 变更函数的调用者（函数、路由、入口点） |
| 间接依赖 | 依赖变更模块的更远层模块 |
| 测试覆盖 | 覆盖变更代码的测试用例 |
| 导入/继承链 | 因导入、继承、调用链而可能被波及的文件 |

### 查询方式

典型查询（通过 MCP 暴露给 AI）：

- "这次变更影响哪些函数和文件？"
- "哪些测试可能需要补？"
- "某个符号在哪里被调用？"
- "这个模块周围有哪些高风险依赖？"

### 准确率特征

- **recall 100%**：不漏检——真正受影响的文件一定会被报告
- **precision 0.38**：会"多报"——部分命中文件可能实际无影响
- **F1 0.54**：在"不漏"和"不多报"之间的平衡点偏向安全侧

> 这种取舍对代码评审是合理的——漏检一个问题的代价远高于多读几个无关文件。

## 与全文搜索的差异

| 维度 | 全文搜索 | 影响面分析 |
|------|----------|-----------|
| 匹配方式 | 关键词/正则 | 结构关系（调用、导入、继承） |
| 关心什么 | 文本是否出现 | 代码之间是否有依赖 |
| 结果质量 | 命中但无关系的噪声多 | 命中即有结构关联 |
| 适用场景 | 符号定位、历史搜索 | 变更影响评估、评审范围划定 |

## 实例

- [[entities/code-review-graph]] 使用 BFS 遍历在 SQLite 图谱上执行影响面分析，通过 MCP 向 AI 助手暴露查询结果

## 与其他概念的关系

- [[concepts/code-structure-graph-for-ai]] — 影响面分析是结构图谱的核心查询场景
- [[concepts/context-and-cost-optimization]] — 精准影响面 = 最小评审集 = 最少 token
- [[concepts/verification-before-completion]] — 影响面分析可以为验证提供"应该测试什么"的结构化依据

## Supporting Sources

- [[sources/code-review-graph]]

## Related Pages

- [[entities/code-review-graph]]
- [[concepts/code-structure-graph-for-ai]]
