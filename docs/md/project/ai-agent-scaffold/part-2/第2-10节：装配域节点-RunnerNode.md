---
title: 第2-10节：装配域节点-RunnerNode
pay: https://t.zsxq.com/pEBw8
---

# 《AI Agent 脚手架》第2-10节：装配域节点-RunnerNode

作者：小傅哥
<br/>博客：[https://bugstack.cn](https://bugstack.cn)
<br/>视频：[https://t.zsxq.com/tMfj3](https://t.zsxq.com/tMfj3)

> 沉淀、分享、成长，让自己和他人都能有所收获！😄

## 一、本章诉求

把构建的智能体，填充到 InMemoryRunner 中，以及注册到 Spring 容器中。这样后续就可以使用 Spring 容器中的对象，进行 AI Agent 对话了。

>目前是把最后构建的 SequentialAgent 写入到 InMemoryRunner 中，后续会做成动态的，让配置任何的一个智能体都可以填充到 InMemoryRunner 中。

## 二、流程设计

如图，智能体构建完成后，则填充到 InMemoryRunner 中；

<div align="center">
	<img src="https://bugstack.cn/images/article/project/ai-agent-scaffold/part-2/2-10/images/ai-agent-scaffold-2-10-01.png" width="700px"/>
</div>

- 从 SequentialAgentNode 节点，流转到 RunnerNode 节点。
- 在 RunnerNode 节点，创建 InMemoryRunner 以及注册到 Spring 容器。这样可以任何一个地方获取到执行对象。