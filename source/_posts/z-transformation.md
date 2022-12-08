---
title: z变换
toc: true
copyright: true
date: 2020-08-21 16:01:57
tags:
- 手撕拉普拉斯
categories:
- 《行于黑暗，侍奉光明，我们是电工》
reward:
---
## 意义
**傅里叶变换的推广**

**针对离散信号**
<!--more-->
## 双边z变换
选择合适的指数信号$r^{-n}$,使得，可以进行傅里叶变换

假设r使X(z)收敛
$$
x[n]r^{-n}=F^{-1}\{X(re^{iw})\}
$$
$$
x[n]=r^{n}F^{-1}\{X(re^{iw})\}
$$
$$
x[n]=\frac{1}{2\pi}\int_{2\pi} X(re^{iw})(re^{jw})^ndw
$$
$$
令z=re^{jw}
$$
$$
\to
x[n]=\frac{1}{2\pi j}\oint_{2\pi} X(z)z^{n-1}dz
$$
$$
X(z)=\sum_{n=-\infty}^{\infty}x[n]z^{-n}
$$
> $\oint$围线积分，以原点为中心，逆时针的线积分

==z变换需要明确收敛域==

### 常见离散信号z变换
+ 单边指数信号
$$
x[n]=u[n]a^n
$$
$$
X(z)=\frac{z}{z-a} 
(|z|>|a|)
$$
$$
x[n]=-u[-n-1]a^n
$$
$$
X(z)=\frac{z}{z-a} 
(|z|<|a|)
$$
+ 双边信号
$$
x[n]=b^{|n|}
$$
$$
X(z)=\frac{1}{1-bz^{-1}}-\frac{1}{1-b^{-1}z^{-1}} 
(|b|<|z|<|1/b|)
$$
> 只有b<1时收敛

> 当左边信号线性叠加右边信号，就会形成圆环，总共有三种情况
+ 幂指数信号
$$
x[n]=nu[n]a^n
$$
$$
X(z)=\frac{az}{(z-a)^2} 
(|z|>|a|)
$$
+ 三角信号
$$
x[n]=cos[w_0n]u[n]
$$
$$
X(z)=\frac{1-z^{-1}[cosw_0]}{1-2z^{-1}[cosw_0]+z^{-2}}
(|z|>1)
$$
$$
x[n]=sin[w_0n]u[n]
$$
$$
X(z)=\frac{1-z^{-1}[sinw_0]}{1-2z^{-1}[cosw_0]+z^{-2}}
(|z|>1)
$$
$$
x[n]=r^ncos[w_0n]u[n]
$$
$$
X(z)=\frac{1-z^{-1}[rcosw_0]}{1-2z^{-1}[2rcosw_0]+r^2z^{-2}}
(|z|>1)
$$
$$
x[n]=rsin[w_0n]u[n]
$$
$$
X(z)=\frac{1-z^{-1}[rsinw_0]}{1-2z^{-1}[2rcosw_0]+r^2z^{-2}}
(|z|>1)
$$

+ 单位冲击
$$
x[n]=\delta[n]
$$
$$
X(z)=1(0=<|z|<\infty)
$$
+ 单位阶跃
$$
x[n]=u[n]
$$
$$
X(z)=\frac{z}{z-1}(|z|>1)
$$
$$
x[n]=-u[-n-1]
$$
$$
X(z)=\frac{z}{z-1}(|z|<1)
$$
## z变换的收敛域
信号绝对可和
$$
\sum_{n=-\infty}^{+\infty}|x[n]|r^{-n}<\infty
$$

>  z变换的收敛域都是以原点为圆心的环状

### 有限长序列

$$
\sum_{n=n_1}^{n_2}|x[n]|r^{-n}<\infty
$$
一定收敛，收敛域为$z=0,z=\infty$,外的整个z平面
+ $n_1>0,0<|z|<=\infty$
+  $n_2<0,0=<|z|<\infty$
+  $n_1>0,n_2<0,0<|z|<\infty$


### 右边序列
当 n< n1,x[n]=0

收敛域为
$$
R_{x^-}<z<\infty
$$
### 左边序列
当 n> n2,x[n]=0

收敛域为
$$
0<z<R_{x^+}
$$
### 双边序列
当 n< n1,n>n2,x[n]=0

收敛域为
$$
R_{x^-}<z<R_{x^+}
$$

## z变换的几何表示
$$
X(z)=\frac{N(z)}{D(z)}
$$
零极点

## z变换的性质
+ 线性性质
   + 收敛域至少为交集，可能出现0极点抵消，收敛域扩大
$$
x[n]=u[n]a^n，
y[n]=u[n-1]a^n
$$
$$
X(z)=\frac{z}{z-a} 
(|z|>|a|)
$$
$$
Y(z)=\frac{a}{z-a} 
(|z|>|a|)
$$
$$
X(z)-Y(z)=1 (0=<|z|<\infty)
$$
+ 时域位移
$$
x[n-m]\underrightarrow{z}z^{-m}X(z)
$$
> 应用：延时器

+ 频域微分
$$
nx[n]\underrightarrow{z}-z\frac{d}{dz}X(z)
$$
+ 尺度变换
$$
a^nx[n]\underrightarrow{z}X(\frac{z}{a})
$$
+ 时域扩展
$$
x[n]_k=
\begin{cases}
x[n/k], n是k的整数倍\\0，, n不是k的整数倍
\end{cases}
$$
$$sa
x[n]_k\underrightarrow{z}X(z^k)（R_{k^-}^{1/k}<|z|<R_{k^+}^{1/k}）
$$
特殊情况，k=-1
$$
（R_{k^-}<|1/z|<R_{k^+}）
$$
+ 时域卷积
$$
x[n]*y[n]\underrightarrow{z}X(z)Y(z)
$$
$$
（max\{R_{x^-},R_{y^-}\}<|z|<min\{R_{x^+},R_{y^+}\}）
$$

+ 共轭性质
$$
x^*[n]\underrightarrow{Z}X^*(z^*)
$$
+ 累加性质
$$
\sum_{k=-\infty}^nx[k]\underrightarrow{Z}\frac{1}{1-z^{-1}}X(z)
$$
+ 初值性质
$$
x[0]=lim_{z\rightarrow\infty}X(z)
$$
> x[n]为因果序列,|z|>Rx-

+ 终值性质
$$
x[0]=lim_{z\rightarrow1}(z-1)X(z)
$$
> x[n]为因果序列,|z|>=1,(z-1)X(Z)收敛

## Z反变换
### 幂级数展开法
$$
X(z)=x(0)z^0+x(1)z^{-1}+x(2)z^{-2}+……+x(n)z^{-n}
$$
### 利用泰勒级数
### 部分分式展开
### 留数法
+ |z|>a
$$
x[n]=\begin{cases}
0,n<n_0\\
\sum_m Res[X(z)z^{n-1}]_{z=p_m},n>=n_0
\end{cases}
$$
+ |z|<a
$$
x[n]=\begin{cases}
-\sum_m Res[X(z)z^{n-1}]_{z=p_m},n<n_0\\
0,n>=n_0\\
\end{cases}
$$
其中
$$
Res[X(z)z^{n-1}]_{z=p_m}=\frac{1}{(L-1)!}[\frac{d^{L-1}}{dz^{L-1}}(z-p_m)^LX(z)z^{n-1}]_{z=p_m}
$$

##  单边z变换
+ 移位性质
$$
x[n+m]u[n]\underrightarrow{UZ}z^m（X(z)-\sum_{k=0}^{m-1}x[k]z^{-k})
$$

## 系统分析
+ 因果性

一个因果 LTI系统其单位脉冲响应h[n]是对于n<0, h[n]=0，ROC包括无限远点
+ 稳定性

一个稳定离散时间LTI系要求其单位脉冲响应h[n]
满足绝对可和的，ROC必须包含单位圆，一个LTI系统当且仅当它的系统函数H(z)的ROC
包括单位圆，|z|=1时，该系统就是稳定的。
+ 因果稳定离散时间LTI系统

一个具有有理系统函数的因果LTI系统，当且仅
当H(z)的全部极点都位于单位圆内时，也即全部极点
其模均小于1时，系统就是稳定的。
