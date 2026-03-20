---
title: 【更】第2-8节：装配域节点-AgentWorkflowNode
pay: https://t.zsxq.com/3mjk1
---

# 《AI Agent 脚手架》第2-8节：装配域节点-AgentWorkflowNode

作者：小傅哥
<br/>博客：[https://bugstack.cn](https://bugstack.cn)
<br/>视频：[https://t.zsxq.com/3EdmN](https://t.zsxq.com/3EdmN)

> 沉淀、分享、成长，让自己和他人都能有所收获！😄

## 一、本章诉求

在 AiApi、ChatModel、Agent 装配完成后，接下来要进入到智能体工作流编排的操作了，他们的组合可能是 LoopAgent 把几个 LlmAgent 作为子 Agent，也有可能是 ParallelAgent 把几个 LlmAgent 作为并行，最后又会被 SequentialAgent 串行使用。

正是因为这块能有多重组合，所以，我们才需要有一个流转判断器的节点，让这些节点的执行可以串联起来。

## 二、流程设计

如图，智能体装配中，AgentWorkflowNode 部分；

<div align="center">
	<img src="https://bugstack.cn/images/article/project/ai-agent-scaffold/part-2/2-8/images/ai-agent-scaffold-2-8-01.png" width="700px"/>
</div>

- 首先，这一节重点设计关于 AgentWorkflowNode 到其他3个节点节点的流转操作，包括；LoopAgent、ParallelAgentNode、SequentialAgentNode，并最终由 SequentialAgentNode 作为结束，也就是最后是一个序列化的执行。
- 注意，LoopAgent、ParallelAgentNode、SequentialAgentNode 这三个节点，本节只关注他们的流转操作，后续在做具体的节点功能实现。
- 另外，还有一种可能，就是单一智能体 LlmAgent 直接作为结束，没有配置 SequentialAgentNode 包装一层序列化执行，后续在扩展这部分。