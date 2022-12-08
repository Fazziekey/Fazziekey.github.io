---
title: com base
toc: true
copyright: true
date: 2020-08-15 15:02:44
tags:
    - communication
categories:
    - 《行于黑暗，侍奉光明，我们是电工》
reward:
---

最近科研碰上大量通讯相关的背景，因此对通讯的一些基本背景知识做简单整理

<!--more-->

## 词汇&简称
+ UE：user equipment
+ BS: base station
+ Tx: transmitter beam
+ Rx: receive beam
+ DFT:离散傅里叶变换
+ LOS:视距
+ NLOS:非视距
+ scattering:散射分量
+ constant：直射分量 
+ AOA：接收角
+ AOD：发射角

## SNR:Signal-to-noise,信噪比
**公式**
$$
SNR=\frac{Signal Power}{Noise Power}=\frac{E[|x(t)|^2]}{E[|v(t)|^2]}=\frac{E_s}{N_0}
$$
$$
SNR_{db}=10log_{10}SNR
$$
## 香农公式
香农公式定义了再高斯白噪声的信道中，信息传输的最大速率
$$
C=W\log_2(1+S/N)
$$
$$
S/N=SNR_{db}
$$

## 信号离散傅里叶变化
$$
\sqrt{(1/N_T)}*e^{(-i2\pi(-1/2+(slot_{ind}-1)/N_T)*[0:N_T-1]^T)}
$$

![](https://cdn.jsdelivr.net/gh/Fazziekey/image-bed@master/2020/08/15/6b7a4e44022c8563e56d40530707232f.png)

## 信道类型：channel type
### los：视距

$$
K_{fdB} = 13.2; % Rician K factor
$$
$$
K_f = 10^{(K_{fdB}/10)}
$$
$$
NumPath = 1
$$
$$
\gamma_k = rand(NumPath)^2\times 10^{-0.2randn(NumPath)}
$$
$$
\gamma_k = \gamma_k/\sum(\gamma_k)
$$
$$
power_{const} = \frac{K_f}{K_f+1}
$$
$$
power_{scatter} = \frac{1}{K_f+1}
$$
$$
g_{constant} = \sqrt{\gamma_k*power_{const}}
$$
$$
g_{scattering} = \sqrt{\gamma_k*power_{scatter}}
$$

### Nlos：非视距

$$
K_{fdB} = 6; % Rician K factor
$$
$$
K_f = 10^{(K_{fdB}/10)}
$$
$$
NumPath = 1.8
$$
$$
\gamma_k = rand(NumPath)^2\times 10^{-0.2randn(NumPath)}
$$
$$
\gamma_k = \gamma_k/\sum(\gamma_k)
$$
$$
power_{const} = \frac{K_f}{K_f+1}
$$
$$
power_{scatter} = \frac{1}{K_f+1}
$$
$$
g_{constant} = \sqrt{\gamma_k*power_{const}}
$$
$$
g_{scattering} = \sqrt{\gamma_k*power_{scatter}}
$$

## 信道矩阵


$$
v = e^{-i2\pi k \sin(AOD)}
$$
$$
u = e^{-i2\pi k \sin(AOA)}
$$
$$       
H = H+g_{constant}uv+ \frac{g_{scattering}}{\sqrt{2}}N+i*N;
$$
$$
N\to N(0,\sigma^2)
$$
## 信道衰减模型
### 什么是信道衰落

对于S—D这样一个发送接收系统来说，理想的无线信号传播（自由空间传播模型）是由S发送的电磁信号经过一定的衰减（attenuation）到达D点，我们可以理解为信号沿着S—D的直线。虽然这样，电磁波实际上是以球面波的形式向周围360度辐射，但其是只有沿着S—D直线传播的信号才能抵达D点，我们也可以把S—D路径称为直射路径。这是对于自由空间来说的，在自由空间模型里面除了S和D什么也没有。

而对于实际的大气传播环境，大气中包含着许多的小颗粒（悬浮物），或者小粒子。从S出发，沿着非S—D方向的其它传播方向的额电磁波可能经过一系列的反射（散射）后而抵达接收端D，我们把这种路径称为散射路径。由于每一条散射路径经历的路程都不一样，这样，他们抵达接收端的相位各不相同，导致总的信号强度变低。这样我们把由于信号经过了多个路径而抵达接收端导致信号强度发生随机变化的现象称为衰落（fading）。

### 瑞利衰落信道模型 （Rayleigh）

假设发送信号为单一频率正弦波，即
$$
s(t)=A\cos w_c t
$$


若不考虑直射路径，多径信道共有n条路径，各条路径具有时变衰耗和时变传输时延，且从各条路径到达接收端的信号相互独立，则接收端接受到的合成波为
$$
r(t)=a_1\cos w_c[t-\tau_1(t)]+a_2\cos w_c[t-\tau_2(t)]+a_3\cos w_c[t-\tau_3(t)]……a_n\cos w_c[t-\tau_n(t)]
$$
$$
=\sum_{i=1}^{n}a_i\cos w_c[t-\tau_i(t)]
$$

r(t)也可表示为如下形式：
$$
r(t)
=\sum_{i=1}^{n}a_i\cos\phi_i\cos- \sum_{i=1}^{n}a_i\sin\phi_i\sin
$$
$$
=X(t)\cos w_ct-Y(t)\sin w_ct
$$

由于X(t)和Y(t)都是相互独立的随机变量之后，根据中心极限定理，大量独立随机变量之和的分布趋于正态分布。因此，当n足够大时，X(t)和Y(t)都趋于正态分布。通常情况下X(t)和Y(t)的均值为0（由于没有直射路径），方差相等。这种表示方式也叫做同相-正交表示法。


**由于包络服从瑞利分布，故其称为瑞利信道模型。**

对于陆地移动信道、短波电离层反射等随参信道，其路径幅度ai(t)和相位函数φi(t)随时间变化与发射信号载波频率相比要缓慢得多。因此，相对于载波来说V(t)和φ(t)是慢变化随机过程，于是r(t)可以看成是一个窄带随机过程。由此得出以下两个结论：

1. 多径传播使单一的正弦信号变成了包络和相位受调制的窄带信号，这种信号称为衰落信号，即多径传播使信号产生瑞利型衰落（多径衰落）。

2.从频谱上看，多径传播使单一谱线变成了窄带频谱，即多径传播引起了频率弥散。



### 莱斯衰落信道模型（Rician）
莱斯信道是当移动台与基站间存在直射波信号时，即有一条主路径，通过主路径传输过来被接收的信号为一个稳定幅度$Ak$和相位$\phi _k$，其余多径传输过来的信号仍如“瑞利衰落概率模型”所述。


当信道中存在一个固定的直射分量时，X(t)与Y(t)的均值不再为0。其接收信号是复高斯信号和直射分量的叠加（即正弦波加窄带高斯过程），其包络的概率密度函数服从莱斯分布，即下式
$$
f(z)=\frac{z}{\sigma_n^2}exp[-\frac{1}{2\sigma^2_n}(z^2+A^2)]I_0(\frac{A_z}{\sigma^2_n}),z>0
$$
#### 莱斯衰弱信道模型matlab仿真程序

    %% 参数设置
    Modulation_Order=2;
    Packet_Length=16;
    SymbolRate=1000;
    SamplesPerSymbol=8;%每个符号的样点数
    df=400;%FSK调制相邻载波频率间隔，单位Hz
    fs=SamplesPerSymbol*SymbolRate;
    SNR=10;
    ts=1/fs;
    fd=0;
    k=3;
    tau=[0 1 2]*ts;%每条径的时延
    pdb=[2 1 0];%每条径的增益
    
    %% 调制器、解调器、莱斯信道设置
    H_Mod = comm.FSKModulator('ModulationOrder',Modulation_Order,'SymbolRate',1000 ,'SamplesPerSymbol',8, 'FrequencySeparation',df); %默认连续相位、整数输入 
    H_Demod = comm.FSKDemodulator('ModulationOrder',Modulation_Order,'SymbolRate',1000 ,'SamplesPerSymbol',8, 'FrequencySeparation',df);
    chan_Rici = ricianchan(ts,fd,k,tau,pdb);


### Nakagami-m信道衰落模型

瑞利和莱斯分布与实验数据有时不太吻合，因此人们提出了能吻合更多实验数据的一种更通用的信道衰落分布，就是Nakagami-m衰落，


