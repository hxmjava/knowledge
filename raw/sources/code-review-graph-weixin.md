# Code Review Graph：给 AI 代码评审装一张本地图谱

**来源**：微信公众号「AI作弊码」
**链接**：https://mp.weixin.qq.com/s/-AzJNiWtO5G_Lbv8xl4BVQ
**发布日期**：2026-05-05
**归档日期**：2026-05-11

---

Code Review Graph 不是又一个"把仓库塞进向量库"的工具。它更像是给 AI 编程助手准备了一张本地代码地图：先解析代码结构，再把函数、类、导入、调用和测试关系存成图，最后通过 MCP 把真正需要读的上下文交给 AI 工具。

## 一. 为什么 AI 评审会浪费上下文

很多 AI 编程助手做代码评审时，会遇到一个朴素但昂贵的问题：它并不知道这次变更真正影响了哪里。

如果只是把相关目录、最近修改文件、搜索结果一股脑塞进上下文，模型确实"看得多"，但读到的无关信息也会变多。上下文窗口越大，成本越高，噪声也越容易稀释判断。

`code-review-graph` 的切入点很明确：不要让 AI 重新猜仓库结构，而是先在本地维护一张结构化图谱。评审时，AI 先查图，再读代码。

![图 1：没有图谱时，AI 更容易读取整个代码库；有图谱后，AI 可以先查询影响面，再读取最小评审集。](raw/assets/code-review-graph-token-comparison.png)

## 二. 代码先变成图

![图 2：从代码仓库出发，经 Tree-sitter 解析为 AST，再写入 SQLite 图谱，最后用影响面分析给 AI 提供最小评审集。](raw/assets/code-review-graph-workflow.png)

这张图里有几个词如果第一次看会有点硬，可以拆开理解。

- **Tree-sitter**：一个增量代码解析器。可以理解成"懂很多编程语言语法的结构化阅读器"，它能稳定识别函数、类、导入、调用等语法结构。
- **AST**：Abstract Syntax Tree，抽象语法树。代码在 AST 里不再是一行行文本，而是一个树状结构。
- **SQLite 图谱**：结构信息存在本地 SQLite 文件里。SQLite 不需要单独起服务；这里的图谱指节点和边，比如函数是节点，调用关系是边。
- **BFS 遍历**：从起点向外一层层扩散的图搜索方法。用在人话里，就是从改动点开始逐层找调用者、依赖项和受影响测试。

所以它做的不是"把代码全文喂给模型"，而是先把仓库压成一张可查询的结构图。模型需要上下文时，查到的是更靠近变更的结构信息。

## 三. 只读可能被波及的部分

![图 3：一次变更会沿调用、导入、测试关系向外扩散。影响面分析的目标是优先找出 AI 应该先读的区域。](raw/assets/code-review-graph-impact-analysis.png)

项目里把这个能力叫 blast-radius analysis，直译是"爆炸半径"，在工程语境里更适合叫"影响面分析"。

- 直接调用变更函数的函数或路由；
- 间接依赖它的模块；
- 覆盖它的测试；
- 因导入、继承、调用链而可能被带到的相关文件。

这也是它相比普通全文搜索更有意思的地方：它关心的是代码之间的结构关系，而不只是关键词是否命中。

## 四. 把图查询交给 AI 助手

MCP 是 Model Context Protocol，可以理解成"让 AI 助手调用外部工具的通用协议"。`code-review-graph` 通过 MCP 暴露查询能力，这样 Claude Code、Cursor、Windsurf、Zed、Codex 等工具，就可以在任务中先问图谱。

![图 4：AI 助手通过 MCP Server 查询本地图谱，再根据返回的影响面、测试缺口和风险分数进行评审。](raw/assets/code-review-graph-mcp-chain.png)

- 这次变更影响哪些函数和文件？
- 哪些测试可能需要补？
- 某个符号在哪里被调用？
- 这个模块周围有哪些高风险依赖？

这层协议的价值在于：AI 不必把图谱实现细节学一遍，只要会调用 MCP 工具，就能拿到结构化上下文。

## 五. 很省 Token，但不是银弹

项目给出的自动评测来自 6 个真实开源仓库、13 个 commits。它报告的平均结果是：增量方案相比全量读法，平均 token 减少 **8.2倍**。

![图 5：benchmark 展示了不同仓库的 token 减少和评审质量对比。数字要结合任务规模理解。](raw/assets/code-review-graph-benchmark.png)

但这个数字不能机械理解成"任何项目都会省 8 倍"。一个反例：在 express 的小型单文件变更里，graph 上下文反而是 **0.7倍**，也就是比直接读文件更重。

图谱上下文有固定开销：节点、边、评审提示、影响链都要占 token。项目越大、变更越跨文件、无关代码越多，图谱裁剪越划算；项目很小、改动很孤立时，直接读文件可能更简单。

影响面准确率也要这样看。报告 recall 为 100%，平均 F1 为 0.54，precision 为 0.38。换句话说，它倾向于"宁可多报一点，也不要漏掉真正受影响的文件"。这对评审是合理取舍，但并不等于每个命中都一定有问题。

## 六. 本地、增量、多语言

![图 6：增量更新不是重扫全仓，而是从 git diff 和依赖关系出发，只重解析相关文件。](raw/assets/code-review-graph-incremental-update.png)

- **本地存储**：图谱存在项目的 `.code-review-graph/` 目录里，不依赖云数据库。
- **增量更新**：它会基于文件变更和 SHA-256 校验，只重解析变更相关内容；在 2,900 文件项目中，重索引用时低于 2 秒。
- **多语言支持**：23 种语言加 Jupyter / Databricks notebook，包括 Python、TypeScript、Go、Rust、Java、C/C++、Swift、Kotlin、Svelte 等。
- **Python 包形态**：`pyproject.toml` 显示包名为 `code-review-graph`，当前归档版本为 2.3.2，要求 Python 3.10+，许可证为 MIT。

![图 7：语言覆盖图展示了 Web、后端、系统、移动端、脚本等不同类别的语法解析能力。](raw/assets/code-review-graph-language-coverage.png)

这些点说明它更像一个"本地开发基础设施"，而不是在线 SaaS。对重视代码隐私、又希望 AI 助手更懂仓库结构的团队，这个形态比较友好。

## 七. 快速上手

官方给出的最短路径是三步：

![图 8：`code-review-graph install` 会尝试自动识别本机已安装的平台，并写入对应 MCP 配置。](raw/assets/code-review-graph-install.png)

```
pip install code-review-graph
code-review-graph install
code-review-graph build
```

`install` 会尝试检测本机已有的 AI 编程工具并写入 MCP 配置；`build` 则负责解析当前项目并构建图谱。建议安装 `uv`，这样 MCP 配置可以优先使用 `uvx`。

```
code-review-graph update
code-review-graph watch
code-review-graph detect-changes
code-review-graph visualize
```

## 八. 适合谁，不适合谁

如果你只是在几十个文件的小项目里偶尔让 AI 改一行代码，这类工具未必能立刻显出价值。图谱构建、维护、上下文描述本身也有成本。

- 仓库很大，AI 经常读到无关文件；
- PR 影响范围不明显，需要追调用链和测试覆盖；
- 团队想把 Claude Code、Cursor、Codex 等工具接入统一的结构化上下文；
- 你希望上下文分析尽量在本地完成，不把全量代码交给外部服务。

我更愿意把它看成一个方向信号：AI 编程的下一步，不只是模型更强，也包括上下文供应链更清晰。模型负责推理，但"该读什么"这件事，应该越来越多交给结构化工具。

如果是需要对项目做一次完整深入的探查，也可以参考 GitNexus：将整个代码仓库变成知识图谱。

## 项目地址

GitHub：https://github.com/tirth8205/code-review-graph
截至本次归档，GitHub API 显示项目约 15.3k Stars、MIT License，主语言为 Python。
