---
title: Beam Alignment and Tracking for Millimeter Wave Communications via Bandit Learning
toc: true
copyright: true
date: 2020-10-19 19:02:08
tags:
    - 强化学习
    - Beam tracking
categories:
    - 《搬砖狗的日常》
reward:
---
# Abstract
Millimeter wave (mmwave) communications have attracted increasing attention thanks to the abundant spectrum resource. The short wave-length of mmwave signals facilitates exploiting large antenna arrays to achieve large array gains and combat the large path-loss. However, the use of large antenna arrays along with narrow beams leads to a large overhead in beam training for obtaining channel state information, especially in dynamic environments. To reduce the overhead of beam training, in this paper we formulate the problem of **beam alignment and tracking** (BA/T) as a **stochastic bandit** problem. In particular, to sense the change of the environments, the actions
are designed based on the offset of successive beam indexes，beam index difference), which measures the rate of change of the envir-onments. Then, we propose two efficient BA/T algorithms based on the stochastic bandit learning. To reveal useful insights,the performance of effective achievable rate is further analyzed for the proposed BA/T algorithms. The analytical results show that the algorithms can sense the change of the environments and adjust beam training strategies intelligently. In addition, they do not require any priori knowledge of dynamic channel modeling, and thus are applicable to a variety of complicated scenarios. Simulation results demonstrate the effectiveness and superiority of the proposed algorithms.
<!--more-->

**Index Terms— Beam alignment, beam tracking, beam training,
stochastic bandit learning, millimeter wave communication.**

简单来说，就是毫米波通信比较严重的路径损耗，在动态环境的波束对准和跟踪问题中需要新的算法，本文使用了多臂老虎机算法进行了优化

--------
# 什么是多臂老虎机？

### 问题定义

赌场的老虎机有一个绰号叫单臂强盗（single-armed bandit），因为它即使只有一只胳膊，也会把你的钱拿走。而多臂老虎机（或多臂强盗）就从这个绰号引申而来。假设你进入一个赌场，面对一排老虎机（所以有多个臂），由于不同老虎机的期望收益和期望损失不同，你采取什么老虎机选择策略来保证你的总收益最高呢？这就是经典的多臂老虎机问题。

---------

这个经典问题集中体现了在线学习及更宽泛的强化学习中一个核心的权衡问题：我们是应该探索（exploration）去尝试新的可能性，还是应该守成（exploitation），坚持目前已知的最好选择?在多臂老虎机问题中，探索意味着去玩还没玩过的老虎机，但这有可能使你花太多时间和金钱在收益不好的机器上；而守成意味着只玩目前为止给你收益最好的机器，但这又可能使你失去找到更好机器的机会。而类似抉择在日常生活中随处可见：去一个餐厅，你是不是也纠结于是点熟悉的菜品，还是点个新菜？去一个地方，是走熟知的老路还是选一条新路？而探索和守成的权衡就是在线学习的核心。

-------

如果我们考虑吧这种算法应用在通信的波束对准场景，通过环境感知来减少训练开销

# System Model
我们只考虑一个点对点的毫米波通讯系统

+ 发射端 N个天线
+ 接收端一个天线

我们构造长度为M的波束码本
$$
C={f_i=a(-1+2i/M)|i=0,1,2,...M-1}
$$
a表示响应向量
$$
a(x)=\frac{1}{N}[1,e^{j2\pi/\lambda dx},e^{j2\pi/\lambda 2dx}...e^{j2\pi/\lambda(N-1) dx}]
$$
+ λ:信号波长
+ d：天线之间的距离

由于毫米波通道的稀疏性，我们采用了扩展的SalehValenzuela几何通道模型。 给出了BS与UE之间的信道向量
$$
h=\sqrt{N/\beta}\sum_{l=1}^L\alpha_l a(\phi_l)
$$
+ $\beta$平均路损
+ L:信道数量
+ $\alpha_l$第l个信道的路径复增益
+ $\phi_l=cos\theta_l,\theta_l$为第l个信道的发射角（AoD）

**在UE处接受信号**
$$
y_i=\sqrt{P}h^Hf_is+n_i
$$
+ P：传输的功率
+ s:试点序列
+ $n_i==N(0,I)$噪声向量

 每个时隙由两个阶段组成，即波束训练和数据传输，采用有效可达速率(EAR)作为度量BA/T算法吞吐量性能的度量，定义为

$$
R_{eff}=(1-T_B/T_S)\log(1+P|h^Hf_i|^2)
$$
+ $T_B$训练时间
+ $T_S$总时间

数据吞吐量的大小和增益之间存在矛盾


# Stochastic Bandit and learning policies
随机老虎机可以定义为一个集合$\{P_a|a\in A\}$和期望$\mu_a$,A是所有可行的操作，学习者和环境进行n轮互动，在每轮互动中，学习者从$A_t\in A$中选取一个操作，环境会给予反馈$R_t\in [0,1]$,学习者的目标是最大化反馈$S_n=\sum_{t=1}^n R_t$
。 由于Sn是一个随机数量，取决于所选择的动作和抽样的奖励，在实践中，我们试图最大化它的期望。

下一个动作将会被过去的动作的时间序列和反馈决定，$S_n$的在行动$\pi$期望定义为

$$
E_n(\pi,\varXi)=E_{\pi,\varXi}(\sum_{t=1}^nR_t)
$$
在本文中我们把动作定义为集合
$$
A=K=\{1,2,...,K\}
$$
在一个n轮互动中选择动作a的次数定义为
$$
T_a(n)=\sum_{t=1}^nII\{A_t=a\}
$$
在前面讲到过随机老虎机的本质问题是探索未知选项和保留已有优质选择的矛盾，我们在这里提出两种算法$\epsilon$贪婪算法和UCB算法来平衡矛盾

# $\epsilon$greedy and UCB

## $\epsilon$greedy
$\bar{\mu}_a(t)$表示t轮后从arm a得到的平均反馈

$$
\bar{\mu}_a(t)=\frac{1}{T}\sum_{s=1}^t\{A_s=a\}R_s
$$

$\epsilon$贪婪算法由参数$\epsilon_1,\epsilon_2...$决定，首先会选择所有arm一次，然后有$1-\epsilon_t$的概率选择$A_t=arg max_a \hat{\mu}_a(t-1)$,否则随机选择选择另一个arm

+ input：action space[K] and exploration parameter $\epsilon_t$
+ initialize:choose each arm once and let t=K+1
+ repeat
    +  $A_t=argmax_a\hat{\mu}_a(t-1)$ has highest reward
    +  choose with$1-\epsilon_t$possibility and otherwise choose other arm randomly
    +  t=t+1


## UCB:upper confidence Bound

$$
UCB_a(t-1)=
\begin{cases}
\infty&if T_a(t-1)=0\\
\hat{\mu}_a(t-1)+\sqrt{\frac{c\log(t)}{T_a(t-1)}}&otherwise
\end{cases}
$$

在第t轮选择$A_t$为
$$
argmax_a UCB_a(t-1)
$$

+ input :action space $[K]=\{1,2,...K\}$
+ initialize:t=1
+ repeat
    + choose arm $A_t=argmax_aUCB_a(t-1)$
    + play arm $A_t$and receive reward $R_t$
    + update the UCB value $UCB_{A_t}(t)$
    + t=t+1



# Stochastic bandit based beam aligment and tracking algogithms

现在我们有了通信场景模型和老虎机算法的基本概念，我们问题的核心转化为了如何设计动作和反馈，在这里我们不是把每个波束定义为一个arm，而是基于两个波束之差定义


## 基于老虎机的通讯场景建模
+ 波束编码差

比如，当前波束是10，在环境缓慢变化时，下一波束可能为11

11-10=1

环境快速变化时下一波束可能是7

10-7=3


我们用（u，b）两个值来定义一个arm，u为波束差，b为扫描的波束数量，动作空间可以描述为

$$
B=\{(u_1,b_1)...(u_L,b_L)\}
$$
L为空间大小，u为了测量环境的平均变化率，b测试变化方差

若当前时刻t的波束为$f_c$,t+1时刻的波束在以下集合选取
$$
F_{u,b}=\{f_{c+u},f_{c+u+1}...f_{c+u+b-1}\}
$$

那么我们如何定义反馈，在上文通讯模型中我们定义过接受信号强度
$$
y_i=\sqrt{P}h^Hf_is+n_i
$$
平均接受功率为
$$
Y_i=|1^Ty_i|^2/L_P
$$
$L_P$为导频序列长度

 下一次时隙t1用于数据传输的光束应该是$f^i_{u，b}，i_{u,b}=argmax_i\{Y_i|f_i \in F_{u,b}\}$ 设T0表示发射一个/单位导频信号的持续时间。 对应于arm(u，b)的奖励，由$R_{u,b}$表示，定义为
 
$$
R_{u,b}=(1-bT_0/T_s)\log(1+P|h^Hf^i_{y,b}|^2)^6
$$
$bT_0$为训练波束的时间开销

所以此时我们的目标是优化时间1到n的EAR
$$
max_{F_t}E(\sum_{t=1}^nR_{eff,t})
$$
## 波束对准和跟踪算法
+ input 
    + codebook
    + action space
+ find out the initial optimal beam from code book
+ 初始化老虎机参数
+ repeat
    + choose optimal arm$(u^*,b^*)$
    + choose optimal beam$f^*$
    + transmit data with beam $f^*$
    + update bandit information of the policy

### $\epsilon$greedy
+ input 
    + codebook
    + action space with size K
+ initialize
    + $\epsilon$sequence$\{\epsilon_n\in (0,1]n>=1 \}$
    + let $T_{u_i,b_i}=0$and$\hat{\mu}_{u_i,b_i}=0(i\in K)$
+ find out an initial optimal beam from code book
+ choose each arm once,update bandit information,let n=K+1
+ repeat 
    + let$(u^*,b^*)$be the arm with highest current average reward
    + play $(u^*,b^*)$with probability $1-\epsilon_n$and playa random arm with probalility $\epsilon_n/K$
    + choose an optimal beam from $F_{u^*,b^*}$,to transmit data
    + update $T_{u^*,b^*}$,and $\hat{\mu}_{u^*,b}$
    + update counter:n=n+1


+ $T_{u,b}$为arm（u，b）被选择的次数


### UCB Based BA/T Algorithm
+ input 
    + codebook C
    + $B=\{(u_i,b_i)\}$ of size K
+ find an initial optimal beam from codebook C
+ play each arm once and update bandit information according to and n=K+1
+ repeat 
    + compute $UCB_{u_i,b_i}(n)$for each $(u_i,b_i)$and let $(u^*,b^*)=argmax_{(u_i,b_i)}UCB_{u_i,b_i}(n-1$
    + play chosen arm
    + choose $F_{u^*,b}$to transmit data
    + update $T_{u^*,b}$and$\hat{\mu}_{u,b}$
    + n=n+1



