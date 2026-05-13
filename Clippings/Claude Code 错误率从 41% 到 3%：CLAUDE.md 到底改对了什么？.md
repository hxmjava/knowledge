---
title: "Claude Code 错误率从 41% 到 3%：CLAUDE.md 到底改对了什么？"
source: "https://mp.weixin.qq.com/s/nAqv-0xAeoalLHS-nCt0TQ"
author:
  - "[[若飞]]"
published:
created: 2026-05-12
description: "把 Agent 昨天犯过的错，写成它明天开工前能读懂的约定。"
tags:
  - "clippings"
---
若飞 *2026年5月11日 22:01*

---

今天刷到一篇关于 `CLAUDE.md` 的长文。

标题里最扎眼的，是一个数字：作者说自己在 30 个代码库上测了 6 周，Claude Code 的错误率从 41% 降到了 3%。

这种数字很容易让人马上想做两件事。

第一，收藏即阅读。  
第二，把文末那 12 条规则复制下来，丢进自己的仓库。

说实话我一开始也差不多。

读完以后，我倒没有急着抄那 12 条。

让我停住的是另一个问题：为什么一份普通的 `CLAUDE.md` ，会对 Claude Code 的行为产生这么大的影响？

先把边界说清楚。

这组数据是作者自己的实验记录，不是独立复现的论文。不同代码库、不同任务、不同模型版本、不同评判标准，结果都会变。所以我不会把“41% 到 3%”当成一个可以直接套用的结论。

不过这个样本还是提醒了我一件事。

我们这段时间一直在聊、 [Harness](https://mp.weixin.qq.com/s?__biz=MzAwNjQwNzU2NQ==&mid=2650409162&idx=1&sn=62556a10e227bcb8d977a4f3e0006c8b&scene=21#wechat_redirect) 、 [上下文工作集](https://mp.weixin.qq.com/s?__biz=MzAwNjQwNzU2NQ==&mid=2650409162&idx=1&sn=62556a10e227bcb8d977a4f3e0006c8b&scene=21#wechat_redirect) 、 [长周期 Agent](https://mp.weixin.qq.com/s?__biz=MzAwNjQwNzU2NQ==&mid=2650409301&idx=1&sn=11fd501a836542bcccc7b4fec03fb43e&scene=21#wechat_redirect) 和可验证交付。落到日常开发里，就是一句话：

Agent 已经开始进工程现场了。

既然进了现场，就不能再只靠每次临场提醒。

`CLAUDE.md` 这类文件的用处，差不多就在这。它不是什么神秘提示词，也不是让模型强行听话的开关，更像是一份写在仓库里的工作约定：把项目里反复出错的地方，提前告诉 Agent。

这也补上了前面几篇没有展开的一小块。讲 [Cursor 的 Harness 方法论](https://mp.weixin.qq.com/s?__biz=MzAwNjQwNzU2NQ==&mid=2650409236&idx=1&sn=71ae43ca6ec5b3cb1f82c258b1542271&scene=21#wechat_redirect) 时，我们把重点放在评估、观测、回滚和模型适配；讲 [Martin Fowler 的 AI 研发提醒](https://mp.weixin.qq.com/s?__biz=MzAwNjQwNzU2NQ==&mid=2650409277&idx=1&sn=f73a7d925414775f9b8dfe9f2ce5ef88&scene=21#wechat_redirect) 时，重点放在非确定性如何进入研发链路；讲 [长周期 Agent](https://mp.weixin.qq.com/s?__biz=MzAwNjQwNzU2NQ==&mid=2650409301&idx=1&sn=11fd501a836542bcccc7b4fec03fb43e&scene=21#wechat_redirect) 时，重点放在目标、状态、验证和接管的证据链。

这次讨论的 `CLAUDE.md` ，看起来只是一个小文件，却正好落在同一条线上。

它把人的工程经验，放到 Agent 每次开工前都能读到的位置。

写得好，它能少踩几次旧坑。

写得差，它会变成另一种上下文噪声。

前面写《[.claude 文件夹里到底应该放什么](https://mp.weixin.qq.com/s?__biz=MzAwNjQwNzU2NQ==&mid=2650409124&idx=1&sn=180416118fbed11d4def779ed4485070&scene=21#wechat_redirect) 》时，我更关心的是东西应该放在哪里：哪些进 `CLAUDE.md` ，哪些进 `settings.json` ，哪些交给 hooks、commands、skills。

读完这篇以后，问题又往前推了一步：放在 `CLAUDE.md` 里的那些话，到底该长什么样，才不会变成一堆看起来正确、实际没什么用的提醒？

---

## 太长不看

- • “错误率从 41% 到 3%”先当作经验样本看，不要当成通用定律。
- • Karpathy 那 4 条规则更值钱的地方，是把几类常见失败模式写清楚了：静默假设、过度复杂、无关改动、没有验证。
- • 12 条规则可以重组为 4 类工程问题：控制改动半径、把确定性交还给代码、让长任务留下检查点、把失败显性化。
- • 扩成 12 条也有价值，但不建议整包复制。规则文件越长，越容易把简单任务拖复杂。
- • 一份好的 `CLAUDE.md` 通常来自坏现场：Agent 曾经怎么翻车，就把那类错误写成下一次能读懂的约定。
- • 想快速用起来，不必等“大规范”。先写命令、边界、验证方式和 5 到 10 条行为约定。
- • `CLAUDE.md` 只能做事前提醒，更能兜底的还是测试、lint、类型检查、权限、hooks、CI 和 review。

---

## 这 4 条为什么会有效

这轮讨论的源头，还是 [Karpathy](https://mp.weixin.qq.com/s?__biz=MzAwNjQwNzU2NQ==&mid=2650409219&idx=1&sn=faa35c5f162f4830e1c90933fc95bad1&scene=21#wechat_redirect) 早前对 Claude 写代码的几类吐槽。

模型会默默做假设。  
模型会把简单问题做复杂。  
模型会顺手改掉不该动的代码。  
模型会给一个看似完成、实际没验证的结果。

Forrest Chang 后来把这些观察整理成了一份 `CLAUDE.md` ，放在 GitHub 上。核心就 4 条：

- • 写代码前先说明假设；
- • 先选简单方案；
- • 只做必要改动；
- • 围绕成功标准循环验证。

单看这几条，并不算新鲜。

甚至有点像资深工程师平时给新人做 code review 时会顺口说的那几句话。

但把它们放到 Agent 里，意义就不太一样了。

人类工程师被提醒一次，通常会记住一阵子。Agent 换一个会话、换一个目录、换一个任务，很可能又从头开始猜。它不是故意乱来，只是没办法稳定继承项目里的工作习惯。

`CLAUDE.md` 干的事很朴素，就是把这些工作习惯固定到仓库里。

下一次 Agent 启动时，至少能先读到这几条。

我会把它理解成一份“轻量行为契约”，比“提示词技巧”更贴近它在工程里的位置。

提示词更多控制当下这一次对话；行为契约放在仓库级别，目标是让每一次会话都少走一点弯路。

Shopify CEO Tobi Lütke 之前在推上提过一个说法，他更喜欢用 `context engineering` 而不是 `prompt engineering` ，因为核心技能其实是“给模型足够的上下文，让任务变得可解”。 `CLAUDE.md` 就属于这层最薄、也最稳定的上下文。

---

## 规则背后的失败现场

原文最有用的一部分，不只在那份清单，也在每条规则后面那个具体的失败现场。

比如有一段代码，让 Claude 自己判断 `503` 时要不要重试。前两周跑得都挺好，后来模型开始把请求 body 也当成决策上下文，重试策略就开始抖。这里的问题不是 Claude 不够聪明，问题出在团队把本该由确定性代码处理的逻辑，交给了一个概率模型。

再比如错误处理。代码库里已经有两套模式，一套 `async/await + try/catch` ，一套全局 error boundary。Claude 没有挑其中一种，而是写了一个“两边都照顾”的版本。结果错误处理器翻倍，错误被吞了两次。

还有一个例子：某个文件附近已经有旧函数做同一件事，Claude 没读到，又自己写了一个新的。新函数因为 import 顺序拿到了优先级，旧函数反而被悄悄绕开。

最麻烦的是那种“看起来成功”的失败。

测试全绿，但 auth 函数只是返回了一个常量；迁移脚本说“完成”，实际跳过了命中约束冲突的记录。日志里有痕迹，但 Agent 没把这件事说出来。

这些例子放到一起，就能看清楚一件事：

`CLAUDE.md` 要防的，往往不是“语法写错”这种低级问题。

它防的，是 Agent 在工程现场里很容易出现的那几类偏差：猜、扩、混、忘、装作完成。

理解这一点，比单纯背下来 12 条规则更重要。

---

## 12 条规则可以看，先别照单全收

为了方便看，我先把这 12 条压成一句话版本。不是让谁去背，先看清楚它们大概在约束什么。

| # | 规则 | 一句话理解 |
| --- | --- | --- |
| 1 | Think Before Coding | 不确定先说假设，不要默默猜 |
| 2 | Simplicity First | 先用最小方案解决问题 |
| 3 | Surgical Changes | 只改必要范围，不顺手重构 |
| 4 | Goal-Driven Execution | 围绕成功标准循环验证 |
| 5 | Model for Judgment Only | 模型做判断，确定性逻辑交给代码 |
| 6 | Token Budgets | 长任务要有预算，超了就停下来整理 |
| 7 | Surface Conflicts | 模式冲突要指出，不要折中平均 |
| 8 | Read Before Write | 写之前先读周边代码 |
| 9 | Tests Verify Intent | 测试要验证业务意图，不只验证返回值 |
| 10 | Checkpoint Steps | 多步骤任务要留下检查点 |
| 11 | Match Conventions | 跟随项目约定，不私自开新风格 |
| 12 | Fail Loud | 不确定、跳过、未验证，都要明说 |

![图片](data:image/svg+xml,%3C%3Fxml version='1.0' encoding='UTF-8'%3F%3E%3Csvg width='1px' height='1px' viewBox='0 0 1 1' version='1.1' xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg stroke='none' stroke-width='1' fill='none' fill-rule='evenodd' fill-opacity='0'%3E%3Cg transform='translate(-249.000000, -126.000000)' fill='%23FFFFFF'%3E%3Crect x='249' y='126' width='1' height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

Claude Code 的 12 条规则栈

*图：这 12 条规则可以先当成一张检查表看，前 4 条来自 Karpathy 的原始约束，后 8 条来自作者在真实代码库里的补充。*

这样列出来以后，反而更容易看清一件事：它们并不是 12 个零散的技巧。

如果按《架构师》这段时间一直在聊的 [Harness](https://mp.weixin.qq.com/s?__biz=MzAwNjQwNzU2NQ==&mid=2650409277&idx=1&sn=f73a7d925414775f9b8dfe9f2ce5ef88&scene=21#wechat_redirect) 视角看，可以把它们重新分成 4 类问题。

| 工程问题 | 对应规则 | 解决的风险 |
| --- | --- | --- |
| 控制改动半径 | 先思考、简单优先、手术式修改、先读再写 | 少猜需求，少顺手改，少重复造轮子 |
| 把确定性交还给代码 | 模型只做判断题、测试验证意图 | 不让模型充当随机 if-else，不让浅测试制造信心 |
| 长任务留下检查点 | token 预算、步骤检查点、冲突不平均 | 防止任务跑久后目标漂移、上下文漂移、模式漂移 |
| 失败显性化 | 匹配约定、失败要说清楚 | 不把跳过、未验证、不确定包装成完成 |

拆到这一层，12 条规则就不太像提示词清单了，更像一组 Harness 的薄层控制点。

它们不直接替你写代码。

它们约束的是：Agent 在写代码前后怎么观察、怎么选择、怎么汇报。

但真要放到自己的项目里，我会先删一轮。

原因也简单： `CLAUDE.md` 会进入上下文窗口。

它不是一份挂在墙上的规范。每一行都会和当前任务抢注意力，也都要消耗 token。Anthropic 自己的文档里也讲得很清楚， `CLAUDE.md` 是上下文，不是硬约束；指令最好具体、简洁、有结构，单个文件控制在 200 行以内；规则互相冲突时，Claude 可能会随机选一条。

这一点很像我们以前写工程规范的老经验。

规范太少，大家靠猜。  
规范太多，没人读。  
规范互相打架，最后靠运气。

Agent 也差不多。

一个两行的小改动，如果带着 400 行规则一起跑，结果很可能就变成：读了一堆无关文档，检查了一堆不相关的边界，绕了一圈才敢动手。

我自己会更保守一点：

**先留下那些真用得上的规则。**

这不是说 12 条不好。只是每个仓库的失败模式不一样。

没有长任务，就先别写复杂的检查点规则。  
没有多服务 monorepo，就别一上来写跨代码库风格选择。  
只是个人工具，也不用把企业审批流程搬进去。

规则文件的第一版，不用追求完整。

只要能减少最近最常见的几类错误，就已经很有用了。

这点和我们在《 [Cursor 的 Harness 方法论](https://mp.weixin.qq.com/s?__biz=MzAwNjQwNzU2NQ==&mid=2650409236&idx=1&sn=71ae43ca6ec5b3cb1f82c258b1542271&scene=21#wechat_redirect) 》里聊过的 dead weight 清理是同一回事。模型会变，团队会变，项目结构也会变。当初为某个老问题加进去的规则，过一阵子可能只是噪声。规则文件不是越厚越稳，最怕的是厚得没有理由。

---

## 好规则通常不是写出来的，是摔出来的

我现在写 `CLAUDE.md` ，会先翻 Agent 最近几次翻车的记录。

它是不是没读调用方，就在旁边又写了一个重复函数？  
它是不是修 bug 时顺手格式化了半个文件？  
它是不是测试没跑完，就说“全部通过”？  
它是不是把 503 重试交给模型判断，而不是写成普通的 if-else？  
它是不是看到两套错误处理模式后，各拿一半，拼出了第三种？

这些现场，比“请保持代码优雅”这种话有用得多。

比如 Agent 经常乱跑命令，不要写：

```
- Be careful when running commands.
```

这句话太虚。

可以改成：

```
- Use \`pnpm test --filter <package>\` for package-level tests.
- Do not run full integration tests unless the task touches cross-service behavior.
- If a command fails because of missing local services, report the missing service instead of retrying blindly.
```

如果 Agent 经常改太大，也不要只写：

```
- Keep changes minimal.
```

可以写得更像项目里的真实约定：

```
- Do not reformat files outside the edited block.
- Do not rename public APIs unless the task explicitly asks for it.
- If a cleanup is useful but not required, mention it as follow-up instead of doing it now.
```

如果 Agent 经常写浅测试，也别只写 “write better tests”。

可以这样写：

```
- A test should fail if the business rule changes.
- Do not test only that a function returns a value.
- Cover the requested edge case before adding broad happy-path tests.
```

这些句子没有什么传播感。

但它们能改变下一次行为。

这里大概就是规则文件值钱的地方。

---

## 先写一份 80 行版本

如果现在让我给一个仓库补 `CLAUDE.md` ，我不会先写长文档。

我会先写一个很小的版本。

```
# CLAUDE.md

These instructions apply to this repository unless a more specific instruction overrides them.

## Working style

- State assumptions before making non-trivial changes.
- Keep changes small and scoped to the request.
- Read the surrounding code before editing.
- Match existing conventions even when another style looks cleaner.
- If existing patterns conflict, choose the newer or better-tested one and say why.
- Do not refactor adjacent code unless the task explicitly asks for it.
- If unsure, stop and ask instead of guessing.

## Verification

- Run the smallest relevant test first.
- If tests are skipped, say exactly which tests were skipped and why.
- Do not report success unless the requested behavior was verified.
- Prefer deterministic tools for formatting, linting, renaming, and validation.

## Project commands

- Install: TODO
- Type check: TODO
- Lint: TODO
- Unit test: TODO
- Integration test: TODO

## Project conventions

- TODO: Error handling pattern.
- TODO: Logging pattern.
- TODO: API/client pattern.
- TODO: Test data and fixture pattern.

## Safety boundaries

- Do not modify TODO without explicit approval.
- Do not run destructive commands without explicit approval.
- For migrations, produce a plan and dry-run output before changing data.
```

这份模板不复杂，但足够开工。

更要花时间填的，是里面的 TODO。

一个团队最容易漏掉的，往往不是“要不要让 Agent 小心”这种提醒，反倒是这些具体问题：

- • 本项目到底怎么安装依赖？
- • 局部测试命令是什么？
- • 哪些目录属于生成代码，不该手工改？
- • 错误处理有没有统一入口？
- • 数据库 migration 有没有 dry-run？
- • 哪些命令会改线上状态？
- • 测试跳过时，怎么汇报？

这些写清楚，比加 20 条“请保持最佳实践”更有用。

---

## 三层文件，比一个大文件稳

`CLAUDE.md` 最容易写成大杂烩。

项目背景、技术栈、部署流程、目录说明、测试策略、设计原则、故障排查，全塞进去。看起来挺完整，实际每次任务都背着一大包上下文走。

这里可以接上前面那篇 `.claude/` 文章里的看法： `CLAUDE.md` 不适合做百科全书，它更适合放“每次都值得带上”的东西。目录结构、权限边界、命令封装、任务模板，都可以有自己的位置，不一定都挤在这个文件里。

这篇就不再把 `.claude/` 全家桶讲一遍，只看 `CLAUDE.md` 这块最容易被写坏的小文件。

![图片](data:image/svg+xml,%3C%3Fxml version='1.0' encoding='UTF-8'%3F%3E%3Csvg width='1px' height='1px' viewBox='0 0 1 1' version='1.1' xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg stroke='none' stroke-width='1' fill='none' fill-rule='evenodd' fill-opacity='0'%3E%3Cg transform='translate(-249.000000, -126.000000)' fill='%23FFFFFF'%3E%3Crect x='249' y='126' width='1' height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

CLAUDE.md 的加载层级

*图：前面聊 `.claude/` 时整理过的一张图。规则最终都会进入会话上下文，越靠近入口，越要短、稳、少冲突。*

我自己更倾向于分三层。

第一层，根目录 `CLAUDE.md` 。

只放高频行为约定：先读再写、小切片、少顺手改、测试要说明、失败要说清楚。控制在 80 到 120 行。

第二层，项目事实文件。

比如 `docs/agent/project.md` 。放命令、目录边界、错误处理模式、日志约定、共享工具入口。

第三层，任务流程文件。

比如：

- • `docs/agent/migrations.md`
- • `docs/agent/api-endpoint.md`
- • `docs/agent/ui-components.md`
- • `docs/agent/release-checklist.md`

主文件只做索引：

```
## Task references

- For database migrations, read \`docs/agent/migrations.md\`.
- For new API endpoints, read \`docs/agent/api-endpoint.md\`.
- For UI component changes, read \`docs/agent/ui-components.md\`.
```

这和我们前面聊《Agent Harness 上下文管理：聊天记录还是工作集？》是同一条线。

上下文窗口不是资料仓库。当前任务需要什么，就让什么靠近模型；低频流程留在外面，要用的时候再读。

这里也能接上《 [长周期 Agent 详解：从 Ralph Loop 到可接管 Harness](https://mp.weixin.qq.com/s?__biz=MzAwNjQwNzU2NQ==&mid=2650409301&idx=1&sn=11fd501a836542bcccc7b4fec03fb43e&scene=21#wechat_redirect) 》的思路。能长期复用的，往往不是一段无限长的聊天记录，而是那些被整理成文件、规则、脚本、检查清单的过程资产。

`CLAUDE.md` 只是其中最朴素的一类。

它不负责记住所有历史，只负责把高频、稳定、跨任务都用得上的经验放在入口处。

---

## 规则救不了一个没有验证的系统

这里要补一句不太讨巧的话。

`CLAUDE.md` 再好，也只是一种提醒。

它提醒 Agent 少乱改，但没办法真的阻止它乱改。  
它要求测试，但不能保证测试写对。  
它要求失败说清楚，但不能自动发现所有沉默失败。  
它提醒 Agent 别碰危险文件，但最后拦住危险动作的，还是权限、hooks、CI 和 review。

我自己不太愿意把 `CLAUDE.md` 神化。

它更像 Harness 里最轻的一层：事前引导。

这个坑我自己也踩过。只在 `CLAUDE.md` 里写“不要读 `.env` ”，心里会踏实一点，但说到底还是一句提醒。真要拦住这类动作，还是要在 `settings.json` 里 deny，或者用 hook 在命令执行前挡住。

前者解决“应该怎么做”，后者解决“能不能这么做”。这两个东西混在一起，文章看着完整，系统并不会因此更稳。

外面还得接上确定性反馈：

- • formatter、lint、类型检查，管格式和静态错误；
- • 单元测试、集成测试，管行为；
- • hooks 和权限，管动作边界；
- • CI 和 review，管合并前检查；
- • 日志、指标、线上信号，管合并后的真实效果。

![图片](data:image/svg+xml,%3C%3Fxml version='1.0' encoding='UTF-8'%3F%3E%3Csvg width='1px' height='1px' viewBox='0 0 1 1' version='1.1' xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg stroke='none' stroke-width='1' fill='none' fill-rule='evenodd' fill-opacity='0'%3E%3Cg transform='translate(-249.000000, -126.000000)' fill='%23FFFFFF'%3E%3Crect x='249' y='126' width='1' height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

Claude hooks 生命周期

*图： `CLAUDE.md` 是提醒，hooks 和权限更像门禁。前者告诉 Agent 怎么做，后者决定危险动作能不能发生。*

Mitchell Hashimoto 在《My AI Adoption Journey》里有个说法我挺喜欢：Agent 犯错后，不能只修这一次，还要顺手补一个机制，让同类错误以后更难再发生。

有些机制是一条 `AGENTS.md` 规则。

更可靠的机制，往往是一个工具。

比如 Agent 总说“页面看起来没问题”，那就给它一个截图脚本；它总跑全量测试浪费时间，就给它一个过滤测试脚本；它总漏掉某类边界，就把边界直接写进测试或 lint。

我理解的 `Engineer the Harness` ，大概就是这件事。

重点不在把提示词写得更玄，在于让 Agent 更容易知道自己错了。

这也呼应了 Martin Fowler 那条提醒：非确定性一旦进了研发链路，确定性反馈反而更值钱。模型可以生成、解释、修复，但最后能不能交付出去，还得靠测试、类型、权限、日志和 review 来兜。

没有这些外部反馈， `CLAUDE.md` 写得再漂亮，也只是一条更有礼貌的建议。

---

## 一个可以直接照着做的小抄

如果手边正好有一个仓库，我会按这个顺序做：

1. 1\. 拉一份最小模板，可以用 Forrest Chang 的模板，也可以用上面那份骨架。
2. 2\. 删到 120 行以内，只留当前项目真的用得上的规则。
3. 3\. 补 5 条项目命令：安装、类型检查、lint、局部测试、全量测试。
4. 4\. 补 5 条项目边界：危险目录、只读文件、禁止命令、数据 dry-run、测试跳过汇报。
5. 5\. 找一个真实小 bug 试跑，不要用玩具任务。
6. 6\. 看 Agent 有没有少问重复问题、少做无关改动、验证汇报有没有更清楚。
7. 7\. 只根据真实失败继续改，不因为“看起来更完整”继续加规则。

这套流程不复杂。

但它有一个好处：规则文件会跟着真实问题长出来。

而不是一次生成一大坨，然后没人敢删。

---

## 我会避开的几种写法

第一种，身份提示。

“你是资深工程师”“你要写生产级代码”这种话可以有，但别指望它真能解决问题。模型本来就会装出一副自己很懂的样子。

更有用的是告诉它：在这个仓库里，生产级代码具体长什么样。

第二种，空泛提醒。

“注意安全”“保持优雅”“考虑边界”“遵循最佳实践”，这些话人看着舒服，Agent 真要执行的时候根本不知道做什么。

能换成具体命令、具体文件、具体模式，就别停在抽象词上。

第三种，禁止清单。

一连串“不要”会让 Agent 变谨慎，但未必变正确。能写成“不要 X，请用 Y”，就尽量写完整。

第四种，永不过期。

规则文件不是祖训。模型升级、框架迁移、测试策略变化之后，旧规则可能反而会误导 Agent。每隔一段时间删一轮，比不断追加更重要。

---

## 写在最后

Karpathy 那 4 条规则值得看，Forrest Chang 的仓库也值得下载，Mnimiy 扩到 12 条的长文里也提供了不少真实失败样本。

但我读完之后，最想留下来的不是“12 条规则”这个数字。

是一个更小的动作：

**把 Agent 昨天犯过的错，写成它明天开工前能读懂的约定。**

这件事不算复杂。

它和我们以前写 README、写 Runbook、写 lint rule、写 CI check 是同一条线。区别只是现在多了一个会读这些文件、也会误读这些文件的协作者。

所以别把 `CLAUDE.md` 当许愿池。

也别把它当一次性模板。

把它当成一份会过期、要删减、要跟着事故复盘一起更新的小文档。

如果它能让 Agent 少猜一次命令、少碰一个危险文件、少说一句没验证的“完成了”，那这份文件就已经很值。

往上再看一层，这就是 Agentic Engineering 很小的一步。

前面我们聊过：开发工具正在从 IDE 变成 Agent 控制台；长周期 Agent 要留下可接管的现场；Cursor 把 Harness 当成持续运营的软件产品在做。 `CLAUDE.md` 没有那么大，但它就在同一条链路上：把人的工程判断，变成 Agent 下次开工前就能继承的那一点约束。

如果说前面那篇 `.claude/` 文章聊的是地基怎么摆，这篇更像是把其中一块砖拿出来多看了一眼： `CLAUDE.md` 很小，但它最容易被写满，也最容易写虚。

这不是终点。

但它确实是很多团队今天就能补上的第一层。

---

## 参考资料

- • Mnimiy：Karpathy's 4 CLAUDE.md rules cut Claude mistakes from 41% to 11%. After 30 codebases, I added 8 more  
	https://x.com/Mnilax/article/2053116311132155938
- • Forrest Chang：andrej-karpathy-skills  
	https://github.com/forrestchang/andrej-karpathy-skills
- • 原始 `CLAUDE.md` 下载  
	https://raw.githubusercontent.com/forrestchang/andrej-karpathy-skills/main/CLAUDE.md
- • Anthropic：How Claude remembers your project  
	https://code.claude.com/docs/en/memory
- • Anthropic：Best practices for Claude Code  
	https://code.claude.com/docs/en/best-practices
- • Mitchell Hashimoto：My AI Adoption Journey  
	https://323.santiago.bz/wp-content/uploads/2026/02/mitchellh.com-My-AI-Adoption-Journey.pdf
- • Tobi Lütke：Context engineering vs. prompt engineering  
	https://x.com/tobi/status/1935533422589399127
- • Evaluating AGENTS.md: Are Repository-Level Context Files Helpful for Coding Agents?  
	https://arxiv.org/abs/2602.11988
- • On the Impact of AGENTS.md Files on the Efficiency of AI Coding Agents  
	https://arxiv.org/abs/2601.20404
- 如喜欢本文，请点击右上角，把文章分享到朋友圈
	如有想了解学习的技术点，请留言给若飞安排分享
	**因公众号更改推送规则，请点“在看”并加“星标”第一时间获取精彩技术分享**
	**·END·**
	```
	相关阅读：
	```
	> 版权申明：内容来源网络，仅供学习研究，版权归原创者所有。如有侵权烦请告知，我们会立即删除并表示歉意。谢谢!
	**架构师**
	我们都是架构师！
	![图片](data:image/svg+xml,%3C%3Fxml version='1.0' encoding='UTF-8'%3F%3E%3Csvg width='1px' height='1px' viewBox='0 0 1 1' version='1.1' xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg stroke='none' stroke-width='1' fill='none' fill-rule='evenodd' fill-opacity='0'%3E%3Cg transform='translate(-249.000000, -126.000000)' fill='%23FFFFFF'%3E%3Crect x='249' y='126' width='1' height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)
	****关注** 架构师(JiaGouX)，添加“星标”**
	**获取每天 AI 技术干货，一起成为牛逼架构师**
	**AI/Agent群请** **加若飞：** **1321113940** **进群**
	投稿、合作、版权等邮箱： **admin@137x.com**
- [如何让单个 Agent 做长任务不失真：Anthropic 给出了一套更工程化的答案](https://mp.weixin.qq.com/s?__biz=MzAwNjQwNzU2NQ==&mid=2650408877&idx=1&sn=d27eb9e99ed526e342df775f0291cb2e&scene=21#wechat_redirect)
	- [Claude Code高手的 8 个 Claude Code 实战习惯](https://mp.weixin.qq.com/s?__biz=MzAwNjQwNzU2NQ==&mid=2650408884&idx=1&sn=6a2fa56f70f15cdd75eb5c2b12e687ef&scene=21#wechat_redirect)
	- [别从 README 开始：一个架构师会怎样翻 Codex 仓库](https://mp.weixin.qq.com/s?__biz=MzAwNjQwNzU2NQ==&mid=2650408870&idx=1&sn=ba53595a44ab55396b36795fbc78791b&scene=21#wechat_redirect)
	- [Spec 不是代码的替代品，它是 AI Coding 的上下文管理层](https://mp.weixin.qq.com/s?__biz=MzAwNjQwNzU2NQ==&mid=2650408860&idx=1&sn=b882b2ee97e3f798fea96e68d27c7071&scene=21#wechat_redirect)
	- [如何让 Agents 自己设计、升级 Agents](https://mp.weixin.qq.com/s?__biz=MzAwNjQwNzU2NQ==&mid=2650408848&idx=1&sn=aabf785116e9849dbd301a4f7c477181&scene=21#wechat_redirect)
	- [OpenAI怎么把开源项目维护做成工作流：Skills、AGENTS.md 和 CI 的一套组合拳](https://mp.weixin.qq.com/s?__biz=MzAwNjQwNzU2NQ==&mid=2650408832&idx=1&sn=ef00408738c853ea2e94be58c0612e51&scene=21#wechat_redirect)
	- [Claude Skills 入门：把“会用 AI”变成“可复制的工程能力”](https://mp.weixin.qq.com/s?__biz=MzAwNjQwNzU2NQ==&mid=2650408200&idx=1&sn=2f2cce7dfcbdb0766eac3590f777a17b&scene=21#wechat_redirect)
	- [一套可复制的 Claude Code 配置方案：CLAUDE.md、Rules、Commands、Hooks](https://mp.weixin.qq.com/s?__biz=MzAwNjQwNzU2NQ==&mid=2650408189&idx=1&sn=7d4f7a442a22af37f95c46ff1048a3df&scene=21#wechat_redirect)
	- [Claude Code 最佳实践：把上下文变成生产力（团队可落地版）](https://mp.weixin.qq.com/s?__biz=MzAwNjQwNzU2NQ==&mid=2650408183&idx=1&sn=0b6f1437465d3a61118db688cc889b17&scene=21#wechat_redirect)
	- [把 AI 当成新同事：Agent Coding 的上下文与验证体系](https://mp.weixin.qq.com/s?__biz=MzAwNjQwNzU2NQ==&mid=2650408169&idx=1&sn=7bba1377a31ffa0ce68932935c8d923a&scene=21#wechat_redirect)
	- [一周写百万行的背后：Cursor长时间运行 Agent 的工程方法论](https://mp.weixin.qq.com/s?__biz=MzAwNjQwNzU2NQ==&mid=2650408161&idx=1&sn=85aaff6f2f779e53b6ae9c5e1f003269&scene=21#wechat_redirect)
	- [我真不敢相信，AI 先加速的是工程师。](https://mp.weixin.qq.com/s?__biz=MzAwNjQwNzU2NQ==&mid=2650408153&idx=1&sn=d33b48464de93a2573a0a0cb025ada9e&scene=21#wechat_redirect)
	- [扒一扒 Claude Cowork 系统提示词：Anthropic 如何打造数字同事](https://mp.weixin.qq.com/s?__biz=MzAwNjQwNzU2NQ==&mid=2650408128&idx=1&sn=1b6c640de61986d1364847bffb2cd28f&scene=21#wechat_redirect)
	- [Cowork 安全架构深度解析：从 Claude Code 到 Cowork，Anthropic 如何把“可控”做成产品](https://mp.weixin.qq.com/s?__biz=MzAwNjQwNzU2NQ==&mid=2650408114&idx=1&sn=29a754281cd07c16b6191c6d146c5837&scene=21#wechat_redirect)
	- [Anthropic官方万字长文：AI Agent评估的系统化方法论](https://mp.weixin.qq.com/s?__biz=MzAwNjQwNzU2NQ==&mid=2650408107&idx=1&sn=905552d68f5b174fd9548360bdea4448&scene=21#wechat_redirect)
	- [银弹还是枷锁？Claude Agent SDK 的架构真相](https://mp.weixin.qq.com/s?__biz=MzAwNjQwNzU2NQ==&mid=2650408084&idx=1&sn=82f274ba084f9c289e2d141aad0c088b&scene=21#wechat_redirect)
	- [Claude Code创始人亲授13条使用技巧](https://mp.weixin.qq.com/s?__biz=MzAwNjQwNzU2NQ==&mid=2650408076&idx=1&sn=f139e90d699b528e80e79c558eed42ee&scene=21#wechat_redirect)
	- [Claude Code 内部工具开源 code-simplifier：终结 AI 屎山代码的终极方案](https://mp.weixin.qq.com/s?__biz=MzAwNjQwNzU2NQ==&mid=2650408028&idx=1&sn=3a8571a9fa0bd5d7e59cd66fc6187b3e&scene=21#wechat_redirect)
- [刚刚，Claude Code“代码泄露”背后：如何重新看 Agent Harness](https://mp.weixin.qq.com/s?__biz=MzAwNjQwNzU2NQ==&mid=2650408930&idx=1&sn=2fd7f3701ae8688e7720f80bb8296936&scene=21#wechat_redirect)
	- [大家都在讲 Harness，但它到底该怎么理解](https://mp.weixin.qq.com/s?__biz=MzAwNjQwNzU2NQ==&mid=2650408900&idx=1&sn=93bbae7c90fc03fb510f450c6fee97e0&scene=21#wechat_redirect)
	- [模型越来越强，为什么大家却开始重写 Harness](https://mp.weixin.qq.com/s?__biz=MzAwNjQwNzU2NQ==&mid=2650408891&idx=1&sn=639dc4a7c8482f6e1ac04d8d53c63459&scene=21#wechat_redirect)

agent · 目录

继续滑动看下一个

架构师

向上滑动看下一个