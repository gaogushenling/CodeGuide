---
title: Q&A：常见开发问题错误解答
lock: no
---

# Q&A：常见开发问题错误解答

作者：小傅哥
<br/>博客：[https://bugstack.cn](https://bugstack.cn)
<br/>课程：[https://t.zsxq.com/Yfbwo](https://t.zsxq.com/Yfbwo)

>沉淀、分享、成长，让自己和他人都能有所收获！😄

## 一、断点调试

- [排查10个Bug](https://www.bilibili.com/video/BV1F6421w71e)
- [打断点查空指针](https://www.bilibili.com/video/BV1q1421Q7Uv)

## 二、开发问题

### 1. Parameter 'teamIds' not found.

如果遇到报错提示，有兼容问题，可以添加 `@Param("teamIds")` 到方法上 `Integer queryAllUserCount(@Param("teamIds") Set<String> teamIds);`

### 2. this is incompatible with sql_mode=only_full_group_by

>一种是修改连接，另外一种是修改库配置。jdbc:mysql://127.0.0.1:3306/group_buy_market?serverTimezone=UTC&characterEncoding=utf8&autoReconnect=true&serverTimezone=Asia/Shanghai&useSSL=true&sessionVariables=sql_mode='NO_ENGINE_SUBSTITUTION,STRICT_TRANS_TABLES'

**添加 my.cnf 文件**

```java
[client]
port                    = 3306
default-character-set   = utf8mb4

[mysqld]
user                    = mysql
port                    = 3306
sql_mode                = NO_ENGINE_SUBSTITUTION,STRICT_TRANS_TABLES

default-storage-engine  = InnoDB
default-authentication-plugin   = mysql_native_password
character-set-server    = utf8mb4
collation-server        = utf8mb4_unicode_ci
init_connect            = 'SET NAMES utf8mb4'

slow_query_log
#long_query_time         = 3
slow-query-log-file     = /var/log/mysql/mysql.slow.log
log-error               = /var/log/mysql/mysql.error.log

default-time-zone       = '+8:00'

[mysql]
default-character-set   = utf8mb4
```

**修改 docker compose**

```javascript
mysql:
  image: registry.cn-hangzhou.aliyuncs.com/xfg-studio/mysql:8.0.32
  container_name: mysql
  command: --default-authentication-plugin=mysql_native_password
  restart: always
  environment:
    TZ: Asia/Shanghai
    MYSQL_ROOT_PASSWORD: 123456
  ports:
    - "13306:3306"
  volumes:
    - ./mysql/my.cnf:/etc/mysql/conf.d/mysql.cnf:ro
    - ./mysql/sql:/docker-entrypoint-initdb.d
  healthcheck:
    test: [ "CMD", "mysqladmin" ,"ping", "-h", "localhost" ]
    interval: 5s
    timeout: 10s
    retries: 10
    start_period: 15s
  networks:
    - my-network
```

- 修改 MySQL 8.0 安装配置
