---
title: HTML
date: 2020-06-10 00:00:00 +0800
updated: 2020-06-10 00:00:00 +0800
categories: [博客, 前端]
tags: [学习, 前端, HTML] 
author: NaClO
---

**HTML**是<u>*htyper text markup language*</u> 的缩写，即超文本标记语言。

**HTML基础模板**

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8" />
		<title></title>
	</head>
	<body>
		
	</body>
</html>
```

**`<!DOCEYPE HTML>`**

> `<!DOCTYPE> `声明必须位于 HTML5 文档中的第一行，也就是位于`<html>` 标签之前。该标签告知浏览器文档所使用的 HTML 规范。
>
> doctype 声明不属于 HTML 标签；它是一条指令，告诉浏览器编写页面所用的标记的版本。

## 标签

* 标签是由一对尖括号包裹的单词构成 例如: `<html>` 
* 标签不区分大小写，`<html>` 和 `<HTML>` 是一样的
* 标签分为两部分: 开始标签`<a>` 和 结束标签`</a>`. 两个标签之间的部分 我们叫做标签体
* 有些标签功能比较简单，使用一个标签即可.这种标签叫做自闭和标签.例如: `<br/><hr/><input/><img/>`
* 标签可以嵌套.但是不能交叉嵌套. `<a><b></a></b>`这样就不对
* 标签的属性通常是以键值对形式出现的. 例如 name="nick"
* 标签的属性只能出现在**开始标签**或**自闭和标签**中
* 标签的属性名字全部小写，属性值必须使用双引号或单引号包裹，例如`name="nick"`
* 如果属性值和属性名完全一样，直接写属性名即可，例如`readonly`

### 常用标签

> `<html>`：定义 HTML 文档。

* 此元素可告知浏览器其自身是一个 HTML 文档。
* `<html> `与 `</html>` 标签限定了文档的开始点和结束点，在它们之间是文档的头部和主体。

> `<head>`：定义关于文档的信息。

* `<head>`元素是所有头部元素的容器。
* `<head>`元素必须包含文档的标题，可以包含脚本、样式、meta 信息以及其他更多的信息。

> `<title>`：定义文档的标题。

* 浏览器会以特殊的方式来使用标题，并且通常把它放置在浏览器窗口的标题栏或状态栏上。同样，当把文档加入用户的链接列表或者收藏夹或书签列表时，标题将成为该文档链接的默认名称。

> `<meta>`：定义关于 HTML 文档的元信息。

* 属性`content` 定义与`http-equiv`或`name`属性相关的元信息，是必要的属性。

* 属性`http-equiv `把`content`属性值关联到http头部。
  * Content-Type（浏览器接受的文档类型，一般是text/html）
  * refresh（网页刷新，以秒为单位）
  * expires（设定网页到期时间，一旦过期，必须到服务器上重传）
* 属性`name` 把`content`属性关联到一个名称。
  * keywords（搜索关键字，用于搜索引擎抓取信息的显示）
  * description（搜索到网站后显示的网页内容简描述）
  * author（站点制作者信息）
  * generator（用以说明生成工具）

> `<base>`：定义页面中所有链接的默认地址或默认目标。

* 通常情况下，浏览器会从当前文档的 URL 中提取相应的元素来填写相对 URL 中的空白。

* 使用`<base>`标签可以改变这一点。浏览器随后将不再使用当前文档的 URL，而使用指定的基本 URL 来解析所有的相对 URL。
* `href='URL'`：规定页面中所有相对链接的基准 URL。

> `<link>`：定义文档与外部资源的关系。

> `<style>`：定义文档的样式信息。

> `<script>`：定义客户端脚本。

> `<body>`：定义文档的主体。

> `<div>`：定义文档中的节。

* 定义文档中的分区或节。

* 把文档分割为独立的、不同的部分。它可以用作严格的组织工具，并且不使用任何格式与其关联。

  ```html
  <div style="color:#00FF00">
    <h3>This is a header</h3>
    <p>This is a paragraph.</p>
  </div>
  ```

> `<a>`：定义超链接标签。

* `href`超链接地址。可以是Web上任意资源，包括图片，网页，样式，脚本文件等。`href="#“`时，表示被链接页面就是当前页面。

  ```html
  # 跳转网页
  <a href="">a</a>
  ```

* `target`文档打开时要显示的目标位置。属性值一般有：blank（新窗口中打开）、self（默认，在超链接所在的容器中打开）、parent（在超链接的父容器中打开）、top（整个容器中打开）、name（框架名称）。

* `name`锚记名称。作用：跳转到文档的某个地方。返回首页。

  ```html
  # 跳转锚记书签名称
  <a name="top"><h3>Top！</h3></a>
  <div style="height：800px"></div>
  <a href="#top">top</a>
  ```

> `<img>`：定义图像。

* `src`图片地址。

* `title`鼠标悬浮在图片上的文字。

* `alt`图片找不到时要替换的文字。如果图片资源使用的是外网资源，则不会显示要替换的文字。如果使用的是本网站的资源（相对路径给出），则找不到图片时会显示替换的文字，并保留图片设置的宽高结构。

* `align`图片周围文字的垂直对齐情况。常用的属性值有：top（与图片的顶部对齐）、middle（与图片的中部对齐）、bottom（默认，与图片的底部对齐）。

* `width`图片的宽

* `height`图片的高 (宽高两个属性只用一个会自动等比缩放)。

  ```html
  <img src="http://images.cnblogs.com/cnblogs_com/suoning/845162/o_ns.png" alt="图片加载失败。。。" title="The knife girl, kiss"/>
  ```

#### 基本标签

> `<h1>~<h6>`：定义HTML标题。

* `<h1>`定义最大的标题。`<h6>`定义最小的标题。

* <h1>h1</h1><h2>h2</h2><h3>h3</h3><h4>h4</h4><h5>h5</h5><h6>h6</h6>

> `<b>`定义粗体字。

> `<strong>`定义强调文本。

> `<em>`定义强调文本。

> `<i>`定义斜体字。

> `<u>`定义下划线文本。

> `<sup>`定义上标文本。

> `<sub>`定义下标文本。

> `<strike>`定义加删除线文本。

> `<p>`：定义段落

> `<span>`：定义文档中的节。

> `<br>`：定义一个简单的换行符。

* `<br>`是空标签，建议使用`<br/>`。

> `<hr>`：定义水平分割线。

* 在HTML页面中创建一条水平线。

* 水平分割线可以在视觉上将文档分割成各个部分。

* `<hr>`是空标签，建议使用`<hr/>`。

* <hr/>

> `<!--..-->`：定义注释。

#### 列表标签

> `<ul>`：定义无序列表。

> `<ol>`：定义有序列表。

> `<li>`：定义列表的项目。

* type指明项目的类型，属性值有：A，a，I，i，1，disc（实心圆），square（实心正方形），circle（空心圆）。
* value表示序号值从几开始。

```html
<ul>
   <li>Coffee</li>
   <li>Tea</li>
   <li>Milk</li>
</ul>
<ol>
   <li>Coffee</li>
   <li>Tea</li>
   <li>Milk</li>
</ol>
```

> `dl`定义定义列表。

> `dt`定义定义列表中的项目。

> `dd`定义定义列表中项目的描述。

```html
<dl>
   <dt>计算机</dt>
   <dd>用来计算的仪器 ... ...</dd>
   <dt>显示器</dt>
   <dd>以视觉方式显示信息的装置 ... ...</dd>
</dl>
```

#### 表格标签

> `<table>`：定义表格。

* > `<caption>`定义表格标题。

* > `<tr>`定义表格中的行。

* > `<th>`定义表格中的表头单元格。

* > `<td>`定义表格中的单元。

* > `<thead>`定义表格中的表头内容。

* > `<tbody>`定义表格中的主体内容。

* > `<tfoot>`定义表格中的表注内容（脚注）。

```html
<table>
    <caption>xxxxxxxxxx</caption>
    <thead>
            <tr>
                <th>序号</th>
                <th>姓名</th>
                <th>年龄</th>
                <th>女神</th>
            </tr>
        </thead>
        <tbody>
            <tr>
                <th>1.</th>
                <td>nick</td>
                <td>18</td>
                <td>可可西</td>
            </tr>
            <tr>
                <th>2.</th>
                <td>jenny</td>
                <td>21</td>
                <td>nick!!!</td>
            </tr>
        </tbody>

</table>
```

<table>
    <caption>xxxxxxxxxx</caption>
    <thead>
            <tr>
                <th>序号</th>
                <th>姓名</th>
                <th>年龄</th>
                <th>女神</th>
            </tr>
        </thead>
        <tbody>
            <tr>
                <th>1.</th>
                <td>nick</td>
                <td>18</td>
                <td>可可西</td>
            </tr>
            <tr>
                <th>2.</th>
                <td>jenny</td>
                <td>21</td>
                <td>nick!!!</td>
            </tr>
        </tbody>
</table>

#### 表单标签


> `<form>`：定义供用户输入的 HTML 表单。

* HTML 表单用于接收不同类型的用户输入，用户提交表单时向服务器传输数据，从而实现用户与Web服务器的交互。表单标签, 要提交的所有内容都应该在该标签中。

* `action`表单要提交的地址，用于处理表单的内容（一般是提交字典到后台的一个接口，这个接口是java写成的，提交到这个接口后后台就知道如何处理这些数据了）。

* `method` 提交的方法，默认是get方式提交。

  * `get`
    1. 提交的键值对.放在地址栏中url后面。
    2. 安全性相对较差。
    3. 对提交内容的长度有限制。
  * `post`
    1. 提交的键值对不在地址栏。
    2. 安全性相对较高。
    3. 对提交内容的长度理论上无限制。

  ```html\
  <form action="https://www.baidu.com/s">
  	<input type="text" name="wd">
  	<input type="submit" value="百度一下">
  </form>
  ```

> `<input>`：定义输入控件。

* `type`
  * `text`文本框
    * `autocomplete`（自动完成输入的内容，要求表单元素要有name属性才有自动完成的效果，off表示自动完成不可用，on表示自动完成可用）
    * `disabled`（设置获取控件的状态，默认是false即可用，等于true时不可用，不能输入内容）

  * `password`密码框（以下属性text和password共有）

    * `value`（设置默认值）

    * `size`（指定表单元素的初始宽度。当type为text或password时，表单元素的大小以字符为单位，对于其他元素，宽度以像素为单位）。
    * `maxlength`（type为text或password时，表示输入的最大字符数），有利于防止sql的注入攻击。
    * `readonly` 只读。
    * `placeholder` 框内预置内容(灰色)，写上内容时才消失。

  * `radio`单选按钮
    * name（将name的值设置为相同值，才表示一组数据，才能实现单选功能）
    * value（必须要写，提交到服务器的key值，实际开发过程中value一般是编号）
    * checked（是否被选中的状态）

  * `checkbox`复选框
    * name（名字一定要一样一样的，才表示是一组数据，添加到同一value值列表提交到服务器）
    * value（必须要写，提交到服务器的key值，实际开发过程中value一般是编号）
    * checked（是否被选中的状态

  * `submit`提交按钮。用于提交表单。

  * `reset` 重置按钮。清空表单的输入，恢复到表单默认的状态。

  * `button`普通按钮。一般结合javascript使用。

  * `image`图片按钮，用来提交表单，与submit是一样的效果。

    * src（图片路径）

  * `date`日期选择器，用来选择日期。

  * `color`颜色选择器，用来选择颜色。

  * `range`范围选择器，用来选择范围

    * `min`（最小值）
    * `max`（最大值）

  * `email`邮件输入框

    * 提交的时候会进行邮件格式校验

  * `url`地址输入框

    * 提交的时候会进行地址格式校验

  * `file`文件域，上传文件（不同的浏览器表现形式不同）

    * `multiple="multiple"`（可以选择多个文件）

  * `hidden`隐藏字段

    * value（隐藏的内容）

> `<textarea>`定义多行的文本输入控件。

* 默认表现形式是可以输入很多行文本的文本框。
* name （表单提交项的key）
* cols（设置文本域宽度）
* rows（设置文本域高度，即行数）

> `<label>`：

* 把元素与文本结合起来

* 不只是选中复选框才能选中并打钩，要求点击对应的文字也能选中该复选框。
  这种情况下要用到<label>标签的for属性（设置或获取给定标签对象指定到的对象，值=另一个元素的id号即可）

  ```html
  <label for="name">姓名</label>
  <input id="name" type="text">
  ```

> `<select>`：定义选择列表（下拉列表）。

* 使用时要结合`<option>`子标签一起使用。
* name（表单提交项的key）
* size（选项个数）
* multiple（多选）

> `<option>` 定义选择列表中的选项。

* value（表单提交项的值）

* selected（selected下拉选默认被选中）

  ```html
  <select>
    <option value ="volvo">Volvo</option>
    <option value ="saab">Saab</option>
    <option value="opel">Opel</option>
    <option value="audi">Audi</option>
  </select>
  ```

### 特殊符号

>HTML 中的预留字符必须被替换为字符实体。
>
>一些在键盘上找不到的字符也可以使用字符实体来替换。
>
>实体名称对大小写敏感！

```html
&nbsp;  空格
&copy;  版权符号 ©
&gt;    大于号 >
&lt;    小于号 <
&quot;  双引号 "
&apos;  单引号 '
```
