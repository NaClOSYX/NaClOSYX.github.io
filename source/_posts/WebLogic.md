---
title: WebLogic
date: '2022-12-01 00:00:00 +0800'
updated: '2022-12-01 00:00:00 +0800'
categories:
  - 博客
  - 配置
tags:
  - 环境
  - 配置
  - 服务器
author: NaClO
abbrlink: 1965655825
---

# weblogic

## MAC 下使用Docker安装weblogic

1. 搜索weblogic镜像

   ```bash
   docker search weblogic
   ```

2. 拉取镜像

   ```bash
   docker pull ismaleiva90/weblogic12
   ```

3. 创建容器

   ```bash
   docker run -d -p 7001:7001 -p 7002:7002  ismaleiva90/weblogic12:latest
   ```

4. 进入容器

   ```bash
   docker exec -it weblogic /bin/bash
   ```

5. 访问

   ```bash
   http://localhost:7001/console
   ```

   - 用户名/密码：weblogic/welcome1