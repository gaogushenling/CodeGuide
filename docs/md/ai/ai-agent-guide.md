---
title: AI Agent 八股文小册
lock: need
---

# AI Agent 八股文

作者：小傅哥
<br/>博客：[https://bugstack.cn](https://bugstack.cn)

>沉淀、分享、成长，让自己和他人都能有所收获！😄

大家好，我是技术UP主小傅哥。

`Agent 架构与传统 LLM 链式调用有什么区别？` `什么是 ReAct 模式，底层工作原理是什么？` `多轮 Agent 对话怎么解决上下文溢出？` `Agent 工具调用的工具类型都有哪些，在长对话中，怎么保证 Agent 的工具调用的可靠性。` 哈，**死鬼**，想转 Agent 应用开发工程师吗，这些问题你准备好了吗，有过项目实践吗？

<div align="center">
	<img src="https://bugstack.cn/images/article/project/walicode/walicode-introduce-01.gif" width="150px"/>
</div>

在此之前，小傅哥，从22年尾就一直跟进 AI 方向，先后做；AI 问答助手、OpenAI 大模型应用、OpenAI 代码自动评审、AI MCP Gateway，基础的做完就开始搞 AI Agent 智能体系列（拖拉拽、脚手架），AI + Draw.io、AI + Moblie，紧接着推出重型项目 `WaLiSSH`、`WaLiCode` 全面推进！

<div align="center">
	<img src="https://bugstack.cn/images/article/project/ai-agent-scaffold/part-1/1-1/images/ai-agent-scaffold-1-1-10.png" width="650px"/>
</div>

**可以这么讲，跟着小傅哥，哪有掉队的可能。** 你还得走到头部呢，而且有这么多 AI Agent 应该应用开发岗位，简直就是这个时代的机会！

<div align="center">
	<img src="https://bugstack.cn/images/article/project/walicode/walicode-introduce-02.png" width="450px"/>
</div>

是个机会，但这个东西吧！整体来讲呢，`AI Agent 应用开发`不算难。不过很多伙伴，并不是一开始就跟着 AI 的，而是 AI 知识都爆发成这样了，才后知后觉。所以，一下子懵😳了，不知道从哪开始学了。

`不过，别着急。小傅哥，再拉你一把！`

[《AI Agent Guide》](https://ai-agent-guide.xiaofuge.cn/) 来啦，从基础认知到面试通关 · 21章渐进式可视化教程。官网：[https://ai-agent-guide.xiaofuge.cn/](https://ai-agent-guide.xiaofuge.cn/)

这是小傅哥基于现在开发的 AI Agent 项目（[WaLiCode](https://walicode.xiaofuge.cn/)），提炼出来的一套智能体入门和面试教程。还附带着免费的 AI 对话，辅助学习。

<div align="center">
	<img src="https://bugstack.cn/images/article/ai/ai-agent-guide-01.png" width="950px"/>
</div>

这是一套**从零到面试通关**的 AI Agent Guide 宝典，用可视化动画拆解复杂概念，循序渐进的由浅入深的帮助大家理解和掌握 Agent 智能体。并且每节内容，都覆盖了核心内容的讲解，八股文章的总结和课后面试问题的考察。除此之外，还附带了 AI 工具（免费的）帮助大家理解和学习整套课程。可以说这套教程，是当下最系统的中文 AI Agent 学习资源之一。

>接下来，小傅哥就详细的介绍下 ai-agent-guide 教程，方便大家知道都可以学习到啥。

## 一、教程能学到啥？

这套教程一共 21 章，小傅哥给大家分成了 6 大篇章，从零基础到面试通关，一步步来。

### 第一篇：Agent 基础认知（第0-5章）

> 🎯 目标：搞懂 AI Agent 是啥，为什么需要它，和 Chatbot 有啥区别。

| 章节 | 标题 | 学完你会 |
|------|------|----------|
| 第0章 | Agent 能力全景展示 | Token、Prompt、Embedding 全景认知，建立整体概念 |
| 第1章 | 大模型与 Agent 基础概念 | LLM 原理、Token 机制、Prompt Engineering 怎么写 |
| 第2章 | 什么是 AI Agent？ | Agent 定义、架构、与 Chatbot 的本质区别 |
| 第3章 | 你的第一个 Agent：天气查询 | 从零构建 Agent，Function Calling 实战 |
| 第4章 | ReAct：让 Agent 学会思考 | Reasoning + Acting 循环，思维链拆解 |
| 第5章 | Agent 的记忆系统 | 短期/长期记忆、向量检索、记忆管理 |

<div align="center">
	<img src="https://bugstack.cn/images/article/ai/ai-agent-guide-02.png" width="750px"/>
</div>
**💡 这一篇是入门关键**，很多伙伴卡在"Agent 到底是啥"这个问题上。小傅哥用可视化动画，把抽象概念具象化，看完你就能跟面试官掰扯明白了。

### 第二篇：工具与技能（第6-9章）

> 🛠️ 目标：让 Agent 拥有"手"和"脑"，能调用工具、组合技能。

| 章节 | 标题 | 学完你会 |
|------|------|----------|
| 第6章 | Function Calling 与工具设计 | 工具协议、参数 Schema、最佳实践 |
| 第7章 | MCP：工具的标准化接口 | Model Context Protocol、Server/Client 架构 |
| 第8章 | Skills：工具的组合与复用 | 技能编排、Prompt 模板、组合调用 |
| 第9章 | CLI 能力：Agent 操作本地工具 | Shell 执行、文件操作、系统交互 |

<div align="center">
	<img src="https://bugstack.cn/images/article/ai/ai-agent-guide-03.png" width="750px"/>
</div>

**💡 这一篇是实战核心**，Agent 光会聊天没用，得能干活。从 Function Calling 到 MCP 协议，再到 Skills 技能组合，最后到 CLI 命令行操作，层层递进，让你的 Agent 真正成为"数字员工"。

### 第三篇：多 Agent 协作（第10-11章）

> 🤝 目标：从单 Agent 到多 Agent 系统，理解协作模式和编排机制。

| 章节 | 标题 | 学完你会 |
|------|------|----------|
| 第10章 | 多 Agent 系统架构 | 协作模式、通信机制、分工策略 |
| 第11章 | LangGraph 与状态机 | 图编排、状态流转、条件分支 |

**💡 这一篇是进阶内容**，单兵作战已经不够了，现实场景都是团队协作。多 Agent 协作、LangGraph 状态机编排，这些是工业级 Agent 系统的必备知识。

### 第四篇：框架与平台（第12-13章）

> 🏗️ 目标：了解主流 Agent 框架和低代码平台，知道怎么选、怎么用。

| 章节 | 标题 | 学完你会 |
|------|------|----------|
| 第12章 | 主流 Agent 框架对比 | LangChain / CrewAI / AutoGen 横评 |
| 第13章 | Dify、Coze 与可视化编排 | 低代码平台、工作流设计、插件生态 |

<div align="center">
	<img src="https://bugstack.cn/images/article/ai/ai-agent-guide-04.png" width="750px"/>
</div>

**💡 这一篇是选型指南**，市面上框架这么多，到底选哪个？小傅哥帮你横向对比，再结合 Dify、Coze 这类低代码平台，让你知道什么时候该写代码、什么时候该拖拽。

### 第五篇：实战场景（第14-16章）

> 🚀 目标：CLI Agent、GUI Agent、RAG 三大实战场景全覆盖。

| 章节 | 标题 | 学完你会 |
|------|------|----------|
| 第14章 | CLI Agent：命令行智能助手 | 终端 Agent 实战、代码生成、运维自动化 |
| 第15章 | GUI Agent：浏览器自动化 | 网页操作、表单填写、截图理解 |
| 第16章 | RAG：检索增强生成 | 文档切分、向量化、检索策略 |

<div align="center">
	<img src="https://bugstack.cn/images/article/ai/ai-agent-guide-05.png" width="750px"/>
</div>

**💡 这一篇是落地实操**，学完就能用在项目里。CLI Agent 帮你自动运维，GUI Agent 帮你自动填表，RAG 帮你做知识库问答。这些都是当下企业最需要的 Agent 应用场景。

### 第六篇：工程化与展望（第17-21章）

> ⚙️ 目标：Agent 的评估、安全、部署，以及未来趋势展望。

| 章节 | 标题 | 学完你会 |
|------|------|----------|
| 第17章 | Agent 评估与可观测性 | 评测指标、Trace 追踪、LangSmith |
| 第18章 | Agent 安全与防护 | Prompt 注入、权限控制、沙箱隔离 |
| 第19章 | Agent 部署与运维 | 容器化、弹性伸缩、监控告警 |
| 第20章 | 推理框架与模型服务化 | Ollama、vLLM、Spring AI 部署实践 |
| 第21章 | 2026 Agent 技术展望 | 多模态、具身智能、Agent 生态趋势 |

**💡 这一篇是收官之作**，从工程化角度保障 Agent 的稳定运行，最后展望未来，让你知道 AI Agent 的未来在哪，提前布局。

## 二、教程有啥特色？

### 1. 可视化动画，概念秒懂

<div align="center">
	<img src="https://bugstack.cn/images/article/ai/ai-agent-guide-06.png" width="750px"/>
</div>

很多教程讲 ReAct、MCP 这些概念，上来就是一堆文字和代码，看半天不知所云。

小傅哥的教程不一样，**每章都有自研的 SVG 流程图引擎**，把抽象概念画成动画。比如 ReAct 的 Reasoning + Acting 循环，你看一遍动画就记住了，比看十遍文字都管用。

### 2. 每章三板斧：文章 + 八股 + 考试

<div align="center">
	<img src="https://bugstack.cn/images/article/ai/ai-agent-guide-07.png" width="450px"/>
</div>

<div align="center">
	<img src="https://bugstack.cn/images/article/ai/ai-agent-guide-08.png" width="450px"/>
</div>


每章内容，小傅哥给你拆成三个部分：

- 📖 **文章**：章节正文，动画流程图 + 代码示例，循序渐进
- 📋 **八股**：面试高频考点精炼总结，面试官视角点评，考前必看
- 📝 **考试**：课后考试题，5 道单选 + 3 道多选，自动判分，错题收录

学完一章，考一下，知道自己掌握没。130+ 道面试题，模拟真实面试场景。

### 3. 内置 AI 助教，边学边问

<div align="center">
	<img src="https://bugstack.cn/images/article/ai/ai-agent-guide-09.png" width="350px"/>
</div>

遇到不懂的？右边直接问 AI 助教！我都帮你做好了匹配这套教程的轻量智能体。

- **开箱即用**：内置免费 API，不用额外配置
- **上下文感知**：AI 知道你正在学哪章，回答更精准
- **多模型支持**：GPT / Claude / Gemini / 国产模型都能配
- **流式响应**：打字机效果，实时显示

## 三、配套工具：让学习更轻松

光有教程还不够，小傅哥还给你准备了实战项目，让你的学习事半功倍。**WaLiCode：AI 编码助手**

<div align="center">
	<img src="https://bugstack.cn/images/article/project/walicode/walicode-introduce-05.png" width="750px"/>
</div>

<div align="center">
	<img src="https://bugstack.cn/images/article/project/walicode/walicode-introduce-11.png" width="750px"/>
</div>

[WaLiCode](https://walicode.xiaofuge.cn/) 是小傅哥自研的 AI 编码助手，这套教程就是基于 WaLiCode 开发的。

- **Skills 技能支持**：安装各种技能包，扩展 AI 能力
- **SSH 远程操作**：直接连接服务器，部署、调试一条龙
- **MCP 协议支持**：连接各种工具和服务
- **多模型切换**：支持多个 LLM 提供商

学教程的过程中，配合 WaLiCode 实践，效果更佳！课程：[https://t.zsxq.com/s83De](https://t.zsxq.com/s83De)

## 四、怎么学最高效？

小傅哥给你规划了一条**最高效的学习路径**：

### 1. 零基础入门（推荐新手）

```
第0章 → 第1章 → 第2章 → 第3章 → 第4章 → 第5章
  ↓         ↓         ↓         ↓         ↓
 建立认知   懂LLM    懂Agent   动手做    懂ReAct  懂记忆
```

**耗时**：约 1 周

这一条路径，适合完全没有 AI Agent 经验的伙伴。按顺序学完前五章，你就能理解 Agent 的基本原理，并且亲手写出你的第一个天气查询 Agent。

### 2. 实战进阶（有基础推荐）

```
第6章 → 第7章 → 第8章 → 第9章 → 第10章 → 第11章
  ↓         ↓         ↓         ↓         ↓         ↓
 工具调用   MCP协议   技能编排   CLI操作   多Agent   状态机
```

**耗时**：约 1.5 周

这条路径适合已经了解 Agent 基础的伙伴，重点攻克工具调用、多 Agent 协作、LangGraph 编排等核心技术。

### 3. 面试突击（求职推荐）

```
全章快速过 → 重点看八股 → 做考试 → 查漏补缺
```

**耗时**：约 3 天

每条路径最后，别忘了做每章的考试！130+ 道面试题，覆盖所有核心考点。面试前刷一遍，心里有底。

---****

