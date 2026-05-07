---
title: "Superpowers 工作流拆解"
type: source
status: active
updated: 2026-05-07
source_count: 1
---

# Source: Superpowers 工作流拆解

## Metadata

- Raw file: `raw/sources/superpowers-workflow-deconstruction.md`
- Author: 地瓜老爸
- Date: 2026-03-27
- URL: https://mp.weixin.qq.com/s/Fko48oWrAgOL4KcOrQ9sPg
- Publisher: 微信公众号

## Summary

- 将 Superpowers 的 14 个 skill 解析为四层架构：总入口/流程控制、实施执行/环境隔离、质量保障/问题处理、收尾/元能力。
- 提炼出两条主链路：功能开发链（brainstorming → plan → worktree → execute → finish）和调试链（systematic-debugging → TDD → verification）。
- 核心论点：Superpowers 真正的价值不是"多装了 14 个 skill"，而是把 Claude Code 从问答模型约束为守流程的工程协作者。
- 强调三条底线工程习惯：设计批准前不准实现、根因查清前不准修复、新鲜验证结果出来前不准宣称完成。

## Key Claims

- Superpowers 的 14 个 skill 不是平铺工具，而是四层分工的工程系统。
- **功能开发链路**：`using-superpowers → brainstorming → writing-plans → worktrees → executing → finishing`，强调"先定义问题，再设计方案，再拆计划，再执行，再交付"的严格顺序。
- **调试链路**：`using-superpowers → systematic-debugging → TDD → verification-before-completion`，用强制门禁对抗 AI "猜一个改一个"的低效路径。
- AI 最容易犯的错不是"不会写"，而是"在还没理解对的时候已经开始写了"——brainstorming 的价值在于硬性拦截这个行为。
- 最该默认启用的底线规则是 **verification-before-completion**：没有新鲜验证结果，不要宣称完成。错误的完成声明比 bug 本身更伤协作体验。
- 真正的工程闭环不是"写完"，而是"审过、验过、合并、保留、清理"的完整交付。

## Evidence Notes

- 文章通过逐条拆解 14 个 skill 并归类为四层，提供了具体的分类依据。
- 两条主链路的提炼基于 skill 之间的逻辑依赖关系，而非简单罗列。
- 文章以 AI 编程中"猜→改→试→再猜"的典型低效路径作为反面论据，支撑 systematic-debugging 的价值。
- verification-before-completion 被作者评为"最该默认启用的底线规则"——这是一个强主张，与其他来源的 TDD 硬门禁视角形成互补。

## Contradictions / Tensions

- 文章将 verification-before-completion 定位为"最该默认启用"的规则，而 [[sources/ai-template2-scaffold]] 更强调 TDD 作为硬门禁。两者并非矛盾，但优先级排序不同——本文更偏"完成纪律"，脚手架更偏"开发纪律"。
- 文章未涉及 Superpowers 的安装、配置或实际部署细节，与之前来源的实操视角形成互补而非替代。

## Linked Entities

- [[entities/superpowers]]
- [[entities/claude-code]]

## Linked Concepts

- [[concepts/spec-driven-workflow-and-review-discipline]]
- [[concepts/tdd-as-hard-gate]]
- [[concepts/verification-before-completion]]
- [[concepts/specialized-agent-pattern]]

## Follow-up Questions

- 14 个 skill 是否全部默认安装，还是按需加载？文章对此未做说明。
- 四层架构是否可以映射到具体项目配置（如 harness 命令分层）？
- "两条主链路"在实际使用中是否有混合场景（如功能开发中发现 bug 需要切换到调试链路）？切换机制是什么？
