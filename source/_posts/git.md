---
title: git
date: '2025-01-01 00:00:00 +0800'
updated: '2025-01-01 00:00:00 +0800'
categories:
  - 博客
tags:
  - 常用
  - 学习
author: NaClO
abbrlink: 1368285564
---

# git

## git错误解决

- git中的SSL certificate problem: unable to get local issuer certificate错误的解决办法

  ```bash
  # 将git中的sslverify关掉
  # 当前用户
  git config --global http.sslverify false
  # 全局所有用户
  git config --system http.sslverify false
  # 当前仓库
  git config http.sslverify false
  
  # npm 
  npm config set strict-ssl false
  
  vim  ~/.gitconfig 将“sslverify”的值改为“false”，注意“=”号两边有空格，保存退出“ZZ”。
  ```
  
- git 报错fatal: unable to access `‘https://github.com/.../.git'`

  - 取消代理

    ```bash
    git config --global --unset http.proxy 
    git config --global --unset https.proxy
    ```

  - 设置代理

    - 打开系统设置，搜索代理设置，并点击编辑按钮。

    - 在代理服务器中，将端口设置为7890，打开使用代理服务器，并点击保存。

    - 终端输入命令

      ```bash
      git config --global http.proxy http://127.0.0.1:7890
      git config --global httpS.proxy http://127.0.0.1:7890
      ```
