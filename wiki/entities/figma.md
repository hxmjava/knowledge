---
title: Figma
type: entity
status: active
updated: 2026-05-09
source_count: 1
---

# Entity: Figma

## What It Is

Figma 是一个基于浏览器的协作设计平台，涵盖 UI/UX 设计（Figma Design）、原型交互（Dev Mode）、白板（FigJam）、演示文稿（Figma Slides）、矢量绘图（Figma Draw）、网站发布（Figma Sites）和 AI 编码（Figma Make）等产品线。

## Relevance

Figma 通过 API 和个人访问令牌（PAT）为第三方集成提供数据访问能力，在设计-to-code 管道中是关键的上游数据源。其令牌安全模型（全量访问、不可恢复一次性展示）是理解 AI 编码工具链中权限治理的一个参考案例。

## Key Facts

- 产品线：Figma Design、Dev Mode、FigJam、Figma Slides、Figma Draw、Figma Buzz (Beta)、Figma Sites (Beta)、Figma Make
- API 访问通过个人访问令牌（PAT）实现，令牌粒度为"全有或全无"
- 支持 MCP server 集成，可接入 AI 编码工作流
- 令牌仅在生成时显示一次，丢失后需重新生成

## Relationships

- 相关概念：[[concepts/policy-driven-tool-permissions]]
- 相关实体：[[entities/claude-code]]（Figma MCP server 可作为 Claude Code 的外部工具）

## Evidence

- [[sources/figma-personal-access-tokens]]

## Open Questions

- Figma PAT 是否支持更细粒度的 scope（如只读、仅限特定团队）？
- Figma 官方 MCP server 的成熟度和安全模型。
- 设计 token 系统与 AI 编码工具链的集成模式。
