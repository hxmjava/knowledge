---
title: 声明式技术图生成
type: concept
status: active
updated: 2026-05-09
source_count: 1
---

# Concept: 声明式技术图生成（Diagram Generation as Skill）

## Definition

将技术图的创建从"手工拖拽"转变为"声明式描述"：用户用自然语言描述系统结构，AI 通过图类型识别、风格选择和语义映射，自动生成可发布的技术图（SVG/PNG）。这是 Claude Code Skill 生态中"领域特化非代码产出"的代表性模式。

## Why It Matters

技术图在架构文档、博客、方案文档中的价值很高，但制作成本也很高。传统工具（draw.io、Visio）需要手工布局；Mermaid 适合快速表达但视觉效果有限。声明式图生成将"描述需求→生成图→嵌入文档"标准化为可复用的 Skill 能力，与 [[concepts/specialized-agent-pattern]] 的理念一致——用领域特化的 Skill 处理特定任务。

## Core Components

- **描述解析层**: 将自然语言输入归类到已有图类型（架构图、时序图、ER 图等），而非简单模板替换。
- **风格系统**: 提供多种预设视觉风格（极简、极客、蓝图、品牌风格等），适应不同输出场景。
- **语义表达映射**: 不同节点形状、箭头样式表达读写/异步/循环等关系，超越"框+箭头"的简单表达。
- **输出工具链**: SVG 生成→语法校验→PNG 导出，形成完整的"技术图生产流水线"。

## Supporting Sources

- [[sources/fireworks-tech-graph]]

## Related Pages

- [[entities/fireworks-tech-graph]]
- [[entities/claude-code]]
- [[concepts/specialized-agent-pattern]]

## Contradictions / Tensions

- 声明式图生成的质量高度依赖底层模型对用户描述的理解能力，对复杂系统（20+ 组件、多层嵌套）的布局质量尚无定量评估。
- 与 Mermaid 等声明式图表语言相比，AI 生成方式的可预测性和可复现性更弱——同一描述可能产出不同结果。
