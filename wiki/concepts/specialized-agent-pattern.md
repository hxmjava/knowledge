---
name: Specialized Agent Pattern
description: Using layer-specific AI agents and domain-specific checker skills instead of a single general-purpose agent for all development tasks.
type: concept
status: draft
updated: 2026-05-09
source_count: 2
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

## Supporting Sources

- [[sources/ai-template2-scaffold]]
- [[sources/fireworks-tech-graph]]

## Related Pages

- [[entities/harness]]
- [[entities/fireworks-tech-graph]]
- [[concepts/layered-project-harness]]
- [[concepts/diagram-generation-as-skill]]

## Contradictions / Nuance

- 技能越多，路由逻辑越复杂：小型项目可能不需要这么多专项检查。
- Agent 自带的技能列表是预设的，如果项目有特殊检查维度（如支付/安全），需要自行扩展。
