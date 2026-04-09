---
title: 【更】第5-7节：使用AutoGLM-Phone-9B构建手机智能体
pay: https://t.zsxq.com/6qOqE
---

# 《AI Agent 场景应用 - MobileOpenClaw》第5-7节：使用AutoGLM-Phone-9B构建手机智能体

作者：小傅哥
<br/>博客：[https://bugstack.cn](https://bugstack.cn)
<br/>视频：[https://t.zsxq.com/06kx8](https://t.zsxq.com/06kx8)

> 沉淀、分享、成长，让自己和他人都能有所收获！😄

## 一、本章诉求

引入智谱发布的 autoglm-phone-9b 专属模型，构建手机智能体。专属模型对手机上的内容操作有更为全面流程控制，比通用视觉模型在处理用户动作时会更加准确。目前这套模型可以使用官网（限时免费 [autoglm-phone](https://docs.bigmodel.cn/cn/guide/models/vlm/autoglm-phone)），也可以在 24G * 2 显卡[自己部署](https://bugstack.cn/md/algorithm/model/autoglm-phone-agent.html)。所以，如果你考虑的是将来在一些场景使用，成本相对也是很低的。

## 二、流程设计

如图，通过 autoglm-phone-9b 专属模型，构建手机智能体设计；

<div align="center">
	<img src="https://bugstack.cn/images/article/project/ai-agent-scaffold/part-5/5-7/images/ai-agent-scaffold-5-7-01.png" width="850px"/>
</div>

- 首先，我们把之前的通用模型的实现，定义为 flow 我们要自己编写流程。把专属的手机模型定义为 auto，因为他提供了默认的一些专属特性，可以减少我们流程化上的操作。
- 之后，对照来看，autoglm-phone-9b 模型，会为我们返回具体的手机的操作指令，如点击、打开、滑动、双击、回到主屏幕等。这部分内容在智谱官网访问也有说明 [AutoGLM-Phone](https://docs.bigmodel.cn/cn/guide/models/vlm/autoglm-phone)
- 那么，现在需要我们改动的内容，主要是围绕着特定官网的给的智能体 prompt 提示词，编写智能体处理过程，与网关通信完成一些列的流程操作。
