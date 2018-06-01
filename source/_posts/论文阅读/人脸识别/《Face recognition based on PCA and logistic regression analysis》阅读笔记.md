---
title: 《Face recognition based on PCA and logistic regression analysis》阅读笔记
date: 2017-10-17 16:07:29
tags:
  - 机器学习
  - 人脸识别
  - 论文阅读
  - PCA
  - 逻辑回归
  - 线性回归
categories:
  - 论文阅读
comments: false
---
## Brief Introduction
&emsp;&emsp;使用PCA进行特征提取，使用LRC作为分类器。

## Proposed Method
&emsp;&emsp;ChangjunZhou proposed a novel face recognition method which is based on PCA and logistic regression.By combining the advantages of both the PCA and logistic regression, they use PCA to extract feature and reduce the dimensions of process data and use logistic regression as the classifier for face recognition.

## Framework
1 Introduction
&emsp;1.1 人脸识别现状（十分热门，但是有挑战性+影响因素，提出了很多方法）
&emsp;1.2 文章解决的两类问题
&emsp;&emsp;1.2.1 特征提取（PCA由来+简介）
&emsp;&emsp;1.2.2 分类器（分类器简介+SVM优点缺点+LRC算法简介和进化）
&emsp;1.3 本文算法优点
&emsp;1.4 文章组织结构
2 Related algorithms
&emsp;2.1 Principal component analysis(PCA)
&emsp;2.2 Logistic regression analysis
3 Proposed face recognition method（算法的流程）
4 Experimental results and discussion
&emsp;4.1 Yale database
&emsp;4.2 ORL database
5 Conclusions

## Sentences
1. Face recognition is an important research hotspot in the fields of pattern recognition and artificial intelligence, and it has attained great success in recent years.
2. Assume we have a training set …… with N images,belonging to c classes.
3. First, we preprocessed the input images, mainly including histogram equalization, geometry normalization, in order to remove the illuminations, shades, and lighting effects possibly, and then partitioned into a training set from face database and the rest is a testing set.
4. To illustrate the efficacy of our proposed method, we compared the performances on two standard databases, i.e., Yale database and the ORL database.
5. The Yale face database contains images with major variations, including changes in illumination conditions, subjects wearing eyeglasses and different facial expressions. This database involves 165 frontal facial images, with 11 images of 15 individuals.
6. To evaluate the effectiveness of the algorithms better, each image is scaled down to the size of 100 × 100 pixels.

## Other
1. 类间离散矩阵：between-class scatter matrix
2. 类内离散矩阵：within-class scatter matrix