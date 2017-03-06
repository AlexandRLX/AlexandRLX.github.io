---
title: Factorization Machines
author: c cm
layout: post
permalink: /factorization machines/
categories: paper
tags:
description:
---

## 1. 模型定义

$$\hat y(\textbf{x}) := w_0 + \sum_{i=1}^n w_ix_i + \sum_{i=1}^n\sum_{j=i+1}^n\langle\textbf{v}_i, \textbf{v}_j\rangle x_ix_j$$
$$\langle\textbf{v}_i, \textbf{v}_j\rangle := \sum_{f=1}^k v_{i,f} \cdot v_{j,f}$$

其中，k为描述分解维度的超参。

优点：  

* 特征稀疏时可用
* 线性复杂度 O(kn)

## 2. 学习
直接优化primal
$$\frac{\partial\hat{y}(x)}{\partial\theta} = \{ {1\ if\ \theta\ is\ w_0\\
   x_i\ if\ \theta\ is\ w_i\\
   x_i\sum_{j=1}^nv_{j,f}x_j - v_{i,f}x_i^2\ if\ \theta\ is\ v_{i, f}}$$


## 3. 模型对比
1. SVM  
    * 线性核SVM一致
    * 比Polynomial核，权重间是相关的

2. 比其他Factorization方法
如Matrix and Tensor Factorization, SVD++, PITF FPMC等都可mimic，且更通用


ref

* Rendle, S. (2010). Factorization machines. Data Mining (ICDM).
