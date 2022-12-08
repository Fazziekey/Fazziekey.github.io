---
title: Radiation
date: 2020-06-21 13:15:55
copyright: true
tags:
    - 手撕麦克斯韦
categories: 
    - 《行于黑暗，侍奉光明，我们是电工》
---

# 5.2 Green's Functions格林函数
本章将考虑在有源情况下的麦克斯韦方程，先写出频域有源情况下的麦克斯韦方程
## Dyadic Green's Functions
<!--more-->
$$
\begin{cases} \nabla\times\overrightarrow{E}=iw\overrightarrow{B}\\
\nabla\times\overrightarrow{H}=-iw\overrightarrow{D}+\overrightarrow{J}\\
\nabla\cdot\overrightarrow{B}=0\\
\nabla\cdot\overrightarrow{D}=\rho
\end{cases}
$$

得到
$$
\nabla \times \nabla\times\bar E-k^2\bar E=iw\mu\bar J
$$
为了解出这个方程，我们引入格林函数

$$
\bar E(\bar r)=iw\mu\iiint d\bar r^{'}\bar G(\bar r,\bar r^{'})\cdot\bar J(\bar r^{'})
$$
> 在数学中，格林函数是一种用来解有初始条件或边界条件的非齐次微分方程的函数。在物理学的多体理论中，格林函数常常指各种关联函数，有时并不符合数学上的定义。

> 从物理上看，一个数学物理方程是表示一种特定的"场"和产生这种场的"源"之间的关系。例如，热传导方程表示温度场和热源之间的关系，泊松方程表示静电场和电荷分布的关系，等等。这样，当源被分解成很多点源的叠加时，如果能设法知道点源产生的场，利用叠加原理，我们可以求出同样边界条件下任意源的场，这种求解数学物理方程的方法就叫格林函数法。而点源产生的场就叫做格林函数。

 [**格林函数的物理意义是什么——知乎**](
https://www.zhihu.com/question/58746631/answer/170741359)

其中电流J存在关系
$$
\bar J(\bar r)=\iiint d\bar r^{'}\delta(\bar r-\bar r^{'})\bar I\cdot\bar J(\bar r^{'})
$$
化简得
$$
\nabla \times \nabla\times\bar G(\bar r,\bar r^{'})-k^2\bar G(\bar r,\bar r^{'})=\delta(\bar r-\bar r^{'})\bar I
$$
令
$$
\bar G(\bar r,\bar r^{'})=[\bar I+\frac{1}{k^2}\nabla\nabla] g(\bar r,\bar r^{'})
$$
代入化简
$$
\nabla^2g(\bar r,\bar r^{'})+k^2g(\bar r,\bar r^{'})=-\delta(\bar r-\bar r^{'})
$$
当r'=0,即电流不随位置变化
$$
\nabla^2g(\bar r)+k^2g(\bar r)=-\delta(\bar r)
$$
得到
$$
g(r)=C\frac{e^{ikr}}{r}
$$
$$
\to g(\bar r,\bar r^{'})=\frac{e^{ik|\bar r-\bar r^{'}|}}{4\pi|\bar r-\bar r^{'}|}
$$
$$
\to \bar E(\bar r)=iw\mu[\bar I+\frac{1}{k^2}\nabla\nabla]\cdot\iiint dr'\frac{e^{ik|\bar r-\bar r^{'}|}}{4\pi|\bar r-\bar r^{'}|}\bar J(\bar r')
$$

## Radiation Field Approximation
当r离辐射源很远时可以进行近似
$$
|\bar r-\bar r'|\approx r-\hat{r}\cdot\bar r'

kr>>1
$$


$$
\bar E(\bar r)=iw\mu[\bar I+\frac{1}{k^2}\nabla\nabla]\cdot\iiint dr'\frac{e^{ik|\bar r-\bar r^{'}|}}{4\pi|\bar r-\bar r^{'}|}\bar J(\bar r')

\approx iw\mu[\bar I+\frac{1}{k^2}\nabla\nabla]\cdot\ \frac{e^{ikr}}{4\pi r}\iiint dr'\bar J(\bar r')e^{-i\bar k\cdot \bar r'}
$$

定义矢量电流矩
$$
\bar f(\theta,\phi)=\iiint d \bar r'\bar J(\bar r')e^{-i\bar k\cdot \bar r'}
$$

得到
$$
\bar E(\bar r)=iw\mu\frac{e^{ikr}}{4\pi r}(\hat{\theta}f_\theta+\hat{\phi}f_\phi)

\bar H(\bar r)=iw\mu\frac{e^{ikr}}{4\pi r}(\hat{\theta}f_\theta-\hat{\phi}f_\phi)

<\bar S>=\hat{r}\frac{1}{2}\sqrt{\frac{\mu}{\epsilon}}(\frac{k}{4\pi r})^2(|f_\theta|^2+|f_\phi|^2)
$$

# 5.3Hertzian Dipoles
## Hertzian Electric Dipole
最简单的辐射情况是赫兹天线

其电流满足

$$
\bar J(\bar r^{'})=\hat{z}Il\delta(\bar r^{'})
$$
对应电流矢量矩
$$
\bar f(\theta,\phi)=\hat{z}Il=(\hat{r}cos\theta-\hat{\theta}sin\theta)Il
$$
![image](https://note.youdao.com/yws/public/resource/d7887d3005300ddc063057fa9bf70e07/xmlnote/C20E125C2113468EBEB26E32D2926873/6259)
**电场和磁场**
$$
\bar E(\bar r)=-\hat{\theta}iw\mu Il\frac{e^{ikr}}{4\pi r}sin\theta
$$
$$
\bar H(\bar r)=-\hat{\phi}ik Il\frac{e^{ikr}}{4\pi r}sin\theta
$$
$$
<\bar S>=\hat{r}\frac{1}{2}\sqrt{\frac{\mu}{\epsilon}}(\frac{kIl}{4\pi r})^2sin^2\theta
$$
![](https://cdn.jsdelivr.net/gh/Fazziekey/image-bed/img/20200621210236.png)
**总辐射功率**
$$
P_r=\frac{4\pi}{s}\eta[\frac{kIl}{4\pi}]^2
$$
**增益**
$$
G(\theta,\phi)=\frac{3}{2}sin^2\theta
$$
天线方向被定义为最大增益处，垂直于偶极轴
$$
D=G(\theta,\phi)_{max}=\frac{3}{2}
$$

# Linear Dipole Arrays多天线阵列
![](https://cdn.jsdelivr.net/gh/Fazziekey/image-bed/img/20200621210237.png)
$$
\bar f(\theta,\phi)=\iiint d \bar r'\bar J(\bar r')e^{-i\bar k\cdot \bar r'}
$$
$$
=\iiint dx^{'}e^{-ikx^{'}}\hat{z}Il(\delta(x^{'})+\delta(x^{'}-d)e^{i\alpha}+\delta(x^{'}-2d)e^{i2\alpha}……+\delta(x^{'}-nd)e^{in\alpha})
$$
$$
=\hat{z}Il(\frac{1-e^{inu}}{1-e^{iu}})
$$
**电场和磁场**
$$
\bar E(\bar r)=-\hat{\theta}iw\mu Il\frac{e^{ikr}}{4\pi r}sin\theta(\frac{1-e^{inu}}{1-e^{iu}})
$$
$$
\bar H(\bar r)=-\hat{\phi}ik Il\frac{e^{ikr}}{4\pi r}sin\theta(\frac{1-e^{inu}}{1-e^{iu}})
$$
$$
<\bar S>=\hat{r}\frac{1}{2}\sqrt{\frac{\mu}{\epsilon}}(\frac{kIl}{4\pi r})^2sin^2\theta
$$
> 阵列因子 $\frac{1-e^{inu}}{1-e^{iu}}$

$$
|F(u)|=|\frac{1-e^{inu}}{1-e^{iu}}|=|\frac{sin(nu/2)}{sin(u/2)}|
$$
$$
u=kdcos\psi-\alpha
$$
$$
cos\psi=sin\theta cos\phi
$$
$\alpha$为相邻天线相位差
![](https://cdn.jsdelivr.net/gh/Fazziekey/image-bed/img/20200621210631.png)

$$
u_n=\frac{2n\pi}{N}  
$$
$$
n=\pm1,\pm2……
$$
![](https://cdn.jsdelivr.net/gh/Fazziekey/image-bed/img/20200621210632.png)

![](https://cdn.jsdelivr.net/gh/Fazziekey/image-bed/img/20200621210633.png)

> n决定主瓣最大强度，n为天线数量