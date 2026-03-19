---
title: 第2-15节：增强装配-回调plugin
pay: https://t.zsxq.com/U1p49
---

# 《AI Agent 脚手架》第2-15节：增强装配-回调plugin

作者：小傅哥
<br/>博客：[https://bugstack.cn](https://bugstack.cn)
<br/>视频：[https://t.zsxq.com/tTIdy](https://t.zsxq.com/tTIdy)

> 沉淀、分享、成长，让自己和他人都能有所收获！😄

## 一、本章诉求

为 InMemoryRunner 运行体扩展 Plugin 插件能力，允许用户在智能体执行的各个阶段获取到上下文信息，并做出一定的监控、调整、治理的动作。

如果你有学习过星球「码农会锁」的扳手工程，在设计模式框架章节，有一个 `applyBefore`、`applyAfter`、`applyAfterError` 的处理，它可以让你在使用的阶段做拦截或者打印最后的结果。这些设计都是相同的，所以说学编程，最后都是学的思想。语言就像你的盗抢棍棒，斧钺钩叉，思想才是你的一招一式。

## 二、流程设计

如图，增强运行体插件配置，可以在各个节点埋入钩子；

<div align="center">
	<img src="https://bugstack.cn/images/article/project/ai-agent-scaffold/part-2/2-15/images/ai-agent-scaffold-2-15-01.png" width="950px"/>
</div>

- Runner 的 Plugin 通过回调钩子在 AI Agent 运行流程生命周期的各个阶段执行。包括；用户输入信息、调用模型、调用工具、智能体执行等步骤中。这一工具，可以用在日志记录、性能分析、步骤调试、策略执行（权限）、监控对接（普罗米修斯）、请求或响应的调整（如敏感词的处理）等。
- 这些操作的步骤，就是图上的各个阶段的节点，可以被采集到。就像你设置的任何一个智能体 Agent 都可以拿到它的运行信息，甚至你可以在上下文中做一些拦截操作。
