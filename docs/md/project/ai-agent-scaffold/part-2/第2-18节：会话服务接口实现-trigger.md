---
title: 【更】第2-18节：会话服务接口实现-trigger
pay: https://t.zsxq.com/IY7j3
---

# 《AI Agent 脚手架》第2-18节：会话服务接口实现-trigger

作者：小傅哥
<br/>博客：[https://bugstack.cn](https://bugstack.cn)
<br/>视频：[https://t.zsxq.com/leFf4](https://t.zsxq.com/leFf4)

> 沉淀、分享、成长，让自己和他人都能有所收获！😄

## 一、本章诉求

对 domain 领域层的 service 服务，进行 trigger 包装，提供 http 接口能力。这样，后续就可以包装页面到调用接口，完整整个会话服务的操作。

## 二、流程设计

如图，会话接口服务所在分层；

<div align="center">
	<img src="https://bugstack.cn/images/article/project/ai-agent-scaffold/part-2/2-18/images/ai-agent-scaffold-2-18-01.png" width="850px"/>
</div>

- 如图，这一节主要是完成 trigger http 接口部分的能力处理，对外提供；`智能体列表`、`创建会话 session`、`发起会话（流式/非流式）`
- 注意，在实际业务开发中，接口的提供方式比较多的，也有可能提供 rpc 接口，还有可能对接口进行扩展，包装更多业务流程进去。那么这个时候，可以考虑增加 case 编排层（一个新的module模块），处理复杂流程业务。case 层的能力，主要就是分摊 trigger 层下的压力，让对外的接口层，更加轻量，只是做一些包装即可。
