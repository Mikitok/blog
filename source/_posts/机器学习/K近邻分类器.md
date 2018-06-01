---
title: K近邻分类器
date: 2017-03-22 16:23:29
tags:
  - matlab
  - 机器学习
  - python
categories:
  - 机器学习
comments: true
---



&emsp;&emsp;K近邻分类器是机器识别中很常用的一种分类方法，以前在做单样本人脸识别的时候常用的最近邻分类方法就是其中k=1的特殊情况。以前都是用matlab写的代码，最近老师动员大家一起来学python，然后我们就都从K近邻算法开始学习编程了。

## K近邻算法
&emsp;&emsp;该方法的思路是：如果一个样本在特征空间中的k个最相似(即特征空间中最邻近)的样本中的大多数属于某一个类别，则该样本也属于这个类别。其实也很好理解，就是现在有n个训练样本，分别对应c个类，现在有一个未知的测试样本，要找到这个测试样本的类别。K近邻的方法就是计算出每个训练样本和测试样本的距离，找到其中最近的K个样本对应的类别，并统计每个类出现的次数，出现的最多的类即使该测试样本对应的类。

## Python代码
&emsp;&emsp;这个代码就是随便写写了，我只用了欧氏距离。其实python有自带的KNN的函数，所以还是推荐大家直接调用函数吧。代码若有错误望指正。
```python
    def knn(trn,label,x,k):
    import numpy as np
    dist=np.zeros(numsamples)
    for i in range(numsamples):
        dist[i] = np.sqrt(np.sum(np.square(trn[i] - x)))
    print (dist)

    index=np.argsort(dist)
    print (index)

    numclass=np.max(label)+1
    times=np.zeros(numclass)
    for i in range(k):
        times[label[index[i]]]=times[label[index[i]]]+1
        print(times)

    ind=np.argmax(times)
    return (label[ind])
```

测试：
``` python
    trn1=np.random.randn(10,2)
    trn2=np.random.randn(10,2)
    trn=np.concatenate((trn1,trn2))
    x=np.random.randn(1,2)
    label=[0,0,0,0,0,0,0,0,0,0,1,1,1,1,1,1,1,1,1,1]
    k=3
    result=knn(trn,label,x,k)
    print (resut)
```
    
## matlab代码
&emsp;&emsp;matlab我把这个分成了两个部分，计算距离和分类，因为可选的参数有点多。
首先是计算距离的函数(discompute.m)：
```matlab
    function [D]=discompute(X_trn,X_tst,method)
    %%%%%%%%%%%%%%%%%%%%%
    %   这个函数是来计算训练样本和测试样本之间的距离
    %   X_trn是训练样本，X_tst是测试样本，都是cell矩阵，一个cell存放一张图片
    %   method有四个值可供选择：chi-square（卡方距离）、manhatton（曼哈顿距离）、cosine（余弦距离）、euclidean（欧氏距离）
    %   返回值D即距离，是cell矩阵，一个cell存放一个测试样本和所有训练样本的距离
    %   对于D中的每个cell，行对应着不同的块，列对应着不同的训练样本
    
    if nargin<3 method='chi-square';end
    D=cell(length(X_tst),1);
    switch lower(method)
        case 'chi-square'
            for j=1:length(X_tst)
                x1=X_tst{j};
                for i=1:length(X_trn)
                    x2=X_trn{i};
                    A=(x1-x2).^2./(x1+x2);
                    in=find(isnan(A)==1);
                    A(in)=0;
                    D{j}(:,i)=sum(A,2);     % Chi-square distance
                end
            end
        case 'manhattan'
            for j=1:length(X_tst)
                x1=X_tst{j};
                for i=1:length(X_trn)
                    x2=X_trn{i};
                    D{j}(:,i)=sum(abs(x1-x2),2); %Mahatton distance
                end
            end
        case 'cosine'
            for j=1:length(X_tst)
                x1=X_tst{j};
    %              [x1]=normlizedata(x1,'1-norm');
                for i=1:length(X_trn)
                    x2=X_trn{i};
    %                    [x2]=normlizedata(x2,'1-norm');
                    D{j}(:,i)=1-(diag(x1*x2')./(sqrt(diag(x1*x1')).*sqrt(diag(x2*x2')))); % Cosine distance
                end
            end
        case 'euclidean'
            for j=1:length(X_tst)
                x1=X_tst{j};
                for i=1:length(X_trn)
                    x2=X_trn{i};
                    D{j}(:,i)=(sum(((x1-x2).^2),2)); %Euclidean distance
                end
            end
    end
```
然后是分类（disclassify.m）:
```matlab
`function [out]=distclassify(D,Y,method,Layer)
    %%%%%%%%%%%%%%%%%%
    %   这个函数是用来进行分类的
    %   参数D是距离（参见discompute.m），Y是所有训练样本的标签
    %   method有四个值可选：vote（投票）、min_dist（最小值）、max_dist（最大值）和sum_dist（总和）。
    %   out返回所有测试样本的标签，是一个行向量
    
    if nargin<2 || nargin>4
        help Distclassify
    else
        numclass=max(Y);
        numtest=length(D);
        if nargin<4 Layer=floor(log(numclass)/log(2));end 
        if nargin<3 method='vote';end
        switch lower(method)
            case 'vote'
                A=zeros(numtest,numclass);
                for i=1:length(D)
                    [~,d]=min(D{i}');
                    for j=1:numclass
                        A(i,j)=sum(Y(j)==d);
                    end
                end
                [~,out]=max(A');
            case 'min_dist'
                A=zeros(numtest,numclass);
                for i=1:numtest
                    A(i,:)=min(D{i});
                end
                [~,out]=min(A');
            case 'max_dist'
                A=zeros(numtest,numclass);
                for i=1:numtest
                    A(i,:)=max(D{i});
                end
                [~,out]=min(A');
            case 'sum_dist'
                A=zeros(numtest,numclass);
                for i=1:length(D)
                    A(i,:)=sum(D{i});
                end
                [~,out]=min(A');
          
        end
    end
```
