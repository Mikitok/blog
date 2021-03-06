---
title: 《统计学习方法》之k近邻法
date: 2017-10-22 14:10:18
tags:
  - 机器学习
  - 《统计学习方法》
categories:
  - 《统计学习方法》
comments: false
mathjax: true
---

&emsp;&emsp;相似度查询有两种方法：
&emsp;1. 范围查询，给定阈值。
&emsp;2. k近邻查询，给定查询点和k。
&emsp;&emsp;k近邻法是一种基本分类与回归的方法。其基本思想是：一个样本的k个最相近的样本大多属于某一个类，则该样本也属于这个类。因此，k近邻算法不具有显式的学习过程。k值的选择、距离度量和分类决策规则是k近邻方法的三个基本要素。

## k近邻算法
> k近邻算法流程
> 输入：训练数据集$T={(x\_1,y\_1),(x\_2,y\_2),…,(x\_N,y\_N)}$，其中，$x \in X \subseteq R^n$为实例的特征向量，$y\_i\in Y={c\_1,c\_2,…,c\_K}$为实例的类别，$i=1,2,…,N$，实例特征向量$x$。
> 输出：实例$x$所属的类$y$。
> (1) 根据给定的距离度量，在训练集$T$中找出与$x$最近的$k$个点，涵盖这$k$个点的$x$邻域记作$N\_k(x)$。
> (2) 在$N\_k(x)$中根据分类决策规则，决定$x$的类别$y$：
> $y=\arg \max \limits\_{c\_j}\{\sum \limits\_{x\_i\in N\_k(x)}I(y\_i=c\_j)\}, i=1,2,…,N; j=1,2,…,K $
> 其中$I$为指示函数，即当$y\_i=c\_j$时，$I$为1，否则为0。

&emsp;&emsp;k近邻的特殊情况是当$k=1$时，此算法被称为最近邻算法。

## k近邻模型
### 模型
&emsp;&emsp;特征空间中，对于每个训练实例点$x\_i$，距离该点比其他店更近的所有点组成的一个区域，叫做单元。k近邻算法就是利用训练数据集对特征向量空间进行划分。

### 距离度量
&emsp;&emsp;距离度量公式定义为：
$$L\_p(x\_i,x\_j)=(\sum\_{l=1}^{n}|x\_i^{(l)}-x\_i^{(l)}|^p)^\frac{1}{p}$$
其中$p\geq 1$
&emsp;&emsp;当$p=1$时，可以得到曼哈顿距离：$L\_1(x\_i,x\_j)=\sum\_{l=1}^{n}|x\_i^{(l)}-x\_i^{(l)}|$
&emsp;&emsp;当$p=2$时，可以得到欧式距离：$L\_2(x\_i,x\_j)=(\sum\_{l=1}^{n}|x\_i^{(l)}-x\_i^{(l)}|^2)^\frac{1}{2}$

### k值的选择
&emsp;&emsp;k值的选择对算法有很大的影响。k值的减小意味着整体模型变得复杂，容易发生过拟合。如果选择较大的k值，可以减少学习的估计误差，但是学习的近似误差会增加。在应用中，k值一般取一个比较小的值。通常采用交叉验证法来选取最合适的k值。

### 分类决策规则
&emsp;&emsp;k近邻法中的分类决策规则往往是多数表决，即由输入实例的k个近邻的训练实例中的多数类决定输入实例的类。这种决策规则等价于经验风险最小化。

## k近邻法的实现：kd树
&emsp;&emsp;我们在进行特征匹配是，通常采用两种方法：线性扫描和构建数据索引，而使用构建数据索引时，在无重叠时可采用kd树，重叠时可采用R树。
&emsp;&emsp;kd树的全称是k-dimension tree，可以用于k近邻的寻找。

### 构造kd树
&emsp;&emsp;kd树是一棵二叉树，也是一颗空间划分树（空间划分树：将整个空间划分为几个特定的部分，然后再特定的部分进行搜索）。
> 构造平衡kd树流程
输入：$k$维空间数据集$T={x\_1,x\_2,…,x\_N}$，其中$x\_i=(x\_i^{(1)},x\_i^{(2)},…,x\_i^{(k)})^T，i=1,2,…,N$
输出：kd树
算法流程：
(1) 开始：构造根结点，根结点对应于包含$T$的$k$维空间的超矩形区域。
&emsp;选择$x^{(1)}$为坐标轴，将$T$中所有实例的$x^{(1)}$的中位数（奇数个：取中间，偶数个：中间偏大）为切分点，将根结点对应的超矩形区域切分成两个子区域。左子结点对应于小于切分点的子区域，有子结点对应于大于切分点的子区域。落在切分超平面上的实例点保存在根节点。
(2) 重复：对深度为$j$的切分点，选择$x^{(l)}$为切分的坐标轴，其中$l=j(modk)+1$（从1到$k$循环取），重复以上操作。
(3) 直到两个子区域没有实例点存在时停止。从而形成kd树的区域划分。


