title: Machine Learning 第三周
date: 2017-11-10 14:50:48
tags:
  - 机器学习
  - matlab
  - Coursera
categories:
  - 机器学习
---
# Week 3
# PROGRAMMING
## Logistic Regression
### Visualizing the data
&emsp;&emsp;这一段可以自己写，但是在pdf中也有直接的代码可以添加在plotdata.m中：
``` matlab
% Find Indices of Positive and Negative Examples
pos = find(y==1); neg = find(y == 0);
% Plot Examples
plot(X(pos, 1), X(pos, 2), 'k+','LineWidth', 2, 'MarkerSize', 7);
plot(X(neg, 1), X(neg, 2), 'ko', 'MarkerFaceColor', 'y', 'MarkerSize', 7);
```

### Sigmoid Function
&emsp;&emsp;根据公式可以直接求出。注意是点除，不是直接的相除。
``` matlab
g=1./(1+exp(-z));
```

### Cost function and gradient
&emsp;&emsp;根据公式，在costFunction.m中添加以下代码：
``` matlab
J=1/m*(-y'*log(sigmoid(X*theta))-(1-y)'*log(1-sigmoid(X*theta)));
grad=1/m*((sigmoid(X*theta)-y)'*X);
```

### Evaluating logistic regression
&emsp;&emsp;这个就是根据结果判断是0还是1了，在predict.m中添加以下代码：
``` matlab
h=sigmoid(X*theta);
p(find(h<0.5))=0;
p(find(h>=0.5))=1;
```

## Regularized logistic regression
### Cost function and gradient
&emsp;&emsp;在原先的基础上添加一个正则项，matlab下标从1开始，这个问题让我找了半天的bug，在costFunctionReg.m中添加以下代码：
``` matlab
J=1/m*(-y'*log(sigmoid(X*theta))-(1-y)'*log(1-sigmoid(X*theta)))+lambda/2/m*(theta(2:end)'*theta(2:end));
grad=1/m*((sigmoid(X*theta)-y)'*X);
grad(2:end)=grad(2:end)+lambda/m*theta(2:end)';
```