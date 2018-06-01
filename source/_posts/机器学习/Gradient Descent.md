---
title: Gradient Descent（梯度下降）
date: 2017-05-9 16:23:29
tags:
  - matlab
  - 机器学习
categories:
  - 机器学习
comments: false
---
&emsp;&emsp;这段时间不是很忙，也看到Andrew Ng在Coursera上的machine learning开课了，就顺带着看看。第一周和第二周讲的都是比较简单的问题，主要就是介绍了Cost Function以及最小化的几个方法。我这里要说的就是其中的一种：Gradient desxcent（梯度下降）。
&emsp;&emsp;梯度下降这个概念对很多人来说都不是很熟悉了，我之前看过关于HOG(方向梯度直方图)的一篇论文，再看梯度下降就有种熟悉感。

## 梯度下降的思想
&emsp;&emsp;在介绍梯度下降之前我们先引入一个Cost function（代价函数）：
$$J(\theta\_0,\theta\_1,...,\theta\_n)=\frac{1}{2m}\sum_{i=1}^{m}(h(x^i)-y^i)^2$$
&emsp;&emsp;$\theta\_t$是$x^t$对应的系数，$m$是样本总数，其中$h(x^i)$是第$i$个变量预测的结果，计算公式定义如下：
$$h(x^i)=\theta\_0+\theta\_1x\_1+...+\theta\_nx\_n$$
&emsp;&emsp;我们的目的就是最小化$J(\theta\_0,\theta\_1,...,\theta\_n)$的值，这是一个有关于$\theta\_0,\theta\_1,...,\theta\_n$的函数。这也是梯度下降想要求得的目标。
&emsp;&emsp;假想我们站在一个山上（当然根据这个题目，这个山可能是多维的，但是不管），我们想要到达海拔最高的地，所以我们的选择是像更矮的地方迈出一步，然后一步一步走到最低点。这也就是梯度下降的思想，根据一定的策略减少$J$的值，然后达到最低点。因为$J(\theta\_0,\theta\_1,...,\theta\_n)$是和$\theta\_0,\theta\_1,...,\theta\_n$有关的函数，所以我们可以通过修改$\theta\_0,\theta\_1,...,\theta\_n$的值来修改$J(\theta\_0,\theta\_1,...,\theta\_n)$的大小。我们以前常用的一种方法就是通过求导来得到最小值所在的位置，梯度下降也是通过求导来逐步修改$\theta\_0,\theta\_1,...,\theta\_n$的值。具体公式如下：
$$$$\begin{matrix}
\left\{
\begin{aligned}
\theta\_0:=\theta\_0-\alpha\frac{1}{2m}\sum_{i=1}^{m}(h(x^i)-y^i)\\
\theta\_n:=\theta\_n-\alpha\frac{1}{2m}\sum_{i=1}^{m}(h(x^i)-y^i)x^i\_n\\
\end{aligned}
\right.
\end{matrix}$$$$
&emsp;&emsp;其中$\alpha$是学习效率，即我们每次的步子究竟是要迈多大。太小了就会走的很慢，太大了容易一步迈过了最小值，可能离最小值越来越远。通常，我们函数在越靠近最小值时下降越平缓，所以没有必要手动的修改（可以设置为$...0.001,...,0.01,...,0.1,...,1...$）。所以我们每次迭代就是根据不同的$\theta$来计算，再根据不同的计算结果修改$\theta$，至于迭代结束的条件，可以设置两次大小相差不超过$10^{-3}$，或者预先设置好迭代次数。
&emsp;&emsp;但是这也带来了一个问题，因为我们身在山中，只知道这个点是我们目前走到的局部最低点，而并不知道是不是想要的全局海拔最低的地方，所以相对应的，梯度下降也是只能得到局部最小值，而不能得到全局最小值。

## matlab代码
&emsp;&emsp;虽然作业分了单个变量和多个变量，但是因为是用Matlab进行矩阵运算，所以写起来没有多大差别。
### 梯度下降
```matlab
function [theta, J_history] = gradientDescent(X, y, theta, alpha, num_iters)
%GRADIENTDESCENT Performs gradient descent to learn theta
%   theta = GRADIENTDESCENT(X, y, theta, alpha, num_iters) updates theta by 
%   taking num_iters gradient steps with learning rate alpha

% Initialize some useful values
m = length(y); % number of training examples
J_history = zeros(num_iters, 1);

for iter = 1:num_iters

    % ====================== YOUR CODE HERE ======================
    % Instructions: Perform a single gradient step on the parameter vector
    %               theta. 
    %
    % Hint: While debugging, it can be useful to print out the values
    %       of the cost function (computeCost) and gradient here.
    %
    h=X*theta;
    theta=theta-alpha/m*((h-y)'*X)';

    % ============================================================

    % Save the cost J in every iteration    
    J_history(iter) = computeCost(X, y, theta);

end
end
```

### 计算代价函数
```matlab
function J = computeCost(X, y, theta)
%COMPUTECOST Compute cost for linear regression
%   J = COMPUTECOST(X, y, theta) computes the cost of using theta as the
%   parameter for linear regression to fit the data points in X and y

% Initialize some useful values
m = length(y); % number of training examples

% You need to return the following variables correctly 
J = 0;

% ====================== YOUR CODE HERE ======================
% Instructions: Compute the cost of a particular choice of theta
%               You should set J to the cost.
h=X*theta;
J=1/2/m*(h-y)'*(h-y);

% =========================================================================

end
```

### 特征一般化
```matlab
function [X_norm, mu, sigma] = featureNormalize(X)
%FEATURENORMALIZE Normalizes the features in X 
%   FEATURENORMALIZE(X) returns a normalized version of X where
%   the mean value of each feature is 0 and the standard deviation
%   is 1. This is often a good preprocessing step to do when
%   working with learning algorithms.

% You need to set these values correctly
X_norm = X;

% ====================== YOUR CODE HERE ======================
% Instructions: First, for each feature dimension, compute the mean
%               of the feature and subtract it from the dataset,
%               storing the mean value in mu. Next, compute the 
%               standard deviation of each feature and divide
%               each feature by it's standard deviation, storing
%               the standard deviation in sigma. 
%
%               Note that X is a matrix where each column is a 
%               feature and each row is an example. You need 
%               to perform the normalization separately for 
%               each feature. 
%
% Hint: You might find the 'mean' and 'std' functions useful.
%       

mun=mean(X);
sigma=std(X);
[m,~]=size(X);
for i=1:m
    X_norm(i,:)=(X(i,:)-mun)./sigma;
end
mu=mun;
% ============================================================

end

```

&emsp;&emsp;作业及代码放在[github][1]了。


  [1]: https://github.com/Mikitok/Machine-Learning/tree/master/machine-learning-ex1