---
title: Paperless-ngx | 文档管理系统
date: '2025-07-17 00:00:00 +0800'
updated: '2025-07-17 00:00:00 +0800'
categories:
  - 博客
  - 工具
tags:
  - 工具
author: NaClO
abbrlink: 1364307048
---
1. 介绍 : Paperless-ngx 是一个社区支持的开源文档管理系统，可将您的物理文档转换为可搜索的在线存档，因此您可以减少纸张的使用。

2. GitHub : https://github.com/paperless-ngx/paperless-ngx

3. 官网 :  https://docs.paperless-ngx.com/

## 使用docker compose安装

1. 确保安装了`docker`和`docker compose`

2. 创建目录

   ```bash
   mkdir paperless-ngx
   cd paperless-ngx
   ```

3. 下载Paperless-ngx的配置

   ```bash
   wget -O docker-compose.yml https://raw.githubusercontent.com/paperless-ngx/paperless-ngx/refs/heads/main/docker/compose/docker-compose.postgres-tika.yml
   ```

4. 下载环境变量

   ```bash
   wget https://raw.githubusercontent.com/paperless-ngx/paperless-ngx/refs/heads/main/docker/compose/.env
   wget https://raw.githubusercontent.com/paperless-ngx/paperless-ngx/refs/heads/main/docker/compose/docker-compose.env
   ```

5. 拉取镜像

   ```bash
   docker compose pull
   ```

6. 启动服务

   ```bash
   docker compose up -d
   ```

7. 创建管理员账号

   ```bash
   docker compose exec webserver python3 manage.py createsuperuser
   ```

   按照提示输入用户名、邮箱和密码。

8. 访问`http://localhost:8000` 使用创建的管理员账户登录 

