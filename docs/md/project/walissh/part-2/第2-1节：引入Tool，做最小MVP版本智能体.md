---
title: 第2-1节：引入Tool，做最小MVP版本智能体
pay: https://t.zsxq.com/9rpjk
---

# 《WaLiSSH - AI Shell 智能终端》第2-1节：引入Tool，做最小MVP版本智能体

作者：小傅哥
<br/>博客：[https://bugstack.cn](https://bugstack.cn)
<br/>视频：[https://t.zsxq.com/UjQBY](https://t.zsxq.com/UjQBY)

>沉淀、分享、成长，让自己和他人都能有所收获！😄

大家好，我是技术UP主小傅哥。

前面第一章，我们完成了 SSH 连接管理、终端命令交互——用户可以在 Web 终端里手动敲命令操作远程服务器。但你想过没有：如果用户不懂 Linux 命令呢？如果用户说一句"帮我查看服务器系统信息"，系统就能自动执行命令并返回分析结果，那是不是比手动敲 `uname -a`、`df -h`、`free -m` 体验好太多了？

这就是 AI Agent 的核心价值——**让大模型不只是"聊天"，而是"干活"**。

今天这节，我们就给 WaLiSSH 装上"手脚"，引入第一个 Tool 工具，做一个最小可用版本（MVP）的智能体；用户输入自然语言 → AI 自动生成 Shell 命令 → 调用工具在 SSH 终端执行 → 分析结果返回用户。这部分本身 Google ADK 就带有轻量的 ReAct 模式，会自主循环直至完成工具输出结果，我们用就它做第一个 MVP 案例。

## 一、本章诉求

实现一个最小 MVP 版本的 SSH AI Agent：基于 Google ADK（Agent Development Kit）+ Spring AI，通过 `FunctionTool` 注册 SSH 命令执行工具，让大模型能够"感知"到工具的存在并主动调用。核心内容包括：

- **Tool 工具开发**：`SshExecuteAdkTool`——用 `@Annotations.Schema` 定义工具参数，供 LLM 识别和调用
- **Agent 装配链路**：`DefaultArmoryFactory` 责任树装配，`AgentNode` 注册工具，`RunnerNode` 包装运行器
- **ReAct 循环机制**：理解 `LlmAgent.runAsyncImpl` → `BaseLlmFlow.run` 的多步推理-行动循环
- **LLM 工具识别全链路**：从 `@Schema` 注解 → `FunctionTool.create()` → `FunctionDeclaration` → HTTP `tools` 字段
- **Plugin 插件观测**：`MyTestPlugin` 在每个关键节点输出日志，让 Agent 执行过程"可见"

你可以把这个过程当成给一个"聪明的实习生"配了一把钥匙（Tool）——他知道什么时候该用钥匙开门（Function Call），开门后看到什么（Tool Response），再决定下一步做什么（ReAct Loop）。

## 二、流程设计

如图，整个智能体 MVP 版本的核心设计；

<div align="center">
    <img src="https://bugstack.cn/images/article/project/walissh/walissh-2-1-01.png" width="950px">
</div>

### 1. ReAct 核心循环流程

ReAct（Reasoning + Acting）是当前主流的 Agent 执行范式——大模型先"推理"（Reasoning）判断需要做什么，再"行动"（Acting）调用工具执行，拿到结果后继续推理，循环直到完成任务。

<div align="center">
    <img src="https://bugstack.cn/images/article/project/walissh/walissh-2-1-02.png" width="950px">
</div>

上图展示了 WaLiSSH 中 ReAct 循环的核心执行链路，对应 Google ADK 的三个关键源码类：

**① `LlmAgent.runAsyncImpl`** — 单步执行入口

当用户消息进入 Agent 后，`runAsyncImpl` 是每个"步"的起点。它调用 `llmFlow.run()` 发起一次 LLM 请求，拿到响应事件流后，通过 `concatMap` 逐个处理：保存中间输出到会话状态（`maybeSaveOutputToState`），检查是否需要暂停（`shouldPauseInvocation`），正常情况下直接透传事件。

**② `BaseLlmFlow.run`** — 多步循环控制器

这是整个 ReAct 机制的核心。`run()` 方法内部是一个递归循环：

```
run(step=0)
  → runOneStep()          // 执行一步：preprocess → callLlm → postprocess
  → .cache()              // 缓存事件流，允许多次订阅
  → concatWith(
      toList() → 判断最后一个事件:
        - finalResponse=true → Flowable.empty()  // 结束
        - endInvocation=true → Flowable.empty()  // 结束
        - 有 functionCall 且未结束 → defer(() → run(step+1))  // 递归下一步
    )
```

👩🏻‍🏫敲黑板：`concatWith` 的作用是——先把当前步的事件**全部输出给用户**（流式），输出完了再判断要不要继续下一步。用户看到的是流畅的"思考→执行→回答"过程，不会卡顿。`Flowable.defer` 保证延迟递归，不会立即执行导致爆栈。

**③ `BaseLlmFlow.runOneStep`** — 单步三段式

每一步内部分三个阶段：

| 阶段 | 方法 | 职责 |
|------|------|------|
| 预处理 | `preprocess()` | 注入 system prompt（instruction）+ 工具声明（FunctionDeclaration） |
| 调用模型 | `callLlm()` | 构建 LlmRequest，调用 Spring AI ChatModel → HTTP 请求大模型 API |
| 后处理 | `postprocess()` | 检查响应中是否有 function call，有则执行工具，无则返回最终文本 |

