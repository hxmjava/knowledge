---
title: fireworks-tech-graph
type: entity
status: active
updated: 2026-05-09
source_count: 1
---

# Entity: fireworks-tech-graph

## What It Is

fireworks-tech-graph 是一个面向技术文档和 AI/Agent 场景的 Claude Code Skill，能将自然语言描述直接转成可发布的 SVG + PNG 技术图。支持 14 种图类型和 7 种视觉风格，覆盖架构图、流程图、时序图、UML、ER 图等常见需求。

## Relevance

该实体展示了 Claude Code Skill 生态向非代码产出领域扩展的案例。它与 [[entities/superpowers]] 的"专项技能"理念一致——用领域特化的 Skill 处理特定任务，而不是依赖通用能力。

## Key Facts

- **仓库**: https://github.com/yizhiyanhua-ai/fireworks-tech-graph
- **License**: MIT
- **安装方式**: `npx skills add yizhiyanhua-ai/fireworks-tech-graph`
- **依赖**: rsvg-convert、Node.js、本地脚本工具链
- **核心能力**: 自然语言 → SVG 技术图 → PNG 导出
- **图类型**: 14 种（架构图、数据流图、流程图、Agent 架构图、Memory 架构图、时序图、对比矩阵、时间线、思维导图、UML 图、ER 图等）
- **视觉风格**: 7 种（扁平图标、暗黑极客、工程蓝图、Notion 极简、玻璃态卡片、Claude 官方、OpenAI 官方）
- **五层架构**: 输入描述→图类型识别→风格系统→语义表达→输出与验证

## Relationships

- **所属平台**: [[entities/claude-code]]（作为 Claude Code Skill 运行）
- **设计理念对齐**: [[entities/superpowers]]（专项技能分工模式）
- **相关概念**: [[concepts/specialized-agent-pattern]]（领域特化 Skill）、[[concepts/diagram-generation-as-skill]]（声明式图生成）
- **对比对象**: Mermaid（快速表达但视觉受限）、draw.io（强大但手工成本高）

## Evidence

- [[sources/fireworks-tech-graph]]

## Open Questions

- 图类型识别的准确率与混合类型支持情况。
- 大型系统（20+ 组件）的 SVG 布局质量。
- Windows 环境下 rsvg-convert 的替代方案。
- 与其他图表类 Claude Code Skill 的差异化定位。
