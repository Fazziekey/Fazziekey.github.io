---
title: Mark Down语法从入门到放弃
date: 2020-04-16 08:47:08
copyright: true
tags:
---
## 一、标题
1.使用#表示标题，其中#号必须在行首

# 一级标题
## 二级标题
### 三级标题
#### 四级标题
##### 五级标题
###### 六级标题
<!--more-->
2.或者用'=====' '----'表示

一级标题
=======

二级标题
-------

- - -
## 二、分割线
使用三个以上'-'或‘ * ’ 表示

## 三、斜体和粗体
使用‘ * ’和‘* ’分别表示斜体和粗体
*斜体* **粗体** ***又斜有粗***

## 四、超链接和图片
写法1：[第一种写法]（www.baidu.com)
写法2：[第二种写法][1]
[1]:www.baidu.com
图片插入：在超链接前+一个‘！’
![echo](http://i2.tiimg.com/716502/c981609de1b23f6e.jpg)

## 五、无序列表
使用‘+ ’ ‘- ’ ‘* ’
+ 一层
	- 两层
		* 三层
			+ 四层

## 六、有序列表
使用‘ 1. ’点号后有空格
1. 你在第一层
	1. 我在第五层

## 七、文字引用
使用‘> ’ 表示
> 第一层
>> 第二层
>>> 第三层

## 八、行内代码块
使用\`表示`\`为转义字符

## 九、代码块
使用四个空格缩进表示代码块

    str='hello world'
    for i in range(11): 
    	print(str[i])

## 十、表格
第二行表示对齐方式
`|---|---:|:---:|`
默认左对齐

|X|Y|与|或|非X|
|---|---|---|---:|:---:|
|0|0|0|0|1|
|0|1|0|1|1|
|1|0|0|1|0|
|1|1|1|1|0|

## 十一、流程图
主要的语法为 `name=>type: describe，`其中 type 主要有以下几种：
1.开始和结束：`start end`
2.输入输出：`inputoutput`
3.操作：`operation`
4.条件：`condition`
5.子程序：`subroutine`

$$

st=>start: Start
io=>inputoutput: input your nuber
op=>operation: operate
cond=>condition: right or no
sub=>subroutine: you choice
e=>end

st->io->op->cond
cond(yes)->e
cond(no)->sub->io
$$

## 十二、数学公式

使用 $ 表示，其中一个 \$ 表示在行内，两个 \$ 表示独占一行。

`eg : $\sum_{i=1}^n a_i=0$

$$\sum_{i=1}^n a_i=0$$


