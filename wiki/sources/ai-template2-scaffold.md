---
title: ai_template2 Multi-Module AI Collaboration Scaffold
type: source
status: active
updated: 2026-04-24
source_count: 1
---

# Source: ai_template2 多模块项目 AI 协作脚手架

## Metadata

- Raw file: `raw/sources/ai-template2-scaffold.md`
- Origin: `D:/Users/Administrator/Desktop/AI/ai_template2`
- Scope: 多模块项目 AI 协作脚手架模板，整合 OpenSpec / Superpowers / Claude Code Harness

## Summary

- ai_template2 是一个面向多模块 Java 项目的 AI 协作脚手架，将 OpenSpec（规范层）、Superpowers（纪律层）和 Claude Code Harness（协作层）整合为可落地工程实践。
- 使用 `{{LAYER_COMMON}}`、`{{LAYER_SERVICE}}`、`{{LAYER_APP}}`、`{{LAYER_MESSAGE}}` 占位符适配具体项目，依赖方向固定为 `app → service → common`。
- 提供 9 个 Claude Code 斜杠命令：日常开发(`/proj-dev`)、模块定位、变更实现(绑定 TDD 铁律)、规格同步、验证收口、风险评审、完成评审、新人上手、测试基建。
- 提供 4 个分层 Agent（app/common/service/message）和 6 个专项检查技能（API/ORM/XML/Message Consumer/Build Verifier/Test Bootstrap）。
- 提供 4 个生命周期 Hooks（PreToolUse/PostToolUse/PostToolUseFailure/Stop），默认 fail-open，做轻量提醒不阻断。
- TDD 铁律：所有生产代码必须由失败测试驱动；无测试基建时自动切换到 test-bootstrap 搭骨架；豁免需显式确认。
- Cursor 侧配套 14 个 Superpowers 命令、4 个 OpenSpec 技能、3 个 AI 上下文文档、9 个提示词模板。

## Key Claims

- 「实现完成」≠「变更完成」：与 OpenSpec 绑定的任务需走规格验收与归档。
- 分层协作：不同业务域无共享表/实体耦合时可并行；触及 common 层应串行。
- 高风险区域变更必须写明执行的构建命令及成功/失败摘要。
- 连续验证失败、依赖不清、跨模块影响过大时，先停下升级讨论。
- 不要让 Superpowers 替代 OpenSpec 定义需求；不要让 `.claude` 命令另起一套需求标准。

## Claude Code 命令体系

| 命令 | 核心职责 |
|------|---------|
| `/proj-dev` | 日常开发编排器：定位层→选路径→暴露风险→同步规格→验证→终审 |
| `/proj-change-apply` | OpenSpec 变更实现，强制 TDD Red-Green-Refactor |
| `/proj-spec-sync` | 实现偏离时同步 proposal/design/tasks/spec |
| `/proj-verify` | 推荐或执行最小足够验证命令 |
| `/proj-review-risk` | 高风险路径专项审查 |
| `/proj-review-complete` | 完成评审终验门 |
| `/proj-test-bootstrap` | 无测试模块的最小测试基建搭建 |
| `/proj-module-locate` | 改动所属层与模块判断 |
| `/proj-onboard` | 新人场景化入口推荐 |

## 专项检查技能

| 技能 | 检查维度 |
|------|---------|
| api-change-checker | 接口签名、DTO 契约、下游调用者、RPC 配置、运行期兼容性 |
| orm-change-checker | entity→mapper→XML 一致性链、共享模型影响、SQL 运行时风险 |
| xml-config-checker | DI 接线、RPC 暴露/引用、ORM 扫描、日志/打包、启动安全 |
| message-consumer-checker | 重试语义、幂等性、异常处理、排序语义、下游副作用 |
| build-module-verifier | 最小足够验证命令选择、升级触发条件、验证差距声明 |
| test-bootstrap | 测试框架基线对齐、目录结构、冒烟测试、验证基建可用 |

## TDD 执行要求

1. **RED** — 写最小失败测试，确认因功能缺失而失败（非编译错误）
2. **GREEN** — 写最少生产代码使测试通过，不扩写多余逻辑
3. **REFACTOR** — 全绿状态整理命名/抽取方法/消除重复，再次确认全绿
4. 严禁一次性批量生成生产代码再补测试
5. 模块无测试基建 → 切换 test-bootstrap 搭骨架 → 回到 RED
6. TDD 豁免需显式征得用户确认，并在完成输出中记录原因

## Contradictions / Tensions

- 模板强调 TDD 铁律，但允许豁免（纯配置/一次性脚本/生成代码/无法搭建测试基建的历史模块）——豁免边界依赖团队自觉。
- 提供 9 个命令 + 6 个技能 + 4 个 Agent，对小型项目可能过重——脚手架本身是占位模板，实际项目可按需裁剪。
- Hooks 默认 fail-open 不阻断，在安全要求高的场景可能需要改为 fail-closed。

## Linked Entities

- [[entities/openspec]]
- [[entities/superpowers]]
- [[entities/claude-code]]
- [[entities/harness]]

## Linked Concepts

- [[concepts/spec-driven-workflow-and-review-discipline]]
- [[concepts/team-governance-for-ai-coding]]
- [[concepts/layered-project-harness]]
- [[concepts/tdd-as-hard-gate]]
- [[concepts/specialized-agent-pattern]]
- [[concepts/hooks-as-safety-net]]
