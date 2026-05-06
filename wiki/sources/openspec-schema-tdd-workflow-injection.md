---
title: 用 OpenSpec Schema 把 Superpowers TDD 焊进编码工作流（实测一半有效）
type: source
status: active
updated: 2026-05-06
source_count: 1
---

# Source: 用 OpenSpec Schema 把 Superpowers TDD 焊进编码工作流（实测一半有效）

## Metadata

- Raw file: `raw/sources/用OpenSpec Schema注入TDD到编码工作流.md`
- 来源：微信公众号「术哥无界」
- 链接：https://mp.weixin.qq.com/s/4dS5rNlsodv1iPCsrlr8bQ
- 发布日期：2026-05-05
- 实测模型：MiniMax 2.7
- Scope: OpenSpec 自定义 schema 机制、TDD 工作流注入、instruction 约束力边界

## Summary

- 本文是一篇**实测验证**文章：用 OpenSpec 的自定义 schema 机制，在每个 artifact 生成阶段嵌入 TDD 纪律，然后完整跑一遍 propose + apply 流程，观察 AI 是否真的按 TDD 循环写代码。
- **结论**：方案在**规划阶段（propose）有效**——自定义 schema 通过 `instruction` 字段确实改变了 AI 产出 specs、tasks、plans 的内容和格式；但在**执行阶段（apply）无效**——instruction 是文本提示而非硬约束，AI 不会严格遵守 RED-GREEN-REFACTOR 循环。
- 核心机制是**三个注入点 + 四层叠加**：`instruction`（schema.yaml，单个 artifact）、`rules`（config.yaml，匹配 id 的 artifact）、`context`（config.yaml，所有 artifact），叠加顺序为 context → rules → instruction → template。
- 用 Todo CRUD 应用做完整验证：propose 阶段 specs 用了 WHEN/THEN、tasks 包含测试描述、plans 自动生成了 1098 行详细计划；但 apply 阶段 AI 一次性写完所有源码和测试再跑 `npm test`，没有 RED→GREEN→REFACTOR 循环。
- 这是 `openspec-superpowers-practice-guide.md` 的**专题深入版**，聚焦于"能不能通过 schema 注入 TDD 纪律"这个具体问题。

## Key Claims

- OpenSpec 内置 `spec-driven` schema 只管"写什么文档"，不管"按什么纪律写代码"；自定义 schema 可以在每个 artifact 的 instruction 里嵌入 TDD 指引。
- 三个注入点分工明确：`instruction` 是每个 artifact 的专属指令，`rules` 针对特定 artifact 的附加规则，`context` 是所有 artifact 共享的项目背景；叠加顺序 context → rules → instruction → template，越靠后越具体。
- OpenSpec 的 DAG 依赖是"赋能者"，不是"门控"——`requires: [proposal]` 的意思是 proposal 的内容会作为上下文传入，不是 proposal 不存在就不让跑。
- `plans` artifact 是新增节点（依赖 tasks），用于创建 TDD 微步骤计划，可选依赖 Superpowers 的 `writing-plans` skill 来生成更细粒度的执行计划。
- instruction 是**文本指令**，不是硬约束。AI 的指令遵循能力取决于具体模型（实测 MiniMax 2.7 效果不如 GLM 5.1）。
- 方案的价值在于**改善规划质量**（specs、tasks、plans 的格式和内容），而不是**强制编码行为**（apply 阶段的 TDD 循环）。

## 三个注入点与四层叠加

| 注入点 | 所在文件 | 作用范围 | 注入时机 |
|--------|----------|----------|----------|
| `instruction` | schema.yaml 的每个 artifact | 仅当前 artifact | AI 生成该 artifact 时 |
| `rules` | config.yaml | 匹配 id 的 artifact | AI 生成匹配的 artifact 时 |
| `context` | config.yaml | 所有 artifact | 每次 AI 生成任何 artifact 时 |

**叠加顺序**：context → rules → instruction → template（四层叠加，越靠后越具体）

## 实测结论对比

| 阶段 | 是否生效 | 实测证据 |
|------|----------|----------|
| **Propose（规划阶段）** | ✅ 有效 | specs 用了 WHEN/THEN、tasks 包含测试描述和预期行为、plans 自动调用了 Superpowers 的 `writing-plans` skill 生成 1098 行详细计划 |
| **Apply（执行阶段）** | ❌ TDD 循环未生效 | AI 一次性写完所有源码和测试再跑 `npm test`，没有 RED→GREEN→REFACTOR 循环，git log 中没有交替的 test/feat 提交 |

## 适用场景

- ✅ 想让 AI 写出更规范的 spec 和 tasks：instruction 能显著改善 propose 阶段的产出质量
- ✅ 想给团队统一 artifact 的输出格式：WHEN/THEN、测试描述等格式约束可以稳定注入
- ✅ 想用 OpenSpec 管理复杂项目的变更流程：五个 artifact 的 DAG 治理本身有价值
- ❌ 想强制 AI 按 TDD 严格循环执行代码：instruction 约束不了 apply 阶段的代码编写顺序

## Schema 核心结构

完整的 `schema.yaml` 定义了 5 个 artifact 节点：
1. **proposal** — 初始变更提案，要求用 WHEN/THEN 格式列出可测试行为
2. **specs** — 行为规格，强制 GIVEN/WHEN/THEN 格式
3. **design** — 技术设计，要求标注测试文件和测试策略
4. **tasks** — 实现清单，按 TDD 顺序（写失败测试 → 最小实现 → 重构 → 提交）
5. **plans** — 详细执行计划（新增），拆成 2-5 分钟的 RED-GREEN-REFACTOR 微步骤

apply 阶段的 `requires: [plans]`，确保 plan 就绪后才开始实现。

## 故障排除要点

- **AI 跳过 TDD 步骤**：在 rules 里加更具体的规则（如 `Never create a .ts file without a corresponding .test.ts file`），把 tasks 拆得更细
- **plans 被截断**：在 plans 的 instruction 里加限制（`Maximum 15 micro-tasks per plan`）
- **不想依赖 Superpowers**：删掉 plans instruction 里的 PRECHECK 和 skill 引用，改成纯文本 TDD 指令即可

## Related

- [[openspec-superpowers-practice-guide]] — 上游综述，OpenSpec + Superpowers 的整体工作流与分工
- [[ai-template2-scaffold]] — AI 项目模板脚手架
