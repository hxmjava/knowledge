---
name: TDD as Hard Gate
description: Treating test-driven development as a non-negotiable gate for all production code changes, with explicit exception procedures rather than silent bypass.
type: concept
status: draft
updated: 2026-04-24
source_count: 1
---

# Concept: TDD as Hard Gate

## Definition

在 AI 辅助开发中，把 TDD（Red-Green-Refactor）从「建议」升级为「硬门禁」：所有生产代码变更必须由失败测试驱动，不允许一次性批量生成生产代码再补测试。

## Why It Matters

AI 编码速度快，容易一次性生成大量代码后再补测试——此时测试往往只是走过场，无法真正捕捉缺陷。硬门禁强制小步推进，每个子任务都有可验证的通过证据。

## Core Rules

1. **RED** — 针对当前子任务写最小失败测试，运行确认因功能缺失而失败
2. **GREEN** — 写最少生产代码使测试通过，不扩写多余逻辑
3. **REFACTOR** — 全绿状态整理代码，再次确认全绿
4. 下一子任务重复循环，严禁批量生成后补测

## Exception Procedure

允许豁免的场景：纯配置变更、一次性脚本、生成代码、无法搭建测试基建的历史模块。但必须：
- 显式征得用户确认
- 在完成输出的 Residual risk 中注明豁免范围与原因

## Test Bootstrap

当模块无测试基建时，自动切换到 test-bootstrap 技能：
- 搭最小测试目录和依赖
- 验证测试命令能跑通
- 交付后通知调用方进入 RED 步骤

## Supporting Sources

- [[sources/ai-template2-scaffold]]

## Related Pages

- [[entities/superpowers]]
- [[entities/harness]]
- [[concepts/spec-driven-workflow-and-review-discipline]]

## Contradictions / Nuance

- 硬门禁增加初期开发时间，对快速原型或一次性脚本可能过度。
- 模块无测试基建时，bootstrap 本身也是额外工作量——但这是技术债暴露而非额外成本。
