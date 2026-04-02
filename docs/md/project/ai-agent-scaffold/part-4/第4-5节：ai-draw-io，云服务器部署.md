---
title: 【更】第4-5节：ai-draw-io，云服务器部署
pay: https://t.zsxq.com/5h1K1
---

# 《AI Agent 场景应用 - ai draw.io》第4-5节：ai-draw-io，云服务器部署

作者：小傅哥
<br/>博客：[https://bugstack.cn](https://bugstack.cn)
<br/>视频：[https://t.zsxq.com/UaVxl](https://t.zsxq.com/UaVxl)

> 沉淀、分享、成长，让自己和他人都能有所收获！😄

## 一、本章诉求

在云服务器（2c4g）部署 ai-draw-io 前后端项目，后端提供智能体能力，前端提供绘图操作。本次构建的镜像，小傅哥提供了动态更换前端访问服务的IP配置，在不进行构建镜像时，也可以直接使用。

>注意，ai-draw-io 绘图操作，模型配置的越好，效果也越好。gpt-5.1 比 gpt-4.1 绘制的效果更好。

## 二、部署过程

如图，部署过程步骤流程；

<div align="center">
	<img src="https://bugstack.cn/images/article/project/ai-agent-scaffold/part-4/4-5/images/ai-agent-scaffold-4-5-01.png" width="850px"/>
</div>

- 首先，你需要一台2c4g云服务器（安装 Ubuntu 24），推荐购买 [https://618.gaga.plus](https://618.gaga.plus) - 腾讯云暂时有买1年送3个月，可以配和 [https://bugstack.cn/md/road-map/ssl-httpsok.html](https://bugstack.cn/md/road-map/ssl-httpsok.html) 申请免费 ssl（自动续期）适合后续有域名的时候使用。
- 之后，在你购买了一台云服务器后，你可以使用小傅哥提供的一键安装脚本，把云服务器部署好 Docker 环境 + Portainer 管理面板。安装脚本：[https://gitcode.com/Yao__Shun__Yu/xfg-dev-tech-docker-install](https://gitcode.com/Yao__Shun__Yu/xfg-dev-tech-docker-install)
- 然后，这里还有项目的部署教程，这里是小傅哥录制好的视频，教你如何部署项目。教程：[https://t.zsxq.com/iDuCt](https://t.zsxq.com/iDuCt) - `你可以做为补充学习，本课程也会带着你部署项目。`
- 另外，这里还有一个本地对项目构建好镜像后推送到阿里云docker镜像库，方便大家上传和拉取。其实也可以推送到官网 docker hub，但会需要代理。教程（阿里云docker镜像使用）：[https://t.zsxq.com/XdoWr](https://t.zsxq.com/XdoWr) 阿里云镜像库地址：[https://cr.console.aliyun.com/cn-hangzhou/instance/credentials](https://cr.console.aliyun.com/cn-hangzhou/instance/credentials)
- 注意，提前在云服务器安全组开放端口；`9000-docker 管理面板`、`8091-后端接口`、`3000-前端页面`

> 综上，所有的云服务器操作，在星球「码农会锁」都提供好了学习教程，可以参考总地址：[https://t.zsxq.com/19osWS4qj](https://t.zsxq.com/19osWS4qj)
