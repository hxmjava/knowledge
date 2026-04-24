---
title: OpenSpec
type: entity
status: active
updated: 2026-04-24
source_count: 1
---

# Entity: OpenSpec

## What It Is

OpenSpec 是一个规格驱动开发框架：先把"做什么"写清楚，再让实现团队按已定规范执行。核心原则是 **Agree before you build**——人类与 AI 在写代码前对规格达成一致，用文档把需求"定死"，减少 AI 自由发挥导致的跑偏与遗漏。

## Relevance

它在本文中承担"规范真相来源"角色，负责把需求、设计、任务和增量变更钩住为可审计链条。与 Superpowers 组合时，OpenSpec 定方向，Superpowers 定计划与纪律。

## Key Facts

- 采用 `openspec/` 分层目录：
  ```
  openspec/
  ├── specs/                 # 当前规范的「真相来源」（类比 main）
  │   └── <capability>/
  │       └── spec.md
  └── changes/               # 提议 / 进行中 / 已归档的变更（类比 feature 分支）
      └── <change-name>/
          ├── proposal.md    # 为什么改、改什么
          ├── tasks.md       # 实施检查清单
          └── specs/         # 对规范的增量「补丁」
  ```
- 变更先进入 `changes/`，成功合并并归档后再反映到 `specs/`，减少"口头改需求、代码偷偷改规范"。
- 核心命令：`/opsx:explore`（探索）→ `/opsx:propose`（提案）→ `/opsx:apply`（实施）→ `/opsx:archive`（归档）。
- 扩展命令（如 verify）需切到 custom profile 并 `openspec update`。
- 安装：`npm install -g @fission-ai/openspec@latest` → `openspec init`。
- GitHub: https://github.com/Fission-AI/OpenSpec

## Relationships

- Related entities: [[entities/superpowers]], [[entities/claude-code]]
- Related concepts: [[concepts/spec-driven-workflow-and-review-discipline]], [[concepts/team-governance-for-ai-coding]], [[concepts/schema-driven-maintenance]]

## Evidence

- [[sources/openspec-superpowers-practice-guide]]

## Open Questions

- 对于小规模 bugfix，`changes/` 体系应如何最小化执行步骤？
- 团队是否规定了 custom profile 下扩展命令的启用策略？
