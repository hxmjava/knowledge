# Wiki Log

Append-only operational timeline.

## [2026-05-13] ingest | Claude Code 自进化系统完整指南

### Scope

- 保存 raw 来源: `raw/sources/self-evolving-claude-code.md`
- 新增来源页面: `wiki/sources/self-evolving-claude-code.md`
- 新增实体页面: `wiki/entities/meta-alchemist.md`, `wiki/entities/engineer-juggling.md`
- 新增概念页面: `wiki/concepts/self-evolving-agent-system.md`, `wiki/concepts/verification-sweep.md`, `wiki/concepts/rule-promotion-ladder.md`
- 更新实体页面: `wiki/entities/claude-code.md`（补充自进化系统四层架构、子智能体模式、路径作用域规则、hooks 结构化执行、150 行限制）
- 更新概念页面: `wiki/concepts/persistent-agent-memory.md`（补充结构化记忆变体对比表）、`wiki/concepts/behavioral-contract-vs-prompt.md`（补充"行为编程"视角和决策框架）、`wiki/concepts/hooks-as-safety-net.md`（补充"结构性执行"升级和三个 hooks 对比表）、`wiki/concepts/verification-before-completion.md`（补充"所有规则需验证"泛化）、`wiki/concepts/context-and-cost-optimization.md`（补充路径作用域规则和 core-invariants 压缩防护）、`wiki/concepts/map-not-manual.md`（补充 150 行限制和 50 行 learned-rules 上限）、`wiki/concepts/specialized-agent-pattern.md`（补充 architect/reviewer 子智能体变体）、`wiki/concepts/bad-case-driven-iteration.md`（补充免疫系统方法对比表）
- 更新 hub 页面: `wiki/overview.md`, `wiki/index.md`, `wiki/log.md`, `wiki/tasks/backlog.md`

### Outcomes

- 完成微信公众号「工程师耍杂技」文章「如何把 Claude Code 改造成一个自进化系统：完整指南」（一天天的/Meta Alchemist）的录入。
- 引入**自进化 Agent 系统**概念——四层架构（认知核心 CLAUDE.md + 子智能体 architect/reviewer + 路径作用域 rules/ + 进化引擎 memory/），核心隐喻是"免疫系统"而非日记本。
- 引入**验证扫描机制**——每条 learned-rules 必须附带 `verify:` 机器可检查行，会话启动时自动执行，全通过时静默。首要原则："没有验证检查的规则是愿望，有验证检查的规则才是护栏。只有护栏才能存活。"
- 引入**规则晋升阶梯**——量化驱动的规则生命周期：纠正 1 次→记录→纠正 2 次同模式→自动晋升 learned-rules→10+ 会话持续通过→候选永久配置。`learned-rules.md` 50 行硬上限，强制晋升或淘汰。
- 将 hooks 定位从"安全提醒（fail-open）"升级为"结构性执行"——SessionStart 注入验证扫描、PreToolUse 检查路径规则、Stop 记录会话评分，"让一切变成结构性的而非依赖 agent 的自觉性"。
- 提出"行为编程"视角——CLAUDE.md 不只是约束行为的契约，更是塑造 agent 认知的代码，包含决策框架（先 grep→评估影响→最小改动→验证计划）和进化协议。
- 提出 CLAUDE.md 150 行以内限制（"超过 150 行指令遵从度下降"），与既有 200 行建议的差异来自 Commands/Architecture 是否计入。
- 路径作用域规则实现上下文精简：`.claude/rules/` 通过 frontmatter `paths:` 字段限定加载范围，`core-invariants.md`（路径 `*/`）在每次工具调用时重新注入——压缩防护。
- 为 Meta Alchemist（一天天的）和「工程师耍杂技」公众号创建实体页，继续扩展来源多元化。
- 与 Claude Code 内置 `/memory` 的关键区别："自动记忆记住事情，这套系统执行它们。"
- 与现有 wiki 的张力：150 行 vs 200 行、"行为编程" vs "行为契约"、自动晋升（2 次纠正→永久规则）vs bad case 驱动（人工判断）。

### Open Questions / Next Actions

- 150 行 CLAUDE.md 限制的实验依据——不同模型版本的指令遵从度阈值是否一致？
- 自动晋升机制（2 次纠正→永久规则）的误晋升率和回滚策略。
- 验证扫描在 50 条规则上限时的启动延迟——大型仓库中是否可接受？
- 进化引擎与 Superpowers 的 hooks 系统能否共存——两套 hooks 是否冲突？
- CLAUDE.md "行为编程"与"行为契约"是否应合并为一个概念——精确区别是什么？
- `verify: manual` 规则在实际使用中的占比——无法自动检查的行为规则如何保证执行？
- 「工程师耍杂技」公众号是否有更多相关文章可供录入。

---

## [2026-05-13] ingest | Vibecoding 五大方法论工程化护栏

### Scope

- 保存 raw 来源: `raw/sources/vibecoding-tdd-atdd-bdd-ddd-sdd.md`
- 新增来源页面: `wiki/sources/vibecoding-tdd-atdd-bdd-ddd-sdd.md`
- 新增实体页面: `wiki/entities/github-spec-kit.md`, `wiki/entities/swingerman-atdd.md`, `wiki/entities/gis-in-frontend.md`
- 新增概念页面: `wiki/concepts/atdd-for-ai-coding.md`, `wiki/concepts/bdd-for-ai-coding.md`, `wiki/concepts/ddd-domain-driven-design.md`, `wiki/concepts/sdd-spec-driven-development.md`
- 更新概念页面: `wiki/concepts/vibe-coding.md`（补充 Karpathy 原始定义、双层术语含义）、`wiki/concepts/tdd-as-hard-gate.md`（补充 AI 提示词视角和双流测试定位）、`wiki/concepts/spec-driven-workflow-and-review-discipline.md`（补充 SDD 交叉引用）
- 更新实体页面: `wiki/entities/superpowers.md`（补充五大方法论中 TDD 执行纪律定位）
- 更新 hub 页面: `wiki/overview.md`, `wiki/index.md`, `wiki/log.md`, `wiki/tasks/backlog.md`

### Outcomes

- 完成微信公众号「GIS人在前端」文章「AI Vibecoding 工程化护栏：TDD、ATDD、BDD、DDD、SDD 五大方法论协同实践」（2026-05-08）的录入。
- 首次引入 **ATDD（验收测试驱动开发）** 概念——纯领域语言的 Given-When-Then 规格作为 AI 代码生成的最高层行为约束，禁止实现细节泄露，AI 约束强度最强。代表工具为 swingerman/atdd 插件（Uncle Bob 风格，含 /atdd:atdd、/atdd:spec-check、/atdd:mutate 命令）。
- 首次引入 **SDD（规格驱动开发）** 概念——规格（Specification）作为唯一事实来源，代码只是规格的表达。代表工具为 github/spec-kit（constitution.md + spec.md + plan.md + tasks.md）。与 OpenSpec 理念相近但定位不同（SDD "规格即真理" vs OpenSpec "规格先行+变更追踪"）。
- 补充 **DDD（领域驱动设计）** 和 **BDD（行为驱动开发）** 概念——DDD 通过统一语言和限界上下文为 AI 提供架构护栏；BDD 通过活文档和统一语言实现跨角色协作。
- 提出**五大方法论分层定位模型**：SDD（战略层：做什么）→ DDD（架构层：怎么组织）→ ATDD+TDD（执行层：怎么验证）→ BDD（协作层：谁来协作）。
- 澄清了 **Vibe Coding 术语的双层含义**：底层编码方式（Karpathy，沉浸式自然语言驱动）vs 上层研发范式（企业实践，A/B 测试驱动 UI 优化），两者共享"低摩擦"特质但应用层次不同。
- 新增 3 个实体页（github/spec-kit、swingerman/atdd、GIS人在前端）和 4 个概念页（ATDD、BDD、DDD、SDD），扩展了方法论维度的知识图谱。
- 与现有 wiki 的连接：[[concepts/tdd-as-hard-gate]]（TDD 执行层）、[[concepts/vibe-coding]]（Vibe Coding 定义修正）、[[concepts/spec-driven-workflow-and-review-discipline]]（SDD vs OpenSpec）、[[concepts/spec-coding]]（文档先行范式）、[[entities/superpowers]]（TDD 执行纪律）。

### Open Questions / Next Actions

- SDD（github/spec-kit）与 OpenSpec 的实质差异是什么？两者是否可以互换还是互补？
- ATDD 的"纯领域语言"约束在复杂业务场景中的可维护性——领域专家能否直接编写和维护规格？
- swingerman/atdd 的变异测试在 AI 生成代码上的实际效果和性能开销。
- DDD 的限界上下文如何与 AI 编码工具结合——AI 是否能自动识别和遵守架构边界？
- Vibecoding "126% 生产力提升"数据的原始来源和实验条件。
- 「GIS人在前端」公众号是否有更多与 AI 编码方法论相关的文章可供录入。

---

## [2026-05-12] ingest | AGENTS.md C.A.R.S 实践指南

### Scope

- 保存 raw 来源: `raw/sources/agents-md-cars-guide.md`
- 新增来源页面: `wiki/sources/agents-md-cars-guide.md`
- 新增实体页面: `wiki/entities/miao.md`, `wiki/entities/fatcat-learn-ai.md`
- 新增概念页面: `wiki/concepts/cars-agents-structure.md`, `wiki/concepts/cross-tool-agents-compatibility.md`
- 更新实体页面: `wiki/entities/agents-md.md`（补充 C.A.R.S 结构、跨工具兼容、索引模式）、`wiki/entities/claude-code.md`（补充来源引用）
- 更新概念页面: `wiki/concepts/map-not-manual.md`（补充行数建议光谱和索引模式详细结构）、`wiki/concepts/bad-case-driven-iteration.md`（补充"演进式更新，而非一次性编写"）
- 更新 hub 页面: `wiki/overview.md`, `wiki/index.md`, `wiki/log.md`

### Outcomes

- 完成微信公众号「肥喵学AI」文章「如何构建一个好的 AGENTS.md：AI 编码 Agent 的项目级行为规范最佳实践」（米奥，2026-05-09）的录入。
- 引入 **C.A.R.S 结构**（Commands, Architecture, Restrictions, Standards）——AGENTS.md 的实用组织框架，Restrictions（不能做什么）被认为是最有价值区块，建议编写优先级为 Commands → Restrictions → Architecture → Standards。
- 新增**跨工具兼容**概念——以 AGENTS.md 为单一事实来源（SSOT），Claude Code 通过符号链接接入、Cursor 配合 `.cursor/rules/*.mdc` 补充、Codex 支持多层级，消除多套文档漂移。
- 补充**大项目索引模式**——AGENTS.md 超过 300 行时切换为 100-120 行目录索引，详细内容下放到 `docs/` 子目录树（adr/、conventions/、workflows/、patterns/、gotchas.md）。
- 行数建议光谱：小项目 30-40 行（覆盖 90% 场景）→ 中大型 200-400 行 → 超 300 行切换索引模式（100-120 行 AGENTS.md + docs/ 子文档）。
- 与 [[sources/agents-md-guide]]（Kirito）形成互补：Kirito 从企业级工程实践出发（仓库聚合、验证闭环、参考项目引入），本文从日常使用痛点出发（命令写死、约束优先、跨工具兼容）。
- 为米奥和「肥喵学AI」公众号创建实体页，继续扩展来源多元化。
- 关键数据点：明确写死 pnpm 可杜绝 90% 以上包管理器错误；30-40 行模板覆盖 90% 场景（未经独立验证）。

### Open Questions / Next Actions

- C.A.R.S 结构在非 Web 项目（移动端、数据工程、ML pipeline）中的适用性验证。
- "30-40 行覆盖 90% 场景"和"90% 包管理器错误"的量化方法和场景分布。
- 跨工具兼容矩阵中各工具对 AGENTS.md 的解析深度和注入方式差异——同一份文件在不同工具中的实际效果是否一致。
- Benjamin Crozat 和 Eric 技术圈的原始文章是否值得作为独立来源深度录入。
- 索引模式下 `docs/` 子目录的粒度——adr/、conventions/、workflows/ 三者之间的边界案例和内容示例。

---

## [2026-05-12] ingest | CLAUDE.md 错误率分析与行为契约（剪藏补全）

### Scope

- 从浏览器剪藏 `Clippings/Claude Code 错误率从 41% 到 3%：CLAUDE.md 到底改对了什么？.md` 合并增量信息
- 更新 raw 来源: `raw/sources/claude-md-error-rate-reduction.md`（补充 3 张配图描述、`.claude/` 关联上下文段落、文末 20 篇系列前作列表）
- 更新来源页面: `wiki/sources/claude-md-error-rate-reduction.md`（补充 2 篇 AGENTS.md 学术论文引用、配图描述、系列前作线索）
- 更新 hub 页面: `wiki/overview.md`（补充开放线索）、`wiki/tasks/backlog.md`（补充 2 项待评估任务）、`wiki/log.md`

### Outcomes

- 本次为"同一来源的剪藏补全"操作——文章已于今日早些时候完成首次录入，浏览器剪藏提供以下增量：
  - **3 张文章配图描述**：12 条规则栈图、CLAUDE.md 加载层级图、Claude hooks 生命周期图。
  - **`.claude/` 关联上下文段落**：作者在"三层文件"章节中接续前作的上下文——"CLAUDE.md 不适合做百科全书，它更适合放'每次都值得带上'的东西"。
  - **2 篇 AGENTS.md 学术论文**：`arxiv 2602.11988`（Evaluating AGENTS.md）和 `arxiv 2601.20404`（On the Impact of AGENTS.md Files），首次引入定量评估视角。
  - **20 篇「架构师」公众号系列前作链接**：覆盖 Harness 方法论、长周期 Agent、上下文工作集、Claude Skills、Cowork 安全架构、Claude Agent SDK 等主题，为后续来源多元化提供索引。

### Open Questions / Next Actions

- 2 篇 AGENTS.md 学术论文是否值得作为独立来源深度录入？
- 「架构师」公众号 20 篇系列前作中哪些与 wiki 主题最相关、值得优先录入？

---

## [2026-05-12] ingest | CLAUDE.md 错误率分析与行为契约

### Scope

- 保存 raw 来源: `raw/sources/claude-md-error-rate-reduction.md`
- 下载文章图片: `raw/assets/claude-md-error-rate-reduction-*.png`（3 张）
- 新增来源页面: `wiki/sources/claude-md-error-rate-reduction.md`
- 新增实体页面: `wiki/entities/ruofei.md`, `wiki/entities/jiagoux.md`, `wiki/entities/karpathy.md`, `wiki/entities/forrest-chang.md`, `wiki/entities/mnimiy.md`, `wiki/entities/mitchell-hashimoto.md`
- 新增概念页面: `wiki/concepts/behavioral-contract-vs-prompt.md`, `wiki/concepts/reminders-vs-hard-enforcement.md`
- 更新实体页面: `wiki/entities/claude-code.md`（补充 Karpathy 4 条规则和行为契约视角）
- 更新概念页面: `wiki/concepts/bad-case-driven-iteration.md`（补充行为契约视角和规则会过期），`wiki/concepts/context-and-cost-optimization.md`（补充 CLAUDE.md Token 预算视角），`wiki/concepts/map-not-manual.md`（补充三层文件结构），`wiki/concepts/hooks-as-safety-net.md`（补充提醒 vs 门禁分工）
- 更新 hub 页面: `wiki/overview.md`, `wiki/index.md`, `wiki/log.md`

### Outcomes

- 完成微信公众号「架构师」文章「Claude Code 错误率从 41% 到 3%：CLAUDE.md 到底改对了什么？」（若飞，2026-05-11）的录入。
- 引入两个新概念：
  - **行为契约 vs 提示词**——CLAUDE.md 不是"更好的提示词"，而是仓库级的跨会话行为约束。Tobi Lütke 的 "context engineering" 视角提供理论支撑。
  - **提醒 vs 硬约束**——CLAUDE.md 只能做事前提醒，真正兜底的是 hooks/权限/CI/lint。Mitchell Hashimoto 原则：犯错后要补机制而非只修一次。
- 为 Karpathy（4 条原始规则提出者）、Forrest Chang（开源模板整理者）、Mnimiy（30 代码库扩展实验者）和 Mitchell Hashimoto（"从错误到机制"原则）创建独立实体页。
- 为若飞和「架构师」公众号创建实体页，扩展来源多元化。
- 关键数据点：Mnimiy 实验 30 代码库 / 6 周 / 41%→3%（未经独立复现）。
- 关键洞察：
  - 12 条规则可重组为 4 类工程问题：控制改动半径、把确定性交还给代码、长任务留检查点、失败显性化——本质是 Harness 薄层控制点。
  - 三层文件结构：根 CLAUDE.md（80-120 行高频行为）→ 项目事实文件 → 任务流程文件按需索引。
  - 四类应避免的写法：身份提示、空泛提醒、纯禁止清单、永不过期规则。
  - 好规则来自翻车记录，且会过期——需要定期删除而非不断追加。
- 标注了与现有 wiki 的张力：CLAUDE.md "上下文非硬约束"（本文）vs AGENTS.md 应有自动化检查配套（agents-md-guide）；80-120 行（本文）vs 200 行（map-not-manual）——差异来自定义范围不同。

### Open Questions / Next Actions

- Mnimiy 的 30 代码库实验的评判标准和代码库分布——不同条件结果可能有很大差异。
- 「架构师」公众号系列文章（Cursor Harness、长周期 Agent、Martin Fowler 研发提醒等）是否值得逐一录入。
- Mitchell Hashimoto《My AI Adoption Journey》全文是否值得作为独立来源深度录入。
- 三层文件结构在不同仓库规模下的最佳实践——个人项目是否需要第二层和第三层。
- "规则会过期"的维护节奏和失效判断标准——是否需要建立定期审查机制。
- Karpathy 的 4 条规则是否已演进为更完整的官方建议。

## [2026-05-11] ingest | Code Review Graph 代码结构图谱工具

### Scope

- 保存 raw 来源: `raw/sources/code-review-graph-weixin.md`
- 下载文章图片: `raw/assets/code-review-graph-*.png`（8 张）
- 新增来源页面: `wiki/sources/code-review-graph.md`
- 新增实体页面: `wiki/entities/code-review-graph.md`, `wiki/entities/ai-cheatcode.md`
- 新增概念页面: `wiki/concepts/code-structure-graph-for-ai.md`, `wiki/concepts/blast-radius-impact-analysis.md`
- 更新实体页面: `wiki/entities/claude-code.md`（补充 MCP 接入代码结构图谱的证据）
- 更新概念页面: `wiki/concepts/context-and-cost-optimization.md`（补充图谱驱动的上下文裁剪策略）
- 更新 hub 页面: `wiki/overview.md`, `wiki/index.md`

### Outcomes

- 完成微信公众号「AI作弊码」文章「Code Review Graph：给 AI 代码评审装一张本地图谱」（2026-05-05）的录入。
- 引入"代码结构图谱"概念：Tree-sitter 解析 → SQLite 图谱存储 → MCP 查询接口，将 AI 代码评审的上下文获取从"全量灌入"推进到"先查图再读代码"。
- 新增 blast-radius-impact-analysis 概念——从变更点沿调用/导入/测试链逐层扩散的影响面分析，recall 100% / F1 0.54 的安全侧取舍。
- 关键数据点：平均 token 节省 8.2×，2,900 文件增量索引 < 2 秒，23 种语言支持，MIT License。
- 标注了适用边界：小型单文件变更（express 0.7×）说明图谱有固定开销，需结合仓库规模判断。
- 与现有 wiki 的连接：[[concepts/context-and-cost-optimization]]（图谱作为上下文优化手段）、[[concepts/map-not-manual]]（代码地图 vs 项目导航地图）、[[entities/fireworks-tech-graph]]（同为领域特化工具但定位不同）。

### Open Questions / Next Actions

- Tree-sitter 解析失败时的降级策略——不支持的语法或解析错误如何处理？
- 大型 monorepo 的 `.code-review-graph/` 文件大小和查询延迟——是否存在规模瓶颈？
- 影响面分析能否支持自定义关系类型（数据流、依赖注入、配置依赖）？
- 与 GitNexus（文中提到的关联项目"将整个代码仓库变成知识图谱"）的能力差异待调研。
- 「AI作弊码」公众号是否有更多与本 wiki 主题相关的文章可供录入。

## [2026-05-11] ingest | OpenSpec+Superpowers规范开发指南（微信完整版更新）

### Scope

- 来源：微信公众号文章「Vibe-Coding规范开发」（URL: https://mp.weixin.qq.com/s/-AzJNiWtO5G_Lbv8xl4BVQ），内容已存在于 `Clippings/Vibe-Coding规范开发.md`
- 更新来源页面：`wiki/sources/openspec-superpowers-practice-guide.md`（该文章为既有来源的完整版）
- 新增概念页面：`wiki/concepts/obsidian-project-symlink.md`
- 更新概念页面：`wiki/concepts/context-and-cost-optimization.md`（补充 AI Coding 提示词技巧与 Context 不足三策略）
- 更新 hub 页面：`wiki/overview.md`、`wiki/index.md`

### Outcomes

- 本文章与既有来源 [[sources/openspec-superpowers-practice-guide]] 为同一文章，但微信版更完整。按"更新既有页面，不创建重复来源"原则处理。
- 新增内容板块：
  - **工程化目录详解**（6 个子目录：docs/、openspec/、plugins/、.cursor/、.claude/、.agents/），含具体命令、技能列表和 hooks 配置。
  - **OpenSpec config.yaml TDD-driven schema 示例**：四层注入模型（context → rules → instruction → template）。
  - **七条 AI 编码使用技巧**：明确目标、精选文件、管理标签、非代码上下文、新对话、示例驱动、图像辅助。
  - **Context 不足的三种补充策略**：Claude-Mem 自动记忆 → 会话总结注入 → OpenSpec 永久归档，三者互补。
  - **Obsidian 软链接集成**：Windows symlink 将项目目录映射到 vault，一套文件双端管理。
  - **AI Template 脚手架**（Gitee: hxm0203/ai_template）：快速生成集成 OpenSpec/Superpowers 的项目模板。
- 新增概念 [[concepts/obsidian-project-symlink]]，补充了 Obsidian 生态中项目文档与知识库的桥接模式。
- 更新 [[concepts/context-and-cost-optimization]]，加入 prompt-level context management 视角，将企业级成本控制与日常提示词实践打通。

### Open Questions / Next Actions

- Obsidian 软链接在 macOS/Linux 上的等效方案（`ln -s`），是否需要补充跨平台说明？
- 工程化目录中 `.cursor/rules/`（.mdc 格式）与 `.claude/skills/` 是否可以统一管理规则来源，避免规则碎片化？
- AI Template 脚手架是否值得作为独立来源进行深度评测？

## [2026-05-11] ingest | 企业级AI Coding五范式组合实战

### Scope

- 保存 raw 来源: `raw/sources/ai-coding-paradigms-618-practice.md`
- 新增来源页面: `wiki/sources/ai-coding-paradigms-618-practice.md`
- 新增实体页面: `wiki/entities/lv-zhaobo.md`, `wiki/entities/muran-cloud.md`
- 新增概念页面: `wiki/concepts/spec-coding.md`, `wiki/concepts/glue-coding.md`, `wiki/concepts/vibe-coding.md`, `wiki/concepts/paradigm-composition.md`
- 更新概念页面: `wiki/concepts/tdd-as-hard-gate.md`（补充"基于Spec的TDD"变体），`wiki/concepts/ai-ci-cd-automation.md`（补充Harness范式视角）
- 更新 hub 页面: `wiki/overview.md`, `wiki/index.md`

### Outcomes

- 完成微信文章「1个场景(618促销)5种范式(Spec/Vibe/Glue/TDD/Harness) ，企业级AI Coding经验分享」（沐然云计算/吕昭波，2026-05-10）的录入。
- 首次引入"多范式组合"视角：同一项目不同阶段可灵活切换 Spec Coding → TDD → Glue Coding → Harness → Vibe Coding。
- 新增4个范式概念页（Spec Coding、Glue Coding、Vibe Coding、范式组合），TDD 和 Harness 已有对应概念页（tdd-as-hard-gate、ai-ci-cd-automation）进行了交叉更新。
- 新增作者实体（吕昭波）和发布平台实体（沐然云计算），扩展来源多元化。
- 本文的关键数据：代码复用率70%、开发周期2周、测试覆盖率85%、部署<10分钟、系统可用性99.95%。
- 标注了与现有 wiki 概念的张力：Spec Coding vs OpenSpec（需求规格 vs 变更追踪）、Glue Coding vs reference-projects-as-context（代码级复用 vs 知识级复用）、Harness 范式 vs AI-CI-CD-Automation（框架限制 vs 流水线控制）。

### Open Questions / Next Actions

- Glue Coding 的技术债务管理策略——缺少明确的重构触发点和债务度量标准。
- Vibe Coding 在低流量场景的适用性——A/B测试需足够样本量。
- 五范式是否覆盖所有企业级AI Coding场景？是否存在遗漏范式？
- 范式组合的切换触发条件——缺少从一种范式切换到另一种的判断标准。
- 作者是否有更深入的单一范式实战文章可供进一步录入。

## [2026-05-11] ingest | Superpowers 深度实战指南

### Scope

- 保存 raw 来源: `raw/sources/superpowers-deep-practice-guide.md`
- 新增来源页面: `wiki/sources/superpowers-deep-practice-guide.md`
- 更新实体页面: `wiki/entities/superpowers.md`（补充多平台接入表、插件系统技术细节、技能设计哲学、性能约束、指令优先级）
- 更新实体页面: `wiki/entities/claude-code.md`（补充 SessionStart hook 引导注入路径说明）
- 更新概念页面: `wiki/concepts/hooks-as-safety-net.md`（补充 Superpowers SessionStart hook 作为行为约束注入的变体）
- 更新概念页面: `wiki/concepts/bad-case-driven-iteration.md`（补充 Superpowers "合理化防范"机制作为并行模式）
- 更新 hub 页面: `wiki/overview.md`, `wiki/index.md`, `wiki/tasks/backlog.md`

### Outcomes

- 完成微信文章「Superpowers 深度实战指南：从入门到精通」（AgentBuff，2026-05-08）的录入。
- 这是 vault 中第 4 篇与 Superpowers 相关的来源，也是迄今最全面的一篇——覆盖架构全景、8 个平台安装配置、14 个 skill 的逐一深度解析。
- Superpowers 实体页大幅扩充：新增多平台接入表（8 平台）、插件系统技术细节（`run-hook.cmd` 多语言脚本、版本管理机制）、技能设计哲学（铁律模式、合理化防范、CSO 搜索优化）、性能词数约束和指令优先级层次。
- Claude Code 实体页补充了 SessionStart hook 作为 Superpowers 主要接入路径的技术细节。
- 新增 hooks-as-safety-net 概念页的"Superpowers SessionStart Hook"变体——区分了安全提醒型 hook 和行为约束注入型 hook。
- 新增 bad-case-driven-iteration 概念页的"合理化防范"并行模式——Superpowers 在技能文档中预见并预堵代理合理化借口，与 AGENTS.md 的事后 bad case 补充形成互补。
- 本文的关键洞察："using-superpowers 才是所有平台共享的行为入口；hook、插件 transform、context file 只是不同 harness 的装配层"——统一的是行为约束模型，不是技术接入点。

### Open Questions / Next Actions

- 8 个平台的安装方式是否全部经过实际验证？特别关注 Factory Droid 和 GitHub Copilot CLI。
- `run-hook.cmd` 在 Windows 找不到 bash 时静默退出 0——是否应改为警告而非静默失败？
- Superpowers 技能词数约束（<150/<200/<500 词）在实际仓库中的遵守情况。
- "合理化防范"机制是否值得抽象为自定义技能的可复用设计模板。
- brainstorming 的 HARD-GATE（"在呈现设计并获得用户批准之前不得调用实现技能"）与 `/opsx:ff` 快速入门路径的张力待澄清。

## [2026-05-09] ingest | fireworks-tech-graph 声明式技术图生成 Skill

### Scope

- 保存 raw 来源: `raw/sources/fireworks-tech-graph.md`
- 下载文章图片: `raw/assets/fireworks-tech-graph-banner.png`
- 新增来源页面: `wiki/sources/fireworks-tech-graph.md`
- 新增实体页面: `wiki/entities/fireworks-tech-graph.md`
- 新增概念页面: `wiki/concepts/diagram-generation-as-skill.md`
- 更新实体页面: `wiki/entities/claude-code.md`（补充 Skill 生态向非代码产出扩展的证据）
- 更新概念页面: `wiki/concepts/specialized-agent-pattern.md`（补充技术图生成作为领域特化 Skill 的实例）
- 更新 hub 页面: `wiki/overview.md`, `wiki/index.md`

### Outcomes

- 完成微信文章「fireworks-tech-graph ：把技术架构图生成这件事做成一个可复用 Skill」（AI技术小林，2026-04-16）的录入。
- 新增 fireworks-tech-graph 实体——记录其作为 Claude Code Skill 的五层架构（输入描述→图类型识别→风格系统→语义表达→输出与验证）、14 种图类型和 7 种视觉风格。
- 新增"声明式技术图生成"概念——将技术图创建从手工拖拽转变为自然语言描述驱动的工程化 Skill 能力，与 specialized-agent-pattern 形成互补。
- 将此来源接入 Claude Code 实体，展示 Skill 生态从代码质量检查（ORM/API checker）到领域特化非代码产出（技术图生成）的边界扩展。
- 标注了与 Mermaid（快速表达但视觉受限）和 draw.io（强大但手工成本高）的定位差异。

### Open Questions / Next Actions

- fireworks-tech-graph 的图类型识别准确率如何？是否支持混合类型？
- 大型系统（20+ 组件）的 SVG 布局质量评估。
- Windows 环境下 rsvg-convert 的替代方案。
- Claude Code Skill 生态中还有哪些非代码产出领域值得封装为 Skill（如文档翻译、幻灯片生成、数据可视化）。

## [2026-05-09] ingest | Figma Personal Access Tokens 管理

### Scope

- 保存 raw 来源: `raw/sources/figma-personal-access-tokens.md`
- 新增来源页面: `wiki/sources/figma-personal-access-tokens.md`
- 新增实体页面: `wiki/entities/figma.md`
- 更新概念页面: `wiki/concepts/policy-driven-tool-permissions.md`（补充 Figma 全量 PAT 作为权限模型光谱的另一端）
- 更新 hub 页面: `wiki/overview.md`, `wiki/index.md`

### Outcomes

- 完成 Figma 官方帮助文档「Manage personal access tokens」的录入。
- 新增 Figma 实体——记录其作为协作设计平台的产品线定位和 API 令牌模型。
- 将 Figma PAT 的"全有或全无"安全模型接入既有的 policy-driven-tool-permissions 概念，形成权限粒度对比（Claude Code 的 Allow/Ask/Deny 三级模型 vs Figma 的全量令牌）。
- 标注文档内部的张力：声称支持 scope 赋值与"access all files and data"之间的矛盾。

### Open Questions / Next Actions

- Figma PAT 的 scope 具体有哪些级别？是否支持只读令牌？需查阅 Figma developer docs。
- Figma 是否支持 OAuth App 作为 PAT 的替代方案，提供更细粒度的授权？
- 在设计-to-code 的 CI/CD 管道中（如 Figma MCP server），PAT 的安全最佳实践是什么？

## [2026-05-07] ingest | AGENTS.md 实践指南

### Scope

- 保存 raw 来源: `raw/sources/agents-md-guide.md`
- 新增来源页面: `wiki/sources/agents-md-guide.md`
- 新增实体页面: `wiki/entities/agents-md.md`, `wiki/entities/harness-creator.md`
- 新增概念页面: `wiki/concepts/map-not-manual.md`, `wiki/concepts/verification-loop.md`, `wiki/concepts/bad-case-driven-iteration.md`, `wiki/concepts/reference-projects-as-context.md`
- 更新实体页面: `wiki/entities/claude-code.md`, `wiki/entities/harness.md`
- 更新概念页面: `wiki/concepts/progressive-disclosure-context-retrieval.md`, `wiki/concepts/context-and-cost-optimization.md`, `wiki/concepts/spec-driven-workflow-and-review-discipline.md`, `wiki/concepts/verification-before-completion.md`
- 更新 hub 页面: `wiki/overview.md`, `wiki/index.md`

### Outcomes

- 完成微信文章「一个文件让 AI Coding 效率翻倍：AGENTS.md 实践指南」（Kirito的技术分享，2026-04-20）的录入。
- 新增 AGENTS.md 实体——记录其作为事实标准的前世今生（Anthropic CLAUDE.md → 工具碎片化 → AMP+OpenAI 推动统一 → Agentic AI Foundation 托管）。
- 提炼"地图，而非手册"概念：与既有渐进式上下文检索共享底层理念，但适用层次不同（项目上下文文件 vs 记忆系统）。
- 新增"验证闭环"概念：「改→构建→启动→验证」端到端循环，包含 curl 规范、Agent Browser 验证和自动化检查，与 verification-before-completion 互补。
- 新增"Bad Case 驱动迭代"和"参考项目引入"两个实践概念。
- 新增 harness-creator 实体，记录其作为 AGENTS.md 一键脚手架工具的角色。
- 标注了本文与 [[sources/ai-template2-scaffold]] 在 AGENTS.md 丰富度上的张力（200 行精简地图 vs 多层 harness 配置）。

### Open Questions / Next Actions

- AGENTS.md 的 200 行建议在大型 monorepo 中的适用性——OpenAI 88 个嵌套 AGENTS.md 的模式是否可复制。
- harness-creator 生成质量和技术栈覆盖范围待评估。
- "源码即文档"策略在上下文窗口有限的模型中的检索效率问题。
- 验证闭环基础设施的最小可行子集——哪些是必选项、哪些是增强项。

## [2026-05-07] ingest | Superpowers 工作流拆解

### Scope

- 保存 raw 来源: `raw/sources/superpowers-workflow-deconstruction.md`
- 新增来源页面: `wiki/sources/superpowers-workflow-deconstruction.md`
- 新增概念页面: `wiki/concepts/verification-before-completion.md`
- 更新实体页面: `wiki/entities/superpowers.md`, `wiki/entities/claude-code.md`
- 更新概念页面: `wiki/concepts/spec-driven-workflow-and-review-discipline.md`, `wiki/concepts/tdd-as-hard-gate.md`
- 更新 hub 页面: `wiki/overview.md`, `wiki/index.md`

### Outcomes

- 完成微信文章「我把 Claude Code 的 Superpowers 全拆了一遍，终于看懂它真正厉害的地方」（地瓜老爸，2026-03-27）的录入。
- 将 Superpowers 的 14 个 skill 解析为四层架构（总入口/流程控制、实施执行/环境隔离、质量保障/问题处理、收尾/元能力），补充到实体页。
- 提炼两条主链路：功能开发链（brainstorming → plan → worktree → execute → finish）和调试链（systematic-debugging → TDD → verification）。
- 新增 "verification-before-completion" 概念：完成声明必须绑定新鲜验证结果，与 TDD 硬门禁互补但不等价（TDD 管开发过程，此概念管交付关口）。
- 标注了本文与 [[sources/ai-template2-scaffold]] 在"最该默认启用的底线规则"上的优先级差异（本文偏完成纪律，脚手架偏开发纪律）。

### Open Questions / Next Actions

- 14 个 skill 是否全部默认安装，还是按需加载？文章未做说明。
- 功能开发链路中发现 bug 需要切换到调试链路时，切换机制是什么？
- "新鲜"验证结果的精确定义（时间窗口/变更范围阈值）待明确。
- 是否值得将四层架构映射到 harness 的命令分层，形成"配置即文档"。

## [2026-05-06] ingest | Claudian Obsidian 插件

### Scope

- 新增来源页面: `wiki/sources/claudian-obsidian-plugin.md`
- 新增实体页面: `wiki/entities/claudian.md`, `wiki/entities/brat.md`
- 新增概念页面: `wiki/concepts/vault-native-ai-assistant.md`, `wiki/concepts/structured-tag-system-for-ai.md`
- 更新实体页面: `wiki/entities/obsidian.md`
- 更新 hub 页面: `wiki/overview.md`, `wiki/index.md`
- 保存 raw 来源: `raw/sources/claudian-obsidian-plugin.md`

### Outcomes

- 完成微信文章 "Claudian：让 AI 直接长在 Obsidian 里的插件" 的录入。
- 引入 "vault-native AI 助手"概念，与既有 LLM wiki 编译、上下文成本优化等主题形成连接。
- 引入"面向 AI 的结构化标签体系"概念，标记了与 MOC 多标签实践的张力。
- Obsidian 实体页更新，反映插件生态扩展（BRAT 分发、AI 集成场景）。

### Open Questions / Next Actions

- Claudian 对大型 vault（1000+ 笔记）的上下文处理策略是什么？是否支持 RAG？
- 对比 Claudian vs Obsidian Copilot vs Smart Connections 的架构差异。
- 是否值得将标签体系设计模板化，作为 vault 维护的可复用 checklist。
- BRAT 安装的 beta 插件的安全模型和更新策略待调研。

## [2026-04-25] refactor | 默认中文输出规则

### Scope

- 更新规则文件: `AGENTS.md`
- 中文化本次 Claude-Mem 录入相关页面: `wiki/sources/claude-mem.md`, `wiki/entities/claude-mem.md`, `wiki/concepts/persistent-agent-memory.md`, `wiki/concepts/progressive-disclosure-context-retrieval.md`
- 中文化相关 hub/任务/日志摘要: `wiki/index.md`, `wiki/overview.md`, `wiki/tasks/backlog.md`, `wiki/log.md`

### Outcomes

- 明确 agent 回复、wiki 页面、index 摘要、overview 综合、tasks 和 log 默认使用简体中文。
- 保留工具名、命令、项目名、路径、来源标题和会降低精度的技术术语原文。
- 将刚录入的 Claude-Mem 相关内容调整为中文表达，保持链接和证据关系不变。

### Open Questions / Next Actions

- 后续 lint 可逐步中文化更早的英文模板与历史页面。

## [2026-04-25] ingest | Claude-Mem 持久化记忆

### Scope

- 新增来源页面: `wiki/sources/claude-mem.md`
- 新增实体页面: `wiki/entities/claude-mem.md`
- 新增概念页面: `wiki/concepts/persistent-agent-memory.md`, `wiki/concepts/progressive-disclosure-context-retrieval.md`
- 更新相关页面: `wiki/entities/claude-code.md`, `wiki/concepts/context-and-cost-optimization.md`, `wiki/concepts/hooks-as-safety-net.md`, `wiki/concepts/persistent-wiki-compilation.md`
- 更新 hub/任务页面: `wiki/overview.md`, `wiki/index.md`, `wiki/tasks/backlog.md`

### Outcomes

- 完成 `raw/sources/claude-mem.md` 的录入。
- 将 Claude-Mem 记录为一个具体的 Claude Code 持久化记忆系统，包含 hooks、worker 服务、SQLite、Chroma、Web 查看器和 `mem-search`。
- 新增“持久化 agent 记忆”和“渐进式上下文检索”两个可复用概念，并接入既有的上下文成本与 wiki 编译主题。
- 标出自动记忆捕获与可审计、经整理 wiki 综合之间的张力。

### Open Questions / Next Actions

- 定义自动捕获 agent 记忆的隐私、保留和修剪规则。
- 判断何时 Claude-Mem 式记忆搜索已经足够，何时应提升为整理后的 wiki 页面。
- 评估个人 vault 和小团队可接受的本地基础设施成本。

## [2026-04-24] ingest | ai_template2 Multi-Module AI Collaboration Scaffold

### Scope

- Added raw source: `raw/sources/ai-template2-scaffold.md`
- Added source page: `wiki/sources/ai-template2-scaffold.md`
- Added entity page: `wiki/entities/harness.md`
- Added concept pages: `wiki/concepts/layered-project-harness.md`, `wiki/concepts/specialized-agent-pattern.md`, `wiki/concepts/tdd-as-hard-gate.md`, `wiki/concepts/hooks-as-safety-net.md`
- Updated hub pages: `wiki/index.md`, `wiki/overview.md`

### Outcomes

- Completed ingest from ai_template2 scaffold (`D:/Users/Administrator/Desktop/AI/ai_template2`).
- Captured the concrete integration of OpenSpec + Superpowers + Claude Code Harness into a single project template.
- Added new entity (Harness) and 4 concepts: layered harness organization, specialized agent routing, TDD hard gates, and lifecycle hooks as safety net.
- Expanded the wiki from theoretical workflow patterns to a concrete, deployable scaffold reference.

### Open Questions / Next Actions

- Decide whether to adapt this scaffold for an actual project (replacing placeholders).
- Explore whether hooks should be fail-closed for security-sensitive projects.
- Define a minimum viable subset of the 9 commands + 6 skills + 4 agents for small teams.

## [2026-04-24] ingest | OpenSpec + Superpowers 源文件完整入库

### Scope

- 更新源页面: `wiki/sources/openspec-superpowers-practice-guide.md`（补充五阶段流水线、场景决策表、FAQ、dlabel-cloud-mall 实战案例、常见问题与改进建议）
- 更新实体页面: `wiki/entities/openspec.md`（补充目录结构、核心命令、安装方式），`wiki/entities/superpowers.md`（补充七步流程、TDD 纪律、安装方式、目录结构）
- 更新概念页面: `wiki/concepts/spec-driven-workflow-and-review-discipline.md`（补充场景决策表、常见坑模式）
- 更新合成页面: `wiki/overview.md`

### Outcomes

- Raw 源文件全部关键内容已录入 wiki：OpenSpec/Superpowers 工作流、五阶段流水线、场景分级、实战案例、经验教训。
- 实体页面现在包含可操作的目录结构和命令参考。
- 概念页面新增常见坑模式，便于后续项目参考。

### Open Questions / Next Actions

- 沉淀统一的 DoD（Definition of Done）模板供 AI 开发使用。
- 明确任务规模触发完整 Superpowers 链路的阈值。

## [2026-04-24] ingest | OpenSpec + Superpowers 规范开发指南

### Scope

- Added source page: `wiki/sources/openspec-superpowers-practice-guide.md`
- Added entity pages: `wiki/entities/openspec.md`, `wiki/entities/superpowers.md`
- Added concept page: `wiki/concepts/spec-driven-workflow-and-review-discipline.md`
- Updated hub pages: `wiki/index.md`, `wiki/overview.md`

### Outcomes

- Completed ingest from `raw/sources/OpenSpec + Superpowers规范开发指南.md`.
- Added the OpenSpec + Superpowers operational layer and its key entities/concept links.
- Connected spec-driven governance concepts into the existing enterprise + personal workflow graph.

### Open Questions / Next Actions

- Define explicit thresholds for when full Superpowers chain is mandatory vs. minimal-flow exceptions.
- Decide whether to add a task-level minimum evidence rubric and make it a shared checklist.

## [2026-04-25] ingest | OpenSpec + Superpowers 深度教程

### Scope

- Added source page: `wiki/sources/ai-coding-advanced-openspec-superpowers-deep-guide.md`
- Updated entity pages: `wiki/entities/openspec.md`, `wiki/entities/superpowers.md`
- Updated concept pages: `wiki/concepts/spec-driven-workflow-and-review-discipline.md`, `wiki/concepts/tdd-as-hard-gate.md`
- Updated hub pages: `wiki/overview.md`, `wiki/index.md`
- Updated task page: `wiki/tasks/backlog.md`

### Outcomes

- Ingested the WeChat article `AI 编程进阶：OpenSpec + Superpowers 组合方案深度使用教程` from `https://mp.weixin.qq.com/s/092HGb6sEfz2Q-Pr-jEX2w`.
- Captured its distinct contribution relative to the earlier OpenSpec + Superpowers guide: a more tutorialized, end-to-end path centered on `/opsx:ff → verify → archive`, a shopping-cart example, and a failure-recovery playbook.
- Strengthened existing OpenSpec / Superpowers / spec-driven workflow / TDD pages with practical signals: fast-forward onboarding, minimal core skills, and boundary-condition checks before verification.

### Open Questions / Next Actions

- Verify whether `/opsx:ff` and `verify` are default OpenSpec commands or profile/scaffold-level wrappers.
- Decide whether the shopping-cart edge-case checklist should become a reusable DoD template for stateful features.

## [2026-04-29] refactor | 补录微信文章备用网址并去重校验

### Scope

- 更新来源页面: `wiki/sources/ai-coding-advanced-openspec-superpowers-deep-guide.md`
- 更新导航页: `wiki/index.md`
- 更新操作日志: `wiki/log.md`

### Outcomes

- 复核用户提供的微信链接 `https://mp.weixin.qq.com/s/HJi8n8t5RXFCevn0ezmLNg`，确认 vault 中已存在同标题来源页 `[[sources/ai-coding-advanced-openspec-superpowers-deep-guide]]`，未新建重复页面。
- 在来源页中补记既有 URL 与本次 Alternate URL，保留“同文多链接”痕迹，便于后续追溯。
- 记录本次复核的限制：直连抓取命中 `secitptpage/verify`，因此未从该备用网址重新抽取正文。

### Open Questions / Next Actions

- 如需更强校验，可把文章原文保存到 `raw/sources/`，以便后续脱离微信验证页做稳定比对。
- 若后续再次出现同标题多链接，可考虑给 source 页面增加固定的 “Known URLs” 字段规范。

## [2026-04-22] refactor | Initialize LLM wiki scaffold

### Scope

- Created schema: `AGENTS.md`
- Created base directories under `raw/` and `wiki/`
- Added starter pages: `wiki/index.md`, `wiki/overview.md`, `wiki/tasks/backlog.md`
- Added workflow templates in `wiki/templates/`

### Outcomes

- Vault is now structured for ingest/query/lint operations.
- Index and log conventions are defined and ready for first source ingest.

### Open Questions / Next Actions

- Add first source into `raw/sources/`.
- Run first ingest to create the initial source + concept/entity graph.

## [2026-04-22] ingest | LLM Wiki

### Scope

- Added source page: `wiki/sources/llm-wiki-pattern.md`
- Added entity pages: `wiki/entities/llm-agent.md`, `wiki/entities/obsidian.md`
- Added concept pages: `wiki/concepts/persistent-wiki-compilation.md`, `wiki/concepts/ingest-query-lint-loop.md`, `wiki/concepts/schema-driven-maintenance.md`
- Updated hub pages: `wiki/overview.md`, `wiki/index.md`

### Outcomes

- Completed first source ingest from `raw/sources/llm-wiki.md`.
- Established initial cross-linked graph across source, entities, and concepts.
- Captured key operating loop (ingest/query/lint) and schema governance concept.

### Open Questions / Next Actions

- Ingest at least 2-3 external examples to test contradictions and refine concepts.
- Decide whether to create an initial analysis page comparing this pattern vs classic RAG workflows.

## [2026-04-22] ingest | Claude Code 综合实战完整指南

### Scope

- Added source page: `wiki/sources/claude-code-enterprise-playbook.md`
- Added entity pages: `wiki/entities/claude-code.md`, `wiki/entities/github-actions.md`
- Added concept pages: `wiki/concepts/team-governance-for-ai-coding.md`, `wiki/concepts/policy-driven-tool-permissions.md`, `wiki/concepts/ai-ci-cd-automation.md`, `wiki/concepts/context-and-cost-optimization.md`
- Updated hub pages: `wiki/overview.md`, `wiki/index.md`

### Outcomes

- Completed ingest from `raw/sources/综合实战完整指南.md`.
- Expanded wiki from conceptual pattern layer to enterprise execution layer.
- Captured actionable governance dimensions: team standards, permission policy, CI/CD automation, and performance-cost controls.

### Open Questions / Next Actions

- Create a durable comparison analysis between personal LLM wiki workflows and enterprise Claude Code governance workflows.
- Add a task page for “minimum secure baseline” templates (`CLAUDE.md`, permissions, and GitHub Actions) for small teams.

## [2026-04-22] query | Personal vs Enterprise LLM Workflows

### Scope

- Added analysis page: `wiki/analyses/personal-vs-enterprise-llm-workflows.md`
- Updated navigation: `wiki/index.md`

### Outcomes

- Produced a durable comparison between personal knowledge-compilation workflows and enterprise AI engineering governance.
- Added a migration path from lightweight personal usage to policy-driven CI/CD operations.

### Open Questions / Next Actions

- Convert the decision framework into a checklist template for team onboarding.
- Define a “minimum secure baseline” starter pack for 1-10 person teams.
