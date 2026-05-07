---
title: 验证闭环
type: concept
status: active
updated: 2026-05-07
source_count: 1
---

# Concept: 验证闭环（Verification Loop）

## Definition

在 AI 辅助开发中，将"改代码"扩展为完整的「改 → 构建 → 启动 → 验证」循环：AI 不仅产出代码，还必须通过构建、启动服务、调用接口等手段自行验证功能正确性，形成端到端的闭环。验证不止于"编译通过"，而是"功能能跑通"。

## Why It Matters

没有验证闭环时，AI 的工作是断裂的——只能完成"改代码"，构建→启动→验证全靠人驱动。这直接限制了 AI 的自主执行能力，特别是夜间无人值守场景下 Agent 自主完成任务的前提条件。

## Core Components

- **统一环境配置**：环境变量集中在 `~/.<project>_env`，启动脚本自动 source，AI 只需一条命令启动。
- **curl 验证规范**：每个 curl 独立执行、用临时文件传递数据、Token 获取模板化、排查路径明确。
- **多层验证手段**：
  - lint/格式检查：每次代码变更后自动触发
  - 后端：bash/curl 验证接口返回
  - 前端：Agent Browser 验证页面渲染和交互（如 Qoder 的 agent-browser）
- **自动化检查**：规则必须有对应的自动化检查（如分层依赖 lint 脚本），否则 AI 和人都会违反。
- **错误信息三要素**：WHAT（违规什么）+ WHY（为什么不允许）+ HOW（怎么修复），同时服务人类和 AI。

## Relationship to Verification Before Completion

本概念与 [[concepts/verification-before-completion]] 互补但侧重不同：

| 维度 | 验证闭环 | Verification Before Completion |
|------|---------|-------------------------------|
| 侧重点 | 构建端到端验证基础设施 | 完成声明必须绑定验证证据 |
| 核心约束 | 改→构建→启动→验证的完整流程 | 没有新鲜验证结果不得宣称完成 |
| 适用阶段 | 开发和测试全过程中 | 交付关口 |

验证闭环是"怎么验证"，verification-before-completion 是"什么时候才算完"。

## Concrete Example

```bash
# Step 1: 登录，结果写文件
curl -s -X POST http://localhost:8080/auth/login \
  -H 'Content-Type: application/json' \
  -d '{"username":"admin","password":"admin"}' > /tmp/login.json

# Step 2: 提取 token
python3 -c "..." > /tmp/token.txt

# Step 3: 业务接口调用
TOKEN=$(cat /tmp/token.txt)
curl -s -X POST http://localhost:8080/providers/list \
  -H "Authorization: Bearer $TOKEN" \
  -d '{"page":0,"size":10}' > /tmp/result.json
```

## Supporting Sources

- [[sources/agents-md-guide]]

## Related Pages

- [[entities/agents-md]]
- [[concepts/verification-before-completion]]
- [[concepts/tdd-as-hard-gate]]
- [[concepts/map-not-manual]]

## Contradictions / Nuance

- 验证闭环的基础设施搭建成本不低（启动脚本、curl 模板、lint 脚本），对小型项目可能过度投入。
- Agent Browser 验证能力依赖特定工具（如 Qoder），跨工具可移植性待验证。
- curl 规范中的"每个 curl 独立执行 + 临时文件中转"虽然稳定但冗长，可能降低 AI 的执行效率。
