---
title: 地图，而非手册
type: concept
status: active
updated: 2026-05-13
source_count: 5
---

# Concept: 地图，而非手册（Map, not Manual）

## Definition

AI 项目上下文文件（如 AGENTS.md、CLAUDE.md）应充当导航地图而非完整手册：只放"去哪里找什么"的索引和硬性规则，详细内容通过链接指向专项文档。建议控制在 200 行左右（小项目 30-40 行即可覆盖 90% 场景；中大型项目 200-400 行；超过 300 行应切换为索引模式，AGENTS.md 本身 100-120 行作为目录索引，详细内容下放到 `docs/` 子目录）。

## Why It Matters

"什么都重要的时候，什么都不重要。" 如果把所有内容塞进上下文文件，AI 的注意力被稀释，真正关键的规则反而被淹没。模型已经足够聪明，知道什么时候该去查阅详细文档和源码——上下文文件只需要告诉它"文档在哪、源码在哪、什么时候该去看"。

## Core Components

- **写入 AGENTS.md 的两类内容**：
  - AI 理解项目全貌的必要信息（技术栈、仓库结构、核心模块、分层架构）
  - 违反会直接导致问题的硬性规则（编码规约、命名约定、禁止项）
- **不写入的内容**：详细文档通过链接指向 `docs/`，按需查阅。
- **判断标准**：AI 不知道就会写出**错误**的代码 → 放 AGENTS.md；只是写出**不够好**的代码 → 放详细文档。
- **渐进式披露**：从 200 行地图出发，链接指向分层文档（架构文档、开发手册、设计文档、参考项目说明）。

## Relationship to Progressive Disclosure

本概念与 [[concepts/progressive-disclosure-context-retrieval]] 在"按层暴露、按需深入"上共享底层理念，但适用层次不同：

| 维度 | Map, not Manual | 渐进式上下文检索 |
|------|----------------|-----------------|
| 适用对象 | 项目上下文文件（AGENTS.md） | Agent 记忆系统（Claude-Mem） |
| 核心操作 | 编写时精简，用链接替代全文 | 检索时按层暴露，先摘要后细节 |
| 设计目标 | 控制注意力稀释 | 控制上下文成本 |

两者可叠加：AGENTS.md 本身遵循"地图"原则，Agent 在执行时通过渐进式检索获取更深层上下文。

## 三层文件结构（来自错误率分析）

[[sources/claude-md-error-rate-reduction]] 提出将"地图"原则具体化为三层结构：

| 层 | 位置 | 内容 | 行数 |
|----|------|------|------|
| 第一层 | 根目录 `CLAUDE.md` | 高频行为约定（先读再写、小切片、少顺手改、测试说明、失败显性化） | 80-120 行 |
| 第二层 | `docs/agent/project.md` | 项目事实（命令、目录边界、错误处理模式、日志约定） | 按需 |
| 第三层 | `docs/agent/migrations.md` 等 | 任务流程（按场景独立的详细指南） | 按需 |

主文件只做索引：

```markdown
## Task references
- For database migrations, read `docs/agent/migrations.md`.
- For new API endpoints, read `docs/agent/api-endpoint.md`.
```

核心理念：上下文窗口不是资料仓库。当前任务需要什么，就让什么靠近模型；低频流程留在外面，用的时候再读。

## 索引模式详细结构

[[sources/agents-md-cars-guide]] 为大项目提供了具体的索引模式目录结构：

```
project-root/
├── AGENTS.md          # 只放概览 + 关键指针 + 硬约束（100~120 行）
├── docs/
│   ├── README.md      # 所有文档的总索引
│   ├── adr/           # 架构决策记录
│   ├── conventions/   # 编码规范
│   ├── workflows/     # 常用操作流程
│   ├── patterns/      # 设计模式
│   └── gotchas.md     # 常见坑
```

触发条件：AGENTS.md 超过 300 行、经常有人抱怨"又过时了"时。

## CLAUDE.md 150 行限制（来自自进化系统）

[[sources/self-evolving-claude-code]] 提出更保守的建议：**CLAUDE.md 控制在 150 行以内**——超过这个长度 Claude 的指令遵从度下降，因为上下文变得嘈杂。领域特定的规则（安全、API 设计、性能）应移到 `.claude/rules/` 目录，通过路径匹配按需加载。

与 200 行建议的差异：本文将 Commands 和 Architecture 部分（项目特定信息）也算入行数预算，而 [[sources/claude-md-error-rate-reduction]] 的 80-120 行主要指"高频行为约定"。

额外约束：`learned-rules.md`（已毕业的自动学习规则）上限 50 行，强制要么晋升到 CLAUDE.md/rules/ 要么淘汰——防止规则无限膨胀。

## Supporting Sources

- [[sources/agents-md-guide]]
- [[sources/superpowers-workflow-deconstruction]]
- [[sources/claude-md-error-rate-reduction]]
- [[sources/agents-md-cars-guide]]
- [[sources/self-evolving-claude-code]]

## Related Pages

- [[entities/agents-md]]
- [[entities/claude-code]]
- [[concepts/progressive-disclosure-context-retrieval]]
- [[concepts/context-and-cost-optimization]]

## Contradictions / Nuance

- 200 行是经验法则而非硬约束；大型 monorepo（如 OpenAI 的 88 个嵌套 AGENTS.md）可能需要不同的精简策略。
- "地图"原则假设模型足够聪明能自行查阅链接文档——但对于复杂架构，模型可能需要更多内联上下文才能做出正确判断。
