---
title: 【更】第2-6节：装配域节点-ChatModelNode
pay: https://t.zsxq.com/mnTej
---

# 《AI Agent 脚手架》第2-6节：装配域节点-ChatModelNode

作者：小傅哥
<br/>博客：[https://bugstack.cn](https://bugstack.cn)
<br/>视频：[https://t.zsxq.com/X0HRO](https://t.zsxq.com/X0HRO)

> 沉淀、分享、成长，让自己和他人都能有所收获！😄

## 一、本章诉求

这一节从 AiApiNode 节点流转 ChatModelNode 模型对话节点的实例化操作，以及实现 ChatModelNode 装配操作。

## 二、流程设计

如图，智能体装配中 ChatModelNode 部分；

<div align="center">
	<img src="https://bugstack.cn/images/article/project/ai-agent-scaffold/part-2/2-6/images/ai-agent-scaffold-2-6-01.png" width="400px"/>
</div>

- 首先，这一个节点是从 AiApiNode 处理完流程，流转过来的节点。节点的流转是在 doApply 处理完成后，执行 router 路由方法。路由方法会调用当前实现类的 get 方法，获取下一个要执行节点。通过这样的方式分离逻辑区和流转区，可以让代码更好维护。
- 之后，到了 ChatModelNode 使用 Spring AI 处理模型构建。构建前还需要从上下文获取 AiApiNode 中关于 OpenAiApi 实例化对象，用于填充到 ChatModel 实例化中。
- 此外，ChatModelNode 还要构建关于 MCP 的构建，这里是把 MCP 填充到模型中使用，这一套都是基于 Spring AI 框架处理的。当然，除了可以使用 Spring AI 也可以使用 langchain4j、google adk 来处理关于 mcp 的部分。