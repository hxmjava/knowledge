---
title: 总览
type: overview
status: active
updated: 2026-05-11
source_count: 13
---

# Overview

本页保存知识库的当前综合结论。
当新来源显著改变综合判断时，应更新本页。

## 当前状态

- 第一篇来源已录入：[[sources/llm-wiki-pattern]]。
- 初始概念/实体图谱已建立并完成交叉链接。
- 第二篇来源已录入：[[sources/claude-code-enterprise-playbook]]，扩展治理与工程实践。
- 第三篇来源已补充：[[sources/openspec-superpowers-practice-guide]]，加入五阶段流水线、场景决策表、dlabel-cloud-mall 实战案例和常见坑模式。
- 第四篇来源已录入：[[sources/ai-template2-scaffold]]，引入具体的多模块 AI 协作脚手架，包括分层 agents、专项检查技能、TDD 硬门禁和生命周期 hooks。
- 第五篇来源已录入：[[sources/claude-mem]]，加入持久化 agent 记忆、渐进式披露检索，以及围绕 Claude Code 的本地记忆基础设施。
- 第六篇来源已录入：[[sources/ai-coding-advanced-openspec-superpowers-deep-guide]]，把 OpenSpec + Superpowers 从”方法组合”推进到”教程化落地”，补充 `/opsx:ff → verify → archive` 端到端路径、购物车案例、失败路径修复思路和按需加载 skills 的实践口径。
- 第七篇来源已录入：[[sources/claudian-obsidian-plugin]]，引入 vault-native AI 的具体实现——Claudian 插件将 Claude/Codex 直接嵌入 Obsidian 笔记库，配合结构化标签体系，使笔记成为 AI 的原生工作上下文。
- 第八篇来源已录入：[[sources/superpowers-workflow-deconstruction]]，将 Superpowers 的 14 个 skill 解析为四层架构并提炼两条主链路（功能开发链、调试链），新增”verification-before-completion”概念——将完成声明与新鲜验证结果强制绑定。
- 第九篇来源已录入：[[sources/agents-md-guide]]，系统化 AGENTS.md 的编写实践——“地图而非手册”原则（约 200 行导航地图）、五大实践（仓库聚合、统一环境配置、验证闭环、自动化检查、参考项目引入）、Bad Case 驱动迭代方法论，以及 harness-creator 一键脚手架工具。
- 第十篇来源已录入：[[sources/figma-personal-access-tokens]]，Figma 官方 PAT 管理文档——展示了外部设计工具 API 令牌的”全有或全无”安全模型，为权限粒度讨论提供反面参考，并为设计-to-code 管道中的令牌治理提供基线认知。
- 第十一篇来源已录入：[[sources/fireworks-tech-graph]]，Claude Code Skill 生态向非代码产出领域扩展的案例——声明式技术图生成（自然语言→SVG/PNG），14 种图类型 × 7 种视觉风格，五层架构含语义表达和输出验证，展示了 Skill 从代码质量检查到领域特化内容生成的边界。
- 第十二篇来源已录入：[[sources/superpowers-deep-practice-guide]]，Superpowers 的全面深度实战指南——覆盖架构全景、8 个平台安装配置、14 个 skill 逐一深度解析、插件系统技术细节（跨平台 hook 机制、版本管理）、技能设计哲学（铁律模式、合理化防范、CSO 搜索优化）和完整 React Todo List 实战示例。
- 第十三篇来源已录入：[[sources/ai-coding-paradigms-618-practice]]，企业级 AI Coding 多范式组合实战——以618促销项目为场景，系统化对比五种研发范式（Spec Coding、TDD、Glue Coding、Harness、Vibe Coding），首次引入”范式组合策略”和”资产复用驱动效率”视角，为 AI Coding 工作流增加了方法论维度的讨论。

## 活跃主题

- LLM 辅助的增量知识编译
- 将持久 wiki 维护作为复利型工作流
- 用 schema 驱动 agent 行为，保持操作一致性
- 面向 AI 编码的团队治理、权限控制和 CI/CD 自动化
- 规格优先开发（OpenSpec）与执行治理（Superpowers）结合
- 用 fast-forward 入口降低规范工作流首次采用门槛，同时保留 verify/archive 收口
- 基于场景选择工作流：核心模块走完整链路，热修走最小流程
- 单一事实来源（SSOT）纪律，避免文档版本漂移
- 分层项目 harness：common/service/app/message 配套专属 agents 和验证策略
- 将 TDD 作为硬门禁：生产代码遵循 Red-Green-Refactor，并有显式例外流程
- 生命周期 hooks 作为轻量安全网（fail-open，仅提醒）
- 持久化 agent 记忆支撑跨会话连续性
- 渐进式披露检索在记忆深度与上下文成本之间取得平衡
- 失败路径修复手册与边界条件清单，帮助把”流程存在”推进到”流程真能落地”
- Vault-native AI 助手：将 AI 嵌入笔记工作区，笔记库直接成为上下文
- 面向 AI 的结构化标签体系：标签质量决定 AI 回答质量
- Superpowers 四层架构与两条主链路：14 个 skill 不是平铺工具，而是分层工程系统
- verification-before-completion：完成声明必须绑定新鲜验证结果，比 TDD 管控更靠后的交付关口
- "地图，而非手册"（Map, not Manual）：AGENTS.md 约 200 行导航地图，详细内容通过链接指向专项文档
- 验证闭环：「改 → 构建 → 启动 → 验证」端到端循环，夜间 Agent 自主执行的前提
- Bad Case 驱动迭代：不一次写完 AGENTS.md，从 AI 实际犯错的地方逐条补充规则
- 参考项目引入：源码即文档，通过 git submodule 引入闭源/私域组件源码作为 AI 上下文
- 外部工具 PAT 的权限模型对比：Figma 全量 PAT vs Claude Code 细粒度 Allow/Ask/Deny，理解不同平台在安全-便利权衡上的不同选择
- Skill 生态的非代码扩展：Claude Code Skill 不限于代码质量检查，可封装领域特化的非代码产出（如技术图生成）
- 声明式技术图生成：用自然语言描述系统→AI 自动识别图类型→风格化渲染→发布级输出，从手工绘图到工程化生产流水线
- Superpowers 的"铁律"模式与"合理化防范"机制：三层防线（Iron Law + Red Flags + Common Rationalizations）预堵代理在压力下的合理化路径
- 多平台插件适配模式：一套 skills + 平台特化装配层（hook / 插件 transform / 上下文文件），统一行为约束模型而非单一技术接入点
- CSO（Claude 搜索优化）：技能 description 只写触发条件、动词优先命名、第三人称撰写，优化代理的技能发现路径
- AI Coding 多范式组合：同一项目不同阶段可灵活切换范式——Spec Coding 定需求、TDD 保核心、Glue Coding 提效率、Harness 自动化、Vibe Coding 优体验
- 资产复用作为效率杠杆：Reference 代码复用率达 70% 时，核心功能开发周期可缩短 60%
- Vibe Coding 在企业级场景的价值：A/B 测试驱动的 UI 优化在促销活动页面可带来约 10 个百分点的转化率差异

## 证据基础

- 当前来源集合：
  - [[sources/llm-wiki-pattern]]
  - [[sources/claude-code-enterprise-playbook]]
  - [[sources/openspec-superpowers-practice-guide]]
  - [[sources/ai-template2-scaffold]]
  - [[sources/claude-mem]]
  - [[sources/ai-coding-advanced-openspec-superpowers-deep-guide]]
  - [[sources/claudian-obsidian-plugin]]
  - [[sources/superpowers-workflow-deconstruction]]
  - [[sources/agents-md-guide]]
  - [[sources/figma-personal-access-tokens]]
  - [[sources/fireworks-tech-graph]]
  - [[sources/superpowers-deep-practice-guide]]
  - [[sources/ai-coding-paradigms-618-practice]]

## 开放线索

- 对比个人知识编译模式与企业治理约束。
- 确定小团队权限与审计的最低基线策略。
- 定义触发完整规格驱动执行链路的任务规模阈值。
- 定义自动捕获 agent 记忆的隐私、修剪和审计规则。
- 核实 `OpenSpec` 默认命令集与教程中 `/opsx:ff`、`verify` 的差异来源，避免把脚手架命令误当成官方默认命令。
- Claudian 对大型 vault 的上下文处理策略：是否支持检索增强（RAG）而非全量注入？
- Claudian vs Obsidian Copilot vs Smart Connections：vault-native AI 插件的架构对比。
- 标签体系标准化：是否值得建立可复用的标签设计模板？
- AGENTS.md 的 200 行建议在大型 monorepo（如 OpenAI 88 个嵌套 AGENTS.md）中的适用性。
- harness-creator 生成质量评估：是否需要人工大幅修正，支持哪些技术栈。
- "源码即文档"策略在 AI 上下文窗口有限时的检索效率问题。
- 验证闭环基础设施（启动脚本、curl 模板、lint 脚本）的最小可行子集是什么？
- Figma PAT 的 scope 细粒度：Figma 文档声称支持 scope 赋值但又说"全量访问"，需查阅 developer docs 确认实际支持的权限边界。
- 设计-to-code AI 管道中 Figma API 令牌的安全最佳实践：是否应使用 OAuth App 替代 PAT？
- fireworks-tech-graph 图类型识别准确率与混合类型支持情况。
- 声明式图生成在大型系统（20+ 组件）中的 SVG 布局质量评估。
- Claude Code Skill 生态中还有哪些非代码产出领域值得封装为 Skill（如文档翻译、幻灯片生成）。
- Superpowers 8 个平台的安装支持成熟度：Factory Droid 和 GitHub Copilot CLI 是否经过充分验证？
- `run-hook.cmd` 静默退出机制的工程合理性：Windows 环境下丢失注入能力却不告知用户是否可接受？
- Superpowers 技能词数约束（<150/<200/<500）在实际仓库中的遵守情况。
- "合理化防范"机制（Red Flags + Rationalizations 表）是否值得抽象为独立的技能设计模板，供自定义技能使用。
- Glue Coding 的技术债务管理策略——"快速复用"与"债务积累"之间缺少明确的重构触发点。
- Vibe Coding 在低流量场景的适用性——A/B测试需要足够样本量才能得出统计显著结论。
- 五范式是否覆盖了所有企业级AI Coding场景，是否存在遗漏范式（如文档生成、测试数据生成）。
- 范式组合的切换触发条件——团队如何判断当前阶段应切换到哪种范式？
