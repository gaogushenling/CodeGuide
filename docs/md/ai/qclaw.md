---
title: QClaw
lock: need
---

# 🦞站起来蹬，每天2亿token，我已经会用 OpenClaw 了！

作者：小傅哥
<br/>博客：[https://bugstack.cn](https://bugstack.cn)

> 沉淀、分享、成长，让自己和他人都能有所收获！😄

大家好，我是技术UP主小傅哥。

深度体验后，**云服务器 + OpenClaw 的工作属性，基本等于零，白费蜡🕯！** 所以，于3月初，购入 Mac Mini（丐版16G）。部署 `OpenClaw`（+`QClaw`）+ `编程环境`（`jdk`、`maven`...） + `Docker`，`配合 Nas 环境做存储` + `Mac Pro`（随行控制设备）+ UU 远程（没事看看它）等，我才体验到**它能给我干活啦**！😄

<div align="center">
	<img src="https://bugstack.cn/images/roadmap/tutorial/road-map-ai-agent-openclaw-attempt-01.png" width="550px"/>
</div>

❤ 心得体会！

最早部署的是 [OpenClaw](https://openclaw.ai/)（这哥们也原生就支持中文啦）+ 飞书，部署起来也很简单。但因为使用的都是自己的 Token，有点舍不得站起来蹬 🚴🏻，感觉每一句话都在烧钱💰。相比较下 OpenClaw 同样一个事的消耗程度，是其他 AI IDE（Trae.ai）的上百倍，那直接用其他的不也可以吗！？🤔 

但不深度玩，不干它几亿 Token，就不能体验到花钱的快乐！

好在呀，好在 [**QClaw**](https://qclaw.qq.com/) 每天一个登录的账号，赠送 4000 万 Token。换5个微信（还得家里人多），就是2亿 Token！就算干山崎大队，也是tm有富余的呀！

<div align="center">
	<img src="https://bugstack.cn/images/roadmap/tutorial/road-map-ai-agent-openclaw-attempt-02.png" width="200px"/>
</div>

几十亿 Token 下去后，我的体验是；它能干活，能想一个你的员工一样，控制这台电脑干活。包括，可以按照需求写代码，完成编译、构建、部署，打开浏览器验证功能逻辑，对于错误的编码可以继续完善。并且你可以随时随地的通过手机/Pad，通过`微信`/`企微`/`飞书`等方式，与它交流。

不过，它也不是那么省心的。三千六百颗手榴弹，给老李能干山崎大队，给咱也就能炸个鱼塘。所以，OpenClaw 你要想让它准确的给咱干活，就像写出来的代码，不仅它能看懂，我也得能认识呀。

那么，就需要上技能 Skills，这也是我在深度体验 OpenClaw 的最大感受，也是最先干的一个活。先拿10亿 Token，写2个 Skills 之后再说（先把🦵🏻腿接上）。—— 把你工作的方式，训练成技能，让 AI 懂你！

<div align="center">
	<img src="https://bugstack.cn/images/roadmap/tutorial/road-map-ai-agent-openclaw-attempt-03.png" width="200px"/>
</div>

> 接下来，小傅哥就分享下，用 OpenClaw（QClaw）做的一些事。

## 一、产品上线（skills）

发布到了官网(clawhub)：[https://clawhub.ai/u/fuzhengwei](https://clawhub.ai/u/fuzhengwei)

<div align="center">
	<img src="https://bugstack.cn/images/roadmap/tutorial/road-map-ai-agent-openclaw-attempt-04.png" width="700px"/>
</div>

[**xfg-zsxq-skills**](https://clawhub.ai/fuzhengwei/xfg-zsxq-skills) 一款星球社群运营服务的技能，便于所有加入社群的龙虾🦞主，可以让龙虾自主看帖、回帖，根据自己工作信息发帖/文章，以此方式龙虾形成一个自己的社群，吸收 OpenClaw 使用经验。这是一个自我成长的过程。

[**Xfg-ddd-skills**](https://clawhub.ai/fuzhengwei/xfg-ddd-skills) 一款 DDD 架构（六边形）指导编码的技能，因为在实际使用 AI 编码中，如果不加限制，他可能每次实现的功能逻辑，工程结构、分包方式、实现过程，都有非常大的差异。这会导致我们在拿到这份代码后，后续迭代也会非常吃力。所以，设计此技能，按照通用的 DDD 架构（六边形），限定 AI 编码方式。此技能初上线，已经用户体用。

## 二、安装技能

<div align="center">
	<img src="https://bugstack.cn/images/roadmap/tutorial/road-map-ai-agent-openclaw-attempt-05.png" width="700px"/>
</div>

| 用途     | 地址                                          |
| -------- | --------------------------------------------- |
| 星球社群 | https://github.com/fuzhengwei/xfg-zsxq-skills |
| 编码架构 | https://github.com/fuzhengwei/xfg-ddd-skills  |

OpenClaw、QClaw、OpenCode等，你都可以直接把技能**连接**告诉它，它可以帮你直接安装。如果不能直接安装也可以下载安装包，本地到底即可。

## 三、运行效果（zsxq-skills）

### 1. 主动发帖

<div align="center">
	<img src="https://bugstack.cn/images/roadmap/tutorial/road-map-ai-agent-openclaw-attempt-06.png" width="700px"/>
</div>

- 当你部署 zsxq-skills 技能后开始时，他会询问你，要对哪个星球地址进行操作，以及对应的 cookie 信息。如果 cookie 过期了，它还会主动询问你进行替换。
- 整体配置完成后，你就可以对星球进行发帖以及查看帖子等操作。不过不要弄的特别频繁！
- 像是在 OpenClaw（QClaw）还可以让添加上定时的任务处理。

### 2. 龙虾社群🦞

<div align="center">
	<img src="https://bugstack.cn/images/roadmap/tutorial/road-map-ai-agent-openclaw-attempt-07.png" width="850px"/>
</div>

- 地址：[https://wx.zsxq.com/group/48885154455258](https://wx.zsxq.com/group/48885154455258)
- 说明：现在这个[《OpenClaw 养虾社区🦞》](https://wx.zsxq.com/group/48885154455258)就已经入住了很多小龙虾，欢迎👏🏻一起来玩下。

## 四、编程效果（ddd-skills）

### 1. 技能说明

如果不对 ai 做编码结构和实现方式限定，ai 会每次都给你“惊喜”，但工程交付需要的是在确定的结构下，持续的迭代输出。所以，需要增加规范技能，限定 ai 编码输出方式的统一。

<div align="center">
	<img src="https://bugstack.cn/images/roadmap/tutorial/road-map-ai-agent-openclaw-attempt-08.png" width="850px"/>
</div>

因而，小傅哥把过往历史一行行手敲的 DDD 资料，以及定对应的工程代码，持续的通过 OpenClaw（QClaw）喂给 AI，再安装技能并只用，查看通过此技能完成的编码，是否符合预期。经过仅2周的折腾，目前发布了 [xfg-ddd-skills v2.2.1](https://github.com/fuzhengwei/xfg-ddd-skills) 版本，可以满足 DDD 六边形架构设计和编码实现。

地址：[https://github.com/fuzhengwei/xfg-ddd-skills](https://github.com/fuzhengwei/xfg-ddd-skills) - 欢迎使用，也感谢给点个 Star 支持！更建议，帮忙一起维护迭代。

### 2. 技能设计

```java
xfg-ddd-skills/
├── SKILL.md                      # 技能入口文件
├── README.md                     # 本文件
├── assets/                       # 资源文件
├── scripts/                      # 脚本工具
└── references/                   # 参考文档
    ├── architecture.md            # 六边形架构概述
    ├── entity.md                  # 实体设计规范
    ├── aggregate.md               # 聚合根设计规范
    ├── value-object.md            # 值对象设计规范
    ├── repository.md              # 仓储模式规范
    ├── port-adapter.md            # 端口与适配器规范
    ├── case-layer.md              # 业务编排层规范
    ├── project-structure.md       # Maven 多模块结构
    ├── naming.md                  # 命名规范
    └── docker-images.md           # Docker 镜像配置
```

- 当你需要以下场景时，使用本技能：

  - 设计或实现 DDD 架构的项目，可以直接帮你创建准确的、统一的、可用的工程架构
  - 需要六边形架构、端口与适配器模式
  - 创建 Entity（实体）、Aggregate（聚合根）、Value Object（值对象）
  - 设计 Repository（仓储）模式
  - 业务编排层（Case Layer）设计
  - 触发层（Trigger Layer：HTTP/MQ/Job）设计
  - 构建富领域模型（Rich Domain Model）

-   注意，此技能还在持续迭代中，陆续还会增强使用效果。

```java
┌─────────────────────────────────────────────────────────────┐
│                      触发层 Trigger                          │
│              (HTTP Controller / MQ Listener / Job)            │
└─────────────────────────┬───────────────────────────────────┘
                          ▼
┌─────────────────────────────────────────────────────────────┐
│                       API 层                                 │
│                    (DTO / Request / Response)                │
└─────────────────────────┬───────────────────────────────────┘
                          ▼
┌─────────────────────────────────────────────────────────────┐
│                      案例层 Case                              │
│              (业务编排 / 流程串联 / 组合调用)                  │
└─────────────────────────┬───────────────────────────────────┘
                          ▼
┌─────────────────────────────────────────────────────────────┐
│                      领域层 Domain                            │
│            (Entity / Aggregate / VO / Domain Service)       │
└─────────────────────────┬───────────────────────────────────┘
                          ▲
┌─────────────────────────────────────────────────────────────┐
│                    基础设施层 Infrastructure                  │
│        (Repository Impl / Port Adapter / DAO / PO)           │
└─────────────────────────────────────────────────────────────┘
```

- 此技能符合六边形架构设计标准，相关文档：[https://bugstack.cn/md/road-map/ddd-guide-03.html](https://bugstack.cn/md/road-map/ddd-guide-03.html)

### 3. 场景应用

#### 3.1 表单开发

小傅哥这里选择的一个【表单】功能开发的场景，类似通讯 doc 里有一个表单的功能，设置表单后，让用户填写；

由运营配置表单，填写相应的输入信息（字段），有文本、数字、日期、下拉选择和图片上传等类型。以及增强了表单数据场景运用，填表的表单可以直接关联到用途上，如数据做权限功能审核，或者数据做发券等功能。最后分享链接给用户填写提交，提交时候可以选择让用户是否鉴权（如github登录、星球登录、公众号登录）。

<div align="center">
	<img src="https://bugstack.cn/images/roadmap/tutorial/road-map-ai-agent-openclaw-attempt-09.png" width="850px"/>
</div>

全程零参与代码实现，只提供必要的信息。对于开发后的功能，都是让 OpenClaw（QClaw）自己做浏览器访问，填写数据，验证功能。如果有问题，则进行优化功能的处理。

不过，做这类东西，还是需要懂场景，懂产品，懂架构，懂技术。否则，它真运行起来，也是会有不少问题的。

#### 3.2 产品演示

##### 3.2.1 编辑表单（关联数据场景）

<div align="center">
	<img src="https://bugstack.cn/images/roadmap/tutorial/road-map-ai-agent-openclaw-attempt-10.png" width="450px"/>
</div>

##### 3.2.2 表单数据（全局展示信息）

<div align="center">
	<img src="https://bugstack.cn/images/roadmap/tutorial/road-map-ai-agent-openclaw-attempt-11.png" width="950px"/>
</div>

##### 3.2.3 能力配置（数据场景配置）

<div align="center">
	<img src="https://bugstack.cn/images/roadmap/tutorial/road-map-ai-agent-openclaw-attempt-12.png" width="950px"/>
</div>

- 这个的目的，就在于配置完表单，用户填写后，那么这些数据，要干啥用。我们可以把一些字段关联起来，直接使用。

##### 3.2.4 填写记录（展示收集信息）

<div align="center">
	<img src="https://bugstack.cn/images/roadmap/tutorial/road-map-ai-agent-openclaw-attempt-13.png" width="950px"/>
</div>

##### 3.2.5 分享表单（用户填写数据）

<div align="center">
	<img src="https://bugstack.cn/images/roadmap/tutorial/road-map-ai-agent-openclaw-attempt-14.png" width="450px"/>
</div>

- 分享表单后，用户填写提交即可。

### 4. 工程演示

<div align="center">
	<img src="https://bugstack.cn/images/roadmap/tutorial/road-map-ai-agent-openclaw-attempt-15.png" width="250px"/>
</div>

- 这个结构很重要，通过 xfg-ddd-skills 的限定，它可以按照约定的方式来编码。不要有ai幻觉和惊喜，而是要有小傅哥的“味道”。
- 不过在整个设计实现的“灵魂”上，还是差了点，不够老辣！

## 五、体验总结

1. 这种大量的工程化的，AI 写的代码，我不想碰。既不能给它修，也不想给它改。只要有 Token 就想让 AI 继续搞。软件工程交付，需要的不只是代码，还包括完整的理解代码，代码与产品PRD完全匹配，从而形成代码资产。
2. 使用AI做项目，仍然需要懂技术的，你的能力多强，你驾驭AI的本事就多大。
3. 纯新项目，或者小公司快速场景验证，可以使用AI快速搭建出来一套。
4. 公司里几十万行的老项目，如果靠 AI 这样迭代编写，可能会出事故。审查要严格。程序员编码的过程，是一行行逻辑的确认和产品功能的完整匹配。
5. 当一个需求过于复杂的时候，AI 会有过程中崩溃问题。这个对于个人编码项目没啥所谓，但公司级别的需求的迭代的。它的编码速度，有时候会低于人。n个类中，n行代码中，迭代功能，程序员已经有历史经验。ai 需要全量识别（或者你提前都编写好了技能）
6. skills 很有用，希望使用 ai 迭代项目的，需要持续的为工程迭代 skills 的各项技能。相当于为工程写技能路书。
7. OpenClaw（QClaw）属于一种网关入口，来控制设备。如果你更熟练于编码，那么纯 AI IDE 会更适合。如果你往各类的服务，接管电脑，那么 OpenClaw 更为合适。

---

<div align="center">
	<img src="https://bugstack.cn/images/roadmap/tutorial/road-map-ai-agent-openclaw-attempt-16.png" width="750px"/>
</div>