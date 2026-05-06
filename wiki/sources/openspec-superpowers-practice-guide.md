---
title: OpenSpec + Superpowers 规范开发指南
type: source
status: active
updated: 2026-04-24
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

**遇到的问题与改进**：

1. **计划完整但执行闭环不足**：设计充分但代码落地进度不可见 → 固定执行顺序为 Spec → Plan → Task → 编译/测试 → 文档回写 → 归档，每 task 必须附可验证证据。
2. **文档分散，版本漂移风险**：`docs/`、`openspec/`、`.cursor/doc/ai-context/` 语义重叠 → 规定 SSOT：规范基线 `openspec/specs/*`，团队实践 `docs/team-guides/*`，结构索引 `docs/project-structure.md`。
3. **跨模块联调成本高**：C 端 render 依赖 base-api、product-api、app-mall 三段改动 → 先落 Dubbo API 契约，再落 Controller。
4. **数据口径待确认**：`moduleType=4` 推荐商品来源双分支未定 → 先完成数据源定稿，再写业务分支。
5. **验证策略未标准化**：缺统一"最小验收脚本清单" → 形成固定的 AI 开发 DoD 模板。

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

## Follow-up Questions

- 哪些任务特征（规模、影响面、风险）应触发完整 Superpowers 链路？
- 在你们仓库，`openspec/changes` 与 `archive` 的分层是否已有正式迁移规范？
- 如何沉淀统一的 DoD（Definition of Done）模板供 AI 开发使用？

## Related

- [[openspec-schema-tdd-workflow-injection]] — 专题实测：用 OpenSpec 自定义 schema 注入 TDD 纪律到编码工作流，结论是 propose 阶段有效、apply 阶段 TDD 循环未生效
