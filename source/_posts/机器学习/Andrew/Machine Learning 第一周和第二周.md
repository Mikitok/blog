title: Machine Learning 第一周和第二周
date: 2017-10-16 9:53:48
tags:
  - 机器学习
  - matlab
  - Coursera
categories:
  - 机器学习
---

&emsp;&emsp;一直有想看Andrew Ng的机器学习课程，但是拖了很久都没有看完。之前也写过一些相关的博客，但是在博客搬家的时候没有保存下来。
&emsp;&emsp;第一周和第二周的内容比较少，作业也是在一起布置的。

# WEEK 1
## Introduction
### What is machine learning?
1. 机器学习的定义：为了完成某个目标T，从经验E中学习，同时具有一定的判断标准P。

### Supervised Learning
1. 监督学习：部分样本已有正确的结果。
2. 分类：
&emsp;回归问题（regression）：预测输出结果是连续值。
&emsp;分类问题（classification）：预测输出结果是离散值。

### Unsupervised Learning
1. 从数据本身的结构中得到模型。
2. 预测结果无反馈。

## Linear Regression with One Variable（单变量线性回归）
### Model Representation
1. 符号定义：
&emsp;$m$：训练样本数
&emsp;$x's$：输入变量
&emsp;$y$：输出变量
&emsp;$(x,y)$：一个训练样本
&emsp;$(x^{(i)},y^{(i)})$：第$i$个训练样本

### Cost Function
1. 假设函数：$h\_\theta(x)=\theta\_0+\theta\_1x$
2. 代价函数（误差平方函数）：$J(\theta\_0,\theta\_1)=\frac{1}{m}\sum\_{i=1}^{m}(h\_{\theta}(x\_i)-y\_i)^2$
3. 目标：最小化代价函数&emsp; $minmize J(\theta\_0,\theta\_1)$

### Cost Function-Intuition 1

### Cost Function-Intuition 2
1. $h\_\theta(x)$是关于$x$的函数，$J(\theta\_0,\theta\_1)$是关于$\theta\_0,\theta\_1$的函数。
2. 可以通过轮廓图来判断$\theta\_0,\theta\_1$和$J(\theta\_0,\theta\_1)$的关系。

### Gradient Descent（梯度下降）
1. 思想：
&emsp;(1). 选取一组$\theta\_0,\theta\_1$（通常都为0）
&emsp;(2). 不断更新$\theta\_0$和$\theta\_1$，直到$J(\theta\_0,\theta\_1)$达到局部最小值。
> repeat until covergence{
&emsp;&emsp;$\theta\_j:=\theta\_j-\alpha\frac{d}{d\theta\_j}J(\theta\_0,\theta\_1)$
> }

&emsp;其中$\alpha$是学习速率
2. 在变量更新过程中应保持同步更新。

### Gradient Descent Intuition
1. $\alpha$（学习速率）：
&emsp;(1). 过大，可能无法达到局部最低点。
&emsp;(2). 过小，十分缓慢地达到局部最低点。
2. 通常，越靠近最低点，曲线的斜率越靠近0，迈的步子越小，所以没有必要在过程中修改$\_alpha$。

### Gradient Descent For Linear Regression
1. 对变量的改变的求导展开为
&emsp;$\theta\_0:=\theta\_0-\alpha\frac{1}{m}\sum\_{i=1}^{m}(h\_{\theta}(x\_i)-y\_i)$
&emsp;$\theta\_1:=\theta\_1-\alpha\frac{1}{m}\sum\_{i=1}^{m}(h\_{\theta}(x\_i)-y\_i)\cdot x\_i$

## Linear Algebra Review
### Matrices and Vextors
1. 一般使用大写字母表示矩阵，小写字母表示向量。
2. $R$表示实数集，$R^n$表示由实数集组成的$n$维向量。

### Addition and Scalar Multiplication
1. Scalar Multiplication：标量乘法，即一个实数乘以一个矩阵。

### Matrix Vector Multiplication
1. 一个$m\times n$的矩阵与一个$n\times 1$的向量相乘的结果是一个$m\times 1$的向量。

### Matrix Matrix Multiplication
1. 一个$m\times n$的矩阵与一个$n\times o$的矩阵相乘的结果是一个$m\times o$的矩阵。

### Matrix Multiplication Properties（矩阵乘法的特性）

### Inverse and Transpose
1. $A$的逆矩阵为$A^{-1}$。
2. 一个非方阵的矩阵无逆矩阵。

# WEEK 2
## Multivariate Linear Regression（多元线性回归）
### Multiple Features
1. 符号定义：
&emsp;$n$：特征的数量
&emsp;$x^{(i)}$：第$i$个样本的特征
&emsp;$x\_{j}^{(i)}$：第$i$个样本的第$j$个特征

### Gradient Descent for Multiple Variables
1. 假设：$h\_\theta(x)=\theta^Tx=\theta\_0x\_0+\theta\_1x\_1+…+\theta\_nx\_n$，其中$x\_0=1$。
2. 变量：$\theta=[\theta\_0,\theta\_1,…,\theta\_n]^T$
3. 代价函数：$J(\theta\_0,\theta\_1)=\frac{1}{m}\sum\_{i=1}^{m}(h\_{\theta}(x\_i)-y\_i)^2$
4. 更新：
> repeat until covergence{
&emsp;&emsp;$\theta\_j:=\theta\_j-\alpha\frac{1}{m}h\_{theta}(x\_i)-y\_i)x\_{j}^{(i)}$
> }

### Gradient Descent in Practice 1-Feature Scaling（特征缩放）
1. 特征的尺度相似时，梯度下降进行得更快。
2. 均一化（Mean normalization）：$x\_i=\frac{x\_i-\mu\_i}{s\_i}$，其中$\mu\_i$是均值，$s\_i$是范围（最大值-最小值）


### Gradient Descent in Practice 2-Learning rate
1. 可以通过画$J(\theta)$和迭代次数的关系曲线图，来判断$\alpha$的选择是否正确。
2. 正常情况下，$J(\theta)$会随着迭代次数的增加而减小。
3. $J(\theta)$下降得很慢，则$\alpha$过小。
4. $J(\theta)$上升或者不是持续下降，则$\alpha$过大。

### Features and Polynomial Regression
1. 改进假设函数的方法：
&emsp;(1). 将多个特征合为一个特征。
&emsp;(2). 多项式回归。

## Computing Parameters Analytically
### Normal Equation（正规方程）
1. 正规方程求解$\theta$时可以一步到位。
2. 假设有$m$个变量，每个变量有$n$个特征。
构建$X=\begin{bmatrix}
 1 & 1 & … & 1 \\\\ 
x^{(1)} & x^{(1)} & … & x^{(m)} 
\end{bmatrix} ^T$，$Y=[y^{(1)},y^{(2)},…,y^{(m)}]^T$
$X\theta = Y$
所以$\theta =(X^TX)^{-1}X^TY$
3. 对正规方程来说，没有必要使用特征缩放。
4. 正规方程：$\theta \in R^{n+1}$，即求得$\theta \_0,\theta \_1, …,\theta \_n$
使得$\frac{d}{d\theta \_j}J(\theta )=…=0$，其中$J(\theta\_0,\theta\_1)=\frac{1}{m}\sum\_{i=1}^{m}(h\_{\theta}(x\_i)-y\_i)^2$。
5. 对比：
|梯度下降|正规方程|
|:--:|:--:|
|需要选择$\alpha$|不需要选择$\alpha$|
|需要迭代|不需要迭代|
|时间复杂度$O(n^2)$|时间复杂度$O(n^3)$|
|$n$大时也有效|当$n$大时，运行缓慢|
6. $n\leq 10000$，可选择正规方程求解。

### Normal Equation Noninvertibility（不可逆性）
1. $X^TX$不可逆的原因可能为：
&emsp;(1). 特征之间关联大。
&emsp;(2). 特征数量太多。

# PROGRAMMING
## warmUpExercise
&emsp;&emsp;在warmUpExercise.m中添加：
``` matlab
A = eye(5);
```
## Linear regression with one variable
### computeCost
&emsp;&emsp;在computeCost.m中添加：
``` matlab
ypre=X*theta;
J=1/2/m*sum((ypre-y).^2);
```

### gradientDescent
&emsp;&emsp;gradientDescent.m中添加：
``` matlab
theta=theta-(alpha/m*sum(bsxfun(@times,X*theta-y,X)))';
```

## Linear regression with multiple variables
### Feature Normalization
&emsp;&emsp;在featureNormalize.m中添加：
``` matlab
mu=mean(X);
sigma=std(X);
X_norm=bsxfun(@rdivide,bsxfun(@minus,X,mu),sigma);
```

### computeCostMulti
&emsp;&emsp;在computeCostMulti.m中添加：
``` matlab
ypre=X*theta;
J=1/2/m*sum((ypre-y).^2);
```

### gradientDescentMulti
&emsp;&emsp;在gradientDescentMulti.m中添加：
``` matlab
theta=theta-(alpha/m*sum(bsxfun(@times,X*theta-y,X)))';
```

&emsp;&emsp;在ex1\_multi.m中修改：
``` matlab
price = [1650,3];
price=[1,(price-mu)./sigma] * theta;
```

## normalEqn
&emsp;&emsp;normalEqn.m中添加：
``` matlab
theta=X'*X \ X'*y;
```
&emsp;&emsp;在ex1\_multi.m中修改：
``` matlab
price = [1,1650,3];
price=price* theta;
```