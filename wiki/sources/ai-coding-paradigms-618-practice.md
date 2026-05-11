---
title: "1个场景(618促销)5种范式(Spec/Vibe/Glue/TDD/Harness) ，企业级AI Coding经验分享"
type: source
status: active
updated: 2026-05-11
source_count: 1
---

# Source: 1个场景(618促销)5种范式，企业级AI Coding经验分享

## Metadata

- Raw file: `raw/sources/ai-coding-paradigms-618-practice.md`
- Author: 吕昭波
- Date: 2026-05-10
- URL: https://mp.weixin.qq.com/s/8dRi3pApghRhMtXh0HWmHg
- Publisher: 微信公众号「沐然云计算」

## Summary

- 以618促销项目为单一场景，系统化对比五种AI Coding研发范式：Spec Coding（文档先行）、TDD（测试先行）、Glue Coding（复用先行）、Harness（自动化先行）、Vibe Coding（体验先行）。
- 核心发现：范式无优劣，场景定选择——不同项目阶段应灵活组合使用不同范式。
- 强调"资产复用"是效率关键：复用春节促销和周年庆的Reference代码，618核心功能开发周期缩短60%，代码复用率达70%。
- 提供完整的量化对比（开发周期、复用率、测试覆盖率、人力成本）和场景匹配矩阵，帮助团队做范式选型。
- 覆盖PM角色在不同范式中的职责变化和跨角色协作流程。

## Key Claims

- **范式无优劣，场景定选择**：Spec Coding重文档、TDD重质量、Glue Coding重效率、Harness重交付、Vibe Coding重体验，应根据项目阶段和需求特点灵活组合。
- **资产复用是效率关键**：复用春节促销和周年庆的Reference代码，核心功能开发周期缩短60%，代码复用率达70%。
- **Glue Coding 适合促销/快速迭代**："天下文章一大抄"——项目中已有稳定代码框架时，没必要让AI重新生成，否则会带来更多隐患和检查代价。
- **基于Spec的TDD比纯TDD更严谨**：结合已有的Spec文档定义"成功的标准"，让测试用例有文档支撑。
- **Harness 是框架，限制边界**：不只做CI/CD，更是一个约束交付边界的自动化框架。
- **Vibe Coding 在企业场景有用**：A/B测试驱动的UI优化、情感化设计、数据驱动决策，在促销活动页面场景价值显著。
- **618实战关键数据**：代码复用率70%、开发周期2周、测试覆盖率85%、部署时间<10分钟、系统可用性99.95%。

## Evidence Notes

- 文章基于真实的企业级618促销项目，使用Mock数据避免客户信息泄露，但逻辑和技术栈是真实的。
- 代码示例均为Java/Spring Boot生态，Reference代码结构（SpringFestivalPromotionService、AnniversaryCouponService）有具体的方法签名。
- 量化数据（60%开发周期缩短、70%复用率、85%测试覆盖）为项目实测，非理论推演。
- Spec Coding部分列出了14份Spec文档编号索引，显示文档化程度高。

## Contradictions / Tensions

- 文章声称"Glue Coding开发速度快"且"代码质量有保障（经过验证的代码）"，但同时标注"可能引入不必要的依赖"和"技术债务"——速度与质量之间存在未完全调和的张力。
- 文章称"Vibe Coding用户体验优先，转化率提升明显"，但其量化对比表中Vibe Coding的测试覆盖率仅30%，低于其他范式——在"体验优先"和"质量可控"之间的权衡未展开讨论。
- 五范式分类与本 wiki 已有的 [[concepts/spec-driven-workflow-and-review-discipline]] 和 [[concepts/tdd-as-hard-gate]] 有交叉但不完全重合——本文的"Spec Coding"更偏向需求规格驱动，而本 wiki 中的 OpenSpec 更偏向变更追踪和规格纪律。
- Glue Coding 的"复用优先"理念与 [[concepts/reference-projects-as-context]] 有共鸣，但本文侧重代码级复用（注入 Service），而非知识级复用（submodule 引入源码供 AI 阅读）。

## Linked Entities

- [[entities/lv-zhaobo]]
- [[entities/muran-cloud]]

## Linked Concepts

- [[concepts/spec-coding]]
- [[concepts/glue-coding]]
- [[concepts/vibe-coding]]
- [[concepts/paradigm-composition]]
- [[concepts/tdd-as-hard-gate]]
- [[concepts/ai-ci-cd-automation]]

## Follow-up Questions

- Glue Coding 的技术债务管理策略——在"快速复用"与"债务积累"之间，实际团队如何设定重构触发点？
- Vibe Coding 的 A/B 测试基础设施在中小团队中最低可行方案是什么？是否需要自建还是有开源/低价替代？
- 五范式是否覆盖了所有企业级AI Coding场景？是否存在遗漏的范式（如文档生成范式、测试数据生成范式）？
- "基于Spec的TDD"在Spec文档尚未完成时如何启动？是否存在"边写Spec边TDD"的混合模式？
- 文章中PM角色变化的讨论是否隐含了一种"范式决定组织结构"的假设？这种假设在实际组织中是否成立？
