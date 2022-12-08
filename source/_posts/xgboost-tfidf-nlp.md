---
title: 基于tfidf和xgboost文本分类
toc: true
copyright: true
date: 2021-12-05 19:59:23
tags:
    - NLP
    - ML
    - xgboost
categories:
    - 《炼金术士修炼手册》
reward:
---
# boost & bagging & stacking 区别
|算法|模型|数据|作用|实现
---|----|----|---|---
Bagging|多个相同不稳定模型|对数据随机采样，每个模型不同|减少 variance|用多个模型平均或投票，并行
Boosting|多个相同弱模型|每次从样本分布不同的数据集采样，上个模型预测错误的数据有更大可能被选择|减少 bias|用多个相同弱模型不断拟合残差，减少方差。串行
Stacking|多个不同模型|全部数据|增强预测效果|用多个不同模型输出concat后生成一个新的数据后再通过一个分类器输出
 
## baggingBagging 
是 bootstrap aggregation的缩写。bagging对于数据集进行取样，每个数据点有同等几率被采样，然后创建n个模型，每个模型进行m个数据采样，最后进行投票（voting）得出最后结果。




# xgboost实现文本分类

+ 导入相关文件


      import xgboost as xgb
      import pandas as pd
      from sklearn.feature_extraction.text import TfidfVectorizer
      from sklearn.metrics import f1_score

+ 数据读取并做TF-IDF处理
xgboost的输入数据要求为DMatrix类，所以要通过`xgb.DMatrix`方法进行转化


      model_path = "./xgboost/"

      train_df = pd.read_csv('./train_set.csv/train_set.csv', sep='\t', nrows=50000)
      tfidf = TfidfVectorizer(ngram_range=(1, 3), max_features=5000, smooth_idf=True)
      label = train_df['label']
    train_test = tfidf.fit_transform(train_df['text'])

      train_data = train_test[:45000]
      train_label = label[:45000]
      dtrain = xgb.DMatrix(train_data, label=train_label, nthread=-1)

      test_data = train_test[45000:50000]
      test_label = label[45000:50000]
      dtest = xgb.DMatrix(test_data, label=test_label, nthread=-1)

+ 设置训练参数


      params = {
            'booster': 'gbtree',           # gbliner 或 gbtree树模型或者线性模型
            'objective': 'multi:softmax',  # 多分类的问题
            'num_class': 14,               # 类别数，与 multisoftmax 并用
            'gamma': 0.1,                  # 用于控制是否后剪枝的参数,越大越保守，一般0.1、0.2这样子。
            'max_depth': 12,               # 构建树的深度，越大越容易过拟合
            'lambda': 2,                   # 控制模型复杂度的权重值的L2正则化项参数，参数越大，模型越不容易过拟合。
            'subsample': 0.7,              # 随机采样训练样本
            'colsample_bytree': 0.7,       # 生成树时进行的列采样
            'min_child_weight': 3,         # 最小叶子节点样本权重和
            'silent': 1,                   # 设置成1则没有运行信息输出，最好是设置为0.
            'eta': 0.1,                  # 学习率
            'seed': 1000,
            'nthread': 4,                  # cpu 线程数
    }


+ 训练模型并保存


    print("start train xgboost classifier")
    xgbc = xgb.train(params, dtrain)  # 初始化xgboost分类器，原生接口默认启用全部线程
    xgbc.save_model(model_path+'xgboost.model')  # 保存模型

+ 预测结果并打印和_score


    print("xgboost train over")
    pre_train = xgbc.predict(xgb.DMatrix(train_data, nthread=-1))   # 训练数据的预测概率矩阵，启用全部线程
    pre_test = xgbc.predict(xgb.DMatrix(test_data, nthread=-1))     # 测试数据的预测概率矩阵，启用全部线程

    print("train data f1score:")
    print(f1_score(train_label, pre_train, average='macro'))

    print("test data f1score:")
    print(f1_score(test_label, pre_test, average='macro'))

+ 输出结果

    train data f1score:
    0.9321652074415424
    test data f1score:
    0.8822079711934986


# 参考文献

[xgboost 调参指南](https://www.analyticsvidhya.com/blog/2016/03/complete-guide-parameter-tuning-xgboost-with-codes-python/)