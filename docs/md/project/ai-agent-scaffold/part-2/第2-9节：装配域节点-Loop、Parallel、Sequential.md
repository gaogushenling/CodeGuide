---
title: 第2-9节：装配域节点-Loop、Parallel、Sequential
pay: https://t.zsxq.com/t29lj
---

# 《AI Agent 脚手架》第2-9节：装配域节点-Loop、Parallel、Sequential

作者：小傅哥
<br/>博客：[https://bugstack.cn](https://bugstack.cn)
<br/>视频：[https://t.zsxq.com/6NKGA](https://t.zsxq.com/6NKGA)

> 沉淀、分享、成长，让自己和他人都能有所收获！😄

## 一、本章诉求

从 AgentWorkflowNode 开始，要进入 LoopAgent、ParallelAgent、SequentialAgent，这几个节点都是类似的，我们一起来处理下。

## 二、流程设计

如图，智能体装配中，LoopAgentNode、ParallelAgentNode、SequentialAgentNode 部分；

<div align="center">
	<img src="https://bugstack.cn/images/article/project/ai-agent-scaffold/part-2/2-9/images/ai-agent-scaffold-2-9-01.png" width="700px"/>
</div>

- LoopAgentNode - 处理循环操作，如一个用户请求，要进行分析、执行、检测，也可以是一段git提交的代码，进行 diff 获取差异，检索代码匹配召回、做出执行review计划，后面在依次执行分析。这些都是可以做循环处理的。
- ParallelAgentNode - 处理并行操作，如我们有一些场景，需要同步并行的一起完成数据处理任务，多条链路一起完成数据的获取、分析和决策，这样可以对复杂的流程显著的提高执行效率。
- SequentialAgentNode - 处理串行操作，主要用于编排子智能体，和 loop 循环、parallel 并行，组合出复杂的智能体流程。当然，你也可以使用 loop 组合 sequence 或者 parallel 等处理过程。
