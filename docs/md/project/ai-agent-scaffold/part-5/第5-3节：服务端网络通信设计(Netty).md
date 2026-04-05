---
title: 【更】第5-3节：服务端网络通信设计(Netty)
pay: https://t.zsxq.com/IB8jJ
---

# 《AI Agent 场景应用 - MobileOpenClaw》第5-3节：服务端网络通信设计(Netty)

作者：小傅哥
<br/>博客：[https://bugstack.cn](https://bugstack.cn)
<br/>视频：[https://t.zsxq.com/UUvY7](https://t.zsxq.com/UUvY7)

> 沉淀、分享、成长，让自己和他人都能有所收获！😄

## 一、本章诉求

引入 Netty 框架，设计服务端 Socket Server 通信模型 + Future 等待响应方式获取客户端（手机）反馈结果。

这样设计的目的就是为了整个流程设计，从用户端发起请求，到后续章节AI分析决策产生指令，再通过 Socket 服务下发到手机端完成一些列的操作动作。

## 二、流程设计

如图，从服务端下发指令到客户端（手机）的流程设计；

<div align="center">
	<img src="https://bugstack.cn/images/article/project/ai-agent-scaffold/part-5/5-3/images/ai-agent-scaffold-5-3-01.png" width="450px"/>
</div>

- 首先，要为整个通信设计一个 Socket 通信模型，以便于服务端和客户端，保持信息数据交互。那么这里在领域层添加了一套 MobileClawService 的服务。
- 之后，整个通信服务的处理，是由基础设施层完成的，发送给手机端指令后，还需要一个等待，用于达到同步响应的效果。否则 socket 通信是异步的，再从其他入口返回来就不好处理了。

> 关于 Netty 这里有一些基础案例教程可以学习[《Netty 基础教程》](https://bugstack.cn/md/netty/base/2019-07-30-netty%E6%A1%88%E4%BE%8B%EF%BC%8Cnetty4.1%E5%9F%BA%E7%A1%80%E5%85%A5%E9%97%A8%E7%AF%87%E9%9B%B6%E3%80%8A%E5%88%9D%E5%85%A5JavaIO%E4%B9%8B%E9%97%A8BIO%E3%80%81NIO%E3%80%81AIO%E5%AE%9E%E6%88%98%E7%BB%83%E4%B9%A0%E3%80%8B.html)
