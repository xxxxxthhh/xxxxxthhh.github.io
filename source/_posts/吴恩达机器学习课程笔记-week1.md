---
title: 吴恩达机器学习课程笔记 - week1
date: 2019-05-08 14:48:06
tags:
  - python
  - 学习
  - 机器学习
categories:
  - python学习笔记
  - 机器学习笔记
mathjax: true
---
<center>之前刷了吴恩达课程的视频，把笔记整理一下，慢慢更新</center>

<!-- more -->


# 绪论：初识机器学习

## 什么是机器学习

一个程序从经验**E**中学习，解决任务**T**，达到性能量度**P**，当且仅当有了经验**E**后，经过**P**评判，程序在处理任务**T**时的性能有所提升。

简单来说，通过投喂数据，教会机器使用算法解决问题。

## 监督学习

数据集包括“正确答案”，根据样本学习进行预测。

问题包括**分类**与**回归**

## 无监督学习

给算法大量无标签数据，从中分析出某种结构。比如对数据进行**聚类**

# 单变量线性回归

## 模型表示

**回归问题**：根据之前的数据预测出一个准确的输出值

![](https://raw.githubusercontent.com/xxxxxthhh/pic_go/master/%E7%9B%91%E7%9D%A3%E5%AD%A6%E4%B9%A0%E7%AE%97%E6%B3%95%E5%B7%A5%E4%BD%9C%E6%B5%81%E7%A8%8B.png)

如图所示为预测房屋价格算法的流程，将训练数据集投入学习算法，输出一个函数 *h*（意为 *hypothesis* 假设），该函数可根据输入的房屋面积预测售价。

上述问题中有可能的 *h* 表达方式为：
$$
h_{\theta}(x)=\theta_{0}+\theta_{1} x
$$
只含有一个特征变量 *x*，因此该问题被称为**单变量线性回归**。

## 代价函数 - Cost Function

上一小节我们知道了函数 *h* 的表达式，但是如何确定两个参数呢？

![](https://raw.githubusercontent.com/xxxxxthhh/pic_go/master/%E5%8D%95%E7%BA%BF%E6%A8%A1%E5%9E%8B%E5%8F%82%E6%95%B0%E9%80%89%E6%8B%A9.png)

例如预测房价，使用预测函数，可以预测数据集外房屋的售价。但是首先该函数一定要适用于已知数据，而参数决定了我们得到的函数相对于训练集的准确程度，如下图所示，预测值（直线）与实际值（X）的差距就是**建模误差（modeling error）**

![](https://raw.githubusercontent.com/xxxxxthhh/pic_go/master/%E5%BB%BA%E6%A8%A1%E8%AF%AF%E5%B7%AE.png)

我们的目标就是通过调整参数，使得预测函数能拟合更多数据，从而使**代价函数（Cost Function）**最小： 
$$
J\left(\theta_{0}, \theta_{1}\right)=\frac{1}{2 m} \sum_{i=1}^{m}\left(h_{\theta}\left(x^{(i)}\right)-y^{(i)}\right)^{2}
$$
可以看出代价函数为建模误差的平方和，*m* 为训练集中实例的数量。

还有其他的[代价函数](https://baike.baidu.com/item/%E4%BB%A3%E4%BB%B7%E5%87%BD%E6%95%B0/7048599?fr=aladdin)可以选择，但平方误差代价函数是解决回归问题的常用手段。

## 代价函数的直观理解

![](https://raw.githubusercontent.com/xxxxxthhh/pic_go/master/%E4%BB%A3%E4%BB%B7%E5%87%BD%E6%95%B0%E7%9B%B4%E8%A7%82%E7%90%86%E8%A7%A3.png)

目标是使**代价函数最小**，根据代价函数 *J* 的三维图像，可知存在一点，在该点的两个参数的取值可使整体代价函数最小，可通过该图进行直观理解。

![](https://raw.githubusercontent.com/xxxxxthhh/pic_go/master/%E4%BB%A3%E4%BB%B7%E5%87%BD%E6%95%B0%E4%B8%89%E7%BB%B4%E5%9B%BE.png)

但是如果每次都通过画图看点来找最小值就太麻烦了，并且某些数据难以进行可视化，所以需要有效的**算法**来自动找出使代价函数 *J* 最小的参数*θ*。

## 梯度下降 - Gradient Descent

梯度下降是一个用来**求函数最小值**的算法，此处可用来求代价函数 *J* 的最小值。

![](https://raw.githubusercontent.com/xxxxxthhh/pic_go/master/%E6%A2%AF%E5%BA%A6%E4%B8%8B%E9%99%8D.png)

随机选取参数作为起始点，计算代价函数，然后下一组寻找能使代价函数下降最多的参数（就如同山顶下山，环顾四周，选择最陡峭下降最快速的方向），直到周围的参数无法使代价函数下降，此时达到了一个 **局部最小值（local minimum）**。
$$
\begin{array}{l}{\text { repeat until convergence }\{ } \\ {\theta_{j} :=\theta_{j}-\alpha \frac{\partial}{\partial \theta_{j}} J\left(\theta_{0}, \theta_{1}\right) \quad(\text { for } j=0 \text { and } j=1)} \\ {\}}\end{array}
$$
上述公式为 **批量梯度下降**（*batch gradient descent*），其中 *α* 是**学习率**（*learning rate*），即控制代价函数的下降速度。

在运算过程中，**同时更新参数**是梯度下降的一种常用方法。
$$
\begin{array}{l}{\text { Correct: Simultaneous update }} \\ {\text { temp 0 } :=\theta_{0}-\alpha \frac{\partial}{\partial \theta_{0}} J\left(\theta_{0}, \theta_{1}\right)} \\ {\text { temp } 1 :=\theta_{1}-\alpha \frac{\partial}{\partial \theta_{1}} J\left(\theta_{0}, \theta_{1}\right)} \\ {\theta_{0} :=\operatorname{temp} 0} \\ {\theta_{1} :=\operatorname{temp} 1}\end{array}
$$

## 梯度下降的直观理解

### 公式理解

![](https://raw.githubusercontent.com/xxxxxthhh/pic_go/master/%E6%A2%AF%E5%BA%A6%E4%B8%8B%E9%99%8D%E5%85%AC%E5%BC%8F%E7%90%86%E8%A7%A3.png)

实际上求导操作是计算该红色直线的斜率，该直线为正斜率，所以新的 *θ<sub>1</sub>* 更新后等于 *θ<sub>1</sub>* 减去一个正数乘以 *α* 。

如果 *θ* 初始化时就在最低点，意味着已经在局部最优点，切线导数为 0，*θ* 的值不会再改变，所以梯度下降算法其实什么也没做，这也是为什么保持学习速率 ***α* 不变**，梯度下降**依然可以收敛**到局部最低点，而不需要边训练边改变参数。

实际上在接近最低点的过程中，导数值自动的变得越来越小（斜率越来越小），所以梯度下降的幅度也会减小，所以没有必要另外减小 *α *。

![](https://raw.githubusercontent.com/xxxxxthhh/pic_go/master/%E6%A2%AF%E5%BA%A6%E4%B8%8B%E9%99%8D%E7%90%86%E8%A7%A3.png)

### *α* 的取值

如果太小了，即学习速率太小，结果就是只能这样像小宝宝一样一点点地挪动，去努力接近最低点，这样就需要很多步才能到达最低点，所以如果太小的话，可能会很慢，因为它会一点点挪动，它会需要很多步才能到达全局最低点。

如果太大，那么梯度下降法可能会越过最低点，甚至可能无法收敛，下一次迭代又移动了一大步，越过一次，又越过一次，一次次越过最低点，直到你发现实际上离最低点越来越远，所以，如果太大，它会导致无法收敛，甚至发散。 

## 梯度下降的线性回归

$$
\begin{array}{c|c}{\text { Gradient descent algorithm }} & {\text { Linear Regression Model }} \\ {\text { repeat until convergence }\{ } & {h_{\theta}(x)=\theta_{0}+\theta_{1} x} \\ {\theta_{j} :=\theta_{j}-\alpha \frac{\partial}{\partial \theta_{j}} J\left(\theta_{0}, \theta_{1}\right)} & {J(\theta)=\frac{1}{2 m} \sum_{i=1}^{m}\left(h_{\theta}\left(x^{(i)}\right)-y^{(i)}\right)^{2}} \\ {\}}\end{array}
$$

了解了梯度下降算法，与之前线性回归想结合解决问题。

将梯度下降应用到线性回归当中，关键在于求出**代价函数的导数**，即：
$$
\frac{\partial}{\partial \theta_{j}} J\left(\theta_{0}, \theta_{1}\right)=\frac{\partial}{\partial \theta_{j}} \frac{1}{2 m} \sum_{i=1}^{m}\left(h_{\theta}\left(x^{(i)}\right)-y^{(i)}\right)^{2}
$$

$$
\begin{aligned} J = 0时：\frac{\partial}{\partial \theta_{0}} J\left(\theta_{0}, \theta_{1}\right) &=\frac{1}{m} \sum_{i=1}^{m}\left(h_{\theta}\left(x^{(i)}\right)-y^{(i)}\right) \\ J = 1时：\frac{\partial}{\partial \theta_{1}} J\left(\theta_{0}, \theta_{1}\right) &=\frac{1}{m} \sum_{i=1}^{m}\left(\left(h_{\theta}\left(x^{(i)}\right)-y^{(i)}\right) \cdot x^{(i)}\right) \end{aligned}
$$

最后梯度下降算法改写为：
$$
\begin{array}{l}{\text { Repeat }\{ } \\ {\theta_{0} :=\theta_{0}-a \frac{1}{m} \sum_{i=1}^{m}\left(h_{\theta}\left(x^{(i)}\right)-y^{(i)}\right)} \\ {\theta_{1} :=\theta_{1}-a \frac{1}{m} \sum_{i=1}^{m}\left(\left(h_{\theta}\left(x^{(i)}\right)-y^{(i)}\right) \cdot x^{(i)}\right)} \\ {\}}\end{array}
$$
**批量**梯度下降的意思在于，每一步的求和运算，都用到了所有的训练样本，当然也有其它类型的梯度下降法，不是“批量”型的，不需要考虑全部数据集。

