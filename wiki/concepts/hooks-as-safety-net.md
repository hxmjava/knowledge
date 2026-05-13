---
name: Hooks as Safety Net
description: Using lifecycle hooks (PreToolUse, PostToolUse, PostToolUseFailure, Stop) as lightweight safety reminders that operate alongside AI agent decisions without blocking.
type: concept
status: draft
updated: 2026-05-13
source_count: 5
---

# Concept: Hooks as Safety Net

## Definition

在 Claude Code 中通过生命周期 Hooks 实现轻量安全提醒：编辑高风险文件前提醒、构建命令结果记录、对话结束时验证状态检查。默认 fail-open（hook 失败不阻塞 AI），做提醒不做强制阻断。

## Why It Matters

AI 可能在大量文件修改中忽略高风险路径，或在宣称「编译通过」后忘记执行构建。Hooks 在关键时点自动注入提醒，无需用户手动提醒，也不依赖 AI 的自觉性。

## Hook Lifecycle

| Hook | 触发时机 | 行为 |
|------|---------|------|
| PreToolUse | Edit/Write/Bash 执行前 | 命中高风险路径时注入提醒；检测到构建命令时记录 |
| PostToolUse | Bash 执行后（成功） | 记录构建验证摘要 |
| PostToolUseFailure | Bash 执行后（失败） | 记录失败摘要 |
| Stop | 对话结束 | 检查高风险改动是否已验证；提醒 OpenSpec 归档 |

## Configuration

通过 `hooks-config.json` 配置：
- 各 Hook 开关
- 构建命令关键字（`mvn `、`gradle `、`npm run ` 等）
- 高风险路径子串数组（`high_risk_markers`）
- 验证/评审命令提示

## Design Principles

- 默认 fail-open：hook 失败不阻塞 Claude Code
- 提醒优先，不做强制 deny
- 与仓库现有高风险规则对齐，不另起一套标准
- 模板提供通用默认值，项目落地时优先改配置而非脚本
- 也可作为记忆系统的捕获入口，将会话、提示、工具使用和结束摘要转化为可检索历史

## Variant: Superpowers SessionStart Hook

Superpowers 使用 `SessionStart` hook 作为 Claude Code/Cursor/Copilot CLI 的引导注入路径：`hooks/session-start` 读取 `skills/using-superpowers/SKILL.md`，转义为 JSON 后嵌入 `<EXTREMELY_IMPORTANT>` 包裹的 bootstrap 文本。`run-hook.cmd` 是多语言脚本（Windows batch + Unix bash），确保跨平台兼容。此 hook 的角色不同于安全提醒，而是**行为约束注入**——将技能系统的总规则送入代理上下文。

## 提醒 vs 门禁的分工（来自错误率分析）

[[sources/claude-md-error-rate-reduction]] 明确区分了两个层次：
- **CLAUDE.md**：告诉 Agent"怎么做"——是提醒，不是门禁。
- **Hooks + 权限**：决定"能不能这么做"——是门禁，不是提醒。

典型场景：CLAUDE.md 写"不要读 .env"只是提醒；在 settings.json 里 deny 或用 PreToolUse hook 挡住才是真正的拦截。Mitchell Hashimoto 原则：Agent 犯错后要顺手补一个机制，机制层次从轻到重是：AGENTS.md 规则 → lint/测试 → hooks/权限 → CI/review。

详见 [[concepts/reminders-vs-hard-enforcement]]。

## "结构性执行"升级（来自自进化系统）

[[sources/self-evolving-claude-code]] 将 hooks 的定位从"安全提醒"推进到"结构性执行"——hooks 不只是在关键时点注入提醒，而是**确保进化循环的每一步都不被跳过**：

| Hook | 传统用法（安全提醒） | 自进化系统用法（结构性执行） |
|------|-------------------|--------------------------|
| SessionStart | 提醒高风险路径 | 注入"读取 learned-rules.md 并运行验证扫描"——在用户第一条消息之前触发 |
| PreToolUse (Edit/Write) | 检测高风险文件名 | 提醒"检查当前文件是否有路径作用域规则"——违规发生之前阻止 |
| Stop | 检查高风险改动是否已验证 | 提醒"记录纠正和观察，写入会话评分卡"——不再有"忘了记录" |

核心差异："指令说要做" vs "系统结构性地让你很难跳过"。自进化系统的三个 hooks 构成了进化循环的骨架——会话启动时扫描、编辑时检查、结束时记录——没有一步依赖 Claude "记得要做"。

详见 [[concepts/verification-sweep]] 和 [[concepts/self-evolving-agent-system]]。

## Supporting Sources

- [[sources/ai-template2-scaffold]]
- [[sources/claude-mem]]
- [[sources/superpowers-deep-practice-guide]]
- [[sources/claude-md-error-rate-reduction]]
- [[sources/self-evolving-claude-code]]

## Related Pages

- [[entities/harness]]
- [[entities/claude-code]]
- [[entities/claude-mem]]
- [[concepts/reminders-vs-hard-enforcement]]
- [[concepts/schema-driven-maintenance]]

## Contradictions / Nuance

- fail-open 在安全敏感项目中可能不够——某些场景可能需要 fail-closed（hook 失败则阻断）。
- Hooks 脚本依赖 Python，在无 Python 环境的项目中需要替代方案。
