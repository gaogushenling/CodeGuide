---
title: a2a
lock: need
---

# A2A，实际跑起来是什么样？

作者：小傅哥
<br/>博客：[https://bugstack.cn](https://bugstack.cn)

> 沉淀、分享、成长，让自己和他人都能有所收获！😄

chatgpt（22年）-> LLM 进阶（23年）->  MCP 协议（24年）-> Skils 技能（25年）-> A2A 标准（25年），这几年 AI 发展的非常迅速，定义了协议，开发了组件，发布了产品。每个阶段，都有非常牛皮的代表性的内容，车速非常快🚌，不知道在坐的各位有没有掉队。

<div align="center">
    <img src="https://bugstack.cn/images/roadmap/tutorial/road-map-a2a-01.gif" width="150px">
</div>

针对这些 LLM 大模型的相关知识，小傅哥也分别提供了相关实战类项目，包括；**AI 问答助手（23年）**、**OpenAi(ChatGPT/ChatGLM) 微服务应用体系构（23年）**、**OpenAI 代码自动评审组件（24年）**、**AI Agent 智能体 - 拖拉拽（25年）**、**AI MCP Gateway 网关服务系统（25年）**、**AI Agent 脚手架 + 场景应用（26年）**，通过这些实战项目，实践各类标准协议和技术组件（spring ai、google adk...）的使用，以及提供非常出色的解决方案。

因为后续的 ai agent 智能体项目，还会涉及到 a2a 协议，所以先给大家做个相关技术的使用方便大家快速实践理解。

>🧧 文末提供了20个实战项目（6个AI、5个业务、8个组件、1套源码），以及各类编程技术小册等。欢迎一起加入学习。

## 一、A2A 是什么？

A2A (Agent2Agent) 协议是 Google于2025年4月推出、并由 Linux基金会托管的开源开放标准。它作为AI智能体之间的“通用语言”，旨在实现不同框架、不同厂商构建的智能体（Agent）间跨平台发现、通信与协作。

随后25年底，Google 发布了 [a2a adk](https://central.sonatype.com/artifact/com.google.adk/google-adk-a2a/0.4.0) 组件（迭代速度很快）。之后借助代理开发工具包 (Google ADK)，我们可以构建复杂的多代理系统，其中不同的代理需要使用代理对代理 (A2A) 协议进行协作和交互！本节提供了一个全面的指南，指导您构建强大的多代理系统，使代理能够安全高效地进行通信和协作。

框架：[https://google.github.io/adk-docs/a2a/](https://google.github.io/adk-docs/a2a/)

源码：[https://github.com/google/adk-java](https://github.com/google/adk-java)

资料：[https://www.ibm.com/cn-zh/think/topics/agent2agent-protocol](https://www.ibm.com/cn-zh/think/topics/agent2agent-protocol)

文档：[https://a2aprotocol.ai/docs/](https://a2aprotocol.ai/docs/)

---

如图，整套智能体架构（含A2A）；

<div align="center">
    <img src="https://bugstack.cn/images/article/project/ai-agent-scaffold/part-1/1-1/images/ai-agent-scaffold-1-1-02.png" width="950px">
</div>

- 左侧，是 LLM 模型智能体构建，基于 Spring AI 框架实现。这部分包括，AiApi 使用、RAG、MCP、Skills 的组合构建。
- 右侧，是 AI Agent 智能体编排，基于 Google ADK 框架实现。这套框架，提供了智能体工作流组装，插件回调钩子等各项基于 Google 发布的协议进行构建的。
- 之后，右上方，是 Google ADK 26年基于 A2A 协议实现的框架组件，方便我们设计出远程的 A2A 服务对接，把远程服务，转换为本地功能组件，编排进智能体中。因此 A2A 协议的作用，就是让一个远程的智能体，可以像构建本地智能体一样，连接起来进行使用。

> 基于 a2a  的协议，也有很多三方框架，但我们需要的是一个整体的解决方案，单一一个功能，还不能解决所有问题。所以这里优先选择 google adk 框架。

## 二、实践案例

### 1. 编程环境

- jdk 17
- google adk 0.8
- spring ai 1.1.0-M3

>相关的版本包，已经在测试工程中的 pom 里引入了。可以打开工程查看。

### 2. 工程结构

<div align="center">
    <img src="https://bugstack.cn/images/roadmap/tutorial/road-map-a2a-02.png" width="550px">
</div>

- 工程：[https://github.com/fuzhengwei/xfg-dev-tech-google-adk-a2a-server](https://github.com/fuzhengwei/xfg-dev-tech-google-adk-a2a-server)
- 说明：基于 Google ADK 框架，构建 A2A 服务端和客户端。注意，服务端的启动方式为 `quarkus.sh` 方式启动服务，之后使用客户端连接。
- 注意：这部分还有一些关于关于 Spring AI + Google ADK 的基础使用知识，是在 ApiTest 中有案例。也可以学习项目 [《AI Agent 脚手架 + 场景应用》](https://bugstack.cn/md/project/ai-agent-scaffold/ai-agent-scaffold.html)

### 3. 测试案例

```java
public class ApiTest {

    public static void main(String[] args) throws Exception {
        OpenAiApi openAiApi = OpenAiApi.builder()
                .baseUrl("https://apis.****.cn")
                .apiKey("sk-tIYdEUUnMqKX3bRf756a31449a4942***需要配置你的key")
                .completionsPath("v1/chat/completions")
                .embeddingsPath("v1/embeddings")
                .build();

        ChatModel chatModel = OpenAiChatModel.builder()
                .openAiApi(openAiApi)
                .defaultOptions(OpenAiChatOptions.builder()
                        .model("gpt-4o")
                        .build())
                .build();

        // agent 测试
        LlmAgent agent = LlmAgent.builder()
                .name("test")
                .description("Chess coach agent")
                .model(new SpringAI(chatModel))
                .instruction("""
                        You are a knowledgeable chess coach
                        who helps chess players train and sharpen their chess skills.
                        """)
                .build();

        InMemoryRunner runner = new InMemoryRunner(agent);

        Session session = runner
                .sessionService()
                .createSession("test", "fzw")
                .blockingGet();

        Flowable<Event> events = runner.runAsync("fzw", session.id(),
                Content.fromParts(Part.fromText("1+1")));

        System.out.print("\nAgent > ");
        events.blockingForEach(event -> System.out.println(event.stringifyContent()));
    }

}
```

- 这是一个 Spring AI + Google ADK 构建的简单智能体，由 LlmAgent 构建时候，创建模型 `new SpringAI(chatModel)` 关联到 Spring AI 框架。
- 之后，由 Google ADK 构建的智能体，使用内存记忆，创建会话之后进行测试。也可以学习项目 [《AI Agent 脚手架 + 场景应用》](https://bugstack.cn/md/project/ai-agent-scaffold/ai-agent-scaffold.html) 锻炼使用相关内容。

### 4. A2A 测试

#### 4.1 服务端

这部分内容的学习，可以打开案例代码，方便对比。

##### 4.1.1 服务提供

```java
@ApplicationScoped
public class AgentExecutorProducer {

    @ConfigProperty(name = "my.adk.app.name", defaultValue = "default-app")
    String appName;

    @Produces
    public AgentExecutor agentExecutor() {
        return new com.google.adk.a2a.executor.AgentExecutor.Builder()
                .agent(Agent.ROOT_AGENT)
                .appName(appName)
                .sessionService(new InMemorySessionService())
                .artifactService(new InMemoryArtifactService())
                .agentExecutorConfig(AgentExecutorConfig.builder().build())
                .build();
    }
    
}
```

- 这部分是把智能体提供出去，通过 google adk 框架，创建 AgentExecutor 实例。
- 之后 Agent.ROOT_AGENT 类似于上面的测试案例，智能体构建的部分。你可以创建任何之后通过 AgentExecutor 发布出去。

##### 4.1.2 卡片提供

```java
@ApplicationScoped
public class AgentCardProducer {

    @Produces
    @PublicAgentCard
    public AgentCard agentCard() {
        try (InputStream is = getClass().getResourceAsStream("/agent/agent.json")) {
            if (is == null) {
                throw new RuntimeException("agent.json not found in resources");
            }

            // Read the JSON file content
            String json = new String(is.readAllBytes(), StandardCharsets.UTF_8);

            // Use the SDK's built-in mapper to convert JSON string to AgentCard record
            return Utils.OBJECT_MAPPER.readValue(json, AgentCard.class);

        } catch (Exception e) {
            throw new RuntimeException("Failed to load AgentCard from JSON", e);
        }
    }

}
```

**/agent/agent.json**

```java
{
  "capabilities": {"streaming": true},
  "defaultInputModes": ["text/plain"],
  "defaultOutputModes": ["application/json"],
  "description": "一个专门检查数字是否为素数的智能体。它可以高效地确定单个数字或数字列表的素性。",
  "name": "check_prime_agent",
  "skills": [
    {
      "id": "prime_checking",
      "name": "Prime Number Checking",
      "description": "使用高效的数学算法检查列表中的数字是否为素数",
      "tags": ["mathematical", "computation", "prime", "numbers"]
    }
  ],
  "preferredTransport": "JSONRPC",
  "url": "http://localhost:9090",
  "version": "1.0.0"
}

```

- 这里要构建一个智能体卡，A2A 的协议中，把服务包装成一个卡片的概念。
- agent.json 配置的是 `Agent.ROOT_AGENT` 智能体的信息。
- 如果你之前学习过小傅哥的 AI MCP 网关项目，会对 JSONRPC 有印象， MCP 协议和 A2A 协议，都是走到 JSONRPC 标准进行的通信。

#### 4.2 客户端

##### 4.2.1 构建端

```java
public final class A2AAgent {

    private static final Random RANDOM = new Random();

    private static final OpenAiApi openAiApi = OpenAiApi.builder()
            .baseUrl("https://apis.****.cn")
            .apiKey("sk-tIYdEUUnMqKX3bRf756a31449a4942***需要配置你的key")
            .completionsPath("v1/chat/completions")
            .embeddingsPath("v1/embeddings")
            .build();

    private static final ChatModel chatModel = OpenAiChatModel.builder()
            .openAiApi(openAiApi)
            .defaultOptions(OpenAiChatOptions.builder()
                    .model("gpt-4.1")
                    .build())
            .build();

    @SuppressWarnings("unchecked")
    public static ImmutableMap<String, Object> rollDie(int sides, ToolContext toolContext) {
        ArrayList<Integer> rolls =
                (ArrayList<Integer>) toolContext.state().computeIfAbsent("rolls", k -> new ArrayList<>());
        int result = RANDOM.nextInt(Math.max(sides, 1)) + 1;
        rolls.add(result);
        return ImmutableMap.of("result", result);
    }

    public static final LlmAgent ROLL_AGENT =
            LlmAgent.builder()
                    .name("roll_agent")
                    .model(new SpringAI(chatModel))
                    .description("处理不同面数骰子的投掷。")
                    .instruction(
                            """
                                      当被要求掷骰子时，始终调用 roll_die 工具并指定面数（如果未指定，默认为 6）。不要编造结果。
                                    """)
                    .tools(ImmutableList.of(FunctionTool.create(A2AAgent.class, "rollDie")))
                    .build();

    public static LlmAgent createRootAgent(String primeAgentBaseUrl) {
        // 远程 agent
        BaseAgent primeAgent = createRemoteAgent(primeAgentBaseUrl);

        // 本地 agent
        return LlmAgent.builder()
                .name("root_agent")
                .model(new SpringAI(chatModel))
                .instruction(
                        """
                                  你可以在本地掷骰子，并将素数检查委托给远程的 prime_agent。
                                  1. 当用户要求掷骰子时，将请求路由给 roll_agent。
                                  2. 当用户要求检查素数时，委托给 prime_agent。
                                  3. 如果用户要求先掷骰子然后检查，先调用 roll_agent，然后将结果传给 prime_agent。
                                  在讨论素数之前，始终先简述骰子结果。
                                """)
                .subAgents(ImmutableList.of(ROLL_AGENT, primeAgent))
                .build();
    }

    private static BaseAgent createRemoteAgent(String primeAgentBaseUrl) {

        String agentCardUrl = primeAgentBaseUrl + "/.well-known/agent-card.json";
        AgentCard publicAgentCard =
                new A2ACardResolver(new JdkA2AHttpClient(), primeAgentBaseUrl, agentCardUrl).getAgentCard();

        Client a2aClient =
                Client.builder(publicAgentCard)
                        .withTransport(JSONRPCTransport.class, new JSONRPCTransportConfig())
                        .clientConfig(
                                new ClientConfig.Builder()
                                        .setStreaming(publicAgentCard.capabilities().streaming())
                                        .build())
                        .build();

        return RemoteA2AAgent.builder()
                .name(publicAgentCard.name())
                .a2aClient(a2aClient)
                .agentCard(publicAgentCard)
                .build();
    }

}
```

- createRootAgent 是构建入口，一个是创建 createRemoteAgent 远程智能体，一个是 `LlmAgent.builder()` 构建本地智能体。之后在构建本地智能体的时候，通过 subAgents 把远程智能体填充到本地的智能体里去了。这个编排的方式有多种多样的。
- createRemoteAgent 远程构建，这是固定协议路径 `/.well-known/agent-card.json`拿到智能体卡片以后（一个卡片上有各类的信息），之后通过 a2aClient 创建客户端，在通过 RemoteA2AAgent 完成本地智能体的转换。

##### 4.2.2 使用端

```java
public final class A2AAgentRun {
    private final String userId;
    private final String sessionId;
    private final Runner runner;

    public A2AAgentRun(BaseAgent agent) {
        this.userId = "test_user";
        String appName = "A2AAgentApp";
        this.sessionId = UUID.randomUUID().toString();

        InMemoryArtifactService artifactService = new InMemoryArtifactService();
        InMemorySessionService sessionService = new InMemorySessionService();
        this.runner =
                new Runner(agent, appName, artifactService, sessionService, /* memoryService= */ null);

        ConcurrentMap<String, Object> initialState = new ConcurrentHashMap<>();
        var unused =
                sessionService.createSession(appName, userId, initialState, sessionId).blockingGet();
    }
    
    // ... 省略部分

    public static void main(String[] args) throws InterruptedException {
        BaseAgent agent = A2AAgent.createRootAgent("http://localhost:9090");
        A2AAgentRun a2aRun = new A2AAgentRun(agent);

        List<Event> events =
                a2aRun.run("掷一个6面的骰子。").toList().timeout(90, TimeUnit.SECONDS).blockingGet();

        events.forEach(A2AAgentRun::printOutEvent);

        events =
                a2aRun.run("这是素数吗？").toList().timeout(90, TimeUnit.SECONDS).blockingGet();

        events.forEach(A2AAgentRun::printOutEvent);
    }

}
```

- A2AAgentRun 测试入口，连接远程的智能体，之后做相关的调用验证。

## 三、测试验证

### 1. 前置准备

1. IntelliJ IDEA 右侧的 maven 点击执行 clean -> install 构建
2. 通过命令启动服务，`mvn quarkus:dev -pl xfg-dev-tech-app`

### 2. 访问服务

#### 2.1 服务首页

<div align="center">
    <img src="https://bugstack.cn/images/roadmap/tutorial/road-map-a2a-03.png" width="650px">
</div>

- 地址：[http://localhost:9090/q/dev-ui/welcome](http://localhost:9090/q/dev-ui/welcome)
- 说明：访问首页，localhost:9090 会看到上面的地址信息，这个是 a2a 协议的入口。

#### 2.2 服务协议

<div align="center">
    <img src="https://bugstack.cn/images/roadmap/tutorial/road-map-a2a-04.png" width="650px">
</div>

- 地址：[http://localhost:9090/.well-known/agent-card.json](http://localhost:9090/.well-known/agent-card.json)
- 说明：点击 agent-card.json 可以看到具体的服务协议信息。

### 3. 调用验证

<div align="center">
    <img src="https://bugstack.cn/images/roadmap/tutorial/road-map-a2a-05.png" width="850px">
</div>

- 点击运行，你可以看到它在进行多个智能体的调用（可能模型原因不准，但核心点在于多个智能体的调用）。
- 好啦，到这关于 A2A 整个内容就演示完了，可以时刻关注 google adk a2a 协议的迭代，这部分内容后续还会有一些调整。

