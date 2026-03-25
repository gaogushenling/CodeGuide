---
title: 第3-1节：Maven脚手架配置
pay: https://t.zsxq.com/jnqmk
---

# 《AI Agent 脚手架》第3-1节：Maven脚手架配置

作者：小傅哥
<br/>博客：[https://bugstack.cn](https://bugstack.cn)
<br/>视频：[https://t.zsxq.com/EwCTb](https://t.zsxq.com/EwCTb)

> 沉淀、分享、成长，让自己和他人都能有所收获！😄

## 一、本章诉求

对 ai-agent-scaffold 脚手架工程配置 maven-archetype-plugin，生成工程脚手架。以及通过命令使用脚手架（jar）创建出新的工程。

脚手架的目的就在于此，我们使用一套通用的代码，按照不同的工程使用新的工程名、包名、版本，来构建一套具有相同基础能力的新的项目。

简单来说，maven-archetype-plugin 是 Maven 世界里的“项目模板生成器”。

如果把开发一个项目比作盖房子，这个插件的作用就是为你提供一套图纸和预制框架。你不需要每次都从零开始挖地基、垒砖头，只需要选好模板，它就会自动帮你把标准的目录结构和基础配置（pom.xml）搭建好。

## 二、流程设计

如图，从工程使用 maven 构建脚手架到使用的过程；

<div align="center">
	<img src="https://bugstack.cn/images/article/project/ai-agent-scaffold/part-3/3-1/images/ai-agent-scaffold-3-1-01.png" width="950px"/>
</div>

- 左侧，对现有工程使用 maven-archetype-plugin 插件，构建工程脚手架。将当前的工程打包成一个可复用的 Archetype 模板。
- 中间，打包好的脚手架，可以在本地直接使用，也可以发布jar到私服，让大家都可以使用。私服部分，后续在做处理。
- 右侧，使用方可以基于命令，或者 IntelliJ IDEA 配置 Maven 脚手架的方式，创建和启动工程。这一节，我们先通过命令的方式使用。
