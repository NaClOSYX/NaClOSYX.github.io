---
title: vue-barcode 条形码组件
date: '2022-06-24 00:00:00 +0800'
updated: '2022-06-24 00:00:00 +0800'
categories:
  - 博客
  - 前端
tags:
  - 前端
  - vue
  - 组件
author: NaClO
abbrlink: 4166319461
---

GitHub：``https://github.com/lindell/vue-barcode``

1. 安装

   ```bash
   npm i -s vue-barcode
   ```

2. 引入

   ```js
   import Vue from 'vue'
   import VueBarcode from "vue-barcode";
   
   Vue.component('vue-barcode', VueBarcode);
   ```

3. 使用

   ```vue
   <template>
       <div id="app">
           <vue-barcode
                   value="12345678"
           />
       </div>
   </template>
   
   <script>
   import vueBarcode from "vue-barcode"
   
   export default {
       name: "app",
       components: {
           vueBarcode
       }
   }
   </script>
   ```

4. 属性

   |     属性     |                                类型                                | 是否必填 |      默认值      |                          描述                           |
   | :----------: | :----------------------------------------------------------------: | :------: | :--------------: | :-----------------------------------------------------: |
   |    value     |                           String\|Number                           |   true   |        -         |                         条码值                          |
   |    format    | String[CODE128, EAN/UPC, CODE39, ITF-14, MSI, pharmacode, codebar] |  false   | "auto" (CODE128) |                      条形码的格式                       |
   |    width     |                           String\|Number                           |  false   |        2         |                          宽度                           |
   |    height    |                           String\|Number                           |  false   |       100        |                          高度                           |
   | displayValue |                              Boolean                               |  false   |       true       |                      是否显示文字                       |
   |     text     |                               String                               |  false   |    undefiend     |            显示的文字，如不设置，显示条码值             |
   | fontOptions  |                               String                               |  false   |        ""        |                        字体格式                         |
   |     font     |                               String                               |  false   |   "monospace"    |                        文字字体                         |
   |  textAlign   |                     String[left,center,right]                      |  false   |     "center"     |                      文字对齐方式                       |
   | textPosition |                         String[bottom,top]                         |  false   |     "bottom"     |                        文字位置                         |
   |  textMargin  |                               Number                               |  false   |        2         |                     文字与条码间距                      |
   |   fontSize   |                               Number                               |  false   |        20        |                        字体大小                         |
   |  background  |                         String (CSS color)                         |  false   |    "#ffffff"     |                         背景色                          |
   |  lineColor   |                         String (CSS color)                         |  false   |    "#000000"     |                        线条颜色                         |
   |    margin    |                               Number                               |  false   |        10        |                     二维码周围间距                      |
   |  marginTop   |                               Number                               |  false   |    undefiend     |                                                         |
   | marginBottom |                               Number                               |  false   |    undefiend     |                                                         |
   |  marginLeft  |                               Number                               |  false   |    undefiend     |                                                         |
   | marginRight  |                               Number                               |  false   |    undefiend     |                                                         |
   |     flat     |                              Boolean                               |  false   |      false       |         只针对于EAN8/EAN13, 隐藏凹槽（防护条）          |
   |    ean128    |                          String\|Boolean                           |  false   |      false       | 只针对于CODE128, 将CODE128格式转换为GS1-128/EAN-128格式 |
   |  elementTag  |                       String[svg,canvas,img]                       |  false   |       svg        |                      条码渲染样式                       |


5. 条码格式

   - CODE128

     > CODE128是一种更通用的条形码。它支持所有128个ASCII字符，但也能高效地编码数字。它有三种模式（A/B/C），但可以随时在它们之间切换。CODE128是JsBarcode在未指定其他内容时将选择的默认条形码。

   - EAN/UPC

     > EAN有多种形式，最常用的是EAN-13（GTIN-13），它在全球范围内用于标记产品的标识。
     >
     > JsBarcode支持EAN-13、EAN-8和UPC格式，以及条形码插件EAN-5和EAN-2。

   - CODE39

     > CODE39是一种旧的条形码类型，可以对数字、大写字母和许多特殊字符进行编码（，，，$，/，+，%和空格）。过去，这是一种常见的条形码类型，但如果不是出于遗留原因，建议使用CODE128。

   - ITF-14

     > ITF-14（Interleaved Two of Five）是GS1对*Interleaved 2 of 5*条码的实现，用于编码全球贸易商品编号。ITF-14符号通常用于产品的包装级别，例如一盒24罐汤。ITF-14将始终编码14位数字。
     >
     > ITF-14条码的最后一位是校验和。它通常包含在内，但如果不包含，JsBarcode可以自动为您计算。

   - MSI

     > MSI或Modified Plessey是由MSI Data Corporation开发的条形码，主要用于库存控制、标记仓库环境中的存储容器和货架。支持数字0-9。JsBarcode提供Mod 10、Mod 11、Mod 1010和Mod 1110的自动校验和计算。

   - pharmacode

     > Pharmacode是制药行业使用的条形码。它可以将从3编码到131070。

   - codebar

     > Codabar是一种旧的条形码类型，可以对数字和一些特殊字符（–、$、：、/、+、）进行编码。
     >
     > 您可以将开始和停止字符设置为A、B、C或D，但如果未定义开始和停止字符，则将使用A。

