---
title: Learning to Rank using Gradient Descent
author: c cm
layout: post
permalink: /learning_to_rank_using_gradient_descent/
categories: paper
tags:
description:
---

关键字：Bing，L2R，RankNet，gradient descent

## Probabilistic Ranking Cost Function
问题表述为：
给定在所有文档集$R^d$一对文档$d_a, d_b$，需要预测$\hat{P}_{ab} $，文档a排序在b之前的概率。

模型$\ f: R^d \to R$，$f(x_1) > f(x_2)$代表前者排序高于后者，即$x_1 \triangleright x_2$。

记，$P(x_i \triangleright x_j) \equiv P_{ij},\ o_i \equiv f(x_i),\ o_{ij} \equiv f(x_i) - f(x_j)$

类似于逻辑回归，记
$$P_{ij} \equiv \frac{e^{o_{ij}}}{1 + e^{o_{ij}}}$$则cross entrophy cost function为
$$C_{ij} \equiv C(o_{ij}) = - \hat{P}_{ij}logP_{ij} - (1 - \hat{P}_{ij})log(1-P_{ij}) = - \hat{P}_{ij}o_{ij} + log(1 + e^{o_{ij}}) $$
渐进于线性，且在P=1/2时对称。

## Adjacency Posteriors

p.3: Theorem: 

Given a sample set $x_i, i = 1, . . . , m$ and any permutation $Q$ of the consecutive integers $\{1, 2, . . . , m\}$, suppose that an arbitrary target posterior $0 ≤ \hat P_{kj} ≤ 1$ is specified for every adjacent pair $k = Q(i),j = Q(i+1), i = 1,...,m−1$.

Denote the set of such $\hat P$’s, for a given choice of $Q$, a set of ’adjacency posteriors’.

Then specifying any set of adjacency posteriors is necessary and sufficient to **uniquely** identify a target posterior $0 ≤ \hat P_{ij} ≤ 1$ for every pair of samples $x_i, x_j$. 

## RankNet

对于一般的神经网络，有：

对第i条训练数据，记神经网络的输出为$o_i$，目标为$t_i$，假设output node总共有q个，cost function为$\sum_{i=1}^q f(o_i, t_i)$。

记$\alpha_k$为模型的参数，那么gradient decent的一步为（$\eta_k$为learning rate）：
$$\delta\alpha_k = -\eta_k\frac{\partial f}{\partial\alpha_k}$$


第j层的transfer function为$g^j$，net可以表述为：
$$o_i = g^3(\sum_j w_{ij}^{32}g^2(\sum_k w_{jk}^{21} + b_j^2) + b_i^3) \equiv g_i^3$$

求偏导结果：
$$\frac{\partial f}{\partial b_i^3} = \frac{\partial f}{\partial o_i}g_i^{\prime 3} \equiv \triangle_i^3 \\
\frac{\partial f}{\partial w_{in}^{32}} = \triangle_i^3 g_n^2 \\
\frac{\partial f}{\partial b_m^2} = g_m^{\prime 2}(\sum_i\triangle_i^3 w_{im}^{32})\equiv \triangle_m^2\\
\frac{\partial f}{\partial w_{mn}^{21}} = x_n\triangle_m^2 
$$

结合之前所述cost function $f(o_2 - o_1)$和上面神经网络的结果，我们得到RankNet。
$$\frac{\partial f}{\partial b^3} = f^\prime (g_2^{\prime 3} - g_1^{\prime 3}) \equiv \triangle_2^3 - \triangle_1^3 \\
\frac{\partial f}{\partial w_{m}^{32}} = \triangle_2^3 g_{2m}^2 - \triangle_1^3 g_{1m}^2\\
\frac{\partial f}{\partial b_m^2} = \triangle_2^3 w_{m}^{32}g_{2m}^{\prime 2} - \triangle_1^3 w_{m}^{32}g_{1m}^{\prime 2}\\
\frac{\partial f}{\partial w_{mn}^{21}} = \triangle_{2m}^2 g_{2n}^1 - \triangle_{1m}^2 g_{1n}^1 
$$

## 优点:
1. 可以训练不consistant的数据, 如rank a > rank b, rank b > rank c, rank c > rank a
2. cost在$o_{ij} = 0$时取到最小值,且在离0点较远的地方渐进于线性,更加robust
3. certain -> more certain

## Furthur reading
[LambdaRank](http://iccm.cc/learning_to_rank_with_nonsmooth_cost_functions/)

[视频](http://videolectures.net/icml2015_burges_learning_to_rank/)
