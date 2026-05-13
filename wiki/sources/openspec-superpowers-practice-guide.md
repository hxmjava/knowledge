---
title: OpenSpec + Superpowers 规范开发指南
type: source
status: active
updated: 2026-05-11
source_count: 1
---

# Source: OpenSpec + Superpowers 规范开发指南

## Metadata

- Raw file: `raw/sources/OpenSpec + Superpowers规范开发指南.md`
- Scope: 规范开发方法、团队工作流、质量流程与交付治理

## Summary

- 提出"OpenSpec + Superpowers"协作方式：前者负责规格定义与变更归档，后者负责执行纪律与工程流程。二者不是互斥替代，而是"先对齐规范 → 再按流程执行"。
- OpenSpec 采用 `openspec/` 分层目录：`specs/` 为规范真相来源，`changes/` 为变更提案与任务，`archive/` 归档已完成变更。改行为先走 `changes/`，合并/归档后再反映到 `specs/`。
- Superpowers 是强制性工作流与可组合技能集合，内置七步流程：brainstorming → using-git-worktrees → writing-plans → subagent-driven-development → test-driven-development → requesting-code-review → finishing-a-development-branch。
- 生产级功能推荐五阶段流水线：提案(OpenSpec) → 纠偏(Superpowers Plan) → 实现(Superpowers) → 验证(测试/CI) → 归档(OpenSpec)。
- 按任务规模分级：核心业务/长期维护模块走完整流程；多人协作需对外说明走 OpenSpec；生产级迭代二者协同；极小 bugfix 用原生 Agent 最小流程。
- 实战案例以 dlabel-cloud-mall-platform 商城二期自定义活动开发为例，展示了目录布局、规格设计、问题诊断与改进动作。
- 工程化目录详解覆盖 `docs/`、`openspec/`（含 TDD-driven schema 配置）、`plugins/`、`.cursor/`、`.claude/`、`.agents/` 六个层级，含具体命令、技能和 hooks 配置。
- 补充了 7 条 AI 编码使用技巧（提示词写法、上下文管理、示例驱动等）和 3 种 Context 不够用的解决方案（Claude-Mem 自动记忆、会话总结注入、永久归档追溯）。
- 介绍了 Obsidian 软链接（symlink）模式：一套文件同时在 Obsidian 知识库和 Cursor/Claude Code 中管理，避免手动同步。

## Key Claims

- 先对齐规范再编码可以显著降低偏航和返工；变更先在 `openspec/changes/` 落地，归档后再回写规格主线。
- 团队化 AI 开发应"硬化工作流"，至少在关键模块上要求规划、TDD、评审与归档。
- 复杂任务不应只写计划：任务要绑定可验证证据（命令日志、接口返回、截图等）。
- OpenSpec 与 Superpowers 不是互斥关系，而是"规范主导 + 纪律执行"的组合：适合生产级或长期维护模块。
- `tasks.md` 可能是初稿；执行中允许由 Plan/评审调整为更合理的 Wave/依赖，但变更要有记录。
- 文档分散（`docs/`、`openspec/`、`.cursor/doc/ai-context/`）存在版本漂移风险，需规定单一事实源（SSOT）。

## OpenSpec 核心工作流

| 命令 | 作用 | 何时用 |
|------|------|--------|
| `/opsx:explore` | 只讨论、不强制产出正式文档 | 需求/方案还不清 |
| `/opsx:propose` | 一次性生成规划类产物 | 方向清楚，要开变更 |
| `/opsx:apply` | 按 `tasks.md` 逐项落地代码 | 规划已冻结，开始实现 |
| `/opsx:archive` | 归档已完成变更 | 实现结束，规范要合回主线认知 |

**检查清单**：

- [ ] 本次改动是否在 `openspec/changes/<name>/` 下有 `proposal.md` + `tasks.md`（以及必要的 spec 增量）？
- [ ] `tasks.md` 是否可被逐条勾掉，且与评审结论一致？
- [ ] 完成后是否执行归档，避免"代码已合并、规范仍停留在旧版"？

## Superpowers 内置流程

| 顺序 | 技能 | 目的 |
|------|------|------|
| 1 | brainstorming | 需求澄清（苏格拉底式提问） |
| 2 | using-git-worktrees | 隔离工作区 |
| 3 | writing-plans | 拆成可执行的小步任务 |
| 4 | subagent-driven-development | 子代理执行 + 审查 |
| 5 | test-driven-development | 强制 TDD（RED → GREEN → REFACTOR） |
| 6 | requesting-code-review | 代码审查，关键问题可阻塞 |
| 7 | finishing-a-development-branch | 收尾与合并选项 |

**检查清单**：

- [ ] 是否先有计划/任务拆分再大规模改代码？
- [ ] 是否对关键路径执行 TDD 或等效的可自动化验证？
- [ ] 是否经过代码审查环节（人工或规范化 checklist）？

## 五阶段流水线

| 阶段 | 主导 | 产出/动作 |
|------|------|-----------|
| 1. 提案 | OpenSpec | `proposal` / `design` / 规范增量 / `tasks.md` |
| 2. 纠偏 | Superpowers（Plan） | 技术栈或约束与初稿不一致时，重写任务分层与依赖（如 Wave 并行批次） |
| 3. 实现 | Superpowers | 子任务并行；工具层读写、诊断、跑测 |
| 4. 验证 | 测试与 CI | 单测/集成测、本地与流水线一致 |
| 5. 归档 | OpenSpec | `/opsx:archive`，规范与实现可追溯 |

## 场景决策表

| 场景 | 推荐 | 原因 |
|------|------|------|
| 核心业务、长期维护模块 | Superpowers（+ 测试/评审） | 质量与可维护性 |
| 多人协作、需对外/对内说明 | OpenSpec | 规范统一、可归档追溯 |
| 生产级功能迭代 | 二者协同 | 规范 + 纪律 |
| 极小范围 bugfix | 原生 Agent / 最小流程 | 避免流程成本大于收益 |

## FAQ 摘要

- **`/opsx:verify` 等命令不存在？** OpenSpec 1.0 默认可能仅启用 explore/propose/apply/archive；扩展能力需切到 custom profile 并 `openspec update` 后重启。
- **`tasks.md` 和实际开发任务不一致？** 可接受；以评审通过的执行计划为准，但应保留"为何调整"的痕迹，归档时说明规范与实现的对应关系。
- **两个都必须装吗？** 否。简单任务原生即可；要规范加 OpenSpec；要质量加 Superpowers；生产级常组合使用。
- **二者是否硬依赖？** 无硬依赖；组合使用效果更好：OpenSpec 定方向，Superpowers 定计划与纪律。

## 实战案例：dlabel-cloud-mall-platform 商城二期

### 仓库目录布局

```
dlabel-cloud-mall-platform/
├── pom.xml                          # 父 POM，统一依赖与模块
├── src/                             # 源码目录
├── docs/                            # 文档（团队指南、方案与规格）
├── openspec/                        # OpenSpec 配置与规格目录
├── plugins/                         # 本地插件（superpowers 技能等）
├── project_img/                     # 项目图片资源
├── .cursor/                         # Cursor 编辑器配置与命令
└── .agents/                         # Agent 相关配置
```

### 自定义活动开发案例

以"自定义活动落地页"为例：

**关键决策**：

- 后台保存接口统一为 `POST + application/x-www-form-urlencoded + modulesJson`。
- C 端 `dudian-app-mall` 不直连数据库，通过 Dubbo API 读取主表/子表。
- 商品展示字段对齐 `product_list.json` 逻辑，避免两套口径。

**后台（manage-mall）方案要点**：

- DDL：`mall_custom_activity_page` + `mall_custom_activity_module`
- 代码分层：domain / mapper / service / controller / validator / test
- 保存逻辑采用"按 page_id 全删后批量插入模块"

**C 端（app-mall）方案要点**：

- 新增只读 Dubbo：`MallCustomActivityReadApi`
- 新增商品保序查询 API：`listProductsByIdsOrderPreserved`
- 抽取 `ProductListDecorationService` 复用商品填充逻辑
- 新增 `GET /customActivity/render.json`，加入 JWT 可选登录路径

### 工程化目录详解

#### `docs/` —— 文档中心

```text
docs/
├── project-structure.md                     # 仓库与模块总览
├── team-guides/                             # 团队流程、工具链实践
└── superpowers/
    ├── plans/                               # 实施计划（如 2026-04-02-custom-activity-backend.md）
    └── specs/                               # 领域/功能设计说明
```

#### `openspec/` —— 规范真相源

完整目录含 `config.yaml`、`project.md`、`specs/`、`changes/archive/`。**TDD-driven schema 示例**：

```yaml
# openspec/config.yaml
schema: tdd-driven

context: |
  Tech stack: TypeScript, Node.js, Jest
  Testing framework: Jest
  API style: RESTful
  All new code must have corresponding tests.

rules:
  proposal:
    - Include testable acceptance criteria
    - Use WHEN/THEN format for expected behaviors
  specs:
    - Use GIVEN/WHEN/THEN format
    - Each scenario must be independently testable
  tasks:
    - Order tasks by TDD cycle: test → implement → refactor
    - Each task must have a test description
  plans:
    - Break each task into 2-5 minute micro-steps
    - Every step must produce a testable outcome
```

注入顺序：`context → rules → instruction → template`，四层叠加。`context` 所有 artifact 共享，`rules` 只注入到匹配 id 的 artifact。

#### `plugins/` —— Superpowers 插件

`plugins/superpowers/skills/` 包含 14 个技能：brainstorming、dispatching-parallel-agents、executing-plans、finishing-a-development-branch、receiving-code-review、requesting-code-review、subagent-driven-development、systematic-debugging、test-driven-development、using-git-worktrees、using-superpowers、verification-before-completion、writing-plans、writing-skills。配合 `hooks/`、`scripts/`、`assets/` 形成完整插件系统。

#### `.cursor/` —— 编辑器配置

- `commands/`：18 个斜杠命令（opsx-* 系列 + Superpowers 各 skill 对应命令）
- `rules/`：AI 持久约束（`.mdc` 格式），如包结构约束、API 设计规范
- `skills/`：OpenSpec 技能入口（explore/propose/apply-change/archive-change）
- `doc/ai-context/`：长期项目上下文（project-structure、architecture、coding-standards）
- `prompts/`：场景化提示词模板（review、fix、debug、optimize、arch、api、sql、trace、compact）

#### `.claude/` —— Claude Code 配置

- `settings.json` + `agents/`（mall-common-agent、mall-service-agent、mall-app-agent、mall-message-agent）
- `commands/`（mall-verify、mall-change-apply、mall-review-risk、mall-module-locate）
- `skills/`：项目级技能（maven-module-verifier、dubbo-api-change-checker、mybatis-change-checker、message-consumer-checker、spring-xml-config-checker）
- `hooks/`：生命周期钩子（hooks.py + hooks-config.json）

**推荐使用顺序**：`/mall-dev` → `/mall-module-locate` → 对应 Agent → 高风险补充 checker → `/mall-spec-sync` → `/mall-verify` → `/mall-review-complete`。

#### `.agents/` —— Agent 配置

`plugins/marketplace.json` 配置本地 marketplace，指向 `./plugins/superpowers`，含 `installation: AVAILABLE` 策略。

### 踩坑复盘（四维度）

| 问题 | 现象 | 根因 | 影响 |
|------|------|------|------|
| 执行闭环不足 | 计划文档任务拆解细但多数未勾选 | 重点偏向方案产出，未按 task-by-task 推进到验证归档 | "计划完成=开发完成"的错觉 |
| 文档分散 | `docs/`、`openspec/`、`.cursor/doc/ai-context/` 语义重叠 | 不同用途文档并行演进，缺 SSOT 声明 | 版本漂移 |
| 跨模块链路长 | C 端 render 依赖三段改动 | 历史分层清晰但跨模块接口多 | 串联回归风险 |
| 数据口径未确认 | `moduleType=4` 双分支未定 | 数据库现状与业务规则未在开发前确认 | 临时逻辑长期化 |

### 改进措施

**流程层（必须）**：
1. 执行顺序固定：`Spec → Plan → Task实施 → 编译/测试 → 文档回写 → 归档`
2. 每 task 附一条「可验证证据」（命令、接口返回、截图或日志摘要）
3. 计划文档 checkbox 作为主进度源，禁止只在聊天中口头同步

**文档层（必须）**：
- SSOT 规定：规范基线 → `openspec/specs/*`；团队实践 → `docs/team-guides/*`；结构索引 → `docs/project-structure.md`
- 重复主题文档首段加「来源与优先级说明」
- 目录新增/迁移同步更新 `docs/project-structure.md`

**技术层（建议）**：
1. 先落 Dubbo API 契约，再落 app-mall Controller
2. `moduleType=4` 先完成数据源定稿，再写业务分支
3. 抽取公共组件后补对齐回归测试用例

### AI Template 脚手架

仓库：[Gitee - hxm0203/ai_template](https://gitee.com/hxm0203/ai_template)。快速生成 AI 辅助开发的项目模板，集成 OpenSpec / Superpowers 等规范工具链的初始结构，减少从零搭建成本。

## 使用心得与上下文管理

### 七条核心技巧

1. **在提示词中明确具体内容**：清晰说明目标而非只描述修改点，含语言/框架/风格约束。
2. **附上相关文件**：只包含与任务直接相关的文件，不要丢整个代码库。
3. **有策略地使用已打开的文件**：Cursor 等工具会自动纳入已打开文件为上下文，只保留相关文件打开。
4. **充分利用可用的上下文来源**：终端输出、linter 错误、测试结果都是有价值的上下文。
5. **保持对话重点突出**：上下文窗口有限，新任务开启新对话，避免单一线程过长导致质量下降。
6. **提供示例**：模型在模仿模式方面表现出色，展示期望的格式或风格示例。
7. **在有帮助时使用图像**：UI 截图或图表能传达难以用文字描述的上下文。

> **核心认知**：做好上下文管理，其影响最终要大于精心设计完美的提示词——输入内容的质量直接决定输出内容的质量。

### 解决 Context 不够用

| 策略 | 工具/方法 | 说明 |
|------|-----------|------|
| 自动记忆 | [[entities/claude-mem\|Claude-Mem]] | 自动捕获工具使用观察、生成语义摘要，跨会话保留上下文 |
| 会话总结与注入 | `prompt process.md` | 总结当前会话生成文件，新会话窗口 `@process.md` 注入 |
| 永久归档追溯 | OpenSpec `proposal/design/spec/tasks.md` | 永久归档，方便历史追溯 |

## Obsidian 软链接：打通项目与知识库

通过 Windows 符号链接，将项目目录映射到 Obsidian vault 中，实现**一套文件、两处管理**：

```powershell
New-Item -ItemType SymbolicLink `
  -Path "F:\obsidian\mall" `
  -Target "F:\claude\mall\project\dlabel-cloud-mall-platform"
```

| 位置 | 用途 |
|------|------|
| `F:\obsidian\mall\` | Obsidian 中以知识库形式浏览、编辑、链接项目文档 |
| `F:\claude\mall\project\...` | Cursor / Claude Code 等编辑器中正常开发 |

核心收益：使用 Obsidian 管理 MD 文档（双向链接、标签、图谱），在 Cursor 等编辑器中直接引用同一份文件，无需手动同步。

## Contradictions / Tensions

- 与偏企业化治理文档相比，本指南对"何时切入完整流程"边界更宽：强调按任务规模分级，但两边都允许通过例外机制压缩流程。
- 文档鼓励流程强制化，却也给了 `hotfix` 的裁剪口径；最终取舍依赖团队成熟度与风险容忍。
- 提倡规范先行，但 `tasks.md` 作为初稿允许在执行中调整——关键在于留痕而非僵化执行。

## Linked Entities

- [[entities/openspec]]
- [[entities/superpowers]]
- [[entities/claude-code]]

## Linked Concepts

- [[concepts/spec-driven-workflow-and-review-discipline]]
- [[concepts/team-governance-for-ai-coding]]
- [[concepts/schema-driven-maintenance]]
- [[concepts/context-and-cost-optimization]]
- [[concepts/obsidian-project-symlink]]

## Follow-up Questions

- 哪些任务特征（规模、影响面、风险）应触发完整 Superpowers 链路？
- 在你们仓库，`openspec/changes` 与 `archive` 的分层是否已有正式迁移规范？
- 如何沉淀统一的 DoD（Definition of Done）模板供 AI 开发使用？

## Related

- [[openspec-schema-tdd-workflow-injection]] — 专题实测：用 OpenSpec 自定义 schema 注入 TDD 纪律到编码工作流，结论是 propose 阶段有效、apply 阶段 TDD 循环未生效
