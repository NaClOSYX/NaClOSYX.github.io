---
title: vue-drag-resize 拖拽组件
date: 2022-06-22 00:00:00 +0800
updated: 2022-06-22 00:00:00 +0800
categories: [博客, 前端]
tags: [前端, vue, 组件] 
author: NaClO
---

GitHub：``https://github.com/kirillmurashov/vue-drag-resize``

1. 安装

   ```bash
   npm i -s vue-drag-resize
   ```

2. 引入

   ```js
   import Vue from 'vue'
   import VueDragResize from 'vue-drag-resize'
   
   Vue.component('vue-drag-resize', VueDragResize)
   ```

3. 使用

   ```vue
   <template>
       <div id="app">
           <VueDragResize :isActive="true" :w="200" :h="200" v-on:resizing="resize" v-on:dragging="resize">
               <h3>Hello World!</h3>
               <p>{{ top }} х {{ left }} </p>
               <p>{{ width }} х {{ height }}</p>
           </VueDragResize>
       </div>
   </template>
   
   <script>
       import VueDragResize from 'vue-drag-resize';
   
       export default {
           name: 'app',
   
           components: {
               VueDragResize
           },
   
           data() {
               return {
                   width: 0,
                   height: 0,
                   top: 0,
                   left: 0
               }
           },
   
           methods: {
               resize(newRect) {
                   this.width = newRect.width;
                   this.height = newRect.height;
                   this.top = newRect.top;
                   this.left = newRect.left;
               }
           }
       }
   </script>
   ```

4. 属性

   |         属性          |         类型          | 是否必填 |                      默认值                      |                                 描述                                 |
   | :-------------------: | :-------------------: | :------: | :----------------------------------------------: | :------------------------------------------------------------------: |
   |       isActive        |        Boolean        |  false   |                      false                       |                          是否应处于活动状态                          |
   |      isDraggable      |        Boolean        |  false   |                       true                       |                               能否拖拽                               |
   |      isResizable      |        Boolean        |  false   |                       true                       |                               能否缩放                               |
   |      aspectRatio      |        Boolean        |  false   |                      false                       |                             等比缩放(坑)                             |
   |         axis          | String[x,y,both,none] |  false   |                       both                       |                             可拖动的方向                             |
   |           w           |    Number\|String     |  false   |                       200                        |                               初始宽度                               |
   |           h           |    Number\|String     |  false   |                       200                        |                               初始高度                               |
   |         minw          |        Number         |  false   |                        50                        |                               最小宽度                               |
   |         minh          |        Number         |  false   |                        50                        |                               最小高度                               |
   |           x           |        Number         |  false   |                        0                         |                              初始X位置                               |
   |           y           |        Number         |  false   |                        0                         |                              初始Y位置                               |
   |           z           |    Number\|String     |  false   |                       auto                       |                                 层级                                 |
   |       stickSize       |        Number         |  false   |                        8                         |                            拖拽节点的大小                            |
   |        sticks         |         Array         |  false   | ['tl', 'tm', 'tr', 'mr', 'br', 'bm', 'bl', 'ml'] |                    定义句柄数组以限制元素大小调整                    |
   |      snapToGrid       |        Boolean        |  false   |                      false                       |                             是否贴合网格                             |
   |         gridX         |      Number(≥0)       |  false   |                        50                        |                             定义网格宽度                             |
   |         gridY         |      Number(≥0)       |  false   |                        50                        |                             定义网格高度                             |
   |   parentLimitation    |        Boolean        |  false   |                      false                       |                    将组件更改的范围限制为其父大小                    |
   | preventActiveBehavior |        Boolean        |  false   |                      false                       |            通过单击组件并单击组件区域外部来禁用组件的行为            |
   |        parentH        |      Number(≥0)       |  false   |                        0                         |                      父元素的初始高度, 指定边界                      |
   |        parentW        |      Number(≥0)       |  false   |                        0                         |                      父元素的初始宽度, 指定边界                      |
   |     parentScaleX      |        Number         |  false   |                        1                         | 定义初始水平比例或父元素。父级的transform:scale（）css定义中的值相同 |
   |     parentScaleY      |        Number         |  false   |                        1                         | 定义初始垂直比例或父元素。父级的transform:scale（）css定义中的值相同 |
   |      dragHandle       |        String         |  false   |                                                  |     定义应该用于拖动组件的选择器，即可以触发拖拽事件的元素选择器     |
   |      dragCancel       |        String         |  false   |                                                  | 定义应该用于防止拖动初始化的选择器，即不可以触发拖拽事件的元素选择器 |
   |     contentClass      |        String         |  false   |                                                  |                               添加类名                               |

5. 方法

   |   方法名    |                  说明                  |              参数              |
   | :---------: | :------------------------------------: | :----------------------------: |
   |   clicked   |             单击组件时调用             |             event              |
   |  activated  |   单击组件时调用，激活组件，显示句柄   |               -                |
   | deactivated | 单击组件外部时调用，停用组件，隐藏句柄 |               -                |
   |  resizing   |          当组件调整大小时调用          | object{left, top,width,height} |
   | resizestop  |        当组件停止调整大小时调用        | object{left, top,width,height} |
   |  dragging   |            当拖动组件时调用            | object{left, top,width,height} |
   |  dragstop   |          当组件停止拖动时调用          | object{left, top,width,height} |

