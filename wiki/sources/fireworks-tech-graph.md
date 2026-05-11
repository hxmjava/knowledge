---
title: fireworks-tech-graph ：把技术架构图生成这件事做成一个可复用 Skill
type: source
status: active
updated: 2026-05-09
source_count: 1
---

# Source: fireworks-tech-graph ：把技术架构图生成这件事做成一个可复用 Skill

## Metadata

- Raw file: `raw/sources/fireworks-tech-graph.md`
- Author: AI技术小林（微信公众号）
- Date: 2026-04-16
- URL: https://mp.weixin.qq.com/s/p0pdjMlvysLdpa8Nosiccg
- Publisher: 微信公众号「AI技术小林」
- GitHub: https://github.com/yizhiyanhua-ai/fireworks-tech-graph
- License: MIT

## Summary

- fireworks-tech-graph 是一个 Claude Code Skill，将自然语言描述直接转成可发布的 SVG + PNG 技术图。
- 支持 14 种图类型（架构图、时序图、UML、ER 图、Agent 图等）和 7 种视觉风格（极简、极客、蓝图、玻璃态、Claude/OpenAI 官方风格等）。
- 架构分为五层：输入描述→图类型识别→风格系统→语义表达→输出与验证，不是简单模板替换而是带领域理解的生成。
- 语义表达层赋予不同节点形状、箭头样式以表达读写/异步/循环等关系，提升技术图的阅读效率。
- 输出工具链完整：SVG 生成→语法校验→rsvg-convert 导出 PNG，适合批量生产场景。
- 通过 `npx skills add yizhiyanhua-ai/fireworks-tech-graph` 一键安装，依赖 rsvg-convert 和 Node.js。

## Key Claims

- 技术图的价值不只在"好看"，而在读者一眼能看懂组件、数据流、控制流和外部依赖的语义关系。
- 对 AI/Agent 领域有天然偏向：Agent 架构图、Memory 架构图、RAG 流程图等不是从零拼凑，而是带着领域结构理解生成。
- 与 Mermaid 的差异：Mermaid 适合快速表达但视觉效果和复杂结构承载能力有限；与 draw.io 的差异：手工拖拽成本高，不适合频繁改稿。
- 将"描述系统→生成图"标准化为 Skill 能力，从一次性手工劳动变为可沉淀、复用、批量生成的工程化流程。

## Evidence Notes

- 仓库支持的图类型覆盖：架构图、数据流图、流程图、Agent 架构图、Memory 架构图、时序图、对比矩阵、时间线、思维导图、各类 UML 图、ER 图。
- 7 种视觉风格：扁平图标风、暗黑极客风、工程蓝图风、Notion 极简风、玻璃态卡片风、Claude 官方风格、OpenAI 官方风格。
- 语义设计：不同节点形状、箭头颜色/虚线样式表达读写/异步/循环、AI/Agent 组件形状词汇、产品图标与品牌色体系。
- 输出脚本：生成图、从模板生成起始 SVG、校验 SVG 语法、批量测试不同风格。

## Contradictions / Tensions

- 与 [[sources/ai-template2-scaffold]] 中的 Skill 生态形成对比：脚手架项目的 Skill 侧重代码质量检查（ORM checker、API checker），fireworks-tech-graph 侧重非代码产出（技术图），展示了 Skill 生态的扩展边界。
- 文章未提及生成质量的定量评估（如与人工绘图的对比），核心论点建立在定性描述上。

## Linked Entities

- [[entities/fireworks-tech-graph]]
- [[entities/claude-code]]

## Linked Concepts

- [[concepts/specialized-agent-pattern]]
- [[concepts/diagram-generation-as-skill]]

## Follow-up Questions

- fireworks-tech-graph 的图类型识别准确率如何？是否支持混合类型（如同时包含时序和架构的图）？
- 在大型系统（20+ 组件）中，SVG 布局质量是否能保持可用？
- 与其他 Claude Code 图表类 Skill（如 mermaid-generation）相比，优势和劣势分别是什么？
- rsvg-convert 的跨平台兼容性如何？Windows 用户是否有替代方案？
