---
title: 第2-2节：Api功能测试
pay: https://t.zsxq.com/uTPE2
---

# 《AI Agent 脚手架》第2-2节：Api功能测试

作者：小傅哥
<br/>博客：[https://bugstack.cn](https://bugstack.cn)
<br/>视频：[https://t.zsxq.com/q2Zug](https://t.zsxq.com/q2Zug)

> 沉淀、分享、成长，让自己和他人都能有所收获！😄

## 一、本章诉求

通过功能测试代码，使用 `Spring AI`、`LangChain4J`、`Google ADK` 框架对接 AI 服务，完成功能验证。为后续做 AI Agent 智能体脚手架做准备。

## 二、框架介绍

### 1. Spring AI

官网：[https://docs.spring.io/spring-ai/reference/1.0/index.html](https://docs.spring.io/spring-ai/reference/1.0/index.html)

Spring AI 项目旨在简化集成人工智能功能的应用程序的开发，避免不必要的复杂性。

该项目从 LangChain 和 LlamaIndex 等知名的 Python 项目中汲取灵感，但 Spring AI 并非这些项目的直接移植。该项目创立的初衷是，下一代生成式人工智能应用不仅面向 Python 开发者，还将广泛应用于多种编程语言。

> 在使用体验下 Spring AI 可以更好的结合 Spring 整个框架，整个接口的定义形式和使用方式，会更符合你对于 Spring 整体的使用习惯。

### 2. LangChain4J

官网：[https://docs.langchain4j.info/](https://docs.langchain4j.info/)

LangChain4j 的目标是简化将 LLM 集成到 Java 应用程序中的过程。

LangChain4j 始于 2023 年初 ChatGPT 热潮期间。 我们注意到与众多 Python 和 JavaScript LLM 库和框架相比，缺少 Java 对应物， 我们必须解决这个问题！ 虽然我们的名字中有"LangChain"，但该项目是 LangChain、Haystack、 LlamaIndex 和更广泛社区的想法和概念的融合，并加入了我们自己的创新。

### 3. Google ADK

官网：[https://google.github.io/adk-docs/get-started/java/#example](https://google.github.io/adk-docs/get-started/java/#example)

代理开发工具包 (ADK) 是一个灵活且模块化的框架，用于开发和部署 AI 代理 。ADK 针对 Gemini 和 Google 生态系统进行了优化，但它与模型和部署方式无关，并且是为……而构建的。 与其他框架的兼容性 。ADK 的设计宗旨是让代理开发更像软件开发，使开发人员能够更轻松地创建、部署和编排从简单任务到复杂工作流程的各种代理架构。

> 在使用体验上 Google ADK 自身是可以完整构建全部智能体的，但它又兼容了 Spring AI、LangChain4j 两个框架，让这2个框架负责 AI 对接，而 Google ADK 负责 Agent 的编排和插件的处理，这样使用起来非常不错。
