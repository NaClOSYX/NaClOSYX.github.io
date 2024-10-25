---
title: vue3常用方法
date: '2024-10-22 00:00:00 +0800'
updated: '2024-10-22 00:00:00 +0800'
categories:
  - 博客
  - 前端
tags:
  - 前端
  - vue
  - 常用
author: NaClO
abbrlink: 3525272420
---

### 组件添加name属性

1. vue3.3之前

   ```vue
   <script lang="ts">
   export default {
     name: '',
   }
   </script>
   
   <script setup lang="ts">
   
   </script>
   ```

2. vue3.3之后

   ```vue
   <script setup lang="ts">
   defineOptions({
     name: '',
   })
   </script>
   ```

### 把views目录下全部添加到路由

```typescript
// 读取 views/ 下所有vue文件
const files = import.meta.glob('../views/**/*.vue', {
  import: 'default', // 导入全部
  eager: true, // 同步加载模块
})

Object.keys(files).forEach(key => {
  const name = files[key].name
  const fileName = files[key].__name
  const obj = {
    name: name,
    path: '/' + fileName,
    component: files[key],
  }
  router.addRoute(obj)
})
```

