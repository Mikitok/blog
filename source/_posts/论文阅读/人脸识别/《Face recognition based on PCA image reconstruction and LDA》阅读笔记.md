---
title: 《Face recognition based on PCA image reconstruction and LDA》阅读笔记
date: 2017-10-17 19:24:29
tags:
  - 机器学习
  - 人脸识别
  - 论文阅读
  - 独立成分分析
  - 主成分分析
  - 无监督学习
categories:
  - 论文阅读
comments: false
---

## Brief Introduction
&emsp;&emsp;预处理（直方图均衡化+PCA图像重建（新）+LDA+SVM

## Proposed Method
&emsp;&emsp; They propose a novel method based on PCA image reconstruction and LDA for face recognition. Our proposed methods effectively combine the advantages of PCA, LDA, and SVM.

## Framework
1. Introduction
&emsp;1.1 人脸识别现状（概念+价值+十分热门+有挑战性）
&emsp;1.2 人脸识别的关键问题（特征提取和分类器）
&emsp;&emsp;1.2.1 PCA（由来+发展）
&emsp;&emsp;1.2.2 LDA（影响+思想+缺点+发展）
&emsp;1.3 本文算法流程+优点
2. Related algorithms
&emsp;2.1 Principal component analysis(PCA)
&emsp;2.2 Linear Discriminant Analysis(LDA)
&emsp;2.3 Support vector machine (SVM)
3. Face recognition based on PCA image reconstruction and LDA
&emsp;3.1 Image preprocessing(histogram equalization)
&emsp;3.2 PCA image reconstruction
&emsp;3.3 PCA image reconstruction and LDA for face recognition（算法流程）
4. Experimental results and discussion
&emsp;4.1 Experiments on ORL database
&emsp;4.2 Discussion
5. Conclusions

## Sentences
1. Face recognition is a technology of using computer to analyze the face images and extract the features for recognizing the identity of the target.
2. The research of face recognition has great theoretical value, involving subjects of pattern recognition, image processing, computer vision, machine learning, physiology, and so on, and it also has a high correlation with other biometrics recognition methods. 
3. In recent years, face recognition is one of the most active and challenging problems in the field of pattern recognition and artificial intelligence.

## Other
1. 直方图均衡化：histogram equalization