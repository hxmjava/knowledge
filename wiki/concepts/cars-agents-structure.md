---
title: C.A.R.S 结构
type: concept
status: active
updated: 2026-05-12
source_count: 1
---

# Concept: C.A.R.S 结构（C.A.R.S Framework for AGENTS.md）

## Definition

一种 AGENTS.md 的组织框架，将内容分为四个区块：**C**ommands（开发命令）、**A**rchitecture（架构与目录）、**R**estrictions（约束与禁忌）、**S**tandards（流程规范）。核心理念是优先写 Commands 和 Restrictions——前者防止低级错误，后者防止大问题。

## Why It Matters

AGENTS.md 的内容组织方式直接影响 AI 的遵守效果。C.A.R.S 提供了一个实用的优先级排序：先写死命令杜绝低级错误，再加硬约束防止严重后果，然后补充架构上下文，最后放日常流程规范。这比"想到什么写什么"更系统化。

## Core Components

- **Commands（开发命令）**：写死具体命令（`pnpm dev`、`pnpm lint && pnpm typecheck`），而非泛泛指示（"使用合适的包管理器"）。AI 默认倾向用 npm，明确写死后可杜绝 90% 以上包管理器错误。
- **Architecture（架构与目录）**：精确到补丁版本的技术栈（"Next.js 15.3 + TypeScript 5.7"）和带注释的目录结构，尤其是 DDD 分层等复杂架构。
- **Restrictions（约束与禁忌）**：被认为是四个区块中最有价值的部分——"不能做什么"比"应该做什么"更能防止大问题。例：金额计算必须用 decimal.js、未确认前不删代码。
- **Standards（流程规范）**：日常协作习惯——Conventional Commits、PR 前完整检查、本地开发端口等。"看起来琐碎，但 AI 真的会照着做。"

## 实战模板（30-40 行）

一份融合 C.A.R.S 模型的紧凑模板声称覆盖日常 90% 以上 Agent 交互场景：

```
# Project Agent Instructions
## Commands — 具体构建/测试/格式化命令
## Architecture — 技术栈+目录结构+分层约定
## Restrictions — NEVER 清单+安全约束
## Standards — 提交规范+验证要求+环境假设
## Verification — 外部 API 行为不确定时查阅文档
```

## 编写优先级

作者建议的编写顺序：先 Commands + Restrictions → 再 Architecture → 最后 Standards + 知识索引。

## Supporting Sources

- [[sources/agents-md-cars-guide]]

## Related Pages

- [[entities/agents-md]]
- [[concepts/map-not-manual]]
- [[concepts/bad-case-driven-iteration]]
- [[concepts/cars-agents-structure]]

## Contradictions / Nuance

- C.A.R.S 是从 Web 项目（Next.js、DDD + CQRS）实践中提炼的框架，在非 Web 项目（移动端、数据工程、ML pipeline）中的适用性待验证。
- Restrictions 作为"最有价值部分"的判断基于作者个人经验，缺乏量化数据支撑——不同项目类型中最有价值的区块可能不同。
- 与 Karpathy 4 条规则的工程分类（控制改动半径、确定性交还给代码、长任务留检查点、失败显性化）在 Restriction 层面有重叠，但 C.A.R.S 更偏操作框架而非设计原则。
