---
title: 离散时间信号频域分析
toc: true
copyright: true
date: 2020-08-20 21:58:19
tags:
    - 手撕拉普拉斯
categories:
    - 《行于黑暗，侍奉光明，我们是电工》
reward:
---
# 离散时间傅里叶级数
$$
x[n]=\sum_{k=<N>}a_ke^{jkw_0n}=\sum_{k=<N>}a_ke^{jk\frac{2\pi}{T_0}n}
$$
$$
a_k=\frac{1}{N}\sum_{n=<N>}x[n]e^{-jkw_0n}
$$

<!--more-->

> 离散时间傅里叶级数不存在着收敛问题和吉布斯现象

# 离散傅里叶变换
$$
X(e^{jw})=\sum_{n=-\infty}^\infty x[n]e^{-jwn}
$$
$$
x[n]=\frac{1}{2\pi}\int_{2\pi}X(e^{jw})e^{jwn}dw
$$
$$
X(e^{jw})=|X(e^{jw})|e^{j\theta(w)}
$$

## 离散时间傅里叶变换的收敛性与吉布斯现象
x[n]要求绝对可和并能量有限

$$
\sum_{n=-\infty}^\infty |x[n]|<\infty
$$
$$
\sum_{n=-\infty}^\infty |x[n]|^2<\infty
$$

## 常见函数离散傅里叶变换
### 单位脉冲
$$
\delta[n]\to 1
$$
### 单边指数
$$
x[n]=a^nu[n] \to\frac{1}{1-ae^{-jw}}
$$
### 双边指数
$$
x[n]=a^{|n|} \to\frac{1-a^2}{1-2a\cos w+a^2}
$$
### 矩形脉冲

$$
x[n]=
\begin{cases}
1&|n|<N_1\\
0&|n|>N_1
\end{cases}
$$
$$
X(e^{jw})=\frac{\sin[(2N_1+1)w/2]}{\sin(w/2)}
$$

### 冲激串
$$
1 \to 2\pi\sum_{k=-\infty}^{\infty}\delta(w-2\pi k)
$$

# 离散周期信号傅里叶变换
$$
X(e^{jw})=2\pi\sum_{k=-\infty}^{\infty}a_k\delta(w-2\pi k/N)
$$

# 离散傅里叶变换性质

### 周期性
### 线性性质

### 时移性质
$$
x[n-n_0]\to e^{-jwn_0}X(e^{jw})
$$

### 频移性质
$$
X(e^{j(w-w_0)})\to x(t)e^{jw_0n}
$$
### 共轭
$$
x^*(t)\to X^*(e^{-jw})
$$
+ x(t)为实值函数，X(jw)实部是偶函数，虚部是奇函数，幅度是偶函数，相位是奇函数
+ x(t)为实值偶函数，则X(jw)也是实值偶函数
+ x(t)为实值奇函数，则X(jw)也是纯虚奇函数
+ 该性质也适用于傅里叶级数情况，

### 差分求和
$$
x[n]-x[n-1]\to (1-e^{-jw})X(jw)
$$
$$
\sum_{m=-\infty}^nx[m] \to \frac{1}{(1-e^{-jw})}X(e^{jw})\pi X(e^{j0})\sum_{m=-\infty}^\infty \delta(w-2\pi k)
$$

### 时域扩展
$$
x_(k)=
\begin{cases}
x[n/k]&n为k整数倍\\
0
\end{cases}
$$
$$
x(k)[n]\to X(e^{jkw})
$$

### 频域微分
$$
j\frac{dX(e^{jw})}{dw}\to nx[n]
$$
### 卷积性质
$$
x[n]*h[n] \to X(e^{jw})H(e^{jw})
$$
#### 周期卷积
$$
\sum_{r=<N>}x[r]h[n-r] \to Na_kb_k
$$
### 调制性质
$$
x[n]y[n] \to \frac{1}{2\pi}X(e^{jw})*Y(e^{jw})
$$

当傅里叶级数存在时
$$
x[n]y[n] \to a_k*b_k
$$


### 帕斯瓦尔定理
$$
\sum_{k=-\infty}^\infty |x(t)|^2dt=\frac{1}{2\pi}\int_{2\pi}|X(e^{jw})|^2dw
$$

# 离散傅里叶变换的对偶性
离散时间傅里叶变换和连续时间傅里叶
级数在数学形式上也是十分相似的，它们之间
也存在着一种对偶关系。

$$
x[n] \to a[k]
$$
$$
a[n] \to \frac{1}{N}x[-k]
$$

# 离散时间LTI系统频率响应
离散LTI系统的频率响应另一种定义可表示为
$$
H(e^{jw})=\frac{Y(e^{jw})}{X(e^{jw})}
$$