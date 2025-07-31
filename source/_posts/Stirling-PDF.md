---
title: Stirling-PDF | PDF操作工具
date: '2025-07-17 00:00:00 +0800'
updated: '2025-07-17 00:00:00 +0800'
categories:
  - 博客
  - 工具
tags:
  - 工具
author: NaClO
abbrlink: 542803054
---
1. 介绍 : Stirling PDF是一个使用Docker的强大的、本地托管的基于web的PDF操作工具。它使您能够对PDF文件执行各种操作，包括拆分、合并、转换、重新组织、添加图像、旋转、压缩等。这个本地托管的web应用程序已经发展到包含一套全面的功能，可以满足您的所有PDF要求。

2. GitHub : https://github.com/Stirling-Tools/Stirling-PDF

3. 官网 : https://www.stirlingpdf.com/

## 使用docker compose安装

1. 确保安装了`docker`和`docker compose`

2. 创建目录

   ```bash
   mkdir stirling-pdf
   cd stirling-pdf
   
   mkdir StirlingPDF
   mkdir StirlingPDF/trainingData
   mkdir StirlingPDF/extraConfigs
   mkdir StirlingPDF/customFiles
   mkdir StirlingPDF/logs
   mkdir StirlingPDF/pipeline
   ```

3. 创建`docker-compose.yml`

   ```bash
   touch docker-compose.yml
   ```

4. 编辑`docker-compose.yml`

   ```yml
   version: '3.3'
   services:
     stirling-pdf:
       image: docker.stirlingpdf.com/stirlingtools/stirling-pdf:latest
       ports:
         - '8080:8080'
       volumes:
         - ./StirlingPDF/trainingData:/usr/share/tessdata # Required for extra OCR languages
         - ./StirlingPDF/extraConfigs:/configs
         - ./StirlingPDF/customFiles:/customFiles/
         - ./StirlingPDF/logs:/logs/
         - ./StirlingPDF/pipeline:/pipeline/
       environment:
         - DISABLE_ADDITIONAL_FEATURES=false
         - LANGS=zh_CN
   ```

5. 拉取镜像

   ```bash
   docker compose pull
   ```

6. 下载OCR识别模型

   ```bash
   # 下载中文模型
   wget -P ./StirlingPDF/trainingData https://raw.githubusercontent.com/tesseract-ocr/tessdata/refs/heads/main/chi_sim.traineddata
   # 下载中文竖版模型
   wget -P ./StirlingPDF/trainingData https://raw.githubusercontent.com/tesseract-ocr/tessdata/refs/heads/main/chi_tra_vert.traineddata
   # 下载英文模型
   wget -P ./StirlingPDF/trainingData https://raw.githubusercontent.com/tesseract-ocr/tessdata/refs/heads/main/eng.traineddata
   ```

7. 启动服务

   ```bash
   docker compose up -d
   ```

8. 访问`http://localhost:8080` 

