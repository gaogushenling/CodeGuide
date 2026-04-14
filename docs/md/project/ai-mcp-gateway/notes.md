---
title: 面试：技能、简历、问题汇总
lock: no
---

# 《AI MCP Gateway 网关服务系统》，关于面试中的技能、简历、问题汇总

作者：小傅哥
<br/>博客：[https://bugstack.cn](https://bugstack.cn)
<br/>课程：[https://t.zsxq.com/SNsgH](https://t.zsxq.com/SNsgH)

>沉淀、分享、成长，让自己和他人都能有所收获！😄

## 一、项目介绍

面试官您好，本套 AI MCP GateWay 网关项目，对标阿里的 higress-ai，以通用方案解决各类业务接口便捷转换为 MCP 协议而设计实现。通过这样的配置，可以大大的简化从普通http、rpc接口到 MCP 协议的转换操作。

该项目采用 DDD 领域驱动架构设计，按照 MCP 协议 json-rpc2 标准，构建 AI MCP GateWay 能力服务。因而设计拆分领域模型为；session 域（会话、消息）、协议域（协议、存储）、网关域、鉴权域、LLM（模型测试网关）、管理域（一般公司的大型项目，会单独拆分这个领域为独立系统），来支撑整个服务实现，最终由 case 层编排逻辑，再给 trigger 接口层调用处理。

为什么自研？对企业来说，公司需要整合内部完整能力的统一 AI MCP 网关解决方案，随着自身的业务发展而不断迭代处理。在这个过程，就可以快速支撑业务诉求，也可以保证系统的安全和可靠性。如果只是引入外部的，那么可能顺带着要引入一大票的额外系统服务，在遇到一些场景诉求或者问题的时候，也很难做到快速处理。所以我们要自研来实现。另外，对个人来说，我们需要一个技术积累，而不是会用。

## 二、简历模板

**项目名称**：AI MCP Gateway 统一网关服务系统

**项目架构**：DDD 领域驱动设计（六边形架构）、JSON-RPC2 MCP 上下文协议、前后端分离

**核心技术**：SpringBoot 3.4、Spring WebFlux、Retrofit 2.9.0 & OkHttp 4.9.3、JDK 17+、MCP（JSON-RPC2）

**项目介绍**：本项目是 AI Agent 智能体，关于 MCP 协议对接的通用网关服务项目，以解决各类业务接口便捷转换为 MCP 协议而设计实现。通过这样的配置，可以大大的简化从普通http、rpc接口到 MCP 协议的转换操作。这样的项目，也是每个互联网公司在做 AI Agent 智能体时，必备的基础设施项目。

**核心职责**：

>简历的职责，是你需要通过不同方面的举证，表述出自己的能力储备。所以，以下是各个方面的描述案例，你可以按照此方式解决描述你的简历。

- 架构设计：
    - 以 DDD 领域驱动设计，四色建模分析领域模型，划分出；session 域（会话、消息）、协议域（协议、存储）、网关域、鉴权域、LLM（模型测试网关）、管理域。
    - 采用六边形架构解耦领域逻辑与基础设施，确保系统可扩展性和可维护性
    - 设计基于 Reactor 的响应式编程模型，实现高性能的 SSE (Server-Sent Events) 通信

- 设计模式：
    - 通过策略模式处理 MCP（JSON-RPC2）消息多场景类型的处理，包括；初始（Initialize）、资源（Resources）、工具（ToolsList）、调用（ToolsCall）的场景，有利于后续其他动作的扩展。
    - 使用组合模式（规则树）在 case 领域层，编排串联 domain 领域服务，让各类场景便于迭代和维护。

- 核心领域（不用都写）：
    - **Session 领域**：设计会话管理核心模型，包括 HandleMessageCommandEntity、SessionConfigVO 等实体，实现会话创建、消息处理、状态管理
    - **Gateway 领域**：构建网关配置模型，包括 GatewayConfigEntity、GatewayToolConfigEntity 等，支持动态网关配置和工具管理
    - **Protocol 领域**：设计 MCP 协议解析和封装机制，实现 JSON-RPC 消息的序列化和反序列化
    - **Admin 领域**：实现管理后台的领域逻辑，支持网关配置、认证管理等核心功能
    - **Domain 层**：定义核心领域接口和值对象，如 ISessionManagementService、IGatewayConfigService 等
    - **Case 层**：实现用例层逻辑，包括 IMcpSessionService、IMcpMessageService 等服务接口
    - **Trigger 层**：开发 HTTP 触发器，实现 MCP 网关的 RESTful API 接口
    - **Infrastructure 层**：构建基础设施适配器，包括数据库访问、Redis 缓存、网关适配器等

- 功能方案：
    - 基于 Spring WebFlux 和 Reactor 实现响应式编程，支持高并发 SSE 连接
    - 设计 MCP 协议解析器，实现 JSON-RPC 消息的标准化处理
    - 开发网关配置管理系统，支持动态配置更新和热部署
    - 实现会话管理机制，包括会话创建、消息处理、状态同步等功能
    - 设计基于 API Key 的认证机制，确保网关访问安全
    - 实现 Spring Security 集成，支持细粒度权限控制
    - 开发速率限制和会话过期机制，防止滥用和资源浪费