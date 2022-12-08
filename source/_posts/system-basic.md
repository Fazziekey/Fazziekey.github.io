---
title: 系统的基本概念
toc: true
copyright: true
date: 2020-08-17 11:34:53
tags:
    - 手撕拉普拉斯
categories:
    - 《行于黑暗，侍奉光明，我们是电工》
reward:
---

# 信号的分类
+ 随机信号和确定信号
+ 连续和离散
+ 周期
+ 奇偶
    + 所有信号可以被分解为奇偶信号   
+ 功率和能量

<!--more-->

能量信号（能量有限信号）：
如果信号x(t)满足: 0<E <$\infin$,而P = 0。

功率信号（功率有限信号）:
如果信号x(t)满足：0 < P <$\infin$, 而E=$\infin$。

> 周期信号一般属于功率信号，属于能量信号的非周期信号也称为脉冲信号
> 
![](https://cdn.jsdelivr.net/gh/Fazziekey/image-bed@master/2020/08/17/74b0c8b8c1a8b64273a37443ae7599b6.png)

# 复指数信号与正弦信号
## 连续时间复指数信号
$$
x(t)=ce^{st}

s=\sigma+jw

T_0=\frac{2\pi}{|w_0|}
$$
## 正弦与复指数信号转换
$$
\cos wt=\frac{1}{2}(e^{jwt}+e^{-jwt})
$$
$$
\sin wt=\frac{1}{2j}(e^{jwt}-e^{-jwt})
$$
$$
A\cos(wt+\phi)=\frac{A}{2}e^{j\phi}e^{jwt}+\frac{A}{2}e^{-j\phi}e^{-jwt}=ARe\{e^{j(wt+\phi)}\}
$$
$$
A\sin(wt+\phi)=Aim\{e^{j(wt+\phi)}\}
$$

## 离散时间复指数信号
$$
x[n]=e^{jwn}=\cos wn+\sin wn
$$

当$\frac{2\pi}{w}$为有理数数时为周期信号

# 单位冲击和单位阶跃函数
## 离散脉冲阶跃
### 单位脉冲
$$
\delta[n]=
\begin{cases}
0& n \not= 0 \\
1& n=0
\end{cases}
$$
**采样特性**

$$
\delta[n]x[n]=x[0]\delta[n]
$$
$$
x[n]\delta[n-n_0]=x[n_0]\delta[n-n_0]
$$
### 单位阶跃
$$
u[n]=
\begin{cases}
0& n < 0 \\
1& n>=0
\end{cases}
$$

**单位脉冲和阶跃关系**

$$
\delta[n]=u[n]-u[n-1]
$$
$$
u[n]=\sum_{k=0}^{\infin}\delta[n-k]=\sum_{k=-\infin}^{n}\delta[k]
$$

### 矩形序列
$$
g_N[n]=
\begin{cases}
0& 0<n < N-1 \\
1& other
\end{cases}
$$
$$
=u[n]-u[n-N]
$$
### 单位斜坡
$$
r[n]=
\begin{cases}
n& n >= 0 \\
0& n<0
\end{cases}
$$
$$
=nu[n]
$$
### 单位脉冲串
$$
\delta_N[n]=\sum_{k=-\infin}^{\infin}\delta[n-kN]
$$

## 连续时间阶跃冲激
### 单位阶跃
$$
u(t)=
\begin{cases}
0& t < 0 \\
1& t>0
\end{cases}
$$
t=0处无定义
### 矩形脉冲
$$
g(t)=u(t)-u(t-t_0)
$$

### 符号函数sgn
$$
sgn(t)=
\begin{cases}
1& t > 0 \\
-1& t<0
\end{cases}
$$
$$
=u(t)-u(-t)
$$
$$
=2u(t)-1
$$

### 单位冲激信号

**狄拉克定义**
$$
\begin{cases}
\int_{-\infin}^{+\infin}\delta(t)dt=1\\
\delta(t)=0 & t=\not0
\end{cases}
$$
$$
\delta(t)=\frac{du(t)}{dt}
$$
$$
u(t)=\int_{-\infin}^{t}\delta(\tau)d\tau
$$
#### 基本性质
+ 抽样
$$
x(t)\delta(t)=x(0)\delta(t)
$$
$$
x(t)\delta(t-t_0)=x(0)\delta(t-t_0)
$$
+ 筛选
$$
\int_{-\infin}^{+\infin}x(t)\delta(t)=x(0)
$$
$$
\int_{-\infin}^{+\infin}x(t)\delta(t-t_0)=x(t_0)
$$
+ 偶函数

### 冲激偶信号
冲激函数的微分称为冲激偶信号

$$
\int_{-\infin}^{+\infin}\delta'(t)dt=0
$$
$$
\int_{-\infin}^{+\infin}\delta'(t)x(t)dt=-x'(0)
$$

### 单位冲激串
$$
\delta_T(t)=\sum_{n=-\infin}^{\infin}\delta(t-nT)
$$
### Sa
$$
Sa(t)=\frac{\sin t}{t}
$$
$$
\int_{-\infin}^{\infin}Sa(t)dt=\pi
$$

# 信号的运算和变换
## 运算
+ 相加
+ 相乘
+ 微分积分
$$
x(t)=u(t-1)-u(t-2)
$$
$$
\frac{dx(t)}{dt}=\delta(t-1)-\delta(t-2)
$$

> 对于任意函数可以用u(t)进行分段表示，然后利用积分的变换进行计算

## 自变量变换
+ 平移，正左负右
+ 反褶
+ 尺度变化
+ 抽取
$$
x_1=x[Nn]
$$
![](https://cdn.jsdelivr.net/gh/Fazziekey/image-bed@master/2020/08/17/9bd9b1dad2d3e0646bff6332d2e3862d.png)
> 信号间隔不变，抽取部分信号

+ 内插
> 在信号间插入0信号
$$
x_2[n]=
\begin{cases}
x[n/N]\\
0
\end{cases}
$$

![](https://cdn.jsdelivr.net/gh/Fazziekey/image-bed@master/2020/08/17/10d0da71152d6e8de478c5c36d2979d7.png)

# 系统基本性质
连续系统可以用微分方程表示

离散系统可以用差分方程表示

## 线性
满足,离散同理
$$
ax_1(t)+bx_2(t)\to ay_1(t)+by_2(t)
$$
### 常见线性
$$
y(t)=x(t)
$$
$$
y(t)=tx(t)
$$
$$
y(t)=dx(t)/dt
$$
$$
y[t]=x[n+1]-x[n]
$$

### 常见非线性
$$
y(t)=x^2(t)
$$
$$
y(t)=e^{x(t)}
$$
$$
y(t)=2x(t)+3
$$

### 判断方法
+ 直接利用定义
+ 与x括号内参数无关，x(t)需要为一次且x(t)外无常数项

## 时变，时不变
$$
x[n]\to y[n] 
$$
$$
x[n-n_0]\to y[n-n_0] 
$$
$$
x(t)\to y(t)
$$
$$
x(t-t_0)\to y(t-t_0)
$$

### 判断方法
+ 定义
+ t只在x括号内且为一次

$$
y=x(sin(t))
$$
$$
y_1(t)=x_1(sin(t))
$$
$$
x_2(t)=x_1(t-t_0)=x_1(sin(t-t_0))
$$
$$
y_2(t)=x_2(sin(t))=x_1(sin(sin(t)-t_0))
$$
$$
\not =
y_1(t-t_0)=x_1(sin(t-t_0))
$$

### 记忆和无记忆
输入仅取决于当前输出为无机盐

输入取决于其他时间为记忆
比如累加器，延迟单元

### 因果
系统输出不取决于未来

非因果系统如
$$
y(t)=x(t+2)
$$
在图像处理中就会有非因果系统

通常把0时刻开始的信号称为因果信号

$$
x(t)=0 ,t<0
$$

## 可逆
不可逆
$$
y(t)=x^2(t)
$$
可逆
$$
y[n]=\sum x[k]
$$
## 稳定
输入有界则输出有界

