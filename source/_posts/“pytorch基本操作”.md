---
title: “pytorch矩阵基本操作”
date: 2020-04-21 08:56:46
copyright: true
tags:
    - pytorch
categories: 
    - 《炼金术士修炼手册》
---
## 导入 pytorch库
    from __future__ import print_function
    import torch
需要配置好环境

## 创建矩阵
### 构造5\*3未初始化的矩阵
    x = torch.empty(5, 3)
	print(x)
输出
   	 tensor([[2.1030e-18, 4.5559e-41, 4.0441e+10],
        [3.0767e-41, 0.0000e+00, 1.4013e-45],
        [0.0000e+00, 0.0000e+00, 0.0000e+00],
        [0.0000e+00, 0.0000e+00, 0.0000e+00],
        [0.0000e+00, 0.0000e+00, 0.0000e+00]])
<!--more-->

### 构建一个随机初始化矩阵
    x = torch.rand(5, 3)
    print(x)

### 构造一个填充零且dtype long的矩阵，长整形
    x = torch.zeros(5, 3, dtype=torch.long)
	print(x)

### 从数据构造张量
    x = torch.tensor([5.5, 3])
    print(x)

### 基于现有张量创建张量。这些方法将重用输入张量的属性，例如dtype，除非用户提供新值
    x = x.new_ones(5, 3, dtype=torch.double)      # new_* methods take in sizes
	print(x)

	x = torch.randn_like(x, dtype=torch.float)    # override dtype!
	print(x)                                     # result has the same size

### 矩阵大小函数
    print(x.size())
    #torch.size 为一个元组

## 矩阵基本运算

### 加法
#### 方法1
    y = torch.rand(5, 3)
	print(x + y)

#### 方法2
    print(torch.add(x, y))

### 加法：提供输出张量作为参数
    result = torch.empty(5, 3)
	torch.add(x, y, out=result)
	print(result)

### 地板加
    # adds x to y
	y.add_(x)
	print(y)

注意
任何使张量就地变化的操作都用固定_。例如：x.copy_(y)，x.t_()，将改变x。

## 矩阵索引
    print(x[:, 1]) 
    #索引第二列，所有矩阵从0算起
    冒号表示范围 如1:3索引第二行到第三行

##  矩阵大小调整
    x = torch.randn(4, 4)
	y = x.view(16)
	z = x.view(-1, 8)  # the size -1 is inferred from other dimensions
	print(x.size(), y.size(), z.size())

输出结果
torch.Size([4, 4]) torch.Size([16]) torch.Size([2, 8])

### 特殊情况，只有一个元素
	如果您具有一个元素张量，请使用.item()将该值作为Python数字获取

## 与numpy之间转换
### torch转numpy
	a = torch.ones(5) #元素全为1矩阵创建
	print(a)
tensor([1., 1., 1., 1., 1.])

    b = a.numpy()
	print(b)
[1. 1. 1. 1. 1.]

	a.add_(1)
	print(a)
	print(b)

tensor([2., 2., 2., 2., 2.])
[2. 2. 2. 2. 2.]

### numpy转torch

    import numpy as np
	a = np.ones(5)
	b = torch.from_numpy(a)
	np.add(a, 1, out=a)
	print(a)
	print(b)

## CUDA张量
### 使用该.to方法可以将张量移动到任何设备上。

    # let us run this cell only if CUDA is available
    # We will use ``torch.device`` objects to move tensors in and out of GPU
	if torch.cuda.is_available():
    	 device = torch.device("cuda")          # a CUDA device object
         y = torch.ones_like(x, device=device)  # directly create a tensor on GPU
         x = x.to(device)                       # or just use strings ``.to("cuda")``
         z = x + y
         print(z)
         print(z.to("cpu", torch.double))       # ``.to`` can also change dtype together!




