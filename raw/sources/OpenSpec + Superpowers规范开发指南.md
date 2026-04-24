# OpenSpec + Superpowers：规范开发指南

## 1.解决问题

### 1.1 典型痛点

- 口头需求 → AI 一次性实现 → 多轮补丁后 →缺乏记录。
- 缺少**事前对齐**、**过程纪律**与**复杂任务下的并行与分工**。

### 1.2 二条线的分工

| 层级 | 工具 | 角色 | 核心职责（团队可复述的一句话） |
|------|------|------|--------------------------------|
| 规范层 | **OpenSpec** | 项目管理员 | 定义「做什么」、管理变更与规范文档 |
| 能力层 | **Superpowers** | 任务指挥官 | 决定「谁来做、按什么工程纪律做」、拆解与并行 |

二者**不是互斥替代**，而是：**先对齐规范 → 再按流程执行**。

---

## 2. OpenSpec：规格驱动开发

### 2.1 原则

- **Agree before you build**：人类与 AI 在写代码前对规格达成一致。
- 用文档把需求「定死」，减少 AI 自由发挥导致的跑偏与遗漏。

### 2.2 目录结构

建议团队在仓库中统一（与具体 CLI 版本无关）：

```text
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

**落地要求**：改行为先走 `changes/`，合并/归档后再反映到 `specs/`，避免「口头改需求、代码里偷偷改规范」。

### 2.3 安装与初始化（通用参考）

github:https://github.com/Fission-AI/OpenSpec

```bash
npm install -g @fission-ai/openspec@latest
openspec --version
cd <your-project>
openspec init
```

**Windows（PowerShell）常见坑**：若提示无法加载脚本，可在当前用户范围执行：`Set-ExecutionPolicy RemoteSigned -Scope CurrentUser`（需管理员/策略允许时）。

### 2.4 核心工作流命令（默认 core workflow）

| 命令 | 作用 | 何时用 |
|------|------|--------|
| `/opsx:explore` | 只讨论、不强制产出正式文档 | 需求/方案还不清 |
| `/opsx:propose` | 一次性生成规划类产物 | 方向清楚，要开变更 |
| `/opsx:apply` | 按 `tasks.md` 逐项落地代码 | 规划已冻结，开始实现 |
| `/opsx:archive` | 归档已完成变更 | 实现结束，规范要合回主线认知 |

**扩展命令**（如 verify 等）：若默认不可用，按项目约定执行 `openspec config profile custom` 与 `openspec update` 后重启工具（以你们环境文档为准）。

### 2.5 团队检查清单（OpenSpec）

- [ ] 本次改动是否在 `openspec/changes/<name>/` 下有 `proposal.md` + `tasks.md`（以及必要的 spec 增量）？
- [ ] `tasks.md` 是否可被逐条勾掉，且与评审结论一致？
- [ ] 完成后是否执行归档，避免「代码已合并、规范仍停留在旧版」？

---

## 3. Superpowers：**强制性软件开发工作流**

### 3.1 原则

- Superpowers 是**工作流与可组合技能（skills）**，目标是把最佳实践变成 Agent 的默认行为，而不是「想起来再提醒」。

### 3.2 内置流程

| 顺序 | 技能（概念名） | 目的 |
|------|----------------|------|
| 1 | brainstorming | 需求澄清（苏格拉底式提问） |
| 2 | using-git-worktrees | 隔离工作区 |
| 3 | writing-plans | 拆成可执行的小步任务 |
| 4 | subagent-driven-development | 子代理执行 + 审查 |
| 5 | test-driven-development | 强制 TDD |
| 6 | requesting-code-review | 代码审查，关键问题可阻塞 |
| 7 | finishing-a-development-branch | 收尾与合并选项 |

**落地要求**：对「长任务 / 核心模块」默认走完整链路；对「一行 hotfix」可裁剪，但要在 PR/记录里写明例外原因。

### 3.3 TDD 纪律（RED → GREEN → REFACTOR）

1. 先写会失败的测试（RED）  
2. 运行确认失败  
3. 最少实现使测试通过（GREEN）  
4. 重构（REFACTOR）

**团队约定**：核心逻辑合并前，测试策略（单测/集成测）与覆盖范围在评审中可审计；避免「事后补测糊弄过关」。

### 3.4 安装与验证

github:https://github.com/obra/superpowers

```
cursor： /add-plugin superpowers
Claude Code：/plugin marketplace add obra/superpowers-marketplace
Codex：Fetch and follow instructions from https://raw.githubusercontent.com/obra/superpowers/refs/heads/main/.codex/INSTALL.md
```

### 3.5 目录结构

```
plugins/superpowers/	   #插件
├── skills/                 
    └── <capability>/	   #技能名称
        └── SKILL.md	   #技能文档
docs/
├── superpowers/                 
    ├── plans/                           # 计划
        └── <capability>.md				 #实现计划
    └── specs/                           # 设计
        └── <change-name>-design.md      # 设计说明

```

### 3.6 团队检查清单

- [ ] 是否先有计划/任务拆分再大规模改代码？
- [ ] 是否对关键路径执行 TDD 或等效的可自动化验证？
- [ ] 是否经过代码审查环节（人工或规范化 checklist）？

---

## 4. 二者如何串成一条流水线

原文以「用户管理 API」为例，可抽象为团队标准五阶段：

| 阶段 | 主导 | 产出/动作 |
|------|------|-----------|
| 1. 提案 | OpenSpec | `proposal` / `design` / 规范增量 / `tasks.md` |
| 2. 纠偏 | Superpowers（Plan） | 技术栈或约束与初稿不一致时，**重写任务分层与依赖**（如 Wave 并行批次） |
| 3. 实现 | Superpowers | 子任务并行；工具层读写、诊断、跑测 |
| 4. 验证 | 测试与 CI | 单测/集成测、本地与流水线一致 |
| 5. 归档 | OpenSpec | `/opsx:archive`，规范与实现可追溯 |

**关键认知**：`tasks.md` 可能是**初稿**；执行中允许由 Plan/评审调整为更合理的 Wave/依赖，但**变更要有记录**（评论、修订版 tasks、或 ADR），避免无法审计。

---

## 5. 什么时候用哪个

| 场景 | 推荐 | 原因 |
|------|------|------|
| 核心业务、长期维护模块 | Superpowers（+ 测试/评审） | 质量与可维护性 |
| 多人协作、需对外/对内说明 | OpenSpec | 规范统一、可归档追溯 |
| 生产级功能迭代 | 二者协同 | 规范 + 纪律 |
| 极小范围 bugfix | 原生 Agent / 最小流程 | 避免流程成本大于收益 |

---

## 6. 常见问题

**Q1：`/opsx:verify` 等命令不存在？**  
A：OpenSpec 1.0 默认可能仅启用 explore / propose / apply / archive；扩展能力需切到 custom profile 并 `openspec update` 后重启（以你们环境为准）。

**Q2：`tasks.md` 和实际开发任务不一致？**  
A：可接受；以**评审通过的执行计划**为准，但应保留「为何调整」的痕迹，归档时说明规范与实现的对应关系。

**Q3：二个都必须装吗？**  
A：否。简单任务原生即可；要规范加 OpenSpec；要质量加 Superpowers；生产级常组合使用。

**Q4：二者是否硬依赖？**  
A：无硬依赖；组合使用效果通常更好：**OpenSpec 定方向，Superpowers 定计划与纪律**。

---

## 7. 角色分工

| 系统 | 职责 | 典型触发 |
|------|------|----------|
| OpenSpec | 规范定义、变更追踪、归档 | propose / archive |
| Superpowers | 规划、并行执行、TDD/审查 | 长任务、核心模块 |

---

## 8. 实践-商城二期

### 8.1仓库顶层目录

```
dlabel-cloud-mall-platform/
├── pom.xml                          # 父 POM，统一依赖与模块
├── src/   							 # 源码目录
├── docs/                            # 文档（含团队指南、方案与规格草稿等）
├── openspec/                        # OpenSpec 配置与规格目录
├── plugins/                         # 本地插件（如 superpowers 技能等）
├── project_img/                     # 项目图片资源
├── .cursor/                         # Cursor 编辑器配置与命令等
└── .agents/                         # Agent 相关配置
```

### 8.2工程化与文档目录（详解）

#### 8.2.1 `docs/`

```
docs/
├── project-structure.md              # 本文件：仓库与模块总览
├── team-guides/                       # 团队流程、工具链实践
│   └── opencode-openspec-superpowers-omo-practice.md
└── superpowers/                       # 与 Superpowers 工作流相关的设计稿（非 OpenSpec 归档时的草案常放此处）
    ├── plans/                         # 实施计划、分阶段任务叙述
    │   ├── 2026-04-02-custom-activity-backend.md
    │   └── 2026-04-02-custom-activity-app-mall-render.md
    └── specs/                         # 领域/功能设计说明（偏叙述性）
        ├── 2026-04-02-custom-activity-app-mall-design.md
        └── 2026-04-02-custom-activity-backend-only-design.md
```

| 子路径                    | 说明                                                         |
| ------------------------- | ------------------------------------------------------------ |
| `docs/team-guides/`       | OpenCode / OpenSpec / Superpowers 等与日常开发结合的实践说明 |
| `docs/superpowers/plans/` | 大块功能的落地计划、里程碑式说明                             |
| `docs/superpowers/specs/` | 产品/技术设计文档，便于评审与留档                            |

#### 8.2.2 `openspec/`

```
openspec/
├── config.yaml                        # 工作流配置（如 schema: spec-driven；可扩展 AI 生成规则）
├── project.md                         # 技术栈、环境、规范摘要，供生成变更/规格时引用
├── specs/                             # 已采纳的能力规格（按能力拆分子目录）
│   ├── custom-activity-page-manage/
│   │   └── spec.md
│   └── smart-address-recognize/
│       └── spec.md
└── changes/
    └── archive/                       # 已归档变更（每变更一个子目录）
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

| 文件/目录                      | 说明                                                         |
| ------------------------------ | ------------------------------------------------------------ |
| `config.yaml`                  | OpenSpec 模式与可选的按产物类型规则（如 proposal/tasks 的写作约束） |
| `project.md`                   | 与 AI/工具共享的项目常量：框架版本、中间件、编码约定等       |
| `specs/<capability>/spec.md`   | 某条能力的正式规格，随变更合并而演进                         |
| `changes/archive/<change-id>/` | 一次变更的全套材料；活跃中的变更也可位于 `changes/<id>/`（有则与 archive 同级） |

#### 8.2.3`plugins/`

```
plugins/
└── superpowers/
    ├── .codex-plugin/
    │   └── plugin.json                # 插件元数据：名称、skills/hooks/mcp 入口等
    ├── skills/                        # 可安装技能（各子目录一个 SKILL.md）
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
    │   ├── using-superpowers/         # 含 references/ 引用材料
    │   ├── verification-before-completion/
    │   ├── writing-plans/
    │   └── writing-skills/            # 含 examples/ 示例
    ├── hooks/                         # 生命周期钩子（见 hooks 目录说明与 plugin.json 中 hooks 配置）
    ├── scripts/                       # 技能或钩子调用的脚本
    ├── assets/                        # 图标等静态资源
    └── README.md（若存在）             # 各子目录也可能有独立 README
```

| 子路径           | 说明                                                  |
| ---------------- | ----------------------------------------------------- |
| `skills/<name>/` | 单技能包：核心为 `SKILL.md`，部分技能含 `scripts/` 等 |
| `hooks/`         | 在特定 IDE/插件事件下触发的自动化                     |
| `scripts/`       | 与技能或运维相关的可执行脚本集合                      |

#### 8.2.4`.cursor/`

```
.cursor/
├── commands/                          # 斜杠命令（frontmatter + 正文指向某技能或流程）
│   ├── opsx-explore.md                # OpenSpec：探索
│   ├── opsx-propose.md                # OpenSpec：提案
│   ├── opsx-apply.md                  # OpenSpec：按任务实施
│   ├── opsx-archive.md                # OpenSpec：归档变更
│   ├── brainstorming.md
│   ├── writing-plans.md
│   ├── executing-plans.md
│   ├── subagent-driven-development.md
│   ├── dispatching-parallel-agents.md
│   ├── test-driven-development.md
│   ├── systematic-debugging.md
│   ├── verification-before-completion.md
│   ├── requesting-code-review.md
│   ├── receiving-code-review.md
│   ├── finishing-a-development-branch.md
│   ├── using-git-worktrees.md
│   ├── using-superpowers.md
│   └── writing-skills.md
├── rules/                             # 始终或按模式生效的 AI 规则（.mdc）
│   ├── skills-create-slash-command.mdc
│   ├── dudian-app-mall-package-structure.mdc
│   ├── dudian-manage-mall-super-package-structure.mdc
│   └── manage-mall-super-api-design.mdc
├── skills/                            # 仓库内 OpenSpec 相关技能入口（SKILL.md）
│   ├── openspec-explore/
│   ├── openspec-propose/
│   ├── openspec-apply-change/
│   └── openspec-archive-change/
├── doc/
│   └── ai-context/                    # 给 AI 的长期项目上下文（可与 openspec/project.md 对照）
│       ├── project-structure.md
│       ├── architecture.md
│       └── coding-standards.md
└── prompts/                           # 场景化提示词片段
    ├── review.md
    ├── fix.md
    ├── debug.md
    ├── optimize.md
    ├── arch.md
    ├── api.md
    ├── sql.md
    ├── trace.md
    └── compact.md
```

| 子路径              | 说明                                                         |
| ------------------- | ------------------------------------------------------------ |
| `commands/`         | 对话中 `/命令名` 触发的说明文件，常引用 `plugins/superpowers/skills/...` 或 `.cursor/skills/...` |
| `rules/*.mdc`       | 包结构、API 设计、技能与命令联动等持久约束（https://cursor.directory/） |
| `skills/openspec-*` | 与 `openspec/` 目录配合使用的 Cursor 技能定义                |
| `doc/ai-context/`   | 架构、目录、编码标准等，适合作为会话初始上下文               |
| `prompts/`          | 代码评审、排错、SQL、链路追踪等短提示模板                    |

#### 8.2.5`.agents/`

```
.agents/
└── plugins/
    └── marketplace.json               # 本地 marketplace：名称、插件 path、安装策略等
```

| 字段含义                         | 说明                                            |
| -------------------------------- | ----------------------------------------------- |
| `name` / `interface.displayName` | 市场在 UI 中的展示名（如 DLabel Local Plugins） |
| `plugins[].source.path`          | 指向 `./plugins/superpowers` 等相对仓库根的路径 |
| `policy`                         | 如 `installation: AVAILABLE`、认证策略等        |

### 8.3功能需求-自定义活动开发

#### 8.3.1需求澄清与边界确定

##### 8.3.1.1`输入`

\- 目标功能：自定义活动落地页。

\- 约束：老技术栈（Java 8 + Spring + Dubbo + MyBatis）、模块化 Maven 工程。

\- 规则：优先按 OpenSpec / Superpowers 工作方式组织产物。

##### 8.3.1.2 关键决策

\- 后台保存接口统一为 `POST + application/x-www-form-urlencoded + modulesJson`，避免 GET 长 URL 风险。

\- C 端 `dudian-app-mall` 不直连数据库，通过 Dubbo API 读取主表/子表。

\- 商品展示字段对齐 `product_list.json` 逻辑，避免两套口径。

##### 8.3.1.3 输出产物

\- 后台实施计划：`docs/superpowers/plans/2026-04-02-custom-activity-backend.md`

\- C 端实施计划：`docs/superpowers/plans/2026-04-02-custom-activity-app-mall-render.md`

#### 8.3.2`规格驱动设计（Spec/Plan）`

##### 8.3.2.1 后台（manage-mall）方案要点

\- DDL：`mall_custom_activity_page` + `mall_custom_activity_module`

\- 代码分层：domain / mapper / service / controller / validator / test

\- 列表与下拉统一关联 `mall_marketing_activity`

\- 保存逻辑采用“按 page_id 全删后批量插入模块”

##### 8.3.2.2 C 端（app-mall）方案要点

\- 新增只读 Dubbo：`MallCustomActivityReadApi`

\- 新增商品保序查询 API：`listProductsByIdsOrderPreserved`

\- 抽取 `ProductListDecorationService` 复用商品填充逻辑

\- 新增 `GET /customActivity/render.json`，并加入 JWT 可选登录路径

##### 8.3.2.3 文档联动

\- `docs/superpowers/specs/*` 与 `openspec/specs/*` 同步方法语义与字段口径

\- 明确模块顺序：`module_type ASC, id ASC`

#### 8.3.3`本次遇到的问题`

##### 8.3.3.1：计划完整但执行闭环不足

\- 现象：两份计划文档任务拆解很细，但多数仍为待勾选状态。

\- 影响：设计很充分，代码落地与验证进度不可见，容易出现“计划完成=开发完成”的错觉。

\- 根因：本轮重点偏向方案产出与结构文档沉淀，未按 task-by-task 持续推进到验证与归档。

##### 8.3.3.2：文档分散，信息重复风险上升

\- 现象：`docs/superpowers/*`、`openspec/*`、`.cursor/doc/ai-context/*` 之间存在语义重叠。

\- 影响：同一事实可能出现多份描述，长期会出现版本漂移。

\- 根因：不同用途文档并行演进，但缺少“单一事实源（SSOT）”声明。

##### 8.3.3.3：跨模块实现链路长，联调成本高

\- 现象：C 端 render 依赖 base-api、product-api、app-mall 三段改动。

\- 影响：任何一段契约变更都可能导致串联回归；排查路径长。

\- 根因：历史分层清晰但跨模块接口多，改动需严格按契约推进。

##### 8.3.3.4：数据口径存在待确认项

\- 现象：`moduleType=4` 推荐商品来源在计划中保留了“有活动商品表/无活动商品表”双分支。

\- 影响：实现时若未先定库表口径，容易产生临时逻辑长期化。

\- 根因：数据库现状与业务规则未在开发前一次性确认。

##### 8.3.3.5：验证策略未标准化沉淀

\- 现象：计划中虽写了编译/冒烟步骤，但缺统一“最小验收脚本清单”。

\- 影响：不同执行者验收粒度不一致，回归质量波动。

\- 根因：尚未形成固定的 AI 开发 DoD（Definition of Done）模板。

#### 8.3.4`已采取或建议的改进动作`

##### 8.3.4.1 流程层（必须）

8.3.4.1.1、执行顺序固定为：`Spec -> Plan -> Task 实施 -> 编译/测试 -> 文档回写 -> 归档`。

8.3.4.1.2、 每完成 1 个 task 必须附一条“可验证证据”（命令、接口返回、截图或日志摘要）。

8.3.4.1.3、计划文档中的 checkbox 作为主进度源，禁止只在聊天中口头同步。

##### 8.3.4.2文档层（必须）

 8.3.4.2.1、规定 SSOT：

   \- 规范基线：`openspec/specs/*`

   \- 团队实践：`docs/team-guides/*`

   \- 结构索引：`docs/project-structure.md`

8.3.4.2.2、在重复主题文档首段加“来源与优先级说明”。

8.3.4.2.3、每次目录新增/迁移，同步更新 `docs/project-structure.md` 第 8 节。

##### 8.3.4.3 技术层（建议）

8.3.4.3.1、 先落 Dubbo API 契约，再落 app-mall Controller，避免前后端接口反复改签名。

8.3.4.3.2、 `moduleType=4` 先完成数据源定稿，再写业务分支；禁止默认长期使用临时方案。

8.3.4.3.3、 抽取 `ProductListDecorationService` 后，补至少 1 个对齐 `product_list` 的回归测试用例。

