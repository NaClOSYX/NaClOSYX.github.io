---
title: pyenv
date: 2022-02-01 00:00:00 +0800
updated: 2022-02-01 00:00:00 +0800
categories: [博客, python]
tags: [学习, 后端, python] 
author: NaClO
---


## Linux下

1. 安装依赖

   ```bash
   yum install zlib-devel bzip2-devel openssl-devel ncurses-devel sqlite-devel readline-devel tk-devel gdbm-devel db4-devel libpcap-devel xz-devel libjpeg-turbo-devel git
   ```

2. 拉取包

   ```bash
   git clone git://github.com/pyenv/pyenv.git ~/.pyenv
   ```

3. 拉取virtualenv

   ````bash
   git clone git://github.com/pyenv/pyenv-virtualenv.git ~/.pyenv/plugins/pyenv-virtualenv
   ````

4. 配置~/.bash_profile

   ```bash
   vi ~/.bash_profile
   ```

   - 第一种
   
     ```bash
     export PYENV_ROOT="$HOME/.pyenv"
     export PATH="$PYENV_ROOT/bin:$PATH"
     if command -v pyenv 1>/dev/null 2>&1; then
      eval "$(pyenv init -)"
     fi
     eval "$(pyenv virtualenv-init -)"
     ```
   
   - 如果第一种不起效 第二种
   
     ```bash
     export PYENV_ROOT="$HOME/.pyenv"
     export PATH="$PYENV_ROOT/bin:$PATH"
     eval "$(pyenv init --path)"
     eval "$(pyenv virtualenv-init -)"
     eval "$(pyenv init -)"
     ```
   
5. 刷新
   
   ```bash
   source ~/.bash_profile
   ```

## 使用

- 列出所有包

  ```bash
  pyenv install --list
  ```

- 安装

  ```bash
  pyenv install 版本号
  ```

  - 因为网络问题 建议直接下载tar.xz源码包，放置在~/.pyenv/cache/目录下在执行install命令

  - 带参数执行

    ```bash
    env PYTHON_CONFIGURE_OPTS="--enable-shared --with-ssl" pyenv install 版本号
    ```

- 应用到本地

  ```bash
  pyenv local 版本号
  ```

- 应用到当前shell

  ```bash
  pyenv shell 版本号
  ```

- 应用到全局

  ```bash
  pyenv global 版本号
  ```

- 取消设置local版本

  ```bash
  pyenv local --unset
  ```

## 安装python包

- 升级pip

  ```bash
  pip  install --index https://pypi.mirrors.ustc.edu.cn/simple/ --upgrade pip
  ```

- 安装依赖包

  ```bash
  pip  install --index https://pypi.mirrors.ustc.edu.cn/simple/ numpy pandas scipy matplotlib scikit-learn pyinstaller==4.3
  ```

- 打包测试

  ```bash
  python3 clustering_exec_main_tree.py m5-failure.csv a b
  # 打包
  pyinstaller -F clustering_exec_main_tree.py
  
  ./clustering_exec_main_tree.py m5-failure.csv a b
  ```

## 报错处理

- `ERROR: The Python ssl extension was not compiled. Missing the OpenSSL lib?`

  - 手动更新OpenSSL

    ```bash
    wget http://www.openssl.org/source/openssl-1.0.2j.tar.gz
    tar -xzf openssl-1.0.2j.tar.gz
    cd openssl-1.0.2j
    ./config shared zlib
    ./config -t
    make
    make install
    cd /usr/local/ssl/lib
    ldconfig -v
    # 把下方新的ssl环境变量导入到.bashrc
    LD_RUN_PATH="/usr/local/ssl/lib" \
    LDFLAGS="-L/usr/local/ssl/lib" \
    CPPFLAGS="-I/usr/local/ssl/include" \
    CFLAGS="-I/usr/local/ssl/include" \
    CONFIGURE_OPTS="--with-openssl=/usr/local/ssl" \
    ```
    
  - 安装以下依赖包，重新执行

    ```bash
    yum install -y openssl-static
    
    yum install -y gcc wget
    
    yum groupinstall "Development tools"
    
    yum install zlib-devel bzip2-devel openssl-devel ncurses-devel sqlite-devel readline-devel tk-devel gdbm-devel db4-devel libpcap-devel xz-devel
    ```

