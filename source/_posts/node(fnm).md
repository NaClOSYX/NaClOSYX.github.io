---
title: Node管理工具——FNM 安装使用
date: '2025-07-01 00:00:00 +0800'
updated: '2025-07-01 00:00:00 +0800'
categories:
  - 博客
  - 配置
tags:
  - 环境
  - 配置
  - 前端
author: NaClO
abbrlink: 281773306
---

## FNM安装

### Windows下安装

1. 下载地址

   - fnm: https://github.com/Schniz/fnm
   
2. 配置fnm

   - fnm解压安装到 `D:\environment\develop\fnm-windows`

   - 创建环境变量

     >FNM_DIR	D:\environment\develop\fnm-windows
     >
     >FNM_NODE_DIST_MIRROR	https://npmmirror.com/mirrors/node/

     > path里面添加
     >
     > %FNM_DIR%
   
   - 验证

     使用cmd输入`fnm --version`可查看版本号

### Mac下安装

1. 使用brew安装

   ```bash
   brew install fnm
   ```

2. 编辑环境变量 修改`~/.zshrc`文件在最后添加

   ```bash
   # fnm profile start ====================================
   
   # --use-on-cd 表示根据当前目录下的 .nvmrc 文件自动切换版本
   # --version-file-strategy=recursive 表示递归查找版本文件
   # --resolve-engines 根据package.json#engines#node切换node版本
   
   eval "$(fnm env --use-on-cd --version-file-strategy=recursive)"
   
   # fnm profile end ====================================
   ```

## FNM使用

- fnm常用命令

  ```bash
  fnm --version                   # 查看当前版本
  fnm --help                      # 显示命令行帮助信息
  fnm env							# 查看环境
  fnm list-remote					# 显示所有可以下载的版本
  fnm install <version>			# 下载对应node版本（如：fnm install 14.20.1）
  fnm use <version>				# 切换node版本
  fnm current						# 查看当前使用的node版本
  fnm list						# 显示已安装的版本
  fnm uninstall <version>			# 卸载node版本
  fnm default <version>			# 设置默认版本
  fnm alias <version> <alias>		# 给不同的版本号添加别名
  fnm unalias <alias>				# 删除已定义的别名
  ```
  
- 自动切换版本

  - 在`.nvmrc`中指定

    ```bash
    v20.18.0
    ```

  - 在`.node-version`中指定

    ```bash
    v20.18.0
    ```

  - 在`package.json`文件中指定版本

    ```BASH
    {
      "engines": {
        "node": ">=20.0.0"
      }
    }
    ```



## 安装node

1. 安装node14

   ```bash
   fnm install 14
   fnm use 14
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

   

