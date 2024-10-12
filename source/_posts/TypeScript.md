---
title: TypeScript
date: 2024-09-01 00:00:00 +0800
updated: 2024-09-01 00:00:00 +0800
categories: [博客, 配置]
tags: [环境, 配置, 前端] 
author: NaClO
---

## 安装

1. 安装TypeScript

   ```bash
   npm i -g typescript ts-node tslib @types/node 
   ```

2. 创建`tsconfig.json`配置文件

3. `tsconfig.json`文件

   ```json
   {
     "compilerOptions": {
       "target": "esnext",
       "module": "esnext",
       "useDefineForClassFields": true,
       "moduleResolution": "node",
       "strict": true,
       "jsx": "preserve",
       "sourceMap": true,
       "resolveJsonModule": true,
       "esModuleInterop": true,
       "lib": ["esnext", "dom"]
     },
     "include": [
       "src/**/*.ts",
       "src/**/*.d.ts",
       "src/**/*.tsx",
       "src/**/*.vue",
     ]
   }
   ```

4. s