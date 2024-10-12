---
title: Linux环境配置
date: '2021-03-01 00:00:00 +0800'
updated: '2021-03-01 00:00:00 +0800'
categories:
  - 博客
  - 配置
tags:
  - 环境
  - 配置
  - 服务器
author: NaClO
abbrlink: 1070965503
---

> 基于CentOS 8 最小安装

# 基础配置

## Mac连接虚拟机

Mac终端连接虚拟机命令`ssh -l root+虚拟机IP地址`

Mac终端传输文件给虚拟机`scp (本机文件所在地址) root@虚拟机IP地址：（所要传到虚拟机的位置）`

## 修改语言

`vim /etc/locale.conf`

英文：en_US.utf8

中文：zh_CN.utf8

## 防火墙

关闭防火墙 `systemctl stop firewalld.service`

关闭开机启动 `systemctl disable firewalld.service`

- 防火墙开放端口
  - tomcat：`firewall-cmd --zone=public --add-port=8080/tcp --permanent`
  - mysql：`firewall-cmd --zone=public --add-port=3306/tcp --permanent`
  - 重新载入：`firewall-cmd --reload`

## 切换阿里云源

1. 备份

   `mv /etc/yum.repos.d/CentOS-Base.repo /etc/yum.repos.d/CentOS-Base.repo.backup`

2. 下载

   `wget -O /etc/yum.repos.d/CentOS-Base.repo http://mirrors.aliyun.com/repo/Centos-8.repo`

3. 生成缓存

   `yum clean all` `yum makecache`

## 安装工具

- wget: `yum -y install wget`

- lrzsz: `yum install lrzsz -y`





# 安装JAVA

1. 下载并上传java安装包到 /usr/local/software/java目录

   https://www.oracle.com/java/technologies/javase/javase-jdk8-downloads.html

2. 解压JAVA `tar -zxvf jdk-8u92-linux-x64.tar.gz`

3. 编辑profile文件，添加环境变量 `vi /etc/profile`

   ````bash
   JAVA_HOME=/usr/local/software/java/jdk1.8.0_92
   JRE_HOME=$JAVA_HOME/jre
   PATH=$PATH:$JAVA_HOME/bin:$JRE_HOME/bin
   CLASSPATH=:$JAVA_HOME/lib/dt.jar:$JAVA_HOME/lib/tools.jar:$JRE_HOME/lib/dt.jar
   export JAVA_HOME JRE_HOME PATH CLASSPATH
   ````

4. 刷新环境变量 `source /etc/profile`

5. 测试安装 `java -version`

# 安装 tomcat

1. 下载并上传tomcat到/usr/local/software/tomcat目录

   http://tomcat.apache.org/

2. 解压

   `tar -xzvf  apache-tomcat-10.0.4.tar.gz`

3. 修改环境变量

   ````
   CATALINA_HOME=/usr/local/software/tomcat
   export PATH=CATALINA_HOME
   ````

4. 启动服务：进入bin目录`./startup.sh`

5. 关闭服务：进入bin目录`./shutdown.sh`

# 安装maven

1. 下载并上传maven到/usr/local/software/maven目录

   http://maven.apache.org/download.cgi

2. 解压

   `tar -xzvf  apache-maven-3.6.3-bin.tar.gz`

3. 修改环境变量

   ````
   export MAVEN_HOME=/usr/local/software/maven/apache-maven-3.6.3
   export PATH=$MAVEN_HOME/bin:$PATH 
   ````

4. 检查版本 `mvn -v `

5. 测试下载 `mvn help:system`

6. 切换下载源 `vi settings.xml ` 

   ````
   <!-- 镜像设置 -->
   <mirrors>
   	<mirror>
         <id>alimaven</id>
         <mirrorOf>central</mirrorOf>
         <name>aliyun maven</name>
         <url>http://maven.aliyun.com/nexus/content/repositories/central/</url>
       </mirror>
       <mirror>
         <id>alimaven</id>
         <name>aliyun maven</name>
         <url>http://maven.aliyun.com/nexus/content/groups/public/</url>
         <mirrorOf>central</mirrorOf>
       </mirror>
       <mirror>
         <id>central</id>
         <name>Maven Repository Switchboard</name>
         <url>http://repo1.maven.org/maven2/</url>
         <mirrorOf>central</mirrorOf>
       </mirror>
       <mirror>
         <id>repo2</id>
         <mirrorOf>central</mirrorOf>
         <name>Human Readable Name for this Mirror.</name>
         <url>http://repo2.maven.org/maven2/</url>
       </mirror>
       <mirror>
         <id>ibiblio</id>
         <mirrorOf>central</mirrorOf>
         <name>Human Readable Name for this Mirror.</name>
         <url>http://mirrors.ibiblio.org/pub/mirrors/maven2/</url>
       </mirror>
       <mirror>
         <id>jboss-public-repository-group</id>
         <mirrorOf>central</mirrorOf>
         <name>JBoss Public Repository Group</name>
         <url>http://repository.jboss.org/nexus/content/groups/public</url>
       </mirror>
       <mirror>
         <id>google-maven-central</id>
         <name>Google Maven Central</name>
         <url>https://maven-central.storage.googleapis.com</url>
         <mirrorOf>central</mirrorOf>
       </mirror>
       <mirror>
         <id>maven.net.cn</id>
         <name>oneof the central mirrors in china</name>
         <url>http://maven.net.cn/content/groups/public/</url>
         <mirrorOf>central</mirrorOf>
       </mirror>
     </mirrors>
   ````

7. 修改本地仓库

   ````
   <!-- 本地仓库 -->
   <localRepository>/Users/naclo/software/apache/maven/maven-repository</localRepository>
   ````

# 安装MySQL

1. 下载或者上传MySQL官方的 Yum源

   https://dev.mysql.com/downloads/repo/yum/

   `wget https://dev.mysql.com/get/mysql80-community-release-el8-1.noarch.rpm`

2. 安装源

   `yum localinstall mysql57-community-release-el7-8.noarch.rpm`

3. 安装mysql

   `yum install mysql-community-server`

   出错先执行：`yum module disable mysql`

4. 启动MySQL服务

   `systemctl start mysqld.service`

5. 查看MySQL运行状态

   `systemctl status mysqld.service`

6. 设置开机启动

   `systemctl enable mysqld`

   `systemctl daemon-reload`

   `systemctl disable mysqld`关闭开机自动启动

7. 修改默认密码

   1. `set password for 'root'@'localhost'=password('new password');`

   2. 查看密码`grep "password" /var/log/mysqld.log`

      使用默认密码登陆数据库修改密码`ALTER USER 'root'@'localhost' IDENTIFIED BY 'new password';`

8. 设置语言

   登录mysql，然后输入status查看状态

   修改my.cnf文件 `vi /etc/my.cnf`

   ````
   [client]
   default-character-set=utf8
   
   [mysqld]
   character-set-server=utf8
   collation-server=utf8_general_ci
   ````

   重启mysql: `service mysqld restart`

9. 开启mysql的远程访问

   `grant all privileges on *.* to 'root'@'%' identified by 'password' with grant option;`

   `FLUSH PRIVILEGES;`

   `EXIT`

- 密码策略
  - 查看密码策略`SHOW VARIABLES LIKE 'validate_password%';`
  - 设置密码的验证强度等级`set global validate_password_policy=LOW; `
  - 修改密码长度`set global validate_password_length=6; `

- 跳过验证登陆

  - 修改my.cnf文件 `vi /etc/my.cnf`

    ````
    [mysqld]
    skip-grant-tables
    ````

    