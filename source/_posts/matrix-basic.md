---
title: '矩阵代数基础'
toc: true
copyright: true
date: 2020-11-15 14:09:01
tags:
    - 矩阵论
categories:
    - 《柯西的传世绝学》
reward:
---
# 典型物理模型
### 多个信号观测模型
$$
x(n)=As(n)+v(n)
$$
<!--more-->
# 书写规范
+ 大写字母下加两线：矩阵
+ 加一线：向量
+ 不加：变量

# 矩阵代数基本性质
$$
\begin{array}{l}
(A+B)^*=A^*+B^*
\\
(A+B)^T=A^T+B^T
\\
(A+B)^H=A^H+B^H
\\
(AB)^T=B^TA^T
\\
(AB)^H=B^HA^H
\\
(AB)^{-1}=B^{-1}A^{-1}
\\
(A^*)^{-1}=(A^{-1})^T
\\
(A^H)^{-1}=(A^{-1})^H
\end{array}
$$

对于任意矩阵A，矩阵$B=A^HA$都是Hermitndian

## 导数积分
$$
\frac{dA}{dt}=
\begin{bmatrix}
\frac{da_{11}}{dt}&...&\frac{da_{1n}}{dt}\\
...&...&...\\
\frac{da_{m1}}{dt}&...&\frac{da_{mn}}{dt}
\end{bmatrix}
$$
+ 指数矩阵函数
$$
exp(At)=I+At+\frac{A^2t^2}{2!}...\frac{A^nt^n}{n!}
$$
+ 指数矩阵导数
$$
\frac{de^{At}}{dt}=Ae^{At}
$$
+ 矩阵乘积的导数
$$
\frac{d}{dt}(AB)=\frac{dA}{dt}B+A\frac{dB}{dt}
$$
+ 对数函数
$$
In(I+A)=\sum_{n=1}^\infty\frac{(-1)^{n-1}}{n}A^n
$$
## 特殊矩阵
+ 幂等矩阵
$$
A^2=A
$$
+ 对合矩阵

$$
A^2=I
$$
+ 正交矩阵

$$
AA^T=I
$$

## 线性无关与奇异性
### 线性方程组
$$
c_1u_1+...c_nu_n=0
$$
+ 向量组线性无关：只有零解
+ 线性相关：有非零解
### 矩阵方程
$$
Ax=0
$$
+ 只有零解：A非奇异
+ 存在非零解：A是奇异的

## 复矩阵方程
$$
(A_r+jA_i)(x_r+jx_i)=b_r+jb_i

\begin{bmatrix}
A_r&-A_i&b_r\\
A_i&A_r&b_i
\end{bmatrix}
\to
\begin{bmatrix}
I_n&O_n&x_r\\
O_n&I_n&x_i
\end{bmatrix}
$$

## 向量空间和线性映射
向量空间是以向量为元素的集合

+ 子空间V到子空间W的映射
$$
T:V\to W
$$
$$
T(c_1u_1...+c_nu_n)=c_1T(u_1)+...+c_nT(u_n)
$$
> 满足线性性质

### 正交投影算子
$$
w=T(x)
$$
$$
\begin{bmatrix}
w_1
\\w_2
\end{bmatrix}
=\begin{bmatrix}
0&0\\
0&1
\end{bmatrix}
\begin{bmatrix}
x
\\y
\end{bmatrix}
$$

# 向量内积与范数
### 典范内积
$$
<x,y>=x^Hy=\sum_{i=1}^nx_{i}^*y_i
$$

### 加权内积
$$
<x,y>=x^HGy
$$
G为正定Hermitian矩阵


### 连续函数内积
$$
<x(t),y(t)>=\int_a^bx(t)y(t)dt
$$

## 向量范数
+ L0范数
$$
||x||_0=^{def}非零元素的个数
$$
> 表示矩阵稀疏程度

+ L1范数
$$
||x||_1=^{def}\sum_{i=1}^m|x_i|
$$
+ L2范数
$$
||x||_2=(|x_1|^2...+|x_n|^2)^{1/2}=\sqrt{x^Tx}
$$
+ $L_{\infty}$
$$
L_{\infty}=max\{x_i\}
$$
+ $L_P$
$$
||x_p||=(\sum_{i=1}^m|x_i|^p)^{1/p}
$$

## 模式识别和机器学习中的向量相似比较
距离测度$D(p||g)$衡量向量相似度

比如k邻近算法中
$$
D_E(x,s_i)=||x-s_i||_2=\sqrt{(x-s_i)^T(x-s_i)}
$$
## 矩阵内积与范数
矩阵列向量化
$$
a=vec(A)=
\begin{bmatrix}
a_1\\
a_2\\
...\\
a_n
\end{bmatrix}
$$
$$
mn\times 1 向量
$$
### 矩阵内积
$$
<A,B>=<vec(A),vec(B)>=\sum_{i=1}^na_i^Hb_i=\sum_i^n<a_i,b_i>
$$
$$
=vec(A)^Hvec(B)=tr<A^HB>
$$
### 诱导范数
$$
||A||=\max\{||Ax||:x\in K^n,||x||=1\}
$$
$$
=\max\{\frac{||Ax||}{||X||}:x\in K^n,||x||=\not 0\}
$$
#### 诱导p范数
诱导$L$和$L_\infty$范数分别直接是该矩阵的各列元素绝对值之和的最大值(最大绝对列和)及最大绝对行和;而诱导L2范数则是矩阵A的最大奇异值。

$$
\begin{array}{l}
\|\boldsymbol{A}\|_{1}=\max _{1 \leqslant j \leqslant n} \sum_{i=1}^{m}\left|a_{i j}\right| \\
\|\boldsymbol{A}\|_{\mathrm{spec}}=\|\boldsymbol{A}\|_{2} \\
\|\boldsymbol{A}\|_{\infty}=\max _{1 \leqslant i \leqslant m} \sum_{j=1}^{n}\left|a_{i j}\right|
\end{array}
$$
### 元素函数
将m×n矩阵先按照列堆栈的形式，排列成一个mn ×1向量，然后采用向量的范数定义，即得到矩阵的范数。由于这类范数是使用矩阵的元素表示的，故称为元素形式范数。元素形式范数是下面的p矩阵范数

$$
\|\boldsymbol{A}\|_{p} \stackrel{\text { def }}{=}\left(\sum_{i=1}^{m} \sum_{j=1}^{n}\left|a_{i j}\right|^{p}\right)^{1 / p}
$$
+ L1函数（和范数）（p=1）
$$
\|\boldsymbol{A}\|_{1} \stackrel{\text { def }}{=} \sum_{i=1}^{m} \sum_{j=1}^{n}\left|a_{i j}\right|
$$
+ Frobenius范数（p=2）
$$
\|\boldsymbol{A}\|_{\mathrm{F}} \stackrel{\text { def }}{=}\left(\sum_{i=1}^{m} \sum_{j=1}^{n}\left|a_{i j}\right|^{2}\right)^{1 / 2}
$$
Frobenius函数又可以写作迹函数的形式

$$
||A||_F=\sqrt{tr(A^HA)}
$$

+ 最大范数
$$
\|\boldsymbol{A}\|_{\infty}=\max _{i=1, \cdots, m ; j=1, \cdots, n}\left\{\left|a_{i j}\right|\right\}
$$
# 随机向量
 
## 均值向量

$$
\boldsymbol{\mu}_{x}=\mathrm{E}\{\boldsymbol{x}(\xi)\}=\left[\begin{array}{c}
\mathrm{E}\left\{x_{1}(\xi)\right\} \\
\vdots \\
\mathrm{E}\left\{x_{m}(\xi)\right\}
\end{array}\right]=\left[\begin{array}{c}
\mu_{1} \\
\vdots \\
\mu_{m}
\end{array}\right]
$$

## 相关矩阵

$$
\boldsymbol{R}_{x} \stackrel{\text { def }}{=} \mathrm{E}\left\{\boldsymbol{x}(\xi) \boldsymbol{x}^{\mathrm{H}}(\xi)\right\}=\left[\begin{array}{ccc}
r_{11} & \cdots & r_{1 m} \\
\vdots & \ddots & \vdots \\
r_{m 1} & \cdots & r_{m m}
\end{array}\right]
$$

## 自协方差矩阵

$$
C_{x}=\operatorname{Cov}(x, x) \stackrel{\text { def }}{=} \mathrm{E}\left\{\left[x(\xi)-\mu_{x}\right]\left[x(\xi)-\mu_{x}\right]^{\mathrm{H}}\right\}=
\left[\begin{array}{ccc}
c_{11} & \cdots & c_{1 m} \\
\vdots & \ddots & \vdots \\
c_{m 1} & \cdots & c_{m m}
\end{array}\right]
$$
### 自相关矩阵与自协方差矩阵之间的关系

$$
C_x=R_x-\mu_x\mu_x^H
$$
## 互协方差矩阵
$$
C_{xy} \stackrel{\text { def }}{=} \mathrm{E}\left\{\left[x(\xi)-\mu_{u}\right]\left[y(\xi)-\mu_{y}\right]^{\mathrm{H}}\right\}=
\left[\begin{array}{ccc}
c_{x_1,y_1} & \cdots & c_{x_1,y_m} \\
\vdots & \ddots & \vdots \\
c_{x_m,y_1} & \cdots & c_{x_m,x_m}
\end{array}\right]
$$

$$
C_x=R_{xy}-\mu_x\mu_y^H
$$
## 相关系数

$$
\rho_{x y} \stackrel{\text { def }}{=} \frac{c_{x y}}{\sqrt{\mathrm{E}\left\{|x(\xi)|^{2}\right\} \mathrm{E}\left\{|y(\xi)|^{2}\right\}}}=\frac{c_{x y}}{\sigma_{x} \sigma_{y}}
$$

## 高斯随机向量

$$
E\{x(t)\}=0
$$
$$
E\{x(t)x^T(t)\}=\sigma I
$$

# 矩阵的性能指标
## 矩阵的二次型
对于任意方阵A的二次型定义为$x^HAx$

$$
f\left(x_{1}, \cdots, x_{n}\right)=\sum_{i=1}^{n} \alpha_{i i} x_{i}^{2}+\sum_{i=1, i \neq j}^{n} \sum_{j=1}^{n} \alpha_{i j} x_{i} x_{j}
$$
为保证唯一性，在讨论矩阵的二次型时，有必要假定矩阵为实对称矩阵或复共轭对称矩阵

+ 正定矩阵，
    + 二次型$x^HAx > 0$
+ 半正定矩阵
    + $x^HAx > 0$ 
+ 负定矩阵
    + 二次型$x^HAx > 0$
+ 半负定矩阵
    + 若二次型$x^HAx > 0$
+ 不定矩阵，若二次型$x^HAx$ 既可能取正值，也可能取负值。


### 用特征值描述矩阵的正定性与非正定性
+ 正定矩阵:所有特征值取正实数的矩阵。
+ 半正定矩阵:各个特征值取非负实数的矩阵。
+ 负定矩阵:全部特征值为负实数的矩阵。
+ 半负定矩阵:每个特征值取非正实数的矩阵。
+ 不定矩阵:特征值有些取正实数,另一些取负实数的矩阵。

> 矩阵的特征值可描述正定性、奇异性及对角元素的特殊结构

## 矩阵的迹
矩阵的迹反映所有特征值之和
## 矩阵的秩
矩阵中线性无关的行或列的数目
+ 适定方程:若m = n，并且 rank(A) = n，即矩阵A非奇异，则称矩阵方程Aa = b为适定(well-determined)方程。
+ 欠定方程:若独立的方程个数小于独立的未知参数个数，则称矩阵方程 Aa = b为欠定(under-determined)方程。
+ 超定方程:若独立的方程个数大于独立的未知参数个数，则称矩阵方程Aa = b为超定(over-determined)方程。

# 逆矩阵和伪逆矩阵
矩阵的可逆和非奇异的叙述中，下列叙述等价
+ A非奇异
+ A-1存在
+ rank(A) = n
+ A的行线性无关
+ A的列线性无关;
+ det(A)≠0
+ A 的值域的维数是n
+ A 的零空间的维数是0
+ Ax = b对每一个$b\in C^n$都是一致方程
+ Ax = b对每一个b有唯一的解
+ Ax = 0只有平凡解x = 0。


n x n矩阵A的逆矩阵A-1具有以下性质
+ A-1A= AA-1 =I。
+ A-1是唯一的。
+ 逆矩阵的行列式等于原矩阵行列式的倒数，即$|A^{-1}|=\frac{1}{|A|}$
+ 逆矩阵是非奇异的。
+ $(A^{-1})^{-1}=A$

## 矩阵求逆定理(Sherman-Morrison)

$$
(A+xy^H)^{-1}=A^{-1}-\frac{A^{-1}xy^HA^{-1}}{1+y^HA^{-1}x}
$$

## 广义逆矩阵
A的广义逆矩阵满足以下四个条件
$$
\begin{array}{l}
A A^{\dagger} A=A\\
A^{\dagger} AA^{\dagger}=A^{\dagger}
\\
AA^{\dagger}=(AA^{\dagger})^H
\\A^{\dagger}A=(A^{\dagger}A)^H
\end{array}
$$

# 矩阵的直和

$$
\boldsymbol{A} \oplus \boldsymbol{B}=\left[\begin{array}{cc}
\boldsymbol{A} & \boldsymbol{O}_{m \times n} \\
\boldsymbol{O}_{n \times m} & \boldsymbol{B}
\end{array}\right]
$$

# Hadamard积
两个同维度矩阵对应元素直接相乘
$$
(A*B)_{ij}=a_{ij}b_{ij}
$$
# Kronecker积
## 左Kronecker积
$$
\boldsymbol{A} \otimes \boldsymbol{B}=\left[\boldsymbol{a}_{1} \boldsymbol{B}, \cdots, \boldsymbol{a}_{n} \boldsymbol{B}\right]=\left[a_{i j} \boldsymbol{B}\right]_{i=1, j=1}^{m, n}=\left[\begin{array}{cccc}
a_{11} \boldsymbol{B} & a_{12} \boldsymbol{B} & \cdots & a_{1 n} \boldsymbol{B} \\
a_{21} \boldsymbol{B} & a_{22} \boldsymbol{B} & \cdots & a_{2 n} \boldsymbol{B} \\
\vdots & \vdots & \ddots & \vdots \\
a_{m 1} \boldsymbol{B} & a_{m 2} \boldsymbol{B} & \cdots & a_{m n} \boldsymbol{B}
\end{array}\right]
$$

## 右Kronecker积
$$
[\boldsymbol{A} \otimes \boldsymbol{B}]_{\text {left }}=\left[\boldsymbol{A} \boldsymbol{b}_{1}, \cdots, \boldsymbol{A} \boldsymbol{b}_{\boldsymbol{q}}\right]=\left[b_{i j} \boldsymbol{A}\right]_{i=1, j=1}^{p, \boldsymbol{q}}=\left[\begin{array}{cccc}
\boldsymbol{A} b_{11} & \boldsymbol{A} b_{12} & \cdots & \boldsymbol{A} b_{1 \boldsymbol{q}} \\
\boldsymbol{A} b_{21} & \boldsymbol{A} b_{22} & \cdots & \boldsymbol{A} b_{2 q} \\
\vdots & \vdots & \ddots & \vdots \\
\boldsymbol{A} b_{\boldsymbol{p} 1} & \boldsymbol{A} b_{p 2} & \cdots & \boldsymbol{A} b_{p q}
\end{array}\right]
$$
# 矩阵向量化
## 按列堆栈

$$
vec (\boldsymbol{A})=\left[a_{11}, \cdots, a_{m 1}, \cdots, a_{1 n}, \cdots, a_{m n}\right]^{\mathrm{T}}
$$
## 按行堆栈
$$
rvec (\boldsymbol{A})=\left[a_{11}, \cdots, a_{1 n}, \cdots, a_{m 1}, \cdots, a_{m n}\right]
$$