---
title: 奇异值SVD
toc: true
copyright: true
date: 2020-10-21 08:51:25
tags:
    - 矩阵论
categories:
    - 《柯西的传世绝学》
reward:
---
# 数值的稳定性与条件数
当输入d受到扰动时，输出f(d) 的扰动情况
<!--more-->
目的：解决病态问题

## 条件数
+ A 数据矩阵 n*n
+ b 数据向量 n*1
+ x 未知向量 n*1


在这里我们研究x受A，或者b扰动的影响
$$
A(x+\delta x)=b+\delta b
$$
$$
A\delta x=\delta b
$$
$$
\delta x=A^{-1}\delta b
$$

由

$$
||AB||<=||A|| ||B||
$$
$$
\to
\begin{cases}
||\delta x||_2<=||A^{-1}||_2 ||\delta b||_2
\\
||b||_2<=||A||_2 ||x||_2\to \frac{1}{||x||_2}<=\frac{||A||_2}{||b||_2}
\end{cases}
$$
两边相乘
$$
\to \frac{||\delta x||_2}{||x||_2}<=||A^{-1}||_2 ||A||_2 \frac{||\delta b||_2}{||b||_2}
$$
一起考虑A扰动的影响，可以得到
$$
(A+\delta A)(x+\delta x)=b
$$
$$
\begin{array}{l}
\delta x=(A+\delta A)^{-1}b-A^{-1}b
\\
=A^{-1}[A-(A+\delta A)](A+\delta A)^{-1}b
\\
=A^{-1}(-\delta A)(A+\delta A)^{-1}b
\\
\to \frac{||\delta x||_2}{||x+\delta x||_2}<=||A^{-1}||||A||_2\frac{||\delta A||_2}{||A||_2}
\end{array}
$$
可以看出噪声（解向量x的误差）与某个数成正比，这个数被称为**条件数**
$$
cond(A)=||A^{-1}||_2||A||_2
$$
有性质
$$
cond(A^HA)=[cond(A)]^2
$$


如果矩阵A不是方阵，可以求出最小二乘解
$$
Ax=b

\to x=(A^HA)^{-1}A^{H}b
$$
求此时的条件数
$$
cond(A^HA)=||A^HA||_2||(A^HA)^{-1}||_2=cond(A)^2
$$
条件数平方后变大，所以此时的最小二乘解不稳定 

# 奇异值分解
奇异值分解定理对于矩阵$A:m\times n$,存在正交或者酉矩阵$U:m\times m,V:n\times n$使得
$$
A=U\Sigma V^H
$$
$$
\Sigma=
\begin{bmatrix}
\Sigma_r &0\\
0 &0
\end{bmatrix}
$$
$$
diag(\Sigma_r)=[\sigma_1,\sigma_2...\sigma_r]
$$
$$
r=rank(A)
$$

$\sigma_1,\sigma_2...\sigma_r，\sigma_{r+1}=...\sigma_n=0$被称为A的奇异值


$$
AV=U\Sigma
$$
$$
\to Av_i=
\begin{cases}
u_i\sigma_i &i<=r\\
0&i>r
\end{cases}
$$
$$
U^HA=\Sigma V^H
$$
$$
u_i^HA=\sigma_iv_i^H
$$
$v_i$为右奇异向量,$u_i$为左奇异向量

+ 矩阵A的奇异值分解式可以改写成向量表达式
$$
A=\Sigma_{i=1}^r\sigma_i u_i v_i^H
$$
+ 当矩阵的秩$r=rank(A)<min(m,n)$
奇异值分解可以被简化为

$$
A=U_r\Sigma_rV_r^H
$$
被称为截断奇异值分解，
只取前r个非0度奇异值

## 奇异值分解和特征分解的关系
$$
A^HA=V\Sigma U^HU\Sigma V^H
$$
$$
=V\Sigma^2V^H
$$

+ $A^HA$的特征值是A奇异值的平方，是右奇异向量
+ $AA^H$的特征值是A奇异值的平方，是左奇异向量
$$
AA^H=U\sum^2U^H
$$
+ 广义逆
$$
A^\dagger=V\Sigma^\dagger U^H
$$
## 奇异值的性质
### 范数性质
+ 诱导谱范数
$$
||A||_{spec}=||A||_2=\sigma_i(最大奇异值)
$$
+ f范数
$$
||A||_F=sqrt{<A,A>}=\sqrt{tr(A^H,A)}=\sqrt{\sum \sigma_i}
$$
所以特征值之和=奇异值平方和
$$
\lambda_1+\lambda_2...+\lambda_r=\sigma_1^2+\sigma_2^2...+\sigma_r^2
$$

> 根据矩阵A的谱范数可以确定最大奇异值



### 酉不变性
$$
A=U\Sigma V^H
$$
在矩阵A的基础上再左乘或者右乘一个酉矩阵
$$
B=PU\Sigma V^HQ^H
$$
B的奇异值不变

### 奇异值与行列式
因为酉矩阵行列式绝对值为1

所以
$$
|detA|=|det\sum|=\sigma_1\sigma_2...\sigma_n
$$
如果$detA\not=0$表明A是非奇异的，若存在$\sigma_i=0,datA=0$,则A奇异，这是把$\sigma$称为奇异值的原因

### 奇异值与条件数
$$
cond(A)=\sigma_1/\sigma_p(p=\{m,n\})
$$
所以条件数总大于1

> 奇异值的内在含义，如果一个矩阵有一个奇异值为0，对于正方矩阵，代表，矩阵奇异，行列式为0，非正方矩阵代表秩亏缺

## 秩亏缺矩阵（LS）
应用奇异值分解求解最小二乘问题的方法常简称为奇异值分解方法。

$$
\begin{array}{l}
Ax=b
\\
U\Sigma V^Hx=b
\\
\Sigma V^Hx=U^Hb
\end{array}
$$
令
$$
x'=V^Hx,y=U^Hb
$$
得到
$$
\to \Sigma x'=y
$$
我们的目标变为优化问题
$$
min||\Sigma x'-y||_2^2

=\sum_{i=1}^r|\sigma_ix_i-y_i|^2+\sum_{i=r+1}^N|y_i|^2=0
$$
得到最小范数解
$$
x_{LS}=\sum_{i=1}^r(u_i^Hb/\sigma_i)v_i
$$
相应的最小残差为
$$
\rho_{LS}=||Ax_{LS}-b||_2=||[u_{r+1},..,u_m]^Hb||_2
$$
### 有效秩的确定 
如果要衡量衡量A，B的逼近程度，P,K分别为A、B的秩
$$
A=\sum_{i=1}^P\sigma_i u_i v_i^H
$$
$$
B=\sum_{i=1}^K\sigma_i u_i v_i^H
$$
+ 谱范数法
$$
||A-B||_{spec}=\sigma_{k+1}
$$
+ F范数法
$$
||A-B||_F=\sqrt{\sum_{i=k+1}^P\sigma_i^2}
$$
#### 衡量标准

对应谱范数
$$
\epsilon=\frac{\sigma_k}{\sigma_1}>=5\%
$$
对应F范数（范数比方法）
$$
V(k)=\frac{\sqrt{\sum^k\sigma^2}}{\sqrt{\sum^P\sigma^2}}
$$
$$
=\frac{||A_k||_F}{||A||_F}>=\alpha
$$
### 奇异值分解在图像视频压缩中的作用
在矩阵A稀疏的情况下
$$
A \to n\times n
$$
$$
A_k=U_k\sum_kV_k^H
$$







