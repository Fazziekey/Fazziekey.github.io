---
title: 使用pytorch进行梯度运算
date: 2020-04-22 11:00:03
copyright: true
tags:
    - pytorch
categories: 
    - 《炼金术士修炼手册》
---



torch.Tensor是程序包的中心类。如果将其属性设置 .requires_grad为True，它将开始跟踪对其的所有操作。完成计算后，可以调用.backward()并自动计算所有梯度。该张量的梯度将累加到.grad属性中。

### 创建一个张量并设置requires_grad=True为跟踪张量
    import torch
    x = torch.ones(2, 2, requires_grad=True)
    print(x)
<!--more-->    
### 运算 

    y = x + 2
    print(y)
    print(y.grad_fn)
输出

    tensor([[3., 3.],
    [3., 3.]], grad_fn=<AddBackward0>)
y是运算产生，存在梯度

    z = y * y * 3
    out = z.mean()
    print(z, out)
    
结果

    tensor([[27., 27.],
    [27., 27.]], grad_fn=<MulBackward0>)
    tensor(27., grad_fn=<MeanBackward0>)
    
.requires_grad_( ... )requires_grad 可以更改现有Tensor的标志。如果未给出输入，则默认为False。

    a = torch.randn(2, 2)
    a = ((a * 3) / (a - 1))
    print(a.requires_grad)
    a.requires_grad_(True)
    print(a.requires_grad)
    b = (a * a).sum()
    print(b.grad_fn)
    
输出

    False
    True
    <SumBackward0 object at 0x7fc4a70d31d0>
    
## 梯度计算
使用反向传播

    out.backward()

$out=\frac{1}{4}\sum_{i=1}^4 z_i,z=3(x+2)^2,\frac{\partial out}{\partial x}=\frac{3}{2}(x+2)=4.5|_{x=1},$
数学上，如果具有向量值函数 $\overrightarrow{y} =f(\overrightarrow{x})$，然后是 $\overrightarrow{y}$关于$\overrightarrow{x}$是雅可比矩阵：

$$J=\begin{pmatrix}
  \frac{\partial y_1}{\partial x_1} & ...& \frac{\partial y_1}{\partial x_n} \ \ ...& &...\ \ 
   \frac{\partial y_1}{\partial x_n} & ... & \frac{\partial y_n}{\partial x_n}
\end{pmatrix}$$

一般来说，torch.autograd是用于计算向量雅可比积的引擎。给定向量$v=(v_1,v_2...v_n)^T$，计算$J*v^T$,如果v 恰好是标量函数的梯度$l=g(\overrightarrow{y})$,则$v=( \frac{\partial l}{\partial y_1}... \frac{\partial l}{\partial y_n})^T$

$$
J^T\cdot v=\begin{pmatrix}
  \frac{\partial l}{\partial x_1} \ \ ...\ \ 
    \frac{\partial l}{\partial x_n}
\end{pmatrix}
$$

    x = torch.randn(3, requires_grad=True)

    y = x * 2
    while y.data.norm() < 1000:
    y = y * 2

    print(y)
    
输出

    tensor([1030.3691,  653.3950, -535.1644], grad_fn=<MulBackward0>)
    
输入

    v = torch.tensor([0.1, 1.0, 0.0001], dtype=torch.float)
    y.backward(v)
    print(x.grad)
    
输出

    tensor([5.1200e+01, 5.1200e+02, 5.1200e-02])

`.requires_grad=True`可以通过将代码块包装在 `with torch.no_grad():`

    print(x.requires_grad)
    print((x ** 2).requires_grad)

    with torch.no_grad():
    print((x ** 2).requires_grad)
    
输出

    True
    True
    False
