---
title: Backlog
type: task
status: active
updated: 2026-05-07
---

# Backlog

## 高优先级

- 定义来源页面的首选引用风格。
- 定义自动捕获 agent 记忆的隐私、保留和修剪规则。
- 核实 `OpenSpec` 默认命令集与教程中 `/opsx:ff`、`verify` 的差异，确认哪些属于 profile / 脚手架封装而非官方默认能力。
- 评估 harness-creator 生成质量和覆盖范围：是否需要人工大幅修正，支持哪些技术栈。
- 验证闭环基础设施的最小可行子集定义：哪些脚本/配置是必选项，哪些是增强项。

## 中优先级

- 添加周期性 lint 节奏（每周或每 N 次 ingest）。
- 评估简单 grep/index 搜索是否仍然足够。
- 对比 Claude-Mem 式自动记忆与本 vault 的人工整理 wiki 编译流程。

## 低优先级

- 为重复维护检查添加自动化脚本。
- 调研 AGENTS.md 嵌套模式在大型 monorepo 中的实践（如 OpenAI 88 个嵌套 AGENTS.md）。
- 评估"源码即文档"策略在 AI 上下文窗口有限时的检索效率。
