---
title: AI 编程进阶：OpenSpec + Superpowers 组合方案深度使用教程
type: source
status: active
updated: 2026-04-25
source_count: 1
---

# Source: AI 编程进阶：OpenSpec + Superpowers 组合方案深度使用教程

## Metadata

- Author: 前端AI行走
- Published: 2026-04-24
- Format: WeChat article

## Summary

- 文章把 `OpenSpec + Superpowers` 定义为一套“规格对齐 + 执行闸门”的组合方案：前者回答“做什么、做到什么程度算完成”，后者回答“如何稳定推进并守住质量”。
- 相比更偏方法论概览的 [[sources/openspec-superpowers-practice-guide]]，这篇更强调“可直接照做”的落地感：给出痛点对照表、`/opsx:ff → verify + archive` 端到端路径、购物车案例，以及失败路径修复手册。
- 文中反复强调目标不是“更酷的 AI 编程”，而是把开发从“凭感觉推进”拉回到可追溯、可验证、可复用的工程流水线。

## Key Claims

- OpenSpec 解决需求不清、完成标准不明和变更追踪不足；Superpowers 解决执行节奏、质量闸门、Git Worktree 隔离与 TDD 约束。
- 组合方案的价值在于“双重保障”：规格先固定方向，执行层再通过 planning、review、test 把偏航和返工压低。
- 对初次落地者，`/opsx:ff` 被包装成低门槛入口：一次性生成规划类 artifacts，再沿 `apply`、`verify`、`archive` 收口。
- 真正有用的不是“技能越多越好”，而是按需加载核心技能，围绕当前项目形成最小可维护组合。

## Practical Workflow Notes

- 文中给出一条清晰的组合链路：`/opsx:ff` 生成提案与任务骨架 → Superpowers 启动 planning / Git Worktree / TDD → 子任务实现与审查 → `verify` → `archive`。
- 购物车案例把“规格到执行”拆成可观测步骤，并要求在 `verify` 前检查幂等、并发、异常降级和至少一个边界用例。
- 对购物车一类状态性功能，作者特别点名三类常见坑：
  1. 数量边界：`quantity <= 0` 时删除还是报错
  2. 价格一致性：是否在购物车中固化价格，还是结算时以商品服务为准
  3. 过期策略：TTL 多久、访问是否续期
- 文末提供快速上手顺序：安装 OpenSpec、安装 Superpowers、初始化测试项目、先跑一个最小变更。

## Contradictions / Tensions

- 本文把 `/opsx:ff`、`verify` 描述成顺手可用的路径，但 [[sources/openspec-superpowers-practice-guide]] 提醒某些命令可能依赖 profile 或版本；这提示“教程路径”与“默认安装体验”之间可能存在版本差异。
- 文章鼓励“按需加载技能”，但同时给出较完整的组合打法；团队实践中仍需定义何时采用全链路、何时采用最小链路。
- 购物车案例强调“先规格后实现”，但实际执行仍需要对边界、价格口径、TTL 等业务细节做人类判断，不能把模板当成自动答案。

## Linked Entities

- [[entities/openspec]]
- [[entities/superpowers]]
- [[entities/claude-code]]

## Linked Concepts

- [[concepts/spec-driven-workflow-and-review-discipline]]
- [[concepts/tdd-as-hard-gate]]
- [[concepts/team-governance-for-ai-coding]]

## Follow-up Questions

- `OpenSpec` 当前版本下，`/opsx:ff`、`verify` 的可用性是否依赖额外 profile、插件或脚手架封装？
- 如果只挑 3-5 个核心技能进入团队默认栈，最小集合应该是什么？
- 购物车案例中的“价格一致性”和“TTL 策略”是否值得抽象为通用 DoD 模板？
