---
title: MySQL
date: 2020-07-25 21:40:41
copyright: true
tags:
    - SQL
categories: 
    - 《栈溢出工程师》
---
## 连接
命令行cd到目录

`C:\Program Files\MySQL\MySQL Server 8.0\bin`

    mysql -u root -p
<!--more-->
## 数据操作
### 添加删除数据
#### 查看DB
    show databases
#### 添加DB
    create database gc
#### 删除DB
    drop database gc
> gc 为数据库名

## 数据类型

### 文本类型
数据类型 | 描述
---|---
CHAR(size) |保存固定长度的字符串(可包含字母、数字以及特殊字符)●在括号中指定字符串的长度。最多255个字符。
VARCHAR(size) | 保存可变长度的字符串(可包含字母、数字以及特殊字符)。在括号中指定字符串的最大长度。最多255个字符。注释:如果值的长度大于255，则被转换为TEXT类型。
TINYTEXT | 存放最大长度为255个字符的字符串。
TEXT | 存放最大长度为65,535个字符的字符串。
BLOB | 用于BLOBs (Binary Large OBjects).存放最多65,535字节的数据。
MEDIUMTEXT | 存放最大长度为16,777,215 个字符的字符串。
MEDIUMBLOB | 用于BLOBs (Binary Large OBjects)。存放最多16,777,215 字节的数据。
LONGTEXT | 存放最大长度为4,294,967,295个字符的字符串。
LONGBLOB | 用于BLOBs (Binary Large OBjects).存放最多4,294,967,295字节的数据。
ENUM(x,y,z,etc.) | 允许你输入可能值的列表。可以在ENUM列表中列出最大65535个值。如果列表中不存在插入的值，则插入空值。注释:这些值是按照你输入的顺序存储的。可以按照此格式输入可能的值: ENUM('X',"Y',;Z')
SET | 与ENUM类似，SET最多只能包含64个列表项，不过SET可存储一个以上的值。

### 数字类型



数据类型 | 描述
---|---
TINYINT(size) | -128到127常规。0到255无符号*。在括号中规定最大位数。
SMALLINT(size) | -32768到32767常规。0到65535无符号*。在括号中规定最大位数。
MEDIUMINT(size) | -8388608到8388607普通。0 to 16777215无符号*。在括号中规定最大位数。
INT(size) | -2147483648到2147483647常规。0到4294967295无符号*。在括号中规定最大位数。
BIGINT(size) | -9223372036854775808到9223372036854775807常规。0到18446744073709551615无符号*。在括号中规定最大位数。
FLOAT(size,d) | 带有浮动小数点的小数字。在括号中规定最大位数。在d参数中规定小数点右侧的最大位数。
DOUBLE(size,d) | 带有浮动小数点的大数字。在括号中规定最大位数。在d参数中规定小数点右侧的最大位数。
DECIMAL(size,d) | 作为字符串存储的DOUBLE类型，允许固定的小数点。

### 日期类型
数据类型 | 描述
---| ---
DATE() | 日期。格式: YYYY-MM-DD注释:支持的范围是从*1000-01-01'到'9999-12-31'
DATETIME() | *日期和时间的组合。格式: YYYY-MM-DD HH:MM:SS注释:支持的范围是从'1000-01-01 00:00:00'到'9999-12-31 23:59:59'
TIMESTAMP() | *时间戳。TIMESTAMP值使用Unix纪元('1970-01-01 00:00:00 UTC)至今的描述来存储。格式: YYYY-MM-DD HH:MM:SS注释:支持的范围是从 *1970-01-0100:00:01 UTC到'2038-01 -0903:14:07' utC
TIME() | 时间。格式: HH:MM:SS注释:支持的范围是从'-838:59:59'到'838:59:59'
YEAR() | 2位或4位格式的年。注释: 4位格式所允许的值: 1901到2155。2位格式所允许的值: 70到69，表示从1970到2069.

## 创建数据表
    create table table_ name (
    colum_ name data_ _type,
    colum_ name data_ type,
    .
    colum_ name data_type
    );

### 例子
    CREATE TABLE account (
    id bigint(20)
    create Time datetime,
    ip varchar(255),
    mobile varchar(255),
    nickname varchar(255),
    passwd varchar(255)，
    username varchar(255),
    avatar varchar(255),
    brief text,
    job varchar(255),
    location varchar(255),
    qq varchar(255), 
    gender int(11)，
    city varchar(255),
    province varchar(255)
    );

### 基本操作

    use gc;#使用数据库
    show tables;#展示数据表
    create account(colum type);#创建数据表
    describe account#查看数据表
    drop account;#删除数据表

## 增加删除行列
### 增加
`alter table [ table_ name ] add [ column_ name][ data_ _type ]
[not null] [default ]`

例子:

    alter table account add c1 int(11) not null default 1;
### 删除
`alter table[ table_ name ] drop[ column_ name ]`

例子:

    alter table account drop c1;

## 修改列信息
`alter table[ table_ name ] change [ old_ column_ name ] [ new_ column_ name ]
[data_ type ]`

1.只改列名:
data_ type和原来一样，old_ _column_ name != new_ column_ name

2.只改数据类型:
old_ column_ name == new_ column_ name, data_ type改变

3.列名和数据类型都改了

## 插入和查看表的数据
### 查看
`select * from table_ name;`

`select col_ name 1 ,col_ name2, ... from table_ name;`
### 插入
`insert into[ tabte_ name ] values(值1, 值....`

`insert into [table_ name] (列1， 列2...) values(值1,值...`

## where 条件
`select * from table_ name where col_ name运算符值`

例子:

    select * from book where title = = t’ ;

### 运算符
运算符 | 描述
--- |---
= | 等于
!= | 不等于
`>` | 大于
< | 小于.
>= | 大于等于
<= |小于等于
between | 在两个值范围内
like | 按某个模式查找

### 组合条件
where后面可以通过and与or运算符组合多个条件筛选

语法:

`select * from table_ name
where toll
=XXXandcol2=XXorcol3>XX`

## null字段的判断
NULL字段无法直接查询

+ 正确 

select * from book where id is null

+ 错误 

select * from book where id = null

## distinct语句
`select distinct col_ name from table_ name ;`

例子:

    select distinct title from book;

> select 语句可以去除重复的语句

## order by对查询结果进行排序

**1.按单一列名排序:**

select * from table_ name [where子句] order by col_ name [asc/desc]

**2.按多列排序:**

select * from table_ name [where子句] order by coll [asc/desc]，col2
[asc,desc]

> asc升序
desc降序

## limit截取查询结果
`select * from table_ name [where子句] [order by子句] limit [offset,] rowCount`

offset:查询结果的起始位置，第一 条记录的其实是0
rowCount:从offset位置开始，获取的记录条数

注意
limit rowCount = limit 0,rowCount

> 作用：截取页面

## 插入命令和查询命令select的组合使用

**一般用法:**

`insert into [表名] values(值1, 值.....`

`insert into[表名] (列1 ，列2...) values(值1,值....`

**Insert into与select的组合用法**

`insert into [表名1] select 列1，列2 from [表名2]`

`insert into 
[表名1]
(列1，列2)
select列3，列4 from
[表名2]`

> 作用：数据迁移

## 更新表的数据

**修改单列:**

`update表名set列名= XXX [where字句]`

**修改多列:**

`update表名set列名1 = xxx,列名2 = xxX... [where 字句]`

## where语句中in,like,between的使用

### in
`select * from表名where列名in (value1 ,value2..)`

`select * from表名where列名in (select 列名from表名)`

例子

    select * from book where title in('sun','color')

### betweeen
`select * from表名where列名between值1 and值2`

`select * from表名where列名not between值1 and值2`

### like
**作用：字符模糊匹配**

`select * from表名where列名[not] like pattern`

**pattern:匹配模式**

比如
`'abc'%abc’,‘abc%’,'%abc%'` ;
“`%`” 是一个通配符，理解_上可以把他当成任何字符串

**例子:**

`'%abc'`
能匹配
`'erttsabc'`













