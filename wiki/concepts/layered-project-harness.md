---
name: Layered Project Harness
description: Organizing AI-assisted development around explicit project layers (common/service/app/message) with dedicated agents, skills, and verification policies per layer.
type: concept
status: draft
updated: 2026-04-24
source_count: 1
---

# Concept: Layered Project Harness

## Definition

将项目按职责拆分为明确的层级层（`{{LAYER_COMMON}}` → `{{LAYER_SERVICE}}` → `{{LAYER_APP}}` / `{{LAYER_MESSAGE}}`），每层绑定专用 Agent、适用技能和验证策略。AI 在处理任务时先判断改动落在哪一层，再选择执行路径。

## Why It Matters

多模块项目中，盲目跨层修改是常见错误来源。显式分层让 AI 知道：
- 哪些文件该改、哪些不该碰
- 改动影响哪些下游模块
- 需要执行什么级别的验证
- 哪些改动必须串行（共享层）而非并行

## Core Components

- **分层目录映射**：项目根目录一级模块对应四层之一。
- **层内 Agent**：每层有专用 Claude Code Agent，自带层相关的检查技能。
- **依赖方向约束**：`app → service → common`，`message → service/common`。新增业务域时沿用既有分层模式。
- **验证分级**：单模块改动跑模块测试；common 层/接口/配置变更扩大验证范围。

## Working Rules

- 改动接口签名时，同步评估 api、impl、调用方 app、消息消费者与 XML 配置。
- 改动共享实体 / Mapper / SQL / 共享常量时，评估所有上游依赖模块。
- 不要把领域逻辑塞入 app 层。
- 连续验证失败或跨模块影响过大时，先停下升级讨论。

## Supporting Sources

- [[sources/ai-template2-scaffold]]

## Related Pages

- [[entities/harness]]
- [[concepts/specialized-agent-pattern]]
- [[concepts/tdd-as-hard-gate]]

## Contradictions / Nuance

- 分层越明确，灵活性越低：对非标准架构项目需要重新定义层级映射。
- 并行策略依赖耦合度判断：「无共享表/实体」的判断本身可能需要深入分析。
