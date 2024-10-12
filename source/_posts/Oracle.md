---
title: Oracle
date: '2022-10-13 00:00:00 +0800'
updated: '2022-10-13 00:00:00 +0800'
categories:
  - 博客
  - 数据库
tags:
  - 常用
  - 学习
  - 数据库
author: NaClO
abbrlink: 4047896278
---
## MAC 下使用Docker安装oracle-xe-11g

1. 搜索Oracle镜像

   ```bash
   docker search oracle
   ```

2. 拉取镜像

   ```bash
   docker pull oracleinanutshell/oracle-xe-11g
   ```

3. 创建容器

   ```bash
   docker run -h "oraclehost" --name "oracle" -d -p 1521:1521 oracleinanutshell/oracle-xe-11g
   ```

   ```
   docker run -h "oraclehost" --name "oracle" -d -v /Users/naclo/MyDockerVolumes/oracle11g/empty/oracle/:/u01/app/oracle -p 1521:1521 oracleinanutshell/oracle-xe-11g
   ```

   

4. 进入容器

   ```bash
   docker exec -it oracle /bin/bash
   ```

5. 使用普通身份登入

   ```bash
   sqlplus system/oracle
   ```

6. 开启关闭 oracle 服务

   ```bash
   docker start oracle
   docker stop oracle
   ```

## MAC 下使用Docker安装oracle-xe-11g

1. 拉取镜像

   ```bash
   docker pull gvenzl/oracle-xe
   docker pull gvenzl/oracle-xe:21-full
   ```

2. 创建容器

   ```bash
   docker run -d -p 1521:1521 -e ORACLE_PASSWORD=123456 --name "oracle21" gvenzl/oracle-xe
   ```

   ```bash
   docker run -d -p 1521:1521 -e ORACLE_PASSWORD=123456 -v \
   /Users/naclo/MyDockerVolumes/oracle21c/00/oracle/:/opt/oracle/oradata \
   --name "oracle21" \
   gvenzl/oracle-xe
   ```

3. 进入容器

   ```bash
   docker exec -it oracle21 /bin/bash
   ```

4. 使用普通身份登入

   ```bash
   sqlplus system/oracle
   ```

5. 开启关闭 oracle 服务

   ```bash
   docker start oracle
   docker stop oracle
   ```

