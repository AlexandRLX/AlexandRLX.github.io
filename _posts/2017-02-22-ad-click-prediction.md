---
title: Ad Click Prediction
author: c cm
layout: post
permalink: /ad_click_prediction/
categories: paper
tags:
description:
---

## 1. FTRL
$\textbf{g}_t$ 第t个样本向量  
$g_{t, i}$ 第t个样本向量的第i个变量  
$\textbf{g}_{1:t} = \sum_1^t \textbf{g}_i$

OGD(Online Gradient Descent):
$$\textbf{w}_{t+1} = \textbf{w}_t - \eta_t\textbf{g}_t$$
其中$\eta$为学习速率。  
缺点为稀疏性不足。

FTRL:
$$\textbf{w}_{t+1} = \underset{\textbf{w}}{argmin}(\textbf{g}_{1:t} \textbf{w} + \frac{1}{2}\sum_{s=1}^{t} \sigma_s \|\textbf{w} - \textbf{w}_s\|_2^2 + \lambda_1\|\textbf{w}\|_1)$$
其中$\sigma$为学习率，$\sigma_{1:t} = 1/\eta_t$



## 2. Per-coordinate learning rate

$$\eta_{t,i} = \frac{\alpha}{\beta + \sqrt{\sum_{s=1}^tg_{s,t}^2}}$$

## 3. Saving memory at massive scale
* Probablistic Feature Inclusion  
    new features in the model probabilistically as they first occur 
    1. Poisson Inclusion
    2. Bloom Filter Inclusion
* Encoding Values with Fewer Bits  
    eg. 分析数据后，用 q2.13 encoding
    需要解决roundoff问题，eg randomized rounding strategy
    $$w_{i, rounded} = 2^{-13}[2^{13}w_i + R]$$
    其中R是0-1之间均匀分布的deviation
* Training Many Similar Models  
* A Single Value Structure
* Compute Learning Rate with Counts  
    $$\sum g_{t,i}^2 = \underset{positive\ events}\sum (1-p_t)^2 + \underset{negative\ events}\sum p_t^2 \\\approx P(1-\frac{P}{N+P})^2 + N (\frac{P}{N+P})^2 = \frac{PN}{N+P}$$
* Subsampling Training Data

## 4. Evaluating Model Performance
* Progressive Validation(online loss)
* Deep Understanding through Visualization
    GridVis

## 5. Confidence Estimates
do not fit standard confidence interval assumptions  
*uncertainty score* calculated using feature learning rate.
$$|\textbf{x w}_t - \textbf{x w}_{t+1}| = \underset{i: |x_i| > 0}\sum \eta_{t,i}|g_{t,i}| \\
\le \alpha \underset{i: |x_i| > 0}\sum \frac{x_{t,i}}{\sqrt{n_{t, i}}} = \alpha \eta \textbf{x} = u(\textbf{x})$$

## 6. Calibrating Predictions
* use Poisson regression to learn $\tau(p) = \gamma p^k$
* use piecewise linear/constant function

## 7. Automated Feature Management


ref 
[24] Follow-the-regularized-leader and mirror descent: Equivalence theorems and L1 regularization
