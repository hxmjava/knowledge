---
title: 验证扫描机制
type: concept
status: active
updated: 2026-05-13
source_count: 1
---

# Concept: 验证扫描机制（Verification Sweep）

## Definition

在 AI agent 会话启动时，自动对所有已学规则执行机器可检查的验证测试：读取 `learned-rules.md`，逐条执行 `verify:` 行定义的 grep/glob/check，只在发现违规时才浮出水面。全通过时静默——"最好的免疫系统是无形的"。

## Why It Matters

传统规则系统依赖 agent "记得遵守"——在长会话中指令遵从度下降，规则形同虚设。验证扫描将合规检查从 agent 的"自觉性"升级为**结构性自动执行**：不管 agent 是否记得，验证都会运行。这让规则系统从"建议"进化为"护栏"。

## 工作机制

### verify: 行格式

每条 learned-rules.md 中的规则都必须附带 `verify:` 行——一个机器可执行的检查指令：

```markdown
- Never use the spread pattern to merge options in fetchJSON.
  verify: Grep("\.\.\.options", path="src/api/client.js") → 0 matches
  [source: corrected 2x, 2026-03-28]
```

### 验证模式

| 模式 | 检查方式 | 预期结果 |
|------|---------|---------|
| 代码模式禁止 | `Grep("[pattern]", path="[scope]")` | → 0 matches |
| 代码模式要求 | `Grep("[pattern]", path="[scope]")` | → 1+ matches |
| 文件必须存在 | `Glob("[pattern]")` | → 1+ matches |
| 文件必须不存在 | `Glob("[pattern]")` | → 0 matches |

### 执行协议

1. 读取 `learned-rules.md`，对每条含 `verify:` 行的规则执行检查
2. **PASS** → 静默，继续下一条
3. **FAIL** → 记录到 `violations.jsonl`，向用户报告：规则、违规内容、文件位置、具体修复建议
4. 全通过 → 不说任何话（最好的免疫系统是无形的）
5. 追踪通过率到 `sessions.jsonl`

### 无 verify: 行的规则

视为技术债。应立即添加 verify 行——如果规则无法写出机器可检查的测试，说明规则太模糊，需要重写直到能写为止。

## 结构化执行（Hooks）

验证扫描从"指令说要做"升级为"结构性地让你很难跳过"：

| Hook | 触发时机 | 功能 |
|------|---------|------|
| SessionStart | 每次新会话启动 | 注入系统消息："读取 learned-rules.md 并运行验证扫描" |
| PreToolUse (Edit/Write) | 每次文件编辑前 | 提醒检查当前文件的路径作用域规则和已学规则 |
| Stop | 会话结束 | 提醒记录纠正和观察，写入会话评分卡 |

> 这是"指令说要做"和"系统结构性地让你很难跳过"之间的区别。

## Relationship to Verification Before Completion

验证扫描将 [[concepts/verification-before-completion]] 的理念从"完成声明需验证"泛化到"所有规则需验证"：

| 维度 | Verification Before Completion | 验证扫描 |
|------|-------------------------------|---------|
| 对象 | 单次任务的完成声明 | 所有已学规则 |
| 时机 | 任务完成前 | 每次会话启动 + 编辑前 |
| 方式 | 运行测试/构建 | 运行 grep/glob 检查 |
| 失败行为 | 不允许宣称完成 | 记录违规并报告 |

两者互补：验证扫描确保已积累的规则在每次会话中被自动检查，verification-before-completion 确保每次任务交付有验证证据。

## Relationship to Hooks as Safety Net

本概念将 [[concepts/hooks-as-safety-net]] 的定位从"轻量安全提醒（fail-open）"推进到"结构性执行机制"——hooks 不只提醒，而是确保验证循环不被跳过。

## Supporting Sources

- [[sources/self-evolving-claude-code]]

## Related Pages

- [[concepts/verification-before-completion]]
- [[concepts/hooks-as-safety-net]]
- [[concepts/rule-promotion-ladder]]
- [[concepts/self-evolving-agent-system]]
- [[concepts/reminders-vs-hard-enforcement]]

## Contradictions / Nuance

- 验证扫描假设 grep 检查足够覆盖规则合规性——行为类规则（如"不要顺手重构"、"保持最小改动"）无法被 grep 检查，只能写为 `verify: manual`，存在执行缺口。
- 规则数量增长时扫描性能如何——50 条规则 × grep 执行在大型仓库中可能引入明显启动延迟。
- hooks 的 fail-open 设计意味着如果 hook 脚本执行失败，验证扫描会被静默跳过——这与"结构性执行"的承诺存在张力。
