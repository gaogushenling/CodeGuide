---
title: 【更】第4-3节：智能体API接口对接
pay: https://t.zsxq.com/hrQVL
---

# 《AI Agent 场景应用 - ai draw.io》第4-3节：智能体API接口对接

作者：小傅哥
<br/>博客：[https://bugstack.cn](https://bugstack.cn)
<br/>视频：[https://t.zsxq.com/RnvaG](https://t.zsxq.com/RnvaG)

> 沉淀、分享、成长，让自己和他人都能有所收获！😄

## 一、本章诉求

通过脚手架创建 AI Agent 智能体服务端工程，并配置用于绘制 draw.io 流程图的专属提示词。之后在前端工程对接智能体 API 服务接口，包括；创建会话 SessionID、调用对话接口进行绘图（这部分会限制智能体以 drawio 格式返回结果）。

## 二、流程设计

如图，前端页面与服务端交互的UML流程设计；

<div align="center">
	<img src="https://bugstack.cn/images/article/project/ai-agent-scaffold/part-4/4-3/images/ai-agent-scaffold-4-3-01.png" width="750px"/>
</div>

- 首先，从用户发起，打开页面开始，则从服务端的智能体列表加载接口，返回智能体列表。
- 之后，选择智能体进行对话，这个过程要先创建会话ID。也就是所有的本次的交互，会有一个会话ID进行，这样在对话的过程中会记录上下文，输出的结果也会更加准确。
- 最后，服务端返回智能体结果，是以 draw.io xml 的方式的方式返回的，之后渲染到 draw.io 面板上。
