---
title: pypy
date: 2022-02-05 00:00:00 +0800
updated: 2022-02-05 00:00:00 +0800
categories: [博客, python]
tags: [学习, 后端, python] 
author: NaClO
---

- 官网 `http://pypy.org/`

## Linux安装PYPY

1. 从官网拉取包

   ```bash
    wget https://downloads.python.org/pypy/pypy3.8-v7.3.7-linux64.tar.bz2
   ```

2. 解压

   ```bash
   tar -xf pypy3.8-v7.3.7-linux64.tar.bz2
   ```

3. 创建软链

   ```bash
   sudo ln -s /root/pypy3.8-v7.3.7-linux64/bin/pypy3 /usr/local/bin
   ```

4. 安装pip

   ```
   wget https://bootstrap.pypa.io/get-pip.py
   pypy3 get-pip.py
   ```

5. 更新pip

   ```bash
   pypy3 -m pip install -U pip
   pypy3 -m pip install --upgrade pip
   ```

6. 使用pip

   ```
   pypy3 -m pip install 包
   ```

   