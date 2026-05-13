---
title: Mnimiy
type: entity
status: active
updated: 2026-05-12
source_count: 1
---

# Entity: Mnimiy

## What It Is

AI 编程实践者，在 X（Twitter）上分享 Claude Code 使用经验。将 Karpathy 的 4 条 CLAUDE.md 规则在 30 个代码库上进行了为期 6 周的扩展实验。

## Key Facts

- 在 Karpathy 4 条规则基础上扩展到 12 条，新增规则包括：Model for Judgment Only、Token Budgets、Surface Conflicts、Read Before Write、Tests Verify Intent、Checkpoint Steps、Match Conventions、Fail Loud。
- 声称实验结果：错误率从 41% 降至 3%（30 个代码库、6 周）。
- 原文发布于 X：[Mnimiy 的文章](https://x.com/Mnilax/article/2053116311132155938)
- 该数据尚未经独立复现验证，不同条件结果可能不同。

## Relationships

- Related entities: [[entities/karpathy]], [[entities/forrest-chang]]
- Related concepts: [[concepts/behavioral-contract-vs-prompt]]

## Evidence

- [[sources/claude-md-error-rate-reduction]]

## Open Questions

- 30 个代码库的规模、语言、类型分布是什么？结果是否对特定领域有偏？
- 评判"错误"的标准是什么？是人工标注还是自动化指标？
- 12 条规则中哪些对错误率下降贡献最大？是否有消融实验数据？
