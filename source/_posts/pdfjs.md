---
title: pdfjs pdf组件
date: 2023-09-15 00:00:00 +0800
categories: [博客, 前端]
tags: [前端, 组件] 
author: NaClO
---

1. GitHub : https://github.com/mozilla/pdf.js

2. 官网 :  https://mozilla.github.io/pdf.js/

3. demo: https://mozilla.github.io/pdf.js/web/viewer.html

4. 兼容ie的最新版 :  [2.7.570](https://github.com/mozilla/pdf.js/releases/download/v2.7.570/pdfjs-2.7.570-es5-dist.zip) 

5. 解压后放在 `static/pdf`目录下，使用iframe方式引入

   ```html
   <iframe
       :src="`./static/pdf/web/viewer.html?file=${pdfUrl}`"
       class="pdf-window"
       width="100%"
       height="100%"
       frameborder="0"
   ></iframe>
   ```

6. 解决电子签章不显示的问题

   - [2.5.207](https://github.com/mozilla/pdf.js/releases/download/v2.5.207/pdfjs-2.5.207-dist.zip) : 批注掉`build/pdf.worker.js`文件中`_this3.setFlags(_util.AnnotationFlag.HIDDEN);`
   - [2.9.359](https://github.com/mozilla/pdf.js/releases/download/v2.9.359/pdfjs-2.9.359-dist.zip)之后的版本: 已经支持了显示电子签章，直接使用

7. 隐藏界面上的一些按钮 : 修改 `web/viewer.js`文件中`webViewerInitialized`方法 在前面添加

   ```javascript
   appConfig.toolbar.presentationModeButton.hidden = true;
   appConfig.toolbar.openFile.hidden = true;
   appConfig.secondaryToolbar.openFileButton.hidden = true;
   appConfig.toolbar.print.hidden = true;
   appConfig.secondaryToolbar.printButton.hidden = true;
   appConfig.toolbar.download.hidden = true;
   appConfig.secondaryToolbar.downloadButton.hidden = true;
   appConfig.toolbar.viewBookmark.hidden = true;
   appConfig.secondaryToolbar.viewBookmarkButton.hidden = true;
   appConfig.secondaryToolbar.toggleButton.hidden = true;
   appConfig.findBar.toggleButton.hidden = true;
   .....
   ```

   

