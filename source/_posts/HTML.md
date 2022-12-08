---
title: HTML
copyright: true
date: 2020-07-28 15:30:15
tags:
     - 前端
     - HTML
categories: 
    - 《栈溢出工程师》
---

# HTML基础
## HTML和CSS关系
+ css是用来修饰html样式的
+ html本身是有一些默认样式,如果我们想改变html标签的样式,就需要借助css
+ html+css构成了我们网页的基本页面结构和样式

<!--more-->

## 标签的使用

+ 标签由英文尖括号<和>括起来，如<html>就是一个标签。
+  html中的标签一般都是成对出现的，分开始标签和结束标签。结束标签比开始标签多了一个/。

如：
+ `<p></p>`

+ `<div></div>`

+ `<span></span>`
+ 标签与标签之间是可以嵌套的，但先后顺序必须保持一致，如：`<div>`里嵌套`<p>`，那么`</p>`必须放在`</div>`的前面。
+ HTML标签不区分大小写，`<h1>`和`<H1>`是一样的，但建议小写，因为大部分程序员都以小写为准。

## HTML基本结构
技术点的解释：

1. `<!DOCTYPE html>`:文档类型声明，表示该文件为 HTML5文件。`<!DOCTYPE>` 声明必须是 HTML 文档的第一行，位于 `<html>` 标签之前

2. `<html></html>`标签对：`<html>`标签位于HTML文档的最前面，用来标识HTML文档的开始；`</html>`标签位于HTML文档的最后面，用来标识HTML 文档的结束；这两个标签对成对存在，中间的部分是文档的头部和主题。

3.`<head></head>`标签对：标签包含有关HTML文档的信息，可以包含一些辅助性标签。如`<title></title>，<link /><meta />，<style></style>，<script></script>`等，但是浏览器除了会在标题栏显示`<title>`元素的内容外，不会向用户显示head元素内的其他任何内容。

4.`<body></body>`标签对：它是HTML文档的主体部分，在此标签中可以包含`<p><h1><br>`等众多标签，`<body>`标签出现在`</head>`标签之后，且必须在闭标签`</html>`之前闭合。
### 案例
    <!DOCTYPE html>
    <html>
        <head>
            <meta charset="UTF-8">
            <title>html文件基本结构</title>
        </head>
        <body>
            <h1>Hello world</h1>
        </body>
    </html>
    

**效果**

<h1>Hello world</h1>
---------------------
## head标签
文档的头部描述了文档的各种属性和信息，包括文档的标题等，绝大多数文档头部包含的数据都不会真正作为内容显示给读者。

下面这些标签可用在 head 部分：

1、head标签为双标签，有尾标签，`<head></head>`。

2、head标签表示头部标签,通常用来嵌套meta、title、style等标签。

3、`<title>`标签：在`<title>`和`</title>`标签之间的文字内容是网页的标题信息，它会出现在浏览器的标题栏中。网页的title标签用于告诉用户和搜索引擎这个网页的主要内容是什么，搜索引擎可以通过网页标题，迅速的判断出网页的主题。每个网页的内容都是不同的，每个网页都应该有一个独一无二的title。

4、`<meta charset="UTF-8">`设置当前文件字符编码

5、style标签：双标签中设置当前文件样式

例如title标签：

    <head>
        <title>hello world</title>
    </head>
    <title>
标签的内容“hello world”会在浏览器中的标题栏上显示出来.

## body标签
### 案例
    <!DOCTYPE html>
    <html>
    
    <head>
        <meta charset="UTF-8">
        <title>了不起的盖茨比</title>
    </head>
    
    <body>
        <!-- 标题标签 -->
        <h1>了不起的盖茨比</h1>
        <!-- 段落标签 -->
        <p>1922年的春天，一个想要成名名叫尼克•卡拉威（托比•马奎尔Tobey Maguire 饰）的作家，离开了美国中西部，来到了纽约。那是一个道德感渐失，爵士乐流行，走私为王，股票飞涨的时代。为了追寻他的<span>美国梦</span>，他搬入纽约附近一海湾居住。</p>
        <!-- 段落标签 -->
        <p>菲茨杰拉德，二十世纪美国文学巨擘之一，兼具作家和编剧双重身份。他以诗人的敏感和戏剧家的想象为"爵士乐时代"吟唱华丽挽歌，其诗人和梦想家的气质亦为那个奢靡年代的不二注解。</p>
    </body>
    
    </html>

## HTML代码注释
`<!--注释文字-->`

# HTML5语义化标签
**标签的用途**

我们学习网页制作时，常常会听到一个词，语义化。那么什么叫做语义化呢，说的通俗点就是：明白每个标签的用途（在什么情况下使用此标签合理）比如，网页上的文章的标题就可以用标题标签，网页上的各个栏目的栏目名称也可以使用标题标签。文章中内容的段落就得放在段落标签中等等

**语义化的好处**

1. 更容易被搜索引擎收录。

2. 更容易让屏幕阅读器读出网页内容。

## 常用标签

`<p>`| 段落标签
---|---
`<span>`| 自定义文字样式
`<hx>`| 标题标签
`<div>`|分块标签
`<header>`|头部标签
`<footer>`|底部标签
`<section>`|区段标签
`<aside>`|侧边栏
`<br>`|换行
`&nbsp`|空格
`<hr>`|分隔线标签
`<ul>,<li>`|列表标签
`<ol>,<li>`|有序列表

## 段落标签
语法：

`<p>段落文本</p>`

 注意一段文字一个`<p>`标签，如在一篇新闻文章中有3段文字，就要把这3个段落分别放到3个`<p>`标签中。
 
## diy文字：`<span>`
 `<span>`标签是没有语义的，它的作用就是为了设置单独的样式用 的。

## `<div>`自定义块
在网页制作过程过中，可以把一些独立的逻辑部分划分出来，放在一个`<div>`标签中，这个`<div>`标签的作用就相当于一个容器。

语法：

`<div>…</div>`

## 列表标签
**语法**

    <ul>
      <li>信息</li>
      <li>信息</li>
       ......
    </ul>
**效果**  
    
<ul>
  <li>信息</li>
  <li>信息</li>
   ......
</ul>

# 插入图片链接
## 插入图片
**语法：**

    <img src="图片地址" alt="下载失败时的替换文本" title = "提示文本">

**举例：**

    <img src = "myimage.gif" alt = "My Image" title = "My Image" />


1、src：标识图像的位置；

2、alt：指定图像的描述性文本，当图像不可见时（下载不成功时），可看到该属性指定的文本；

3、title：提供在图像可见时对图像的描述(鼠标滑过图片时显示的文本)；

4、图像可以是GIF，PNG，JPEG格式的图像文件。

## 插入超链接
使用`<a>`标签可实现超链接，它在网页制作中可以说是无处不在，只要有链接的地方，就会有这个标签。

语法：

`<a  href="目标网址"  title="鼠标滑过显示的文本">`链接显示的文本`</a>`

**例如：**

    <a  href="http://www.fazzie-key.cool"  title="点击进入慕课网">click here!</a>
上面例子作用是单击click here!文字，网页链接到http://www.fazzie-key.cool这个网页。

**效果**

  <a  href="http://www.fazzie-key.cool"  title="点击进入慕课网">click here!</a>

> title属性的作用，鼠标滑过链接文字时会显示这个属性的文本内容。这个属性在实际网页开发中作用很大，主要方便搜索引擎了解链接地址的内容（语义化更友好），）。

### 打开新窗口
a标签有的target属性，代表打开网页的方式。可选值为”_self和_blank”，默认值为_self，代表在当前页面打开链接，_blank代表在新窗口打开链接。

## 插入表格
创建表格的四个元素：table、tr、th、td

1、<table>…</table>：整个表格以<table>标记开始、</table>标记结束。

2、<tr>…</tr>：表格的一行，所以有几对tr 表格就有几行。

3、<td>…</td>：表格的一个单元格，一行中包含几对<td>...</td>，说明一行中就有几列。

4、<th>…</th>：表格的头部的一个单元格，表格表头。

5、表格中列的个数，取决于一行中数据单元格的个数。

6、border属性可以为表格添加边框，属性值为数字。

**注意：**

1、table标签用来定义整个表格，为双标签，必须有结束标签。

2、table标签里面可以放caption标签和tr标签。

3、caption标签用来定义表格的标题。

4、tr标签用来设置表格的行，tr里面只能放th或者td标签，一组tr标签代表一行。

5、th用来设置表格的标题，会加粗居中显示。也就是th标签中的文本默认为粗体并且居中显示。

6、td同来设置表格的列，一组td标签代表一列。

7、table表格在没有添加border属性之前, 在浏览器中显示是没有表格线的。

**案例：**

    <table border ="1">
        <caption> 前端三件套</caption>
        <tr>
            <th>语言</th>
            <th>难度</th>
        </tr>
         <tr>
            <td>HTML</td>
            <td>7</td>
        </tr>
          <tr>
            <td>CSS</td>
            <td>8</td>
        </tr>
          <tr>
            <td>JavaScript</td>
            <td>9</td>
        </tr>
    </table>
**效果**
<table border ="1">
    <caption> 前端三件套</caption>
    <tr>
        <th>语言</th>
        <th>难度</th>
    </tr>
     <tr>
        <td>HTML</td>
        <td>7</td>
    </tr>
      <tr>
        <td>CSS</td>
        <td>8</td>
    </tr>
      <tr>
        <td>JavaScript</td>
        <td>9</td>
    </tr>
</table>

1、`<thead>` 标签定义表格的表头。该标签用于组合 HTML 表格的表头内容。

2、`<tbody>…</tbody>`：如果不加`<thead><tbody><tfooter>` , table表格加载完后才显示。加上这些表格结构， tbody包含行的内容下载完优先显示，不必等待表格结束后在显示，同时如果表格很长，用tbody分段，可以一部分一部分地显示。（通俗理解table 可以按结构一块块的显示，不在等整个表格加载完后显示。）

3、`<tfoot>` 元素用于对 HTML 表格中的表注（页脚）内容进行分组。

4、thead、tfoot 以及 tbody 元素使您有能力对表格中的行进行分组。当您创建某个表格时，您也许希望拥有一个标题行，一些带有数据的行，以及位于底部的一个总计行。这种划分使浏览器有能力支持独立于表格标题和页脚的表格正文滚动。当长的表格被打印时，表格的表头和页脚可被打印在包含表格数据的每张页面上。

# 网站与用户交互

网站怎样与用户进行交互？答案是使用HTML表单(form)。表单是可以把浏览者输入的数据传送到服务器端，这样服务器端程序就可以处理表单传过来的数据。

**语法：**

`<form   method="传送方式"   action="服务器文件">`
讲解：

1.`<form>` ：`<form>`标签是成对出现的，以`<form>`开始，以`</form>`结束。

2.action ：浏览者输入的数据被传送到的地方,比如一个PHP页面(save.php)。

3.method ： 数据传送的方式（get/post）。

    <form    method="post"   action="save.php">
            <label for="username">用户名:</label>
            <input type="text" name="username" />
            <label for="pass">密码:</label>
            <input type="password" name="pass" />
    </form>

**效果**

![](https://cdn.jsdelivr.net/gh/Fazziekey/image-bed@master/2020/07/28/632bd87adb5745d95e801801a74e9b49.png)

## 输入方式
当用户要在表单中键入字母、数字等内容时，就会用到文本输入框。文本框也可以转化为密码输入框。
**
语法：**

    <form>
       <input type="text/password" name="名称" value="文本" />
    </form>
**1、type：**

   当type="text"时，输入框为文本输入框;
   当type="password"时, 输入框为密码输入框。

**2、name**：

为文本框命名，以备后台程序ASP 、PHP使用。

**3、value**：

为文本输入框设置默认值。(一般起到提示作用)

举例：

    <form>
      姓名：
      <input type="text" name="myName">
      <br/>
      密码：
      <input type="password" name="pass">
    </form>

## placeholder属性
input标签中占位符placeholder,属性，有时候需要提示用户输入框需要输入框的内容，
    
    <input type="password" placeholder="请输入密码" name="pass">
    
## 数字输入框
1、input的type属性设置为number,则表示该输入框的类型为数字。

2、数字框只能输入数字，输入其他字符无效。

3、数字框最右侧会有一个加减符号,可以调整输入数字的大小,不同浏览器表现不一致。

    <input type="number">

## 网址输入框
1、input的type属性设置为url,则表示该输入框的类型为网址。

2、数字框的值需以http://或者https://开头,且后面必须有内容,否则表单提交的时候会报错误提示。

    <input type="url">
    
## 邮箱输入框

1、Input的type属性设置为email,则表示该输入框的类型为邮箱。

2、数字框的值必须包含@。

3、数字框的值@之后必须有内容,否则会报错误提示。

     <input type="email">

## 文本框（评论系统）
当用户需要在表单中输入大段文字时，需要用到文本输入域。

语法：

`<textarea  rows="行数" cols="列数">`文本`</textarea>`
1、`<textarea>`标签是成对出现的，以`<textarea>`开始，以`</textarea>`结束。

2、cols ：多行输入域的列数。

3、rows ：多行输入域的行数。

4、在`<textarea></textarea>`标签之间可以输入默认值。

举例：

    <form  method="post" action="save.php">
            <label>联系我们</label>
            <textarea cols="50" rows="10" >在这里输入内容...</textarea>
    </form>

## label标签
label标签不会向用户呈现任何特殊效果，它的作用是为鼠标用户改进了可用性。如果你在 label 标签内点击文本，就会触发此控件。就是说，当用户单击选中该label标签时，浏览器就会自动将焦点转到和标签相关的表单控件上（就自动选中和该label标签相关连的表单控件上）。

**语法：**

`<label for="控件id名称">`
注意：标签的 for 属性中的值应当与相关控件的 id 属性值一定要相同。

**例子：**
    
    <form
      <label for="email">输入你的邮箱地址</label>
      <input type="email" id="email" placeholder="Enter email">
    </form>

## 选框
在使用表单设计调查表时，为了减少用户的操作，使用选择框是一个好主意，html中有两种选择框，即单选框和复选框，两者的区别是单选框中的选项用户只能选择一项，而复选框中用户可以任意选择多项，甚至全选。请看下面的例子:

**语法：**

    <input   type="radio/checkbox"   value="值"    name="名称"   checked="checked"/>
1、**type**:

   当 type="radio" 时，控件为单选框

   当 type="checkbox" 时，控件为复选框

2、**value**：提交数据到服务器的值（后台程序PHP使用）

3、**name**：为控件命名，以备后台程序 ASP、PHP 使用

4、**checked**：当设置 checked="checked" 时，该选项被默认选中

如下面代码：

    <form action="save.php" method="post">
            <label>性别:</label>
            <label>男</label>
            <input type="radio" value="1" name="gender" />
            <label>女</label>
            <input type="radio" value="2" name="gender" />
        </form>

## 下拉框
下拉列表在网页中也常会用到，它可以有效的节省网页空间。既可以单选、又可以多选。如下代码：

    <form>
            <select>
                <option value="看书">看书</option>
                <option value="旅游">旅游</option>
                <option value="运动">运动</option>
                <option value="购物">购物</option>
            </select>
        </form>

## 提交按钮
在表单中有两种按钮可以使用，分别为：提交按钮、重置。这一小节讲解提交按钮：当用户需要提交表单信息到服务器时，需要用到提交按钮。

**语法：**

`<input   type="submit"   value="提交">`

**type**：只有当type值设置为submit时，按钮才有提交作用

**value**：按钮上显示的文字


        <form method="post" action="save.php">
            <label for="myName">姓名：</label>
            <input type="text" value=" " name="myName " />
            <input type="submit" value="提交" name="submitBtn" />
        </form>

## 重置
当用户需要重置表单信息到初始时的状态时，比如用户输入“用户名”后，发现书写有误，可以使用重置按钮使输入框恢复到初始状态。只需要把type设置为"reset"就可以。

语法：

    <input type="reset" value="重置">

**type**：只有当type值设置为reset时，按钮才有重置作用

**value**：按钮上显示的文字