---
title: Spec-DD
lock: need
---

# Spec 规约编程，可视化 Skills 技能。几十万代码的工程，也能让 AI 清楚的把控迭代！

作者：小傅哥
<br/>博客：[https://bugstack.cn](https://bugstack.cn)

> 沉淀、分享、成长，让自己和他人都能有所收获！😄

大家好，我是技术UP主小傅哥。

**其实很多伙伴都是小卡拉米**！整一份源码不知道从哪看，接一个需求不知道怎么干。啥也不懂就让 AI 干，AI 干完不 Review 还不敢上线。咋整！是不焦虑，是不着急。—— `来吧，我给你一份大厂的解决方案吧！`

<div align="center">      
	<img src="https://bugstack.cn/images/article/project/ai-rag-knowledge/ai-rag-knowledge-0-00.png" width="150px"/>      
</div>

**用一个技能，给你份全览地图。**

`读源码`、`做项目`、`改bug`，当你面对一份全新工程，甚至是有历史沉淀下来**几十万行**的代码工程，那你大概率不知道从哪下手。无论是老鸟还是小白，这个过程都是非常困难的。

当然，现在有 AI 可以一个 prompt 描述过去，就吭哧吭哧给你干了。但 AI 干的这东西，因为没有过你的脑子，所以你压根也不知道 AI 干的对不对。本来阅读一份新的工程源码都费劲，在阅读 AI 改的代码就更吃力了。

所以，这份技能给你的是一份全览图。👍🏻

用 AI Agent + Skills 技能，为你要`读的源码`、`改的需求`，提供一份；左侧是工程结构（类似 IntelliJ IDEA）和代码文件以及方法，中间是流程图 + 时序图，右侧是改动/介绍说明。

从左到右，你可以点击**方法**，**流程**，**指引**，这个时候会有一条连线串联，告诉它们之间的关系。此外还会有一份引导，可以带着你一步步点击，告诉你本次流程涉及全部链路，从哪开始到哪结束。**这对学习源码和修改需求，就不烧心啦！** 如图；

<div align="center">      
	<img src="https://bugstack.cn/images/article/ai/xfg-coding-map-skills-01.png" width="950px"/>      
</div>

**死鬼，你看吧，这多清楚。**

改了啥，动了啥，要看啥，都一步步的给你列出来。中间有全景图、时序图、流程图，一步步的带着你走。无论你是想学源码，还是想加功能，都能清晰可见的知道他们在哪，在干啥。

> 💐 好啦，接下来小傅哥就给大家介绍下这个技能是怎么用的，效果咋样，看完你也能一句话给自己生成一张代码地图。走起！

## 一、技能安装

- Github：[https://github.com/fuzhengwei/xfg-coding-map-skills](https://github.com/fuzhengwei/xfg-coding-map-skills)
- Gitcode：[https://gitcode.com/fuzhengwei/xfg-coding-map-skills](https://gitcode.com/fuzhengwei/xfg-coding-map-skills)

安装这个技能非常简单，把下面这句话复制给你的 AI（`WorkBuddy`/`Claude Code`/`Codex`/`WaLiCode` 等支持 Skills 的智能体）就能自动完成安装；

```text
请帮我安装"代码地图生成技能"，从代码仓库 https://gitcode.com/fuzhengwei/xfg-coding-map-skills 拉取技能文件，并安装到用户级技能目录，安装完成后告诉我怎么使用。
```

<div align="center">      
	<img src="https://bugstack.cn/images/article/ai/xfg-coding-map-skills-02.png" width="950px"/>      
</div>

💡 备选安装，你可以把 Skills 下载到本地解压。在 AI Agent 工具里，选择安装。也可以把本地地址告诉 AI 工具进行安装。

## 二、使用技能

安装完成后，你就可以对着 AI 说一句；`帮我为 xxx 项目生成一份代码地图`，例如；

- 帮我为 deepseek-harness-java 项目的插件机制生成一份代码地图。
- 我需要在 deepseek-harness-java 增加应用连接器能力，通过连接器对接QQ邮箱📮，帮我设计出实现方案。并同一份代码地图。
- 我遇到一个线下bug，在用户使用 deepseek-harness-java web 服务的时候，遇到审批后卡主，不执行工具的问题，帮我分析原因，并给出一份代码地图，指导修复。

>AI 就会自动分析工程结构、梳理核心链路，给你生成一份可交互的三栏全景图 HTML，用浏览器打开即可开逛。🧭

#### 1. 分析流程

<div align="center">      
	<img src="https://bugstack.cn/images/article/ai/xfg-coding-map-skills-03.png" width="950px"/>      
</div>

- 工具：Workbuddy
- 话术：`/xfg-coding-map-skills 帮我为 deepseek-harness-java 项目的插件机制生成一份代码地图。`
- 产出：dsh java 插件功能全览图，点击到一个模块、类、方法下，就能联动时序图/流程图，来看具体的代码实现。

#### 2. 修复异常

<div align="center">      
	<img src="https://bugstack.cn/images/article/ai/xfg-coding-map-skills-04.png" width="950px"/>      
</div>

- 工具：[WaLiCode](https://walicode.xiaofuge.cn/)
- 话术：ai-mcp-gateway 找出 这个项目的一个bug，之后用 [Skill: xfg-coding-map-skills] 技能给出全览图，可以直观看到bug在哪，怎么处理。
- 产出：这类场景非常适合分析线上故障，通过日志排查后，直接给你把对应的工程里的代码定位到，再给你渲染出来。这定位可就轻松多了。哪怕你是个刚接手这个项目的小白，也能快速知道到底是哪里的问题。

#### 3. 需求迭代

<div align="center">      
	<img src="https://bugstack.cn/images/article/ai/xfg-coding-map-skills-05.png" width="950px"/>      
</div>

- 工具：[WaLiCode](https://walicode.xiaofuge.cn/)
- 话术：ai-mcp-gateway 要增加分布式能力，设计分析后 [Skill: xfg-coding-map-skills] 通过技能，给出新需求开发全览图。
- 产出：新的需求开发，可以基于开发导航，一步步的知道你要做什么功能逻辑。这比你在几十万行的代码工程里，自己去翻看代码要容易的多。而且 AI 按照这套设计进行编码，更加可靠。

> 😄 嘿，不错吧。这样可靠的可视化全景图，可以非常好的帮助你约束（S）代码分析、迭代、排查问题。用起来吧！

## 三、其他技能

一路伴随着 AI 走来，小傅哥还做了很多好玩的小技能，用于场景提效。接下来在给大家分享几个。

> 安装方式和代码地图一样，把下面这段话里的**仓库地址和技能名替换一下**，复制给你的 AI（`WorkBuddy`/`Claude Code`/`Codex`/`WaLiCode` 等支持 Skills 的智能体）就能自动完成安装。

#### 1. DDD 规约编程（xfg-ddd-skills）

**这是啥：** 一套 DDD 六边形架构的规约编程技能。内含触发器层、应用层、领域层、基础设施层的**设计模式、代码模板、命名规范**，还有一套脚手架脚本和 Docker 部署脚本。有了它，AI 写出来的代码就不再是"能跑就行"的单体大泥球，而是结构统一、边界清晰的大厂规约工程。哪怕你对 DDD 不熟，AI 也会按照这套规约帮你把工程搭得明明白白。

```text
请帮我安装"DDD 规约编程技能"，从代码仓库 https://gitcode.com/fuzhengwei/xfg-ddd-skills 拉取技能文件，并安装到用户级技能目录，安装完成后告诉我怎么使用。
```

**怎么用：** 安装后直接和 AI 说需求即可，例如；`用 DDD 六边形架构帮我设计一个营销试算服务，出一份工程结构`、`给这个项目补充 Docker 部署脚本`。AI 会按四层规约输出设计和代码。

<div align="center">      
	<img src="https://bugstack.cn/images/article/ai/xfg-coding-map-skills-06.png" width="950px"/>      
</div>
> 地址：https://gitcode.com/fuzhengwei/xfg-ddd-skills

#### 2. B站/小红书视频封面（xfg-skills-video-cover）

**这是啥：** 这玩意可大，这是一套视频封面生成器，尤其是不知道要做啥封面的时候，整就行。输入课程标题或一份 PPT，自动生成大字体突出、俏皮、抓眼球的爆款封面。内置 **437 种风格方案 × 231 套配色**，4 大分类（科技知识/生活娱乐/视觉冲击/文艺清新），支持 B站、小红书、微信视频号、手机竖版 4 种尺寸一键出图，还有爆款标题生成器帮你起标题。

```text
请帮我安装"视频封面生成技能"，从代码仓库 https://gitcode.com/fuzhengwei/xfg-skills-video-cover 拉取技能文件，并安装到用户级技能目录，安装完成后告诉我怎么使用。
```

**怎么用：** 安装后说一句 `给这期视频做个B站封面，主题是 xxx`，AI 会先帮你优化标题，再生成一张 437 种风格的选择墙（每张卡片都是真实渲染效果），你挑一个喜欢的风格，4 种平台尺寸的封面就全出来了。

<div align="center">      
	<img src="https://bugstack.cn/images/article/ai/xfg-coding-map-skills-07.png" width="950px"/>      
</div>
> 地址：https://gitcode.com/fuzhengwei/xfg-skills-video-cover

#### 3. HTML PPT 效果

**这是啥：** HTML PPT 生成技能。把你的课程大纲、分享内容做成一套**深蓝+金色科技风**的网页幻灯片：总封面、课程大纲、章节封面、内容页（卡片/架构图/代码高亮）、总结页，支持键盘/点击/缩略图三种翻页方式。单文件交付，双击就能打开，特别适合录课、技术分享，章节封面裁下来还能直接当视频封面用。

```text
请帮我安装"HTML PPT 生成技能"，从代码仓库 https://gitcode.com/fuzhengwei/xfg-skills-html2ppt 拉取技能文件，并安装到用户级技能目录，安装完成后告诉我怎么使用。
```

**怎么用：** 安装后说一句 `帮我做一个HTML PPT，主题是《Spring Boot 入门实战》，分3节：环境搭建/REST API/数据持久化，讲师小傅哥`，AI 就会自动规划页面结构，生成一套可翻页的幻灯片。

<div align="center">      
	<img src="https://bugstack.cn/images/article/ai/xfg-coding-map-skills-08.png" width="950px"/>      
</div>
> 地址：https://gitcode.com/fuzhengwei/xfg-skills-html2ppt）
