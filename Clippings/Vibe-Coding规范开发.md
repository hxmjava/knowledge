## 概览
![[Clippings/assets/doc-structure-overview.excalidraw]]
## 一、工具介绍

### 1.1 核心思路

传统 AI 辅助开发的典型痛点：

- 口头需求 → AI 一次性实现 → 多轮补丁后 → 缺乏记录
- 缺少**事前对齐**、**过程纪律**与**复杂任务下的并行与分工**

OpenSpec 与 Superpowers 正是为解决这些问题而生的两套工具，二者**不是互斥替代**，而是：**先对齐规范 → 再按流程执行**。

| 层级 | 工具 | 角色 | 核心职责（一句话） |
|------|------|------|---------------------|
| 规范层 | **OpenSpec** | 项目管理员 | 定义「做什么」，管理变更与规范文档 |
| 能力层 | **Superpowers** | 任务指挥官 | 决定「谁来做、按什么工程纪律做」，拆解与并行 |

![[Clippings/assets/1.1-tool-architecture.excalidraw.md]]

---

### 1.2 OpenSpec：规格驱动开发

> **原则**：*Agree before you build* —— 人类与 AI 在写代码前对规格达成一致。用文档把需求「定死」，减少 AI 自由发挥导致的跑偏与遗漏。

#### 1.2.1 安装

```bash
npm install -g @fission-ai/openspec@latest
openspec --version
cd <your-project>
openspec init
```

> [!tip] Windows（PowerShell）常见坑
> 若提示无法加载脚本，可在当前用户范围执行：
> `Set-ExecutionPolicy RemoteSigned -Scope CurrentUser`（需管理员/策略允许时）。

源码：[GitHub - Fission-AI/OpenSpec](https://github.com/Fission-AI/OpenSpec)

#### 1.2.2 目录结构

```text
openspec/
├── specs/                 # 规范的「真相来源」（类比 main）
│   └── <capability>/
│       └── spec.md
└── changes/               # 提议 / 进行中 / 已归档的变更（类比 feature 分支）
    └── <change-name>/
        ├── proposal.md    # 为什么改、改什么
        ├── tasks.md       # 实施检查清单
        └── specs/         # 对规范的增量「补丁」
```

**落地要求**：改行为先走 `changes/`，合并/归档后再反映到 `specs/`，避免「口头改需求、代码里偷偷改规范」。

#### 1.2.3 核心工作流命令

![[Clippings/assets/1.2.3-openspec-workflow.excalidraw.md]]

| 命令 | 作用 | 何时用 |
|------|------|--------|
| `/opsx:explore` | 只讨论、不强制产出正式文档 | 需求/方案还不清楚 |
| `/opsx:propose` | 一次性生成规划类产物 | 方向清楚，要开变更 |
| `/opsx:apply` | 按 `tasks.md` 逐项落地代码 | 规划已冻结，开始实现 |
| `/opsx:archive` | 归档已完成变更 | 实现结束，规范合回主线认知 |

> [!note] 扩展命令
> 如 `verify` 等：若默认不可用，按项目约定执行 `openspec config profile custom` 与 `openspec update` 后重启工具。

#### 1.2.4 团队检查清单

- [ ] 本次改动是否在 `openspec/changes/<name>/` 下有 `proposal.md` + `tasks.md`？
- [ ] `tasks.md` 是否可被逐条勾掉，且与评审结论一致？
- [ ] 完成后是否执行归档，避免「代码已合并、规范仍停留在旧版」？

---

### 1.3 Superpowers：强制性软件开发工作流

> **原则**：Superpowers 是**工作流与可组合技能（Skills）**，目标是把最佳实践变成 Agent 的默认行为，而不是「想起来再提醒」。

#### 1.3.1 安装

```text
Cursor：       /add-plugin superpowers
Claude Code：  /plugin marketplace add obra/superpowers-marketplace
Codex：        Fetch and follow instructions from
               https://raw.githubusercontent.com/obra/superpowers/refs/heads/main/.codex/INSTALL.md
```

源码：[GitHub - obra/superpowers](https://github.com/obra/superpowers)

#### 1.3.2 内置流程（按顺序执行）

![[Clippings/assets/1.3.2-superpowers-workflow.excalidraw.md]]

| 顺序 | 技能 | 目的 |
|------|------|------|
| 1 | `brainstorming` | 需求澄清（苏格拉底式提问） |
| 2 | `using-git-worktrees` | 隔离工作区 |
| 3 | `writing-plans` | 拆成可执行的小步任务 |
| 4 | `subagent-driven-development` | 子代理执行 + 审查 |
| 5 | `test-driven-development` | 强制 TDD |
| 6 | `requesting-code-review` | 代码审查，关键问题可阻塞 |
| 7 | `finishing-a-development-branch` | 收尾与合并选项 |

**落地要求**：对「长任务/核心模块」默认走完整链路；对「一行 hotfix」可裁剪，但要在 PR/记录里写明例外原因。

#### 1.3.3 TDD 纪律（RED → GREEN → REFACTOR）

![[Clippings/assets/1.3.3-tdd-cycle.excalidraw.md]]

1. **RED**：先写会失败的测试
2. **GREEN**：最少实现使测试通过
3. **REFACTOR**：重构优化

> [!important] 团队约定
> 核心逻辑合并前，测试策略（单测/集成测）与覆盖范围在评审中可审计；避免「事后补测糊弄过关」。

#### 1.3.4 目录结构

```text
plugins/superpowers/          # 插件根目录
├── skills/                   # 可安装技能
│   └── <capability>/
│       └── SKILL.md          # 技能文档
docs/
└── superpowers/
    ├── plans/                # 实施计划
    │   └── <capability>.md
    └── specs/                # 设计说明
        └── <change-name>-design.md
```

#### 1.3.5 团队检查清单

- [ ] 是否先有计划/任务拆分再大规模改代码？
- [ ] 是否对关键路径执行 TDD 或等效的可自动化验证？
- [ ] 是否经过代码审查环节（人工或规范化 checklist）？

---

## 二、协同使用场景与流水线

### 2.1 什么时候用哪个

| 场景 | 推荐 | 原因 |
|------|------|------|
| 核心业务、长期维护模块 | Superpowers（+ 测试/评审） | 质量与可维护性 |
| 多人协作、需对外/对内说明 | OpenSpec | 规范统一、可归档追溯 |
| 生产级功能迭代 | **二者协同** | 规范 + 纪律 |
| 极小范围 bugfix | 原生 Agent / 最小流程 | 避免流程成本大于收益 |

![[Clippings/assets/2.1-scenario-decision.excalidraw.md]]

### 2.2 五阶段流水线

以实际功能开发为例，二者串联为一条标准流水线：

![[Clippings/assets/2.2-five-stage-pipeline.excalidraw.md]]

| 阶段        | 主导                | 产出/动作                                     |
| --------- | ----------------- | ----------------------------------------- |
| **1. 提案** | OpenSpec          | `proposal` / `design` / spec / `tasks.md` |
| **2. 纠偏** | Superpowers（Plan） | 技术栈或约束与初稿不一致时，重写任务分层与依赖                   |
| **3. 实现** | Superpowers       | 子任务并行；工具层读写、诊断、跑测                         |
| **4. 验证** | 测试与 CI            | 单测/集成测、本地与流水线一致                           |
| **5. 归档** | OpenSpec          | `/opsx:archive`，规范与实现可追溯                  |

> [!tip] 关键认知
> `tasks.md` 可能是**初稿**；执行中允许由 Plan/评审调整为更合理的 Wave/依赖，但**变更要有记录**（评论、修订版 tasks、或 ADR），避免无法审计。

### 2.3 角色分工速查

| 系统 | 职责 | 典型触发 |
|------|------|----------|
| OpenSpec | 规范定义、变更追踪、归档 | `propose` / `archive` |
| Superpowers | 规划、并行执行、TDD/审查 | 长任务、核心模块 |

---

## 三、项目实践

### 3.1 仓库顶层目录

```text
dlabel-cloud-mall-platform/
├── AGENTS.md        # Agent 配置说明，供 Claude Code / Codex 等读取
├── CLAUDE.md        # Claude Code 项目级指令与约束
├── README.md        # 项目说明文档
├── pom.xml          # 父 POM，统一依赖与模块
├── src/             # 源码目录
├── docs/            # 文档（团队指南、方案与规格草稿等）
├── openspec/        # OpenSpec 配置与规格目录
├── plugins/         # 本地插件（如 Superpowers 技能等）
├── project_img/     # 项目图片资源
├── .cursor/         # Cursor 编辑器配置与命令
├── .claude/         # Claude Code 配置与技能
└── .agents/         # Agent 相关配置
```

### 3.2 工程化目录详解

#### 3.2.1 `docs/` —— 文档中心

```text
docs/
├── project-structure.md                        # 仓库与模块总览
├── team-guides/                                # 团队流程、工具链实践
│   └── opencode-openspec-superpowers-omo-practice.md
└── superpowers/
    ├── plans/                                  # 实施计划
    │   ├── 2026-04-02-custom-activity-backend.md
    │   └── 2026-04-02-custom-activity-app-mall-render.md
    └── specs/                                  # 领域/功能设计说明
        ├── 2026-04-02-custom-activity-app-mall-design.md
        └── 2026-04-02-custom-activity-backend-only-design.md
```

| 子路径 | 说明 |
|--------|------|
| `docs/team-guides/` | OpenCode / OpenSpec / Superpowers 等与日常开发结合的实践说明 |
| `docs/superpowers/plans/` | 大块功能的落地计划、里程碑式说明 |
| `docs/superpowers/specs/` | 产品/技术设计文档，便于评审与留档 |

#### 3.2.2 `openspec/` —— 规范真相源

```text
openspec/
├── config.yaml                              # 工作流配置（schema: spec-driven 等）
├── project.md                               # 技术栈、环境、规范摘要
├── specs/                                   # 已采纳的能力规格
│   ├── custom-activity-page-manage/
│   │   └── spec.md
│   └── smart-address-recognize/
│       └── spec.md
└── changes/
    └── archive/                             # 已归档变更
        ├── 2026-03-19-admin-custom-activity-config/
        │   ├── .openspec.yaml
        │   ├── proposal.md
        │   ├── design.md
        │   ├── tasks.md
        │   └── specs/custom-activity-page-manage/spec.md
        └── 2026-03-19-smart-address-recognition/
            ├── .openspec.yaml
            ├── proposal.md
            ├── design.md
            ├── tasks.md
            └── specs/smart-address-recognize/spec.md
```

| 文件/目录                          | 说明                            |
| ------------------------------ | ----------------------------- |
| `config.yaml`                  | OpenSpec 模式与可选的按产物类型规则        |
| `project.md`                   | 与 AI/工具共享的项目常量：框架版本、中间件、编码约定等 |
| `specs/<capability>/spec.md`   | 某条能力的正式规格，随变更合并而演进            |
| `changes/archive/<change-id>/` | 一次变更的全套材料                     |

**配置示例：TDD-driven schema**

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
    - Reference existing patterns before inventing new ones
  tasks:
    - Order tasks by TDD cycle: test → implement → refactor
    - Each task must have a test description
  plans:
    - Break each task into 2-5 minute micro-steps
    - Every step must produce a testable outcome
```

> [!note] context 与 rules 的分工
> - `context`：所有 artifact 共享的信息（技术栈、测试框架等）
> - `rules`：只注入到匹配 id 的 artifact（如 `rules.specs` 只出现在 specs prompt 中）
>
> 注入顺序：`context → rules → instruction → template`，四层叠加。

![[Clippings/assets/3.2.2-config-injection.excalidraw.md]]

#### 3.2.3 `plugins/` —— Superpowers 插件

```text
plugins/
└── superpowers/
    ├── .codex-plugin/
    │   └── plugin.json
    ├── skills/                              # 可安装技能
    │   ├── brainstorming/
    │   ├── dispatching-parallel-agents/
    │   ├── executing-plans/
    │   ├── finishing-a-development-branch/
    │   ├── receiving-code-review/
    │   ├── requesting-code-review/
    │   ├── subagent-driven-development/
    │   ├── systematic-debugging/
    │   ├── test-driven-development/
    │   ├── using-git-worktrees/
    │   ├── using-superpowers/
    │   ├── verification-before-completion/
    │   ├── writing-plans/
    │   └── writing-skills/
    ├── hooks/                               # 生命周期钩子
    ├── scripts/                             # 技能或钩子调用的脚本
    └── assets/                              # 静态资源
```

#### 3.2.4 `.cursor/` —— 编辑器配置

```text
.cursor/
├── commands/                                # 斜杠命令
│   ├── opsx-explore.md                      # OpenSpec 探索
│   ├── opsx-propose.md                      # OpenSpec 提案
│   ├── opsx-apply.md                        # OpenSpec 实施
│   ├── opsx-archive.md                      # OpenSpec 归档
│   ├── using-superpowers.md                 # 总入口，判断当前任务走哪条流程
│   ├── brainstorming.md                     # 实现前先澄清需求、比较方案、完成设计
│   ├── writing-plans.md                     # 把设计拆成可执行、可验证的实施计划
│   ├── using-git-worktrees.md               # 创建隔离工作区和独立分支
│   ├── subagent-driven-development.md       # 子代理分工实现，审查流程内建
│   ├── executing-plans.md                   # 按既定 plan 串行推进，逐项执行和验证
│   ├── test-driven-development.md           # 先写失败测试，再最小实现，最后重构
│   ├── systematic-debugging.md              # 先查根因、验证假设，再进入修复
│   ├── requesting-code-review.md            # 在关键节点主动发起代码审查
│   ├── receiving-code-review.md             # 处理 review 反馈，逐项修复
│   ├── verification-before-completion.md    # 没有最新验证结果前，不允许宣称完成
│   ├── finishing-a-development-branch.md    # 统一处理测试、分支、合并和清理
│   ├── dispatching-parallel-agents.md       # 把独立问题分发给多个代理并行处理
│   └── writing-skills.md                   # 编写和迭代 skill 本身的元能力
├── rules/                                   # AI 持久约束（.mdc）
│   ├── skills-create-slash-command.mdc
│   ├── dudian-app-mall-package-structure.mdc
│   ├── dudian-manage-mall-super-package-structure.mdc
│   └── manage-mall-super-api-design.mdc
├── skills/                                  # OpenSpec 技能入口
│   ├── openspec-explore/
│   ├── openspec-propose/
│   ├── openspec-apply-change/
│   └── openspec-archive-change/
├── doc/ai-context/                          # 长期项目上下文
│   ├── project-structure.md
│   ├── architecture.md
│   └── coding-standards.md
└── prompts/                                 # 场景化提示词模板
    ├── review.md / fix.md / debug.md
    ├── optimize.md / arch.md / api.md
    ├── sql.md / trace.md / compact.md
```

#### 3.2.5 `.claude/` —— Claude Code 配置

```text
.claude/
├── settings.json
├── agents/                                    # 项目级 Agent 定义
│   ├── mall-common-agent.md
│   ├── mall-service-agent.md
│   ├── mall-app-agent.md
│   └── mall-message-agent.md
├── commands/                                  # 斜杠命令
│   ├── mall-verify.md
│   ├── mall-change-apply.md
│   ├── mall-review-risk.md
│   └── mall-module-locate.md
├── skills/                                    # 项目级技能
│   ├── maven-module-verifier/
│   │   └── SKILL.md
│   ├── dubbo-api-change-checker/
│   │   └── SKILL.md
│   ├── mybatis-change-checker/
│   │   └── SKILL.md
│   ├── message-consumer-checker/
│   │   └── SKILL.md
│   └── spring-xml-config-checker/
│       └── SKILL.md
└── hooks/                                     # 生命周期钩子
    ├── HOOKS-README.md
    ├── scripts/
    │   └── hooks.py
    └── config/
        └── hooks-config.json
```

**推荐使用顺序：**

1. 日常开发优先从 `/mall-dev` 开始
2. 如果只想判断需求落点，再单独用 `/mall-module-locate`
3. 再根据层级交给对应 Agent
4. 若涉及高风险改动，补充使用 `dubbo-api-change-checker`、`mybatis-change-checker`、`message-consumer-checker`、`spring-xml-config-checker` 或 `/mall-review-risk`
5. 如果实现让 OpenSpec 发生漂移，使用 `/mall-spec-sync` 回写 `proposal / design / tasks / spec`
6. 最后用 `/mall-verify` 生成或执行最小但足够的 Maven 验证
7. 高风险、跨层或准备交付时，再用 `/mall-review-complete` 做一次统一收口
   ![[3.2.5-claude-workflow.excalidraw]]

#### 3.2.6 `.agents/` —— Agent 配置

```text
.agents/
└── plugins/
    └── marketplace.json                     # 本地 marketplace 配置
```

| 字段 | 说明 |
|------|------|
| `name` / `interface.displayName` | 市场在 UI 中的展示名 |
| `plugins[].source.path` | 指向 `./plugins/superpowers` 等相对仓库根的路径 |
| `policy` | 如 `installation: AVAILABLE`、认证策略等 |

---

### 3.3 功能开发实战：自定义活动落地页

#### 3.3.1 需求澄清与边界确定

**输入：**
![[Pasted image 20260508095709.png]]
- 目标功能：自定义活动落地页
- 约束：老技术栈（Java 8 + Spring + Dubbo + MyBatis）、模块化 Maven 工程
- 规则：优先按 OpenSpec / Superpowers 工作方式组织产物
- 输出：`proposal` / `design` / spec / `tasks.md`
![[Pasted image 20260508150111.png]]

**关键决策：**
![[Pasted image 20260508095845.png]]

- 后台保存接口统一为 `POST + application/x-www-form-urlencoded + modulesJson`，避免 GET 长 URL 风险
- C 端 `dudian-app-mall` 不直连数据库，通过 Dubbo API 读取主表/子表
- 商品展示字段对齐 `product_list.json` 逻辑，避免两套口径

**输出产物：**

![[Pasted image 20260508100110.png]]
- 后台实施计划：`docs/superpowers/plans/2026-04-02-custom-activity-backend.md`
- C 端实施计划：`docs/superpowers/plans/2026-04-02-custom-activity-app-mall-render.md`
![[Pasted image 20260508150159.png]]
#### 3.3.2 规格驱动设计

**后台（manage-mall）方案要点：**

- DDL：`mall_custom_activity_page` + `mall_custom_activity_module`
- 代码分层：domain / mapper / service / controller / validator / test
- 列表与下拉统一关联 `mall_marketing_activity`
- 保存逻辑采用「按 page_id 全删后批量插入模块」

**C 端（app-mall）方案要点：**

- 新增只读 Dubbo：`MallCustomActivityReadApi`
- 新增商品保序查询 API：`listProductsByIdsOrderPreserved`
- 抽取 `ProductListDecorationService` 复用商品填充逻辑
- 新增 `GET /customActivity/render.json`，并加入 JWT 可选登录路径

**文档联动：**

- `docs/superpowers/specs/*` 与 `openspec/specs/*` 同步方法语义与字段口径
- 明确模块排序规则：`module_type ASC, id ASC`

---

### 3.4 踩坑复盘

#### 问题一：计划完整但执行闭环不足

| 维度 | 说明 |
|------|------|
| **现象** | 两份计划文档任务拆解很细，但多数仍为待勾选状态 |
| **影响** | 设计很充分，代码落地与验证进度不可见，容易出现「计划完成 = 开发完成」的错觉 |
| **根因** | 本轮重点偏向方案产出与结构文档沉淀，未按 task-by-task 持续推进到验证与归档 |

#### 问题二：文档分散，信息重复

| 维度     | 说明                                                                    |
| ------ | --------------------------------------------------------------------- |
| **现象** | `docs/superpowers/*`、`openspec/*`、`.cursor/doc/ai-context/*` 之间存在语义重叠 |
| **影响** | 同一事实可能出现多份描述，长期会出现版本漂移                                                |
| **根因** | 不同用途文档并行演进，但缺少「单一事实源（SSOT）」声明                                         |

#### 问题三：跨模块实现链路长

![[Clippings/assets/3.3-cross-module-dependency.excalidraw.md]]

| 维度 | 说明 |
|------|------|
| **现象** | C 端 render 依赖 base-api、product-api、app-mall 三段改动 |
| **影响** | 任何一段契约变更都可能导致串联回归；排查路径长 |
| **根因** | 历史分层清晰但跨模块接口多，改动需严格按契约推进 |

#### 问题四：数据口径未提前确认

| 维度 | 说明 |
|------|------|
| **现象** | `moduleType=4` 推荐商品来源保留了「有活动商品表 / 无活动商品表」双分支 |
| **影响** | 实现时若未先定库表口径，容易产生临时逻辑长期化 |
| **根因** | 数据库现状与业务规则未在开发前一次性确认 |

---

### 3.5 改进措施

#### 3.5.1 流程层（必须）

1. 执行顺序固定为：`Spec → Plan → Task 实施 → 编译/测试 → 文档回写 → 归档`
2. 每完成 1 个 task 必须附一条「可验证证据」（命令、接口返回、截图或日志摘要）
3. 计划文档中的 checkbox 作为主进度源，禁止只在聊天中口头同步

#### 3.5.2 文档层（必须）

规定 SSOT（单一事实源）：

| 文档类型 | SSOT 位置 |
|----------|-----------|
| 规范基线 | `openspec/specs/*` |
| 团队实践 | `docs/team-guides/*` |
| 结构索引 | `docs/project-structure.md` |

- 在重复主题文档首段加「来源与优先级说明」
- 每次目录新增/迁移，同步更新 `docs/project-structure.md`

#### 3.5.3 技术层（建议）

1. 先落 Dubbo API 契约，再落 app-mall Controller，避免前后端接口反复改签名
2. `moduleType=4` 先完成数据源定稿，再写业务分支；禁止默认长期使用临时方案
3. 抽取 `ProductListDecorationService` 后，补至少 1 个对齐 `product_list` 的回归测试用例

---

### 3.6 推荐工具与脚手架

#### 3.6.7 AI Template 脚手架

**仓库地址**：[Gitee - hxm0203/ai_template](https://gitee.com/hxm0203/ai_template)

> [!tip] 用途
> 快速生成 AI 辅助开发的项目模板，集成 OpenSpec / Superpowers 等规范工具链的初始结构，减少从零搭建的成本。

---

## 四、使用心得

### 4.1 小技巧总结

#### 4.1.1 在提示词中明确具体内容

清晰说明你想要达成的目标，而不只是需要修改的地方。要包含相关的限制条件（语言、框架、风格等）。

#### 4.1.2 附上相关文件

只包含与你的任务直接相关的文件。不要一股脑儿地把整个代码库都丢过去 —— 重点放在相关的内容上。

#### 4.1.3 有策略地使用已打开的文件

像 Cursor 这类工具会自动将已打开的文件纳入上下文。只保留相关的文件处于打开状态，以避免出现干扰信息。

#### 4.1.4 充分利用可用的上下文来源

终端输出、代码检查器错误信息以及测试结果等都是很有价值的上下文。在调试或解决问题时，要把这些内容包含进去。

#### 4.1.5 保持对话重点突出

上下文窗口是有限的。对于新任务，要开启新的对话，而不是让单个对话线程变得过长，因为这会逐渐降低质量。

#### 4.1.6 提供示例

如果你希望输出具有特定的格式或风格，那就展示一个示例。模型在模仿模式方面表现出色。

#### 4.1.7 在有帮助时使用图像

许多 AI 工具支持附加图像。用户界面的截图或图表能够传达那些难以用文字描述的上下文信息。

> [!important] 核心认知
> 做好上下文管理，其影响最终要大于精心设计完美的提示词 —— 你输入内容的质量直接决定了你输出内容的质量。

### 4.2 解决 Context 上下文不够用

#### 4.2.1 Claude-Mem 自动记忆

通过自动捕获工具使用观察、生成语义摘要并使其可用于未来会话，无缝保留跨会话的上下文。

#### 4.2.2 会话总结与注入

通过 `prompt process.md` 总结当前会话，生成文件到 `docs/process.md`，在新会话窗口 `@process.md` 进行上下文注入。

#### 4.2.3 永久归档追溯

通过 `proposal` / `design` / `spec` / `tasks.md` 永久归档，方便历史追溯。

---

## 五、管理MD文件

### 5.1 用「软链接」打通项目和 Obsidian

通过 Windows 符号链接，将项目目录映射到 Obsidian 知识库中，实现**一套文件、两处管理**：

```powershell
New-Item -ItemType SymbolicLink `
  -Path "F:\obsidian\mall" `
  -Target "F:\claude\mall\project\dlabel-cloud-mall-platform"
```

**效果**

| 位置 | 用途 |
|------|------|
| `F:\obsidian\mall\` | Obsidian 中以知识库形式浏览、编辑、链接项目文档 |
| `F:\claude\mall\project\dlabel-cloud-mall-platform\` | Cursor / Claude Code 等编辑器中正常开发 |

> [!tip] 核心收益
> 使用 Obsidian 管理 MD 文档（双向链接、标签、图谱），在 Cursor 等编辑器中直接引用同一份文件，无需手动同步。

---

## 六、常见问题

**Q1：`/opsx:verify` 等命令不存在？**
A：OpenSpec 1.0 默认仅启用 explore / propose / apply / archive；扩展能力需切到 custom profile 并 `openspec update` 后重启。

**Q2：`tasks.md` 和实际开发任务不一致？**
A：可接受；以**评审通过的执行计划**为准，但应保留「为何调整」的痕迹，归档时说明规范与实现的对应关系。

**Q3：两个工具都必须装吗？**
A：否。简单任务原生即可；要规范加 OpenSpec；要质量加 Superpowers；生产级常组合使用。

**Q4：二者是否硬依赖？**
A：无硬依赖；组合使用效果通常更好：**OpenSpec 定方向，Superpowers 定计划与纪律**。

---

