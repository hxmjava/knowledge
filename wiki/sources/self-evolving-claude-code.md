---
title: 如何把 Claude Code 改造成一个自进化系统：完整指南
type: source
status: active
updated: 2026-05-13
source_count: 1
---

# Source: 如何把 Claude Code 改造成一个自进化系统：完整指南

## Metadata

- Raw file: `raw/sources/self-evolving-claude-code.md`
- Author: 一天天的（Meta Alchemist）
- Date: 未标注（公众号文章）
- URL / Publisher: 微信公众号「工程师耍杂技」 / [原文](https://mp.weixin.qq.com/s/SheSKVGfJIvS6VNMik4Ogw)

## Summary

- 将 Claude Code 从开箱即用的 CLI 改造为**四层自进化系统**：认知核心（CLAUDE.md）、专用子智能体（architect/reviewer）、路径作用域规则（rules/）、进化引擎（memory/ + evolution skill）。
- 提出 **"行为编程"** 概念：CLAUDE.md 不是文档而是行为塑造——直接编程 Claude 的思维方式，包含决策框架（先 grep、评估影响范围、最小改动、验证计划）和完成标准（typecheck/lint/test 五项全过）。
- 进化引擎的核心是**免疫系统**而非日记本：每条规则附带 `verify:` 机器可检查行，会话启动时自动执行验证扫描，违规则记录到 `violations.jsonl`；好的免疫系统是无形的——全通过时静默。
- **纠正自动晋升机制**：第 1 次纠正记录到 `corrections.jsonl`，第 2 次相同模式自动晋升到 `learned-rules.md`（附 verify 行）；10+ 会话持续通过则晋升为永久配置（CLAUDE.md 或 rules/）。
- **路径作用域规则**：安全规则只在编辑认证代码时加载、API 设计规则只在 handlers 目录激活、性能规则全局监控 N+1 查询——上下文保持精简。
- 用三个 hooks（SessionStart/PreToolUse/Stop）将进化系统从"指令说要做"升级为"结构性地让你很难跳过"——让一切变成结构性的而非依赖 Claude 的自觉性。
- 提出 **CLAUDE.md 控制在 150 行以内**（超过指令遵从度下降），领域特定规则移到 `.claude/rules/`。
- `learned-rules.md` 设计上限 50 行，强制要么晋升（到 CLAUDE.md/rules/）要么淘汰——规则不会无限膨胀。
- 首要原则："**没有验证检查的规则是愿望，有验证检查的规则才是护栏。只有护栏才能存活。**"

## Key Claims

1. CLAUDE.md 是"行为编程"——每一行都直接加载到系统提示词中塑造 Claude 的思维方式，不只是列出命令。
2. 决策框架应在写代码前运行：先 grep 查找现有模式 → 评估影响范围 → 不确定就问一个澄清问题 → 最小改动 → 验证计划。
3. 子智能体（architect/reviewer）在隔离上下文窗口启动，使用不同工具权限和模型，执行专注任务后汇报。
4. 路径作用域规则让上下文保持精简——编辑 CSS 时 Claude 不会去读 200 行安全规范。
5. 进化引擎用免疫系统比喻：验证扫描静默运行，只在违规时浮出水面；session scoring 追踪纠正趋势判断系统是否真在改进。
6. CLAUDE.md 150 行以内、learned-rules.md 50 行以内——强制晋升或淘汰，防止规则膨胀。
7. hooks 结构化执行：SessionStart 注入"读 learned-rules 并运行验证扫描"，PreToolUse 提醒"检查该文件的路径规则"，Stop 提醒"记录纠正和观察"。
8. observations 必须立即验证后才记录——"Never log a guess. Verify it immediately or don't log it"。confirmed + 0 反例 → 直接晋升 learned-rules.md。
9. 与 Claude Code 内置 `/memory` 的区别：自动记忆是便签本，本系统增加了验证检查、晋升阶梯和会话评分。

## Evidence Notes

- 文章提供完整的可复制文件：CLAUDE.md（约 100 行）、settings.json（权限 + hooks）、4 个 rules 文件、2 个 agents 文件、3 个 commands、1 个 evolution skill、memory 目录结构。
- 所有规则要求附带 `verify:` 行——模式为 `Grep("[pattern]", path="[scope]") → N matches`。
- `sessions.jsonl` 支持趋势检测：5+ 条目后检查纠正是否递减、规则是否通过率稳定。
- 验证模式：代码模式禁止 → grep 0 匹配；代码模式要求 → grep 1+ 匹配；文件必须存在/不存在 → glob 匹配。
- 未提供量化性能数据（如纠正下降的具体百分比）。
- 适用任意技术栈：替换 npm 为 pytest/go test/cargo test，调整目录结构和编码约定即可。

## Contradictions / Tensions

- **150 行 vs 200 行**：本文建议 CLAUDE.md 控制在 150 行（"超过 150 行指令遵从度下降"），而 [[sources/claude-md-error-rate-reduction]] 和 [[sources/agents-md-cars-guide]] 建议 200 行、根文件 80-120 行——差异可能来自是否把 Commands/Architecture 算入。
- **"行为编程" vs "行为契约"**：本文用"行为编程"（编程 Claude 的思维方式），既有 wiki 用"行为契约"（仓库级跨会话约定）——前者强调塑造认知，后者强调约束行为，视角不同但目标一致。
- **自动晋升 vs Bad Case 驱动**：进化引擎的自动晋升（2 次纠正 → 永久规则）比 [[concepts/bad-case-driven-iteration]] 的人工判断更激进——可能产生误晋升风险。
- **hooks 作为结构性执行 vs hooks 作为安全提醒**：本文将 hooks 定位为"让一切变成结构性的"（核心执行机制），既有 wiki 定位为"轻量安全提醒"（fail-open）——本文用法更强硬。
- **免疫系统比喻的隐含假设**：系统假设 grep 验证足够覆盖规则合规性——对于行为类规则（如"不要顺手重构"）机器可检查性有限。

## Linked Entities

- [[entities/meta-alchemist]]
- [[entities/engineer-juggling]]
- [[entities/claude-code]]

## Linked Concepts

- [[concepts/self-evolving-agent-system]]
- [[concepts/verification-sweep]]
- [[concepts/rule-promotion-ladder]]
- [[concepts/persistent-agent-memory]]
- [[concepts/behavioral-contract-vs-prompt]]
- [[concepts/hooks-as-safety-net]]
- [[concepts/verification-before-completion]]
- [[concepts/context-and-cost-optimization]]
- [[concepts/specialized-agent-pattern]]
- [[concepts/bad-case-driven-iteration]]

## Follow-up Questions

- 150 行 CLAUDE.md 限制的实验数据来源——不同模型版本的指令遵从度是否一致？
- 自动晋升机制（2 次纠正 → 永久规则）在实践中误晋升率如何？是否有回滚机制？
- `verify: manual` 规则（无法自动检查的规则）在 evolved-rules 中的占比——这类规则的执行靠什么保证？
- 验证扫描的性能开销——规则数量增长到 50 条上限时，会话启动延迟是否可接受？
- 路径作用域规则与 CLAUDE.md 分层配置（全局/项目/子目录）的重叠和分工。
- 进化系统与 Superpowers 的 skill 系统能否共存——两套 hooks 是否冲突？
