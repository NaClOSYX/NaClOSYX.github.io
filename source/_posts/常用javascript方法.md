---
title: 常用javascript方法
date: 2022-12-25 00:00:00 +0800
categories: [博客, 前端]
tags: [常用, 前端, JavaScript] 
author: NaClO
---

## 字体相关

### 设置网页根字体

```javascript
document.getElementsByTagName("html")[0].setAttribute("style", "font-size:" + window.innerWidth / 10 + "px")
```

### 获取页面上实际字体大小

```javascript
window.getComputedStyle(document.querySelector('html'),null).getPropertyValue('font-size')
```

### 使页面上的字体大小不随系统设置的字体改变

```javascript
document.getElementsByTagName("html")[0].setAttribute("style", "font-size:" + 16*16/window.getComputedStyle(document.querySelector('html'),null).getPropertyValue('font-size').replace('px','') + "px")
```



## 浏览器版本相关

### 获取浏览器ua

````javascript
var ua = window.navigator.userAgent;
var ua = window.navigator.userAgent.toLowerCase();
````

### 判断浏览器版本

```javascript
function getBrowser() {
    var ua = window.navigator.userAgent;
    var isIE = window.ActiveXObject != undefined && ua.indexOf("MSIE") != -1;
    var isFirefox = ua.indexOf("Firefox") != -1;
    var isOpera = window.opr != undefined;
    var isChrome = ua.indexOf("Chrome") && window.chrome;
    var isSafari = ua.indexOf("Safari") != -1 && ua.indexOf("Version") != -1;
        if (isIE) {
            return "IE";
        } else if (isFirefox) {
            return "Firefox";
        } else if (isOpera) {
            return "Opera";
        } else if (isChrome) {
            return "Chrome";
        } else if (isSafari) {
            return "Safari";
        } else {
            return "Unkown";
        }
    }
```

### 判断是否为ios

```javascript
function isIOS() {
    const ua = window.navigator.userAgent;
    const isiOS = !!ua.match(/\(i[^;]+;( U;)? CPU.+Mac OS X/)
    return isiOS
}
```

### 判断是否为企业微信

```javascript
function isWechat() {
    var ua = window.navigator.userAgent.toLowerCase();
    if (ua.match(/MicroMessenger/i) == "micromessenger" && ua.match(/wxwork/i) == "wxwork") {
        return true;
    }
    return false;
}
```

## url相关

### 获取base URL

```javascript
const getBaseURL = url => url.replace(/[?#].*$/, '')
```

### 判断URL是否绝对

```javascript
const isAbsoluteURL = str => /^[a-z][a-z0-9+.-]*:/.test(str)
```

### 获取url参数作为对象

```javascript
const getURLParameters = url =>
  (url.match(/([^?=&]+)(=([^&]*))/g) || []).reduce(
    (a, v) => (
      (a[v.slice(0, v.indexOf('='))] = v.slice(v.indexOf('=') + 1)), a
    ),
    {}
  );
```

## 硬件相关

### 获取选中文字

```javascript
const getSelectedText = () => window.getSelection().toString()
```

### 复制文字到剪贴板

```javascript
const copyToClipboard = str => {
  if (navigator && navigator.clipboard && navigator.clipboard.writeText)
    return navigator.clipboard.writeText(str)
  return Promise.reject('The Clipboard API is not available.')
};
```

### 切换全屏模式

```javascript
const fullscreen = (mode = true, el = 'body') =>
  mode ? document.querySelector(el).requestFullscreen() : document.exitFullscreen();
```

### 查看用户的首选语言

```javascript
const detectLanguage = (defaultLang = 'en-US') =>
  navigator.language || (Array.isArray(navigator.languages) && navigator.languages[0]) || defaultLang
```

### 查看设备是否支持触屏操作

```javascript
const supportsTouchEvents = () =>
  window && 'ontouchstart' in window;
```

### 移动端判断横竖屏

```javascript
window.addEventListener('orientationchange', function(event){
    if ( window.orientation == 180 || window.orientation==0 ) {
        alert("竖屏");
    }
    if( window.orientation == 90 || window.orientation == -90 ) {
        alert("横屏");
    }
});
```

## 其他

### 生成UUID

```javascript
const UUIDGeneratorBrowser = () =>
  ([1e7] + -1e3 + -4e3 + -8e3 + -1e11).replace(/[018]/g, c =>
    (
      c ^ (crypto.getRandomValues(new Uint8Array(1))[0] & (15 >> (c / 4)))
    ).toString(16)
  );
```

### 禁止*鼠标右键*和*F12*

```javascript
<script>
    //禁止鼠标 右键
    document.oncontextmenu = function () {
        alert('禁止右键');
        return false;
    }
    // 禁止 F12 快捷键
    document.onkeydown = document.onkeyup = document.onkeypress = function () {
        if (window.event.keyCode == 123) {
            alert("F12已禁用");
            window.event.returnValue = false;
        }
    }
</script>
```

