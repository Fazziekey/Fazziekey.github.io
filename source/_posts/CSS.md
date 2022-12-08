---
title: CSS
date: 2020-07-28 23:22:38
copyright: true
tags:
    - CSS
    - 前端
categories: 
    - 《栈溢出工程师》
---
# CSS基础
CSS全称为“层叠样式表 (Cascading Style Sheets)”，它主要是用于定义HTML内容在浏览器内的显示样式，如文字大小、颜色、字体加粗等。

<!--more-->
如下列代码：

    p{
       font-size:12px;
       color:red;
       font-weight:bold;
    }
使用CSS样式的一个好处是通过定义某个样式，可以让不同网页位置的文字有着统一的字体、字号或者颜色等。

## CSS语法
css 样式由选择符和声明组成，而声明又由属性和值组成。

选择符：又称选择器，指明网页中要应用样式规则的元素，如本例中是网页中所有的段（p）的文字将变成蓝色，而其他的元素（如ol）不会受到影响。

声明：在英文大括号“｛｝”中的的就是声明，属性和值之间用英文冒号“：”分隔。当有多条声明时，中间可以英文分号“;”分隔，如下所示：

    p{font-size:12px;color:red;}
注意：

1、最后一条声明可以没有分号，但是为了以后修改方便，一般也加上分号。

2、为了使用样式更加容易阅读，可以将每条代码写在一个新行内，如下所示：

    p{
       font-size:12px;
       color:red;
    }

### CSS注释

`/*注释语句*/`

## CSS的插入方式
？从CSS 样式代码插入的形式来看基本可以分为以下3种：内联式、嵌入式和外部式三种。

### 内联式
内联式css样式表就是把css代码直接写在现有的HTML标签中，如下面代码：

    <p style="color:red">这里文字是红色。</p>
    
注意要写在元素的开始标签里，下面这种写法是错误的：

    <p>这里文字是红色。</p style="color:red">
并且css样式代码要写在style=""双引号中，如果有多条css样式代码设置可以写在一起，中间用分号隔开。如下代码：

    <p style="color:red;font-size:12px">这里文字是红色。</p>
**效果**
<p style="color:red;font-size:12px">这里文字是红色。</p>

### 嵌入式
嵌入式css样式，就是可以把css样式代码写在`<style type="text/css"></style>`标签之间。如下面代码实现把三个`<span>`标签中的文字设置为红色：

    <style type="text/css">
    span{
    color:red;
    }
    </style>
    
嵌入式css样式必须写在`<style></style>`之间，并且一般情况下嵌入式css样式写在`<head></head>`之间。如右边编辑器中的代码。

### 外部式
外部式css样式(也可称为外联式)就是把css代码写一个单独的外部文件中，这个css样式文件以“.css”为扩展名，在`<head>`内（不是在`<style>`标签内）使用`<link>`标签将css样式文件链接到HTML文件内，如下面代码：

    <link href="base.css" rel="stylesheet" type="text/css" />

注意：

1、css样式文件名称以有意义的英文字母命名，如 main.css。

2、rel="stylesheet" type="text/css" 是固定写法不可修改。

3、`<link>`标签位置一般写在`<head>`标签之内。

### 三种方式的优先级
如果有一种情况：对于同一个元素我们同时用了三种方法设置css样式，那么哪种方法真正有效呢？

1、使用内联式CSS设置文字为粉色。

2、然后使用嵌入式CSS来设置文字为红色。

3、最后又使用外部式设置文字为蓝色（style.css文件中设置）。

但最终你可以观察到文本被设置为了粉色。因为这三种样式是有优先级的，记住他们的优先级：**内联式 > 嵌入式 > 外部式**

但是嵌入式>外部式有一个前提：嵌入式css样式的位置一定在外部式的后面。如`<link href="style.css" ...>代码在<style type="text/css">...</style>`

其实总结来说，就是--就近原则（离被设置元素越近优先级别越高。

# CSS选择器
## 什么是选择器？
每一条css样式声明（定义）由两部分组成，形式如下：

    选择器{
        样式;
    }
    
在{}之前的部分就是“选择器”，“选择器”指明了{}中的“样式”的作用对象，也就是“样式”作用于网页中的哪些元素。

标签选择器其实就是html代码中的标签。如右侧代码编辑器中的`<html>、<body>、<h1>、<p>、<img>`。例如下面代码：

    p{font-size:12px;line-height:1.6em;}
上面的css样式代码的作用：为p标签设置12px字号，行间距设置1.6em的样式。

## 类选择器
类选择器在css样式编码中是最常用到的，如右侧代码编辑器中的代码:可以实现为“胆小如鼠”、“勇气”字体设置为红色。

**语法**：

    .类选器名称{css样式代码;}
注意：

1、英文圆点开头

2、其中类选器名称可以任意起名（但不要起中文噢）

使用方法：

第一步：使用合适的标签把要修饰的内容标记起来，如下：

    <span>胆小如鼠</span>
第二步：使用class="类选择器名称"为标签设置一个类，如下：

    <span class="stress">胆小如鼠</span>
第三步：设置类选器css样式，如下：

    .stress{color:red;}/*类前面要加入一个英文圆点*/

## ID选择器


1、使用ID选择器，必须给标签添加上id属性，为标签设置id="ID名称"，而不是class="类名称"。

2、ID选择符的前面是井号（#）号，而不是英文圆点（.）。

3、id属性的值既为当前标签的id，尽量见名思意，语义化。


## ID和类选择器的区别


**相同点**：可以应用于任何元素

**不同点**：

1、ID选择器只能在文档中使用一次。与类选择器不同，在一个HTML文档中，ID选择器只能使用一次，而且仅一次。而类选择器可以使用多次。

下面代码是正确的：

     <p>三年级时，我还是一个<span class="stress">胆小如鼠</span>的小女孩，
     
     上课从来不敢回答老师提出的问题，生怕回答错了老师会批评我。就一直没有这个
     
     <span class="stress">勇气</span>来回答老师提出的问题。</p>
而下面代码是错误的：

     <p>三年级时，我还是一个<span id="stress">胆小如鼠</span>的小女孩，
     
     上课从来不敢回答老师提出的问题，生怕回答错了老师会批评我。就一直没有这个<span 
     id="stress">勇气</span>来回答老师提出的问题。</p>
     
2、可以使用类选择器词列表方法为一个元素同时设置多个样式。我们可以为一个元素同时设多个样式，但只可以用类选择器的方法实现，ID选择器是不可以的（不能使用 ID 词列表）。

下面的代码是正确的

    .stress{
        color:red;
    }
    .bigsize{
        font-size:25px;
    }
    <p>到了<span class="stress bigsize">三年级</span>下学期时，我们班上了一节公开课...</p>
上面代码的作用是为“三年级”三个文字设置文本颜色为红色并且字号为25px。

下面的代码是不正确的

    #stressid{
        color:red;
    }
    #bigsizeid{
        font-size:25px;
    }
    <p>到了<span id="stressid bigsizeid">三年级</span>下学期时，我们班上了一节公开课...</p>
上面代码不可以实现为“三年级”三个文字设置文本颜色为红色并且字号为25px的作用。

## 子选择器
还有一个比较有用的选择器子选择器，即大于符号(>),用于选择指定标签元素的第一代子元素。如右侧代码编辑器中的代码：

    .food>li{border:1px solid red;}
这行代码会使class名为food下的子元素li（水果、蔬菜）加入红色实线边框。

## 后代选择器
包含选择器，即加入空格,用于选择指定标签元素下的后辈元素。

    .first  span{color:red;}

请注意这个选择器与子选择器的区别，子选择器（child selector）仅是指它的直接后代，或者你可以理解为作用于子元素的第一代后代。而后代选择器是作用于所有子后代元素。后代选择器通过空格来进行选择，而子选择器是通过“>”进行选择。

> 总结：>作用于元素的第一代后代，空格作用于元素的所有后代。

## 通用选择器
通用选择器是功能最强大的选择器，它使用一个（*）号指定，它的作用是匹配html中所有标签元素，如下使用下面代码使用html中任意标签元素字体颜色全部设置为红色：

    * {color:red;}
    
## 伪选择器
更有趣的是伪类选择符，为什么叫做伪类选择符，它允许给html不存在的标签（标签的某种状态）设置样式，比如说我们给html中一个标签元素的鼠标滑过的状态来设置字体颜色：

    a:hover{color:red;}
上面一行代码就是为 a 标签鼠标滑过的状态设置字体颜色变红。这样就会使第一段文字内容中的“胆小如鼠”文字加入鼠标滑过字体颜色变为红色特效。

## 分组选择器

当你想为html中多个标签元素设置同一个样式时，可以使用分组选择符（，），如下代码为右侧代码编辑器中的h1、span标签同时设置字体颜色为红色：

    h1,span{color:red;}
它相当于下面两行代码：

    h1{color:red;}
    span{color:red;}
    
## CSS的继承
CSS的某些样式是具有继承性的，那么什么是继承呢？继承是一种规则，它允许样式不仅应用于某个特定html标签元素，而且应用于其后代。比如下面代码：如某种颜色应用于p标签，这个颜色设置不仅应用p标签，还应用于p标签中的所有子元素文本，这里子元素为span标签。

    p{color:red;}
    
    <p>三年级时，我还是一个<span>胆小如鼠</span>的小女孩。</p>
可见右侧结果窗口中p中的文本与span中的文本都设置为了红色。但注意有一些css样式是不具有继承性的。如border:1px solid red;

    p{border:1px solid red;}
    
    <p>三年级时，我还是一个<span>胆小如鼠</span>的小女孩。</p>
在上面例子中它代码的作用只是给p标签设置了边框为1像素、红色、实心边框线，而对于子元素span是没用起到作用的。

## 选择器优先级
1、如果一个元素使用了多个选择器,则会按照选择器的优先级来给定样式。

2、选择器的优先级依次是: 内联样式 > id选择器 > 类选择器 > 标签选择器 > 通配符选择器

## 标签权值
有的时候我们为同一个元素设置了不同的CSS样式代码，那么元素会启用哪一个CSS样式呢？下面我们一起来看一下代码：

    p{color:red;}
    .first{color:green;}
    <p class="first">三年级时，我还是一个<span>胆小如鼠</span>的小女孩。</p>
p和.first都匹配到了p这个标签上，那么会显示哪种颜色呢？green是正确的颜色，那么为什么呢？是因为浏览器是根据权值来判断使用哪种css样式的，权值高的就使用哪种css样式。

下面是权值的规则：

标签的权值为1，类选择符的权值为10，ID选择符的权值最高为100。例如下面的代码：

    p{color:red;} /*权值为1*/
    p span{color:green;} /*权值为1+1=2*/
    .warning{color:white;} /*权值为10*/
    p span.warning{color:purple;} /*权值为1+1+10=12*/
    #footer .note p{color:yellow;} /*权值为100+10+1=111*/
注意：还有一个权值比较特殊--继承也有权值但很低，有的文献提出它只有0.1，所以可以理解为继承的权值最低。

## 最高优先级
我们在做网页代码的时，有些特殊的情况需要为某些样式设置具有最高权值，怎么办？这时候我们可以使用!important来解决。

如下代码：

    p{color:red!important;}
    p{color:green;}
    <p class="first">三年级时，我还是一个<span>胆小如鼠</span>的小女孩。</p>
    这时 p 段落中的文本会显示的red红色。

注意：**!important**要写在分号的前面

这里注意当网页制作者不设置css样式时，浏览器会按照自己的一套样式来显示网页。并且用户也可以在浏览器中设置自己习惯的样式，比如有的用户习惯把字号设置为大一些，使其查看网页的文本更加清楚。这时注意样式优先级为：**浏览器默认的样式 < 网页制作者样式 < 用户自己设置的样式**，但记住!important优先级样式是个例外，权值高于用户自己设置的样式。

# 字体
## 更换字体
我们可以使用css样式为网页中的文字设置字体、字号、颜色等样式属性。下面我们来看一个例子，下面代码实现：为网页中的文字设置字体为宋体。

    body{font-family:"宋体";}
这里注意不要设置不常用的字体，因为如果用户本地电脑上如果没有安装你设置的字体，就会显示浏览器默认的字体。（因为用户是否可以看到你设置的字体样式取决于用户本地电脑上是否安装你设置的字体。）
现在一般网页喜欢设置“微软雅黑”，如下代码：

    body{font-family:"Microsoft Yahei";}
或

    body{font-family:"微软雅黑";}
注意：第一种方法比第二种方法兼容性更好一些。

## 字体大小、加粗、倾斜
可以使用下面代码设置网页中文字的字号为12像素：

    body{font-size:12px;}

我们还可以使用css样式来改变文字的样式：粗体、斜体、下划线、删除线，可以使用下面代码实现设置文字以粗体样式显示出来。

    p span{font-weight:bold;}
    
1、font-style可以设置字体样式，并且有种3设置方式。

2、正常字体为normal,也是font-style的默认值。

3、italic为设置字体为斜体，用于字体本身就有倾斜的样式。

4、oblique为设置倾斜的字体，强制将字体倾斜。

    p{font-style:italic}

## 字体颜色
技术点的解释：

1、color属性可以设置字体颜色。

2、color的值有3种设置方式：

英文命令颜色

    p{color:red;}
RGB颜色
这个与 photoshop 中的 RGB 颜色是一致的，由 R(red)、G(green)、B(blue) 三种颜色的比例来配色。

    p{color:rgb(133,45,200);}
每一项的值可以是 0~255 之间的整数，也可以是 0%~100% 的百分数。如：

    p{color:rgb(20%,33%,25%);}

十六进制颜色
这种颜色设置方法是现在比较普遍使用的方法，其原理其实也是 RGB 设置，但是其每一项的值由 0-255 变成了十六进制 00-ff。

    p{color:#00ffff;}
## font字体简写
网页中的字体css样式代码也有他自己的缩写方式，下面是给网页设置字体的代码：

    body{
        font-style:italic;
        font-weight:bold; 
        font-size:12px; 
        line-height:1.5em; 
        font-family:"宋体",sans-serif;
    }
这么多行的代码其实可以缩写为一句：

    body{
        font:italic  bold  12px/1.5em  "宋体",sans-serif;
    }
注意：

1、使用这一简写方式你至少要指定 font-size 和 font-family 属性，其他的属性(如 font-weight、font-style、font-variant、line-height)如未指定将自动使用默认值。

2、在缩写时 font-size 与 line-height 中间要加入“/”斜扛。

一般情况下因为对于中文网站，英文还是比较少的，所以下面缩写代码比较常用：

    body{
        font:12px/1.5em  "宋体",sans-serif;
    }
只是有字号、行间距、中文字体、英文字体设置。

# 文本样式
## 划线
1、text-decoration可以设置添加到文本的修饰。

2、text-decoration默认值为none, 定义标准的文本。

3、text-decoration的值为underline为定义文本下的一条线。

4、text-decoration的值为overline为定义文本上的一条线。

5、text-decoration的值为line-through为定义穿过文本下的一条线，一般用于商品折扣价。

## 首行缩进
**语法**

    p{text-indent:2em;}
    
## 行间距

    p{line-height:1.5em;}
    
## 字符间距
中文字间隔、字母间隔设置：

如果想在网页排版中设置文字间隔或者字母间隔就可以使用    letter-spacing 来实现，如下面代码：

    h1{
        letter-spacing:50px;
    }
    ...
    <h1>了不起的盖茨比</h1>
注意：这个样式使用在英文单词时，是设置字母与字母之间的间距。

单词间距设置：

如果我想设置英文单词之间的间距呢？可以使用 word-spacing 来实现。如下代码：

    h1{
        word-spacing:50px;
    }
    ...
    <h1>welcome to imooc!</h1>
    
## 排列方式

想为块状元素中的文本、图片设置居中样式，可以使用text-align样式代码，如下代码可实现文本居中显示。

    h1{
        text-align:center;
    }
    <h1>了不起的盖茨比</h1>
同样可以设置居左：

    h1{
        text-align:left;
    }
    <h1>了不起的盖茨比</h1>
还可以设置居右：

    h1{
        text-align:right;
    }
    <h1>了不起的盖茨比</h1>
    
## 长度值
长度单位总结一下，目前比较常用到px（像素）、em、% 百分比，要注意其实这三种单位都是相对单位。

1、像素

像素为什么是相对单位呢？因为像素指的是显示器上的小点（CSS规范中假设“90像素=1英寸”）。实际情况是浏览器会使用显示器的实际像素值有关，在目前大多数的设计者都倾向于使用像素（px）作为单位。

2、em

就是本元素给定字体的 font-size 值，如果元素的 font-size 为 14px ，那么 1em = 14px；如果 font-size 为 18px，那么 1em = 18px。如下代码：

    p{font-size:12px;text-indent:2em;}
上面代码就是可以实现段落首行缩进 24px（也就是两个字体大小的距离）。

下面注意一个特殊情况：

但当给 font-size 设置单位为 em 时，此时计算的标准以 p 的父元素的 font-size 为基础。如下代码：

html:

    <p>以这个<span>例子</span>为例。</p>
css:

    p{font-size:14px}
    span{font-size:0.8em;}
结果 span 中的字体“例子”字体大小就为 11.2px（14 * 0.8 = 11.2px）。

3、百分比

    p{font-size:12px;line-height:130%}
设置行高（行间距）为字体的130%（12 * 1.3 = 15.6px）。

# CSS盒模型
## 元素分类
在CSS中，html中的标签元素大体被分为三种不同的类型：块状元素、内联元素(又叫行内元素)和内联块状元素。

常用的块状元素有：

`<div>、<p>、<h1>...<h6>、<ol>、<ul>、<dl>、<table>、<address>、<blockquote> 、<form>`

常用的内联元素有：

`<a>、<span>、<br>、<i>、<em>、<strong>、<label>、<q>、<var>、<cite>、<code>`

常用的内联块状元素有：

`<img>、<input>`

## 块元素
什么是块级元素？在html中`<div>、 <p>、<h1>、<form>、<ul> `和 `<li>`就是块级元素。设置display:block就是将元素显示为块级元素。如下代码就是将内联元素a转换为块状元素，从而使a元素具有块状元素特点。

`a{display:block;}`
块级元素特点：

1、每个块级元素都从新的一行开始，并且其后的元素也另起一行。

2、元素的高度、宽度、行高以及顶和底边距都可设置。

3、元素宽度在不设置的情况下，是它本身父容器的100%（和父元素的宽度一致），除非设定一个宽度。

## 内联元素
在html中，`<span>、<a>、<label>、 <strong>` 和`<em>`就是典型的内联元素（行内元素）（inline）元素。当然块状元素也可以通过代码display:inline将元素设置为内联元素。如下代码就是将块状元素div转换为内联元素，从而使 div 元素具有内联元素特点。

     div{
         display:inline;
     }
    
    ......
    
    <div>我要变成内联元素</div>
    内联元素特点：

1、和其他元素都在一行上；

2、元素的高度、宽度及顶部和底部边距不可设置；

3、元素的宽度就是它包含的文字或图片的宽度，不可改变。

## 内联块状元素
内联块状元素（inline-block）就是同时具备内联元素、块状元素的特点，代码display:inline-block就是将元素设置为内联块状元素。(css2.1新增)，`<img>、<input>`标签就是这种内联块状标签。

inline-block 元素特点：

1、和其他元素都在一行上；

2、元素的高度、宽度、行高以及顶和底边距都可设置。

## 元素隐藏
none设置此元素不会被显示，当想要元素隐藏的时候可以使用此值。

## 盒子模型长宽
盒模型宽度和高度和我们平常所说的物体的宽度和高度理解是不一样的，css内定义的宽（width）和高（height），指的是填充以里的内容范围。

因此一个元素实际宽度（盒子的宽度）=左边界+左边框+左填充+内容宽度+右填充+右边框+右边界。
![](https://cdn.jsdelivr.net/gh/Fazziekey/image-bed@master/2020/07/28/50582b4bd6adf5aa7daf256cb59cb258.png)


元素的高度也是同理。

比如：

css代码：

    div{
        width:200px;
        padding:20px;
        border:1px solid red;
        margin:10px;    
    }
html代码：

    <body>
       <div>文本内容</div>
    </body>
元素的实际长度为：10px+1px+20px+200px+20px+1px+10px=262px。在chrome浏览器下可查看元素盒模型，如下图：

![](https://cdn.jsdelivr.net/gh/Fazziekey/image-bed@master/2020/07/28/443afb8d1153a2a42ea2552f6f477c0b.png)

## 设置背景色
网页中的标签不论是行内元素还是块状元素都可以给它设置一个背景色。

为标签设置背景颜色可以使background-color:颜色值来实现。

例子如下：

    div{background-color:red;}//为块状元素设置
    a{background-color:green;}//为行内元素设置
    
## 盒子边框
盒子模型的边框就是围绕着内容及补白的线，这条线你可以设置它的粗细、样式和颜色(边框三个属性)。

如下面代码为 div 来设置边框粗细为 2px、样式为实心的、颜色为红色的边框：

    div{
        border:2px  solid  red;
    }
上面是 border 代码的缩写形式，可以分开写：

    div{
        border-width:2px;
        border-style:solid;
        border-color:red;
    }
注意：

1、border-style（边框样式）常见样式有：

dashed（虚线）| dotted（点线）| solid（实线）。


2、border-color（边框颜色）中的颜色可设置为十六进制颜色，如:

    border-color:#888;//前面的井号不要忘掉。

3、border-width（边框宽度）中的宽度也可以设置为：

thin | medium | thick（但不是很常用），最常还是用像素（px）。

### 特定边框
现在有一个问题，如果有想为 p 标签单独设置下边框，而其它三边都不设置边框样式怎么办呢？css 样式中允许只为一个方向的边框设置样式：

    div{border-bottom:1px solid red;}
同样可以使用下面代码实现其它三边(上、右、左)边框的设置：

    border-top:1px solid red;
    border-right:1px solid red; 
    border-left:1px solid red;
    
## 加入圆角

元素边框的圆角效果可以使用border-radius属性来设置。圆角可分为左上、右上、右下、左下。如下代码：

     div{border-radius: 20px 10px 15px 30px;}

也可以分开写：

    div{
        border-top-left-radius: 20px;
       border-top-right-radius: 10px;
       border-bottom-right-radius: 15px;
       border-bottom-left-radius: 30px;
    }
如果四个圆角都为10px;可以这么写：

    div{ border-radius:10px;}
如果左上角和右下角圆角效果一样为10px，右上角和左下角圆角一样为20px，可以这么写：

    div{ border-radius:10px 20px;}
需要特别注意的：一个正方形，当设置圆角效果值为元素宽度一半时，显示效果为圆形。例如：

     div {
            width: 200px;
            height: 200px;
            border: 5px solid red;
            border-radius: 100px;
        }

也可以写为百分比50%

     div {
            width: 200px;
            height: 200px;
            border: 5px solid red;
            border-radius: 100px;
        }

## 设置内边距
元素内容与边框之间是可以设置距离的，称之为“内边距（填充）”。填充也可分为上、右、下、左(顺时针)。如下代码：

    div{padding:20px 10px 15px 30px;}
    
顺序一定不要搞混。可以分开写上面代码：

    div{
       padding-top:20px;
       padding-right:10px;
       padding-bottom:15px;
       padding-left:30px;
    }
如果上、右、下、左的填充都为10px;可以这么写

    div{padding:10px;}
如果上下填充一样为10px，左右一样为20px，可以这么写：

    div{padding:10px 20px;}

## 外边距
元素与其它元素之间的距离可以使用边界（margin）来设置。边界也是可分为上、右、下、左。如下代码：

    div{margin:20px 10px 15px 30px;}

也可以分开写：

    div{
       margin-top:20px;
       margin-right:10px;
       margin-bottom:15px;
       margin-left:30px;
    }
如果上右下左的边界都为10px;可以这么写：

    div{ margin:10px;}
如果上下边界一样为10px，左右一样为20px，可以这么写：

    div{ margin:10px 20px;}
总结一下：padding和margin的区别，padding在边框里，margin在边框外。

# CSS布局模型
布局模型与盒模型一样都是 CSS3 最基本、 最核心的概念。 但布局模型是建立在盒模型基础之上，又不同于我们常说的 CSS3 布局样式或 CSS3 布局模板。如果说布局模型是本，那么 CSS3 布局模板就是末了，是外在的表现形式。 
CSS3包含3种基本的布局模型，用英文概括为：Flow、Layer 和 Float。
在网页中，元素有三种布局模型：

1、流动模型（Flow）

2、浮动模型 (Float)

3、层模型（Layer）

## 流动模型
流动（Flow）是默认的网页布局模式。也就是说网页在默认状态下的 HTML 网页元素都是根据流动模型来分布网页内容的。

流动布局模型具有2个比较典型的特征：

第一点，块状元素都会在所处的包含元素内自上而下按顺序垂直延伸分布，因为在默认状态下，块状元素的宽度都为100%。实际上，块状元素都会以行的形式占据位置。如右侧代码编辑器中三个块状元素标签(div，h1，p)宽度显示为100%。

第二点，在流动模型下，内联元素都会在所处的包含元素内从左到右水平分布显示。

## 浮动模型
任何元素在默认情况下是不能浮动的，但可以用 CSS 定义为浮动，如 div、p、table、img 等元素都可以被定义为浮动。如下代码可以实现两个 div 元素一行显示。

    div{
        width:200px;
        height:200px;
        border:2px red solid;
        float:left;
    }

当然你也可以同时设置两个元素右浮动也可以实现一行显示。

    div{
        width:200px;
        height:200px;
        border:2px red solid;
        float:right;
    }


两个元素一左一右可以实现一行显示吗？

    div{
        width:200px;
        height:200px;
        border:2px red solid;
    }

## 层模型
什么是层布局模型？层布局模型就像是图像软件PhotoShop中非常流行的图层编辑功能一样，每个图层能够精确定位操作，但在网页设计领域，由于网页大小的活动性，层布局没能受到热捧。但是在网页上局部使用层布局还是有其方便之处的。

如何让html元素在网页中精确定位，就像图像软件PhotoShop中的图层一样可以对每个图层能够精确定位操作。CSS定义了一组定位（positioning）属性来支持层布局模型。

层模型有三种形式：

1、绝对定位(position: absolute)

2、相对定位(position: relative)

3、固定定位(position: fixed)

### 绝对定位
如果想为元素设置层模型中的绝对定位，需要设置position:absolute(表示绝对定位)，这条语句的作用将元素从文档流中拖出来，然后使用left、right、top、bottom属性相对于其最接近的一个具有定位属性的父包含块进行绝对定位。如果不存在这样的包含块，则相对于body元素，即相对于浏览器窗口。

如下面代码可以实现div元素相对于浏览器窗口向右移动100px，向下移动50px。

    div{
        width:200px;
        height:200px;
        border:2px red solid;
        position:absolute;
        left:100px;
        top:50px;
    }
    <div id="div1"></div>
  
## 相对定位    
    如果想为元素设置层模型中的相对定位，需要设置position:relative（表示相对定位），它通过left、right、top、bottom属性确定元素在正常文档流中的偏移位置。相对定位完成的过程是首先按static(float)方式生成一个元素(并且元素像层一样浮动了起来)，然后相对于以前的位置移动，移动的方向和幅度由left、right、top、bottom属性确定，偏移前的位置保留不动。

如下代码实现相对于以前位置向下移动50px，向右移动100px;

    #div1{
        width:200px;
        height:200px;
        border:2px red solid;
        position:relative;
        left:100px;
        top:50px;
    }
    
    <div id="div1"></div>

### 固定定位
fixed：表示固定定位，与absolute定位类型类似，但它的相对移动的坐标是视图（屏幕内的网页窗口）本身。由于视图本身是固定的，它不会随浏览器窗口的滚动条滚动而变化，除非你在屏幕中移动浏览器窗口的屏幕位置，或改变浏览器窗口的显示大小，因此固定定位的元素会始终位于浏览器窗口内视图的某个位置，不会受文档流动影响，这与background-attachment:fixed;属性功能相同。以下代码可以实现相对于浏览器视图向右移动100px，向下移动50px。并且拖动滚动条时位置固定不变。

    #div1{
        width:200px;
        height:200px;
        border:2px red solid;
        position:fixed;
        left:100px;
        top:50px;
    }
    
## Relative与Absolute组合使用

1、参照定位的元素必须是相对定位元素的前辈元素：

    <div id="box1"><!--参照定位的元素-->
        <div id="box2">相对参照元素进行定位</div><!--相对定位元素-->
    </div>
从上面代码可以看出box1是box2的父元素（父元素当然也是前辈元素了）。

2、参照定位的元素必须加入position:relative;

    #box1{
        width:200px;
        height:200px;
        position:relative;        
    }
3、定位元素加入position:absolute，便可以使用top、bottom、left、right来进行偏移定位了。

    #box2{
        position:absolute;
        top:20px;
        left:30px;         
    }
这样box2就可以相对于父元素box1定位了（这里注意参照物就可以不是浏览器了，而可以自由设置了）。

# 弹性盒模型

    <style type="text/css">
        .box {
            background: blue;
            display: flex;
        }
    
        .box div {
            width: 200px;
            height: 200px;
        }
    
        .box1 {
            background: red;
        }
    
        .box2 {
            background: orange;
        }
    
        .box3 {
            background: green;
        }
        </style>
    </head>
    
    <body>
        <div class="box">
            <div class="box1"></div>
            <div class="box2"></div>
            <div class="box3"></div>
        </div>
    </body>
上面的代码：

三个块元素设置大小以及背景色，在父容器中添加flex。

技术点的解释：

1、设置display: flex属性可以把块级元素在一排显示。

2、flex需要添加在父元素上，改变子元素的排列顺序。

3、默认为从左往右依次排列,且和父元素左边没有间隙。

## 横轴排列
justify-content属性，本属性定义了项目在主轴上的对齐方式。结合上一节的布局例子进行理解，属性值分别为：

     justify-content: flex-start | flex-end | center | space-between | space-around;
     
flex-start：交叉轴的起点对齐

     .box {
            background: blue;
            display: flex;
            justify-content: flex-start;
        }
flex-end：右对齐

     .box {
            background: blue;
            display: flex;
            justify-content: flex-end;
        }

center： 居中

     .box {
            background: blue;
            display: flex;
            justify-content: center;
        }


space-between：两端对齐，项目之间的间隔都相等。

     .box {
            background: blue;
            display: flex;
            justify-content: space-between;
        }




space-around：每个项目两侧的间隔相等。所以，项目之间的间隔比项目与边框的间隔大一倍。

    .box {
            background: blue;
            display: flex;
            justify-content: space-around;
        }
        
## 竖轴
align-items属性定义了项目在交叉轴上的对齐方式。属性值分别为：

align-items: flex-start | flex-end | center | baseline | stretch;
结合右侧编辑器中的布局以及下面的样式设置进行理解：

flex-start：默认值，左对齐
    
       .box {
            height: 700px;
            background: blue;
            display: flex;
            align-items: flex-start;
        }




flex-end：交叉轴的终点对齐

     .box {
            height: 700px;
            background: blue;
            display: flex;
            align-items: flex-end;
        }



center： 交叉轴的中点对齐

    .box {
            height: 700px;
            background: blue;
            display: flex;
            align-items: center;
        }




baseline：项目的第一行文字的基线对齐。

    .box {
            height: 700px;
            background: blue;
            display: flex;
            align-items: baseline;
        }
三个盒子中设置不同的字体大小，可以参考右侧编辑器中的代码进行测试。

stretch（默认值）：如果项目未设置高度或设为auto，将占满整个容器的高度。

     .box {
            height: 300px;
            background: blue;
            display: flex;
            align-items: stretch;
        }

    .box div {
        /*不设置高度，元素在垂直方向上铺满父容器*/
        width: 200px;
    }

## 子元素占比
1、给子元素设置flex属性,可以设置子元素相对于父元素的占比。

2、flex属性的值只能是正整数,表示占比多少。

3、给子元素设置了flex之后,其宽度属性会失效。


