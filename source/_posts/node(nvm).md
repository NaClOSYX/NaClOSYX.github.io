---
title: Node管理工具——NVM 安装使用
date: '2024-09-01 00:00:00 +0800'
updated: '2024-09-01 00:00:00 +0800'
categories:
  - 博客
  - 配置
tags:
  - 环境
  - 配置
  - 前端
author: NaClO
abbrlink: 3113073277
---

## NVM安装

### Windows下安装

1. 下载地址

   - nvm : https://github.com/coreybutler/nvm-windows
   
2. 配置nvm

   - nvm解压安装到 `D:\environment\develop\nvm`

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

   - 验证

     使用cmd输入`nvm -v`可查看版本号

### Mac下安装

1. 使用brew安装

   ```bash
   brew install nvm
   ```

2. 编辑环境变量 修改`~/.zshrc`文件在最后添加

   ```bash
   # nvm profile start ====================================
   
   export NVM_DIR="$HOME/.nvm"
     [ -s "/usr/local/opt/nvm/nvm.sh" ] && \. "/usr/local/opt/nvm/nvm.sh"  # This loads nvm
     [ -s "/usr/local/opt/nvm/etc/bash_completion.d/nvm" ] && \. "/usr/local/opt/nvm/etc/bash_completion.d/nvm"  # This loads nvm bash_completion
   
   # nvm profile end ====================================
   ```

3. 验证

   使用zsh输入`nvm -v`可查看版本号

## NVM使用

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

## 安装node

1. 安装node14

   ```bash
   nvm install 14
   nvm use 14
   ```

2. 配置node

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

3. 安装组件

   ```bash
   # 源管理
   npm i -g nrm
   # yarn
   npm i -g yarn
   # cnpm
   npm i -g cnpm
   # vue
   npm i -g @vue/cli
   
   # ts
   npm i -g  typescript ts-node tslib @types/node
   
   npm i -g nrm yarn cnpm @vue/cli typescript ts-node tslib @types/node 
   ```

   

