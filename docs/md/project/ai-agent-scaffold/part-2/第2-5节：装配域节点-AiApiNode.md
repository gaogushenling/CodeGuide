---
title: 【更】第2-5节：装配域节点-AiApiNode
pay: https://t.zsxq.com/wetnI
---

# 《AI Agent 脚手架》第2-5节：装配域节点-AiApiNode

作者：小傅哥
<br/>博客：[https://bugstack.cn](https://bugstack.cn)
<br/>视频：[https://t.zsxq.com/D3LGP](https://t.zsxq.com/D3LGP)

> 沉淀、分享、成长，让自己和他人都能有所收获！😄

## 一、本章诉求

从本节装配 AI Agent 智能体各个节点开始，每一节都只负责一小部分独立内容的实现，方便大家可以在回顾的时候，直接找到对应章节进行查看。

这一节装配第一个节点 AiApiNode，它的目的是和 AI 接口，建立请求连接。

## 二、流程设计

如图，智能体装配中 AiApiNode 部分；

<div align="center">
	<img src="https://bugstack.cn/images/article/project/ai-agent-scaffold/part-2/2-5/images/ai-agent-scaffold-2-5-01.png" width="700px"/>
</div>

AiApiNode 节点的装配，使用的是 Spring AI 框架提供的构建方法。在咱们课程前面也讲解过 LangChain4j，后面如果你想锻炼，也可以更换下，完全都是可以到 Agent 装配的时候做兼容的。