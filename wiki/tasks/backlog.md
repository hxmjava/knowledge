---
title: Backlog
type: task
status: active
updated: 2026-05-13
---

# Backlog

## 高优先级

- 定义来源页面的首选引用风格。
- 定义自动捕获 agent 记忆的隐私、保留和修剪规则。
- 核实 `OpenSpec` 默认命令集与教程中 `/opsx:ff`、`verify` 的差异，确认哪些属于 profile / 脚手架封装而非官方默认能力。
- 评估 harness-creator 生成质量和覆盖范围：是否需要人工大幅修正，支持哪些技术栈。
- 验证闭环基础设施的最小可行子集定义：哪些脚本/配置是必选项，哪些是增强项。

## 中优先级

- 评估 Superpowers 8 个平台安装方式的实际验证程度，特别关注 Factory Droid 和 GitHub Copilot CLI 的成熟度。
- 评估"合理化防范"机制（Red Flags + Rationalizations 表）是否值得抽象为自定义技能的可复用设计模板。
- 添加周期性 lint 节奏（每周或每 N 次 ingest）。
- 评估简单 grep/index 搜索是否仍然足够。
- 对比 Claude-Mem 式自动记忆与本 vault 的人工整理 wiki 编译流程。

## 中优先级

- 深度对比 SDD（github/spec-kit）与 OpenSpec 的文件结构、工作流和实际差异——判断是否应合并为一个概念页还是保持独立。
- 调研 swingerman/atdd 插件的实际使用体验和社区活跃度，验证变异测试在 AI 生成代码上的效果。
- 调研 DDD 在 AI 编码工具中的集成方式——AI 是否能自动识别和遵守限界上下文？

## 低优先级

- 为重复维护检查添加自动化脚本。
- 调研 AGENTS.md 嵌套模式在大型 monorepo 中的实践（如 OpenAI 88 个嵌套 AGENTS.md）。
- 评估"源码即文档"策略在 AI 上下文窗口有限时的检索效率。
- 评估 2 篇 AGENTS.md 学术论文（arxiv 2602.11988、2601.20404）对 repo-level context file 的定量评估结果，判断是否需要作为独立来源录入。
- 评估「架构师」公众号 20 篇系列前作中哪些与 wiki 主题最相关、值得优先录入（Harness 方法论、长周期 Agent、Claude Skills 入门、配置方案等）。
- 150 行 CLAUDE.md 限制 vs 200 行建议的实验依据——不同模型版本（Sonnet 3.5/4/4.5）的指令遵从度阈值是否有差异？
- 自动晋升机制（2 次纠正 → 永久规则）的误晋升率评估——需要多少样本量才能得出结论？
- 进化系统的验证扫描在 50 条规则上限时的启动延迟——在大型仓库（10k+ 文件）中 grep 执行是否可接受？
- 进化引擎与 Superpowers 的 hooks 系统能否共存——两套 SessionStart/Stop hooks 是否冲突或叠加？
- CLAUDE.md "行为编程"视角与既有"行为契约"视角是否应合并为一个概念页——两者核心区别是什么？
- 「工程师耍杂技」公众号是否有更多与 wiki 主题相关的文章可供录入。
- `verify: manual` 规则（无法自动检查的行为规则）在实际使用中的占比和执行缺口的弥补方案。
