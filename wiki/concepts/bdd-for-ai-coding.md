---
title: BDD for AI Coding（行为驱动开发）
type: concept
status: active
updated: 2026-05-13
source_count: 1
---

# Concept: BDD for AI Coding（行为驱动开发）

## Definition

行为驱动开发（Behavior-Driven Development）在 AI 辅助开发中的应用：使用业务可读的行为描述（如 Gherkin 的 Given-When-Then）编写"活文档"，作为跨角色（业务、开发、测试）协作的统一语言，并为 AI 提供行为上下文。BDD 强调"活文档"——可执行的行为规格既是文档也是测试。

## Why It Matters

BDD 的核心价值在 AI 时代从"减少需求歧义"扩展为"跨角色协作提示词"——业务人员编写的 Given-When-Then 场景可以直接作为 AI 的行为约束上下文，弥合自然语言与代码之间的翻译损耗。

## Core Components

- **活文档**（Living Documentation）：行为规格既是文档也是可执行测试，持续保持一致性。
- **统一语言**：业务和技术团队使用同一套 Given-When-Then 描述系统行为。
- **Gherkin 语法**：Feature → Scenario → Given/When/Then 的结构化行为描述。
- **跨角色协作**：业务定义验收标准，开发实现，测试验证——三方在同一个文档上对齐。

## 与 ATDD 的定位差异

BDD 更侧重协作性和活文档价值，ATDD 更侧重 AI 约束强度和可执行性。在 AI Vibecoding 场景中：

- **ATDD 为主**：用于生成严格的行为约束，防止 AI 实现细节泄露。
- **BDD 为辅**：用于跨角色沟通和活文档维护，保持业务可读性。

## Concrete Example

```gherkin
Feature: 用户注册
  作为一名新用户
  我想要使用邮箱和密码注册账号
  以便能够登录系统并使用服务

  Scenario: 使用邮箱和密码成功注册
    Given 系统中还没有使用 「alice@example.com」 注册的用户
    When 用户在注册页面输入邮箱 「alice@example.com」 和密码 「secret123」
    And 点击"注册"按钮
    Then 系统成功创建用户账户
    And 用户可以使用该邮箱和密码立即登录系统
```

注意：此版本允许"注册页面""点击按钮"等轻微 UI 描述，在纯 ATDD 视角下被视为实现细节泄露。

## Supporting Sources

- [[sources/vibecoding-tdd-atdd-bdd-ddd-sdd]]

## Related Pages

- [[concepts/atdd-for-ai-coding]]（对比方法论，AI 约束更强）
- [[concepts/ddd-domain-driven-design]]（统一语言的理论基础）
- [[concepts/spec-driven-workflow-and-review-discipline]]

## Contradictions / Nuance

- BDD 声称使用"统一语言"，但 Gherkin 语法本身对非技术人员仍有一定学习门槛——实际协作中是否真正实现了跨角色对齐？
- BDD 的"允许轻微 UI 描述"与 ATDD 的"严格纯领域语言"之间的边界在实践中模糊——"点击注册按钮"算实现细节还是行为描述？
- Cucumber 生态在 AI 编码工具中的集成成熟度如何？是否有类似 swingerman/atdd 的 AI 原生 BDD 工具？
