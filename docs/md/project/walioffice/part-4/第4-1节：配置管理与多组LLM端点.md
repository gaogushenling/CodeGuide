---
title: 第4-1节：配置管理与多组LLM端点
pay: https://t.zsxq.com/5AIrD
---

# 《WaLiOffice - AI Agent 智能办公平台》第4-1节：配置管理与多组LLM端点

作者：小傅哥
<br/>博客：[https://bugstack.cn](https://bugstack.cn)

>沉淀、分享、成长，让自己和他人都能有所收获！😄

## 一、前言

大家好，我是技术UP主小傅哥。

Part 3 我们把 Agent 的工具系统全部跑通了——Markdown、Word、Excel、图表、PPT、图片、视频。但有没有想过一个问题：**LLM 的 API 地址在哪？数据库用 MySQL 还是 SQLite？JWT 密钥是什么？** 这些运行时参数总不能写死在代码里，每改一次都要重新编译。

这节我们就来搞定**配置管理**——把所有运行时参数收敛到 `.env` 文件，程序启动时通过 `Config::from_env()` 一次性读取。同时要讲清楚 WaLiOffice 特有的**多组 LLM 端点**设计：一个 AI 办公平台要同时调三种完全不同类型的模型——文本生成（glm-4）、图片生成（agnes-image）、视频生成（agnes-video），它们的服务商、端点、密钥、限流策略各不相同，必须分开配置。

## 一、本章诉求

1. **理解配置分层**env` 文件 → 环境变量 → `Config` 结构体 → 全局单例 → 运行时使用，全链路清晰
2. **掌握多组 LLM 端点设计**：为什么文本/图片/视频要分三组配置，每组怎么支持多 Key 轮询、多模型列表
3. **数据库灵活切换**：`DATABASE_URL` 一行配置切换 SQLite/MySQL，业务代码零改动
4. **目录自动创建**：启动时 `ensure_dirs()` 自动建目录，避免"文件找不到"的奇怪报错

## 二、流程设计

### 2.1 配置加载全流程

<div align="center">
    <img src="https://bugstack.cn/images/article/project/walioffice/walioffice-4-1-01.png" width="950px">
</div>

> 配图源文件：[draw.io/config-loading-flow.drawio](draw.io/config-loading-flow.drawio)

```
程序启动 main()
    ↓
① config::config()                        // 全局单例，OnceLock 只初始化一次
    └─ Config::from_env()
         ├─ dotenvy::dotenv()              // 加载 .env 文件（存在才加载，不存在静默跳过）
         ├─ env_or_required("AIPPT_JWT_SECRET")   // 必填，缺失 → 打印提示 + exit(1)
         ├─ 三组 LLM：BASE_URL / API_KEY（必填）
         │    └─ split_api_keys()           // "sk-a,sk-b,sk-c" → Vec<String> 多 Key
         ├─ 模型列表：LLM_TEXT_MODELS（复数，逗号分隔）
         │    └─ 没配复数？回退用 LLM_TEXT_MODEL（单数）包装成单元素列表  // 向后兼容
         │    └─ 默认模型 = *_MODELS_DEFAULT 或列表第一个
         ├─ 其余项 env_or(key, default)     // 有默认值：端口 8000、超时 30 分钟……
         └─ DATABASE_URL 不配 → 默认 sqlite://{data_dir}/walioffice.db?mode=rwc
    ↓
② cfg.ensure_dirs()                        // create_dir_all 递归建目录，已存在则跳过
    ↓
③ state::init_db_pool().await
    └─ db::init_pool(&cfg.database_url, ...)
         ├─ sqlx::any::install_default_drivers()   // AnyPool 前必须安装驱动
         ├─ mysql:// 开头 → MySqlPool 跑 001_init_mysql.sql → AnyPool 连接
         └─ 否则       → SqlitePool 跑 001_init.sql       → AnyPool 连接
    ↓
④ 启动日志：🚀 运行地址 / 📝 LLM 模型@端点 / 📂 目录 / 🗄️ Database 类型
```

**👩🏻‍🏫敲黑板**：整个链路是**"fail fast"（快速失败）**哲学——必填配置缺失时程序在启动瞬间就退出，而不是带着空密钥跑起来、等第一个用户请求报 401 才发现。`env_or_required()` 里直接 `std::process::exit(1)`，宁可启动失败，绝不带病运行。

