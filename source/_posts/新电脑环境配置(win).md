---
title: 新电脑环境配置(win)
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
abbrlink: 2361082684
---

## 下载地址

- git
  - git : https://git-scm.com/download/win
  - tortoisegit : https://tortoisegit.org/
  - sourcetree : https://www.sourcetreeapp.com/
- svn 
  - svn : https://subversion.apache.org/
  - tortoisesvn : https://tortoisesvn.subversion.org.cn/
- tomcat :  https://archive.apache.org/dist/tomcat/
- dbeaver : https://dbeaver.io/download/
- nginx : https://nginx.org/en/

## java

- 下载地址 : https://www.oracle.com/cn/java/technologies/downloads/



## jetBrains

1. 下载地址 :

   > idea :  https://www.jetbrains.com/idea/download/
   >
   > webstorm : https://www.jetbrains.com/webstorm/download/

2. 激活

   >激活教程：https://www.quanxiaoha.com/dev-tools/
   >
   >激活脚本网盘下载链接:
   >链接：https://pan.baidu.com/s/1ERBNn6WpYT3bUDd_WSyNRw?pwd=rp6y 
   >提取码：rp6y
   >
   >备用链接1（蓝奏网盘）：
   >https://wwv.lanzouh.com/ivGcA270tnzc
   >
   >备用链接2:
   >链接：https://pan.baidu.com/s/1wl0giGl2I9qItkszvMUhNQ?pwd=u94m 
   > 提取码：u94m



## maven

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

## node (nvm)

1. 下载地址

   - nvm : https://github.com/coreybutler/nvm-windows
   - node : https://nodejs.org/dist/

2. 配置nvm

   - nvm安装到 `D:\environment\develop\nvm`

   - 在 nvm 的安装路径下，找到 settings.txt，在后面加上这两行

     > node_mirror: https://npmmirror.com/mirrors/node/
     >
     > npm_mirror: https://npmmirror.com/mirrors/npm/

   - 编辑系统环境变量

     > NVM_HOME     D:\environment\develop\nvm
     >
     > NVM_SYMLINK   D:\environment\develop\nodejs

     > path里面添加
     >
     > %NVM_HOME%
     >
     > %NVM_SYMLINK%
     >
     > %NVM_SYMLINK%\node_global

   - nvm常用命令

     ```bash
     nvm -v                          # 查看当前版本
     nvm --help                      # 显示命令行帮助信息
     nvm list                        # 显示已安装的版本（同 nvm list installed）
     nvm list installed              # 显示已安装的版本
     nvm list available              # 显示所有可以下载的版本
     nvm install <version>           # 下载对应node版本（如：nvm install 14.20.1）
     nvm install latest              # 安装最新版本
     nvm uninstall <version>         # 卸载node版本
     nvm use <version>               # 切换node版本
     nvm on                          # 开启nvm
     nvm off                         # 关闭nvm
     nvm current                     # 查看当前使用的node版本
     nvm ls                          # 查看所有本地可用的node版本
     nvm alias <alias> <version>     # 给不同的版本号添加别名
     nvm unalias <alias>             # 删除已定义的别名
     nvm alias default <version>     # 设置默认版本
     ```

3. node

   - 安装node14

     ```bash
     nvm install 14
     nvm use 14
     ```

   - 配置node

     ```bash
     # 查询源
     npm config get registry
     
     # 更换国内源
     npm config set registry https://registry.npmmirror.com
     
     # 全局安装路径
     npm config set prefix "D:\environment\develop\nodejs\node_global"
     # 全局缓存路径
     npm config set cache "D:\environment\develop\nodejs\node_cache"
     # 配置完后请确认配置成功
     npm config ls
     ```

4. 安装组件

   ```bash
   # 源管理
   npm i -g nrm
   # yarn
   npm i -g yarn
   # cnpm
   npm i -g cnpm
   # vue
   npm i -g @vue/cli
   # react
   
   # ts
   npm i -g  typescript ts-node tslib @types/node
   
   
   npm i -g nrm yarn cnpm @vue/cli typescript ts-node tslib @types/node 
   ```

## VSCode

1. 下载地址 : https://code.visualstudio.com/download      下载 **System Installer**版本

2. 常用组件

   - 通用
     - 简体中文插件 : [Chinese (Simplified) (简体中文) Language Pack for Visual Studio Code](https://marketplace.visualstudio.com/items?itemName=MS-CEINTL.vscode-language-pack-zh-hans)
     - 图标插件 : [vscode-icons](https://marketplace.visualstudio.com/items?itemName=vscode-icons-team.vscode-icons)
     - 自动重命名标签 : [Auto Rename Tag](https://marketplace.visualstudio.com/items?itemName=formulahendry.auto-rename-tag)
     - 自动闭合标签 : [Auto Close Tag](https://marketplace.visualstudio.com/items?itemName=formulahendry.auto-close-tag)
     - 高亮标签 : [Highlight Matching Tag](https://marketplace.visualstudio.com/items?itemName=vincaslt.highlight-matching-tag)
     - 函数定义跳转 : [Goto definition alias](https://marketplace.visualstudio.com/items?itemName=antfu.goto-alias)
     - 文件名自动补全 : [Path Intellisense](https://marketplace.visualstudio.com/items?itemName=christian-kohler.path-intellisense)
     - 代码格式化 : [Prettier - Code formatter](https://marketplace.visualstudio.com/items?itemName=esbenp.prettier-vscode)
     - emoji支持 : [:emojisense:](https://marketplace.visualstudio.com/items?itemName=bierner.emojisense)
     - 拼写检查 : [Code Spell Checker](https://marketplace.visualstudio.com/items?itemName=streetsidesoftware.code-spell-checker)
     - 代码注释高亮 : [Better Comments](https://marketplace.visualstudio.com/items?itemName=aaron-bond.better-comments)
     - 代码一键运行 : [Code Runner](https://marketplace.visualstudio.com/items?itemName=formulahendry.code-runner)
     - 高亮颜色 : [colorize](https://marketplace.visualstudio.com/items?itemName=kamikillerto.vscode-colorize)
     - 正则测试 : [Regex Previewer](https://marketplace.visualstudio.com/items?itemName=chrmarti.regex)

   - 前端: 
     - JS,TS支持 : [JavaScript and TypeScript Nightly](https://marketplace.visualstudio.com/items?itemName=ms-vscode.vscode-typescript-next)
     - ESLint : [ESLint](https://marketplace.visualstudio.com/items?itemName=dbaeumer.vscode-eslint)
     - Vue支持 : [Vue - Official](https://marketplace.visualstudio.com/items?itemName=Vue.volar)
     - element-ui支持 : [vscode-element-helper](https://marketplace.visualstudio.com/items?itemName=ElemeFE.vscode-element-helper)
     - 组件提示(element-ui, antd vue, vant) : [vue-helper](https://marketplace.visualstudio.com/items?itemName=shenjiaolong.vue-helper)
     - CSS扩展 : [HTML CSS Support ](https://marketplace.visualstudio.com/items?itemName=ecmel.vscode-html-css)
     - less插件 : [Easy LESS](https://marketplace.visualstudio.com/items?itemName=mrcrowl.easy-less)
     - SVG预览 : [SVG](https://marketplace.visualstudio.com/items?itemName=jock.svg)

   - 版本控制
     - git支持 : [GitLens — Git supercharged](https://marketplace.visualstudio.com/items?itemName=eamodio.gitlens)
     - git历史版本 : [Git History](https://marketplace.visualstudio.com/items?itemName=donjayamanne.githistory)
     - git历史可视化操作 : [Git Graph](https://marketplace.visualstudio.com/items?itemName=mhutchie.git-graph)
   - Markdown
     - Markdown支持 : [Markdown All in One](https://marketplace.visualstudio.com/items?itemName=yzhang.markdown-all-in-one)
     - Markdown预览 : [Markdown Preview Enhanced](https://marketplace.visualstudio.com/items?itemName=shd101wyy.markdown-preview-enhanced)
   - 其他
     - XML工具 : [XML Tools](https://marketplace.visualstudio.com/items?itemName=DotJoshJohnson.xml)