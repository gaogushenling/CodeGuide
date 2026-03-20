---
title: 【更】第2-7节：装配域节点-AgentNode
pay: https://t.zsxq.com/908Fo
---

# 《AI Agent 脚手架》第2-7节：装配域节点-AgentNode

作者：小傅哥
<br/>博客：[https://bugstack.cn](https://bugstack.cn)
<br/>视频：[https://t.zsxq.com/PFBNl](https://t.zsxq.com/PFBNl)

> 沉淀、分享、成长，让自己和他人都能有所收获！😄

## 一、本章诉求

这一节从 ChatModelNode 节点流转 AgentNode 节点，做智能体 LlmAgent 的实例化操作，以及实现 AgentNode 装配操作。

## 二、流程设计

如图，智能体装配中，AgentNode 部分；

<div align="center">
	<img src="https://bugstack.cn/images/article/project/ai-agent-scaffold/part-2/2-7/images/ai-agent-scaffold-2-7-01.png" width="600px"/>
</div>

- 首先，AgentNode 节点是由 ChatModelNode 节点流转过来的，每个节点的流转都是类似的操作，处理完业务功能后，则路由到下一个节点继续完成其他业务。
- 之后，AgentNode 是一个多 LlmAgent 装配的过程，我们在配置智能体的时候，有一些复杂的场景则要多个 LlmAgent 分别做不同的事情，来完成一个整体的流程。所以这类的智能体是多个 LlmAgent 配置。