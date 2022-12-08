---
title: 子空间理论
toc: true
copyright: true
date: 2020-11-16 21:36:39
tags:
    - 矩阵论
categories:
 - 《柯西的传世绝学》
reward:
---
# 子空间的基本理论
## 子空间的基
**定义**：若$S=\{u_1,u_2...u_m\}$是向量空间V的向量子集合，则向量所有的线性组合
W，称为$u_1,u_2...u_m$构成的子空间
<!--more-->
$$
W=span\{u_1,u_2...u_m\}=\{u|u=a_1u_1+...+a_mu_m\}
$$
当这些向量线性无关时，称为W的一组基

## 张成集定理(spanning set theorem)
令S ={u…,um}是向量空间V的一个子集，并且W= Span{u,…,um}是由S的m个列向量张成的一个子空间。

+ 如果S内有某个向量(例如uk)是其他向量的线性组合，则从S中删去向量uk后，其他向量仍然张成子空间W。
+ 若W≠{0}即W为非平凡子空间，则在S内一定存在某个由线性无关的向量组成的子集合，它张成子空间W。

# 矩阵行空间，列空间
对于矩阵$A\in C^{m\times n}$

$$
A=[a_1,a_2...a_n]
$$
$$
=\begin{bmatrix}
r_1\\r_2\\...\\r_m
\end{bmatrix}
$$
矩阵的列空间为矩阵列向量张成
$$
Col(A)=span\{a_1,a_2...a_n\}
$$
行空间同理
$$
Row(A)=span\{r_1^*,r_2^*...r_m^*\}
$$
# 基本空间的标准正交基的构造：奇异值分解

根据奇异值分解的性质，我们知道矩阵A可以被分解为
$$
A=U_r\Sigma_rV_r^H
$$
$$
=sum_{i=1}^r \sigma_i u_iv_i
$$
定义$A\in C^{m\times n},A$的值域Range定义为
$$
Rang(A)=\{y\in C^m|Ax=y,x\in C^n\}
$$
此时的线性映射从$C^n$空间到$C^m$

## 零空间
**零空间**被定义为满足
$$
Ax=0
$$
的向量x集合
$$
Null(A)=ker(A)=\{x\in C^n|Ax=0\}
$$

## 列空间的标准正交基
与r个非零奇异值所对于的左奇异向量$u_1,u_2...u_r$构成列空间col（A）的一组基
$$
Range(A)=\{y\in c^m|y=Ax,x\in C^n\}
$$
$$
=\{y|y=\sum_{i=1}^ru_i(\sigma_iv_i^Hx)\}
$$
$$
=\{y|y=\sum_{i=1}^r\alpha_iu_i，\alpha_i=\sigma_iv_i^Hx\}
$$
$$
=span\{u_1,u_2...u_r\}
$$

# 行空间标准正交基
与列空间的推导同理
$$
Range(A^H)=\{y\in C^n|y=\sum_{i=1}^r \alpha_iv_i,\alpha_i=\sigma_iu_i^Hx\}
$$

# 信号子空间和噪声子空间
如果观测数据A存在噪声误差
$$
X=A+W=[x_1,x_2...x_n]\in C^{m\times n}
$$
定义
+ 观测数据子空间
$$
span(X)=span\{x_1,x_2...x_n\}
$$
+ 噪声子空间
$$
span(W)=span\{w_1,w_2...w_n\}
$$

+ X的协方差矩阵为
$$
E\{x^Hx\}=E\{(A+W)^H(A+W)\}
$$
$$
=E\{A^HA\}+E\{W^HW\}
$$
$$
=R+\sigma_wI
$$
令A的秩为r

则
$$
R_X=U\Sigma U^H+\sigma_w^2I=U(\Sigma+\sigma_w^2 I)U^H
$$
$$
\Sigma+\sigma_w^2I=diag(\sigma_1^2+\sigma_w^2...\sigma_r^2+\sigma_w^2,\sigma_w^2...\sigma_w^2)
$$
如果信噪比足够大，即$\sigma_r^2>\sigma_w^2$

则前r个大特征值称为**主特征**

剩余n-r个称为**次特征**

$$
R_x=[S,G]\begin{bmatrix}\Sigma_s&0\\
0&\Sigma_n
\end{bmatrix}
\begin{bmatrix}
S^H\\G^H
\end{bmatrix}
$$
$$
=S\Sigma_sS^H+G\Sigma_nG^H
$$
此时
$$
S=[s_1..s_2...s_r]=[u_1,u_2...u_r]
\\
G=[g_1,g_2...g_{n-r}]=[u_{r+1}...u_n]
\\
\Sigma_s=diag(\sigma_1^2+\sigma_w^2...\sigma_r^2+\sigma_w^2)
\\
\Sigma_n=diag(\sigma_w^2...\sigma_w^2)
$$

+ $Range(S)$称为信号子空间

+ $Range(G)$称为噪声子空间

## 重要性质
噪声子空间和信号子空间正交
$$
UU^H=SS^H+GG^H=I
$$