---
title: Harr 小波变换
date: 2017-04-04 16:53:18
tags:
  - 机器学习
  - matlab
  - 单样本人脸识别
categories:
  - 机器学习
mathjax: true
---
&emsp;&emsp;我在网上了解小波变换的时候，发现它是常用于信号处理的一种方法，但是在论文里也常看到小波变换用于图像处理。小波函数在一定的时间间隔内波形幅度的平均值为0。现在有很多小波函数，Haar小波变换函数是其中最基础的一种，是最简单的正交归一化小波

## Harr 简介
&emsp;&emsp;我们先看一下Harr相关的函数图形：
![Haar 缩放函数图形和小波函数图形](/images/haar-1.png)

&emsp;&emsp;由上图可以以得知Harr小波函数是一个支撑域(函数$\psi(t)$不为0的区间)在$[0,1]$内的单个矩形波，公式如下：
$$\psi(t)=\begin{equation}
\left \\{
\begin{aligned}
1  && 0 \leq x < 0.5\\\\
-1 && 0.5 \leq x \leq 1\\\\
0 && otherwise\\\\
\end{aligned}
\right.
\end{equation}$$

## 算法流程
### Haar小波变换步骤

>  1. 把小波w(t)和原函数f(t)的开始部分进行比较，计算系数C。系数C表示该部分函数与小波的相似程度。
>  2. 把小波向右移k单位，得到小波w(t-k)，重复1。重复该部知道函数f结束。
>  3. 扩展小波w(t)，得到小波w(t/2)，重复步骤1,2。
>  4. 不断扩展小波，重复1,2,3。

&emsp;&emsp;假设我们现在有一个一维的表示特征的矩阵$X=\{x\_1,x\_2,x\_3,x\_4\}$。
&emsp;&emsp;然后对这个一维矩阵进行一次变换：
$$a\_{1,0}=\frac{x\_1+x\_2}{2}$$
$$a\_{1,1}=\frac{x\_3+x\_4}{2}$$
$$d\_{1,3}=\frac{x\_1-x\_2}{2}$$
$$d\_{1,4}=\frac{x\_3-x\_4}{2}$$
&emsp;&emsp;这样可以得到一个一维矩阵$Y=\{a\_{1,0},a\_{1,1},d\_{1,3},d\_{1,4}\}$。这里的$a\_{1,0}$和$a\_{1,1}$分别是$x\_1,x\_2$和$x\_3,x\_4$的均分，反映了它们的基本特征，所以我们称之为低频成分；而$d\_{1,3}$和$d\_{1,4}$分别是$x\_1,x\_2$和$x\_3,x\_4$的差值，反映了它们的细节信息，所以我们称之为高频成分。
&emsp;&emsp;我们也可以再次运用以上的思想对矩阵$Y$再进行一次Haar小波变换，得到最终的小波系数$\{a\_{2,0},d\_{2,1},d\_{1,3},d\_{1,4}\}$。

### 图像处理中的Harr小波变换
&emsp;&emsp;对二维图像进行Haar小波变换有两种方法：标准分解和非标准分解。标准分解是指先使用一维小波对图像的每一行的像素值进行变换,产生每一行像素的平均值和细节系数,然后再使用一维小波对这个经过行变换的图像的列进行变换,产生这个图像的平均值和细节系数。非标准分解是指使用一维小波交替地对每一行和每一列像素值进行变换。
&emsp;&emsp;对于对图像做小波变换，可以根据自己的需求编写函数，但是matlab也有自带的小波变换函数：dwt2和wavedec2。其中dwt2是二维单尺度小波变换，其可以通过指定小波或者分解滤波器进行二维单尺度小波分解。而wavedec2是二维多尺度小波分解。dwt2的一种语法格式是[cA,cH,cV,cD]=dwt2(X,'wname')；而对应的wavedec的语法格式是[C,S]=wavedec2(X,N,'wname'),其中N为大于1的正整数。也就是说dwt2只能对某个输入矩阵X进行一次分解，而wavedec2可以对输入矩阵X进行N次分解。

## matlab示例
### Harr小波示例
&emsp;&emsp;虽然matlab有自带的小波变换的函数，也可以通过open或者edit打开函数文件，查看源代码，但是忧伤的是，它的源代码往往互相之间都有联系，我打开了也是看不太懂。所以自己写了一个Haar小波的函数，没有做边界处理，就请将就着看看吧。
```matlab
    function [L,H] = MyHarr( line )
    % line: 一维矩阵，表示一个信号序列，最好行和列都是2的倍数
    % L: 低频成分
    % H: 高频成分
    
    n=length(line);
    n=n/2;
    L=zeros(1, n);
    H=zeros(1,n);
    
    for i=1:n
        L(i)=(line(2*i-1)+line(2*i))/2;
        H(i)=(line(2*i-1)-line(2*i))/2;
    end
    end
```

### matlab的dwt2()函数
&emsp;&emsp;dwt2()函数的一般形式就是：

    [CA,CH,CV,CD] = dwt2(X,'wname') 

> CA：approximation coefficients matrix（近似系数矩阵）
> CH、CV、CD：details coefficients matrices（细节系数矩阵）

&emsp;&emsp;使用并显示的代码如下：
```matlab
    A=imread('lena.jpg');

    [CA,CH,CV,CD] = dwt2(A,'haar') ;
    subplot(2,2,1);
    imshow(uint8(CA));
    subplot(2,2,2);
    imshow(uint8(CH));
    subplot(2,2,3);
    imshow(uint8(CV));
    subplot(2,2,4);
    imshow(uint8(CD));
```
&emsp;&emsp;显示的效果图为：
![lena处理后的显示意图](/images/haar-2.png)

### matlab的wavedec2()函数
&emsp;&emsp;wavedec2()一般使用形式为：

    [C,S] = wavedec2(X,N,'wname') 

&emsp;&emsp;这是一种二维多尺度小波分解函数，分解的次数和传入的参数N有关。其中C是一个行向量，它的组成如下：
> C = [ A(N) | H(N) | V(N) | D(N) | ... H(N-1) | V(N-1) | D(N-1) | ... | H(1) | V(1) | D(1) ].

&emsp;&emsp;介于这个不太好显示结果，我就不放出matlab代码了，实在需要的话相关的文档中有一段。
