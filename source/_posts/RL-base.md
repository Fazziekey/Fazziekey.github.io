---
title: 强化学习基础和马尔科夫决策过程
toc: true
copyright: true
date: 2020-11-23 19:13:01
tags:
    - RL
categories:
    - 《炼金术士修炼手册》
reward:
---
# 强化学习基本过程

![](https://cdn.jsdelivr.net/gh/Fazziekey/image-bed@master/2020/10/26/50ca94f0a4326ee91f2dd480a8019e8e.png)

<!--more-->
## 强化学习基本要素
+ 模型
+ 政策
+ 价值

## 深度学习不同点
+ 没有标签，只有反馈
+ 学习的过程来自于试错
+ 学习的反馈有延迟
+ 动作会影响数据
+ 观察数据有时间的关联


# 马尔科夫基本过程（MDP）
马尔科夫过程的下一状态只取决于当前状态

## 马尔科夫奖励过程
+ S：state
+ R: Reward,$R(s_t=s)$
+ Discount factor $\gamma\in [0,1]$
+ P:dynamics/transition model 


### Horizon
+ Number of maximum time steps in each episode
+ Can be infinite,otherwise called finite Markov (reward) Process

### Return
$$
G_t=R_{t+1}+\gamma R_{t+2}+\gamma^2R_{t+3}...\gamma^{T-t-1}R_T
$$
> 可以看出随着时间变化，奖励值会衰减，只有离开某个状态才能获得奖励，所以奖励来自于未来的状态

### state value function Vt(s) for a MRP
#### Expected
$$
V_t(s)=E[G_t|s_t=s]
\\
=E[R_{t+1}+\gamma R_{t+2}+\gamma^2R_{t+3}...\gamma^{T-t-1}R_T|s_t=s]
$$

### Discount Factor $\gamma$
可以作为强化学习的超参数调整

+ 当$\gamma=0$，奖励只取决于当前状态

## Bellman equation
Bellman方程描述了状态的迭代关系
$$
V(s)=R(s)+\gamma\sum_{s'\in S}P(s'|s)V(s')
$$
也可以写为矩阵的形式
![](https://cdn.jsdelivr.net/gh/Fazziekey/image-bed@master/2020/10/26/59d7a52b2f3c05290c0959d8c6aa3c77.png)
我们可以通过矩阵求逆的过程求出V
$$
V=R+\gamma PV
\\
\to V=(1-\gamma P)^{-1}R
$$
矩阵求逆的计算量太大，所以我们一般用迭代的方法求解
+ 动态规划法
+ 蒙特卡洛采样法
+ Temporal-Difference learning

### 蒙特卡洛法
![](https://cdn.jsdelivr.net/gh/Fazziekey/image-bed@master/2020/10/26/a55f81b89fcd2007ad93eddc865932e2.png)

### 动态规划
![](https://cdn.jsdelivr.net/gh/Fazziekey/image-bed@master/2020/10/26/786e9d90dfae4df9e7f9d18318a693c5.png)

## 马尔科夫决策过程
增加了一个动作
+ S：state
+ A: action
+ R: Reward,$R(s_t=s)$
+ Discount factor $\gamma\in [0,1]$
+ P:dynamics/transition model $P(s_{t+1}=s'|s_t=s,a_t=a$

### Policy
+ policy决定了当前采取的策略
+ Policy：$\pi(a|s)=P(a_t=a|a_t=s)$
+ Policies are stationary (time-independent)，$A_t～ \pi(a|s)$ for any t > 0


+ Given an MDP $(S,A, P,R,\gamma)$ and a policy $\pi$
+ The state sequence S1, S2,... is a Markov process $(S, P^\pi)$
+ The state and reward sequence S1,R2,S2, R2,... is a Markov reward
process (S, PT,R", ) where,

$$
P^{\pi}\left(s^{\prime} \mid s\right)=\sum_{a \in A} \pi(a \mid s) P\left(s^{\prime} \mid s, a\right)
\\
R^{\pi}(s)=\sum_{a \in A} \pi(a \mid s) R(s, a)
$$
> 当policy$\pi$已知时，马尔科夫决策过程会转化为马尔科夫奖励过程

![](https://cdn.jsdelivr.net/gh/Fazziekey/image-bed@master/2020/10/27/35e02eaa2e13b99ebf06d7482e031e6b.png)
马尔科夫决策过程的下一状态先由当前状态采取的决策决定

### State Value Function

$$
{v}^{\pi}(s)=\mathbb{E}_{\pi}\left[G_{t} \mid s_{t}=s\right]
$$
#### action-value function 

$$
q^{\pi}(s, a)=\mathbb{E}_{\pi}\left[G_{t} \mid s_{t}=s, A_{t}=a\right]
$$

#### 状态价值函数和动作价值函数的关系

$$
v^{\pi}(s)=\sum_{a \in A} \pi(a \mid s) q^{\pi}(s, a)
$$
### Bellman Equation

$$
v^{\pi}(s)=E_{\pi}\left[R_{t+1}+\gamma v^{\pi}\left(s_{t+1}\right) \mid s_{t}=s\right]
\\
=\sum_{a \in A} \pi(a \mid s) q^{\pi}(s, a)
\\
=\sum_{a \in A} \pi(a \mid s)\left(R(s, a)+\gamma \sum_{s^{\prime} \in S} P\left(s^{\prime} \mid s, a\right) v^{\pi}\left(s^{\prime}\right)\right)
$$

---
$$
q^{\pi}(s, a)=E_{\pi}\left[R_{t+1}+\gamma q^{\pi}\left(s_{t+1}, A_{t+1}\right) \mid s_{t}=s, A_{t}=a\right]
\\
=R_{s}^{a}+\gamma \sum_{s^{\prime} \in S} P\left(s^{\prime} \mid s, a\right) v^{\pi}\left(s^{\prime}\right)
\\
=R(s, a)+\gamma \sum_{s^{\prime} \in S} P\left(s^{\prime} \mid s, a\right) \sum_{a^{\prime} \in A} \pi\left(a^{\prime} \mid s^{\prime}\right) q^{\pi}\left(s^{\prime}, a^{\prime}\right)
$$

> $v^\pi$表示了采用policy$\pi$得到奖励的期望

## 马尔科夫决策过程的预测和控制
+ 预测
    + 预测价值 
+ 控制
    + 寻找最佳策略 

### predition
尝试所有策略，收敛后得到价值函数
![](https://cdn.jsdelivr.net/gh/Fazziekey/image-bed@master/2020/10/27/99bf59fcb81437835eb58274c0722285.png)

### optimal value function and policy


$$
v^*(s)=max_\pi v^\pi(s)
\\
\pi^* (s)=arg max_\pi v^\pi (s)
$$
**如何寻找最佳的policy?**
最佳行为可以定义为

$$
\pi^{*}(a \mid s)=\left\{\begin{array}{ll}
1, & \text { if } a=\arg \max _{a \in A} q^{*}(s, a) \\
0, & \text { otherwise }
\end{array}\right.
$$

### policy search
策略搜索的方法主要有以下两种
#### policy iteration
策略迭代算法有两个步骤
+ 估计当前政策价值函数
+ 采用贪心算法改进策略

$$
\pi'=greedy(v^\pi)
$$
![](https://cdn.jsdelivr.net/gh/Fazziekey/image-bed@master/2020/10/27/d62fb722c177cdcefdd042d6e18329ee.png)

##### policy improvwment
+ 计算当前策略价值
$$
q^{\pi_{i}}(s, a)=R(s, a)+\gamma \sum_{s^{\prime} \in S} P\left(s^{\prime} \mid s, a\right) v^{\pi_{i}}\left(s^{\prime}\right)
$$
+ 计算新政策价值
$$
\pi_{i+1}(s)=\underset{a}{\arg \max } q^{\pi_{i}}(s, a)
$$
![](https://cdn.jsdelivr.net/gh/Fazziekey/image-bed@master/2020/10/27/5ec4e37080c6df000eed9aef386056a0.png)

$$
q^{\pi}(s,\pi'(s))=\max_{a\in A}q^\pi(s,a)
$$
#### value iteration

$$
v(s)=\max_{a\in A}(R(s, a)+\gamma \sum_{s^{\prime} \in S}
P\left(s^{\prime} \mid s, a\right) v\left(s^{\prime}\right))
$$
![](https://cdn.jsdelivr.net/gh/Fazziekey/image-bed@master/2020/10/27/d9028f7e8b382d4b3b0e56c32f302801.png)