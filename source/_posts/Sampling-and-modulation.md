---
title: 采样和调制
toc: true
copyright: true
date: 2020-08-21 15:57:08
tags:
     - 手撕拉普拉斯
categories:
     - 《行于黑暗，侍奉光明，我们是电工》
reward:
mathjax: true
---
# 连续时间采样定理
## 冲激串采样定理
$$
x_p(t)=x(t)p(t)
$$

$$
p(t)=\sum_{n=-\infty}^\infty\delta(t-nT)
$$
T为采样周期

<!--more-->

$$
X_p(jw)=\frac{1}{2\pi}X(jw)*P(jw)
$$
$$
=\frac{1}{T}\sum_{k=-\infty}^\infty X(j(w-kw_s))
$$
相当于将信号频域的图像左右平移
![](https://cdn.jsdelivr.net/gh/Fazziekey/image-bed@master/2020/08/21/cd375deb4debf84d4eec89018faaf266.png)

## 采样定理
+ $x(t)$是一带限信号，$X(jw)=0,|w|>w_M$
+ 采样频率$w_s>2w_M$,其中$w_s=2\pi/T$,T为抽样周期，当$w_s=2w_M$,称作奈奎斯特率。满足条件的信号可以采样后重建。


![](https://cdn.jsdelivr.net/gh/Fazziekey/image-bed@master/2020/08/21/99a6952d0e3d2da0ff8aaff1d2f26420.png)

+ H( jw)为一低通滤波器

$$
x_r(t)=\sum_{n=-\infty}^\infty x(nT)\delta(t-nT)*h(t)
$$
$$
=\sum_{n=-\infty}^\infty x(nT)h(t-nT)
$$

### 带限内插
+ 当h(t)为理想滤波器时，即

$$
h(t)=T\frac{w_c}{\pi}Sa(w_ct)
$$
当$w_c$满足：$w_M<w_c<w_s-w_M$时，重建是精确的。 

![](https://cdn.jsdelivr.net/gh/Fazziekey/image-bed@master/2020/08/21/c8aacd6ecdb8de1aeaf235fdaf867e99.png)


$$
x_r(t)=\sum_{n=-N}^N x(nT)T\frac{w_c}{\pi}Sa(w_c(t-nT))
$$

### 零阶保持
如果h(t)取矩形窗函数
![](https://cdn.jsdelivr.net/gh/Fazziekey/image-bed@master/2020/08/21/c92525f0e7e3da23eda6d3cefd8ca72b.png)

![](https://cdn.jsdelivr.net/gh/Fazziekey/image-bed@master/2020/08/21/e2a0babfc3c05b2aff3e432089c665b0.png)


### 零阶保持采样
冲激串抽样的数学模型在实际工程应用中是无法实
现的，其重要意义是在理论上建立采样定理。在实际工
程应用中，往往采用零阶保持的方法来获取采样信号。

![](https://cdn.jsdelivr.net/gh/Fazziekey/image-bed@master/2020/08/21/bb5d4862a3afe394d519b8f6c21149cd.png)

### 欠采样
被采用的信号若是正弦信号，在频谱混叠的情况下可以获得重建信号

# 离散时间信号的时域采样定理
## 脉冲串采样
$$
p[n]=\sum_{k=-\infty}^\infty \delta[n-kN]
$$
$$
x_p[n]=x[n]p[n]
$$
$$
=\sum_{k=-\infty}^\infty x[kN] \delta[n-kN]
$$

![](https://cdn.jsdelivr.net/gh/Fazziekey/image-bed@master/2020/08/21/04275e4d4edb28371ab3a55dad3c6998.png)

$$
P(e^{jw})=\frac{2\pi}{N}\sum_{k=-\infty}^\infty \delta(w-kw_s)
$$
$$
X_p(e^{jw})=\frac{1}{N}\sum_{k=0}^{N-1}X(e^{j(w-kw_s)})
$$
![](https://cdn.jsdelivr.net/gh/Fazziekey/image-bed@master/2020/08/21/a2786c4c28f8bf0599e8798e8df94a1d.png)

## 离散时间的采样定理
设x[n]是某一带限信号，即在$w_M<|w|<\pi$时,$X(e^{jw})=0$。如果采样频
率$w_s>2w_M$，那么x[n] 就唯一地由其样
本x[kN]， 所确定。

## 离散时间的抽取与内插
### 抽取和减采样
$$
x_s[n]=x[nN]=x_p[nN]
$$
![](https://cdn.jsdelivr.net/gh/Fazziekey/image-bed@master/2020/08/21/c68233b27e0550fd3ffb7954428ab64c.png)
$$
X_s(e^{jw})=X_p(e^{jw/N})
$$

$x_s[n]$的频谱将$X_p(e^{jw})$扩展了N 倍

### 内插和增采样
$$
x[n]=
\begin{cases}
x_s(n/N)\\
0
\end{cases}
$$
$$
X(e^{jw})=X_s(e^{jwN})
$$

# 连续时间系统的离散实现

![](https://cdn.jsdelivr.net/gh/Fazziekey/image-bed@master/2020/08/21/2734e97ea60f009c907ff61dd321c77a.png)

# 正弦载波调制
$$
y(t)=x(t)\cdot c(t)
$$
![](https://cdn.jsdelivr.net/gh/Fazziekey/image-bed@master/2020/08/21/4cf88c3169d4d98b334db888eedacadd.png)
正弦载波幅度调制的主要功能是实现频谱搬移功能。
DSB调制通常也称为抑制载波的正弦载波调制
$$
x_r=(y(t)\cos w_ct)*h(t)
$$
$$
=(x(t)\frac{\cos(2w_ct)+1}{2})*h(t)=\frac{1}{2}x(t)
$$


# 脉冲幅度调制
PAM是脉冲载波的幅度随调制信号变化的
一种调制方式：它是对调制信号的取样，即抽
取某一时间间隙内的调制信号的信息。脉冲调
制有两种基本形式：

+ 自然采样
+ 平顶采样（零阶保持采样）。