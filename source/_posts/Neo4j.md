---
title: Neo4j
date: '2022-10-14 00:00:00 +0800'
updated: '2022-10-14 00:00:00 +0800'
categories:
  - 博客
  - 数据库
tags:
  - 常用
  - 学习
  - 数据库
author: NaClO
abbrlink: 2027938216
---

## MAC 下使用Docker安装Neo4j

1. 搜索Oracle镜像

   ```bash
   docker search neo4j
   ```

2. 拉取镜像

   ```bash
   docker pull neo4j
   ```

3. 创建容器

   ```
   docker run -d --name neo4j \
   	-p 7474:7474 -p 7687:7687 \
   	-v /Users/naclo/MyDockerVolumes/neo4j/01/data:/data \
   	-v /Users/naclo/MyDockerVolumes/neo4j/01/logs:/logs \
   	-v /Users/naclo/MyDockerVolumes/neo4j/01/conf:/var/lib/neo4j/conf \
   	-v /Users/naclo/MyDockerVolumes/neo4j/01/import:/var/lib/neo4j/import \
   	--env NEO4J_AUTH=neo4j/password \
   	neo4j
   ```

   - `/data` : 数据目录
   - `/logs` : 日志目录
   - `/var/lib/neo4j/conf` : 配置目录
   - `/var/lib/neo4j/import` : 数据导入目录
   - `--env NEO4J_AUTH=neo4j/password`  : 设定数据库的名字的访问密码

4. 进入容器

   ```bash
   docker exec -it neo4j /bin/bash
   ```

5. 访问

   ```bash
   http://127.0.0.1:7474
   ```

   - 用户名/密码：root/root

6. 修改配置文件 开启远程访问

   ```bash
   cd /Users/naclo/MyDockerVolumes/neo4j/01/conf
   vim neo4j.conf
   ```

   ```
   // 进行以下更改
   //在文件配置末尾添加这一行
   dbms.connectors.default_listen_address=0.0.0.0  //指定连接器的默认监听ip为0.0.0.0，即允许任何ip连接到数据库
   
   //修改
   dbms.connector.bolt.listen_address=0.0.0.0:7687  //取消注释并把对bolt请求的监听“地址:端口”改为“0.0.0.0:7687”
   dbms.connector.http.listen_address=0.0.0.0:7474  //取消注释并把对http请求的监听“地址:端口”改为“0.0.0.0:7474”
   ```