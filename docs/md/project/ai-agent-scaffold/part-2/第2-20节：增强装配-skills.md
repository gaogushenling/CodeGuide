---
title: 第2-20节：增强装配-skills
pay: https://t.zsxq.com/7uVom
---

# 《AI Agent 脚手架》第2-20节：增强装配-skills

作者：小傅哥
<br/>博客：[https://bugstack.cn](https://bugstack.cn)
<br/>视频：[https://t.zsxq.com/7uVom](https://t.zsxq.com/7uVom)

> 沉淀、分享、成长，让自己和他人都能有所收获！😄

## 一、本章诉求

为对话模型（ChatModelNode）的装配，添加 skills 技能配置，允许用户使用 resource 资源和映射的 path 路径的方式，在构建 AI Agent 智能体时，完成装配。

skill 是什么？它像是一本技能书📚，把一阳指（mcp/py/shell/js）和狮吼功（prompt）合成了一整招。缩短了从用户把提示词发给AI客户端，进行分析，决策，再到 mcp 执行的过程，让诉求直达结果，token 减少了，幻觉减少了！

随着 LLM 大模型能力的不断提升，并与 RAG、MCP、Skill 的结合，使得 Agent 智能体与完整的计算机环境（Computer/Phone）交互成为可能。这个过程中，一方面不断产生新的技术方案，一方面又不断的优化设计。就像 Skill 的出现，它不是替代 MCP，而是更准确的使用 MCP 能力。

## 二、技术介绍（skills 和 prompt + mcp）

如图，演示了一段 skill 的编写案例；

<div align="center">
	<img src="https://bugstack.cn/images/article/project/ai-agent-scaffold/part-2/2-20/images/ai-agent-scaffold-2-20-01.png" width="850px"/>
</div>

- 场景：案例中体现的是，对电脑性能检测后，用一段下达命令的方式，告知用户如何优化电脑性能。
- 重点：如果不使用 skill，则需要描述一大段话术，让 ai 自己完成对用户场景诉求的分析，并按照步骤来调用对应的各个 mcp 服务（没有 skill 则需要把各类内容，都包装为 mcp 服务）。这个过程是比较消耗 token 的，也可能有不小的幻觉。现在有了 skill，我们可以适当的完整的写一段诉求文档，文档里嵌入可执行的脚本/mcp服务，让执行更可靠。
- 用途：那都有哪些场景可以写 skill 技能书呢？🤔 如；互联网公司里的系统巡检，在接收到报警日志后，拿到一个报警的系统和接口信息，之后用 skill 技能书，分别采集出对应的系统配置、上线日志、数据库/缓存情况、运营操作记录、全链路监控上的接口耗时情况等。之后在根据我们日常排查问题的时候经验，编写过程步骤，这样会更加准确。

>所以，不是 skill、mcp 谁替代谁，而是 skill 对 mcp 进行增强，让 ai 执行时更加可靠。
