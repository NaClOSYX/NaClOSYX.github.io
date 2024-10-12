---
title: PHP
date: 2020-09-20 00:00:00 +0800
updated: 2020-09-20 00:00:00 +0800
categories: [博客, PHP]
tags: [学习, 后端, PHP] 
author: NaClO
---

## 安装

### Apache服务

1. 安装路径 : ` /private/etc/apache2 `

2. 启动命令

   ````bash
   sudo apachectl start
   ````

3. 关闭命令

   ````bash
   sudo apachectl stop
   ````

4. 重启命令

   ```bash
   sudo apachectl restart
   ```

5. 项目目录: `/Library/WebServer/Documents/`

####  httpd.conf配置

1. 修改项目路径: `DocumentRoot`
2. 修改端口号: `Listen`

### php

1. brew安装php

   ````bash
   brew install php@7.3  
   ````

2. 创建软链

   ````bash
   brew link php@7.3 --force
   ````

3. 编辑环境变量

   ````
   # PHP_PATH
   export PHP_PATH=/usr/local/opt/php@7.3/
   
   export PATH=$PATH:$PHP_PATH/bin:$PHP_PATH/sbin
   ````

4. 修改https.conf

   ````
   LoadModule php7_module /usr/local/opt/php@7.3/lib/httpd/modules/libphp7.so
   ````

## 插件使用

### redis

#### mac下安装php-redis插件

1. 下载插件

   https://pecl.php.net/package/redis

2. 解压安装包

   ````bash
   tar -xzvf redis-*.*.*.tgz
   ````

3. 通过phpize生成编译configure配置文件

   ````bash
   cd redis-*.*.*/
   
   phpize
   
   ./configure --with-php-config=/usr/local/opt/php\@7.*/bin/php-config
   ````

4. 编译

   ````bash
   make
   
   make install
   ````

5. 配置 php.ini文件

   /usr/local/etc/php/7.*/php.ini

   ````ini
   extension="redis.so"
   ````

6. 访问测试

   ````php
   <?php
   //实例化redis对象
   $redis = new redis();
   //连接redis,第一个参数是redis服务的IP127.0.0.1是自己的,6379是端口号
   $redis->connect('127.0.0.1', 6379);
   echo "Server is running: " . $redis->ping();
   ````

   输出：Server is running: +PONG

## php



