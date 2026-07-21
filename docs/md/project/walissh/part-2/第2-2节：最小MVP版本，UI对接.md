---
title: 第2-2节：最小MVP版本，UI对接
pay: https://t.zsxq.com/CUrhk
---

# 《WaLiSSH - AI Shell 智能终端》第2-2节：最小MVP版本，UI对接

作者：小傅哥
<br/>博客：[https://bugstack.cn](https://bugstack.cn)
<br/>视频：[https://t.zsxq.com/nuZqN](https://t.zsxq.com/nuZqN)

>沉淀、分享、成长，让自己和他人都能有所收获！😄

大家好，我是技术UP主小傅哥。

上一节我们在后端把智能体跑通了——控制台里输入"查看服务器系统信息"，AI 就能自动调 `executeCommand` 工具，在 SSH 终端里执行命令并分析结果。但这还有点“玩具”，用户在前端界面上还看不到任何东西：右侧面板发消息还是 `setTimeout` 模拟的假回复，AI 执行了什么命令、命令输出了什么，用户一概不知。

今天这节，我们就把 AI 智能体和前端 UI 真正"接上电"——用户在右侧对话框说一句"帮我看看磁盘使用情况"，AI 自动在左侧终端执行 `df -h`，执行过程实时可见，分析结果流式输出到对话框。这才是真正意义上的"AI Shell 智能终端"。

## 一、本章诉求

完成 AI Agent 的前后端 UI 对接，让用户可以在右侧面板与智能体对话，AI 自动调用 SSH 终端执行命令并流式返回分析结果。核心内容包括：

- **SSE 事件协议设计**：把 ADK 的 `Flowable<Event>` 事件流，转为前端可区分的结构化 JSON 事件（text / tool_call / tool_result / done / error），让 UI 能分别渲染"AI 说的话"和"工具干的事"。
- **AI 命令同步执行**：新增 `executeCommandAndWait`——上一节 AI 执行命令是"写入后立刻读"，输出可能还没回来；本节改为"写入后阻塞等待 Shell prompt 重新出现"，拿到完整输出再返回给 LLM。
- **线程安全的会话传递**：`ThreadLocal` 在线程池场景下会失效，新增会话级变量回退，保证工具一定能拿到终端会话 ID。
- **前端流式对接**：新增 `api/agent.ts`，用 fetch `ReadableStream` 逐行解析 SSE 事件；`agentStore` 从"模拟回复"改为真实流式发送；`RightSidebar` 增加智能体选择器、连接状态提示、停止生成按钮。

你可以把这个过程当成给一辆已经发动起来的车"装方向盘和仪表盘"——发动机（Agent）上一节已经点火，这节要让驾驶员（用户）能控制方向（发消息）、看到仪表（工具执行过程）。

<div align="center">
    <img src="https://bugstack.cn/images/article/project/walissh/walissh-2-2-03.png" width="950px">
</div>

## 二、流程设计

如图，本节 UI 对接后的完整数据流；

<div align="center">
    <img src="https://bugstack.cn/images/article/project/walissh/walissh-2-2-01.png" width="950px">
</div>

整个链路分为用户发起和AI反馈；

- 用户消息 → LLM 推理 → 决定调用 `executeCommand` → `SshExecuteAdkTool` 从 ThreadLocal（或会话级变量）拿到 `terminalSessionId` → `TerminalSessionPort.executeCommandAndWait` 写入命令并**阻塞等待** Shell 输出完成 → 返回清理后的结果给 LLM。
- `chatStream` 把 ADK 事件流逐条转为结构化 JSON → 通过 `ResponseBodyEmitter` 以 SSE 方式推送 → 前端 `ReadableStream` 逐行读取解析 → 按事件类型更新 UI（text 流式追加到对话框、tool_call/tool_result 展示工具执行过程）。