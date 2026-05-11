---
title: Manage Personal Access Tokens (Figma)
type: source
status: active
updated: 2026-05-09
source_count: 1
---

# Source: Manage Personal Access Tokens (Figma)

## Metadata

- Raw file: `raw/sources/figma-personal-access-tokens.md`
- Author: Figma Help Center
- Date: 持续更新的官方文档
- URL: https://help.figma.com/hc/en-us/articles/8085703771159-Manage-personal-access-tokens
- Publisher: Figma

## Summary

- Figma 个人访问令牌（PAT）用于授权第三方集成和插件通过 API 访问用户数据。
- 每个令牌仅对应一个集成，需为不同集成分别生成。
- 令牌授予的是**全量数据访问权限**——无法限制范围，这是与 OAuth scope 模型的关键差异。
- 生成后令牌仅显示一次，离开页面即不可再查看，需重新生成。
- 可随时撤销令牌以切断第三方访问。

## Key Claims

- PAT 的粒度是"全有或全无"：无法限制到特定文件或团队，安全边界依赖用户信任判断。
- 令牌是不可恢复的一次性展示，丢失后只能重新生成——这是业界常见的安全设计模式。
- 撤销令牌后，第三方集成立即失去 API 访问能力，但需手动重新配置才能恢复。

## Evidence Notes

- 文档明确警告"All of your files and data"，说明这是全权限令牌而非细粒度令牌。
- 令牌支持 scope 赋值（"assign the scopes you want"），但文档未展开 scope 列表，指向 developer docs。

## Contradictions / Tensions

- 文档声称"assign the scopes you want"暗示存在作用域，但同时又说"access all of your files"——这两处表述存在张力。可能 scope 控制的是 API 操作类型（读/写），而非数据范围。

## Linked Entities

- [[entities/figma]]

## Linked Concepts

- [[concepts/policy-driven-tool-permissions]]

## Follow-up Questions

- Figma PAT 的 scope 具体有哪些级别？是否支持只读令牌？
- Figma 是否支持 OAuth App 作为 PAT 的替代方案，提供更细粒度的授权？
- 在设计-to-code 的 CI/CD 管道中，Figma PAT 的最佳实践是什么（如用于 Figma MCP server）？
