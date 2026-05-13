---
title: Obsidian Project Symlink
type: concept
status: active
updated: 2026-05-11
source_count: 1
---

# Concept: Obsidian 软链接管理项目文档

## 定义

通过 Windows 符号链接（symlink）将项目仓库目录映射到 Obsidian vault 中，实现**一套文件、两处管理**：Obsidian 负责知识库浏览与双向链接，Cursor / Claude Code 等编辑器负责开发，无需手动同步。

## 为什么重要

- 消除文档双写：同一份 MD 文件既在 IDE 中引用，又在 Obsidian 中作为知识图谱节点存在。
- 利用 Obsidian 的双向链接、标签和图谱可视化，增强项目文档的可导航性。
- 降低上下文切换成本：在 Obsidian 中浏览项目文档时，可以直接使用 wiki 级链接和搜索。

## 核心操作

```powershell
New-Item -ItemType SymbolicLink `
  -Path "F:\obsidian\mall" `
  -Target "F:\claude\mall\project\dlabel-cloud-mall-platform"
```

| 位置 | 用途 |
|------|------|
| `F:\obsidian\mall\` | Obsidian 中以知识库形式浏览、编辑、链接项目文档 |
| `F:\claude\mall\project\...` | Cursor / Claude Code 等编辑器中正常开发 |

## 适用场景

- 项目文档（`docs/`、`openspec/`、AGENTS.md、CLAUDE.md）需要长期维护和交叉引用。
- 团队希望用 Obsidian 图谱可视化项目文档之间的引用关系。
- 需要将项目上下文（如 `project-structure.md`、`architecture.md`）同时提供给 AI 编码工具和人工查阅。

## 注意事项

- 软链接在 Windows 上需要管理员权限或启用开发者模式。
- Obsidian 中编辑的文件会直接反映到项目目录（因为指向同一文件），需注意 Obsidian 自动格式化与 IDE 格式化规则的冲突。
- 大型项目目录（含 `node_modules`、构建产物）不宜整体 symlink，建议只映射文档子目录。

## Supporting Sources

- [[sources/openspec-superpowers-practice-guide]]

## Related Pages

- [[entities/obsidian]]
- [[concepts/vault-native-ai-assistant]]
- [[concepts/spec-driven-workflow-and-review-discipline]]
