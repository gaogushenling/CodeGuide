---
title: 【更】第4-2节：在页面嵌入draw.io组件和对话框
pay: https://t.zsxq.com/JoT4f
---

# 《AI Agent 场景应用 - ai draw.io》第4-2节：在页面嵌入draw.io组件和对话框

作者：小傅哥
<br/>博客：[https://bugstack.cn](https://bugstack.cn)
<br/>视频：[https://t.zsxq.com/wtWx6](https://t.zsxq.com/wtWx6)

> 沉淀、分享、成长，让自己和他人都能有所收获！😄

## 一、本章诉求

在 React 前端工程中，嵌入 draw.io 组件。以及在整个页面的右侧放入一个对话框，用于后续与服务端的 ai 接口进行对话。

这部分的实现，会使用到 ai ide 工具来处理，你常用的任何一款工具都可以。

## 二、流程设计

如图，前端页面交互的流程设计；

<div align="center">
	<img src="https://bugstack.cn/images/article/project/ai-agent-scaffold/part-4/4-2/images/ai-agent-scaffold-4-2-01.png" width="550px"/>
</div>

- 这是一个简单的交互，引入 react-drawio 到初始页面，并在右侧设置一个对话框。
