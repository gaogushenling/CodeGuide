---
title: 手机小龙虾，这次我比小米下手早！
lock: no
---

# 手机小龙虾，这次我比小米下手早！

作者：小傅哥
<br/>博客：[https://bugstack.cn](https://bugstack.cn)

> 沉淀、分享、成长，让自己和他人都能有所收获！😄

大家好，我是技术UP主小傅哥。

🦞 OpenClaw 太火了，火到什么程度，给 Mac Mini 干断货了，各行各业都找程序员👨🏻‍💻安装小龙虾，上门部署 OpenClaw 也成了生意！3月6日，深圳腾讯大厦，公益装机，也排起了长长的队伍。很多父母带着电脑过来，给自己娃的电脑装上小龙虾。

<div align="center">
	<img src="https://bugstack.cn/images/article/project/ai-agent-scaffold/part-0/images/ai-agent-scaffold-mobileopenclaw-260307-02.png" width="450px"/>
</div>

但当所有人都盯着 OpenClaw 小龙虾时，小米发布了 miclaw 手机版龙虾🦞，对标豆包手机、AutoGLM-Phone，首批支持小米17系列机型。

但，嘿嘿，不谋而合。我在看到和体验 OpenClaw 后，也想着，我的手机、平板，也可以来一个 Mobile-OpenClaw 呀！让这些电子设备，帮我完成一些工作不是美滋滋！`下文我会演示通过小龙虾手机的案例视频。`

<div align="center">
	<img src="https://bugstack.cn/images/article/project/ai-agent-scaffold/part-0/images/ai-agent-scaffold-mobileopenclaw-260307-01.png" width="850px"/>
</div>

所以，在小米 miclaw 发布之前，我也已经开始设计实现手机版龙虾。并且还申请了一个手机版龙虾的域名，哈哈哈 死鬼，早有预谋哇！

<div align="center">
	<img src="https://bugstack.cn/images/article/project/ai-agent-scaffold/part-0/images/ai-agent-scaffold-mobileopenclaw-260307-03.png" width="550px"/>
</div>

那手机版龙虾怎么做？🤔 它可以，通过 AI Agent 智能体，分析用户行为。之后下达一些列指令到应用设备的 Socket 网关端点上，完成功能指令动作。`小米 miclaw` 应该也是类似的，以后也可以体验下，但他可以原生态直接从系统上支持，控制整个米家的应用生态 👍🏻。

闲言少叙，接下来我们演示下运行效果。我的小米 Pad 7 Pro 也到位了。新的设备测试起来速度更快。😂 最近是一顿花钱呀，Mac Mini（电脑龙虾）、Pad 7 Pro（手机龙虾）、群辉 Nas（数据存储 + qwen3.5:9b）！**这个世界，终究是程序员的！**

## 一、演示场景

小傅哥这里做了2个演示场景，一个是在小红书🍠发帖，一个是汽水音乐🎵自动看广告开会员。

### 1. 小红书 - 自动发帖

```java
打开小红书，点击下面的红色按钮，发送一个帖子。先写想法为，你好，世界，我是手机版小龙虾 🦞 想法编写后，点击【下一步】继续。在发帖页面，输入标题为；你好，世界，我是手机版小龙虾 🦞 内容为；我是 @小傅哥 正在测试开发的 MobileOpenClaw 欢迎关注我的动向！编写后，点击右上角【发布】。
```

--

### 2. 汽水音乐 - 看广告

```java
打开汽水音乐，看广告获得VIP时长，操作流程；

1. 点击右上角【免】按钮。
2. 点击【免】后会进入后，右上角有倒计时播放广告，播放完成后显示为【领取成功】。这个时候点击【领取成功】，会有一个弹窗，点击弹窗的【领取奖励】，不要点x关闭。
3. 完成领取后，继续看广告，重复步骤2，一直领取奖励，直至没有。
```

--

## 二、项目学习

### 1. 学习路线

小傅哥的社群星球「码农会锁」，现已经有20个实战项目，6个AI、5个业务、8个组件 + 1套源码（MyBatis），这6个AI项目，你可以按需选择学习。

<div align="center">
	<img src="https://bugstack.cn/images/article/project/ai-agent-scaffold/part-1/1-1/images/ai-agent-scaffold-1-1-10.png" width="650px"/>
</div>

### 2. 龙虾手机 - 实战项目

首先，这是一整套从0到1，文档 + 视频 + 源码，包含前后端 + DevOps 的综合实战项目。带着大家进行需求分析、底座构建、脚手架设计、应用场景实践（draw.io 画图 + 手机龙虾）。所以，你可以非常完整的学习到关于 AI Agent 智能体的全部内容，让你具备企业级项目开发能力。

<div align="center">
	<img src="https://bugstack.cn/images/article/project/ai-agent-scaffold/part-1/1-1/images/ai-agent-scaffold-1-1-02.png" width="650px"/>
</div>

#### 介绍

[AI Agent 脚手架 + 场景应用](#) - 综合 Spring AI、LangChain4j + Google ADK（a2a、mcp、skills），打造全新智能体架构方案。

[面试：技能、简历、问题汇总](#)

#### 第1部分：需求与架构

- [第1-1节：脚手架需求分析](#)
- [第1-2节：系统架构设计](#)

#### 第2部分：基础底座开发

- [第2-1节：工程初始化创建](#)
- [第2-2节：Api功能测试](#)
- [第2-3节：智能体配置表设计](#)
- [第2-4节：装配域结构化定义](#)
- [第2-5节：装配域节点-AiApiNode](#)
- [第2-6节：装配域节点-ChatModelNode](#)
- [第2-7节：装配域节点-AgentNode](#)
- [第2-8节：装配域节点-AgentWorkflowNode](#)
- [第2-9节：装配域节点-Loop、Parallel、Sequential](#)
- [第2-10节：装配域节点-RunnerNode](#)
- [第2-11节：智能体加载使用验证](#)
- [第2-12节：增强装配-RunnerNode](#)
- [第2-13节：增强装配-AgentWorkflowNode](#)
- [第2-14节：增强装配-本地mcp](#)
- [第2-15节：增强装配-回调plugin](#)
- [第2-16节：fix-多模态能力使用](#)
- [第2-17节：会话服务接口实现-service](#)
- [第2-18节：会话服务接口实现-trigger](#)
- [第2-19节：会话服务接口对接-ui](#)
- [第2-20节：增强装配-skills](#)

#### 第3部分：脚手架工程化

- [第3-1节：Maven脚手架配置](#)
- [第3-2节：上传jar到maven仓库](#)
- [第3-3节：部署脚手架网页](#)

#### 第4部分：业务场景（ai+draw.io） - `这部分内容非常有实用价值！`

- [第4-0节：ai + draw.io 产品设计](#)
- [第4-1节：初始化工程搭建](#)
- [第4-2节：在页面嵌入draw.io组件和对话框](#)
- [第4-3节：智能体API接口对接](#)
- [第4-4节：AI+用户+DrawIO，交互式画图](#)
- [第4-5节：ai-draw-io，云服务器部署](#)

#### 第5部分：业务场景（MobileOpenClaw）- `这部分内容非常有意思！`

- [第5-0节：MobileOpenClaw 产品设计](#)
- [第5-1节：初始化工程搭建](#)
- [第5-2节：手机网关能力设计](#)
- [第5-3节：通过 Netty 进行同步等待通信](#)
- [第5-4节：智能体初步配置使用](#)
- [第5-5节：智能体工作流设计](#)
- [第5-6节：异步结果响应](#)
- [第5-7节：图片位点识别增强](#)
- [第5-8节：多版本安卓版本策略支持](#)
- [第5-9节：会话上下文细化处理](#)

>星球里另外一套 AI Agent 还对接了 ELK、普罗米修斯、微信公众号等，也可以把 MCP 对接过来进行系统巡检。有了这套脚手架的学习，你可以完成非常多的场景对接使用。

