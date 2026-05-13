---
name: Specialized Agent Pattern
description: Using layer-specific AI agents and domain-specific checker skills instead of a single general-purpose agent for all development tasks.
type: concept
status: draft
updated: 2026-05-13
source_count: 3
---

# Concept: Specialized Agent Pattern

## Definition

在多模块项目中，不为所有任务使用单一通用 Agent，而是根据改动所属层级和检查维度，选择对应的专用 Agent 和专项技能。

## Why It Matters

通用 Agent 容易在跨模块场景中遗漏层特定的风险（如 ORM 一致性、RPC 接线、消息幂等）。专用 Agent 自带层相关的预设知识和检查清单，减少遗漏。

## How It Works

**分层 Agent 路由**：

| 改动落在 | 使用 Agent | 自带技能 |
|---------|-----------|---------|
| app 层（Controller/Web/Job） | proj-app-agent | build-module-verifier, xml-config-checker |
| common 层（实体/Mapper/工具） | proj-common-agent | orm-change-checker, xml-config-checker |
| service 层（接口/实现） | proj-service-agent | api-change-checker, build-module-verifier |
| message 层（MQ 消费） | proj-message-agent | message-consumer-checker |

**专项技能触发条件**：

- 改 `*-api` 目录 → api-change-checker
- 改实体/Mapper/XML → orm-change-checker
- 改 resources/** → xml-config-checker
- 改消息消费模块 → message-consumer-checker
- 询问验证范围 → build-module-verifier
- 模块无测试基建 → test-bootstrap

## Architect / Reviewer 子智能体变体（来自自进化系统）

[[sources/self-evolving-claude-code]] 提出更通用的双角色子智能体模式：

| 角色 | 触发条件 | 模型 | 工具 | 职责 |
|------|---------|------|------|------|
| architect | 3+ 文件变更、新功能（非 bug fix）、需要理解组件交互 | sonnet | Read, Grep, Glob, Bash（只读） | 产出 PLAN/CHANGE/CREATE/RISK/ORDER/VERIFY 结构化输出 |
| reviewer | 提交前验证、PR 审查 | sonnet | Read, Grep, Glob（只读） | 按优先级检查：崩溃→可利用→会慢→是否测试→可读性，输出 VERDICT |

关键设计：两者都在**隔离上下文窗口**中启动——不共享主会话的上下文历史，避免上下文污染。architect 小于 3 文件时跳过（"This doesn't need a plan. Just do it."），避免过度设计。

## Supporting Sources

- [[sources/ai-template2-scaffold]]
- [[sources/fireworks-tech-graph]]
- [[sources/self-evolving-claude-code]]

## Related Pages

- [[entities/harness]]
- [[entities/fireworks-tech-graph]]
- [[concepts/layered-project-harness]]
- [[concepts/diagram-generation-as-skill]]

## Contradictions / Nuance

- 技能越多，路由逻辑越复杂：小型项目可能不需要这么多专项检查。
- Agent 自带的技能列表是预设的，如果项目有特殊检查维度（如支付/安全），需要自行扩展。
