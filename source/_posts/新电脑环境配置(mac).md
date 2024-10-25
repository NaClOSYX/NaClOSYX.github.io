---
title: 新电脑环境配置(mac)
date: '2024-09-01 00:00:00 +0800'
updated: '2024-09-01 00:00:00 +0800'
categories:
  - 博客
  - 配置
tags:
  - 环境
  - 配置
author: NaClO
sticky: 10000
abbrlink: 149281275
---

## 修改Terminal中@后的名字

- 修改计算机名 ComputerName

  1. 修改

     ```bash
     scutil --set ComputerName "New ComputerName"
     ```

  2. 重启mac

  3. 查看

     ```bash
     scutil --get ComputerName
     ```

- 修改主机名 HostName

  1. 修改

     ```bash
     scutil --set HostName "New HostName"
     ```

  2. 重启mac

  3. 查看

     ```bash
     scutil --get HostName
     ```

- 修改本地主机名 LocalHostName 

  1. 修改

     ```bash
     scutil --set LocalHostName  "New HostName"
     ```

  2. 重启mac

  3. 查看

     ```bash
     scutil --get LocalHostName
     ```
## Homebrew

1. 官网 : https://brew.sh/zh-cn/

2. 运行命令

   - 官网安装源

     ```bash
     /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
     ```

   - 国内安装源

     ```bash
     /bin/zsh -c "$(curl -fsSL https://gitee.com/cunkai/HomebrewCN/raw/master/Homebrew.sh)"
     ```



## oh-my-zsh

- 切换zsh为默认shell

- 安装oh-my-zsh

  1. 官网 : https://ohmyz.sh/

  2. 安装

     - 自动安装

     ```bash
     sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
     ```

     - 手动安装

       1. 从git克隆

          ```bash
          git clone --depth=1 https://github.com/ohmyzsh/ohmyzsh.git ~/.oh-my-zsh
          ```

       2. 从template模板创建配置文件

          ```bash
          cp ~/.oh-my-zsh/templates/zshrc.zsh-template ~/.zshrc
          ```

  3. 重启终端或者执行`source ~/.zshrc`命令

- 切换主题

  - 修改`~/.zshrc`文件内 ZSH_THEME 行

    ```properties
    # 单个主题
    ZSH_THEME=“theme”
    # 多个主题随机
    ZSH_THEME_RANDOM_CANDIDATES=( "theme1" "theme2" "theme3" )
    ```

    主题文件在 `~/.oh-my-zsh/themes` 目录下

    主题预览 : https://github.com/ohmyzsh/ohmyzsh/wiki/Themes

- 插件安装

  - zsh-completions

    - 简介 : 额外的自动补全功能
  
    - 地址 : https://github.com/zsh-users/zsh-completions
  
    - 安装
  
      使用homebrew进行安装
  
      ```bash
      brew install zsh-completions
      ```
  
      根据控制台输出的提示，修改`~/.zshrc`文件在最后添加
  
      ```properties
      # 插件 额外的自动补全功能 start ============================================
      if type brew &>/dev/null; then
        FPATH=$(brew --prefix)/share/zsh-completions:$FPATH
      
        autoload -Uz compinit
        compinit
      fi
      # 插件 额外的自动补全功能 end ============================================
      ```
  
      重启终端或者执行`source ~/.zshrc`命令
  
  - zsh-autosuggestions
  
    - 简介 : 历史命令记录提示(灰色), 按 → 键补全
  
    - 地址 : https://github.com/zsh-users/zsh-autosuggestions
  
    - 安装 
  
      执行命令
  
      ```bash
      git clone --depth=1 https://github.com/zsh-users/zsh-autosuggestions.git ${ZSH_CUSTOM:-${ZSH:-~/.oh-my-zsh}/custom}/plugins/zsh-autosuggestions
      ```
  
      修改`~/.zshrc`文件`plugins=(`行后 添加 `zsh-autosuggestions`
  
      ```properties
      plugins=(
      	git
      	xxxxxxxx
      	# 历史命令记录提示
      	zsh-syntax-highlighting
      )
      ```
  
      重启终端或者执行`source ~/.zshrc`命令
  
  - zsh-syntax-highlighting
  
    - 简介 : 语法高亮插件 红色: 语法错误; 绿色: 语法正确;  下划线: 路径存在
  
    - 地址 : https://github.com/zsh-users/zsh-syntax-highlighting
  
    - 安装 
  
      执行命令
  
      ```bash
      git clone --depth=1 https://github.com/zsh-users/zsh-syntax-highlighting.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting
      ```
  
      修改`~/.zshrc`文件`plugins=(`行后 添加 `zsh-syntax-highlighting`
  
      ```properties
      plugins=(
      	git
      	xxxxxxxx
      	# 语法高亮插件
      	zsh-syntax-highlighting
      )
      ```
  
      重启终端或者执行`source ~/.zshrc`命令

## java

1. 下载地址 : https://www.oracle.com/cn/java/technologies/downloads/

2. 多版本切换配置

   - jdk默认安装目录 : `/Library/Java/JavaVirtualMachines/`

   - 修改

     ```properties
     # java profile start ============================================
     export JAVA_7_HOME=$(/usr/libexec/java_home -v1.7)
     export JAVA_8_HOME=$(/usr/libexec/java_home -v1.8)
     export JAVA_11_HOME=$(/usr/libexec/java_home -v11)
     export JAVA_17_HOME=$(/usr/libexec/java_home -v17)
     export JAVA_21_HOME=$(/usr/libexec/java_home -v21)
     
     
     alias jdk7='export JAVA_HOME=$JAVA_7_HOME'
     alias jdk8='export JAVA_HOME=$JAVA_8_HOME'
     alias jdk11='export JAVA_HOME=$JAVA_11_HOME'
     alias jdk17='export JAVA_HOME=$JAVA_17_HOME'
     alias jdk21='export JAVA_HOME=$JAVA_21_HOME'
     alias jdk23='export JAVA_HOME=$JAVA_23_HOME'
     
     
     # 默认java版本
     export JAVA_HOME=$JAVA_8_HOME
     export PATH=$JAVA_HOME/bin:$PATH:.
     # export CLASSPATH=$JAVA_HOME/lib/tools.jar:$JAVA_HOME/lib/dt.jar:$CLASSPATH:.
     # java profile end ============================================
     ```
   
   - 重新加载配置
   
     ```bash
     source ~/.zshrc
     ```
   
   - 检查
   
     - 查看JAVA_HOME
   
       ```bash
       echo $JAVA_HOME
       ```
   
     - 查看java版本
   
       ```bash
       java -version 
       ```

   - 切换命令
   
     ```bash
     jdk8
     ```
     

## maven

1. 下载地址 :  https://archive.apache.org/dist/maven/

2. 解压到目录 `~/environment/apache/maven`

3. 编辑`~/.zshrc`文件

   ```properties
   export MAVEN_HOME=~/environment/apache/maven/apache-maven-3.9.9
   export M2_HOME=~/environment/apache/maven/apache-maven-3.9.9
   export PATH=$MAVEN_HOME/bin:$PATH:.
   ```

   

4. 配置maven, 修改`settings.xml`文件

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   
   <settings xmlns="http://maven.apache.org/SETTINGS/1.2.0"
             xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
             xsi:schemaLocation="http://maven.apache.org/SETTINGS/1.2.0 https://maven.apache.org/xsd/settings-1.2.0.xsd">
   
      <!-- 本地仓库 -->
     <localRepository>/Users/naclo/environment/apache/maven/maven-repositry</localRepository>
   
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

## nvm

1. 使用brew安装

   ```bash
   brew install nvm
   ```

   

