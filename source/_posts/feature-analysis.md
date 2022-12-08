---
title: 矩阵特征分析
toc: true
copyright: true
date: 2020-10-21 08:55:55
tags:
    - 矩阵论
categories:
    - 《柯西的传世绝学》
reward:
---
# 特征值求解方法 
如果
$$
L[u]=\lambda u
$$
$$
u =\not 0
$$
则$\lambda$称为线性算子L的特征值，u为特征向量
<!--more-->

特征值求解
$$
Au=\lambda u
$$
$$
\to det(A-\lambda I)=0
$$

如果A为Hermitian矩阵，则
$$
A=U\Sigma U^H
$$
$$
U=[u_1...u_n]^T
$$
$$
\Sigma=diag(\lambda_1...\lambda_2)
$$
## 特征值的基本概念
+ 称A的特征值入具有代数多重度(algebraic multiplicity) u，若$\lambda$是特征多项式
det(A - zI)=0的u重根。
+ 若特征值$\lambda$的代数多重度为1，则称该特征值为单特征值(simple eigenvalue)。非
单的特征值称为多重特征值(multiple eigenvalue)。
+ 称A的特征值入具有几何多重度(geometric multiplicity)~，若与入对应的线性
无关特征向量的个数为$\gamma$。换言之，几何多重度，是特征空间Null(A -入I)的维数。
+ 矩阵A称为减次矩阵(derogatory matrix)，若至少有一个特征值的几何多重度
大于1。
+ 一特征值称为半单特征值(semi-simple eigenvalue)，若它的代数多重度等于它的
几何多重度。不是半单的特征值称为亏损特征值(defective eigenvalue)。
## 特征多项式
$$
P(x)=det(A-xI)
=P_nx^n...P_1x+P_0
$$

### 特征方程
P(x)=0为特征方程

## 特征值性质
+ 矩阵A奇异，当且仅当至少有一个特征值$\lambda$=0。
+  矩阵A和$A^T$具有相同的特征值。

$$
\begin{array}{l}
A\to \lambda
\\
A^T\to \lambda
\\
A^H\to \lambda^*
\\
A^k\to \lambda^k
\\
A^{-1}\to \lambda^{-1}
\\
A+\sigma^2 I\to\lambda+\sigma^2
\end{array}
$$
+ 共轭特征值和共轭特征向量成对出现
+ 对角矩阵和三角矩阵特征值为对角线元素值
+ 幂等矩阵$A^2=A$特征值全部为0、1
+ 实正交矩阵特征值全部在单位圆上
+ 奇异矩阵至少一个特征值为0
+ 非奇异矩阵所有特征值非0
+ 特征值之和=迹
$$
\sum_{i=1}^n\lambda_i=tr(A)
$$
+ 一个Hermitian矩阵A是正定(或半正定)的，当且仅当它的特征值是正(或者
非负)的。
+ 特征值之积等于行列式
$$
\prod \lambda=det(A)=|A|
$$
+ 特征值与秩的关系:
    + 若n×n矩阵A有r个非零特征值，则rank(A) ≥T。
    + 若0是n×n矩阵A的无多重的特征值，则rank(A)= n - 1。
    + 若rank(A -$\lambda$I)≤n -1，则$\lambda$是矩阵A的特征值。

+ 若A的特征值不相同，则一定可以找到一个相似矩阵$S^{-1}AS= D$(对角矩阵)，
其对角元素即是矩阵A的特征值。
+ n xn矩阵A的任何一个特征值$\lambda$的几何多重度都不可能大于$\lambda$的代数多
重度。
+ Caley-harmilton定理
$$
\prod(A-\lambda_iI)=0
$$


+ 特征值和相似矩阵
    + 若$\lambda$是nxn矩阵A的一个特征值，并且nxn矩阵B非奇异，则入也是矩阵B-1AB的一个特征值，但对应的特征向量一般不相同。
    + 若$\lambda$是n×n矩阵A的一个特征值，并且n×n矩阵B是酉矩阵，则$\lambda$也是矩阵$B^HAB$的一个特征值，但对应的特征向量一般不相同。
    + 若$\lambda$是nxn矩阵A的一个特征值，并且nxn矩阵B是正交矩阵，则$\lambda$也是
矩阵$B^TAB$的一个特征值，但对应的特征向量一般不相同。
+ 一个n xn矩阵A的最大特征值以该矩阵的列元素之和的最大值为界，
$$
\lambda_{max}<max\sum_{j=1}^n a_{ij}
$$
+ 随机向量$x(t)= [x_1(t),x_2(t),… ,x_n(t)]^T$的相关矩阵$R=E\{x(t)x^H(t)\}$的特征值以最大和最小功率为界
$$
P_{min}<=\lambda<=P_{max}
$$
## 矩阵的谱
矩阵所有特征值的集合
### 谱半径
$$
\rho=max(\lambda_i)
$$
## 矩阵对角化
+ 定义： 一个n×n实矩阵A若与一个对角矩阵相似，则称矩阵A是可对角化
的(diagonalizable)。

+ 定理：一个nxn实矩阵A是可对角化的，当且仅当A具有n个线性无关的
特征向量。
$$
U^{-1}AU=\Sigma 
$$
$$
U=[u_1...u_n]^T
$$
$$
\Sigma=diag(\lambda_1...\lambda_2)
$$


# Caley-harmlton定理及应用
若
$$
P(x)=P_nA^n+...P_1A+P_0I=O
$$
则
$$
P(x)=P_nx^n+...P_1x+P_0
$$
是使A零化的多项式，则
$$
P(A)=0
$$



## 可以利用该定理求逆

左右同乘A的逆
$$
A^{-1}=-\frac{1}{P_0}(P_nA^{n-1}+P_{n-1}A^{n-2}+...+P_1I)
$$

+ example
$$
A=\begin{bmatrix}
1&5\\
4&6
\end{bmatrix}
$$
$$
\operatorname{det}(\boldsymbol{A}-x \boldsymbol{I})=\left|\begin{array}{cc}
1-x & 5 \\
4 & 6-x
\end{array}\right|=(1-x)(6-x)-5 \times 4=x^{2}-7 x-14
$$
$$
\boldsymbol{A}^{-1}=\frac{1}{14}(\boldsymbol{A}-7 \boldsymbol{I})=\frac{1}{14}\left(\left[\begin{array}{ll}
1 & 5 \\
4 & 6
\end{array}\right]-7\left[\begin{array}{ll}
1 & 0 \\
0 & 1
\end{array}\right]\right)=\left[\begin{array}{rr}
-\frac{3}{7} & \frac{5}{14} \\
\frac{2}{7} & -\frac{1}{14}
\end{array}\right]
$$

## 矩阵指数函数的计算
$$
e^{At}=I+At...\frac{1}{k!}A^kt^k...
$$
对于常见的一阶微分方程
$$
x'(t)=Ax(t)
$$
$$
x(0)=x_0
$$
解为
$$
x(t)=e^{At}x_0
$$
### 多阶矩阵微分方程
若A的特征多项式为
$$
p(\lambda)=\lambda^n+c_{n-1}\lambda^{n-1}...+c_1\lambda+c_0
$$

对于矩阵微分方程
$$
Y^{(n)}(t)+c_{n-1}Y^{(n-1)}(t)...Y(t)=O
$$
且满足初始条件
$$
\begin{array}{l}
Y(0)=I
\\
Y'(0)=A\\
...
\\
Y^{(n-1)}(t)=A^{n-1}
\end{array}
$$
则$Y(t)=e^{At}$为矩阵方程唯一解

那么如何求解这个唯一解？
$$
Y(t)=x_1(t)I+x_2(t)A+...x_nA^{n-1}
$$
其中$x_k(t)$满足微分方程
$$
x^{(n)}(t)+c_{n-1}x^{(n-1)}(t)...c_1x'(t)+c_0x(t)=0
$$
且满足初始条件
$$
x_i^{(i-1)}=1
$$
其他所有为0

----------------

# 特征分解的应用
给定一组彼此相关的随机变量，常常希望通过线性变换，把它变换成另外一组统计不相关的随机变量。甚至更进一步，希望变换后的一组统计不相关随机变量各个分量还具有单位方差。这两个任务可以通过标准正交变换和迷向圆变换分别完成。

## 标准正交变换
x 为m维随机向量，将x转化为0均值的随机向量，此时自相关矩阵和协方差矩阵相同，$m_x$为其均值向量

$$
x_0=x-m_x
$$
$$
R_{x_0}=C_x
$$
其特征分解为
$$
C_x=U_x\Sigma_xU_x^H
$$
令
$$
w=U_x^Hx_0=U_x^H(x-m_x)
$$
$$
m_w=0
$$
$$
C_w=R_w=U_x^HU_x\Sigma_x U_x^HU_x=\Sigma_x
$$
> 该变化用于有色噪声白化

## 迷向圆变化
在上面的标准正交变换中，线性变换$w= U^H_x(x-m_x)$的自相关矩阵(与协方差矩阵相等)
$R_x$。为对角矩阵，但不是单位矩阵Ⅰ。要使u的自相关矩阵为单位矩阵，就需要对w再
作另一个线性变换
$$
y=\Sigma_x^{-1/2}w=\Sigma_x^{-1/2}U_x^H(x-m_x)
$$
则
$$
R_y=\Sigma_x^{-1/2}\Sigma\Sigma_x^{-1/2}=I
$$

## 离散K-L变换
在许多信号处理和模式识别应用中，常常需要将随机信号的观测样本用另外一组数(或系数)表示，同时使这种新的表示具有某些所希望的性质。例如，对于编码而言，希望信号可以用少数系数表示，同时这些系数集中了原信号的功率。又如，对于最优滤波，则希望变换后的样本统计不相关，这样就可以降低滤波器的复杂度，或者提高信噪比。实现上述目标的通用做法是将信号展开成正交基函数的线性组合，使得信号相对于基函数的各个分量不会相互干扰。

如果正交基函数根据信号观测样本的协方差矩阵适当选择，就有可能在所有正交基函数中，获得具有最小均方误差的信号表示。在均方误差最小的意义上，这样一种信号表示是最优的信号表示，它在随机信号的分析与编码中具有重要的意义和应用。这种信号变换是Karhunen和 Loeve 针对连续随机信号提出的，称为Kauhunen-Loeve变换。

对于M维向量
$$
x=[x_1,x_2...x_M]^T
$$
是一零均值向量


我们用小维度的w表示x,$Q$为一个酉矩阵
$$
W=Q^Hx
$$

$$
x=QW=\sum_{i=1}^Mq_iw_i
$$
为了减小变换后的系数u;的个数,假定在上式中只使用w的前m个系数$w_1,…, w_m(m = 1,… M)$逼近随机信号向量c，即

$$
\hat{x}=\sum_{i=1}^mq_iw_i ,( 1=<m<=M)
$$
## 主分量分析
组分量分析的核心思想是吧，存在信息冗余的特征向量空间，通过正交变换进行降维，变成无信息冗余的向量空间

令Rx是数据向量x 的自相关矩阵，它有K个主特征值，与这些主特征值对应的K个特征向量称为数据向量x的主分量。
### 过程
+ 降维
+ 正交化
+ 功率最大化

$$
\hat{x}=Q^Hx=\sum_{i=1}^p q_ix_i\approx \sum_{i=1}^kq_ix_i(k<p)
$$

# 广义特征分解
$$
Au=\lambda Bu
$$
$$
det(A-\lambda B)=0
$$


# Rayleigh商
## Rayleigh商定义及其性质
Hermitian矩阵 $A\in C^{n\times n}$的 Rayleigh商或Rayleigh-Ritz 比 R(z)是一个标量，定义为

$$
R(x)=\frac{x^HAx}{x^Hx}
$$
> 瑞利商的目的是找到x让瑞利商最大或者最小,常在滤波中使用

假设信号如下，如果要对信号进行滤波，利用滤波器x，让滤波后信噪比最大

$$
r(t)=B\alpha S(t)+n(t)
$$
+ 滤波器$x^H$进行滤波后，SNR为
$$
\frac{|x^HB\alpha S(t)|^2}{|x^Hn|^2}
$$
$$
=\frac{x^HAx}{x^Hn^Hnx}(噪声为白噪声时)
$$
$$
=\frac{x^HAx}{\sigma^2 x^Hx}
$$

## Rayleigh-Ritz定理
取x取最大最小特征值对应的特征向量时可以得到极值，极值为最大或最小特征值
$$
Ax=\lambda x
$$
$$
max \frac{x^HAx}{x^Hx}=\lambda_{max}
$$
$$
min \frac{x^HAx}{x^Hx}=\lambda_{min}
$$

## 广义瑞利商
当噪声不为白噪声时，噪声相关矩阵为B
$$
R(x)=\frac{x^HAx}{x^HBx}
$$


应用变量代换
$$
\hat{x}=B^{1/2}x
$$
$$
R(\hat{x})=\frac{\hat{x}^H(B^{-1/2})^HAB^{1/2}\hat{x}}{\hat{x}^H\hat{x}}
$$
最大最小值为矩阵
$$
(B^{-1/2})^HAB^{1/2}
$$
的最大或最小特征值

变量代换后求广义特征值
$$
Ax=\lambda Bx
$$
