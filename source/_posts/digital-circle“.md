---
title: 数字电路笔记
toc: true
copyright: true
date: 2020-08-30 14:38:11
tags:
    - 数字电路
categories:
    - 《行于黑暗，侍奉光明，我们是电工》
reward:
---
# 逻辑运算
## 基本公式
<!--more-->

![](https://cdn.jsdelivr.net/gh/Fazziekey/image-bed@master/2020/08/29/8e92915a66d8d4f231c227da492da482.png)

![](https://cdn.jsdelivr.net/gh/Fazziekey/image-bed@master/2020/08/29/29b4891c74db0d44aeb0aa57f0b3b7a5.png)
-------------------
## 基本定理
### 代入定理
### 反演定理
-------------------
## 逻辑函数表示方法
+ 真值表
+ 逻辑式
    + 将输入/输出之间的逻辑关系用与/或/非的运算式表示 就得到逻辑式
+ 逻辑图
+ 波形图
+ 卡诺图

## 标准形式
+ 最小项之和
    + 利用公式:A=(B'+B)A 
    + A'B'C'=000=m0
+ 最大项之积
    + A+B+C=000=M0
    + A'+B'+C'=111=M7
### 转化方式
$$
Y=\sum m_i
$$
$$
\to Y'=\sum_{k=\not i} m_k
$$
$$
\to Y=(\sum_{k=\not i} m_k)'
$$
$$
\to Y=\prod_{i=\not k}m_k'=\prod_{i=\not k}M_k'
$$



## 逻辑函数化简
### 公式法
+ AB+A'C+BC=AB+A'C
+ A+AB=A
### 卡诺图
- 用卡诺图表示逻辑函数
- 找出可合并的最小项
- 化简后的乘积项相加

#### 约束项
在逻辑函数中，对输入变量取值的 限制，在这些取值下为1的最小项称 为约束项
#### 任意项
在输入变量某些取值下，函数值为1或 为0不影响逻辑电路的功能，在这些取 值下为1的最小项称为任意项

### 常用编码
#### 补码反码
**反码**
$$
(N)_{1NV}=
\begin{cases}
N&N>0\\
2^n-1-N&N<0
\end{cases}
$$
负数补码为反码+1

#### 格雷码
![](https://cdn.jsdelivr.net/gh/Fazziekey/image-bed@master/2020/08/29/4b23dcbbf4bbab30acb637c5144ca451.png)
 
# 组合逻辑
### 特点
+ 任意时刻输出仅取决于输入，没有反馈
+ 不含存储单元

## 编码器
### 普通编码器

![](https://cdn.jsdelivr.net/gh/Fazziekey/image-bed@master/2020/08/29/3dafecfcfdb8748e3b78aefe984b2e56.png)


### 优先编码器

![](https://cdn.jsdelivr.net/gh/Fazziekey/image-bed@master/2020/08/29/3dafecfcfdb8748e3b78aefe984b2e56.png)

### 两片编码器合并
![](https://cdn.jsdelivr.net/gh/Fazziekey/image-bed@master/2020/08/29/47318ffa87981c9121cb533abd61cec9.png)

## 译码器
![](https://cdn.jsdelivr.net/gh/Fazziekey/image-bed@master/2020/08/29/6407612531b958e19cb0b0c1d2a69d37.png)

## 数据选择器
![](https://cdn.jsdelivr.net/gh/Fazziekey/image-bed@master/2020/08/29/3d478372091bf08492331f428a6cad30.png)
## 半加器
![](https://cdn.jsdelivr.net/gh/Fazziekey/image-bed@master/2020/08/29/9e65b07450d9abe5d27e2c5e0a2388a0.png)
## 全加器
![](https://cdn.jsdelivr.net/gh/Fazziekey/image-bed@master/2020/08/29/ef91ccff1032bc06f75fcee2dae18e95.png)
### 用半加器实现全加器
![](https://cdn.jsdelivr.net/gh/Fazziekey/image-bed@master/2020/08/29/44f8cad67b8c43ce2173ec6d607e35d9.png)

## 数值比较器
![](https://cdn.jsdelivr.net/gh/Fazziekey/image-bed@master/2020/08/29/8dd053a1a2eebc458891eb36e144a730.png)
### 多位数值比较器
![](https://cdn.jsdelivr.net/gh/Fazziekey/image-bed@master/2020/08/29/7b7a86568eebce30b90f40ded69963e7.png)
### 组合电路的竞争和冒险

![](https://cdn.jsdelivr.net/gh/Fazziekey/image-bed@master/2020/08/29/db54f98d06b427de82aeee77fb6804c4.png)
增加冗余项可以消除改现象

-----------------



# 触发器
**如何存储数据？**
## SR锁存器
![](https://cdn.jsdelivr.net/gh/Fazziekey/image-bed@master/2020/08/29/630ef5c5f7c05305a877cfc57244a195.png)
![](https://cdn.jsdelivr.net/gh/Fazziekey/image-bed@master/2020/08/29/a65bb1bd7eb84e3a2bd20298f9efd50b.png)
![](https://cdn.jsdelivr.net/gh/Fazziekey/image-bed@master/2020/08/29/c5ca359b23826a6067feb32316409faf.png)


## 电平触发器
+ 只有在clk信号为高电平时才会改变输出
+ 缺陷：抗干扰能力差

![](https://cdn.jsdelivr.net/gh/Fazziekey/image-bed@master/2020/08/29/e6452f3b86dbd3673f433dedb121c2cd.png)
![](https://cdn.jsdelivr.net/gh/Fazziekey/image-bed@master/2020/08/29/d7bcf2a902a5de57da284a9659bf3065.png)
## 边沿触发器

+ 仅在电平上升下降沿发生变化 
![](https://cdn.jsdelivr.net/gh/Fazziekey/image-bed@master/2020/08/29/5cef502bbb8a6f5462c3872ac4273d01.png)
![](https://cdn.jsdelivr.net/gh/Fazziekey/image-bed@master/2020/08/29/c47c4c90ad167daf01aacd2801e9f889.png)
## 脉冲触发器
+ 把边沿触发器的D触发器变为SR触发器
+ 在clk高电平期间所有输入决定下降沿时的输出变化，因为SR都变为0时第一个触发器输出不变
![](https://cdn.jsdelivr.net/gh/Fazziekey/image-bed@master/2020/08/29/b68a8737431ccac41aaa799f2eb60d97.png)
![](https://cdn.jsdelivr.net/gh/Fazziekey/image-bed@master/2020/08/29/33ced500518724939bd310f16b69d7e7.png)
## 锁存器分类
![](https://cdn.jsdelivr.net/gh/Fazziekey/image-bed@master/2020/08/29/d7461cd449d4a8f8eeec95571e8d3ff8.png)
![](https://cdn.jsdelivr.net/gh/Fazziekey/image-bed@master/2020/08/29/e8a7d67812a0223a51e2be60e9994da4.png)
![](https://cdn.jsdelivr.net/gh/Fazziekey/image-bed@master/2020/08/29/bc22041af8755f0c05a063ee16e55152.png)
![](https://cdn.jsdelivr.net/gh/Fazziekey/image-bed@master/2020/08/29/24e4f04968e85fa665547aa6d3416e45.png)

### D触发器实现JK触发器
![](https://cdn.jsdelivr.net/gh/Fazziekey/image-bed@master/2020/08/19/6b9b912c12513e9003768e5b131de9b5.png)

> RS，T触发器都可以用JK触发器转化

## 触发器动态特性
+ 建立时间
+ 保持时间
+ 传输延迟时间
+ 最高时钟频率
-------------------



# 时序电路
## 时序逻辑电路类型
+ Mealy型
    + 输出信号取决于存储电路状态和输入变量
+ Moore型
    + 输出只是存储电路现态的函数
    + 输出与时钟同步
### 三个方程
+ 驱动方程
+ 状态方程
+ 输出方程


### 移位寄存器
![](https://cdn.jsdelivr.net/gh/Fazziekey/image-bed@master/2020/08/29/bf1491725d774e6f6a34c59b1c25f102.png)

### 计数器
![](https://cdn.jsdelivr.net/gh/Fazziekey/image-bed@master/2020/08/29/338638bd127f0db616eb85bb84bacf50.png)
![](https://cdn.jsdelivr.net/gh/Fazziekey/image-bed@master/2020/08/29/50be44c389dee6a5afd71faf0ae7c04c.png)
#### 计数器设计
![](https://cdn.jsdelivr.net/gh/Fazziekey/image-bed@master/2020/08/29/6016833e368c940d14e84ac4bbbd568d.png)
![](https://cdn.jsdelivr.net/gh/Fazziekey/image-bed@master/2020/08/29/3e922bc992d2b179a0e86a1b3deea238.png)
![](https://cdn.jsdelivr.net/gh/Fazziekey/image-bed@master/2020/08/29/5c53976db301e995f1a45e296b027df8.png)



# 存储器与可编程逻辑阵列
## 只读存储器ROM

![](https://cdn.jsdelivr.net/gh/Fazziekey/image-bed@master/2020/08/29/82e6321b289919805a28fa3486224e58.png)

--------------------

# 控制器
## 控制器设计基本方法
+ 每个状态一个触发器（one-hot，热位）
+ 序列寄存器―译码器法
+ 可编程逻辑阵列PLA控制法（选择器法）
+ 微程序控制法
## 算法流程图
+ **状态框**
![](https://cdn.jsdelivr.net/gh/Fazziekey/image-bed@master/2020/08/29/eee27af82e50fb299080b111f89d4d7b.png)
+ **判断框**
![](https://cdn.jsdelivr.net/gh/Fazziekey/image-bed@master/2020/08/29/c7a6bb0427add204d4253c4b9a2c1f58.png)
+ **条件框**
![](https://cdn.jsdelivr.net/gh/Fazziekey/image-bed@master/2020/08/29/08bc38c8212f168a1266030338b81dcd.png)
## 控制器类型
+ 计数器型
+ 数据选择器型

## 微程序控制器
![](https://cdn.jsdelivr.net/gh/Fazziekey/image-bed@master/2020/08/29/daec2de369c6936908f33be54d12d24b.png)

## 微命令
+ 微指令除给出微命令信息外，还给出测试判别信息
+ 微指令中还包含一个下址字段，该字段将指明存储器中下一条
微指令的地址
+ 微程序是由若干条微码指令组成的序列
![](https://cdn.jsdelivr.net/gh/Fazziekey/image-bed@master/2020/08/30/6cfc36e268cdcbbf284885f237e7c1d7.png)
![](https://cdn.jsdelivr.net/gh/Fazziekey/image-bed@master/2020/08/30/8c8bb5ea2d07bfc7bddae58a31ded079.png)


# TTL电路
### 三极管非门
![](https://cdn.jsdelivr.net/gh/Fazziekey/image-bed@master/2020/08/29/3c8b93eb14b3ab1a8a13403474e3c5a0.png)
### TTL反相器
![](https://cdn.jsdelivr.net/gh/Fazziekey/image-bed@master/2020/08/29/67c76ff25dcdfbaea40046d47385b762.png)

# CMOS
### 传输门
![](https://cdn.jsdelivr.net/gh/Fazziekey/image-bed@master/2020/08/29/cfc93ba8869ea0cb0ffe74cfb041d9cb.png)

### 三态门
![](https://cdn.jsdelivr.net/gh/Fazziekey/image-bed@master/2020/08/29/dfd338364f5507d127901f4c98c6e7f7.png)

> CMOS1和TTL电路最大区别，TTL电路输入端接大电阻变为高电平输入

# 脉冲电路
## 施密特电路
![](https://cdn.jsdelivr.net/gh/Fazziekey/image-bed@master/2020/08/29/b9eceacb663c025f80018e935ce1f091.png)
+ 正向阈值电压
$$
v_i=(1+\frac{R_1}{R_2})v_{TH}
$$
+ 负向阈值电压
$$
v_i=(1-\frac{R_1}{R_2})v_{TH}
$$
+ 特点：滞后特性

### 作用：
+ 波形变换（整形），抗干扰能力强
+ 用于脉冲鉴幅

## 单稳态电路
### 微分电路
$$
t_w=In2RC=0.69RC
$$
### 积分电路
$$
t_w=In2(R+R_o)C
$$

## 多谐振荡器
### 对称式
$$
T=2R_ECIn\frac{V_E-V_{IK}}{V_E-V_{TH}}
$$
### 非对称
$$
T=2R_FCIn3
$$

### 环形震荡器
$$
T=2nt_{pd}
$$

## 集电极开路门电路（OC门）
![](https://cdn.jsdelivr.net/gh/Fazziekey/image-bed@master/2020/08/29/0e1513e0c121639db13e6c9f646d925d.png)
## 555定时器
![](https://cdn.jsdelivr.net/gh/Fazziekey/image-bed@master/2020/08/29/4e8155002d47fcee20b42b092cb84baf.png)
### 555做施密特触发器
![](https://cdn.jsdelivr.net/gh/Fazziekey/image-bed@master/2020/08/29/7c554d55db34728ef6927b95ee8b7261.png)
### 555做单稳态
![](https://cdn.jsdelivr.net/gh/Fazziekey/image-bed@master/2020/08/29/88368cda5707cf762cf0ffc5c255162b.png)
$$
T=1.1RC
$$

### 555做多谐振荡
![](https://cdn.jsdelivr.net/gh/Fazziekey/image-bed@master/2020/08/29/dcd9a43ac32ea76bda7fd73474811fb9.png)
$$
T=(R_1+2R_2)CIn2
$$

# 测试
## SA1&SA0
![](https://cdn.jsdelivr.net/gh/Fazziekey/image-bed@master/2020/08/30/9c23bda387263fbcd582641ee9b82d49.png)

## 路径敏化

![](https://cdn.jsdelivr.net/gh/Fazziekey/image-bed@master/2020/08/30/7eb382150ceac2caaea24b6392ace302.png)

只考虑单个输入变化，其他输入固定，让门退化，与门输入1，或门输入0

$$
w_2=1
$$
$$
w_3=0
$$
$$
w_4=1
$$
可以测试

$$
w_1=1
$$
$$
a/0
$$
$$
b/0
$$
$$
c/1
$$

-------------
$$
w_1=0
$$
$$
a/1
$$
$$
b/1
$$
$$
c/0
$$
> 路径敏化可以一组输入测试多个故障

## 树型结构
![](https://cdn.jsdelivr.net/gh/Fazziekey/image-bed@master/2020/08/30/680ed85a1bc29dd541011938feb141f6.png)

## 时序电路测试
### 扫描测试
加入多路选择器把内部状态逐级传递出来

在测试时钟的控制下通过扫描输入（ScanIn）引线输入逻辑模块 A（和/或 B）的
激励向量并将其移入寄存器。
激励被加到逻辑模块的输入并传播到它的输出。通过产生一个系统时钟事件把它
的结果锁存到寄存器中。
寄存器中的结果通过扫描输出（ScanOut）引线送出电路并与期望的数据进行比较。
此时一个新的激励向量可以被同时输入。

![](https://cdn.jsdelivr.net/gh/Fazziekey/image-bed@master/2020/08/30/9992c841a2c31e9a0d895c124c6a6867.png)
### 内建自测试
![](https://cdn.jsdelivr.net/gh/Fazziekey/image-bed@master/2020/08/30/571abc9b7f9a7324d0486c51796b5646.png)
![](https://cdn.jsdelivr.net/gh/Fazziekey/image-bed@master/2020/08/30/6af28ea46e9b62eeea5c9d84a18a12c4.png)
### 专门测试
![](https://cdn.jsdelivr.net/gh/Fazziekey/image-bed@master/2020/08/30/834946b7da49c32910baf7db6d41afab.png)

# 微处理器

## 什么是微处理器？
• 微处理器由一片或少数几片大规模集成电路组成的中央处理器。

• 这些电路执行控制部件和算术逻辑部件的功能。

• 微处理器能完成取指令、执行指令，以及与外界存储器和逻辑部件交换信息等操作，
是微型计算机的运算控制部分。

## 微处理器的主要结构
### 冯诺依曼结构

• 将程序存储和数据存储放在同一物理存储空间

• 相同的总线

• 硬件简单

**组成**

+ 输入 INPUT
+ 输出 OUTPUT
+ 存储器 MEMORY
+ 微处理器 CPU

### 哈佛结构
• 将程序存储和数据存储分别放在不同的物理存储空间

• 不同的总线

• 灵活、速度快

## 微处理器内部结构
### 控制单元
+ 用于控制数据通路的所有操作，实现微处理器运算的正确性
### 数据通路
+ 主要包括运算单元ALU、存储单元（寄存器）及其相互连接

## 指令集
专门执行一些指令集的微处理器
• 利用指令集编写不同的程序完成不同的处理任务
## 微处理器三个执行步骤
+ 取指
+ 译指
+ 执行指令

## 微处理器指令集 ISA
+ 指令（Instruction） 
    + 计算机语言里的单词
+ 指令集（Instruction Set Architecture） 
    + 计算机的词汇
+ 指令需指明要执行的操作和要使用的操作数
+ 机器语言（Machine Language）
    + 指令编码为二进制数格式
+ 汇编语言（Assembly Language）
    + 符号格式表示各种指令
+ 基本指令
  + 加、减和跳转指令

## 操作数
+ 常数（Constants）和变量
+ 寄存器（register）
    + 寄存器组（register set） + 寄存器文件（register file） 
+  寄存器操作
$$
\$ S_0=a,\$ S_1=b,\$ S_2=c

add \$S_0.\$S_1.\$S_2
$$


+ MIPS寄存器名称由$符号开头
+ 变量a、b和c放置在$S0、$S1和$S2
+ 该指令将存在$S1(b)和$S2(C)的32位值相加，32位结果写入$S0(a)

## 立即数
+ 立即数操作
$$
addi 
\$S_0.\$S_0.4
$$
$$
\# a=a+4
$$
+ 立即数是一个16位二进制补码数据
+ 范围是[-32768，32767]


## MIPS指令格式
### R型------三个寄存器操作数格式
• 用于如add和sub指令，有三个寄存器操作数

+ R-type Instructions
    + R型是寄存器类型（register-type）的缩写
    + 32位指令

op | rs |rt |rd |shamt |funct
---|---|---|---|---|---|---
6bits | 5bits|5bits|5bits|5bits|6bits



+ 六个数字域
    + op，（也称为opcode或操作码），R型指令的opcode为6‘b000000
    + rs，rt，源寄存器
    + rd，目标寄存器
    + shamt，只用于移位操作，其它R型指令，shamt为5’b00000
    + funct，（也称为功能码），确定特定的R型操作
+ 每个字段为5比特或6比特


### I型--------两个寄存器操作数格式
• 用于如lw和sw指令，具有两个寄存器操作数和一个16位立即数

+ I型是立即数类型（immediate-type）的缩写

op | rs |rt |imm|
---|---|---|---|
6bits | 5bits|5bits|16bits

+ 四个字段
    + op，操作码
    + rs，源操作数
    + rt，如addi和lw用作目标操作数，sw作为另一种源操作数
    + imm，源操作立即数 
    + rs和imm始终用作源操作数
    

### J型-------无寄存器格式
• 有一个26位的立即数，无寄存器

J型是跳转型（jump-type）的缩写

• 此格式只用跳转指令使用。

• 用26位的地址操作数，addr

• 用于指定一个地址

op | addr
---|---
6bits | 26bits




