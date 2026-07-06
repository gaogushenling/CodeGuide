---
title: 第1-7节：SSH命令处理
pay: https://t.zsxq.com/zjJkn
---

# 《WaLiSSH - AI Shell 智能终端》第1-7节：SSH命令处理

作者：小傅哥
<br/>博客：[https://bugstack.cn](https://bugstack.cn)
<br/>视频：[https://t.zsxq.com/TxVuy](https://t.zsxq.com/TxVuy)

>沉淀、分享、成长，让自己和他人都能有所收获！😄

大家好，我是技术UP主小傅哥。

上一节我们完成了前端和后端 SSH 连接 API 的对接，可以在界面上完成创建、编辑、删除、连接、断开 SSH 服务器等操作。但连接上服务器之后呢？终端面板还只是一个空壳，没办法输入命令、看不到输出。

今天这节，我们就把终端面板"盘活"——让用户可以在 WaLiSSH 里像使用本地终端一样，远程操作云服务器。

## 一、本章诉求

实现 SSH 终端的核心交互能力：打开终端会话、输入命令、读取输出、调整窗口大小、断连检测与重连。涉及后端终端会话管理（Domain + Infrastructure）和前端 xterm.js 集成（TerminalPanel 改造）。

你可以把这个过程就是当成你自己在承接一次产品需求——用户说"我要在 Web 终端里敲命令"，你需要设计从后端 Shell 通道到前端渲染的完整链路。

## 二、流程设计

如图，从前端 xterm.js 到后端 JSch Shell 通道的完整数据流；

<div align="center">
    <img src="https://bugstack.cn/images/article/project/walissh/walissh-1-7-01.png" width="950px">
</div>

- 整个数据流分两条路径：**输入路径**和**输出路径**。
- 输入路径：用户在 xterm.js 里敲键盘 → `onData` 事件拿到输入字符 → 写入缓冲（10ms 批量合并）→ 调用 `POST /terminal/write` 发到后端 → 后端写入 JSch Shell 的 `OutputStream` → 远程 Shell 收到字符并执行。
- 输出路径：远程 Shell 产生输出 → 后台读取线程持续从 JSch `InputStream` 读取 → 写入 `StringBuilder` 缓冲区 → 前端每 50ms 调用 `GET /terminal/read` 轮询 → 拿到输出后 `terminal.write()` 渲染到 xterm.js。
- 👩🏻‍🏫敲黑板：这里没有用 WebSocket，而是用 HTTP 轮询。为什么？因为 WaLiSSH 是 Tauri 桌面应用，前后端都在本地，网络延迟极低，50ms 的轮询间隔对终端操作来说完全够用，实现也更简单。