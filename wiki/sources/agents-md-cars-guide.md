---
title: AGENTS.md C.A.R.S 实践指南
type: source
status: active
updated: 2026-05-12
source_count: 1
---

# Source: 如何构建一个好的 AGENTS.md：AI 编码 Agent 的项目级行为规范最佳实践

## Metadata

- Raw file: `raw/sources/agents-md-cars-guide.md`
- Author: 米奥
- Date: 2026-05-09
- URL: https://mp.weixin.qq.com/s/RxRCmsc3ehIuqV_DwG-Kog
- Publisher: 肥喵学AI（微信公众号）

## Summary

- 提出 **C.A.R.S 结构**组织 AGENTS.md：Commands（开发命令）、Architecture（架构与目录）、Restrictions（约束与禁忌）、Standards（流程规范），强调 Commands 和 Restrictions 优先编写。
- 核心观点：AGENTS.md 是 AI 的**项目级行为约束文件**，本质是"团队共识固化"而非提示词集合；明确写死命令（如"只用 pnpm"）可杜绝 90% 以上包管理器错误。
- **跨工具兼容策略**：以 AGENTS.md 为单一事实来源，Claude Code 通过 `ln -s AGENTS.md CLAUDE.md` 符号链接接入，Cursor 配合 `.cursor/rules/*.mdc` 细粒度规则。
- **大项目索引模式**：AGENTS.md 超过 300 行时切换为"目录索引"（100-120 行概览+指针），详细内容下放到 `docs/` 子目录（adr/、conventions/、workflows/、patterns/、gotchas.md）。
- 行数建议：小项目单文件 30-40 行即覆盖 90% 场景，中大型项目 200-400 行，超 300 行应拆分为索引+子文档。
- 提供一份可直接复用的 30-40 行紧凑模板（改编自 Benjamin Crozat 实战仓库）。

## Key Claims

- AGENTS.md 的本质是 AI 的项目级行为约束文件，而非一次性提示词集合——把"我个人觉得这样写比较好"变成"团队约定必须这么做"。
- Restrictions（不能做什么）是整个 AGENTS.md 中最有价值的部分——"不能做什么"比"应该做什么"更能防止大问题。
- Commands 部分应写死具体命令而非泛泛指示——AI 默认喜欢用 npm，尤其是新模型，明确写死后低级错误会少非常多。
- 技术栈应精确到补丁版本——写"Next.js 15.3 + TypeScript 5.7"而非"Next.js + TypeScript"。
- AGENTS.md 超过 300 行时 AI 开始"挑着读"或忽略，应切换为索引模式。

## Evidence Notes

- 作者结合 Benjamin Crozat（《How to use AGENTS.md with Codex, Cursor, and Claude Code》）、Eric 技术圈（《一套可落地的企业级 AGENTS.md 项目规则实践》）和 Cursor 官方文档的经验整理。
- 引用 OpenAI Harness 团队和 Sagar Mandal 的大型项目索引实践。
- 跨工具兼容矩阵基于 2026 年 5 月最新工具支持情况。
- 30-40 行模板声称覆盖"日常 90% 以上的 Agent 交互场景"——未提供量化验证。

## Contradictions / Tensions

- 行数建议存在内在张力：文章同时建议"200-400 行"（第 6 节）和"100-120 行"（第 8 节索引模式的 AGENTS.md 上限）。两者适用场景不同（单文件 vs 索引），但文章未明确切换阈值。
- 与 [[sources/agents-md-guide]] 对比：Kirito 的"地图，而非手册"建议约 200 行，本文建议 200-400 行——差异可能来自项目类型和技术栈复杂度不同。
- 与 [[sources/claude-md-error-rate-reduction]] 对比：Mnimiy 的三层文件结构中根文件建议 80-120 行，本文索引模式下 AGENTS.md 也是 100-120 行——两者在此达成共识；但本文的 C.A.R.S 全量模式允许 200-400 行，比前两者宽松。
- "200-400 行过长会导致 AI 遵守率下降"这一说法缺乏引用——遵守率下降的阈值和度量标准未说明。

## Linked Entities

- [[entities/agents-md]]
- [[entities/claude-code]]
- [[entities/miao]]
- [[entities/fatcat-learn-ai]]

## Linked Concepts

- [[concepts/cars-agents-structure]]
- [[concepts/map-not-manual]]
- [[concepts/bad-case-driven-iteration]]
- [[concepts/cross-tool-agents-compatibility]]
- [[concepts/context-and-cost-optimization]]

## Follow-up Questions

- C.A.R.S 结构在非 Web 项目（如移动端、数据工程、ML pipeline）中的适用性？
- "30-40 行覆盖 90% 场景"的验证方法和场景分布？
- 跨工具兼容矩阵中各工具对 AGENTS.md 的解析深度和注入方式差异？
- Benjamin Crozat 和 Eric 技术圈的原始文章是否值得作为独立来源深度录入？
- 索引模式下 `docs/` 子目录的粒度——adr/、conventions/、workflows/ 三者之间的边界案例？
