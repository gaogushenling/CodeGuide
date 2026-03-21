---
title: 【更】第2-17节：会话服务接口实现-service
pay: https://t.zsxq.com/lxqLY
---

# 《AI Agent 脚手架》第2-17节：会话服务接口实现-service

作者：小傅哥
<br/>博客：[https://bugstack.cn](https://bugstack.cn)
<br/>视频：[https://t.zsxq.com/vLd8O](https://t.zsxq.com/vLd8O)

> 沉淀、分享、成长，让自己和他人都能有所收获！😄

## 一、本章诉求

在智能体完成装配以后，接下来我们要做的就是提供标准的会话服务接口能力，使用智能体。这包括了，所装配智能体的列表（agentId）、会话的创建、消息的处理（同步/异步）。

## 二、流程设计

如图，会话接口服务所在分层；

<div align="center">
	<img src="https://bugstack.cn/images/article/project/ai-agent-scaffold/part-2/2-17/images/ai-agent-scaffold-2-17-01.png" width="850px"/>
</div>

- 首先，在 Agent 装配后，是要对外提供服务，服务由 trigger 分层下的 http 接口提供。这个 trigger 也就是 mvc 分层里的 controller，但因为在微服务下，接口、消息、定时任务，都是一种触发行为。触发可以理解为，别人打你，可以用拳头，可以用石头，还分可以榔头，这些都可以抽象为一种名称，触发。所以在 ddd 分层下，增加了 trigger 触发器层。
- 之后，这一节我们先来实现 service 服务层，也就是在 domain 领域下，agent 里除了做装配实现，还要做一层会话处理。在 service 实现后，后面就是包装 trigger 层的对外接口。
