---
title: 【更】第3-2节：上传jar到maven仓库
pay: https://t.zsxq.com/GHNso
---

# 《AI Agent 脚手架》第3-2节：上传jar到maven仓库

作者：小傅哥
<br/>博客：[https://bugstack.cn](https://bugstack.cn)
<br/>视频：[https://t.zsxq.com/6xBLn](https://t.zsxq.com/6xBLn)

> 沉淀、分享、成长，让自己和他人都能有所收获！😄

## 一、本章诉求

发布脚手架工程 Jar 包到阿里云 Maven 私有制品库。

在公司里，这块的目的在于，我们设计一款通用的脚手架，让公司里的伙伴都可以使用。那么公司里会把这样的脚手架jar，推送到公司内的私服仓库，之后公司内的用户配置了私服 Maven 地址，就可以使用了。

注意，可以检索下 Maven 私服搭建，面试也可能会问，企业里应该怎么做。

## 二、流程设计

如图，把 jar 发布到 maven 私服仓库；

<div align="center">
	<img src="https://bugstack.cn/images/article/project/ai-agent-scaffold/part-3/3-2/images/ai-agent-scaffold-3-2-01.png" width="650px"/>
</div>

- 在整个大流程中，我们要上传jar到maven私服仓库，这部分阿里云有提供，可以申请使用。另外，可以尝试检索下 Maven 私服搭建和使用。
- 这一部分会使用到 IntelliJ IDEA Maven Deploy + Maven Settings.xml 配置阿里云私服。
