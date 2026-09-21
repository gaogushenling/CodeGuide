---
title: DSH Java Desktop
lock: no
---

# DSH-Java + A2A，我构建了桌面版数字人！

作者：小傅哥
<br/>博客：[https://bugstack.cn](https://bugstack.cn)
<br/>项目：[https://t.zsxq.com/kYcVt](https://t.zsxq.com/kYcVt)

>沉淀、分享、成长，让自己和他人都能有所收获！😄

大家好，我是技术UP主小傅哥。

**来啦，死鬼！** 👻 一款基于  DSH Java Agent Runtime 构建的 AI 智能体桌面端整好了；具备`编码`、`绘图`、`文档`、`图表`等多场景工作能力！

<div align="center">
    <img src="https://bugstack.cn/images/article/project/deepseek-harness-java/dsh-java-desktop-01.png" width="250px">
</div>

**但，它还不只局限于此！**

以 **A2A（+dsh.v1）** 的开放协议设计（*`把大腿🦵接上啦`*），我让这款智能体具备了跨端协作能力，通过多 Agent 协作会话，把单应用智能体升级为数字人 👬🏻 协同（开了个微信聊天群）；`云服务器的 Agent`、`产品库 PRD Agent`、`舆情监测和故障巡检 Agent`、`开发机 Agent`、`大数据数仓 Agent`、`离职同事蒸馏 Agent`等，现在他们就像你的同事，都在一个聊天群里进行对话协作办公。再结合，Skills、MCP、CLI，让你可以无限连接🔗。

<div align="center">
    <img src="https://bugstack.cn/images/article/project/deepseek-harness-java/dsh-java-desktop-02.png" width="950px">
</div>

`DSH Java Desktop` 是 `deepseek-harness-java`（Agent Runtime 服务端）的桌面工作台：使用 **TypeScript + React** 构建界面，通过 **Tauri 2** 负责窗口、进程与本机能力；智能体能力依赖于 DSH Java 服务，通过桌面壳启动 `deepseek-harness-java` 的 Spring Boot JAR，并通过本机 HTTP/SSE API 调用完成会话。这套东西设计的流程性蛮不错的，核心 Agent 运行时升级迭代方便。

在使用中，通过对话可以直接完成 draw.io 流程图制作、也能搞定 excel、word、md 多种类型文件，还能把一群人（跨端 Agent）拉倒一个群里对话协议做。咋样，是不挺帅的。接下来，小傅哥就给大家介绍这套软件；`怎么运行体验`、`了解架构设计`、`如何二次开发`。

>💐 文末（结尾）提供了 DSH-Java 项目服务端源码，以及 WaLiSSH、WaLiAPI、WaLIOffice、AI MCP Gateway 等各项编程项目的工程源码源码。

## 一、我的思路

我用过 Spring AI，也跟过 Google ADK，在早期也基于 OpenAI 协议文档，手搓 SDK 包。我想做各类场景的智能体实现，但不想每个场景都从头实现。MCP 可以连接服务、Skills 可以做规约限制，但仍然需要，找到一个更好的架构方式，在各场景快速完成智能体实现。所以，我干了现在的事，让底层提供一套干净的运行时 Agent。`后面有其他小公司找我做场景应用智能体，我基本可以一天内就完成初步的对接。`

>有人提到，为啥不用 Codex、Claude Claude 直接作为公司的商城的智能客服（配置个 skill 就可以），先说不人家会扒你裤衩🩲，上传你代码不。而是这样的软件本身就有一套庞大的提示词（起步60k）来支撑特定场景使用。所以，即使你的 Skills 约束再多，也免不了提供的商城客服，可能反手就帮用户做其他的去了，比如画个猫和老鼠，给我写个 Hello World！

第一阶段是 `Dify`、`Coze` 方案，通过拖拉拽编排场景智能体。第二阶段是 AI Agent 脚手架，把 Spring AI + Google ADK 做成通用智能体开发框架，快速搭建通用工程实现。现在是第三阶段 Harness 🐴 马具，以 DSH 为参考，设计实现 Java 版本，通过 ClassLoader 热加载机制，对用户实现的插件进行装配使用。

所以，一个多月时间，我分了三步走 👣
- 第1步；基于 Java + DDD，1:1 复刻 DeepSeek Harness 项目。
- 第2步；上线 [dsh-java.xiaofuge.cn](https://dsh-java.xiaofuge.cn/) 官网，通过商城智能客服、MySQL 运维平台，教大家如何通过插件开发快速构建智能体。
- 第3步；就是现在，我还要给你一个桌面版（虽然当前阶段他还没有那么完善，但更为重要的是这整套的架构方案，以及你可以拿去二开），为大家提供跨端Agent 协同办公。这是企业里非常重要的数字人设计。—— 你也可以学习后，承接各类小企业的活，构建数字人智能体。

## 二、产品介绍

### 1. 下载安装

**产品官网**；[https://dsh-java.xiaofuge.cn](https://dsh-java.xiaofuge.cn/) - `mac\windows\linux`，产品初期可能会存在一些小 Bug（但不会把你的代码搬走），可以拿到源码后，陆续迭代使用。`授权；所有小傅哥社群用户，可以修改软件名称，发布成自己的作品，让用户安装使用。`

<div align="center">
    <img src="https://bugstack.cn/images/article/project/deepseek-harness-java/dsh-java-desktop-11.png" width="850px">
</div>

如果你想体验数字人的多 Agent 协作，可以把在其他地方部署 DSH-Java 服务（下文有数字人方式），在桌面端配置数字人管理起来。嘿，估计用不了多久，很多桌面端程序也都会陆续引入数字人场景。

### 2. 源码启动

桌面版应用由两套东西组成，一个是后端 DSH-Java 运行时服务，另外一个是前端 DSH-Java-Desktop。整个应用的过程，是把 DSH-Java 构建的 Jar 放到前端工程中，并加入 JVM 最小依赖用于启动 Jar 包。

这样我们就把整个东西链接起来了，正因为如此，我们把运行时智能体做成了服务，那么这套服务，既可以是桌面直接启动的本地的，也可以是远程服务器上的。那么，Agent 协同办公的数字人就随之而来了。

<div align="center">
    <img src="https://bugstack.cn/images/article/project/deepseek-harness-java/dsh-java-desktop-03.png" width="600px">
</div>

> 目前这2套工程源码，开放在小傅哥的社群「码农会锁」，项目地址；[https://t.zsxq.com/kYcVt](https://t.zsxq.com/kYcVt)

#### 2.1 环境要求

| 依赖 | 版本要求 | 说明 |
| --- | --- | --- |
| Node.js | ≥ 20 | 前端构建（推荐 22） |
| Rust 工具链 | 稳定版 | Tauri 壳编译必须，通过 [rustup](https://rustup.rs) 安装 |
| JDK | ≥ 17 | 仅编译服务端 JAR 时需要（运行时应用会优先用内置 JRE） |
| Maven | ≥ 3.8 | 仅编译服务端 JAR 时需要 |

平台额外依赖：

- **macOS**：Xcode Command Line Tools（`xcode-select --install`）。
- **Windows**：已自带 WebView2（Win10/11 一般无需操作）；需 Visual Studio C++ Build Tools。
- **Linux**：`webkit2gtk-4.1`、`libappindicator` 等系统库（参考 Tauri 官方 prerequisites）。

#### 2.2 获取代码

桌面端与配套服务端**必须同级放置**（服务端路径被开发模式回退逻辑引用）：

```bash
mkdir -p ~/coding/github/deepseek-harness && cd ~/coding/github/deepseek-harness
git clone git@gitcode.net:KnowledgePlanet/deepseek-harness-java.git deepseek-harness-java
git clone git@gitcode.net:KnowledgePlanet/dsh-java-desktop.git DSH-Java-Desktop
```

目录结构应为：

```text
deepseek-harness/
├── deepseek-harness-java/    # 服务端（Spring Boot，产出内置 JAR）
└── DSH-Java-Desktop/         # 桌面端（本工程）
```

#### 2.3 构建内置服务端 JAR（一次性）

桌面端启动时会拉起一个内置的 Spring Boot JAR（`resources/agent/deepseek-harness-java-app.jar`，不入 Git），首次准备需要构建它：

```bash
cd DSH-Java-Desktop
npm run agent:prepare
```

这一条命令会依次完成：

1. `agent:build` —— 到 `../deepseek-harness-java` 执行 `mvn -DskipTests package`；
2. `agent:copy` —— 把产出的 JAR 复制为 `resources/agent/deepseek-harness-java-app.jar`；
3. `agent:runtime` —— 按当前平台下载 Temurin JRE 17 到 `resources/agent/runtime`（可选，下载失败也不影响开发运行，见第 4 步说明）。

> 如果不想下载内置 JRE，可跳过第 3 步：开发模式下 Java 运行时按 `DSH_AGENT_JAVA` 环境变量 → 内置 Runtime → 系统 `java` 的顺序选择，只要系统装有 JDK 17+ 即可。

---

#### 2.4 安装依赖并启动

```bash
cd DSH-Java-Desktop
npm install         # 换机器 / 拉新代码后如报 Failed to resolve import，先执行这步
npm run tauri dev
```

首次执行会编译 Rust 壳，耗时较长（几分钟），后续启动很快。成功后会弹出桌面窗口，窗口内即 React 界面。

启动过程中 Tauri Rust 层会自动：

1. 选择一个空闲的本机端口；
2. 用内置 Runtime（或系统 Java）拉起服务端 JAR 子进程；
3. 把端口、运行状态写入 `<app-data-dir>/agent-runtime.json`（macOS 为 `~/Library/Application Support/cn.xiaofuge.desktop/`）。

> 综上，如果你之前没怎么折腾过这块内容，可以在 AI Agent 工具里，让帮你完成工程的初始化和启动。

### 3. 功能简述

DSH-Java Desktop 桌面版，基本与市面 Codex 类型的产品是类似的。差一点主要在于`数字人`功能，创建数字人，把数字人加入到项目上，之后对话的时候就可以自动的使用数字人了。

#### 3.1 基础功能

<div align="center">
    <img src="https://bugstack.cn/images/article/project/deepseek-harness-java/dsh-java-desktop-04.png" width="850px">
</div>

| 能力域 | 覆盖内容 |
| --- | --- |
| 对话与工作区 | 项目/工作区选择（含多子工程）、会话管理（置顶、自定义标题、排序）、流式消息（SSE）、Markdown/GFM 渲染、停止生成 |
| 流式稳定性 | 空闲看门狗（120s 无字节中断）、AbortSignal 接入读循环、失败后按 agentId 走 REST 对账静默兜底、房间流指数退避自动重连 + 事件续传 + 运行期 5s REST 轮询对账 |
| 模型接入 | 渠道模板、Base URL + API Key 配置、同步上游模型列表、模型激活与删除、运行时模型切换 |
| 工具审批 | 运行期工具调用以对话区内紧凑提示条处理，允许/拒绝 |
| 资源插件 | 内置 **Word / Excel / Markdown / ECharts / draw.io** 五类资源生成，各有专属图标与预览 |
| draw.io | 内嵌 embed.diagrams.net：预览（chromeless）/ 编辑（kennedy UI + 800ms 防抖自动保存落盘） |
| 文件产物 | 消息内联文件卡片（代码文件带行号源码查看）、按扩展名分类图标与颜色、右键菜单（打开 / 打开文件夹 / 另存为 / 复制路径）、目录识别与打开、失效路径置灰标识 |
| 数字人协作 | 数字人目录（本地 DSH / 远端 DSH / A2A 三类接入）、添加向导（自动探测 Agent Card）、协作房间、群聊消息流、任务编排（Planner 自动分工 + 任务 DAG 依赖）、成员定向问答（ASK 协议）、失败自动恢复（改派/重试）、任务取消与级联终止、产物卡与审批 |
| 开放协议 | 服务端侧：DSH v1 卡片、A2A 0.3.x 标准卡片与 JSON-RPC（message/send、message/stream SSE、tasks/get、tasks/cancel）；客户端侧：双协议探测发现、凭据随请求携带 |
| 扩展管理 | 设置页统一管理：**Skills**（Git 安装 / 启停 / 删除）、**MCP Servers**（增删改 + 保存前测连 + 运行期热更新）、**CLI 命令**（claude / codex / acp）；服务端同时注册 6 个 `extension_*` 对话工具，可在对话中直接管理扩展 |
| 运行信息面板 | 工作区与子工程的 Git 分支展示与下拉切换（git checkout）、Git 变更查看 |
| 桌面体验 | 系统通知（未聚焦会话时）、对话完成提示音（Web Audio 合成，成功/失败双音）、侧边栏拖宽、自动更新 |

#### 3.2 数字人（多Agent协作）

##### 步骤1 - 下载jar

下载 DSH Java 服务的 Jar 地址；[https://drive.weixin.qq.com/s?k=ACMA4AfQABUnIBrQ39](https://drive.weixin.qq.com/s?k=ACMA4AfQABUnIBrQ39)

##### 步骤2 - 启动服务，可以是云服务器

<div align="center">
    <img src="https://bugstack.cn/images/article/project/deepseek-harness-java/dsh-java-desktop-07.png" width="950px">
</div>

```java
curl -fsSLO https://dsh-java.xiaofuge.cn/scripts/start-local-jar.sh
chmod +x start-local-jar.sh
./start-local-jar.sh
```

- 如果是云服务器，注意⚠️在安全组，开放端口 `8090`
- 之后，云服务器IP:8090 访问，设置里配置模型，之后验证对话。

##### 步骤3 - 链接数字人

<div align="center">
    <img src="https://bugstack.cn/images/article/project/deepseek-harness-java/dsh-java-desktop-08.png" width="950px">
</div>

- 通过 A2A 协议，链接远程 Agent 智能体。

##### 步骤4 - 添加数字人

<div align="center">
    <img src="https://bugstack.cn/images/article/project/deepseek-harness-java/dsh-java-desktop-09.png" width="950px">
</div>

- 点项目里的操作（3个点），添加数字人。
- 添加完成后，就可以对话使用了。在当前项目下对话，会自动识别数字人并使用。

## 三、架构设计（DSH Java Desktop）

> 这里是《DSH Java Desktop》项目的架构设计相关的简要介绍，面向有一定工程背景的读者，重点讲清三个问题：为什么桌面端要"只做壳"、一个 Java 实现的 Agent Runtime 如何驱动 ReAct 循环、以及多数字人协作如何在不失控的前提下并行。

<div align="center">
    <img src="https://bugstack.cn/images/article/project/deepseek-harness-java/dsh-java-desktop-05.png" width="650px">
</div>

### 1. 顶层设计决策：桌面端只做壳，能力由服务端承载

大多数 AI 桌面应用的路径是把 Agent 逻辑写进前端或 Node 侧，遇到复杂编排就会把 UI 项目拖成大杂烩。DSH Java Desktop 做了相反的选择——**智能体能力内嵌而非重写**：

- `deepseek-harness-java-app.jar`（Spring Boot 3.3，DDD 六边形架构）作为 Tauri bundle resource 直接打进安装包（`resources/agent/`）。ReactLoopAgent 主循环、会话事件溯源、工具注册与执行、任务队列、权限审批、模型渠道管理、数字人协作域，全部由服务端实现，桌面端只做 UI 投影。
- 服务端以 `standalone` profile 运行，存储使用本地 H2，数据落在应用数据目录——桌面场景做到零外部依赖，不要求用户先部署 MySQL。
- 发布版内置 Temurin JRE 17（`resources/agent/runtime`，由 `scripts/prepare-runtime.mjs` 按平台下载），用户无需安装或配置 JDK，应用也不污染 `JAVA_HOME` / `PATH`。

这个决策带来两个直接收益：**桌面端与服务端可以独立演进**（服务端改动只需重打 JAR 覆盖 resource）；**同一套 Runtime 既能内嵌在桌面端，也能部署在远端服务器**，为后面的"数字人协作"铺平了道路——本地数字人和远端数字人本质上是同一种东西。

### 2、 三层结构：Rust 壳、React UI、内嵌 Java Runtime

```
┌─────────────────────────────────────────────────┐
│  桌面端（Tauri 2 + React 19 + TypeScript）        │
│                                                 │
│  React UI ──invoke(22个自定义命令)──► Tauri Rust 壳 │
│      │                                │         │
│      │ HTTP/SSE (127.0.0.1)           │ spawn   │
│      ▼                                ▼         │
│  ┌───────────────────────────────────────────┐  │
│  │  deepseek-harness-java-app.jar (Spring Boot)│ │
│  │  trigger 协议接入层 / domain 核心服务层       │  │
│  │  infrastructure 基础设施层                  │  │
│  └───────────────────────────────────────────┘  │
│              ▲ 内置 Java 17 Runtime              │
└─────────────────────────────────────────────────┘
```

**Tauri Rust 壳承担的是"操作系统代理"职责**，共 22 个自定义命令：选择空闲端口、拉起/停止 JAR 子进程、捕获日志、记录运行状态到 `<app-data-dir>/agent-runtime.json`，以及本地文件读写、凭据安全存储、系统通知、Git 分支查看与切换、自动更新。一个值得注意的细节是崩溃恢复：上次异常退出时，下次启动会先清理遗留 JAR 进程，避免 H2 文件锁冲突导致服务起不来。前端不暴露任何执行命令的安全面，UI 与 Rust 之间的边界是明确的命令契约。

**服务端是标准的 DDD 六边形架构**，按 Maven 多模块拆分：

- `trigger`（协议接入层）：Agent SSE 流、DSH 网关、A2A/AgentCard 端点、数字人协作 API、扩展管理 API；
- `domain`（核心服务层）：ReactLoopAgent、会话事件、任务/审批、模型渠道、协作编排——不依赖任何框架细节；
- `infrastructure`（基础设施层）：工具注册、MCP、Skills、CLI、H2/MySQL 持久化、远端网关实现。

端口依赖全部内向：domain 定义 `ILlmRuntimePort`、`ISkillProviderPort`、`IExtensionManagementPort` 等出站端口，infrastructure 提供适配器。这使得 LLM 供应商、扩展存储、协作协议都可以替换而不触碰核心逻辑。

**通信模型刻意收敛为两条通道**：UI → Rust 走 Tauri invoke（能力调用），UI → Java 走 `127.0.0.1` 上的 HTTP/SSE（数据流）。本地端口不进入主对话区，只在设置页展示诊断信息。

### 3. 核心：ReactLoopAgent 与事件溯源

Agent 运行时的心脏是 `ReactLoopAgent`，一个线程安全的 ReAct 驱动器：

1. 收到 Inbox 输入后唤醒，在虚拟线程中异步执行；
2. 打开 turn，流式调用 LLM（Reason）→ 执行工具（Act）→ 结果作为观察值回填下一轮输入（Observe）；
3. 直到模型不再请求工具后关闭 turn，循环处理直到 Inbox 为空。

几个实现细节体现了工程考量：

- **阶段状态机**：`phase` 用 volatile 维护，所有阶段切换在同步控制下完成；`activityDone` 用 `AtomicReference<CompletableFuture<Void>>` 追踪当前活动，保证并发唤醒时不会出现两个 turn 交叉执行。
- **流式sink按次设置**：`streamDeltaSink` / `streamToolCallSink` / `streamFinishSink` 等由 SSE 请求按次注入，把"模型增量输出"实时推给前端分段渲染，同时不与长驻的 Agent 生命周期耦合。
- **上下文压缩**：`CompactionEngine` 在会话变长时压缩历史，避免长对话撑爆上下文窗口。
- **事件溯源**：每一步（模型输出、工具调用、结果回填）都通过 `SessionEventFactory` 写入会话事件日志（SessionLog / SessionEvent）。配套有 `SessionWriteLeaseService`（写租约防并发写坏）、`SessionRebuilderService`（从事件重建会话状态）和 `InMemorySessionProjectionCache`（读投影缓存）。**事件日志是唯一事实源，UI 只是投影**——这个原则贯穿整个系统。

### 4. 数字人协作域：房间、任务 DAG 与开放协议

<div align="center">
    <img src="https://bugstack.cn/images/article/project/deepseek-harness-java/dsh-java-desktop-06.png" width="950px">
</div>

<div align="center">
    <img src="https://bugstack.cn/images/article/project/deepseek-harness-java/dsh-java-desktop-10.png" width="950px">
</div>

"数字人"在 DSH 里不是带头像的聊天入口，而是**可被发现、被授权、可执行任务、可参与协作的 Agent 身份**。身份（名称、头像、用途、权限）与执行体（模型、工具、会话）解耦：同一个数字人身份可以指向本地 Runtime，也可以指向远端服务。

协作采用"**房间承载上下文，任务承载分工，事件日志承载审计**"的模式，刻意回避了自由群聊式多 Agent 协作常见的重复劳动与上下文膨胀：

1. 用户在房间描述目标，或 `@成员名` 定向派发；
2. Planner 生成计划，展开为**任务 DAG**——无依赖任务并行执行，有依赖的任务等上游产物就绪后自动续跑；
3. 成员执行中可通过 ASK 协议定向提问，答复自动注入指令续跑；
4. 失败恢复有明确预算：每任务 1 次恢复机会，优先改派（按能力标签匹配），无候选则同员重试，耗尽才级联终止下游；
5. 取消语义完整：任务注册表 + FutureTask 取消 + 状态不被覆盖 + 下游级联置 FAILED。

所有协作事件归一化为 RoomEvent 落库，前端通过 SSE 订阅 + REST 轮询对账消费——聊天消息、工具卡、任务状态、产物、审批都只是事件流的投影。

**协议层是双栈设计**。服务端同时实现 DSH v1 Agent Card（`/.well-known/dsh-agent-card`）与标准 **A2A 0.3.x** 协议（`/.well-known/agent-card.json` + JSON-RPC `/a2a` 端点，支持 `message/send`、`message/stream` SSE、`tasks/get`、`tasks/cancel`）。客户端侧做双协议探测发现——添加数字人时填入 Base URL，应用自动探测 Agent Card 并预填能力信息。这意味着远端任何符合 A2A 标准的第三方 Agent 都能接入房间，与本地数字人同场协作，不需要对方也跑 DSH。

> DSH Java Desktop 的架构可以用一句话收束：**桌面端是投影，服务端是事实，协议是边界**。桌面端做壳换取部署简单与服务端复用；事件溯源换取断流可恢复与协作可审计；DSH/A2A 双协议换取本地与远端、自有与第三方的互通。这三个选择互为支撑，构成了一个既能单机开箱即用、又能跨端组建数字人团队的完整体系。

## 四、项目学习（包含所有源码）

这里为伙伴们推荐一套 AI 从通识、应用、项目，全套流程路线。你可以刷到 AI 八股，也可以学会 AI VibeCoding 编程，还能实践各类 AI 项目。如，市面的 AI IDE（walissh、walicode）教你做一套市面上的 trae.ai/qcoder 一样的编程工具。WaLiAPI（LLM 负载、日志审计、RAG 知识库）、AI MCP Gateway 教你如何构建 AI Infra 基础设施。

这里的所有内容，所有的项目，都从 [bugstack.cn](https://bugstack.cn/)实战项目进入学习；

<div align="center">
    <img src="https://bugstack.cn/images/article/project/ai-agent-scaffold/part-1/1-1/images/ai-agent-scaffold-1-1-10.png" width="850px">
</div>

> 该路线，体现了3套架构（拖拉拽-Dify方案、AI Agent 脚手架方案、Deepseek-harness-java 插件方案），以及一套基础设施（AI MCP Gateway\WaLiAPI），和业务类型、技术类型，以及基础知识教程。

<div align="center">
    <img src="https://bugstack.cn/images/article/project/deepseek-harness-java/dsh-java-desktop-12.png" width="950px">
</div>
