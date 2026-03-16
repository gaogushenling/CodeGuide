---
title: 面试：技能、简历、问题汇总
lock: no
---

# 面试：技能、简历、问题汇总

作者：小傅哥
<br/>博客：[https://bugstack.cn](https://bugstack.cn)

> 沉淀、分享、成长，让自己和他人都能有所收获！😄

## 一、项目介绍

面试官您好，本套 AI Agent 综合智能体脚手架 项目，主要为降低智能体开发门槛、提升业务系统集成效率而构建。项目涵盖了：`工程脚手架自动生成`、`智能工作流编排`、`多模态交互（文本/绘图/动作）` ，以及`手机自动化网关控制`等核心功能和场景方案。

整套项目，核心抽象并拆分了 AI Agent 执行过程所需的各项组件（`Armory 装配域` 、`Runner 执行器` 、 `Skills 技能库`等）到结构化的配置定义中，使其具备自由配置、灵活编排的特性。以此方式，开发者可以结合实际业务场景诉求，像搭积木一样编排复杂的智能体协作流程——例如项目中实现的 "AI + Draw.io 交互式绘图" 和 "Android 手机自动化网关 - MobileOpenClaw" 场景，达到“业务需要什么能力，就组装什么节点”的 AI Auto Agent 效果。

该项目在架构设计上，严格遵循 DDD（领域驱动设计） 分层架构进行开发，核心采用了 **组合模式（Composite Pattern）**，构建智能体的执行规则树（支持串行、并行、循环流转），并结合**工厂模式 （创建不同类型的 Agent/Tool 节点）**、 **策略模式 （处理不同的模型调用策略）** 以及 **责任链设计思维模式（这块按照不同的理解，说成规则树也可以） （处理节点间的上下文传递）** 来处理具体流程细节。这种设计不仅解耦了底层模型（支持 Spring AI、Google ADK）与上层业务逻辑，也使得系统在面对未来各类扩展性诉求（如新增 MCP 协议、对接新模型）时，能够更加灵活方便地进行迭代。

## 二、简历模板

**项目名称**：AI Agent 智能体通用脚手架（可以自己起项目名称）

**项目架构**：DDD 领域驱动设计（六边形架构）、事件驱动架构、前后端分离、组合模式规则引擎、模块化微服务

**核心技术** ：Spring Boot 3.4、JDK 17+、Spring AI（LangChain4j）、Google ADK（Application Development Kit）、Kotlin (Android)、MCP (Model Context Protocol)、RAG (Vector Store)、Netty、Websocket、React、Draw.io (mxGraph)、TypeScript、Maven Archetype、Docker、Nginx - `不用都写，可以适当减少。`

**项目描述** ：

本项目是一套企业级 AI Agent 综合解决方案与标准化脚手架，旨在解决智能体开发中“编排难、落地难、复用难”的痛点。系统基于 DDD 分层架构，创新性地设计了 Armory（装配域） 引擎，将复杂的业务流程抽象为可配置的节点（Node）流转。支持用户通过低代码方式，动态组装 Advisor（顾问） 、 Tools（工具） 和 Workflows（工作流） 。此外基于本套脚手架，实现了从“文本对话”到“自动绘图（Draw.io）”再到“物理设备控制（手机网关）”的全链路智能化。该平台不仅显著降低了 AI 应用的开发门槛，还通过标准化的 MCP 协议，实现了跨生态的能力互通。

**核心职责** ：

- 智能体架构设计与 DDD 建模 ：
  
  - 主导系统的领域驱动设计，划分 Armory（装配） 、 Runner（执行） 、 Skill（技能）等核心领域。采用 六边形架构 解耦底层模型依赖（Spring AI / Google ADK），确保系统可无缝切换不同的大模型供应商（OpenAI, Claude, DeepSeek）。
  - 设计基于 组合模式（Composite Pattern） 的执行规则引擎，实现了 Loop（循环优化） 、 Parallel（并行处理） 、 Sequential（串行执行） 等多种编排策略，支持复杂的动态工作流配置。
- 核心组件抽象与开发 ：
  
  - 拆解并标准化 AI Agent 的核心原子能力，构建了包括 AgentNode （智能体节点）、 AiApiNode （接口节点）、 RouterNode （路由节点）在内的组件库。
  - 设计 DynamicContext（动态上下文） 机制，利用 责任链模式 在节点间传递会话状态与中间结果，解决了多智能体协作时的数据共享与状态一致性问题。
- 多智能体协作与可视化场景实现（AI + Draw.io）- `这个场景可以独立展开作为一个简历` ：
  
  - 针对业务流程图绘制场景，设计了 Analyst（需求分析） -> Drawer（绘图执行） -> Reviewer（质量审查） 的多智能体协作链路（Multi-Agent System）。
  - 基于 React + Draw.io (mxGraph) 定制前端组件，开发了专门的 JSON 交互协议，使 AI 能够直接生成和修改 XML 图表数据，实现了“一句话生成专业 UML/流程图”的端到端能力。
  - 集成并适配（百度搜索） https://sai.baidu.com 等公开 MCP Server 资源，让绘图可以检索网络资源。
- 智能体与硬件设备交互（端侧网关建设） - `这个场景可以独立展开作为一个简历` ：
  
  - 开发了 MobileOpenClaw（手机网关） ，通过 Netty 长连接 与 Android 端 AccessibilityService（无障碍服务） 通信，赋予 AI 操作物理设备的能力（点击、滑动、截图）。以 AutoPhone GLM 为参考，做设备通信设计。
  - 使用 auto-glm-9b 模型，分析用户诉求，网关网关入口下达操作指令。让手机端完成用户的行为动作。如；点赞、下单、刷抖音、收藏、发微信，等行为动作。
- 脚手架工程化与提效 ：
  
  - 设计并发布 Maven Archetype 脚手架，支持一键生成包含完整依赖与最佳实践的 AI 工程代码。
  - 实现了 Agent 预热机制 ，在 Spring 容器启动时动态加载和校验模型配置，支持运营人员在不重启服务的情况下，通过配置中心热更新 Prompt 和编排逻辑。

## 三、面试题归档

### 项目架构与设计模式

#### 1. 请简述本项目的整体架构设计，以及为什么选择 DDD（领域驱动设计）？
**参考答案：**
本项目采用了 **DDD（领域驱动设计）** 配合 **六边形架构（Hexagonal Architecture）**。
- **分层设计**：将系统划分为 **API 接口层**（Controller/Trigger）、**应用层**（Service/Application）、**领域层**（Domain/Model）和 **基础设施层**（Infrastructure）。
- **核心优势**：
    - **解耦业务与技术**：核心业务逻辑（如 Agent 编排、策略执行）定义在 Domain 层，不依赖具体的 AI 模型（OpenAI/Claude）或数据库实现。通过 **适配器模式（Adapter Pattern）** 在 Infrastructure 层实现具体技术细节，方便随时替换底层 AI 服务商。
    - **高内聚低耦合**：各层职责清晰，便于单元测试和维护。例如，Armory 装配域专注于智能体构建，Chat 领域专注于对话逻辑。

#### 2. 在“智能体装配（Armory）”模块中，你是如何处理复杂的配置解析和对象构建的？使用了哪些设计模式？
**参考答案：**
- **设计模式**：核心使用了 **组合模式（Composite Pattern）** 和 **责任链模式（Chain of Responsibility）** 的思想，构建了一个 **节点（Node）处理管道**。
- **实现逻辑**：
    - 将复杂的 Agent 构建流程拆解为一系列独立的 **Node**（如 `AiApiNode` 配置 API、`ChatModelNode` 配置模型、`AgentNode` 实例化智能体、`AgentWorkflowNode` 处理编排）。
    - 定义了统一的 `IArmoryService` 接口和 `AbstractArmorySupport` 抽象类，确保所有节点遵循相同的规范。
    - 使用 **工厂模式（Factory Pattern）**（`DefaultArmoryFactory`）来创建和管理这些节点。
    - 通过 **上下文对象（DynamicContext）** 在节点间传递配置数据，避免了方法参数爆炸，实现了构建逻辑的 **高扩展性**（新增节点只需实现接口并注册即可）。

#### 3. 项目中是如何实现 MCP (Model Context Protocol) 的？特别是“本地 MCP”是如何设计的？
**参考答案：**
- **多协议支持**：项目支持 **SSE**（Server-Sent Events）和 **Stdio** 标准协议，通过 `McpClient` 统一封装。
- **本地 MCP 设计**：
    - **策略模式（Strategy Pattern）**：定义了 `ToolMcpCreateService` 策略接口，分别实现了 `SseMcpCreateStrategy`、`StdioMcpCreateStrategy` 和 **`LocalMcpCreateStrategy`**。
    - **反射与 Spring 容器**：**本地 MCP** 的核心是利用 Java 反射机制和 Spring 的 `ApplicationContext`。它根据配置的 `beanName` 和 `methodName` 直接查找并调用本地 Spring Bean 的方法，将其封装为 `FunctionCallback` 提供给 AI 模型。这使得 AI 可以直接调用本地业务代码（如查询数据库、发送邮件），无需走网络协议，**性能更高** 且 **开发更便捷**。

---

### 二、 并发编程与网络通信 (Netty)

#### 4. 在“手机网关”模块中，Netty 服务端是如何解决 TCP 粘包/拆包问题的？通信协议是如何设计的？
**参考答案：**
- **粘包/拆包解决方案**：使用了 Netty 自带的 **`LineBasedFrameDecoder`**。
    - **原理**：以换行符 `\n` 作为消息结束的标志。发送端在 JSON 数据后追加换行符，接收端的 Decoder 会自动根据换行符分割出完整的消息帧，从而解决 TCP 粘包和拆包问题。
- **通信协议设计**：采用 **JSON 文本协议**。
    - **请求**：`{"type": "action", "command": "click", "x": 100, "y": 200}\n`
    - **响应**：`{"type": "response", "status": "success", "data": "..."}\n`
    - **优势**：协议简单，易于调试（人类可读），且 JSON 解析库成熟。

#### 5. Netty 是异步通信的，但业务层调用（如“让手机截图”）通常需要同步等待结果，你是如何实现的？
**参考答案：**
- **核心机制**：使用了 JDK 的 **`CompletableFuture`** 实现 **异步转同步**。
- **实现步骤**：
    1.  **请求映射**：在发送指令前，创建一个 `CompletableFuture` 对象，并将其存入一个线程安全的 `ConcurrentHashMap`（Key 为请求 ID）。
    2.  **同步等待**：业务线程调用 `future.get(timeout)`，进入阻塞等待状态。
    3.  **异步回调**：当 Netty 的 `channelRead` 方法收到客户端响应时，根据响应中的 ID 从 Map 中取出对应的 `future`。
    4.  **唤醒线程**：调用 `future.complete(response)` 将结果填入，此时阻塞的业务线程会被唤醒并获取到结果。
    5.  **超时处理**：如果 `future.get()` 超时，抛出异常并从 Map 中移除该 Future，防止内存泄漏。

---

### 三、 AI 智能体编排与业务逻辑

#### 6. 请介绍一下项目中 Agent 工作流（Workflow）的设计，Loop、Parallel 和 Sequential 节点分别解决了什么问题？
**参考答案：**
项目通过 `AgentWorkflowNode` 实现了类似 **LangChain** 或 **Google ADK** 的编排能力：
- **Sequential（串行编排）**：
    - **场景**：任务之间有严格依赖关系。例如：`搜索信息` -> `整理摘要` -> `生成报告`。
    - **实现**：按顺序依次执行 List 中的 Agent，上一个 Agent 的输出作为下一个的输入。
- **Parallel（并行编排）**：
    - **场景**：任务独立且耗时，需要提高效率。例如：同时`搜索技术方案 A`、`搜索技术方案 B`、`搜索技术方案 C`，最后汇总对比。
    - **实现**：使用线程池并发执行多个 Agent，最后通过 `CountDownLatch` 或 `CompletableFuture.allOf` 等待所有任务完成并聚合结果。
- **Loop（循环编排）**：
    - **场景**：需要反复迭代直到满足条件。例如：`生成代码` -> `运行测试` -> `报错` -> `修正代码` -> `再运行测试`... 直到测试通过或达到最大重试次数。
    - **实现**：在 `LoopAgentNode` 中维护一个循环逻辑，根据 **评估函数（Evaluator）** 的结果决定是继续循环还是输出最终结果。

#### 7. 在“AI + Draw.io”场景中，如何确保 AI 生成的 XML 是可用的？前后端交互协议是如何设计的？
**参考答案：**
- **质量控制（Reviewer Agent）**：
    - 引入了 **多智能体协作（Multi-Agent System）** 机制。
    - 设计了专门的 **Reviewer（审查员）** 智能体。在 **Drawer（绘图员）** 生成 XML 后，Reviewer 会检查 XML 的语法正确性、连线逻辑（如是否交叉、是否有孤立节点）等。如果发现问题，Reviewer 会反馈给 Drawer 进行修正，直到通过审查。
- **交互协议设计**：
    - 定义了包含 `type` 字段的 JSON 协议：
        - `type: "user"`：表示 AI 需要用户补充信息（如“请问您想要画什么类型的图？”），前端渲染为对话框。
        - `type: "drawio"`：表示 AI 生成了绘图数据，前端解析 XML 并调用 Draw.io 组件进行渲染。
        - `type: "review"`：表示正在审查中（可选，用于展示状态）。
    - **优势**：明确区分了 **对话交互** 和 **指令执行**，提升了用户体验。

#### 8. 你提到的“Spring AI 动态预热”是如何实现的？有什么作用？
**参考答案：**
- **作用**：
    - **快速响应**：AI 模型（尤其是加载了大量 Prompt 或上下文的模型）初始化较慢，预热可以避免用户第一次请求时的长延迟。
    - **配置校验**：在应用启动时尽早发现 API Key 错误、网络不通等配置问题，避免上线后报错。
- **实现**：
    - 利用 Spring 的 `ApplicationRunner` 或 `CommandLineRunner` 接口，在 Spring 容器启动完成后自动触发。
    - 读取配置文件中的 `warm-up` 列表，模拟一次简单的 AI 调用（如发送 "Hello"），强制初始化底层的 `ChatModel` 和 `Token` 连接池。

---

### 进阶与优化 (Spring AI/Skills/性能)

#### 9. 在 Spring AI 集成中，项目是如何利用 "Skills" 机制来增强 RAG 或替代传统向量检索的？
**参考答案：**
- **Skills 概念**：项目引入 `spring-ai-agent-utils`，将特定领域的知识（如 PDF 处理、系统巡检脚本）封装为 **Skills（技能书）**，这不仅仅是静态文本，还包含了可执行的代码逻辑（Tools）。
- **与传统 RAG 对比**：
    - **传统 RAG**：侧重于 **检索 (Retrieval)**，即从向量数据库中找到相关文本片段喂给 LLM。优点是知识覆盖面广，缺点是不仅准确率受限于检索算法，而且无法直接操作。
    - **Skills**：侧重于 **执行 (Action)**。它将“工具定义 + Prompt 模板 + 执行脚本（Python/Shell）”打包。Agent 识别到意图后，直接加载对应的 Skill 并执行脚本。
    - **优势**：减少了 LLM 的幻觉（执行逻辑是确定性的代码），缩短了 "Prompt -> 分析 -> 找工具 -> 执行" 的决策链路，对于特定任务（如“重启服务器”）比 RAG 更精准、更安全。

#### 10. 移动网关系统中，服务端如何处理 Netty 的异步通信与 Agent 同步决策之间的矛盾？
**参考答案：**
- **矛盾点**：Netty 是基于事件驱动的异步框架，而 Agent 的思维链（Chain of Thought）通常是线性的、同步等待每一步结果的（例如：点击按钮 -> 等待截图 -> 分析截图 -> 下一步）。
- **实现机制**：
    - **Future 模式**：服务端维护一个 `Map<String, CompletableFuture<GatewayResponseVO>> pendingResponses`。
    - **同步等待**：Agent 线程在发送指令后，调用 `future.get(timeout)` 阻塞等待。
    - **异步唤醒**：Netty 的 Handler 收到手机端响应后，根据 ID 从 Map 中取出对应的 Future，调用 `future.complete(response)`。
    - **异常处理**：设置超时时间（如 30秒），防止因手机端无响应导致 Agent 线程永久阻塞。

#### 11. 项目在装配 MCP (Model Context Protocol) 工具时使用了什么设计模式？解决了什么问题？
**参考答案：**
- **设计模式**：使用了 **策略模式 (Strategy Pattern)** 配合 **工厂模式 (Factory Pattern)**。
- **解决痛点**：在 `ChatModelNode` 中，如果使用大量的 `if-else` 来判断是创建 SSE 客户端、Stdio 客户端还是本地 Bean 调用，代码会非常臃肿且难以维护。
- **实现细节**：
    - 定义了 `ToolMcpCreateService` 策略接口。
    - 实现了 `SseMcpCreateStrategy`、`StdioMcpCreateStrategy`、`LocalMcpCreateStrategy` 等具体策略类。
    - 工厂类 `DefaultMcpClientFactory` 根据配置自动分发请求到对应的策略实现，从而实现了代码的 **开闭原则（Open/Closed Principle）**——新增一种协议只需增加一个策略类，无需修改原有逻辑。

#### 12. 针对智能体服务的异常处理，项目采用了怎样的分层处理策略？如果 Netty 服务端突然宕机，如何保证 Agent 任务的一致性？
**参考答案：**
- **分层异常处理**：
    - **Trigger 层**：`AgentServiceController` 使用 `try-catch` 全局捕获异常，并封装为统一的 `Response<T>` 对象（包含错误码和提示信息），确保前端总是收到合法的 JSON 响应。
    - **Service 层**：业务逻辑中抛出自定义 `AppException`（如 `E0001` 智能体不存在），由上层统一处理，避免将底层堆栈信息直接暴露给用户。
- **宕机恢复方案（进阶）**：
    - **现状**：目前架构中 `CompletableFuture` 存储在内存中，宕机会导致任务丢失。
    - **优化思路**：引入 **持久化状态机（State Machine）**。在下发指令前，将 Task 状态（如 `PENDING_SCREENSHOT`）写入 Redis 或数据库。服务重启后，通过 Session ID 恢复上下文，或者手机端实现 **断线重连（Heartbeat）** 机制，重连后主动上报当前状态，Agent 根据最新截图重新规划后续步骤。

---

### AI Agent 核心八股文 (概念与原理)

#### 13. 什么是 AI Agent（智能体）？它与传统的 LLM 应用（如 ChatGPT）有什么本质区别？
**参考答案：**
- **AI Agent 定义**：AI Agent 是一个能够感知环境、进行推理规划、主动调用工具并采取行动以实现目标的智能系统。它具备 **感知（Perception）**、**大脑（Brain/LLM）**、**规划（Planning）** 和 **行动（Action/Tools）** 四大核心组件。
- **与传统 LLM 区别**：
    - **被动 vs 主动**：ChatGPT 等 LLM 应用通常是 **被动响应** 用户输入的（Input -> Output），无状态且单次交互。而 AI Agent 具备 **主观能动性**，它能将复杂目标拆解为一系列子任务，并主动调用工具（如搜索、API、代码执行）来获取信息或改变环境状态。
    - **工具使用能力**：传统 LLM 仅依赖训练数据（内部知识），存在幻觉且无法获取实时信息。Agent 通过 **Function Calling** 或 **MCP** 协议连接外部世界（Google、数据库、API），极大地扩展了能力边界。
    - **循环迭代**：Agent 通常采用 **ReAct (Reasoning + Acting)** 范式，即“思考 -> 行动 -> 观察结果 -> 再思考”，形成一个闭环，直到目标达成。

#### 14. 什么是 ReAct 范式？它是如何让 Agent 具备推理能力的？
**参考答案：**
- **概念**：ReAct 是 **Reasoning（推理）** 和 **Acting（行动）** 的组合。它是一种 Prompt Engineering 技术，要求 LLM 在执行具体动作前，先生成一段“思维链（Thought）”。
- **工作流程**：
    1.  **Thought（思考）**：LLM 分析当前任务，决定下一步该做什么（例如：“我需要先搜索一下今天的日期”）。
    2.  **Action（行动）**：LLM 生成调用工具的指令（例如：`SearchTool.search("current date")`）。
    3.  **Observation（观察）**：工具执行并返回结果（例如：“2023-10-27”）。
    4.  **Repeat（循环）**：LLM 根据观察结果进行下一轮思考，直到得出最终答案（Final Answer）。
- **优势**：相比直接生成答案（Zero-shot），ReAct 显著减少了幻觉，增强了解决复杂多步问题的能力，并提供了可解释的推理过程。

#### 15. 请解释 RAG（检索增强生成）与 Fine-tuning（微调）的区别及各自适用场景。
**参考答案：**
- **RAG (Retrieval-Augmented Generation)**：
    - **原理**：类似于“开卷考试”。在 LLM 生成答案前，先从外部知识库（向量数据库）中检索相关文档片段，作为上下文（Context）拼接到 Prompt 中喂给 LLM。
    - **适用场景**：需要**实时更新知识**（如新闻）、**私有数据查询**（如企业文档）、**降低成本**（无需训练模型）的场景。
    - **优缺点**：成本低、无遗忘问题，但受限于检索精度和 Context Window 长度。
- **Fine-tuning (微调)**：
    - **原理**：类似于“复习内化”。使用特定领域的数据集对预训练模型进行进一步训练，调整模型参数，使其掌握特定领域的知识或风格。
    - **适用场景**：需要**特定格式输出**（如代码生成、JSON提取）、**特定领域深度理解**（如医疗诊断）、**降低延迟**（无需检索）的场景。
    - **优缺点**：效果好、响应快，但成本高、知识更新困难（需重新训练）。

#### 16. 什么是向量数据库（Vector Database）？它在 AI Agent 中起什么作用？
**参考答案：**
- **定义**：专门用于存储和检索高维向量（Vector / Embedding）的数据库。它支持 **近似最近邻搜索（ANN）**，能快速找到与查询向量距离最近的数据。
- **Embedding（嵌入）**：将文本、图片、音频等非结构化数据转化为数字向量的过程。语义相似的内容，其向量在空间中的距离更近（如 Cosine Similarity）。
- **在 Agent 中的作用**：
    - **长期记忆（Long-term Memory）**：Agent 可以将对话历史、用户偏好存储在向量库中，实现跨会话记忆。
    - **知识库检索（Knowledge Base）**：存储海量文档片段，供 RAG 检索使用，弥补 LLM 训练数据的滞后性。

#### 17. 什么是 Chain of Thought (CoT)？它如何提升 LLM 的推理能力？
**参考答案：**
- **概念**：思维链（Chain of Thought）是一种通过引导 LLM 生成**中间推理步骤**来解决复杂问题的技术。
- **原理**：对于数学题或逻辑推理题，如果直接问答案，LLM 容易出错。但如果提示它“**Let's think step by step（让我们一步步思考）**”，或者在 Few-shot 示例中展示推理过程，LLM 就会模仿这种思维方式，将大问题拆解为小问题逐个击破。
- **类型**：
    - **Zero-Shot CoT**：仅添加提示词 "Let's think step by step"。
    - **Few-Shot CoT**：在 Prompt 中提供包含推理步骤的示例（<Q, A_steps>）。
- **价值**：显著提升了 LLM 在算术、常识推理和符号推理任务上的准确率，是 Agent 实现复杂规划的基础。

#### 18. 什么是 MCP (Model Context Protocol)？为什么它对 Agent 生态很重要？
**参考答案：**
- **定义**：MCP 是一个开放标准协议，用于标准化 AI 模型与外部数据/工具的连接方式。它定义了统一的接口规范，使得工具（Tools）、资源（Resources）和提示（Prompts）可以跨平台、跨模型复用。
- **核心价值**：
    - **去碎片化**：解决了每个 AI 应用都需要为 Google Drive、Slack、GitHub 等写独立连接器（Connector）的问题。MCP 提供了统一的“插座”。
    - **即插即用**：开发者只需编写一次 MCP Server，任何支持 MCP 的 Client（如 Claude Desktop、Cursor、IDEA）都可以直接使用该工具。
    - **安全性**：通过标准化的鉴权机制（如 SSE + Token）管理数据访问权限。
