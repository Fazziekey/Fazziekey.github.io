---
title: Media
date: 2020-06-19 15:45:15
copyright: true
tags:
	- 手撕麦克斯韦
categories: 
    - 《行于黑暗，侍奉光明，我们是电工》
---
# 3.1time-harmonic field 正弦时变场
## 信号频域分析

### 基本公式

$$
\overrightarrow{E}(\overrightarrow{r},t)=Re\{\overrightarrow{E}(\overrightarrow{r})e^{-iwt}\}
$$
$$
\overrightarrow{B}(\overrightarrow{r},t)=Re\{\overrightarrow{B}(\overrightarrow{r})e^{-iwt}\}
$$
$$
\overrightarrow{D}(\overrightarrow{r},t)=Re\{\overrightarrow{D}(\overrightarrow{r})e^{-iwt}\}
$$
$$
\overrightarrow{H}(\overrightarrow{r},t)=Re\{\overrightarrow{H}(\overrightarrow{r})e^{-iwt}\}
$$
$$
\overrightarrow{J}(\overrightarrow{r},t)=Re\{\overrightarrow{J}(\overrightarrow{r})e^{-iwt}\}
$$
$$
\overrightarrow{\rho}(\overrightarrow{r},t)=Re\{\overrightarrow{\rho}(\overrightarrow{r})e^{-iwt}\}
$$
> 作用，去除麦克斯韦方程中微分，把微分方程化为代数方程

<!--more-->

### 频域麦克斯韦
#### 推导
$$
\nabla\times\overrightarrow{E}(\overrightarrow{r},t)=-\frac{\partial}{\partial t}\overrightarrow{B}(\overrightarrow{r},t)
$$

$$
Re\{[\nabla\times\overrightarrow{E}(\overrightarrow{r})-iw\overrightarrow{B}(\overrightarrow{r})]e^{-iwt}\}=0
$$

$$
\nabla\times\overrightarrow{E}(\overrightarrow{r})-iw\overrightarrow{B}(\overrightarrow{r})=0
$$
#### 频域麦克斯韦方程组
$$
\begin{cases} \nabla\times\overrightarrow{E}=iw\overrightarrow{B}\\
\nabla\times\overrightarrow{H}=-iw\overrightarrow{D}+\overrightarrow{J}\\
\nabla\cdot\overrightarrow{B}=0\\
\nabla\cdot\overrightarrow{D}=\rho
\end{cases}
$$
### 频域亥姆霍兹方程

$$
(\nabla^2+w^2\mu\varepsilon)\overrightarrow{E}=0
$$
## 极化（Polarization of Monochromatic Waves）

对于$\overrightarrow{E}(\overrightarrow{r},t)$当r=0，令频域
$$
\overrightarrow{E}=\overrightarrow{E}_R+i\overrightarrow{E}_I
$$
由$\overrightarrow{E}_R$,$\overrightarrow{E}_I$定义的的平面称为极化平面

$$
\overrightarrow{E}(t)=Re\{(\overrightarrow{E}_R+i\overrightarrow{E}_I)e^{-iwt}\}=\overrightarrow{E}_Rcoswt+\overrightarrow{E}_Isinwt
$$

$$
\frac{\partial\overrightarrow{E}(t)}{\partial t}=w[-\overrightarrow{E}_Rsinwt+i\overrightarrow{E}_Icoswt]
$$
![](https://cdn.jsdelivr.net/gh/Fazziekey/image-bed/img/20200619163521.png)

> 当$E_R，E_I$平行时,波线性极化，垂直时圆极化或椭圆极化

--------------
## 频域功率计算
定义**频域波印廷矢量**

$$
\overrightarrow{S}=\overrightarrow{E}\times\overrightarrow{H}^*
$$


定义
$$
\overrightarrow{E}(\overrightarrow{r})=\overrightarrow{E}_R(\overrightarrow{r})+i\overrightarrow{E}_I(\overrightarrow{r})
$$
$$
\overrightarrow{H}(\overrightarrow{r})=\overrightarrow{H}_R(\overrightarrow{r})+i\overrightarrow{H}_I(\overrightarrow{r})
$$
可得
$$
\overrightarrow{E}(\overrightarrow{r},t)=Re\{\overrightarrow{E}(\overrightarrow{r})e^{-iwt}\}=\overrightarrow{E}_Rcoswt+\overrightarrow{E}_Isinwt
$$
同理
$$
\overrightarrow{H}(\overrightarrow{r},t)=Re\{\overrightarrow{H}(\overrightarrow{r})e^{-iwt}\}=\overrightarrow{H}_Rcoswt+\overrightarrow{E}_Isinwt
$$
所以频域波印廷矢量
$$
\overrightarrow{S}=\overrightarrow{E}_R\times\overrightarrow{H}_R+\overrightarrow{E}_I\times\overrightarrow{H}_I+i(\overrightarrow{E}_I\times\overrightarrow{H}_R-\overrightarrow{E}_R\times\overrightarrow{H}_I)
$$
时域波印廷矢量
$$
\overrightarrow{S}(\overrightarrow{r},t)=\overrightarrow{E}(\overrightarrow{r},t)\times\overrightarrow{H}(\overrightarrow{r},t)
$$
代入得
$$
\overrightarrow{S}=\overrightarrow{E}_R\times\overrightarrow{H}_Rcos^2wt+\overrightarrow{E}_I\times\overrightarrow{H}_Isin^2wt+(\overrightarrow{E}_I\times\overrightarrow{H}_R+\overrightarrow{E}_R\times\overrightarrow{H}_I)sinwtcoswt
$$
**在2$\pi$的时间内时域波印廷矢量的平均值**
$$
<\overrightarrow{S}(\overrightarrow{r},t)>=\frac{1}{2\pi}\int_0^{2\pi}d(wt)\overrightarrow{S}(\overrightarrow{r},t)=\frac{1}{2}[\overrightarrow{E}_R\times\overrightarrow{H}_R+\overrightarrow{E}_I\times\overrightarrow{H}_I]=\frac{1}{2}Re{\overrightarrow{S}(\overrightarrow{r})}
$$
-----------------------
> 计算时域能量可以用频域公式去除积分，化简运算
--------------------------
## Conducting media介质中的波
在导电介质中，根据欧姆定律
$$
\overrightarrow{J}_c=\sigma\overrightarrow{E}
$$
> $\overrightarrow{J}_c$为欧姆电流,$\overrightarrow{J}_f$为传导电流

由
$$
\nabla\times\overrightarrow{H}=-iw\overrightarrow{D}+\overrightarrow{J}_c+\overrightarrow{J}_f
$$
$$
\nabla\times\overrightarrow{H}=-iw[\varepsilon+\frac{i}{w}\sigma]\overrightarrow{E}+\overrightarrow{J}_f
$$
令
$$
\varepsilon_c=\varepsilon+\frac{i}{w}\sigma
$$
当没有自由电流时得
$$
(\nabla^2+w^2\mu\varepsilon_c)\overrightarrow{E}=0
$$
取电场只有x方向最简单的解$\overrightarrow{E}=\hat{x}\overrightarrow{E}=\hat{x}\overrightarrow{E}_0e^{ikz}$
$$
k^2=w^2\mu\varepsilon_c=w^2\mu(\varepsilon+\frac{i}{w}\sigma)
$$
解得
$$
k=w\sqrt{\mu\varepsilon}(\varepsilon+\frac{i}{w}\sigma)^{\frac{1}{2}}=k_R+ik_I
$$
频域电场强度
$$
\overrightarrow{E}=\hat{x}E_0e^{-k_Iz+ik_Rz}
$$
转化为时域
$$
\overrightarrow{E}=\hat{x}E_0e^{-k_Iz}cos(k_Rz-wt)
$$

> 可以看出波沿传导方向指数衰减
$$
k_I=w\sqrt{\mu_0\epsilon}[1/2(\sqrt{1+\frac{\sigma^2}{\epsilon^2w^2}}-1)]^{1/2}
$$

定义穿透深度
$$
d_p=\frac{1}{k_I}
$$
> 当波衰减为0时刻的1/e

![](https://cdn.jsdelivr.net/gh/Fazziekey/image-bed/img/20200619163522.png)

根据频率，介质特性分两种情况，系数定义为损耗正切
+ $1<<\frac{\sigma}{w\varepsilon}$ 一般取0.1
    + 导电能力弱
    + 穿透深度大
$$
k=k_R+ik_I=w\sqrt{\mu\varepsilon}(i\frac{\sigma}{w\epsilon})^{\frac{1}{2}}=\sqrt{\frac{w\mu\sigma}{2}}(1+i)
$$
$$
d_p=\sqrt{\frac{2}{w\mu\sigma}}
$$
+ $1>>\frac{\sigma}{w\epsilon}$ 一般取10
    + 导电能力强
    + 穿透深度小
$$
k=k_R+ik_I=w\sqrt{\mu\varepsilon}(\varepsilon+i\frac{\sigma}{2w\varepsilon})=w\sqrt{\mu\varepsilon}+i\frac{\sigma}{2}(\frac{\mu}{\varepsilon})^{\frac{1}{2}}
$$
$$
d_p=\frac{2}{\sigma}(\frac{\varepsilon}{\mu})^{\frac{1}{2}}
$$
---------------------
### Plasme Media中的波

等离子体介质由自由电子和正离子构成，存在极化电场$\overrightarrow{P}$
，因为离子体电子速度v远小于光速c
$$
f=q(\overrightarrow{E}+\overrightarrow{v}\times\overrightarrow{B})\approx q\overrightarrow{E}=-mw^2\overrightarrow{r}
$$
$$
\overrightarrow{P}=Nq\overrightarrow{r}=-\frac{Nq^2}{mw^2}\overrightarrow{E}
$$
$$
\nabla\times\overrightarrow{H}=-iw\overrightarrow{D}=-iw(\epsilon\overrightarrow{E}+\overrightarrow{P})=-iw\epsilon(1-\frac{Nq^2}{mw^2})\overrightarrow{E}
$$
定义
$$
\epsilon_p(w)=\epsilon_0[1-\frac{w_p^2}{w^2}]
$$
$$
w_p=\sqrt{\frac{Nq^2}{m\epsilon_0}}\approx 56.4\sqrt{N}
$$
得到亥姆霍兹方程
$$
(\nabla^2+w^2\mu\varepsilon_p)\overrightarrow{E}=0
$$
$$
k^2=w^2\mu\varepsilon_p=w^2\mu_0\varepsilon_0(1-\frac{w_p^2}{w^2})
$$
根据$w_p$的大小，有两种解
+ $w>w_p$
$$
\begin{cases} k=\frac{w}{c}\sqrt{1-\frac{w_p^2}{w^2}}\\
\overrightarrow{E}=\hat{x}E_0e^{ikz}\\
\overrightarrow{H}=\hat{y}\frac{k}{w\mu}E_0e^{ikz}\\
\overrightarrow{S}=\hat{z}\frac{k}{w\mu}|E_0|^2\\
<\overrightarrow{S}>=\hat{z}\frac{k}{2w\mu}|E_0|^2
\end{cases}
$$
+  $w<w_p$
$$
\begin{cases} k=i\frac{w}{c}\sqrt{\frac{w_p^2}{w^2}-1}\\
\overrightarrow{E}=\hat{x}E_0e^{-k_Iz}\\
\overrightarrow{H}=\hat{y}\frac{ik_I}{w\mu}E_0e^{k_Iz}\\
\overrightarrow{S}=\hat{z}\frac{-ik_I}{w\mu}|E_0|^2e^{-k_Iz}\\
<\overrightarrow{S}>=0
\end{cases}
$$
> 按指数衰减而不传播时间平均功率的波称为倏逝波。在全反射章节中会再次出现，全反射时的透射波也是倏逝波，不传播能量

### phase and group velocities相速度和群速度
$$
k(w)=\frac{w}{c}\sqrt{1-\frac{w_p^2}{w^2}}
$$
当$w>w_p$
令$w_1=w_0+\delta w$,$w_2=w_0-\delta w$
$$
\overrightarrow{E}_x(z,t)=cos(k_1z-w_1t)+cos(k_2z-w_2t)=2cos(k_0z-w_0t)cos(\delta kz-\delta wt)
$$
![](https://cdn.jsdelivr.net/gh/Fazziekey/image-bed/img/20200619163523.png)
> 两个波线性叠加，形成驻波

**定义**
> phase velocity=w/k

> group velocity=$\frac{1}{\partial k/\partial  w}$

则$v_p=\frac{w}{k}=\frac{c}{\sqrt{1-w_p^2/w^2}}>c$

$v_g=\frac{1}{\partial k/\partial  w}=c\sqrt{1-w_p^2/w^2}<c$

$v_gv_p=c^2$

> 相速度可以理解为简谐波在传播的过程中固定相位的点沿着波传播方向上的速度，例如，波峰的传播速度或者波谷的传播速度，也就是波长除以周期。这个概念比较好形象的解释。群速度可以解释为振幅值的变化的传播速度（对于简谐振动，我们可以理解为群速度不存在。因为不存在振幅值的变化，更别提这个变化的传播了。所以群速度都是针对非简谐振动而言的。对于折射系数大于1的介质，相速度大于群速度，对于折射系数小于1的介质，相速度小于群速度（反常介质，不存在）

-------------
### Dispersive Media
$$
q\overrightarrow{E}=m(\frac{d^2\overrightarrow{r}}{dt^2}+\gamma\frac{d\overrightarrow{r}}{dt}+w_0^2\overrightarrow{r})
$$
$$
\overrightarrow{P}=Nq\overrightarrow{r}=-\frac{Nq^2}{m(w^2-w_0^2+iw\gamma)}\overrightarrow{E}
$$
亥姆霍兹方程
$$
(\nabla^2+w^2\mu\varepsilon_d)\overrightarrow{E}=0
$$
$$
\epsilon_d(w)=\epsilon_0[1-\frac{w_p^2}{w^2-w_0^2+iw\gamma}]
$$
$$
w_p=\sqrt{\frac{Nq^2}{m\epsilon_0}}\approx 56.4\sqrt{N}
$$
化简得
$$
\epsilon_d(w)=\epsilon_R+i\epsilon_I=\epsilon_0[1-\frac{(w^2-w_0^2)w_p^2}{(w^2-w_0^2)^2+(w\gamma)^2}]+i\frac{w\gamma w_p^2}{(w^2-w_0^2)^2+(w\gamma)^2}
$$
![](https://cdn.jsdelivr.net/gh/Fazziekey/image-bed/img/20200619163525.png)
