---
title: 总览
type: overview
status: active
updated: 2026-05-13
source_count: 18
---

# Overview

本页保存知识库的当前综合结论。
当新来源显著改变综合判断时，应更新本页。

## 当前状态

- 第一篇来源已录入：[[sources/llm-wiki-pattern]]。
- 初始概念/实体图谱已建立并完成交叉链接。
- 第二篇来源已录入：[[sources/claude-code-enterprise-playbook]]，扩展治理与工程实践。
- 第三篇来源已补充：[[sources/openspec-superpowers-practice-guide]]，加入五阶段流水线、场景决策表、dlabel-cloud-mall 实战案例和常见坑模式。（2026-05-11 更新：从微信完整版补充工程化目录详解、TDD-driven schema 配置、AI 编码使用技巧、上下文管理三策略、Obsidian 软链接集成等内容）
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
- 第十四篇来源已录入：[[sources/code-review-graph]]，代码结构图谱工具——用 Tree-sitter 解析代码、SQLite 存储结构关系、MCP 暴露影响面查询，将 AI 代码评审的上下文获取从”全量灌入”推向”先查图再读代码”，平均 token 节省 8.2×。
- 第十五篇来源已录入：[[sources/claude-md-error-rate-reduction]]，CLAUDE.md 行为契约深度分析——Karpathy 4 条规则→Forrest Chang 模板→Mnimiy 12 条扩展（30 代码库/6 周/41%→3%），提炼”行为契约 vs 提示词””提醒 vs 硬约束”两个新概念，提出三层文件结构和”规则来自翻车记录”的迭代方法论。
- 第十六篇来源已录入：[[sources/agents-md-cars-guide]]，AGENTS.md 的 C.A.R.S 组织框架——Commands/Architecture/Restrictions/Standards 四区块，跨工具兼容矩阵（Cursor+Codex+Claude Code 符号链接策略），大项目索引模式（100-120 行概览→`docs/` 子文档树），30-40 行紧凑模板覆盖 90% 日常场景。
- 第十七篇来源已录入：[[sources/vibecoding-tdd-atdd-bdd-ddd-sdd]]，Vibecoding 五大方法论工程化护栏——系统分析 TDD/ATDD/BDD/DDD/SDD 如何为"氛围编程"注入工程纪律，引入分层定位模型（SDD 战略层→DDD 架构层→ATDD+TDD 执行层），首次引入 ATDD 和 SDD（github/spec-kit）两个新概念和 swingerman/atdd 插件实体。
- 第十八篇来源已录入：[[sources/self-evolving-claude-code]]，将 Claude Code 改造为四层自进化系统——认知核心（行为编程 CLAUDE.md）、子智能体（architect/reviewer）、路径作用域规则、进化引擎（记忆+验证+晋升）。引入"免疫系统"隐喻和"规则无验证即愿望"原则，提出 verify 行、验证扫描、规则晋升阶梯和 hooks 结构化执行机制。

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
- Obsidian 软链接模式：通过 Windows symlink 将项目仓库映射到 vault，实现一套文档在 Obsidian 知识库和 IDE 中双端管理，消除手动同步
- AI 编码中的上下文管理七原则：明确目标、精选文件、管理已打开标签、利用非代码上下文、新任务新对话、示例驱动、图像辅助——输入质量决定输出质量
- Context 不足的三种补充策略：Claude-Mem 自动记忆（被动跨会话）→ 会话总结注入（主动注入）→ OpenSpec 永久归档（不可变追溯），三者互补形成完整上下文连续性方案
- OpenSpec config.yaml 四层注入模型：context（共享）→ rules（按 artifact 匹配）→ instruction → template，实现精细化的 AI 行为约束
- 代码结构图谱作为 AI 上下文供应链：Tree-sitter + SQLite 本地图谱 + MCP 查询接口，将"该读什么"从人类选择或全量灌入转变为结构化工具决策
- 影响面分析（blast-radius analysis）：沿调用/导入/测试关系扩散的代码依赖追踪，recall 100% + precision 0.38 的安全侧取舍适合评审场景
- 图谱上下文的规模阈值：大仓库跨文件变更适合图谱裁剪（8.2× 节省），小项目孤立改动不如直接读文件（0.7×）——工具选型要考虑仓库规模
- CLAUDE.md 作为"轻量行为契约"：区别于提示词（控制单次对话），行为契约是仓库级的跨会话工作约定——把 Agent 的翻车模式写成下次开工前能读懂的约定
- 提醒 vs 硬约束的分工：CLAUDE.md 是事前提醒（"应该怎么做"），hooks/权限/CI/lint 是硬约束（"能不能这么做"）——两者不可混淆，也不能互相替代
- CLAUDE.md 的 Token 预算管理：规则会消耗上下文窗口，200 行以内为宜；三层文件结构（80-120 行根文件→项目事实→任务流程按需索引）避免大杂烩
- Karpathy 4 条规则的工程分类：12 条规则可重组为 4 类——控制改动半径、把确定性交还给代码、长任务留检查点、失败显性化——本质是一组 Harness 薄层控制点
- C.A.R.S 结构作为 AGENTS.md 的实用组织框架：Commands 写死命令防低级错误，Restrictions（不能做什么）是最高价值区块，Architecture 精确到补丁版本，Standards 覆盖日常协作习惯
- 跨工具 AGENTS.md 兼容策略：以 AGENTS.md 为单一事实来源，Claude Code 符号链接接入、Cursor `.cursor/rules` 补充、Codex 多层级支持——消除多套文档漂移
- AGENTS.md 索引模式：超 300 行时 AGENTS.md 退化为 100-120 行目录索引，详细内容下放到 `docs/` 子目录树（adr/、conventions/、workflows/、patterns/、gotchas.md）
- Vibecoding 五大方法论协同：SDD 提供战略规格 → DDD 提供架构边界 → ATDD/BDD 提供验收约束 → TDD 提供实现纪律，让"靠感觉编码"进化为"有护栏、可追溯、可重复"的工程化范式
- ATDD 作为 Vibecoding 最高层验收约束：纯领域语言的 Given-When-Then 规格禁止实现细节泄露，双流测试（WHAT + HOW）+ 变异测试构成三层验证
- SDD 规格即真理：github/spec-kit 的 constitution.md + spec.md + plan.md + tasks.md 将规格提升为唯一事实来源，与 Superpowers（工作流即真理）互补
- Vibe Coding 术语双层含义：底层编码方式（Karpathy，沉浸式自然语言驱动）vs 上层研发范式（企业实践，A/B 测试驱动 UI 优化），两者共享"低摩擦"特质但应用层次不同
- 自进化 Agent 系统：四层架构（认知核心→子智能体→路径作用域规则→进化引擎）将 AI 编码工具从静态配置改造为持续自我改进系统
- "规则无验证即愿望"原则：每条已学规则必须附带机器可检查的 `verify:` 行——没有验证的规则是愿望，有验证的规则才是护栏，只有护栏才能存活
- 验证扫描作为结构性执行：会话启动时自动运行所有规则的 verify 检查，全通过时静默，只在违规时报告——最好的免疫系统是无形的
- 规则晋升阶梯：纠正 1 次→记录→纠正 2 次同模式→自动晋升 learned-rules→10+ 会话通过→候选永久配置——量化驱动的规则生命周期管理
- hooks 从安全提醒升级为结构性执行：SessionStart/PreToolUse/Stop 三个 hooks 构成进化循环骨架，"让一切变成结构性的而非依赖 agent 的自觉性"
- 路径作用域规则实现上下文精简：`.claude/rules/` 通过 frontmatter paths 字段限定加载范围，编辑 CSS 时不读 200 行安全规范
- CLAUDE.md "行为编程"视角：不只是约束行为的契约，更是塑造 agent 认知的代码——包含决策框架（先 grep→评估影响→最小改动→验证计划）和进化协议
- 与内置 /memory 的区别：自动记忆是便签本，自进化系统增加了验证检查、晋升阶梯和会话评分——"自动记忆记住事情，这套系统执行它们"

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
  - [[sources/code-review-graph]]
  - [[sources/claude-md-error-rate-reduction]]
  - [[sources/agents-md-cars-guide]]
  - [[sources/vibecoding-tdd-atdd-bdd-ddd-sdd]]
  - [[sources/self-evolving-claude-code]]

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
- code-review-graph 的 Tree-sitter 解析失败降级策略——不支持的语法或解析错误时如何处理？
- 代码结构图谱在大型 monorepo 中的文件大小和查询延迟——是否存在规模瓶颈？
- 影响面分析能否扩展到自定义关系类型（数据流、依赖注入、配置依赖）？
- code-review-graph 与 GitNexus（文中提到的关联项目）的能力差异——各自适合什么场景？
- Mnimiy 的 30 代码库实验可否独立复现？评判标准和代码库分布是什么？
- 「架构师」公众号系列文章（Cursor Harness 方法论、长周期 Agent、Martin Fowler 研发提醒等）是否值得逐一录入？
- Mitchell Hashimoto《My AI Adoption Journey》全文是否值得作为独立来源深度录入？
- "三层文件结构"在不同仓库规模（个人/小团队/大型 monorepo）下的最佳实践和行数分配？
- "规则会过期"的维护节奏——多久一轮审查？谁来判断规则是否已失效？
- 文末引用的 2 篇 AGENTS.md 学术论文（arxiv 2602.11988、2601.20404）对 repo-level context file 的定量评估结果如何？
- 「架构师」公众号 20 篇系列前作（Harness 方法论、长周期 Agent、Claude Skills、Cowork 安全架构等）中哪些值得优先录入？
- SDD（github/spec-kit）与 OpenSpec 的实质差异——两者是互换还是互补？
- ATDD 的"纯领域语言"约束在复杂业务场景中的可维护性——领域专家能否直接编写和维护 ATDD 规格？
- swingerman/atdd 的变异测试在 AI 生成代码上的实际效果——AI 代码更容易还是更难被变异测试捕获缺陷？
- DDD 的限界上下文如何与 AI 编码工具结合——AI 是否能自动识别和遵守架构边界？
- Vibecoding "126% 生产力提升"数据的原始来源和实验条件。
- 150 行 CLAUDE.md 限制的实验依据——不同模型版本的指令遵从度阈值是否一致？
- 自动晋升机制（2 次纠正 → 永久规则）的误晋升率和回滚策略。
- 进化系统的验证扫描在 50 条规则上限时的启动延迟——大型仓库中是否可接受？
- 进化引擎与 Superpowers 的 hooks 系统能否共存——两套 hooks 是否冲突？
- CLAUDE.md "行为编程"视角与既有"行为契约"视角的精确区别——两者是否应合并为一个概念？
