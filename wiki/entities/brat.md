---
title: BRAT
type: entity
status: active
updated: 2026-05-06
source_count: 1
---

# Entity: BRAT

## What It Is

BRAT（Beta Reviewer's Auto-update Tool）是 Obsidian 的社区插件，用于安装和管理尚未正式上架社区插件市场的测试版插件。用户只需填写 GitHub 仓库地址，BRAT 便自动拉取、安装并启用目标插件。

## Relevance

BRAT 是许多新 Obsidian 插件的分发桥梁。对于尚未通过社区市场审核的插件（如 Claudian），BRAT 是目前主要的安装渠道。了解 BRAT 有助于跟踪 Obsidian 插件生态的早期采用动态。

## Key Facts

- 全称：Beta Reviewer's Auto-update Tool。
- 本身已上架 Obsidian 社区市场，可直接搜索安装。
- 安装测试版插件的流程：设置 → BRAT → Add a beta plugin for testing → 填入 GitHub 仓库地址 → 回车。
- 也可通过命令面板（Ctrl+P / Cmd+P）输入 BRAT 触发。
- 自动处理拉取和启用，无需手动下载 zip。

## Relationships

- Related entities: [[entities/obsidian]], [[entities/claudian]]

## Evidence

- [[sources/claudian-obsidian-plugin]]

## Open Questions

- BRAT 安装的插件是否自动接收更新推送？更新策略如何？
- 安全模型：BRAT 安装的 beta 插件是否经过任何安全审查？
