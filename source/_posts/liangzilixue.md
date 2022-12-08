---
title: 量子力学
toc: true
copyright: true
date: 2021-02-23 23:55:07
tags:
    - physical
    - 学废了
categories:
    - 《行于黑暗，侍奉光明，我们是电工》
reward:
---
不要尝试去理解量子力学！！！
---

# 量子力学原理
## 能量子
+ 普朗克常数
$$
h=6.626\times 10^{-34}J\cdot s
$$

### 黑体辐射
#### 斯特藩-玻尔兹曼定律
总辐出度与温度的四次方成正比
$$
M(T)=\sigma T^4
$$
#### 韦恩位移定律
黑体辐射光谱的峰值频率与黑体温度成正比:
$$
v=CT
$$
## 波粒二象性
### 散射增强条件
$$
d\sin\theta=n\lambda
$$

## 测不准原理
+ 动量测不准
$$
\Delta p\Delta x>=\hat{h}/2
$$
+ 能量时间测不准
$$
\Delta E\Delta t>=\hat{h}/2
$$
+ 角动量测不准
$$
\Delta P\Delta \varphi>=\hat{h}/2
$$

没有人比我更懂量子力学。
----

# 薛定谔波动方程
$$
\frac{-\hbar^2}{2m}\nabla^2\Psi(x,t)+U(x)\Psi(x,t)=j\hat{h}\frac{\partial\Psi(x,t)}{\partial t}
$$
## 一维非相对论薛定谔方程
$$
\frac{-\hbar^2}{2m}\frac{\partial^2\Psi(x,t)}{\partial x^2}+U(x)\Psi(x,t)=j\hat{h}\frac{\partial\Psi(x,t)}{\partial t}
$$

对波函数进行变量分离
$$
\Psi(r,t)=\psi(r)\varphi(t)
$$

### 时间部分为正弦波形式
$$
\varphi(t)=exp(-j\frac{E}{\hbar   }t)=exp(-jwt)
$$
$$
E=\hbar w
$$

## 定态薛定谔方程（与时间无关）
$$
\frac{d\psi(x)}{dx^2}+\frac{2m}{\hbar^2}[E-U(x)]\psi(x)=0
$$
> 概率密度函数表示在给定时间和位置出现粒子的概率

### 波函数
$$
\Psi(r,t)=\psi(r)\varphi(t)=\psi(r)exp(-jwt)
$$
### 粒子在某时刻某位置出现的概率
$$
\Psi^2=\psi^2
$$
> 粒子的几率密度只与位置有关，与时间无关

## 边界条件
$$
\iiint_{-\infty}^{\infty}\Psi(r,t)\Psi^*(r,t)dxdydz=\iiint_{-\infty}^{\infty}|\psi(r,t)|^2dxdydz=1
$$
### 几率密度
+ $\psi(r)$有限、单值、连续

### 动量
+ $\nabla\psi(r)$有限、单值、连续
### 能量
+ $\nabla^2\psi(r)$有限

> 各种势场的薛定谔方程的参数往往由边界条件待定


# 薛定谔方程实例
## 自由空间中电子
当$U(x)=0$

$$
\frac{d\psi(x)}{dx^2}+\frac{2m}{\hbar^2}E\psi(x)=0
$$
### 波函数解为
$$
\psi(x)=Aexp[\frac{j}{\hbar}x\sqrt{2mE}]+Bexp[-\frac{j}{\hbar}x\sqrt{2mE}]
$$
$$
\varphi(t)=exp(-j\frac{E}{\hbar}t)=exp(-jwt)
$$
$$
\Psi(x,t)=Aexp[\frac{j}{\hbar}(x\sqrt{2mE}-Et)]+Bexp[-frac{j}{\hbar}(x\sqrt{2mE}+Et)]
$$
+ 圆频率
$$
w=E/\hbar
$$
+ 波数
$$
k=\sqrt{2mE}/\hbar
$$
+ 波长
$$
\lambda=h/\sqrt{2mE}
$$
+ 动量
$$
p=h/\lambda=\sqrt{2mE}=\hbar k
$$

$$
\Psi(x,t)\approx 2\cos\{0.5[(dk)x-(dw)t]\}\sin(kx-wt)
$$
![](https://cdn.jsdelivr.net/gh/Fazziekey/image-bed@master/2020/10/04/0ed88ae8c24060d6a50b85ce3901aa6f.png)

## 无限深势井

当$U(x)_1=0$,$U(x)_2=\infty$
![](https://cdn.jsdelivr.net/gh/Fazziekey/image-bed@master/2020/10/04/8152ce57263865160e057bf7c3f534d0.png)
### 区2
+ 薛定谔方程
$$
\frac{d\psi(x)}{dx^2}+\frac{2m}{\hbar^2}E\psi(x)=0
$$

+ 波数
$$
k=\sqrt{2mE}/\hbar
$$
+ 波函数
$$
\psi(x)=A_1\cos(kx)+A_2\sin(kx)
$$
### 区13
$$
\psi(x)=0
$$

根据边界条件
解得
$$
A_1=0
$$
$$
A_2=\sqrt{2/a}
$$
$$
k=n\pi/a=\sqrt{2mE}/\hbar
$$
+ 分立能级
$$
E_n=\frac{\hbar^2\pi^2}{2ma^2}n^2
$$
![](https://cdn.jsdelivr.net/gh/Fazziekey/image-bed@master/2020/10/05/b4ca1e6285cbbfda8fc5a193e952be46.png)

## 阶跃位函数
![](https://cdn.jsdelivr.net/gh/Fazziekey/image-bed@master/2020/10/05/aba080a1c40a69686a8f388c4205d70a.png)
### 区1
$$
\psi(x)=A_1exp(jk_1x)+B_1exp(-jk_1x)
$$
$$
k_1=\sqrt{\frac{2mE}{\hat{h}^2}}
$$

### 区2
$$
\psi(x)=A_2\exp(-k_2x)+B_2exp(k_2x)
$$
$$
k_2=\sqrt{\frac{2m(U_0-E)}{\hat{h}^2}}
$$

$$
B_2=0
$$
根据边界条件 解得
$$
B_1=\frac{k_2+jk_1}{jk_1-k_2}A_1
$$
$$
A_2=\frac{2jk_1}{jk_1-k_2}A_1
$$

反射率R=1

> 粒子有一定几率可以穿越II区，但最终都会掉头返回

# 势垒
+ 区1
$$
\psi_1=A_1exp(jk_1x)+B_1exp(-jk_1x)\\
k_1=\sqrt{2mE}/\hbar
$$
+ 区2
$$
\psi_2=A_2exp(jk_2x)+B_2exp(-jk_2x)\\
k_2=\sqrt{2m(U_0-E)}/\hbar
$$
+ 区3
$$
\psi_3=A_3exp(jk_3x)+B_3exp(-jk_3x)\\
k_3=\sqrt{2mE}/\hbar
$$
![image](C00878AC16F24FABA530D72BEC2DF953)
+ 透射率
$$
T\approx16(\frac{E}{U_0})(1-\frac{E}{U_0})exp(-2k_2a)
$$
+ 反射率
$$
R=1-T
$$
> 低能量粒子能渗入
或贯穿高能势垒

# 原子的波动理论
## 单电子原子
### 质子和电子产生的位函数
$$
U(r)=\frac{-e^2}{4\pi \epsilon_0r}
$$

### 电子的能量
将势函数代入薛定谔方程，并转化为球坐标下进行求解，分离变量可以得到电子的能量
$$
E_n=\frac{-m_0e^4}{(4\pi\epsilon_0)^22\hbar^2n^2}=-13.6eV
$$
+ 电子质量
$$
9.1 \times 10^{-31}
$$
+ 电子电荷量
$$
1.6 \times 10^{-19}
$$

#### 电子的量子数
+ n 主量子数
n=1,2,3...
+ l 角量子数
l=n-1,n-2...0
+ m 磁量子数
|m|=l,l-1...0
+ s自旋量子数
s=1/2
$$
L=\sqrt{l(l+1)}\hbar
\\
L_z=m\hbar
\\
S=\sqrt{s(s+1)}\hbar=\sqrt{3}\hbar /2
$$


