---
title: Maven
date: 2024-09-01 00:00:00 +0800
categories: [博客, 配置]
tags: [环境, 配置, 后端] 
author: NaClO
---

## 安装

1. 下载地址 :  https://archive.apache.org/dist/maven/

2. 解压到目录 `D:\environment\develop\maven`

3. 编辑系统环境变量

   > MAVEN_HOME       D:\environment\develop\maven\apache-maven-3.9.9
   >
   > M2_HOME              D:\environment\develop\maven\apache-maven-3.9.9\maven-repositry

   > 在path里面添加 %MAVEN_HOME%\bin

4. 配置maven

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   
   <settings xmlns="http://maven.apache.org/SETTINGS/1.2.0"
             xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
             xsi:schemaLocation="http://maven.apache.org/SETTINGS/1.2.0 https://maven.apache.org/xsd/settings-1.2.0.xsd">
   
      <!-- 本地仓库 -->
     <localRepository>D:\environment\develop\maven\maven-repositry</localRepository>
   
     <pluginGroups></pluginGroups>
   
     <proxies></proxies>
   
     <servers></servers>
   
     <mirrors>
   
       <!-- 阿里云仓库 -->
       <mirror>
         <id>aliyunmaven</id>
         <mirrorOf>*</mirrorOf>
         <name>阿里云公共仓库</name>
         <url>https://maven.aliyun.com/repository/public</url>
       </mirror>
   
       <mirror>
         <id>maven-default-http-blocker</id>
         <mirrorOf>external:http:*</mirrorOf>
         <name>Pseudo repository to mirror external repositories initially using HTTP.</name>
         <url>http://0.0.0.0/</url>
         <blocked>true</blocked>
       </mirror>
     </mirrors>
   
     <profiles>
       <!-- java版本 --> 
       <profile>
           <id>jdk-1.8</id>
           <activation>
           <activeByDefault>true</activeByDefault>
           <jdk>1.8</jdk>
           </activation>
       
           <properties>
           <maven.compiler.source>1.8</maven.compiler.source>
           <maven.compiler.target>1.8</maven.compiler.target>
           <maven.compiler.compilerVersion>1.8</maven.compiler.compilerVersion>
           </properties>
       </profile>
     </profiles>
   
   </settings>
   ```

5. 运行测试命令

   ```bash
   mvn -v
   mvn help:system
   ```

## 配置

- 阿里云地址 : https://maven.aliyun.com/

- 配置 : 

  ```xml
  <!-- 阿里云公共仓库 -->
  <mirror>
    <id>aliyunmaven</id>
    <mirrorOf>*</mirrorOf>
    <name>阿里云公共仓库</name>
    <url>https://maven.aliyun.com/repository/public</url>
  </mirror>
  ```

- 删除 `.lastUpdated文件`

  > Windows环境，先在cmd命令行中进入到maven仓库文件下，执行命令：` for /r %i in (*.lastUpdated) do del %i`
  >
  > Linux环境，可执行命令：`find /app/maven/localRepository -name "*.lastUpdated" -exec grep -q "Could not transfer" {} \; -print -exec rm {} \;`

