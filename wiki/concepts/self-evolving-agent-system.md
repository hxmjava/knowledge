---
title: 自进化 Agent 系统
type: concept
status: active
updated: 2026-05-13
source_count: 1
---

# Concept: 自进化 Agent 系统（Self-Evolving Agent System）

## Definition

将 AI 编码 agent 从静态配置的工具改造为持续自我改进的系统：通过结构化的记忆捕获、规则验证和晋升机制，让 agent 每次会话都基于真实反馈变得更精确。核心隐喻是**免疫系统**而非日记本——好的系统全通过时静默，只在违规时浮出水面。

## Why It Matters

大多数 AI 编码配置是静态的：写一次 CLAUDE.md，之后要么不更新，要么越加越臃肿。自进化系统将"改进"从人工维护任务升级为系统内置能力——agent 自动观察、捕获纠正、验证合规，并将反复验证通过的模式晋升为永久规则。核心价值在于**第 1 次会话和第 20 次会话之间的差距**会持续拉大。

## 四层架构

| 层 | 名称 | 职责 | 实现 |
|---|------|------|------|
| 第一层 | 认知核心（Cognitive Core） | 编程 agent 的思维方式：决策框架 + 完成标准 + 进化协议 | `CLAUDE.md` |
| 第二层 | 专用子智能体 | 在隔离上下文窗口中执行专注任务 | `.claude/agents/`（architect.md, reviewer.md） |
| 第三层 | 路径作用域规则 | 只在相关场景下加载安全/性能/API 规则，保持上下文精简 | `.claude/rules/`（security.md, api-design.md, performance.md） |
| 第四层 | 进化引擎 | 捕获纠正和观察、自动验证、晋升规则、追踪趋势 | `.claude/memory/` + `.claude/skills/evolution/` |

## 决策框架（写代码前必须运行）

1. **先 grep**：搜索现有模式再创建新内容——如果已有约定就遵循它
2. **评估影响范围**：哪些依赖会受影响？检查 imports、tests、consumers
3. **不确定就问**：只问一个澄清问题，不猜测不连问五个
4. **最小改动**：解决被问到的问题，不做顺手重构
5. **验证计划**：写代码前先想好怎么证明它能工作

## 进化循环

```
会话启动 → 验证扫描（每条规则的 verify: 检查）
    ↓
会话活动 → 观察（自动验证后记录）+ 纠正（自动生成 verify: 行）
    ↓
会话结束 → 会话评分卡（纠正数、规则通过率、趋势检测）
    ↓
定期 /evolve → 审计：晋升、淘汰、重写，等用户审批
```

## 核心设计原则

- **"没有验证检查的规则是愿望，有验证检查的规则才是护栏。只有护栏才能存活。"**
- 规则不靠 agent 记忆遵守——直接运行 grep 确认合规，只有违规时才报告。
- CLAUDE.md 150 行以内（超过指令遵从度下降），learned-rules.md 50 行以内——强制晋升或淘汰。
- 纠正 2 次同模式 → 自动晋升为 learned-rules（附 verify 行）；10+ 会话持续通过 → 候选晋升到 CLAUDE.md 或 rules/。
- 拒绝的规则记入 evolution-log.md，永不重新提议。
- 不删除纠正日志（它们是 provenance）。
- 永远不削弱安全规则和完成标准。

## Relationship to Other Concepts

本概念是多个既有概念的系统化整合：

| 既有概念 | 本概念的增量 |
|---------|------------|
| [[concepts/persistent-agent-memory]] | 记忆系统增加了 verify 行、晋升逻辑和会话评分——从"便签本"升级为"免疫系统" |
| [[concepts/behavioral-contract-vs-prompt]] | 用"行为编程"（behavior programming）强化了这一视角——CLAUDE.md 是塑造认知的代码 |
| [[concepts/hooks-as-safety-net]] | hooks 从"安全提醒"升级为"结构性执行"——让进化循环不依赖 agent 的自觉性 |
| [[concepts/bad-case-driven-iteration]] | 从人工判断的"事后补规则"升级为自动验证 + 自动晋升——更激进但有误晋升风险 |
| [[concepts/verification-before-completion]] | 每条规则都需 verify 行——将"完成需验证"泛化为"所有规则需验证" |

## Supporting Sources

- [[sources/self-evolving-claude-code]]

## Related Pages

- [[entities/claude-code]]
- [[entities/meta-alchemist]]
- [[concepts/verification-sweep]]
- [[concepts/rule-promotion-ladder]]
- [[concepts/persistent-agent-memory]]
- [[concepts/hooks-as-safety-net]]
- [[concepts/context-and-cost-optimization]]

## Contradictions / Nuance

- 自动晋升（2 次纠正 → 永久规则）比 bad case 驱动迭代的人工判断更激进——可能产生误晋升，需要 `/evolve` 定期审计作为安全阀。
- `verify: manual` 规则（无法自动检查的规则）存在执行缺口——系统设计上承认这是"技术债"，但未提供具体解决方案。
- 验证扫描的性能开销随规则数量增长——50 条上限是经验值，大型项目可能不够。
- 免疫系统隐喻假设所有规则都能被机器检查——行为类规则（如"不要顺手重构"）的可检查性有限。
