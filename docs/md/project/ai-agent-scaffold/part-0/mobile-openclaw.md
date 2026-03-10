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



