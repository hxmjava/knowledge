---
title: CC Switch
type: entity
status: active
updated: 2026-05-06
source_count: 1
url: https://github.com/farion1231/cc-switch
homepage: https://www.ccswitch.io
language: Rust / TypeScript
framework: Tauri 2 + React
license: MIT
stars: 60596
---

# Entity: CC Switch

## What It Is

CC Switch 是一款跨平台桌面 All-in-One 管理工具，为 [[entities/claude-code]]、Codex、Gemini CLI、OpenCode 和 OpenClaw 提供统一的 Provider 切换、MCP 管理、Prompts 管理、Skills 管理与会话浏览能力。基于 Tauri 2（Rust 后端）+ React（TypeScript 前端）构建，支持 Windows、macOS 和 Linux。

## Relevance

CC Switch 将多个 AI 编码 CLI 工具的配置管理统一到一个 GUI 中，降低了多工具、多 Provider 场景下的切换成本与配置出错风险。它体现了"AI 工具运维层"这一新兴需求——在 Agent 能力之上叠加可控的配置编排与运行时管理。

## Key Facts

- **Provider 管理**：支持预设与自定义 Provider 配置，一键切换，支持 Shared Config 在 Provider 间传递公共数据（插件、MCP 等）。
- **MCP 管理**：通过模板或自定义配置添加 MCP Server，可按应用粒度开关同步。
- **Prompts 管理**：内置 Markdown 编辑器创建预设，激活后自动同步到对应工具的 Prompt 文件。
- **Skills 管理**：浏览 GitHub 仓库中的 Skills，一键安装到所有支持的应用。
- **Sessions 浏览**：跨应用浏览、搜索和恢复会话历史。
- **本地代理**：支持本地 Proxy 模式，热切换，格式自动转换。
- **数据存储**：SQLite 单一数据源（`~/.cc-switch/cc-switch.db`），JSON 设备级设置，自动备份轮转（保留最近 10 份）。
- **架构模式**：分层架构（Commands → Services → DAO → Database），原子写入，互斥锁并发安全。
- **Claude Code 热切换**：切换 Provider 后无需重启终端即可生效（其他 CLI 工具需重启）。
- **跨平台**：Windows（MSI / 便携版）、macOS（Homebrew / DMG，已 Apple 公证）、Linux（deb / rpm / AppImage / AUR）。
- Stars 超过 60K，社区活跃度极高。

## Relationships

- Related entities: [[entities/claude-code]], [[entities/llm-agent]]
- Related concepts: [[concepts/context-and-cost-optimization]], [[concepts/team-governance-for-ai-coding]]

## Evidence

- [GitHub Repository](https://github.com/farion1231/cc-switch)
- [Official Website](https://www.ccswitch.io)

## Open Questions

- 与企业级部署场景的兼容性（如内网离线环境、SSO 集成）。
- Skills 生态的治理机制——如何确保社区 Skill 的安全性与质量。
- 多人团队共享 Provider 配置的协作方案。
