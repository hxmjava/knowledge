---
title: ATDD for AI Coding（验收测试驱动开发）
type: concept
status: active
updated: 2026-05-13
source_count: 1
---

# Concept: ATDD for AI Coding（验收测试驱动开发）

## Definition

验收测试驱动开发（Acceptance Test-Driven Development）在 AI 辅助开发中的应用：使用纯领域语言（无实现细节）编写 Given-When-Then 验收规格，作为 AI 代码生成的最高层行为约束。验收测试定义"做什么"（WHAT），单元测试定义"怎么做"（HOW），两者必须同时通过。

## Why It Matters

AI 编码的两大核心问题——无约束生成和实现细节泄露——恰好是 ATDD 的靶心。纯领域语言的验收规格将 AI 的"自由发挥"空间压缩到业务语义允许的范围内，同时避免 AI 在规格中混入类名、API 路径、数据库表名等实现细节，保持规格的可读性和可维护性。

## Core Components

- **纯领域语言规格**：使用 Given-When-Then 格式，每条语句以句号结尾，禁止任何实现细节（类名、API、数据库表名）。
- **双流测试**：验收测试（WHAT）定义业务行为，单元测试（HOW）验证实现细节，两者独立运行且必须同时通过。
- **变异测试**（Mutation Testing）：作为第三层验证，通过故意引入代码变异来检测测试套件的缺陷捕获能力。
- **spec-check 泄露检查**：自动检测规格中是否混入了实现细节（如"注册页面""点击按钮"等 UI 描述）。
- **多代理团队编排**：Spec Writer（编写规格）、Implementer（实现代码）、Spec Guardian（守护规格纯度）。

## 与 BDD 的关键区别

| 维度 | BDD | ATDD |
|------|-----|------|
| 语言纯度 | 允许轻微 UI/流程描述 | 严格纯领域语言 |
| 可执行性 | 需要额外自动化步骤 | 天然可执行 |
| AI 约束强度 | 中等 | 极强（防止实现细节泄露） |
| 协作性 | 极强（业务+开发共同编写） | 较强（验收定义为主） |
| 文档价值 | 活文档 | 可执行标准 |

推荐策略：ATDD 为主（约束 AI），BDD 为辅（跨角色协作和活文档）。

## Concrete Example

功能：用户使用邮箱和密码注册账号

```
; 用户可以使用邮箱和密码注册新账号。
GIVEN 系统中没有使用邮箱 「alice@example.com」 注册的用户。

WHEN 一个新用户使用邮箱 「alice@example.com」 和密码 「secret123」 完成注册。

THEN 系统中存在 1 个使用该邮箱注册的用户。
THEN 该用户可以使用邮箱 「alice@example.com」 和密码 「secret123」 成功登录系统。
```

关键设计：
- 禁止"注册页面""点击按钮"等实现暗示。
- 每条语句以句号结尾，便于 AI 解析。
- 直接可转化为失败的验收测试。

## Representative Tool: swingerman/atdd

- Claude Code 插件（支持 Cursor 等编辑器）。
- 命令：`/atdd:atdd` 启动流程，`/atdd:spec-check` 检查泄露，`/atdd:mutate` 变异测试。
- 灵感来源于 Uncle Bob 的 empire-2025 项目。

## Supporting Sources

- [[sources/vibecoding-tdd-atdd-bdd-ddd-sdd]]

## Related Pages

- [[entities/swingerman-atdd]]
- [[concepts/bdd-for-ai-coding]]（对比方法论）
- [[concepts/tdd-as-hard-gate]]（执行层互补）
- [[concepts/sdd-spec-driven-development]]（战略层互补）
- [[concepts/verification-before-completion]]

## Contradictions / Nuance

- "纯领域语言"约束在 BDD 社区也有类似主张，但实践中 BDD 仍允许轻微 UI 描述——ATDD 的"严格纯领域语言"在大型项目中是否会导致规格可读性下降？
- ATDD 的变异测试作为第三层验证增加了验证成本——在快速迭代场景中是否总是值得投入？
- 多代理团队编排（Spec Writer、Implementer、Spec Guardian）增加了协调开销——对小团队或个人开发者是否过度？
