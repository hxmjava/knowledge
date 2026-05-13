---
title: 规则晋升阶梯
type: concept
status: active
updated: 2026-05-13
source_count: 1
---

# Concept: 规则晋升阶梯（Rule Promotion Ladder）

## Definition

将 AI agent 的学习信号按置信度分层存储和晋升：纠正记录 → 自动晋升为已学规则 → 人工审批后晋升为永久配置。每一层都要求更高的证据标准和机器可检查的验证，防止低质量信号污染长期配置。

## Why It Matters

AI agent 在使用中会积累大量信号（用户纠正、代码模式观察、违规记录），但并非所有信号都值得永久化。晋升阶梯确保：(1) 每条信号有明确来源和验证；(2) 反复出现的模式自动升级；(3) 过时或误判的信号被定期淘汰；(4) 永久配置只包含高置信度、经验证的规则。

## 晋升层级

| 信号类型 | 存储位置 | 晋升条件 | 下一目标 |
|---------|---------|---------|---------|
| 纠正 1 次 | `corrections.jsonl` | 记录 + 自动生成 verify 行 | 同模式纠正第 2 次 |
| 纠正 2 次同模式 | `learned-rules.md` | **自动晋升**，附 verify 行 | 10+ 会话持续通过 |
| 观察 confirmed + 0 反例 | `learned-rules.md` | **自动晋升**（不需要 `/evolve`） | 10+ 会话持续通过 |
| 观察 low-confidence | `observations.jsonl` | 记录，标记 `recheck_after: 3 sessions` | 等待更多证据 |
| 在 learned-rules 10+ 会话 | 候选 | `/evolve` 审批 | CLAUDE.md 或 rules/ |
| 拒绝的提议 | `evolution-log.md` | 永不重新提议 | — |

## 容量管理

- `learned-rules.md` 设计上限 **50 行**——强制晋升或淘汰。
- 接近 50 行时检查：
  - 哪些规则连续通过 10+ 会话 → 晋升候选
  - 哪些规则的 verify 行是 `manual` → 重写或淘汰候选
  - 建议运行 `/evolve` 做全面审计

## /evolve 审计命令

定期运行（建议每 10+ 会话），执行以下步骤：

1. **分析纠正**：按模式分组，找重复纠正（应已晋升）、纠正聚类（指向缺失规则）、纠正与现有规则矛盾（规则错了，不是用户）
2. **分析观察**：高置信度多次确认 → 晋升候选；与纠正匹配的观察（汇合信号最强）
3. **审计已学规则**：还相关吗？该晋升吗？已被 linter/CLAUDE.md 覆盖？太模糊？
4. **检查进化日志**：不重新提议被拒绝的规则
5. **列出提案**：每条显示 PROPOSE → 规则文本 → 来源 → 证据 → 目标位置
6. **等待审批**：用户逐条 approve/reject/modify，全部记录到 evolution-log.md

提案类别：PROMOTE（观察→learned-rules）、GRADUATE（learned-rules→永久）、PRUNE（淘汰过时）、UPDATE（新证据修改）、ADD（纠正模式新规则）

## 约束条件

- 永不删除安全规则
- 永不削弱完成标准
- 永不添加与 CLAUDE.md 矛盾的规则
- 每条规则必须足够具体，能够测试合规性
- 偏好具体性而非抽象性

## Relationship to Bad Case Driven Iteration

本概念是 [[concepts/bad-case-driven-iteration]] 的自动化变体：

| 维度 | Bad Case 驱动迭代 | 规则晋升阶梯 |
|------|-----------------|------------|
| 驱动力 | 人工判断 AI 犯错 | 系统自动检测纠正模式 |
| 晋升决策 | 人工判断放全局还是模块级 | 量化触发（2 次纠正/10 次通过） |
| 验证方式 | 补充自动化检查 | 每条规则自带 verify 行 |
| 淘汰机制 | 定期 lint 审查 | 容量上限（50 行）+ `/evolve` 审计 |
| 风险 | 规则体系缺乏系统性 | 可能误晋升低质量规则 |

## Relationship to Persistent Agent Memory

本概念将 [[concepts/persistent-agent-memory]] 的存储-检索模型扩展为存储-验证-晋升模型——记忆不只是"记住发生了什么"，还要"执行学到的规则"并"将反复验证的知识固化"。

## Supporting Sources

- [[sources/self-evolving-claude-code]]

## Related Pages

- [[concepts/self-evolving-agent-system]]
- [[concepts/verification-sweep]]
- [[concepts/persistent-agent-memory]]
- [[concepts/bad-case-driven-iteration]]
- [[concepts/verification-before-completion]]

## Contradictions / Nuance

- 量化触发条件（2 次纠正 → 自动晋升）比人工判断更激进——在纠正来自同一误解模式时可能误晋升。
- 50 行上限在复杂项目中可能不够——但放宽上限又会增加上下文负担，这是设计上的有意取舍。
- "永不重新提议被拒绝的规则"需要稳定的进化日志——如果日志丢失或项目重启，被拒绝的规则可能被重新提议。
