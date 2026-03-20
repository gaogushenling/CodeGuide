---
title: 【更】第2-12节：增强装配-RunnerNode
pay: https://t.zsxq.com/jxbVS
---

# 《AI Agent 脚手架》第2-12节：增强装配-RunnerNode

作者：小傅哥
<br/>博客：[https://bugstack.cn](https://bugstack.cn)
<br/>视频：[https://t.zsxq.com/Ls0hf](https://t.zsxq.com/Ls0hf)

> 沉淀、分享、成长，让自己和他人都能有所收获！😄

## 一、本章诉求

基础的智能体装配一个链路做完，并验证了会话的设计，让整个链路跑通。之后我们做一下增强设计操作。让整个智能体可以在后续适应更多的场景使用。

这一节，我们先来做下 RunnerNode 的增强，也就是前面提到的，用户如果只是配置一个基础的 Agent 不在配置其他的 loop（循环）、parallel（并行）、sequential（序列），就结束了。那么这里要怎么流转到 RunnerNode。

## 二、流程设计

如图，从 AgentWorkflowNode 流转到 RunnerNode 设计；

<div align="center">
	<img src="https://bugstack.cn/images/article/project/ai-agent-scaffold/part-2/2-12/images/ai-agent-scaffold-2-12-01.png" width="700px"/>
</div>

- 首先，在有了前面的内容学习后，我们了解到 RunnerNode 会做 InMemoryRunner 的构建，而这个对象的构建是需要拿到 SequentialAgentNode 作为最后一个节点，构建的 SequentialAgent 写入到上下文，到 RunnerNode 节点使用。它的核心本质是拿到 InMemoryRunner 创建的时候，所需 Agent 智能体。
- 之后，这个 Agent 智能体，不非得以一个固定的写死，而是可以在配置文件中添加以 runner 配置，指定装配到 runner 中的 agent 名称。之后在 RunnerNode 构建 InMemoryRunner 的时候，则从上下文通过智能体名称获取 agent 装配进来即可。
- 最后，思考下，AgentWorkflowNode 什么时候流转，这个流转则是根据当前 agentWorkflows 是不为空了，为空则直接流转到 RunnerNode 即可。RunnerNode 会根据配置的关联 agentName 进行配置。`这部分看代码的yml文件会更加清晰`
