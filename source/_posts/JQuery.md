---
title: JQuery
date: '2020-06-10 00:00:00 +0800'
updated: '2020-06-10 00:00:00 +0800'
categories:
  - 博客
  - 学习
tags:
  - 学习
  - 前端
  - JavaScript
author: NaClO
abbrlink: 1012917595
---

## 简介

### 百度百科

* jQuery是一个==快速==、==简洁==的==JavaScript框架==，是继Prototype之后又一个优秀的JavaScript代码库（*或JavaScript框架*）。jQuery设计的宗旨是==“write Less，Do More”==，即倡导写更少的代码，做更多的事情。它封装JavaScript常用的功能代码，提供一种简便的JavaScript设计模式，优化HTML文档操作、事件处理、动画设计和Ajax交互。
* jQuery的核心特性可以总结为：具有独特的链式语法和短小清晰的多功能接口；具有高效灵活的css选择器，并且可对CSS选择器进行扩展；拥有便捷的插件扩展机制和丰富的插件。jQuery兼容各种主流浏览器，如IE 6.0+、FF 1.5+、Safari 2.0+、Opera 9.0+等

### 官网

* 官网：https://jquery.com/

* 菜鸟教程：https://www.runoob.com/jquery/jquery-tutorial.html

* API中文手册：https://jquery.cuishifeng.cn/

### 如何下载

* 下载地址

  https://jquery.com/download/

  * 完全版
    * 生产版本： https://code.jquery.com/jquery-3.5.1.min.js
    * 开发版本：https://code.jquery.com/jquery-3.5.1.js
  * 不带ajax和effects的版本
    * 生产版本： https://code.jquery.com/jquery-3.5.1.slim.min.js
    * 开发版本：https://code.jquery.com/jquery-3.5.1.slim.js

  html页面中引入

  ````html
  <script type="text/javascript" src="js/jquery-3.5.1.min.js"></script>
  ````

* cdn

````html
<!-- 开发版（未压缩） -->
<script src="https://cdn.bootcdn.net/ajax/libs/jquery/3.5.1/jquery.js"></script>
<!-- 生产版（压缩版） -->
<script src="https://cdn.bootcdn.net/ajax/libs/jquery/3.5.1/jquery.min.js"></script>
````

## JQuery的使用

### JQuery语法

* jQuery 语法是为 HTML 元素的选取编制的，可以对元素执行某些操作。

* 基础语法是：`$(selector).action()`
  * 美元符号定义 jQuery
  * 选择符（selector）"查询"和"查找" HTML 元素
  * jQuery 的 action() 执行对元素的操作

### 选择器

* 选择器是jQuery的核心。
* 总结就是`#id .class`

1. ID选择器

   ````javascript
   //原生js写法
   document.getElementById("id);
   //JQuery写法
   $("#id);
   ````

2. 类选择器
   ````javascript
   //原生js写法
   document.getElementsByClassName("id");
   //JQuery写法
   $(".class");
   ````
   
3. 标签选择器

      ````javascript
   //原生js写法
   document.document.getElementsByTagName("id");
   //JQuery写法
   $("tag");
      ````

4. 属性选择器

   ````javascript
   $("[href]") //选取所有带有 href 属性的元素。
   $("[href='#']") //选取所有带有 href 值等于 "#" 的元素。
   $("[href!='#']") //选取所有带有 href 值不等于 "#" 的元素。
   $("[href$='.jpg']") //选取所有 href 值以 ".jpg" 结尾的元素。
   ````

5. 选择文档中所有的标签

   ````javascript
   $("*");
   ````

6. 其他选择器

   ````javascript
   $("A B");//查找A元素下面的所有子节点，包括非直接子节点。
   $("A > B");//查找A元素下面的直接B子节点。
   $("A + B");//查找A元素后面的兄弟节点,包括非直接子节点。
   $("A ~ B");//查找A元素后面的兄弟节点,不包括非直接子节点。
   next(); //当前元素之后的紧邻着的第一个兄弟元素(下一个)。
   nextAll();//当前元素之后的所有兄弟元素。
   prev();//当前元素之前的紧邻着的兄弟元素(上一个) .
   prevA1l();//当前元素之前的所有兄弟元素.
   siblings();//当前元素的所有兄弟元素。
   ````

7. 所有选择

   | 选择器                                                                                              | 实例                       | 选取                                       |
   | :-------------------------------------------------------------------------------------------------- | :------------------------- | :----------------------------------------- |
   | [*](https://www.w3school.com.cn/jquery/selector_all.asp)                                            | $("*")                     | 所有元素                                   |
   | [#*id*](https://www.w3school.com.cn/jquery/selector_id.asp)                                         | $("#lastname")             | id="lastname" 的元素                       |
   | [.*class*](https://www.w3school.com.cn/jquery/selector_class.asp)                                   | $(".intro")                | 所有 class="intro" 的元素                  |
   | [*element*](https://www.w3school.com.cn/jquery/selector_element.asp)                                | $("p")                     | 所有 <p> 元素                              |
   | .*class*.*class*                                                                                    | $(".intro.demo")           | 所有 class="intro" 且 class="demo" 的元素  |
   |                                                                                                     |                            |                                            |
   | [:first](https://www.w3school.com.cn/jquery/selector_first.asp)                                     | $("p:first")               | 第一个 <p> 元素                            |
   | [:last](https://www.w3school.com.cn/jquery/selector_last.asp)                                       | $("p:last")                | 最后一个 <p> 元素                          |
   | [:even](https://www.w3school.com.cn/jquery/selector_even.asp)                                       | $("tr:even")               | 所有偶数 <tr> 元素                         |
   | [:odd](https://www.w3school.com.cn/jquery/selector_odd.asp)                                         | $("tr:odd")                | 所有奇数 <tr> 元素                         |
   |                                                                                                     |                            |                                            |
   | [:eq(*index*)](https://www.w3school.com.cn/jquery/selector_eq.asp)                                  | $("ul li:eq(3)")           | 列表中的第四个元素（index 从 0 开始）      |
   | [:gt(*no*)](https://www.w3school.com.cn/jquery/selector_gt.asp)                                     | $("ul li:gt(3)")           | 列出 index 大于 3 的元素                   |
   | [:lt(*no*)](https://www.w3school.com.cn/jquery/selector_lt.asp)                                     | $("ul li:lt(3)")           | 列出 index 小于 3 的元素                   |
   | :not(*selector*)                                                                                    | $("input:not(:empty)")     | 所有不为空的 input 元素                    |
   |                                                                                                     |                            |                                            |
   | [:header](https://www.w3school.com.cn/jquery/selector_header.asp)                                   | $(":header")               | 所有标题元素 <h1> - <h6>                   |
   | [:animated](https://www.w3school.com.cn/jquery/selector_animated.asp)                               |                            | 所有动画元素                               |
   |                                                                                                     |                            |                                            |
   | [:contains(*text*)](https://www.w3school.com.cn/jquery/selector_contains.asp)                       | $(":contains('W3School')") | 包含指定字符串的所有元素                   |
   | [:empty](https://www.w3school.com.cn/jquery/selector_empty.asp)                                     | $(":empty")                | 无子（元素）节点的所有元素                 |
   | :hidden                                                                                             | $("p:hidden")              | 所有隐藏的 <p> 元素                        |
   | [:visible](https://www.w3school.com.cn/jquery/selector_visible.asp)                                 | $("table:visible")         | 所有可见的表格                             |
   |                                                                                                     |                            |                                            |
   | s1,s2,s3                                                                                            | $("th,td,.intro")          | 所有带有匹配选择的元素                     |
   |                                                                                                     |                            |                                            |
   | [[*attribute*\]](https://www.w3school.com.cn/jquery/selector_attribute.asp)                         | $("[href]")                | 所有带有 href 属性的元素                   |
   | [[*attribute*=*value*\]](https://www.w3school.com.cn/jquery/selector_attribute_equal_value.asp)     | $("[href='#']")            | 所有 href 属性的值等于 "#" 的元素          |
   | [[*attribute*!=*value*\]](https://www.w3school.com.cn/jquery/selector_attribute_notequal_value.asp) | $("[href!='#']")           | 所有 href 属性的值不等于 "#" 的元素        |
   | [[*attribute*$=*value*\]](https://www.w3school.com.cn/jquery/selector_attribute_end_value.asp)      | $("[href$='.jpg']")        | 所有 href 属性的值包含以 ".jpg" 结尾的元素 |
   |                                                                                                     |                            |                                            |
   | [:input](https://www.w3school.com.cn/jquery/selector_input.asp)                                     | $(":input")                | 所有 <input> 元素                          |
   | [:text](https://www.w3school.com.cn/jquery/selector_input_text.asp)                                 | $(":text")                 | 所有 type="text" 的 <input> 元素           |
   | [:password](https://www.w3school.com.cn/jquery/selector_input_password.asp)                         | $(":password")             | 所有 type="password" 的 <input> 元素       |
   | [:radio](https://www.w3school.com.cn/jquery/selector_input_radio.asp)                               | $(":radio")                | 所有 type="radio" 的 <input> 元素          |
   | [:checkbox](https://www.w3school.com.cn/jquery/selector_input_checkbox.asp)                         | $(":checkbox")             | 所有 type="checkbox" 的 <input> 元素       |
   | [:submit](https://www.w3school.com.cn/jquery/selector_input_submit.asp)                             | $(":submit")               | 所有 type="submit" 的 <input> 元素         |
   | [:reset](https://www.w3school.com.cn/jquery/selector_input_reset.asp)                               | $(":reset")                | 所有 type="reset" 的 <input> 元素          |
   | [:button](https://www.w3school.com.cn/jquery/selector_input_button.asp)                             | $(":button")               | 所有 type="button" 的 <input> 元素         |
   | [:image](https://www.w3school.com.cn/jquery/selector_input_image.asp)                               | $(":image")                | 所有 type="image" 的 <input> 元素          |
   | [:file](https://www.w3school.com.cn/jquery/selector_input_file.asp)                                 | $(":file")                 | 所有 type="file" 的 <input> 元素           |
   |                                                                                                     |                            |                                            |
   | [:enabled](https://www.w3school.com.cn/jquery/selector_input_enabled.asp)                           | $(":enabled")              | 所有激活的 input 元素                      |
   | [:disabled](https://www.w3school.com.cn/jquery/selector_input_disabled.asp)                         | $(":disabled")             | 所有禁用的 input 元素                      |
   | [:selected](https://www.w3school.com.cn/jquery/selector_input_selected.asp)                         | $(":selected")             | 所有被选取的 input 元素                    |
   | [:checked](https://www.w3school.com.cn/jquery/selector_input_checked.asp)                           | $(":checked")              | 所有被选中的 input 元素                    |

### 文档操作

* jQuery 中非常重要的部分，就是操作 DOM 的能力。

* jQuery 提供一系列与 DOM 相关的方法，这使访问和操作元素和属性变得很容易。

1. 获得内容 - text()、html() 以及 val()

   - text() - 设置或返回所选元素的文本内容
   - html() - 设置或返回所选元素的内容（包括 HTML 标记）
   - val() - 设置或返回表单字段的值

2. 所有操作

   | 方法                                                                               | 描述                                                   |
   | :--------------------------------------------------------------------------------- | :----------------------------------------------------- |
   | [addClass()](https://www.w3school.com.cn/jquery/attributes_addclass.asp)           | 向匹配的元素添加指定的类名。                           |
   | [after()](https://www.w3school.com.cn/jquery/manipulation_after.asp)               | 在匹配的元素之后插入内容。                             |
   | [append()](https://www.w3school.com.cn/jquery/manipulation_append.asp)             | 向匹配元素集合中的每个元素结尾插入由参数指定的内容。   |
   | [appendTo()](https://www.w3school.com.cn/jquery/manipulation_appendto.asp)         | 向目标结尾插入匹配元素集合中的每个元素。               |
   | [attr()](https://www.w3school.com.cn/jquery/attributes_attr.asp)                   | 设置或返回匹配元素的属性和值。                         |
   | [before()](https://www.w3school.com.cn/jquery/manipulation_before.asp)             | 在每个匹配的元素之前插入内容。                         |
   | [clone()](https://www.w3school.com.cn/jquery/manipulation_clone.asp)               | 创建匹配元素集合的副本。                               |
   | [detach()](https://www.w3school.com.cn/jquery/manipulation_detach.asp)             | 从 DOM 中移除匹配元素集合。                            |
   | [empty()](https://www.w3school.com.cn/jquery/manipulation_empty.asp)               | 删除匹配的元素集合中所有的子节点。                     |
   | [hasClass()](https://www.w3school.com.cn/jquery/attributes_hasclass.asp)           | 检查匹配的元素是否拥有指定的类。                       |
   | [html()](https://www.w3school.com.cn/jquery/manipulation_html.asp)                 | 设置或返回匹配的元素集合中的 HTML 内容。               |
   | [insertAfter()](https://www.w3school.com.cn/jquery/manipulation_insertafter.asp)   | 把匹配的元素插入到另一个指定的元素集合的后面。         |
   | [insertBefore()](https://www.w3school.com.cn/jquery/manipulation_insertbefore.asp) | 把匹配的元素插入到另一个指定的元素集合的前面。         |
   | [prepend()](https://www.w3school.com.cn/jquery/manipulation_prepend.asp)           | 向匹配元素集合中的每个元素开头插入由参数指定的内容。   |
   | [prependTo()](https://www.w3school.com.cn/jquery/manipulation_perpendto.asp)       | 向目标开头插入匹配元素集合中的每个元素。               |
   | [remove()](https://www.w3school.com.cn/jquery/manipulation_remove.asp)             | 移除所有匹配的元素。                                   |
   | [removeAttr()](https://www.w3school.com.cn/jquery/attributes_removeattr.asp)       | 从所有匹配的元素中移除指定的属性。                     |
   | [removeClass()](https://www.w3school.com.cn/jquery/attributes_removeclass.asp)     | 从所有匹配的元素中删除全部或者指定的类。               |
   | [replaceAll()](https://www.w3school.com.cn/jquery/manipulation_replaceall.asp)     | 用匹配的元素替换所有匹配到的元素。                     |
   | [replaceWith()](https://www.w3school.com.cn/jquery/manipulation_replacewith.asp)   | 用新内容替换匹配的元素。                               |
   | [text()](https://www.w3school.com.cn/jquery/manipulation_text.asp)                 | 设置或返回匹配元素的内容。                             |
   | [toggleClass()](https://www.w3school.com.cn/jquery/attributes_toggleclass.asp)     | 从匹配的元素中添加或删除一个类。                       |
   | [unwrap()](https://www.w3school.com.cn/jquery/manipulation_unwrap.asp)             | 移除并替换指定元素的父元素。                           |
   | [val()](https://www.w3school.com.cn/jquery/attributes_val.asp)                     | 设置或返回匹配元素的值。                               |
   | [wrap()](https://www.w3school.com.cn/jquery/manipulation_wrap.asp)                 | 把匹配的元素用指定的内容或元素包裹起来。               |
   | [wrapAll()](https://www.w3school.com.cn/jquery/manipulation_wrapall.asp)           | 把所有匹配的元素用指定的内容或元素包裹起来。           |
   | [wrapinner()](https://www.w3school.com.cn/jquery/manipulation_wrapinner.asp)       | 将每一个匹配的元素的子内容用指定的内容或元素包裹起来。 |

### 事件

* 事件方法会触发匹配元素的事件，或将函数绑定到所有匹配元素的某个事件。

* 用法

  ````html
  <script>
      $(function () {
      	$('selector').on('action', function () {
              ......
      	});
      });
  </script>
  ````

  简单写：

  ````html
  <script>
      $(function () {
          $('selector').action(function () {
  			......
          });
      });
  </script>
  ````

1. 鼠标事件

   1. click: 鼠标单击时触发
   2. dblclick：鼠标双击时触发
   3. mouseenter：鼠标进入时触发
   4. mouseleave：鼠标移出时触发
   5. mousemove：鼠标在DOM内部移动时触发
   6. hover：鼠标进入和退出时触发两个函数，相当于mouseenter加上mouseleave

2. 键盘事件

   1. keydown：键盘按下时触发
   2.  keyup：键盘松开时触发
   3. keypress：按一次键后触发

3. 其他事件

   1. focus：当DOM获得焦点时触发
   2. blur：当DOM失去焦点时触发
   3. change：当内容改变时触发
   4. submit：当提交时触发
   5.  ready：当页面被载入并且DOM树完成初始化后触发

4. 所有事件

   | 方法                                                                                          | 描述                                                          |
   | :-------------------------------------------------------------------------------------------- | :------------------------------------------------------------ |
   | [bind()](https://www.w3school.com.cn/jquery/event_bind.asp)                                   | 向匹配元素附加一个或更多事件处理器                            |
   | [blur()](https://www.w3school.com.cn/jquery/event_blur.asp)                                   | 触发、或将函数绑定到指定元素的 blur 事件                      |
   | [change()](https://www.w3school.com.cn/jquery/event_change.asp)                               | 触发、或将函数绑定到指定元素的 change 事件                    |
   | [click()](https://www.w3school.com.cn/jquery/event_click.asp)                                 | 触发、或将函数绑定到指定元素的 click 事件                     |
   | [dblclick()](https://www.w3school.com.cn/jquery/event_dblclick.asp)                           | 触发、或将函数绑定到指定元素的 double click 事件              |
   | [delegate()](https://www.w3school.com.cn/jquery/event_delegate.asp)                           | 向匹配元素的当前或未来的子元素附加一个或多个事件处理器        |
   | [die()](https://www.w3school.com.cn/jquery/event_die.asp)                                     | 移除所有通过 live() 函数添加的事件处理程序。                  |
   | [error()](https://www.w3school.com.cn/jquery/event_error.asp)                                 | 触发、或将函数绑定到指定元素的 error 事件                     |
   | [event.isDefaultPrevented()](https://www.w3school.com.cn/jquery/event_isdefaultprevented.asp) | 返回 event 对象上是否调用了 event.preventDefault()。          |
   | [event.pageX](https://www.w3school.com.cn/jquery/event_pagex.asp)                             | 相对于文档左边缘的鼠标位置。                                  |
   | [event.pageY](https://www.w3school.com.cn/jquery/event_pagey.asp)                             | 相对于文档上边缘的鼠标位置。                                  |
   | [event.preventDefault()](https://www.w3school.com.cn/jquery/event_preventdefault.asp)         | 阻止事件的默认动作。                                          |
   | [event.result](https://www.w3school.com.cn/jquery/event_result.asp)                           | 包含由被指定事件触发的事件处理器返回的最后一个值。            |
   | [event.target](https://www.w3school.com.cn/jquery/event_target.asp)                           | 触发该事件的 DOM 元素。                                       |
   | [event.timeStamp](https://www.w3school.com.cn/jquery/event_timeStamp.asp)                     | 该属性返回从 1970 年 1 月 1 日到事件发生时的毫秒数。          |
   | [event.type](https://www.w3school.com.cn/jquery/event_type.asp)                               | 描述事件的类型。                                              |
   | [event.which](https://www.w3school.com.cn/jquery/event_which.asp)                             | 指示按了哪个键或按钮。                                        |
   | [focus()](https://www.w3school.com.cn/jquery/event_focus.asp)                                 | 触发、或将函数绑定到指定元素的 focus 事件                     |
   | [keydown()](https://www.w3school.com.cn/jquery/event_keydown.asp)                             | 触发、或将函数绑定到指定元素的 key down 事件                  |
   | [keypress()](https://www.w3school.com.cn/jquery/event_keypress.asp)                           | 触发、或将函数绑定到指定元素的 key press 事件                 |
   | [keyup()](https://www.w3school.com.cn/jquery/event_keyup.asp)                                 | 触发、或将函数绑定到指定元素的 key up 事件                    |
   | [live()](https://www.w3school.com.cn/jquery/event_live.asp)                                   | 为当前或未来的匹配元素添加一个或多个事件处理器                |
   | [load()](https://www.w3school.com.cn/jquery/event_load.asp)                                   | 触发、或将函数绑定到指定元素的 load 事件                      |
   | [mousedown()](https://www.w3school.com.cn/jquery/event_mousedown.asp)                         | 触发、或将函数绑定到指定元素的 mouse down 事件                |
   | [mouseenter()](https://www.w3school.com.cn/jquery/event_mouseenter.asp)                       | 触发、或将函数绑定到指定元素的 mouse enter 事件               |
   | [mouseleave()](https://www.w3school.com.cn/jquery/event_mouseleave.asp)                       | 触发、或将函数绑定到指定元素的 mouse leave 事件               |
   | [mousemove()](https://www.w3school.com.cn/jquery/event_mousemove.asp)                         | 触发、或将函数绑定到指定元素的 mouse move 事件                |
   | [mouseout()](https://www.w3school.com.cn/jquery/event_mouseout.asp)                           | 触发、或将函数绑定到指定元素的 mouse out 事件                 |
   | [mouseover()](https://www.w3school.com.cn/jquery/event_mouseover.asp)                         | 触发、或将函数绑定到指定元素的 mouse over 事件                |
   | [mouseup()](https://www.w3school.com.cn/jquery/event_mouseup.asp)                             | 触发、或将函数绑定到指定元素的 mouse up 事件                  |
   | [one()](https://www.w3school.com.cn/jquery/event_one.asp)                                     | 向匹配元素添加事件处理器。每个元素只能触发一次该处理器。      |
   | [ready()](https://www.w3school.com.cn/jquery/event_ready.asp)                                 | 文档就绪事件（当 HTML 文档就绪可用时）                        |
   | [resize()](https://www.w3school.com.cn/jquery/event_resize.asp)                               | 触发、或将函数绑定到指定元素的 resize 事件                    |
   | [scroll()](https://www.w3school.com.cn/jquery/event_scroll.asp)                               | 触发、或将函数绑定到指定元素的 scroll 事件                    |
   | [select()](https://www.w3school.com.cn/jquery/event_select.asp)                               | 触发、或将函数绑定到指定元素的 select 事件                    |
   | [submit()](https://www.w3school.com.cn/jquery/event_submit.asp)                               | 触发、或将函数绑定到指定元素的 submit 事件                    |
   | [toggle()](https://www.w3school.com.cn/jquery/event_toggle.asp)                               | 绑定两个或多个事件处理器函数，当发生轮流的 click 事件时执行。 |
   | [trigger()](https://www.w3school.com.cn/jquery/event_trigger.asp)                             | 所有匹配元素的指定事件                                        |
   | [triggerHandler()](https://www.w3school.com.cn/jquery/event_triggerhandler.asp)               | 第一个被匹配元素的指定事件                                    |
   | [unbind()](https://www.w3school.com.cn/jquery/event_unbind.asp)                               | 从匹配元素移除一个被添加的事件处理器                          |
   | [undelegate()](https://www.w3school.com.cn/jquery/event_undelegate.asp)                       | 从匹配元素移除一个被添加的事件处理器，现在或将来              |
   | [unload()](https://www.w3school.com.cn/jquery/event_unload.asp)                               | 触发、或将函数绑定到指定元素的 unload 事件                    |

### Ajax

* AJAX 是与服务器交换数据的艺术，它在不重载全部页面的情况下，实现了对部分网页的更新。
* 什么是 AJAX？
  * AJAX = 异步 JavaScript 和 XML（Asynchronous JavaScript and XML）。
  * 简短地说，在不重载整个网页的情况下，AJAX 通过后台加载数据，并在网页上进行显示。

* 用法

  ````javascript
  $.ajax({
      type: "POST",//请求方式，post或者get
      url: "/aaa",//请求的url
      data: {key:value},//传的参数，key:value,多个参数用逗号隔开
      dataType: "json",//返回值的类型
      success: function (data) {//请求成功处理
          console.log("请求成功")
      },
      error: function (data) {//请求异常处理
          console.log("请求异常")
      }
  });
  ````

  