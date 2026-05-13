---
title: "如何构建一个好的 AGENTS.md：AI 编码 Agent 的项目级行为规范最佳实践"
source: "https://mp.weixin.qq.com/s/RxRCmsc3ehIuqV_DwG-Kog"
author:
  - "[[米奥]]"
published:
created: 2026-05-12
description: "在 AI 辅助编程从「Vibe Coding」走向工程化实践的今天，AGENTS.md 已成为 Cursor、Codex、Claude Code 等主流 AI 编码工具的事实标准项目指令文件。"
tags:
  - "clippings"
---
米奥 *2026年5月9日 08:14*

## 摘要

最近在用 Cursor 和 Codex 写代码的时候，我越来越发现一个问题：每次新开会话，AI 都要重新问一遍项目结构、用什么包管理器、代码该放哪层。久而久之就觉得烦。

`AGENTS.md` 就是用来解决这个问题的。它本质上就是给 AI 准备的「项目说明书」，放在仓库根目录，告诉 Agent 在这个项目里应该怎么做事。

本文结合了 Benjamin Crozat、Eric 技术圈等人的实际经验，以及 Cursor 官方的文档，整理了以下几点：

- 为什么需要 AGENTS.md，它到底能带来什么好处
- 推荐的 C.A.R.S 结构怎么写
- 项目大了之后，如何把 AGENTS.md 做成「索引」而不是把所有知识全塞进去
- 跨工具怎么共用，以及日常维护的坑

希望看完之后，你的项目里也能少一些「AI 又犯傻了」的情况。

---

## 1\. 什么是 AGENTS.md，为什么它如此重要

`AGENTS.md` 是一个放置在项目根目录的纯 Markdown 文件，专门用于指导 AI 编码 Agent 的行为。

与传统的 `README.md` （面向人类开发者）不同， `AGENTS.md` 的受众是 AI：

- 它告诉 Agent「 **在这个项目里，到底应该如何** 执行任务」
- 它提供 **可执行的具体命令** 、 **精确到补丁版本的技术栈** 、 **明确的约束边界**
- 它减少 Agent 的「上下文幻觉」和「默认假设错误」

为什么需要它？

在 Vibe Coding 初期，开发者往往通过长对话式 Prompt 指导 AI。但当项目规模扩大、团队多成员协作、或需要在 Cursor ↔ Codex ↔ Claude Code 之间切换时，问题会集中爆发：

- AI 反复使用错误的包管理器（ `npm` vs `pnpm` ）
- 生成的代码被放在错误目录，或完全不符合现有架构分层
- 每次开启新会话都要从零重复解释项目规范
- 低级错误（如 JavaScript 浮点精度、未加保护的删除操作）被忽略，最终引发生产事故

`AGENTS.md` 的本质是 **AI 的项目级行为约束文件** ，而非一次性提示词集合。它把「团队共识」固化下来，让 AI 成为真正「懂项目」的成员。

---

## 2\. 为什么大家都在用 AGENTS.md

我见过不少人用了一段时间 Cursor 之后，都会遇到类似的问题：

- AI 老是跑 `npm install` ，但项目明明用的是 pnpm
- 生成的代码经常放错目录，完全不按现有的 DDD 分层走
- 每次换个新模型，或者新同事用同一套规则，又得重新讲一遍

一份写得好的 `AGENTS.md` 能明显改善这些情况：

- **命令更靠谱** ：明确写「只用 pnpm」，基本能杜绝 90% 以上的包管理器错误。
- **代码位置更对** ：告诉它「领域逻辑放 domain 层，查询放 queries」，AI 就不容易瞎放。
- **新会话成本低** ：不用每次都从头解释项目规范，新人或者新模型都能快速上手。
- **安全一点** ：可以加一些硬约束，比如「没问我之前不要删代码」「不要恢复被删的内容」。
- **多工具统一** ：Cursor、Codex、Claude Code 都能读同一份文件，规则不漂移。

最重要的是，它把「我个人觉得这样写比较好」变成了「团队约定必须这么做」。

---

## 3\. 推荐的 C.A.R.S 结构

我自己写 AGENTS.md 的时候，基本都按 **C.A.R.S** 这个框架来组织，效果还不错。

### 3.1 Commands（开发命令）

这一部分最实用，也最容易被忽略。

不要写「请使用合适的包管理器」，而要直接写死：

```
- Dev: \`pnpm dev\`
- Format: \`pnpm format\`
- Lint + Typecheck: \`pnpm lint && pnpm typecheck\`
- Test: \`pnpm test --parallel\`
- Build: \`pnpm build\`
```

AI 默认喜欢用 npm，尤其是新模型。明确写死之后，这类低级错误会少非常多。

### 3.2 Architecture（架构与目录）

这里要写得具体一点。

不要只写「使用 Next.js」，而是写「Next.js 15.3 + TypeScript 5.7 + Prisma 5.20」。

最好再加一个带注释的目录结构，告诉 AI 每个文件夹是干什么的，尤其是 DDD 分层这种比较绕的架构。

### 3.3 Restrictions（约束与禁忌）

这一节我认为是整个 AGENTS.md 里最有价值的部分。

「不能做什么」比「应该做什么」更能防止大问题。常见的写法包括：

- 微信小程序端严禁执行 npm/pnpm 命令
- 所有金额计算必须用 decimal.js
- 没问我之前不要删代码，也不要恢复被删的内容
- 提交前必须跑 lint + typecheck + test

### 3.4 Standards（流程规范）

放一些日常协作的习惯：

- 提交信息用 Conventional Commits
- PR 前必须跑完整检查
- 改完 Markdown 文章后要跑同步脚本
- 本地开发默认访问 http://localhost:3000

这些东西看起来琐碎，但 AI 真的会照着做。

---

## 4\. 实战示例：一个紧凑而完整的 AGENTS.md 模板

以下模板改编自 Benjamin Crozat 的实战仓库，并融合 C.A.R.S 模型，可直接用于大多数现代 Web 项目：

```
# Project Agent Instructions

## Commands
- Dev: \`pnpm dev\`
- Format: \`pnpm format\`
- Lint: \`pnpm lint\`
- Typecheck: \`pnpm typecheck\`
- Test: \`pnpm test --parallel\`
- Build: \`pnpm build\`
- Content sync: \`pnpm sync-posts\`

## Architecture
- Stack: Next.js 15.3, TypeScript 5.7, Tailwind 4.0, Prisma 5.20, tRPC
- Use App Router + React Server Components + Server Actions
- Domain logic lives in \`lib/domain\`
- Follow DDD + CQRS: Commands in \`commands/\`, Queries in \`queries/\`

## Restrictions
- NEVER run \`npm\` commands — always use \`pnpm\`
- Do not use \`any\` in TypeScript unless explicitly justified and documented
- Never overwrite user edits or restore deleted code without explicit confirmation
- WeChat Mini Program code: do not execute npm/pnpm at all
- JS number calculations must use \`decimal.js\` or native \`BigInt\`

## Standards
- Commit messages follow Conventional Commits
- Always run full \`lint + typecheck + test\` before suggesting a PR or merge
- For Markdown post edits in \`content/posts\`, run \`pnpm sync-posts\` afterwards
- Assume local dev server runs at http://localhost:3000 unless otherwise stated
- Verify any version-specific or vendor-specific claims in official documentation

## Verification
- When uncertain about external APIs, framework behavior, or version details, browse official docs instead of guessing
```

这份模板通常只有 30-40 行，却能覆盖日常 90% 以上的 Agent 交互场景。

---

## 5\. 跨工具兼容与集成策略

不同工具对指令文件的支持情况（2026 年 5 月最新）：

| 工具 | 支持文件 | 推荐集成方式 |
| --- | --- | --- |
| Cursor | `AGENTS.md` + `.cursor/rules/*.mdc` | 根目录放 `AGENTS.md` ，细粒度规则放 `.cursor/rules` |
| Codex | `AGENTS.md` （支持多层级） | repo-root + `~/.codex/AGENTS.md` 全局 |
| Claude Code | `CLAUDE.md` | 创建符号链接 `ln -s AGENTS.md CLAUDE.md` |
| 其他工具 | 视情况 | 以 `AGENTS.md` 为单一事实来源 |

**最佳实践** ：把 `AGENTS.md` 作为「单一事实来源」，其他工具通过符号链接或引用共享，避免多套文档漂移。

---

## 6\. 编写与维护的最佳实践

**保持简短可维护**

目标控制在 200-400 行。过长会导致 AI 遵守率下降。

**演进式更新，而非一次性编写**

发现 AI 反复犯同一个错误 → 立即补充对应规则。

**精确到版本，而非泛泛而谈**

写「Java 21 + Spring Boot 3.5.4」而不是「Java + Spring Boot」。

**每条规则最好可验证**

能对应一个可运行命令或自动化检查点。

**与代码一起 Review**

定期 review `AGENTS.md` ，删除过时规则。

1. **分层设计**

项目级通用规则 → `AGENTS.md` 细粒度、条件触发规则 → `.cursor/rules/*.mdc` 可复用技能/工作流 → Skills / Hooks

---

## 7\. 常见陷阱与避免方法

- **把 AGENTS.md 变成「通用编程建议」dump 地**

→ 只保留项目特定内容，通用最佳实践交给模型本身。

- **长期不更新导致规则过时**

→ 建立「任何规则修改必须伴随代码 review」的流程。

- **规则之间互相矛盾**

→ 定期梳理，保持一致性。

- **把复杂工作流全部塞进 AGENTS.md**

→ 复杂流程交给专用 Skills 或子 Agent 承载。

---

## 8\. 项目大了之后：把 AGENTS.md 做成索引而不是百科全书

写到后面我发现一个问题：AGENTS.md 越来越长，规则越来越多，最后 AI 反而开始「挑着读」，或者干脆忽略了。

后面我看了 OpenAI Harness 团队和一些重度用户（比如 Sagar Mandal）的做法，发现一个更可持续的模式： **把 AGENTS.md 做成「目录索引」** ，而不是把所有知识全塞进去。

### 推荐的目录结构

```
project-root/
├── AGENTS.md          # 只放概览 + 关键指针 + 硬约束（目标 100~120 行）
├── docs/
│   ├── README.md      # 所有文档的总索引
│   ├── adr/           # 架构决策记录
│   ├── conventions/   # 编码规范
│   ├── workflows/     # 常用操作流程
│   ├── patterns/      # 设计模式
│   └── gotchas.md     # 常见坑
```

### 为什么这么做更好？

- AGENTS.md 保持简短，AI 读起来没那么累。
- 知识可以版本化管理，和代码一起 review。
- Agent 需要的时候再去读具体文档，而不是一开始就把所有内容都塞进上下文。
- 多人协作的时候，大家都知道该去哪个文件夹找规范。

小项目其实没必要这么折腾，单文件 + `.cursor/rules/` 就够了。但当你发现 AGENTS.md 已经超过 300 行、经常有人抱怨「又过时了」的时候，就可以考虑切成这种结构了。

---

## 结语

写 AGENTS.md 这件事，说大不大，说小也不小。

它其实就是在回答一个问题： **我们希望 AI 在这个项目里，以什么样的方式工作？**

把这个答案写下来、维护好，比每次都临时想提示词要省事得多。

我自己的经验是，先从 Commands 和 Restrictions 两部分开始写最实用。后面再慢慢补 Architecture 和知识索引。

等你项目里真的用起来之后，再回来看这篇文章，可能会有不一样的

---

**参考与延伸阅读**

- Benjamin Crozat：《How to use AGENTS.md with Codex, Cursor, and Claude Code》
- Eric 技术圈：《一套可落地的企业级 AGENTS.md 项目规则实践》
- Cursor 官方：《使用智能体编码的最佳实践》
- Cursor 文档：Rules、Commands、Agent Workflows

---

AI技术学习 · 目录

继续滑动看下一个

肥喵学AI

向上滑动看下一个