---
title: Bianisotropic media
date: 2020-06-19 20:02:31
copyright: true
tags:
	- 手撕麦克斯韦
categories: 
    - 《行于黑暗，侍奉光明，我们是电工》
---


## Anisotropic Media各向异性介质
物质本构关系
$$
\overrightarrow{D}=\bar{\epsilon}\overrightarrow{E}
$$
$$
\overrightarrow{B}=\bar{\mu}\overrightarrow{H}
$$
> 各方向介电值，磁导率不同

<!--more-->

### 最简单的z轴为光轴的单轴晶体

石英，方解石，存在双折射现象
$$
\bar{\epsilon}=
\begin{bmatrix}
\epsilon&0&0\\
0&\epsilon&0\\
0&0&\epsilon_z
\end{bmatrix}
$$
> $\epsilon_z>\epsilon$正单轴 positive uniaxial

> $\epsilon_z<\epsilon$ 负单轴 nagative uniaxial

### 外加直流磁场的plasma media
磁场方向为z0方向时

$$
\bar{\epsilon}=
\begin{bmatrix}
\epsilon&i\epsilon_g&0\\
i\epsilon_g&\epsilon&0\\
0&0&\epsilon_z
\end{bmatrix}
$$
> $wc=qB_0/m$
### gyromagnetic madium 回转磁性介质
media characterized by hermitian permittivity tensor。铁氧体

$$
\bar{\epsilon}=
\begin{bmatrix}
\mu&i\mu_g&0\\
i\mu_g&\mu&0\\
0&0&\mu_z
\end{bmatrix}
$$

## Biisotropic 双各向同性介质
物质本构关系
$$
\overrightarrow{D}=\epsilon\overrightarrow{E}+\xi\overrightarrow{H}
$$
$$
\overrightarrow{B}=\mu\overrightarrow{H}+\zeta\overrightarrow{E}
$$

#### Tellegen medium
非互易介质
$$
\overrightarrow{D}=\epsilon\overrightarrow{E}+\tau\overrightarrow{H}
$$
$$
\overrightarrow{B}=\mu\overrightarrow{H}+\tau\overrightarrow{E}
$$
> $\tau^2/\mu\epsilon\approx1$

#### Chiral Media
手性介质
$$
\overrightarrow{D}=\epsilon\overrightarrow{E}+i\chi\overrightarrow{H}
$$
$$
\overrightarrow{B}=\mu\overrightarrow{H}-i\chi\overrightarrow{E}
$$
> DNA $\chi$为手性参数

## Bianisotropic media双各向异性介质
物质本构关系
$$
\overrightarrow{D}=\bar\epsilon\overrightarrow{E}+\bar\xi\overrightarrow{H}
$$
$$
\overrightarrow{B}=\bar\mu\overrightarrow{H}+\bar\zeta\overrightarrow{E}
$$
> 用36个复数或72个实数，2 * 9 * 4可以概括宇宙中所有介质

## Stmmetry condition for lossless media无损介质

+ 无损介质的定义lossless
$$
<\nabla\cdot\overrightarrow{S}>=0
$$
> 散度的物理意义为流出的能量

+ passive
$$
<\nabla\cdot\overrightarrow{S}><0
$$
+ active
$$
<\nabla\cdot\overrightarrow{S}>>0
$$

其中

$$
\nabla\cdot\overrightarrow{S}=1/2Re[iw(\overrightarrow{H}^*\cdot\overrightarrow{B}-\overrightarrow{E}\cdot\overrightarrow{D})]
$$

$$
	=1/4[iw(\overrightarrow{H}^*\cdot\overrightarrow{B}-\overrightarrow{E}\cdot\overrightarrow{D})-iw(\overrightarrow{H}^*\cdot\overrightarrow{B}-\overrightarrow{E}\cdot\overrightarrow{D})^*]   
$$

$$
\#\#Re\{i(a+bi)=1/2((a+bi)-(a-bi))\#\#
$$

$$
	=\frac{iw}{4}\{\overrightarrow{E}^*\cdot(\bar\epsilon-\bar\epsilon^+)\cdot\overrightarrow{E}+\overrightarrow{H}^*\cdot(\bar\mu-\bar\mu^+)\cdot\overrightarrow{H}+\overrightarrow{E}^*\cdot(\bar\xi-\bar\zeta^+)\cdot\overrightarrow{H}+\overrightarrow{H}^*\cdot(\bar\zeta-\bar\xi^+)\cdot\overrightarrow{E}\}   
$$

#### lossless无损条件

$$
\bar\epsilon=\bar\epsilon^+
$$
$$
\mu=\bar\mu^+
$$
$$
\bar\zeta=\bar\xi^+
$$
$$
\bar\xi=\bar\zeta^+
$$

> 厄米矩阵：
将一矩阵A的行与列互换，并取各矩阵元素的共轭复数，得一新矩阵，称为厄米特共轭，以A+表之，对角线必为实数，如
$$
		\begin{bmatrix}
		2&2+i\\
		2-i&2
		\end{bmatrix}
$$

可推导
$$
\bar\kappa=\bar\kappa^+
$$
$$
\bar\nu=\bar\nu^+
$$
$$
\bar\chi=\bar\gamma^+
$$
----------------
$$
\bar P=\bar P^+
$$
$$
\bar Q=\bar Q^+
$$
$$
\bar L=\bar M^+
$$

## Reciprocity Media互易介质

#### reciprocity condition
**互易条件**
$$
\bar\epsilon=\bar\epsilon^T
$$
$$
\mu=\bar\mu^T
$$
$$
-\bar\zeta=\bar\xi^T
$$
$$
\bar\kappa=\bar\kappa^T
$$
$$
\bar\nu=\bar\nu^T
$$
$$
\bar\chi=-\bar\gamma^T
$$
