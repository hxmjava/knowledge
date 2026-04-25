# ai_template2：多模块项目 AI 协作脚手架

## 1. 项目概述

ai_template2 是一个面向多模块 Java 项目的 AI 协作脚手架模板，将 OpenSpec（规范层）、Superpowers（纪律层）和 Claude Code Harness（协作层）整合为一套可落地的工程实践。

核心定位：**项目地图 + AI 执行入口**，让 AI 快速理解工程结构与模块边界，让业务代码、AI 协作配置、规格文档三类资产各归其位。

## 2. 核心设计

### 2.1 分层架构

| 层次 | 管什么 | 本仓主要落点 | 对 Agent 的期望 |
| -- | -- | -- | -- |
| 规范层（OpenSpec） | 做什么：需求、接口、验收 | `openspec/` | 以 spec/任务清单为单一事实来源 |
| 纪律层（Superpowers） | 怎么做：计划、TDD、审查、完成前验证 | `plugins/superpowers/skills/` | 按任务类型按需加载技能 |
| 协作层（Harness） | 谁来做、如何并行、如何兜底 | `.claude/`、AGENTS.md、分层目录约束 | 先判断改动落在哪一层，再动手 |

**调用链**：读取 OpenSpec 变更或规格 → 按 AGENTS.md 划定模块与风险 → 用 Superpowers/项目规则约束实现过程 → 用构建工具做硬门禁 → 回到 OpenSpec 做验收或归档。

### 2.2 项目分层（占位变量）

脚手架使用 `{{LAYER_COMMON}}`、`{{LAYER_MESSAGE}}`、`{{LAYER_SERVICE}}`、`{{LAYER_APP}}` 占位符，实际项目替换为真实模块名（如 `manage-mall-common`、`manage-mall-service` 等）。

依赖方向：
```
app --> service(api / impl) --> common
message --> service(api) / common
service impl --> service api + common
```

### 2.3 TDD 铁律

`proj-change-apply` 命令要求严格执行 TDD Red-Green-Refactor 循环：

1. **RED** — 写最小失败测试，确认因功能缺失而失败
2. **GREEN** — 写最少生产代码使测试通过
3. **REFACTOR** — 全绿状态下整理代码，再次跑测试
4. 严禁一次性批量生成生产代码再补测试

若模块无测试基建，自动切换到 `/proj-test-bootstrap` 搭骨架。TDD 豁免需显式征得用户确认并记录原因。

## 3. Claude Code 工作流资产

### 3.1 斜杠命令（9 个）

| 命令 | 用途 |
|------|------|
| `/proj-dev` | 日常开发入口：定位层→选路径→暴露风险→同步规格→验证→终审 |
| `/proj-onboard` | 新人上手指南：根据场景推荐最佳入口命令 |
| `/proj-module-locate` | 模块定位：判断改动属于哪层哪模块 |
| `/proj-change-apply` | OpenSpec 变更实现：绑定 TDD 铁律、分层映射、规格同步 |
| `/proj-spec-sync` | 规格同步：实现偏离时同步 proposal/design/tasks/spec |
| `/proj-verify` | 验证收口：推荐或执行最小足够验证命令 |
| `/proj-review-risk` | 风险评审：针对高风险路径的专项审查 |
| `/proj-review-complete` | 完成评审：终验门，检查层/规格/验证/风险 |
| `/proj-test-bootstrap` | 测试基建搭建：为无测试模块搭最小骨架 |

### 3.2 分层 Agent（4 个）

| Agent | 职责范围 | 自带技能 |
|-------|---------|---------|
| proj-app-agent | `{{LAYER_APP}}` 层：Controller/Web/Job/Callback | build-module-verifier, xml-config-checker |
| proj-common-agent | `{{LAYER_COMMON}}` 层：共享实体/Mapper/工具 | orm-change-checker, xml-config-checker |
| proj-service-agent | `{{LAYER_SERVICE}}` 层：领域接口与实现 | api-change-checker, build-module-verifier |
| proj-message-agent | `{{LAYER_MESSAGE}}` 层：MQ 消费链路 | message-consumer-checker |

### 3.3 专项检查技能（6 个）

| 技能 | 触发条件 | 检查维度 |
|------|---------|---------|
| api-change-checker | 改动 `*-api` 目录 | 接口签名、DTO 契约、下游调用者、RPC 配置 |
| orm-change-checker | 改动实体/Mapper/XML | 一致性链（entity→mapper→XML）、共享影响 |
| xml-config-checker | 改动 resources/** | DI 接线、RPC 暴露、ORM 扫描、日志/打包 |
| message-consumer-checker | 改动消息消费模块 | 重试、幂等、异常处理、排序语义 |
| build-module-verifier | 询问验证范围 | 最小足够验证命令选择、升级触发条件 |
| test-bootstrap | 模块无测试基建 | 测试框架依赖、目录结构、冒烟测试、验证 |

### 3.4 Hooks 系统

通过 `.claude/hooks/scripts/hooks.py` 实现四生命周期钩子：

| Hook | 触发时机 | 行为 |
|------|---------|------|
| PreToolUse | Edit/Write/Bash 执行前 | 命中高风险路径时注入提醒；记录构建命令 |
| PostToolUse | Bash 执行后（成功） | 记录构建验证摘要 |
| PostToolUseFailure | Bash 执行后（失败） | 记录失败摘要 |
| Stop | 对话结束 | 检查高风险改动是否已验证；提醒 OpenSpec 归档 |

hook 默认 fail-open，不阻塞 Claude Code，只做轻量提醒。

## 4. Cursor 资产

- **14 个 Superpowers 命令**：brainstorming、writing-plans、executing-plans、subagent-driven-development、TDD、systematic-debugging、code-review 等
- **4 个 OpenSpec 技能**：openspec-explore/propose/apply/archive
- **3 个 AI 上下文文档**：architecture.md、coding-standards.md、project-structure.md
- **9 个提示词模板**：review、fix、debug、optimize、arch、api、sql、trace、compact
- **1 条规则**：skills-create-slash-command.mdc

## 5. OpenSpec 配置

- `config.yaml`：`schema: spec-driven`
- `project.md`：项目上下文（占位模板，含模块结构、依赖关系、高风险区、编码约束、构建验证、写作建议）

## 6. 高风险区域

以下区域变更需提高审查等级并附验证说明：

- 根构建文件（pom.xml / build.gradle / package.json）
- `{{LAYER_COMMON}}/**`：共享实体、Mapper、工具类
- `{{LAYER_SERVICE}}/**/api/**`：对外接口定义
- `{{LAYER_SERVICE}}/**/resources/**`：Spring/Dubbo/MyBatis 配置
- `{{LAYER_APP}}/**/resources/**`：应用启动、Web 配置
- `{{LAYER_MESSAGE}}/**`：消费链路、重试、幂等
- `.cursor/**`、`.claude/**`、`openspec/**`

## 7. 维护规则

以下变化发生时同步更新 AGENTS.md：

- 根构建文件的模块聚合结构变化
- 一级/二级子模块新增、重命名、删除
- 模块分层职责变化
- 核心验证命令变化
- AI 协作入口变化
- 高风险区域发生新增或迁移

## 8. 设计原则

- 单一事实来源：需求与验收以 openspec/ 为准
- 不同业务域无耦合时可并行；触及 common 层应串行
- 改动高风险区必须写明执行的构建命令及结果
- 与 OpenSpec 绑定的任务：「实现完成」≠「变更完成」
- 连续验证失败、依赖不清、跨模块影响过大时，先停下升级讨论
