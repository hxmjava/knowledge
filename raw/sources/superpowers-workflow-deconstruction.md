# 我把 Claude Code 的 Superpowers 全拆了一遍，终于看懂它真正厉害的地方

- 来源：微信公众号「地瓜老爸」
- 发布日期：2026-03-27
- URL：https://mp.weixin.qq.com/s/Fko48oWrAgOL4KcOrQ9sPg

---

很多人第一次看到 Superpowers，注意力都会落在那些 skill 名字上。
brainstorming、systematic-debugging、verification-before-completion、writing-plans……
看起来像一组功能很多、覆盖很全的插件。
但把整套东西一条条拆完之后，结论反而变得很简单：
Superpowers 真正厉害的地方，不是"给 Claude Code 多装了 14 个能力"，而是把它塞进了一套更像工程团队的工作方式里。
如果只谈"它很先进""它很强"，其实没有太大意义。真正值得问的，只有一个问题：
它到底把 Claude Code 约束成了什么样的工作流？

## 一、表面上是 14 个 skill，底层其实是 4 层能力

先看表面。
这套 Superpowers 里，一共有 14 个 skill：

| Skill | 功能 |
|-------|------|
| using-superpowers | 整套系统的总入口，先判断当前任务该走哪条流程 |
| brainstorming | 在实现前先澄清需求、比较方案、完成设计 |
| writing-plans | 把设计继续拆成可执行、可验证的实施计划 |
| using-git-worktrees | 创建隔离工作区和独立分支，降低直接改主环境的风险 |
| subagent-driven-development | 把任务交给子代理分工实现，并把审查流程内建进去 |
| executing-plans | 按既定 plan 串行推进任务，逐项执行和验证 |
| test-driven-development | 先写失败测试，再做最小实现，最后重构 |
| systematic-debugging | 先查根因、验证假设，再进入修复 |
| requesting-code-review | 在关键节点主动发起代码审查 |
| receiving-code-review | 处理 review 反馈，判断建议是否成立并逐项修复 |
| verification-before-completion | 没有最新验证结果前，不允许宣称完成 |
| finishing-a-development-branch | 在任务尾声统一处理测试、分支、合并和清理 |
| dispatching-parallel-agents | 把彼此独立的问题分发给多个代理并行处理 |
| writing-skills | 用来编写和迭代 skill 本身的元能力 |

如果只看名字，它们像一组平铺的工具。
但真往里读，就会发现它们其实不是并列关系，而是四层分工。

### 1. 总入口与流程控制

- using-superpowers
- brainstorming
- writing-plans

这一层负责的是先判断任务属于哪种模式，再决定后面的执行路线。

### 2. 实施执行与环境隔离

- using-git-worktrees
- subagent-driven-development
- executing-plans
- dispatching-parallel-agents

这一层负责的是怎么开始做、在哪里做、是串行做还是并行做。

### 3. 质量保障与问题处理

- test-driven-development
- systematic-debugging
- requesting-code-review
- receiving-code-review
- verification-before-completion

这一层最像"工程纪律"。它不让 Claude 只管往前输出，而是不断追问：你有证据吗？你验证了吗？你真的理解问题了吗？

### 4. 收尾与元能力

- finishing-a-development-branch
- writing-skills

这一层解决的是最后怎么收口，以及怎么继续扩展这套 skill 系统本身。

所以看完整体之后，Superpowers 给我的第一感觉不是"功能很全"，而是：
它在努力把 Claude Code 从一个会回答问题的模型，往一个守流程的工程协作者上拽。

## 二、两条主链路

真正值得看的，不是每个 skill 单独能做什么，而是它们是怎么串起来的。

### 1. 做新功能、改行为的主链路

这类任务的主链路很清楚：

```
using-superpowers
→ brainstorming
→ writing-plans
→ using-git-worktrees
→ subagent-driven-development 或 executing-plans
→ finishing-a-development-branch
```

这条链路翻译成人话，就是：
1. 先判断任务类型
2. 先把需求和设计说清楚
3. 再把实施计划拆清楚
4. 执行前先进入隔离环境
5. 然后按计划推进
6. 最后统一收尾

注意，它不是"用户提一句，Claude 直接开始写"。
它强调的是：
先定义问题，再设计方案，再拆计划，再执行，再交付。
这个顺序，本身就是 Superpowers 最核心的价值之一。

### 2. 修 bug、查异常的调试链路

如果任务是 bug、测试失败、行为异常，它走的是另一条更短但更硬的链路：

```
using-superpowers
→ systematic-debugging
→ test-driven-development
→ verification-before-completion
```

这条链路背后的逻辑也非常明确：
- 不先查到根因，不要动手修
- 不先看到失败测试，不要急着写实现
- 不做新鲜验证，不要宣布完成

很多 AI 编程流程最常见的问题，其实都出在这里。
它们太容易直接给修复建议，也太容易在没有证据的情况下说"应该好了"。
Superpowers 做的事，就是把这些最容易出错的环节，变成强制门禁。

## 三、它真正解决的，不是"会不会写代码"，而是"会不会按工程方式交付"

把这两条链路放在一起看，Superpowers 真正在解决的问题就很清楚了。
它不是单纯提高生成能力，而是在补 AI 最容易缺的几种工程习惯。

### 1. 先把问题定义清楚，而不是先开始做

brainstorming 最重要的价值，不是"帮你想点子"，而是硬性要求：
设计没被批准之前，不准直接进入实现。

这条规则看起来啰嗦，但其实非常关键。
因为 AI 最容易犯的错，不是不会写，而是在还没理解对的时候，已经开始写了。

### 2. 先找根因，再谈修复

systematic-debugging 的核心很硬：
没有查清根因，不要修。

这等于直接反过来对抗一种很常见的低效路径：
- 猜一个地方
- 改一下
- 试一下
- 再猜一个地方

对人来说，这已经很浪费时间；对 AI 来说，更危险，因为它太擅长给出"看起来像答案"的东西。

### 3. 先给证据，再宣布完成

如果只让我选一个最该默认启用的底线规则，我会选 verification-before-completion。
它的原则非常简单：
没有新鲜验证结果，不要宣称完成。

这句话对人与 AI 协作特别重要。
因为最伤体验的，通常不是 bug 本身，而是错误的完成声明。
一旦模型可以轻易说出"修好了""搞定了""应该没问题"，协作成本就会突然变高。

### 4. 把 review 和收尾也做成流程内建动作

requesting-code-review、receiving-code-review、finishing-a-development-branch 这些 skill 说明了一件事：
Superpowers 不是停在"代码已经写出来"这一步。
它考虑的是完整交付。
也就是说，在它的设计里，真正的结束不是"写完"，而是：
- 审过
- 验过
- 该合并的合并
- 该保留的保留
- 该清理的清理

这才是一个完整的工程闭环。
