---
title: 基于TF-IDF和线性回归的简单文本分类
toc: true
copyright: true
date: 2021-11-29 22:51:02
tags:
    - NLP
    - ML
categories:
    - 《炼金术士修炼手册》
reward:
---

在机器学习算法的训练过程中，假设给定 
N个样本，每个样本有 M个特征，这样组成了 `N×M`的样本矩阵，然后完成算法的训练和预测。同样的在计算机视觉中可以将图片的像素看作特征，每张图片看作`hight×width×3`的特征图，一个三维的矩阵来进入计算机进行计算。

但是在自然语言领域，上述方法却不可行：文本是不定长度的。文本表示成计算机能够运算的数字或向量的方法一般称为词嵌入（Word Embedding）方法。词嵌入将不定长的文本转换到定长的空间内，是文本分类的第一步。
## Word Emdedding方法
### One-hot
One-hot是最简单的词嵌入方法，这里的One-hot与数据挖掘任务中的操作是一致的，即将每一个单词使用一个离散的向量表示。具体将每个字/词编码一个索引，然后根据索引进行赋值。

One-hot表示方法的例子如下：

句子1：我 爱 北 京 天 安 门
句子2：我 喜 欢 上 海
首先对所有句子的字进行索引，即将每个字确定一个编号：

{
    '我': 1, '爱': 2, '北': 3, '京': 4, '天': 5,
  '安': 6, '门': 7, '喜': 8, '欢': 9, '上': 10, '海': 11
}
在这里共包括11个字，因此每个字可以转换为一个11维度稀疏向量：

我：[1, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0]
爱：[0, 1, 0, 0, 0, 0, 0, 0, 0, 0, 0]
...
海：[0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 1]

### Bag of Words(词袋模型)

Bag of Words（词袋表示），也称为Count Vectors，每个文档的字/词可以使用其出现次数来进行表示。比如

    句子1：我 爱 北 京 天 安 门
    句子2：我 喜 欢 上 海
    
直接统计每个字出现的次数，并进行赋值：

    句子1：我 爱 北 京 天 安 门
    [1, 1, 1, 1, 1, 1, 1, 0, 0, 0, 0]

    句子2：我 喜 欢 上 海
    [2, 0, 0, 0, 0, 0, 0, 1, 1, 1, 1]
   
   
其中‘我’出现两次，所以被赋值为2

在sklearn中可以直接CountVectorizer来实现这一步骤：

    from sklearn.feature_extraction.text import CountVectorizer
    corpus = [
        'This is the first document.',
        'This document is the second document.',
        'And this is the third one.',
        'Is this the first document?',
    ]
    vectorizer = CountVectorizer()
    vectorizer.fit_transform(corpus).toarray()
   
词袋模型存在的问题和One-Hot相同，编码方式并没有体现相邻词的相关性，只显示单个词的统计频率。
    
### N-gram
N-gram与词袋模型类似，不过加入了相邻单词组合成为新的单词，并进行计数，这样做的好处是增加了词之间的关联信息。

如果N取值为2，则句子1和句子2就变为：

    句子1：我爱 爱北 北京 京天 天安 安门
    句子2：我喜 喜欢 欢上 上海

但词袋模型和N-gram都存在同一问题，对于一个长文本，类似于‘的’这样的介词会出现多次，而这些词所含文本的信息量极少，赋予一个较高的权值并不合理。

### TF-IDF
TF-IDF解决了上述问题。
TF-IDF 分数由两部分组成：第一部分是词语频率（Term Frequency），第二部分是逆文档频率（Inverse Document Frequency）。其中计算语料库中文档总数除以含有该词语的文档数量，然后再取对数就是逆文档频率。

$$
TF(t)= \frac{该词语在当前文档出现的次数}{ 当前文档中词语的总数}

IDF(t)= log_e（\frac{文档总数}{ 出现该词语的文档总数}）

TF-IDF = IDF(t) * TF(t)
$$
对于在所有文档中出现的词，取对数后为0，计算结果为0；

## 使用Bag of Words(词袋模型)进行预测

我们使用Bag of Words(词袋模型)进行编码后，采用最简单的逻辑回归进行预测，代码如下：

    import pandas as pd
    from sklearn.feature_extraction.text import CountVectorizer
    from sklearn.linear_model import RidgeClassifier
    from sklearn.metrics import f1_score
    
    train_df = pd.read_csv('./train_set.csv/train_set.csv', sep='\t', nrows=15000)
    vectorizer = CountVectorizer(max_features=3000)
    train_test = vectorizer.fit_transform(train_df['text'])
    clf = RidgeClassifier()
    clf.fit(train_test[:10000], train_df['label'].values[:10000])
    
    val_pred = clf.predict(train_test[10000:])
    print(f1_score(train_df['label'].values[10000:], val_pred, average='macro'))
    
    
输出结果用f1_score作为评分标准

    0.7416952793751392

## 使用TF-IDF进行预测

    from sklearn.feature_extraction.text import TfidfVectorizer

    tfidf = TfidfVectorizer(ngram_range=(1, 3), max_features=3000)
    train_test = tfidf.fit_transform(train_df['text'])
    clf.fit(train_test[:10000], train_df['label'].values[:10000])
    
    val_pred = clf.predict(train_test[10000:])
    print(f1_score(train_df['label'].values[10000:], val_pred, average='macro'))
    
输出结果

    0.8721598830546126
    
对比词袋模型提升明显

我们将最大特征提高到5000


    tfidf = TfidfVectorizer(ngram_range=(1, 3), max_features=5000)
    
输出

    0.8850817067811825

因为训练样本较少，加入平滑措施，此时idf公式变为
$$
idf(t)=log( \frac{(1+训练集文本总数) } {(1+包含词t的文本数) )}+1
$$

    tfidf = TfidfVectorizer(ngram_range=(1, 3), max_features=5000, smooth_idf=True)
    
输出结果

    0.8891785268087526