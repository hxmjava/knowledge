---
title: Context and Cost Optimization
type: concept
status: active
updated: 2026-05-13
source_count: 6
---

# Concept: Context and Cost Optimization

## Definition

通过上下文精简、任务拆分、调试可观测与模型选型，控制 AI 编码系统的响应性能与调用成本。

## Why It Matters

在企业长期使用中，性能与成本不是附属指标，而是系统能否持续运行的约束条件。

## Core Components

- 精简 `CLAUDE.md` 与分层配置（见下方"CLAUDE.md 的 Token 预算视角"）
- 控制会话上下文规模（清理历史、拆分大任务）
- 使用 `--verbose` 定位瓶颈
- 按任务复杂度选择模型并设置预算阈值
- 使用渐进式披露检索历史上下文，先取摘要和最近上下文，再按需深入观察、文件或时间线

### Prompt-Level Context Management（来自 AI Coding 实践）

七条实测有效的提示词上下文管理技巧：

1. **明确目标而非只描述修改点**：含语言/框架/风格约束，减少返工轮次。
2. **只附相关文件**：针对性地选择文件，不丢整个代码库。
3. **策略性管理已打开文件**：Cursor 等工具自动将已打开文件纳入上下文；只保留相关文件打开。
4. **利用非代码上下文来源**：终端输出、linter 错误、测试结果都是有价值的调试上下文。
5. **新任务开新对话**：上下文窗口有限，避免单一线程过长导致质量下降。
6. **提供格式/风格示例**：模型在模仿模式方面表现出色，示例比描述更高效。
7. **使用图像辅助**：UI 截图或图表能传达难以用文字描述的上下文信息。

> **核心认知**：做好上下文管理，其影响最终要大于精心设计完美的提示词——输入内容的质量直接决定输出内容的质量。

### Context 不足的三种补充策略

| 策略 | 工具/方法 | 说明 |
|------|-----------|------|
| 自动记忆 | [[entities/claude-mem\|Claude-Mem]] | 自动捕获工具使用观察、生成语义摘要，跨会话保留上下文 |
| 会话总结与注入 | `prompt process.md` | 总结当前会话生成文件，新会话窗口 `@process.md` 注入 |
| 永久归档追溯 | OpenSpec `proposal/design/spec/tasks.md` | 永久归档，方便历史追溯 |

> 三者互补：Claude-Mem 提供跨会话的被动记忆，会话总结提供主动的上下文注入，OpenSpec 归档提供不可变的历史追溯。

### 图谱驱动的上下文裁剪（来自 code-review-graph）

当仓库足够大、变更跨文件时，可以在本地维护代码结构图谱（Tree-sitter → SQLite），AI 助手通过 MCP 查询影响面，只读取变更真正波及的代码子集。

- 实测平均 token 节省 8.2×（6 仓库 13 commits）
- 小型单文件变更可能开销更大（0.7×），图谱有固定 token 开销
- 核心权衡：recall 100%（不漏检）vs precision 0.38（倾向多报）

> 将上下文优化从"人类手动选择文件"推进到"结构化工具自动推荐最小评审集"。

详见 [[concepts/code-structure-graph-for-ai]] 和 [[concepts/blast-radius-impact-analysis]]。

### 路径作用域规则（来自自进化系统）

[[sources/self-evolving-claude-code]] 提出用 **路径作用域规则** 实现上下文精简：`.claude/rules/` 中的 `.md` 文件通过 frontmatter `paths:` 字段限定加载范围，Claude 只在处理匹配路径的文件时才加载对应规则——编辑 CSS 时不读 200 行安全规范。

| 规则文件 | 加载路径 | 覆盖范围 |
|---------|---------|---------|
| `security.md` | `src/api/**/*`, `src/auth/**/*` | 输入验证、鉴权、SQL 注入、PII 掩码 |
| `api-design.md` | `src/api/**/*`, `src/handlers/**/*` | Handler 结构、响应格式、分页、限流 |
| `performance.md` | `src/**/*`（全局） | N+1 查询、缺失索引、无界查询 |
| `core-invariants.md` | `*/`（全局、压缩防护） | 项目最痛的 3-5 条底线规则 |

`core-invariants.md`（路径 `*/`）在每次工具调用时重新注入，即使对话上下文被压缩也不受影响——是"压缩防护"的关键机制。

### CLAUDE.md 的 Token 预算视角（来自错误率分析）

[[sources/claude-md-error-rate-reduction]] 强调 CLAUDE.md 是上下文窗口的常驻消费者——每一行都会和当前任务抢注意力和 token。关键约束：

- Anthropic 官方建议：单文件控制在 200 行以内，指令具体简洁有结构。
- 规则互相冲突时，Claude 可能随机选一条——规范越厚，冲突概率越高。
- 一个两行的小改动，如果带着 400 行规则一起跑，模型可能读了一堆无关文档、检查了一堆不相关边界才敢动手。
- Mnimiy 的 12 条规则本身有价值，但不应整包复制——没有长任务就先别写复杂的检查点规则，没有多服务 monorepo 就别写跨代码库风格选择。

解决方案：三层文件结构（根目录 CLAUDE.md 80-120 行 → 项目事实文件 → 任务流程文件按需索引），与 [[concepts/map-not-manual]] 的"地图"原则一致。

## Supporting Sources

- [[sources/claude-code-enterprise-playbook]]
- [[sources/claude-mem]]
- [[sources/agents-md-guide]]
- [[sources/openspec-superpowers-practice-guide]]
- [[sources/code-review-graph]]
- [[sources/claude-md-error-rate-reduction]]
- [[sources/self-evolving-claude-code]]

## Related Pages

- [[entities/claude-code]]
- [[entities/code-review-graph]]
- [[entities/claude-mem]]
- [[entities/agents-md]]
- [[concepts/team-governance-for-ai-coding]]
- [[concepts/ingest-query-lint-loop]]
- [[concepts/progressive-disclosure-context-retrieval]]
- [[concepts/map-not-manual]]
- [[concepts/obsidian-project-symlink]]
- [[concepts/self-evolving-agent-system]]

## Contradictions / Nuance

- 追求极致低成本可能牺牲复杂问题质量；需按任务价值匹配模型与预算。
