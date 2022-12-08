---
title: RNN
date: 2020-07-18 16:00:31
copyright: true
tags:
    - Deep learning
    - NLP
categories: 
    - 《炼金术士修炼手册》
---

# 循环序列模型
## 为什么选择序列模型
![](http://www.ai-start.com/dl2017/images/ae2970d80a119cd341ef31c684bfac49.png)
<!--more-->
## 数学符号
+ 输入$x^{<t>}$
+ 输出$y^{<t>}$
+ 序列长度$T_x$
+ 词向量one-hot编码
![](http://www.ai-start.com/dl2017/images/8deca8a84f06466155d2d8d53d26e05d.png)

## RNN模型
### 用普通神经网络的问题
+ 输出和输入维度不对应
+ 序列前后不存在联系

### 解决，引入RNN
![](http://www.ai-start.com/dl2017/images/cb041c33b65e17600842ebf87174c4f2.png)
$$
a^{<1>}=g_1(w_{aa}a^{<0>}+w_{<ax>x^{1}}+b_a)
$$
$$
\hat{y}=g_2(w_{ya}a^{<1>}+b_y)
$$

### 更一般情况
$$
a^{<t>}=g_1(w_{aa}a^{<t-1>}+w_{<ax>x^{t}}+b_a)
$$
$$
\hat{y}=g_2(w_{ya}a^{<t>}+b_y)
$$
### 进一步化简
$$
a^{<t>}=g_1(w_{a}[a^{<t-1>},x^{t}]+b_a)
$$
$$
\hat{y}=g_2(w_{ya}a^{<t>}+b_y)
$$
### 前向传播
![](http://www.ai-start.com/dl2017/images/rnn-f.png)

### RNN常用激活函数
+ tanh
+ ReLU

## 通过时间的反向传播
### 单个单元Loss Function
$$
L^{<t>}(\hat{y}^{<t>},y^{<t>})=
-y^{<t>}log\hat{y}^{<t>}-(1-y^{<t>})log(1-\hat{y}^{<t>})
$$
### Loss function
$$
L(\hat{y}^{<t>},y^{<t>})=
\sum_{t=1}^{T_n}L^{<t>}(\hat{y}^{<t>},y^{<t>})
$$

### RNN反向传播计算
![](http://www.ai-start.com/dl2017/images/rnn_cell_backprop.png)

## 不同类型的RNN结构
![](http://www.ai-start.com/dl2017/images/329b0748f7282efc206ea8de6a709833.png)

### 多对一
![](http://www.ai-start.com/dl2017/images/14e1df0a7a8cdd1584b2e92e87e23aa7.png)
### 一对一
![](http://www.ai-start.com/dl2017/images/14e1df0a7a8cdd1584b2e92e87e23aa7.png)
### 一对多
![](http://www.ai-start.com/dl2017/images/db580f1dfd6095d672fc62cce74ce5e2.png)

## 语言模型和序列生成
语言模型所做的就是，它会告诉你某个特定的句子它出现的概率是多少

### 语言模型建立步骤
+ 获取大量数据集
+ 句子标记化
+ 构建RNN


## RNN梯度消失的问题
![](http://www.ai-start.com/dl2017/images/8fb1c4afe30b7a0ede26522b355068ba.png)
### RNN存在问题
+ 缺乏长期记忆，如cat和were
+ 梯度爆炸

### 如何解决？
+ GRU
+ LSTM

## GRU
### cell单元
+ 功能：记忆
$$
\hat{c}^{<t>}=tanh(W_c[c^{<t-1>},x^{<t>}]+b_c)
$$
### 记忆门
$$
\Gamma_u=\sigma(W_u[c^{<t-1>},x^{<t>}]+b_u)
$$

### GRU简化模型
$$
c^{<t>}=\Gamma \hat{c}^{<t>}+(1-\Gamma_u)c^{<t-1>}
$$

### 相关性
$$
\Gamma_r=\sigma(W_r[c^{<t-1>},x^{<t>}]+b_r)
$$

$$
\hat{c}^{<t>}=tanh(W_c[\Gamma_r*c^{<t-1>},x^{<t>}]+b_c)
$$

## LSTM
### LSTM模型图
![](http://www.ai-start.com/dl2017/images/LSTM.png)
### LSTM单元
+ 更新门
+ 遗忘门
+ 输出门
+ 激活函数
+ 相关性门

### LSTM的前向传播
![](http://www.ai-start.com/dl2017/images/LSTM_rnn.png)

### LSTM反向传播
#### 门求偏导
![](https://cdn.jsdelivr.net/gh/Fazziekey/image-bed/img/20200712162521.png)
#### 参数求偏导
![](https://cdn.jsdelivr.net/gh/Fazziekey/image-bed/img/20200712162520.png)
#### 参数更新
![](https://cdn.jsdelivr.net/gh/Fazziekey/image-bed/img/20200712162522.png)

## 双向RNN
![](http://www.ai-start.com/dl2017/images/48c787912f7f8daee638dd311583d6cf.png)

## 深层RNN
![](http://www.ai-start.com/dl2017/images/8378c2bfe73e1ac9f85d6aa79b71b5eb.png)

--------------------------

# 自然语言处理和词嵌入
![](http://www.ai-start.com/dl2017/images/68d7c930146724f39782cb57d33161e9.png)

## 词汇表征
### one-hot编码的缺点
+ 每个词孤立，泛化能力不强
+ 数据量太大

### 如何改进？
#### 应用特征向量
![](http://www.ai-start.com/dl2017/images/ce30c9ae7912bdb3562199bf85eca1cd.png)

### t-SNE 算法
将一维词向量转化为二维可视化
![](http://www.ai-start.com/dl2017/images/59fb45cfdf7faa53571ec7b921b78358.png)

## 使用词嵌入
![](http://www.ai-start.com/dl2017/images/b4bf4b0cdcef0c9d021707c47d5aecda.png)

### 词嵌入做迁移学习的方法
+ 先从大量的文本集中学习词嵌入。一个非常大的文本集，或者下载预训练好的词嵌入模型
+ 用这些词嵌入模型把它迁移到新的只有少量标注训练集的任务中，比如说用这个300维的词嵌入来表示的单词。这样做的一个好处就是可以用更低维度的特征向量代替原来的10000维的one-hot向量，现在你可以用一个300维更加紧凑的向量。尽管one-hot向量很快计算，而学到的用于词嵌入的300维的向量会更加紧凑。

+ 在你的任务上训练模型时，在你的命名实体识别任务上，只有少量的标记数据集上，你可以自己选择要不要继续微调，用新的数据调整词嵌入。实际中，只有这个第二步中有很大的数据集你才会这样做，如果你标记的数据集不是很大，通常我不会在微调词嵌入上费力气。

## 词嵌入的特性
+ 类比推理

$$
e_{man}-e_{women}=
\begin{bmatrix}
-1\\
0.01\\
0.03
\\0.09
\end{bmatrix}
-
\begin{bmatrix}
-1\\
0.02\\
0.02
\\0.01
\end{bmatrix}

=
\begin{bmatrix}
-2\\
-0.01\\
0.01
\\0.08
\end{bmatrix}
\approx
\begin{bmatrix}
-2\\
0\\
0
\\0
\end{bmatrix}
$$

$$
e_{king}-e_{queen}=
\begin{bmatrix}
-0.95\\
0.093\\
0.70
\\0.09
\end{bmatrix}
-
\begin{bmatrix}
0.97\\
0.95\\
0.69
\\0.01
\end{bmatrix}

=
\begin{bmatrix}
-1.92\\
-0.02\\
0.01
\\0.01
\end{bmatrix}
\approx
\begin{bmatrix}
-2\\
0\\
0
\\0
\end{bmatrix}
$$
![](https://cdn.jsdelivr.net/gh/Fazziekey/image-bed@master/2020/07/16/db12137b26fb4e84e5261b2dcb49ddf9.png)
$$
e_{man}-e_{woman}\approx e_{king}-e_{queen}
$$

### 如何反映相似度？
**余弦相似度**
$$
sim(u,v)=\frac{u^Tv}{|u|_2|v|_2}
$$
![](https://cdn.jsdelivr.net/gh/Fazziekey/image-bed@master/2020/07/16/b71d0cddd12a41ab5c9212b24497a92c.png)

## 嵌入矩阵
学习词嵌入其实是学习一个嵌入矩阵
![](https://cdn.jsdelivr.net/gh/Fazziekey/image-bed@master/2020/07/16/f319dc21af8e248c2e7418883f160097.png)
$$
E\cdot o_i=e_{i}
$$


## 学习词嵌入
![](https://cdn.jsdelivr.net/gh/Fazziekey/image-bed@master/2020/07/16/b6b25908f6ab1c94d6d102191377160f.png)
### skip-gram
**输入：预测的词汇前n个单词，上下文**

**输出：softmax的rank**

+ 随机生成一个嵌入矩阵
+ 学习嵌入矩阵参数


## Word2Vec
学习映射关系

$$
o_c \to E \to e_c\to o_{softmax}\to \hat{y}
$$
+ 随机选择目标单词上下文的另一个单词
+ 输入one-hot向量
+ 监督学习



> softmax:

$$
p(t|c)=\frac{e^{\theta_t^T}e_c}{\sum_{j=1}^{10000}e^{\theta_t^T}e_c}
$$

### 存在问题
softmax运算量太大

### 解决方法
+ 分级
+ 负采样

### CBOM和skip-gram 

![](https://cdn.jsdelivr.net/gh/Fazziekey/image-bed@master/2020/07/16/774dd0cfce8313c273f7155aa064869a.png)

## 负采样（Negative Sampling）

+ 给定一对单词和target
+ 使用逻辑回归

![](https://cdn.jsdelivr.net/gh/Fazziekey/image-bed@master/2020/07/16/1b1dd8a7cbddd05425e6b728cbbac957.png)

$$
P(y=1|c,t)=\sigma(\theta_t^Te_c)
$$

+ 输入one-hot向量
+ 传递给嵌入矩阵
+ 得到10000个逻辑回归问题
+ 只选取其中K个进行训练
+ 转化为K个二分类问题

## Glove(global vectors for word represengtation) 

+ $x_{ij}$:单词i和单词j在上下文出现的次数
 

$$
minimize\sum_{i=1}^{10000}\sum_{j=1}^{10000}f(x_{ij})(\theta_i^Te_j+b_i-b_j+\log x_{ij})^2
$$
![](https://cdn.jsdelivr.net/gh/Fazziekey/image-bed@master/2020/07/17/c649b0538387f6bac50010d96b8ca019.png)

## 情感分类
![](https://cdn.jsdelivr.net/gh/Fazziekey/image-bed@master/2020/07/17/af7d6b80483a8a5ad04a78ebaabeca7d.png)


![](https://cdn.jsdelivr.net/gh/Fazziekey/image-bed@master/2020/07/17/134af70c48588b247e437f8a5cab420e.png)

##  词嵌入除偏（Debiasing Word Embeddings）

![](https://cdn.jsdelivr.net/gh/Fazziekey/image-bed@master/2020/07/17/7640e02d6663dd97ec7cf1e152041e1e.png)

+ 求平均
+ 中和
+ 均衡步


# 序列模型和注意力机制（Sequence models & Attention mechanism

## 基础模型
### 应用
+ 机器翻译
+ 语言识别

### 机器翻译
![](https://cdn.jsdelivr.net/gh/Fazziekey/image-bed@master/2020/07/18/4e15947a9ec31763d8545715e20e707c.png)
+ 输入法语，输出英语
+ 网络结构：LSTM或GR

### 图片描述
![](https://cdn.jsdelivr.net/gh/Fazziekey/image-bed@master/2020/07/18/2683ae07c70d727208561dc32a64d43a.png)

+ 输入图片
+ 进入卷积神经网络如AlexNet
+ 把softmax单元更换为RNN结构
+ 输出描述图片的序列

## 选择最可能的句子（Picking the most likely sentence）

### 语言模型和机器翻译模型的区别
![](https://cdn.jsdelivr.net/gh/Fazziekey/image-bed@master/2020/07/18/d6b739666d9d7af497ce06ea4a3b14fc.png)
+ 语言模型以零向量开始，翻译模型从句子开始
+ 翻译模型为条件语言模型

**最大化以下式子**
$$
P(y^{<1>},...,t^{<T_y>}|x)
$$

### 为什么不用Greed search
+ 我们需要一次性输出整个句子而不是一个单词
+ 运算量太大

> 贪心搜索是一种来自计算机科学的算法，生成第一个词的分布以后，它将会根据你的条件语言模型挑选出最有可能的第一个词进入你的机器翻译模型中，在挑选出第一个词之后它将会继续挑选出最有可能的第二个词，然后继续挑选第三个最有可能的词，这种算法就叫做贪心搜索。

## Beam Search

+ beam width$B=3$,选择softmax前三个最大值

![](https://cdn.jsdelivr.net/gh/Fazziekey/image-bed@master/2020/07/18/a620354d4ceafdca5ca0f9ee8b5b658b.png)
+ 输入句子，如“Jane visite l'Afrique en Septembre”
+ 选择第一个单词，保留前三的可能性
+ 确认单词对的最大可能性
+ 继续重复该步骤

## Beam search 改进
### Length normalization
$$
arg max\prod_{t=1}^
{T_y}P(y^{<t>}|x,y^{<1>},...,y^{<t-1>})
$$
加入log函数
$$
arg max\sum_{t=1}^
{T_y}\log P(y^{<t>}|x,y^{<1>},...,y^{<t-1>})
$$
加入参数$\alpha$

$$
\frac{1}{T_y^{\alpha}}arg max\sum_{t=1}^
{T_y}\log P(y^{<t>}|x,y^{<1>},...,y^{<t-1>})
$$

### how to choose Beam width B
+ B=1贪心算法
+ B过大，计算量大，效果没有显著提升

## Beam search 误差分析
+ $P(y^*|x)>P(\hat{y}|x)$束搜索算法出错
+ $P(y^*|x)<P(\hat{y}|x)$RNN模型出错

> RNN实际上是一个编码器合解码器

## 如何评价一个翻译系统的好坏
+ 与人工翻译进行对比
+ 观察输出是否在参考中
+ 每个单词加入计分上限

### Blue score
考虑词组得分

![](https://cdn.jsdelivr.net/gh/Fazziekey/image-bed@master/2020/07/18/143d162f91004d79ff47338ad85be5d7.png)

## 注意力模型（Attention Model）
### 长句子的问题
blue score降低
![](https://cdn.jsdelivr.net/gh/Fazziekey/image-bed@master/2020/07/18/d1ab68289592565fa9abf0df235039e3.png)

### 注意力权重$\alpha<t,t'>$
第t个输出单词对应第t‘个输入单词的权重
![](https://cdn.jsdelivr.net/gh/Fazziekey/image-bed@master/2020/07/18/c629b0432b83a9875e5a80ebb2558484.png)

$$
c^{<t>}=\sum_{t'}\alpha^{<t,t'>}a^{<t'>}
$$

$$
\alpha^{<t,t'>}=\frac{exp(e^{<t,t'>})}{\sum_{t'=1}^{T_x}exp(e^{<t,t'>})}
$$
![](https://cdn.jsdelivr.net/gh/Fazziekey/image-bed@master/2020/07/18/b6ff6fb462ce466873c06b366060a817.png)
![](https://cdn.jsdelivr.net/gh/Fazziekey/image-bed@master/2020/07/18/4560eb03dfac3d28c6e1e831295d64e7.png)

### 网络结构梳理
$$
activate：x^t \to a^t
$$
$$
a^t,s^{t-1}\to e^t
$$
$$
softmax:e \to \alpha
$$
$$
\alpha,a\to c
$$
$$
activate：c \to s 
$$
$$
s^t\to y^t
$$

## 语音识别

+ 输入音频
+ 输出文字序列

### phonemes方法
将声音分解为最基本的音位

### CTC cost（Connectionist temporal classification）
+ 折叠重复字符
![](https://cdn.jsdelivr.net/gh/Fazziekey/image-bed@master/2020/07/18/f16abb639f18e3ab3674c1db485590c8.png)

## 触发字检测（Trigger Word Detection）
![](https://cdn.jsdelivr.net/gh/Fazziekey/image-bed@master/2020/07/18/16d66c2dd1d9b048e93013002beef77e.png)