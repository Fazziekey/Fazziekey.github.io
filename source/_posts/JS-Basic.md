---
title: JS Basic
date: 2020-07-31 13:53:48
copyright: true
tags:
    - 前端
    - JavaScript
categories: 
    - 《栈溢出工程师》
---
# JavaScript 基础
1. 所有主流浏览器都支持JavaScript。

2. 目前，全世界大部分网页都使用JavaScript。

3. 它可以让网页呈现各种动态效果。

<!--more-->

## 如何插入JS
使用`<script>`标签在HTML网页中插入JavaScript代码。注意， `<script>`标签要成对出现，并把JavaScript代码写在`<script></script>`之间。

`<script type="text/javascript">`表示在`<script></script>`之间的是文本类型(text),javascript是为了告诉浏览器里面的文本是属于JavaScript语言。

## 应用JS文件
JS文件不能直接运行，需嵌入到HTML文件中执行，我们需在HTML中添加如下代码，就可将JS文件嵌入HTML文件中。

    <script src="script.js"></script>
    
## 嵌入JS的位置
我们可以将JavaScript代码放在html文件中任何位置，但是我们一般放在网页的head或者body部分。
放在`<head>`部分
最常用的方式是在页面中head部分放置`<script>`元素，浏览器解析head部分就会执行这个代码，然后才解析页面的其余部分。
放在`<body>`部分
JavaScript代码在网页读取到该语句的时候就会执行。



> 注意: javascript作为一种脚本语言可以放在html页面中任何位置，但是浏览器解释html时是按先后顺序的，所以前面的script就先被执行。比如进行页面显示初始化的js必须放在head里面，因为初始化都要求提前进行（如给页面body设置css等）；而如果是通过事件调用执行的function那么对位置没什么要求的。

## JS语句和符号
JavaScript语句是发给浏览器的命令。这些命令的作用是告诉浏览器要做的事情。

每一句JavaScript代码格式: 语句;

先来看看下面代码

    <script type="text/javascript">
       alert("hello!");
    </script>
例子中的alert("hello!");就是一个JavaScript语句。

一行的结束就被认定为语句的结束，通常在结尾加上一个分号";"来表示语句的结束。

看看下面这段代码,有三条语句，每句结束后都有";"，按顺序执行语句。

    <script type="text/javascript">
       document.write("I");
       document.write("love");
       document.write("JavaScript");
    </script>
注意:

1. “;”分号要在英文状态下输入，同样，JS中的代码和符号都要在英文状态下输入。

2. 虽然分号“;”也可以不写，但我们要养成编程的好习惯，记得在语句末尾写上分号。

## JS注释

注释的作用是提高代码的可读性，帮助自己和别人阅读和理解你所编写的JavaScript代码，注释的内容不会在网页中显示。注释可分为单行注释与多行注释两种。

我们为了方便阅读，注释内容一般放到需要解释语句的结尾处或周围。

单行注释，在注释内容前加符号 “//”。

    <script type="text/javascript">
      document.write("单行注释使用'//'");  // 我是注释，该语句功能在网页中输出内容
    </script>
    多行注释以"/*"开始，以"*/"结束。
    
    <script type="text/javascript">
       document.write("多行注释使用/*注释内容*/");
       /*
        多行注释
        养成书写注释的良好习惯
       */
    </script>
    
## JS变量
定义变量使用关键字var,语法如下：

var 变量名
变量名可以任意取名，但要遵循命名规则:

    1.变量必须使用字母、下划线(_)或者美元符($)开始。

    2.然后可以使用任意多个英文字母、数字、下划线(_)或者美元符($)组成。

    3.不能使用JavaScript关键词与JavaScript保留字。

变量要先声明再赋值，如下：

    var mychar;
    mychar="javascript";
    var mynum = 6;
变量可以重复赋值，如下：

    var mychar;
    mychar="javascript";
    mychar="hello";
注意:

1. 在JS中区分大小写，如变量mychar与myChar是不一样的，表示是两个变量。

2. 变量虽然也可以不声明，直接使用，但不规范，需要先声明，后使用。

## 判断语句

if...else语句是在指定的条件成立时执行代码，在条件不成立时执行else后的代码。

语法:

if(条件)
{ 条件成立时执行的代码 }
else
{ 条件不成立时执行的代码 }
假设我们通过年龄来判断是否为成年人，如年龄大于等于18岁，是成年人，否则不是成年人。代码表示如下:

    <script type="text/javascript">
       var myage = 18;
       if(myage>=18)  //myage>=18是判断条件
       { document.write("你是成年人。");}
       else  //否则年龄小于18
       { document.write("未满18岁，你不是成年人。");}
    </script>
    
## JS函数
如何定义一个函数呢？基本语法如下:

    function 函数名()
    {
         函数代码;
    }
说明:

1. function定义函数的关键字。

2. "函数名"你为函数取的名字。

3. "函数代码"替换为完成特定功能的代码。

我们来编写一个实现两数相加的简单函数,并给函数起个有意义的名字：“add2”，代码如下：

    function add2(){
       var sum = 3 + 2;
       alert(sum);
    }
函数调用:

函数定义好后，是不能自动执行的，所以需调用它,只需直接在需要的位置写函数就ok了,代码如下:

# JS互动
## JS输出内容
document.write() 可用于直接向 HTML 输出流写内容。简单的说就是直接在网页中输出内容。

第一种:输出内容用""括起，直接输出""号内的内容。

    <script type="text/javascript">
      document.write("I love JavaScript！"); //内容用""括起来，""里的内容直接输出。
    </script>
第二种:通过变量，输出内容

    <script type="text/javascript">
      var mystr="hello world!";
      document.write(mystr);  //直接写变量名，输出变量存储的内容。
    </script>
第三种:输出多项内容，内容之间用+号连接。

    <script type="text/javascript">
      var mystr="hello";
      document.write(mystr+"I love JavaScript"); //多项内容之间用+号连接
    </script>
第四种:输出HTML标签，并起作用，标签使用""括起来。

    <script type="text/javascript">
      var mystr="hello";
    document.write(mystr+"<br>");//输出hello后，输出一个换行符
      document.write("JavaScript");
    </script>
    
## 警告框
我们在访问网站的时候，有时会突然弹出一个小窗口，上面写着一段提示信息文字。如果你不点击“确定”，就不能对网页做任何操作，这个小窗口就是使用alert实现的。

**语法:**

alert(字符串或变量);  
看下面的代码:
    
    <script type="text/javascript">
       var mynum = 30;
       alert("hello!");
       alert(mynum);
    </script>
注:alert弹出消息对话框(包含一个确定按钮)。

结果:按顺序弹出消息框

注意:

1. 在点击对话框"确定"按钮前，不能进行任何其它操作。

2. 消息对话框通常可以用于调试程序。

3. alert输出内容，可以是字符串或变量，与document.write 相似。

## confirm消息对话框
onfirm 消息对话框通常用于允许用户做选择的动作，如：“你对吗？”等。弹出对话框(包括一个确定按钮和一个取消按钮)。

**语法:**

confirm(str);
参数说明:

str：在消息对话框中要显示的文本
返回值: Boolean值
返回值:

当用户点击"确定"按钮时，返回true
当用户点击"取消"按钮时，返回false
注: 通过返回值可以判断用户点击了什么按钮

看下面的代码:

    <script type="text/javascript">
        var mymessage=confirm("你喜欢JavaScript吗?");
        if(mymessage==true)
        {   document.write("很好,加油!");   }
        else
        {  document.write("JS功能强大，要学习噢!");   }
    </script>

## promot对话框
prompt弹出消息对话框,通常用于询问一些需要与用户交互的信息。弹出消息对话框（包含一个确定按钮、取消按钮与一个文本输入框）。

**语法:**

prompt(str1, str2);
参数说明：

str1: 要显示在消息对话框中的文本，不可修改
str2：文本框中的内容，可以修改
返回值:

1. 点击确定按钮，文本框中的内容将作为函数返回值
2. 点击取消按钮，将返回null
看看下面代码:


    var myname=prompt("请输入你的姓名:");
    if(myname!=null)
      {   alert("你好"+myname); }
    else
      {  alert("你好 my friend.");  }
      
## 打开新窗口
open() 方法可以查找一个已经存在或者新建的浏览器窗口。

**语法：**

    window.open([URL], [窗口名称], [参数字符串])
**参数说明:**

URL：可选参数，在窗口中要显示网页的网址或路径。如果省略这个参数，或者它的值是空字符串，那么窗口就不显示任何文档。
窗口名称：可选参数，被打开窗口的名称。
    1.该名称由字母、数字和下划线字符组成。
    2."_top"、"_blank"、"_self"具有特殊意义的名称。
       _blank：在新窗口显示目标网页
       _self：在当前窗口显示目标网页
       _top：框架网页中在上部窗口中显示目标网页
    3.相同 name 的窗口只能创建一个，要想创建多个窗口则 name 不能相同。
   4.name 不能包含有空格。
参数字符串：可选参数，设置窗口参数，各参数用逗号隔开。

![](https://cdn.jsdelivr.net/gh/Fazziekey/image-bed@master/2020/07/31/9621f92441c7d561518f086bf718c5e9.png)

## 关闭窗口
close()关闭窗口

用法：

window.close();   //关闭本窗口
或

<窗口对象>.close();   //关闭指定的窗口
例如:关闭新建的窗口。

    <script type="text/javascript">
       var mywin=window.open('http://fazzie-key.cool'); //将新打的窗口对象，存储在变量mywin中
       mywin.close();
    </script>
注意:上面代码在打开新窗口的同时，关闭该窗口，看不到被打开的窗口。

# DOM
文档对象模型DOM（Document Object Model）定义访问和处理HTML文档的标准方法。DOM 将HTML文档呈现为带有元素、属性和文本的树结构（节点树）。

HTML文档可以说由节点构成的集合，三种常见的DOM节点:

1. 元素节点：上图中<html>、<body>、<p>等都是元素节点，即标签。

2. 文本节点:向用户展示的内容，如`<li>...</li>`中的JavaScript、DOM、CSS等文本。

3. 属性节点:元素属性，如<a>标签的链接属性href="http://fazzie-key.cool"。

## 通过ID获取元素
网页由标签将信息组织起来，而标签的id属性值是唯一的，就像是每人有一个身份证号一样，只要通过身份证号就可以找到相对应的人。那么在网页中，我们通过id先找到标签，然后进行操作。

**语法:**

     document.getElementById("id") 
 
> 获取的元素是一个对象，如想对元素进行操作，我们要通过它的属性或方法。


    < !DOCTYPE HTML>
    c<html>
    o <head>
    <meta http-equiv=”Content-Type”
    content=" text/html; charset=gb2312” />
    <title>获取元素</title>
    <script type=" text/ javascript" >
    var mye = document. getElementById("con");//获取元素存储在变量mye中
    document. write (mye) ;//输出变量mye
    </ script>
    </head> 
    <body>
    <h3>Hello</h3>
    <p id="con">I love JavaScript</p>
    </ body>
    </html>
    
## innerHTML属性
innerHTML 属性用于获取或替换 HTML 元素的内容。

语法:

Object.innerHTML
注意:

1.Object是获取的元素对象，如通过document.getElementById("ID")获取的元素。

2.注意书写，innerHTML区分大小写。

我们通过id="con"获取<p> 元素，并将元素的内容输出和改变元素内容，代码如下:

    < !DOCTYPE HTML>
    (html>
    <head>
    <title> innerHTML</title>
    </head>
    <body>
    <p id="con">Hello World!</p> 
    <script>
    var mycon= document.getElementById(" con") ;
    document. write("p标签原始内容:”+ mycon. innerHTML+"<br>");
    //输入元素内容
    mycon. innerHTML ="New text!"; //修改p元素内容
    document. write(" p标签修改后内容:"+ mycon. innerHTML) ;
    </script>
    </body>
    </html>
    
## 改变样式
HTML DOM 允许 JavaScript 改变 HTML 元素的样式。如何改变 HTML 元素的样式呢？

语法:

    Object.style.property=new style;
    
> Object是获取的元素对象，如通过document.getElementById("id")获取的元素。

+ backgroundColor:背景颜色
+ height:高度
+ width：宽度
+ cplor：文本颜色
+ font：字体属性
+ fontFamily：字体系列
+ fontsize：字体大小

> 该表只是一小部分CSS样式属性，其它样式也可以通过该方法设置和修改。

看看下面的代码:

改变 `<p>` 元素的样式，将颜色改为红色，字号改为20,背景颜色改为蓝：

    <p id="pcon">Hello World!</p>
    <script>
       var mychar = document.getElementById("pcon");
       mychar.style.color="red";
       mychar.style.fontSize="20";
       mychar.style.backgroundColor ="blue";
    </script>
    
## 隐藏和显示
网页中经常会看到显示和隐藏的效果，可通过display属性来设置。

**语法：**

    Object.style.display = value

> Object是获取的元素对象，如通过document.getElementById("id")获取的元素。



值| 描述
---|---
none | 隐藏
block | 显示


    < !DOCTYPE HTML>
    <html>
    <head>
    <meta http-equiv=" Content- Type" content=" text/html; charset=gb2312">
    <title>display</title>
    <script type=" text/ javascript" >
    function hidetext (){
    document. getElementById(" con"). style. display=”none' ;}
    function showtext (){
    document. getElementById( 'con' ). style. display="block" ;}
    </script>
    </ head>
    <body>
    <h1> JavaScript</h1>
    <p id=" con">
    做为一个Web开发师来说，如果你想提供漂亮的网页、令用户满意的上网体验，JavaScript是 必
    不可少的工具。</p>
    < form>
    <input type="button" onclick="hidetext()" value="不显示段落内容”/>
    <input type=" button”onclick=" showtext()”value="显示 段落内容”/>
    </ form>
    </body>
    </html>
    
## 控制类名
className 属性设置或返回元素的class 属性。

**语法：**

    object.className = classname
**作用:**

1.获取元素的class 属性

2. 为网页内的某个元素指定一个css样式来更改该元素的外观

看看下面代码，获得 `<p>` 元素的 class 属性和改变className：

    < !DOCTYPE HTML>
    <html>
    <head>
    <meta http-equiv=" Content- -Type" content=" text/html; charset=gb2312">
    <title>className属性</title>
    <style type=" text/css" >
    input{
    font-size: 10px;}
    .one{
    width: 200px ;
    background-color :#CCC;}
    .two {
    font-size: 18px;
    color:#F00;}
    </style>
    </head>
    <body>
    <p id=" con”class=" one">JavaScript</p>
    <form>
    <input type=" button” value="点击更改”onclick=' modifyclass()”/>
    </ form>
    <script type=" text/ javascript' >
    var mychar= document. getElementById( con' ) ;
    document. write(" p元素Class值为:”+ mychar. className+"<br>");
    //输出p元素Class属性
    function modifyclass() {
    mychar. className=" two”; / /改变className }
    </script>
    </body>
    </html>



