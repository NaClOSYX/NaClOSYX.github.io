---
title: ArangoDB
date: '2022-10-16 00:00:00 +0800'
updated: '2022-10-16 00:00:00 +0800'
categories:
  - 博客
  - 数据库
tags:
  - 常用
  - 学习
  - 数据库
author: NaClO
abbrlink: 4160037073
---

## MAC 下使用Docker安装ArangoDB

1. 搜索Oracle镜像

   ```bash
   docker search arangodb
   ```

2. 拉取镜像

   ```bash
   docker pull arangodb/arangodb  
   ```

3. 创建容器

   ```
   docker run -e ARANGO_ROOT_PASSWORD=root -p 8529:8529 -d \
             -v /Users/naclo/MyDockerVolumes/arangodb/01:/var/lib/arangodb3 \
              --name arangodb \
             arangodb/arangodb
   ```

   

4. 进入容器

   ```bash
   docker exec -it arangodb /bin/bash
   ```

5. 访问

   ```bash
   http://127.0.0.1:8529
   ```

   - 用户名/密码：root/root

6. 开启关闭 oracle 服务

   ```bash
   docker start arangodb
   docker stop arangodb
   ```