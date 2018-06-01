---
title: 《A two-phase face recognition method in frequency domain》阅读笔记
date: 2017-10-18 14:30:29
tags:
  - 机器学习
  - 人脸识别
  - 论文阅读
  - 离散余弦变换
  - 离散傅立叶变换
  - 无监督学习
categories:
  - 论文阅读
comments: false
---

## Brief Introduction
&emsp;&emsp;对图像进行DCT和DFT特征提取+（第一项）先求得k个近邻+将图像分成K个图片的融合，并求得每张图片对应的系数+计算测试样本和每类之间的距离

## Proposed Method
&emsp;&emsp; They proposed a two-phase representation method that uses DCT coefficients or DFT amplitude spectra for face recognition. It is more efficient than the naïve 1 norm-based sparse representation method.

## Framework
1. Introduction
&emsp;1.1 人脸识别价值+基于变换域的方法
&emsp;1.2 基于DCT和DFT的算法的发展和分类+基于变换域的方法的优点
&emsp;&emsp;1.2.1 使用一部分DCT系数和DFT幅度谱
&emsp;&emsp;1.2.2 使用全部DCT系数和DFT幅度谱
&emsp;1.3 新的二相分类方法算法+优点
&emsp;1.4 本文算法流程
&emsp;1.5 文章组织结构
2. The Proposed algorithm
3. Experimental results
&emsp;3.1 Performance comparison
&emsp;3.2 Number of DCT coefficients and DFT amplitude spectra
4. Conclusions

## Other
1. 离散余弦变换：discrete cosine transform
2. 离散傅立叶变换：discrete Fourier transform
3. 幅度谱：amplitude spectra
4. 变换域：transform domain
5. 整体的：holistic
6. 误差：deviation 