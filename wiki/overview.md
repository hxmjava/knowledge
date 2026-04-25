---
title: 总览
type: overview
status: active
updated: 2026-04-25
source_count: 5
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

## 活跃主题

- LLM 辅助的增量知识编译
- 将持久 wiki 维护作为复利型工作流
- 用 schema 驱动 agent 行为，保持操作一致性
- 面向 AI 编码的团队治理、权限控制和 CI/CD 自动化
- 规格优先开发（OpenSpec）与执行治理（Superpowers）结合
- 基于场景选择工作流：核心模块走完整链路，热修走最小流程
- 单一事实来源（SSOT）纪律，避免文档版本漂移
- 分层项目 harness：common/service/app/message 配套专属 agents 和验证策略
- 将 TDD 作为硬门禁：生产代码遵循 Red-Green-Refactor，并有显式例外流程
- 生命周期 hooks 作为轻量安全网（fail-open，仅提醒）
- 持久化 agent 记忆支撑跨会话连续性
- 渐进式披露检索在记忆深度与上下文成本之间取得平衡

## 证据基础

- 当前来源集合：
  - [[sources/llm-wiki-pattern]]
  - [[sources/claude-code-enterprise-playbook]]
  - [[sources/openspec-superpowers-practice-guide]]
  - [[sources/ai-template2-scaffold]]
  - [[sources/claude-mem]]

## 开放线索

- 对比个人知识编译模式与企业治理约束。
- 确定小团队权限与审计的最低基线策略。
- 定义触发完整规格驱动执行链路的任务规模阈值。
- 定义自动捕获 agent 记忆的隐私、修剪和审计规则。
