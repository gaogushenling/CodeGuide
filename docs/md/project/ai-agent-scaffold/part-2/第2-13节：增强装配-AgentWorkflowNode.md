---
title: 【更】第2-13：增强装配-AgentWorkflowNode
pay: https://t.zsxq.com/qjhUb
---

# 《AI Agent 脚手架》第2-13：增强装配-AgentWorkflowNode

作者：小傅哥
<br/>博客：[https://bugstack.cn](https://bugstack.cn)
<br/>视频：[https://t.zsxq.com/AuQlk](https://t.zsxq.com/AuQlk)

> 沉淀、分享、成长，让自己和他人都能有所收获！😄

## 一、本章诉求

换种设计方式，增强 AgentWorkflowNode 流转能力，让 LoopAgentNode、ParallelAgentNode、SequentialAgentNode 不在负责判断流转，而是每个流程处理完毕后，都回到 AgentWorkflowNode 中进行流转决策。这样我们就可以组合出更为复杂的智能体编排。

## 二、流程设计

如图，增强 AgentWorkflowNode 流转能力，每个节点流转完都重新回到 AgentWorkflowNode 节点进行决策；

<div align="center">
	<img src="https://bugstack.cn/images/article/project/ai-agent-scaffold/part-2/2-13/images/ai-agent-scaffold-2-13-01.png" width="800px"/>
</div>

- 左侧是旧版流程，LoopAgentNode、ParallelAgentNode、SequentialAgentNode，每个节点交叉流转。这次换到新版流程，所有的流转都由 AgentWorkflowNode 负责。这样会让三个功能 Agent 节点的职责更为清晰。
- 这样，AgentWorkflowNode 就成了分发中心，三个 LoopAgentNode、ParallelAgentNode、SequentialAgentNode 智能体节点处理完业务后都回到 AgentWorkflowNode 即可。

## 三、功能实现

### 1. 工程结构

<div align="center">
	<img src="https://bugstack.cn/images/article/project/ai-agent-scaffold/part-2/2-13/images/ai-agent-scaffold-2-13-02.png" width="350px"/>
</div>

- 修改 LoopAgentNode、ParallelAgentNode、SequentialAgentNode，三个节点中的流转操作，都转移到 AgentWorkflowNode 处理。
- 在 AgentWorkflowNode 中，要拿到当前 agentWorkflows 配置的列表中，步骤中第N个，把拿到的值作为当前的信息存储到上下文，之后流转到任何一个节点，只负责从上下文取到当前值即可。

### 2. 核心模块

#### 2.1 定义上下文

```java
@Data
@Builder
@AllArgsConstructor
@NoArgsConstructor
public static class DynamicContext {

    /**
     * LLM API
     */
    private OpenAiApi openAiApi;

    /**
     * 对话模型
     */
    private ChatModel chatModel;

    /**
     * 原子安全的递进步骤
     */
    private AtomicInteger currentStepIndex = new AtomicInteger(0);

    /**
     * 当前的智能体
     */
    private AiAgentConfigTableVO.Module.AgentWorkflow currentAgentWorkflow;

    /**
     * 智能体组
     */
    private Map<String, BaseAgent> agentGroup = new HashMap<>();

    private Map<String, Object> dataObjects = new HashMap<>();
}   
```

- 首先，去掉 agentWorkflows 列表值，增加一个 currentAgentWorkflow 当前值。
- 之后，添加 currentStepIndex 步骤完成一个，则迭代+1，从 agentWorkflows 渠道的当前对象存储到 currentAgentWorkflow，这样会更加方便判断。（`这个就是前面提到的另外的一个方案设计，小傅哥在项目里也给大家增加这种演进的迭代设计，可以让大家多一些积累`）

#### 2.2 增强流转

```java
@Slf4j
@Service
public class AgentWorkflowNode extends AbstractArmorySupport {

    @Resource
    private LoopAgentNode loopAgentNode;

    @Resource
    private ParallelAgentNode parallelAgentNode;

    @Resource
    private SequentialAgentNode sequentialAgentNode;

    @Resource
    private RunnerNode runnerNode;

    @Override
    protected AiAgentRegisterVO doApply(ArmoryCommandEntity requestParameter, DefaultArmoryFactory.DynamicContext dynamicContext) throws Exception {
        log.info("Ai Agent 装配操作 - AgentWorkflowNode");

        AiAgentConfigTableVO aiAgentConfigTableVO = requestParameter.getAiAgentConfigTableVO();
        List<AiAgentConfigTableVO.Module.AgentWorkflow> agentWorkflows = aiAgentConfigTableVO.getModule().getAgentWorkflows();

        // 如果未配置 agentWorkflows 则直接流转到 RunnerNode
        if (null == agentWorkflows || agentWorkflows.isEmpty() || dynamicContext.getCurrentStepIndex() >= agentWorkflows.size()) {
            // 设置结果值
            dynamicContext.setCurrentAgentWorkflow(null);
            // 路由下节点
            return router(requestParameter, dynamicContext);
        }

        // 设置当前判断流程对象
        dynamicContext.setCurrentAgentWorkflow(agentWorkflows.get(dynamicContext.getCurrentStepIndex()));

        // 步骤值增加
        dynamicContext.addCurrentStepIndex();

        return router(requestParameter, dynamicContext);
    }

    @Override
    public StrategyHandler<ArmoryCommandEntity, DefaultArmoryFactory.DynamicContext, AiAgentRegisterVO> get(ArmoryCommandEntity requestParameter, DefaultArmoryFactory.DynamicContext dynamicContext) throws Exception {

        AiAgentConfigTableVO.Module.AgentWorkflow currentAgentWorkflow = dynamicContext.getCurrentAgentWorkflow();

        // 没有下一个节点，流转到结束节点
        if (null == currentAgentWorkflow) {
            return runnerNode;
        }

        String type = currentAgentWorkflow.getType();
        AgentTypeEnum agentTypeEnum = AgentTypeEnum.fromType(type);

        if (null == agentTypeEnum) {
            throw new RuntimeException("agentWorkflow type is error!");
        }

        String node = agentTypeEnum.getNode();

        return switch (node) {
            case "loopAgentNode" -> loopAgentNode;
            case "parallelAgentNode" -> parallelAgentNode;
            case "sequentialAgentNode" -> sequentialAgentNode;
            default -> runnerNode;
        };

    }

}
```

- doApply 方法的核心是判断是否配置 agentWorkflows，以及不断的取值（类似for循环），是否取到了最后一个。如果是，则设置 `dynamicContext.setCurrentAgentWorkflow(null);` 并路由走。否则，从 agentWorkflows 获取当前步骤的对象并设置到上下文中，以及给步骤 +1 处理。
- get 则负责节点流转，判断当前节点是否为null，为null则表示没有要处理的节点，直接进入 runnerNode 即可。如果不是 null 则按照不同的 node 流转到子 agent 智能体节点。

#### 2.3 子智能体节点

##### 2.3.1 LoopAgentNode

```java
@Service
public class LoopAgentNode extends AbstractArmorySupport {

    @Override
    protected AiAgentRegisterVO doApply(ArmoryCommandEntity requestParameter, DefaultArmoryFactory.DynamicContext dynamicContext) throws Exception {
        log.info("Ai Agent 装配操作 - LoopAgentNode");

        AiAgentConfigTableVO.Module.AgentWorkflow currentAgentWorkflow = dynamicContext.getCurrentAgentWorkflow();

        List<BaseAgent> subAgents = dynamicContext.queryAgentList(currentAgentWorkflow.getSubAgents());

        LoopAgent loopAgent =
                LoopAgent.builder()
                        .name(currentAgentWorkflow.getName())
                        .description(currentAgentWorkflow.getDescription())
                        .subAgents(subAgents)
                        .maxIterations(currentAgentWorkflow.getMaxIterations())
                        .build();

        dynamicContext.getAgentGroup().put(currentAgentWorkflow.getName(), loopAgent);

        return router(requestParameter, dynamicContext);
    }

    @Override
    public StrategyHandler<ArmoryCommandEntity, DefaultArmoryFactory.DynamicContext, AiAgentRegisterVO> get(ArmoryCommandEntity requestParameter, DefaultArmoryFactory.DynamicContext dynamicContext) throws Exception {
        return getBean("agentWorkflowNode");
    }

}
```

- doApply 要修改为从上下文的 `dynamicContext.getCurrentAgentWorkflow()` 获取当前节点的数据，构建 Agent 之后路由。
- get 则负责流转回 `getBean("agentWorkflowNode")` 让 agentWorkflowNode 继续负责节点的流转判断。

##### 2.3.2 ParallelAgentNode

```java
@Service
public class ParallelAgentNode extends AbstractArmorySupport {

    @Override
    protected AiAgentRegisterVO doApply(ArmoryCommandEntity requestParameter, DefaultArmoryFactory.DynamicContext dynamicContext) throws Exception {
        log.info("Ai Agent 装配操作 - ParallelAgentNode");

        AiAgentConfigTableVO.Module.AgentWorkflow currentAgentWorkflow = dynamicContext.getCurrentAgentWorkflow();

        List<BaseAgent> subAgents = dynamicContext.queryAgentList(currentAgentWorkflow.getSubAgents());

        ParallelAgent parallelAgent =
                ParallelAgent.builder()
                        .name(currentAgentWorkflow.getName())
                        .subAgents(subAgents)
                        .description(currentAgentWorkflow.getDescription())
                        .build();

        dynamicContext.getAgentGroup().put(currentAgentWorkflow.getName(), parallelAgent);

        return router(requestParameter, dynamicContext);
    }

    @Override
    public StrategyHandler<ArmoryCommandEntity, DefaultArmoryFactory.DynamicContext, AiAgentRegisterVO> get(ArmoryCommandEntity requestParameter, DefaultArmoryFactory.DynamicContext dynamicContext) throws Exception {
        return getBean("agentWorkflowNode");
    }
}
```

- 代码修改方式同 `LoopAgentNode`

##### 2.3.3 SequentialAgentNode

```java
@Service
public class SequentialAgentNode extends AbstractArmorySupport {

    @Override
    protected AiAgentRegisterVO doApply(ArmoryCommandEntity requestParameter, DefaultArmoryFactory.DynamicContext dynamicContext) throws Exception {
        log.info("Ai Agent 装配操作 - SequentialAgentNode");

        AiAgentConfigTableVO.Module.AgentWorkflow currentAgentWorkflow = dynamicContext.getCurrentAgentWorkflow();

        List<BaseAgent> subAgents = dynamicContext.queryAgentList(currentAgentWorkflow.getSubAgents());

        SequentialAgent sequentialAgent =
                SequentialAgent.builder()
                        .name(currentAgentWorkflow.getName())
                        .description(currentAgentWorkflow.getDescription())
                        .subAgents(subAgents)
                        .build();

        dynamicContext.getAgentGroup().put(currentAgentWorkflow.getName(), sequentialAgent);

        return router(requestParameter, dynamicContext);
    }

    @Override
    public StrategyHandler<ArmoryCommandEntity, DefaultArmoryFactory.DynamicContext, AiAgentRegisterVO> get(ArmoryCommandEntity requestParameter, DefaultArmoryFactory.DynamicContext dynamicContext) throws Exception {
        return getBean("agentWorkflowNode");
    }

}
```

- 代码修改方式同 `LoopAgentNode`

## 四、测试验证

### 1. 修改配置文件

**parallel_research_app.yml**

```java
ai:
  agent:
    config:
      tables:
        testAgent02:
          app-name: ResearchAndSynthesisPipeline
          agent:
            agent-id: 100002
            agent-name: 测试智能体02
            agent-desc: 并行研究并汇总的智能体管道
          module:
            ai-api:
              base-url: https://apis.itedus.cn
              api-key: sk-Sp2jx3yeq7x7HJ663bDc9bF0D34b4f609f833840271519B1
              completions-path: v1/chat/completions
              embeddings-path: v1/embeddings
            chat-model:
              model: gpt-4.1
              tool-mcp-list:
                - sse:
                    name: baidu-search
                    base-uri: https://appbuilder.baidu.com/v2/ai_search/mcp/
                    sse-endpoint: sse?api_key=bce-v3/ALTAK-3zODLb9qHozIftQlGwez5/2696e92781f5bf1ba1870e2958f239fd6dc822a4
                    request-timeout: 5000
            agents:
              - name: RenewableEnergyResearcher
                description: Researches renewable energy sources.
                instruction: |
                  You are an AI Research Assistant specializing in energy.
                  Research the latest advancements in 'renewable energy sources'.
                  Use the Google Search tool provided.
                  Summarize your key findings concisely (1-2 sentences).
                  Output *only* the summary.
                output-key: renewable_energy_result
              - name: EVResearcher
                description: Researches electric vehicle technology.
                instruction: |
                  You are an AI Research Assistant specializing in transportation.
                  Research the latest developments in 'electric vehicle technology'.
                  Use the Google Search tool provided.
                  Summarize your key findings concisely (1-2 sentences).
                  Output *only* the summary.
                output-key: ev_technology_result
              - name: CarbonCaptureResearcher
                description: Researches carbon capture methods.
                instruction: |
                  You are an AI Research Assistant specializing in climate solutions.
                  Research the current state of 'carbon capture methods'.
                  Use the Google Search tool provided.
                  Summarize your key findings concisely (1-2 sentences).
                  Output *only* the summary.
                output-key: carbon_capture_result
              - name: SynthesisAgent
                description: Combines research findings into a structured report.
                instruction: |
                  You are an AI Assistant responsible for combining research findings into a structured report.
                  Your primary task is to synthesize the following research summaries, clearly attributing findings to their source areas. Structure your response using headings for each topic. Ensure the report is coherent and integrates the key points smoothly.
                  **Crucially: Your entire response MUST be grounded *exclusively* on the information provided in the 'Input Summaries' below. Do NOT add any external knowledge, facts, or details not present in these specific summaries.**
                  **Input Summaries:**

                  *   **Renewable Energy:**
                      {renewable_energy_result}

                  *   **Electric Vehicles:**
                      {ev_technology_result}

                  *   **Carbon Capture:**
                      {carbon_capture_result}

                  **Output Format:**

                  ## Summary of Recent Sustainable Technology Advancements

                  ### Renewable Energy Findings
                  (Based on RenewableEnergyResearcher's findings)
                  [Synthesize and elaborate *only* on the renewable energy input summary provided above.]

                  ### Electric Vehicle Findings
                  (Based on EVResearcher's findings)
                  [Synthesize and elaborate *only* on the EV input summary provided above.]

                  ### Carbon Capture Findings
                  (Based on CarbonCaptureResearcher's findings)
                  [Synthesize and elaborate *only* on the carbon capture input summary provided above.]

                  ### Overall Conclusion
                  [Provide a brief (1-2 sentence) concluding statement that connects *only* the findings presented above.]

                  Output *only* the structured report following this format. Do not include introductory or concluding phrases outside this structure, and strictly adhere to using only the provided input summary content.
            agent-workflows:
              - type: parallel
                name: ParallelWebResearchAgent
                description: Runs multiple research agents in parallel to gather information.
                sub-agents:
                  - RenewableEnergyResearcher
                  - EVResearcher
                  - CarbonCaptureResearcher
              - type: sequential
                name: ResearchAndSynthesisPipeline
                description: Coordinates parallel research and synthesizes the results.
                sub-agents:
                  - ParallelWebResearchAgent
                  - SynthesisAgent
            runner:
              agent-name: ResearchAndSynthesisPipeline
```

- agent-workflows 配置下 ParallelWebResearchAgent、ResearchAndSynthesisPipeline，这样可以测试循环处理。
- runner 则配置 ResearchAndSynthesisPipeline 进行运行体转配。

### 2. 测试方法

```java
@Test
public void test_handlerMessage_03(){
    AiAgentRegisterVO aiAgentRegisterVO = applicationContext.getBean("100002", AiAgentRegisterVO.class);
    String appName = aiAgentRegisterVO.getAppName();
    InMemoryRunner runner = aiAgentRegisterVO.getRunner();
    Session session = runner.sessionService()
            .createSession(appName, "xiaofuge")
            .blockingGet();
    Content userMsg = Content.fromParts(Part.fromText("你具备哪些能力"));
    Flowable<Event> events = runner.runAsync("xiaofuge", session.id(), userMsg);
    List<String> outputs = new ArrayList<>();
    events.blockingForEach(event -> outputs.add(event.stringifyContent()));
    log.info("测试结果:{}", JSON.toJSONString(outputs));
}
```

```java
26-01-01.13:20:04.106 [main            ] INFO  test_handlerMessage_03        - 测试结果:["我可以帮助你查询和分析可再生能源领域的最新进展，包括太阳能、风能、生物能、地热能、海洋能等各类新能源技术的发展趋势、创新成果及政策动态。同时，我可以利用互联网搜索功能，快速获取最新科研成果、行业动态和相关数据，并将关键信息进行简明总结。","我是专注于电动汽车技术（electric vehicle technology）研究的AI助理，具备以下能力：\n\n1. **新技术检索与总结**：我能利用Google搜索等工具，快速检索最新的电动汽车技术发展、行业动态和科研突破，并进行简洁明了的总结。\n2. **趋势与前沿分析**：能够获取并分析行业趋势，例如电池创新、驱动系统进展、智能网联、电驱动新材料等领域的最新动向。\n3. **政策与市场信息搜集**：可查询全球各地与电动汽车相关的政策、市场增长、补贴政策等信息。\n4. **参考文献和数据追溯**：能帮助定位权威期刊、会议论文、专利等技术文档，提供学术研究支持。\n5. **技术对比与评估**：可对比不同品牌、技术路径或产品，分析其优劣及市场应用前景。\n6. **简明交流和摘要能力**：围绕“电动汽车技术”，可将复杂技术信息压缩为1-2句话的核心摘要，便于快速理解。\n\n如果你有特定方向的需求（如电池、驱动控制、充电技术等），我也能定向进行最新信息搜索和研究。","我具备以下能力，专注于碳捕集（carbon capture）相关的研究与信息获取：\n\n1. 实时网络检索：我可以通过专业搜索工具实时获取最新关于碳捕集方法、技术进展、应用案例、政策法规等公开信息。\n2. 资料梳理与总结：对检索到的信息快速提炼要点，进行结构化、简明扼要的总结，便于决策与参考。\n3. 技术分类与比较：能够对比不同类型的碳捕集技术（如直接空气捕集、点源捕集、碳矿化、生物碳捕集等）的原理、优缺点和应用现状。\n4. 最新动态追踪：跟踪全球范围内碳捕集领域的最新动态、前沿研究和重大项目进展。\n5. FAQ解答：针对碳捕集相关的常见问题（如成本、能效、行业难点等）进行专业、准确回答。\n\n如需获取某一具体问题或领域的最新信息，请直接告诉我！","## Summary of Recent Sustainable Technology ...
```

- 运行后可以看到执行的结果。也表示了，我们的装配方式是没问题的。

## 五、读者作业

- 简单作业：完成本节功能的编写，理解此处的架构设计。对于节点的流转，打开思路，之后活学活用。
- 复杂作业：尝试配置一个多层嵌套的智能体，来验证这样的装配。

