---
title: 【更】第4-0节：ai + draw.io 产品设计
pay: https://t.zsxq.com/AAwjy
---

# 《AI Agent 场景应用 - ai draw.io》第4-0节：ai + draw.io 产品设计

作者：小傅哥
<br/>博客：[https://bugstack.cn](https://bugstack.cn)
<br/>视频：[https://t.zsxq.com/035hj](https://t.zsxq.com/035hj)

> 沉淀、分享、成长，让自己和他人都能有所收获！😄

## 一、本章诉求

基于 AI Agent 智能体脚手架，在 draw.io 场景，使用 react 开发一套 ai + draw.io 智能绘图功能场景。

当前章节的这套场景功能会比较轻量，不会结合toc用户诉求。但当你越来越多的熟练星球的各个项目以后，你可以在 ai + draw.io 的功能上，添加公众号扫码登录、微信支付购买使用额度 + 拼团购买、数据库记录个人绘图信息、分享绘图数据在统一平台、其他用户可以查看和收藏，以及使用后有抽奖、积分、兑换营销能力等。这些功能在星球的其他项目都有体现，可以陆续学习后扩展补充。

## 二、产品效果

如图，ai + draw.io 使用 ai agent 脚手架，所能实现的效果；

<div align="center">
	<img src="https://bugstack.cn/images/article/project/ai-agent-scaffold/part-4/4-0/images/ai-agent-scaffold-4-0-01.png" width="950px"/>
</div>

- 首先，需要结合 [react-drawio](https://github.com/marcveens/react-drawio) 插件，把 draw.io 嵌入到 react 程序里。在 react-drawio 的插件里，提供了相关的 API 操作，这可以让我们把 ai 生成的 xml 文件，让 draw.io 渲染出来。也可以读取到 draw.io 上的内容，再发给 ai 进行分析和调整。
- 之后，是 ai agent 脚手架开发的程序，编写智能体提示词，让其可以以 xml 的格式返回。当然这部分也可以做一些限定，比如返回的数据是一个带有类型和内容的对象，如果类型 type 是对话，那么可以进行多次交流，如果返回类型是 xml，那么则直接渲染。目前的案例程序，会先直接返回 xml 直接渲染进来。
- 最后，我们做这类内容，我们先有一个简单的清晰的流程和实现方案，能把整个流程串联起来。当你做的透彻以后，就可以继续扩展迭代功能了。
