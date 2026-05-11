---
title: "Superpowers 深度实战指南：从入门到精通"
type: source
status: active
updated: 2026-05-11
source_count: 1
---

# Source: Superpowers 深度实战指南：从入门到精通

## Metadata

- Raw file: `raw/sources/superpowers-deep-practice-guide.md`
- Author: AgentBuff
- Date: 2026-05-08
- URL: https://mp.weixin.qq.com/s/BvrB7td8iJd4vNQW3T_UFg
- Publisher: 微信公众号

## Summary

- Superpowers 的全面参考文章，覆盖架构全景、8 个平台安装配置、14 个 skill 的深度解析、插件系统技术细节、完整 React Todo List 实战示例。
- 核心理念：代理不需要"被建议"怎么做，而是需要"被强制"怎么做——通过 HARD-GATE、Iron Law、Red Flags 三层防线实现。
- 技能系统（Skills System）是真正的主体，通过结构化 Markdown 文档与各平台 bootstrap 机制注入行为约束。
- 统一流程：会话启动/插件加载 → bootstrap 上下文注入 → 技能发现与按需加载 → 技能自动触发。

## Key Claims

- **using-superpowers 是所有平台共享的行为入口**；hook、插件 transform、context file 只是不同 harness 的装配层。三条路径：路径 A（Claude Code/Cursor/Copilot CLI 的 SessionStart hook）、路径 B（OpenCode 插件消息 transform）、路径 C（Gemini CLI 的上下文文件引用）。
- **技能文件以 `description` 优先描述触发条件**，而非概述工作流——让代理先命中技能，再读取正文执行。这一设计模式被称为"Claude 搜索优化"（CSO）。
- **"铁律"模式**：每个核心技能有一条不可违反的铁律（TDD: 没有先写失败测试就不能写生产代码；调试: 没有根因调查就不能提出修复方案；验证: 没有新鲜验证证据就不能声称完成）。
- **"合理化防范"机制**：每个技能包含 Red Flags 表 + Common Rationalizations 表 + Good/Bad 对比示例，预堵代理在压力下的合理化借口。
- **子代理驱动开发的核心设计**：每个任务分配全新子代理（隔离上下文、精确构造指令），完成后经两阶段审查（规格审查 + 代码质量审查），且默认连续执行整个计划不回头询问用户。
- **writing-plans 的任务粒度**：每个步骤 2-5 分钟的一个动作，禁止占位符（TBD、TODO、"类似 Task N"），必须重复完整代码。
- **"人的搭档"语言**：Superpowers 使用 "your human partner" 而非 "the user"，建立协作关系而非服务关系。
- **插件系统技术细节**：`run-hook.cmd` 是多语言脚本（Windows batch + Unix bash），Windows 找不到 bash 时静默退出 0（不崩但丢失注入能力）；版本管理通过 `scripts/bump-version.sh` + `.version-bump.json` 同步 6 个配置文件。
- **跨平台适配表**：Claude Code（插件 + SessionStart hook）、Codex CLI/App（同一插件包，App 额外读取 UI 元数据）、Cursor（插件 + Cursor hook）、OpenCode（Git 插件 + 消息 transform）、Gemini CLI（扩展清单 + GEMINI.md）、GitHub Copilot CLI（市场 + SDK 标准注入）、Factory Droid（市场安装入口）。

## Evidence Notes

- 文章提供了完整的目录结构（superpowers/ 根目录下的所有子目录和文件），可作为理解 Superpowers 仓库布局的权威参考。
- 每个技能的解析均包含触发条件、铁律、完整流程和常见合理化借口表，深度超过之前的来源。
- React Todo List 实战示例从会话启动到子代理执行展示了端到端流程，是之前来源中缺少的具体落地案例。
- 插件系统的技术细节（hook 脚本的跨平台实现、版本管理配置）是此前所有来源均未涉及的内容。

## Contradictions / Tensions

- 本文强调 **技能发现与按需加载** 是统一流程的关键步骤，而 [[sources/superpowers-workflow-deconstruction]] 的四层架构分类更偏向静态结构分析。两者视角互补，但对"默认加载哪些技能"这一实际问题的建议略有张力。
- 本文将 brainstorming 的视觉伴侣（Visual companion）描述为可选功能，需征得用户同意；但整体流程中 brainstorming 本身是强制 HARD-GATE——"在呈现设计并获得用户批准之前，不得调用任何实现技能"。这与 [[sources/ai-coding-advanced-openspec-superpowers-deep-guide]] 中 `/opsx:ff` 快速入门路径存在张力：快速入门是否绕过了 brainstorming 的硬门控？
- writing-plans 要求"假设执行者是一个有技能但零上下文、品味存疑、不愿测试的热心初级工程师"——这种防御性设计与 [[sources/ai-template2-scaffold]] 中 harness 的信任模型（将 TDD 作为可配置硬门禁）存在风格差异。

## Linked Entities

- [[entities/superpowers]]
- [[entities/claude-code]]

## Linked Concepts

- [[concepts/spec-driven-workflow-and-review-discipline]]
- [[concepts/tdd-as-hard-gate]]
- [[concepts/verification-before-completion]]
- [[concepts/specialized-agent-pattern]]
- [[concepts/hooks-as-safety-net]]
- [[concepts/bad-case-driven-iteration]]

## Follow-up Questions

- "使用 Superpowers 的深度实践建议"中提到的技能词数限制（using-superpowers <150 词，频繁引用 <200 词，其他 <500 词）在实际仓库中是否被严格遵守？
- 8 个平台的安装方式是否全部经过验证，还是部分为声明性支持？特别关注 Factory Droid 和 GitHub Copilot CLI 的成熟度。
- Codex App 与 Codex CLI 共享插件包但 App 额外读取 `interface` 字段——这一分叉是否会导致 CLI 用户遗漏 UI 提示？
- brainstorming 的"视觉伴侣"功能的实际使用率和用户接受度如何？
- `run-hook.cmd` 在 Windows 找不到 bash 时静默退出——这是否应该改为警告而非静默失败？
