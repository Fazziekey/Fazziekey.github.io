---
title: 矩阵微分
toc: true
copyright: true
date: 2020-11-16 23:02:28
tags:
- 矩阵论
categories:
- 《柯西的传世绝学》
reward:
---
# 雅可比矩阵和矩阵微分
## 实值函数分类
![](https://cdn.jsdelivr.net/gh/Fazziekey/image-bed@master/2020/11/16/a8eb220fbe1dcb1de74a1ede789e8738.png)
## 雅可比矩阵
在向量分析中，雅可比矩阵是函数以一阶偏导数以一定方式排列成的矩阵，其行列式称为雅可比行列式
<!--more-->
+ $1\times m$行向量偏导算子定义为
$$
D_x\overset{def}{=}\frac{\partial}{\partial x^T}=[\frac{\partial}{\partial x_1}...\frac{\partial}{\partial x_m}]
$$
所以实值标量函数f（x）在x的偏导向量由$1\times m$行向量给出

$$
D_x f(x)=\frac{\partial f(x)}{\partial x^T}
$$
$$
=[\frac{ \partial f(x)}{\partial x_1},...,\frac{\partial f(x)}{\partial x_m}]
$$
当实值标量函数f（X）的变元为实值矩阵$X\in R^{m\times n}$，可能存在两种定义
+ Jacobian偏导
$$
D_xf(x)\overset{def}{=}\frac{\partial f(X)}{\partial X^T}
=\begin{bmatrix}
\frac{\partial f(X)}{\partial x_{11}}&...&\frac{\partial f(X)}{\partial x_{m1}}\\
...&...&...\\
\frac{\partial f(X)}{\partial x_{1n}}&...&\frac{ \partial f(X)}{\partial x_{mn}}
\end{bmatrix}
$$
+ 行向量偏导
$$
D_{vecX}f(X)=\frac{\partial f(X)}{\partial_{vec^T(X) }}=[\frac{\partial f(X)}{\partial x_{11}}...\frac{\partial f(X)}{\partial x_{m1}}...\frac{\partial f(X)}{\partial x_{1n}}...\frac{\partial f(X)}{\partial x_{mn}}]
$$
+ 两者关系
$$
D_{vec}f(X)=rvec(D_Xf(X))=(vec(D_X^Tf(X)))^T
$$
即实值标量函数f(X)的行向量偏导$Dvec_Xf(X)$等于Jacobian矩阵的转置$D_X^Tf(X)$的列向量化

### 矩阵函数雅克比矩阵
函数为矩阵，变元为矩阵
$$
D_XF(X)=\frac{\partial f(X)}{\partial X^T}
=\begin{bmatrix}
\frac{\partial f(X)}{\partial X^T}&...&\frac{\partial f(X)}{\partial X^T}\\
...&...&...\\
\frac{\partial f(X)}{\partial X^T}&...&\frac{ \partial f(X)}{\partial X^T}
\end{bmatrix}
$$
$$
=
\begin{bmatrix}
\frac{\partial f_{11}}{\partial x_{11}}&...&\frac{\partial f_{11}}{\partial x_{m1}}&...&\frac{\partial f_{11}}{\partial x_{1n}}&...&\frac{\partial f_{11}}{\partial x_{m1}}\\
...&...&...&...&...&...\\
\frac{\partial f_{p1}}{\partial x_{11}}&...&\frac{\partial f_{p1}}{\partial x_{m1}}&...&\frac{\partial f_{p1}}{\partial x_{1n}}&...&\frac{\partial f_{p1}}{\partial x_{m1}}\\
...&...&...&...&...&...\\
\frac{\partial f_{1q}}{\partial x_{11}}&...&\frac{\partial f_{1q}}{\partial x_{m1}}&...&\frac{\partial f_{1q}}{\partial x_{1n}}&...&\frac{\partial f_{1q}}{\partial x_{m1}}\\
...&...&...&...&...&...\\
\frac{\partial f_{pq}}{\partial x_{11}}&...&\frac{\partial f_{pq}}{\partial x_{m1}}&...&\frac{\partial f_{pq}}{\partial x_{1n}}&...&\frac{\partial f_{pq}}{\partial x_{m1}}\\
\end{bmatrix}
$$

## 梯度矩阵
采用列向量作为偏导算子称为偏导算子

$$
\nabla_x \overset{def}{=}
[\frac{ \partial }{\partial x_1},...,\frac{\partial }{\partial x_m}]^T
=\frac{\partial}{\partial x}
$$
+ 标量函数的梯度向量
$$
\nabla_xf(x)=[\frac{ \partial f(x) }{\partial x_1},...,\frac{\partial f(x) }{\partial x_m}]^T
$$

+ 矩阵梯度向量
$$
\nabla_{vecX}f(X)=\frac{\partial f(X)}{\partial_{ve  cX }}=[\frac{\partial f(X)}{\partial x_{11}}...\frac{\partial f(X)}{\partial x_{m1}}...\frac{\partial f(X)}{\partial x_{1n}}...\frac{\partial f(X)}{\partial x_{mn}}]^T
$$
+ 梯度矩阵
$$
\nabla_xf(x)=\frac{\partial f(X)}{\partial X^T}
=\begin{bmatrix}
\frac{\partial f(X)}{\partial x_{11}}&...&\frac{\partial f(X)}{\partial x_{1n}}\\
...&...&...\\
\frac{\partial f(X)}{\partial x_{m1}}&...&\frac{ \partial f(X)}{\partial x_{mn}}
\end{bmatrix}
$$

> 实标量函数和矩阵函数的梯度矩阵是雅克比矩阵的转置

# 偏导和梯度计算
+ 若$F(X)=c$为常数，其中X为$m\times n$矩阵，则梯度$\frac{\partial c}{\partial X}=O_{m\times n}$
+ 线性法则
+ 乘积法则
+ 商法则
+ 链式法则

## 独立性基本假设
假定实值函数的向量变元和矩阵变元无任何特殊结构则

$$
\frac{\partial x_i}{\partial x_j}=
\begin{cases}
1&i=j\\
0&other
\end{cases}
$$
$$
\frac{\partial x_{kl}}{\partial x_{ij}}=
\begin{cases}
1&k=i,l=j\\
0&other
\end{cases}
$$
## example
求实值函数$f(x)=x^TAx$的Jacobian矩阵，$x^TAx=\sum_{k=1}^n\sum_{l=1}^na_{kl}x_kx_l$，我们可以求出行偏导向量$\frac{\partial x^TAx}{\partial x^T}$的第i个分量为

$$
\frac{\partial x^TAx}{\partial x^T}=\frac{\partial}{\partial x_i}\sum_{k=1}^n\sum_{l=1}^na_{kl}x_kx_l=\sum_{k=1}^nx_ka_{ki}+\sum_{l=1}^nx_la_{il}
$$
我可以得到行偏导向量和梯度向量
$$
Df(x)=x^TA+x^TA^T=x^T(A+A^T)
$$
$$
\nabla_Xf(x)=(A^T+A)x
$$


# 一阶实矩阵微分
+ 标量函数tr(U)的微分
$$
d[tr(U)]=d(\sum_{i=1}^nu_{ii})=\sum_{i=1}^ndu_{ii}=tr(dU)
$$
+ 矩阵乘积UV的微分矩阵
$$
d(UV)=(dU)V+U(dV)
$$
+ 矩阵的迹的矩阵微分等于矩阵微分的迹
$$
d(tr(X))=tr(dX)
$$

## 标量函数f（x）的jacobian矩阵辨识
+ 以向量为变元的标量函数f(x)的微分
$$
df(x)=\frac{\partial f(x)}{\partial x_1}dx_1+...+\frac{\partial f(x)}{\partial x_m}dx_m
$$
$$
=\frac{\partial f(x)}{\partial x^T}dx=(dx)^T\frac{\partial f(x)}{\partial x}
$$
如果令
$$
A=\frac{\partial f(x)}{\partial x^T}
$$
我们可以把一阶微分写成迹的形式
$$
df(x)=tr(Adx)
$$
$$
D_ xf(x)=\frac{\partial f(x)}{\partial x^T}=A
$$

## 标量函数f（X）的jacobian矩阵辨识
$$
df(X)=(vec(A^T))^Td(vecX)
$$
A为标量函数f（X）的Jacobin矩阵

$$
df(x)=tr(Adx)\to D_xf(x)=\frac{\partial f(x)}{\partial x^T}=A
$$

$$
df(X)=tr(AdX)\to D_Xf(X)=\frac{\partial f(X)}{\partial X^T}=A
$$
$$
D_Xf(X)=\frac{\partial f(X)}{\partial X^T}=A\to \nabla_Xf(X)=A^T
$$

# Hessian 矩阵
$$
H[f(x)]=\frac{\partial ^2f(x)}{\partial x\partial x^T}
$$
$$
=\begin{bmatrix}
\frac{\partial^2f}{\partial x_1\partial x_1}&...&\frac{\partial f^2}{\partial x_1\partial x_m}\\
...&...&...\\
\frac{\partial ^2f}{\partial x_m\partial x_1}&...&\frac{\partial ^2f}{\partial x_m\partial x_m}
\end{bmatrix}\in R^{m\times m}
$$
$$
H[f(x)]=\nabla^2_xf(x)=\nabla_x(D_xf(x))
$$
$$
[Hf(x)]_{i,j}=[\frac{\partial^2f(x)}{\partial x\partial x^T}]=\frac{\partial}{\partial x_i}[\frac{\partial f(x)}{\partial x_j}]
$$

# 共轭梯度和复Hessian矩阵

## 形式偏导
$$
\frac{\partial }{\partial z}=\frac{1}{2}
> (\frac{\partial}{\partial x}-j\frac{\partial}{\partial y})
$$
## 实部和虚部相互独立

## 单个复变量梯度
$$
\nabla_zf(z,z^*)=\frac{\partial f(z,z^*)}{\partial }|_{z^*=C}
$$
## 单个复变量微分
$$
df(z,z^*)=\frac{\partial f(z,z^*}{\partial z}dz+\frac{\partial f(z,z^*)}{\partial z^*}dz^*
$$
## 复变元向量违法
$$
df(z,z^*)=\frac{\partial f(z,z^*)}{\partial  z^T}dz+\frac{\partial(z,z^*)}{\partial z^H}dz^*
$$

## 标量函数的梯度向量和共轭梯度向量
$$
\nabla_z f(z,z^*)=(D_zf(z,z^*))^T
$$

## 常见矩阵偏导
$$
\frac{\partial a^Tx}{\partial x}=a
$$
$$
\frac{\partial x^Ta}{\partial x}=a
$$
$$
\frac{\partial x^TAx}{\partial x}=(A+A^T)x
$$
$$
\frac{\partial x^TAx}{\partial x^T}=x^T(A+A^T)
$$
$$
\frac{\partial x^TA}{\partial x}=A
$$
$$
\frac{\partial (a-Ax)^TB(a-Ax)}{\partial x}=-2A^TB(a-Ax)
$$