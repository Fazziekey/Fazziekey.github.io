---
title: 特殊矩阵
toc: true
copyright: true
date: 2020-11-15 15:42:25
tags:
    - 矩阵论
categories:
    - 《柯西的传世绝学》
reward:
---
# Hermitian矩阵
复共轭对称矩阵
<!--more-->
$$
R=R^H
$$
# 置换矩阵
一个正方矩阵称为置换矩阵(permutation matrix)，若它的每一行和每一列有一个且仅有一个非零元素1。

$$
\begin{array}{l}
P_{m\times n}^T=P_{n\times m}\\
P^TP=PP^T=I\\
P^T=P^{-1}
\end{array}
$$
> 置换矩阵是正交矩阵。

# 互换矩阵

$$
\boldsymbol{J}=\left[\begin{array}{ccc}
0 & & &1 \\
& & 1 \\
& \cdot \cdot & \\
1 & & & 0
\end{array}\right]
$$
+ 左乘：矩阵的行顺序反转
+ 右乘：矩阵的列顺序反转

# 正交矩阵和酉矩阵
+ U非奇异且，$U^H=U^{-1}$
+ $UU^H=U^HU=I$
+ U的行列向量组成标准正交组

## 酉不变性
+ <x,y>=<Ax,Ay>
+ ||Ax||^2 =||x||^2
$$
cos\theta=\frac{<Ax,Ay>}{||Ax||||Ay||}=\frac{<x,y>}{||x|| ||y||}
$$
# 三角矩阵
+ 上三角
+ 下三角

# 相似矩阵
S为非奇异矩阵
$$
B=S^{-1}AS
$$
+ 特征值相同
+ 特征向量存在线性变换关系

$$
det(B)=det(A)

tr(B)=tr(A)
$$
# Vandermonde矩阵


$$
\boldsymbol{A}=\left[\begin{array}{cccc}
1 & 1 & \cdots & 1 \\
x_{1} & x_{2} & \cdots & x_{n} \\
x_{1}^{2} & x_{2}^{2} & \cdots & x_{n}^{2} \\
\vdots & \vdots & \vdots & \vdots \\
x_{1}^{n-1} & x_{2}^{n-1} & \cdots & x_{n}^{n-1}
\end{array}\right] \quad \boldsymbol{A}=\left[\begin{array}{ccccc}
1 & x_{1} & x_{1}^{2} & \cdots & x_{1}^{n-1} \\
1 & x_{2} & x_{2}^{2} & \cdots & x_{2}^{n-1} \\
\vdots & \vdots & \vdots & \vdots & \vdots \\
1 & x_{n} & x_{n}^{2} & \cdots & x_{n}^{n-1}
\end{array}\right]
$$
# Fourier 矩阵
Fourier矩阵是一种特殊结构的Vandermonde

$$
\boldsymbol{F}=\left[\begin{array}{cccc}
1 & 1 & \cdots & 1 \\
1 & w & \cdots & w^{N-1} \\
\vdots & \vdots & \vdots & \vdots \\
1 & w^{N-1} & \cdots & w^{(N-1)(N-1)}
\end{array}\right],
$$

# Hadamard矩阵
所有元素取1，-1，且
$$
H_nH_n^T=H_n^TH_n=nI
$$
+ 矩阵维度只能是2的倍数

# Toeplitz矩阵
任意一条对角线元素取相同值
$$
A=
\begin{bmatrix}
a_0&a_{-1}&a_{-2}&...&a_{-n}\\
a_1&a_0&a_{-1}&...&a_{-n+1}\\
a_2&a_1&a_0&...&...\\
...&...&...&...&...\\
a_n&a_{n-1}&...&a_1&a_0
\end{bmatrix}
=[a_{i-j}]^n_{i,j=0}
$$
若元素满足复共轭关系
$$
a_{-i}=a_i^*
$$
则称为Hermitian Toeplitz 矩阵
# Hankle矩阵

$$
\boldsymbol{A}=\left[\begin{array}{ccccc}
a_{0} & a_{1} & a_{2} & \cdots & a_{n} \\
a_{1} & a_{2} & a_{3} & \cdots & a_{n+1} \\
a_{2} & a_{3} & a_{4} & \cdots & a_{n+2} \\
\vdots & \vdots & \vdots & \vdots & \vdots \\
a_{n} & a_{n+1} & a_{n+2} & \cdots & a_{2 n}
\end{array}\right]
$$
