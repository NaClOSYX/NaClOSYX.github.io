---
title: Mongodb
date: 2022-10-17 00:00:00 +0800
categories: [博客, 数据库]
tags: [常用, 学习, 数据库] 
author: NaClO
---

## MAC 下使用Docker安装mongodb

1. 搜索Oracle镜像

   ```bash
   docker search mongo
   ```

2. 拉取镜像

   ```bash
   docker pull mongo:latest
   ```

3. 创建容器

   ```bash
   docker run -itd --name mongo -p 27017:27017 mongo --auth
   ```

   - **-p 27017:27017** ：映射容器服务的 27017 端口到宿主机的 27017 端口。外部可以直接通过 宿主机 ip:27017 访问到 mongo 的服务。
   - **--auth**：需要密码才能访问容器服务。

4. 进入容器

   ```bash
   docker exec -it mongo mongo admin
   ```

5. 使用普通身份登入

   ```bash
   # 创建一个名为 admin，密码为 123456 的用户。
   db.createUser({ user:'admin',pwd:'123456',roles:[ { role:'userAdminAnyDatabase', db: 'admin'},"readWriteAnyDatabase"]});
   # 尝试使用上面创建的用户信息进行连接。
   db.auth('admin', '123456')
   ```