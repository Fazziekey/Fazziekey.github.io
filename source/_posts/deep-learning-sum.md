---
title: 深度学习激活函数和优化
toc: true
copyright: true
date: 2021-03-14 15:17:33
tags:
    - Deep learning
categories:
    - 《炼金术士修炼手册》
reward:
---


# BatchNormalization的作用

神经网络在训练的时候随着网络层数的加深,激活函数的输入值的整体分布逐渐往激活函数的取值区间上下限靠近,从而导致在反向传播时低层的神经网络的梯度消失。而Batch![img](https://uploadfiles.nowcoder.com/images/20190317/311436_1552801230080_095961B16BE2B8C2E508F4A1AB257B7D)Normalization的作用是通过规范化的手段,将越来越偏的分布拉回到标准化的分布,使得激活函数的输入值落在激活函数对输入比较敏感的区域,从而使梯度变大,加快学习收敛速度,避免梯度消失的问题。


# 激活函数

## 激活函数的作用

如果不用激励函数（其实相当于激励函数是f(x) = x），在这种情况下你每一层节点的输入都是上层输出的线性函数，很容易验证，无论你神经网络有多少层，输出都是输入的线性组合，与没有隐藏层效果相当，那么网络的逼近能力就相当有限。正因为上面的原因，我们决定引入非线性函数作为激励函数，这样深层神经网络表达能力就更加强大（不再是输入的线性组合，而是几乎可以逼近任意函数）。

## 常见的激活函数

![](https://tva1.sinaimg.cn/large/007S8ZIlly1gg7yinpjnqj30u01e87af.jpg)

## 激活函数特点

- Sigmoid函数
  - 梯度消失问题：Sigmoid函数造成梯度消失的主要原因在于，一般来说输入是介于[0,1]之间，而Sigmoid的导数在[0,1]的定义域内的值域为[0.2,0.25]，那么在反向传播的过程中这个值会变得很小，越靠近输入层值越小，导致输入层的参数难以被更新。
  - 均值不为0：均值不为0产生的主要问题在于反正传播要么都往正向传播要么都往负向传播，这使得收敛变慢，但是目前一般都使用batch来进行梯度下降，可以一定程度上解决这个问题。
  - 解析式含有幂运算，计算机求解耗时。
- Tanh函数
  - 显然，tanh函数解决了0均值的问题，但是梯度消失和幂运算的问题仍然存在。
- ReLU
  - 解决部分梯度消失问题：非负区间的梯度是一个常数，可以解决一部分的梯度消失问题，但是仍然存在梯度消失问题，
  - 计算速度、收敛快，很容易理解，只需要取max就好了
  - 存在非0均值的问题，存在某些神经元可能永远不能被激活（Dead relu problem），这主要和初始化有关。
- Leaky Relu :
  - leaky relu解决了dead relu problem的问题，但是计算会慢一些，且从实际效果来说没有总是好于relu
- Maxout
  - 函数为$max(w_1x+b_1, w_2x+b_2)$，能很好地解决relu的dead问题，可以说relu是maxout的特殊形式，也就是$w_1=0, b_1=0$的情况。
  - 推荐使用


- **Dropout**



## 优化算法Optimizer

### **Batch Gradient Descent （BGD）**

全部的数据用于一次梯度下降

$\theta=\theta-\eta \cdot \nabla_{\theta} J(\theta)$



###  **Stochastic Gradient Descent (SGD)**

  一次一个数据用户更新梯度

  

### **Mini-Batch Gradient Descent （MBGD）**

  一次部分数据用于更新梯度，常取16、32、64、128、256

  

### **Momentum**

  引入了指数加权平均，$\gamma$一般取0.9

  $v_{t}=\gamma v_{t-1}+\eta \nabla_{\theta} J(\theta)$
  $\theta=\theta-v_{t}$

  加入的这一项，**可以使得梯度方向不变的维度上速度变快，梯度方向有所改变的维度上的更新速度变慢，这样就可以加快收敛并减小震荡。**



### **Nesterov Accelerated Gradient**

  $\begin{array}{l}
  v_{t}=\gamma v_{t-1}+\eta \nabla_{\theta} J\left(\theta-\gamma v_{t-1}\right) \\
  \theta=\theta-v_{t}
  \end{array}$

  用 $θ−γv_t−1$ 来近似当做参数下一步会变成的值，则在计算梯度时，**不是在当前位置，而是未来的位置上**

  

  与Momentum的对比：

  ![img](https://images2018.cnblogs.com/blog/1192699/201803/1192699-20180310224024153-1974893457.png)

  蓝色是 Momentum 的过程，会先计算当前的梯度，然后在更新后的累积梯度后会有一个大的跳跃。
  而 NAG 会先在前一步的累积梯度上(brown vector)有一个大的跳跃，然后衡量一下梯度做一下修正(red vector)，这种预期的更新可以避免我们走的太快。

  NAG 可以使 RNN 在很多任务上有更好的表现。

  

### **Adagrad （Adaptive gradient algorithm）**

  $\theta_{t+1, i}=\theta_{t, i}-\frac{\eta}{\sqrt{G_{t, i i}+\epsilon}} \cdot g_{t, i}$

  在原来的learning_rate的基础上除以之前所有梯度的平方和再开根号。$\epsilon$ 一个很小的值，防止分母为0

  **缺点**:分母会不断积累，这样学习率就会收缩并最终会变得非常小。**学习率会急剧下降。**

  

###  **Adadelta**

  $\Delta \theta_{t}=-\frac{\eta}{\sqrt{E\left[g^{2}\right]_{t}+\epsilon}} g_{t}$

  $E\left[g^{2}\right]_{t}=\gamma E\left[g^{2}\right]_{t-1}+(1-\gamma) g_{t}^{2}$

  当$\gamma=0.5$时，$E\left[g^{2}\right]_{t}=RMS[g]_t$ 梯度的均方根。即，与adagrade相比分母变成了梯度平方的均值。

  还可以将学习率 $\eta$ 换成RMS：

  $\begin{array}{l}
  \theta_{t+1}=\theta_{t}-\frac{R M S[\Delta \theta]_{t-1}}{R M S[g]_{t}} g_{t}
  \end{array}$

  

### **RMSprop**

$$
\begin{array}{l}
E\left[g^{2}\right]_{t}=0.9 E\left[g^{2}\right]_{t-1}+0.1 g_{t}^{2} \\
\theta_{t+1}=\theta_{t}-\frac{\eta}{\sqrt{E\left[g^{2}\right]_{t}+\epsilon}} g_{t}
\end{array}
$$

  引入了指数加权平均，旨在消除梯度下降中的摆动。

### **Adam：Adaptive Moment Estimation**

**相当于 RMSprop + Momentum**, 除了像 Adadelta 和 RMSprop 一样存储了过去梯度的平方 vt 的指数衰减平均值 ，也像 momentum 一样保持了过去梯度 mt 的指数衰减平均值：

$$
\begin{array}{l}
mm_{t}=\beta_{1} m_{t-1}+\left(1-\beta_{1}\right) g_{t} \\
v_{t}=\beta_{2} v_{t-1}+\left(1-\beta_{2}\right) g_{t}^{2}
\end{array}
$$

  如果 mt 和 vt 被初始化为 0 向量，那它们就会向 0 偏置，所以做了**偏差校正**，通过计算偏差校正后的 mt 和 vt 来抵消这些偏差：

$$
\hat{m}_{t}=\frac{m_{t}}{1-\beta_{1}^{t}} \\
  \begin{array}{l}
  \hat{v}_{t}=\frac{v_{t}}{1-\beta_{2}^{t}} \\
  \quad \\ 
  \theta_{t+1}=\theta_{t}-\frac{\eta}{\sqrt{\hat{v}_{t}}+\epsilon} \hat{m}_{t}
  \end{array}
$$





