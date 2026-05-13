---
title: Andrej Karpathy
type: entity
status: active
updated: 2026-05-12
source_count: 1
---

# Entity: Andrej Karpathy

## What It Is

AI 领域知名研究者和实践者，前 Tesla AI 总监、OpenAI 联合创始人。在 AI 编程领域以对 Claude Code 等工具的直率评价和实用建议著称。

## Key Facts

- 提出 CLAUDE.md 4 条核心规则，针对 Claude Code 编码中的常见失败模式：
  1. **写代码前先说明假设**——防止模型默默做假设
  2. **先选简单方案**——防止过度复杂化
  3. **只做必要改动**——防止顺手改不该动的代码
  4. **围绕成功标准循环验证**——防止空口宣称完成
- 这 4 条被 Forrest Chang 整理为开源 CLAUDE.md 模板，后被 Mnimiy 在 30 个代码库上扩展验证。
- 其观察的底层洞见：Agent 的失败模式（猜、扩、混、忘、装作完成）与人类新手工程师类似，但 Agent 无法通过"被提醒一次"来记住——需要写入仓库。

## Relationships

- Related entities: [[entities/forrest-chang]], [[entities/mnimiy]], [[entities/claude-code]]
- Related concepts: [[concepts/bad-case-driven-iteration]], [[concepts/behavioral-contract-vs-prompt]]

## Evidence

- [[sources/claude-md-error-rate-reduction]]

## Open Questions

- Karpathy 是否有更多关于 AI 编程工具使用方法的公开分享？
- 4 条规则是否已演进为更完整的官方建议？
