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

记，$P(x_i \triangleright x_j) \triangleq P_{ij},\ o_i \triangleq f(x_i),\ o_{ij} \triangleq f(x_i) - f(x_j)$

类似于逻辑回归，记
$$P_{ij} \triangleq \frac{e^{o_{ij}}}{1 + e^{o_{ij}}}$$则cross entrophy cost function为
$$C_{ij} \triangleq C(o_{ij}) = - \hat{P}_{ij}logP_{ij} - (1 - \hat{P}_{ij})log(1-P_{ij}) = - \hat{P}_{ij}o_{ij} + log(1 + e^{o_{ij}}) $$
渐进于线性，且在P=1/2时对称。


p.3: Theorem: Given a sample set xi, i = 1, . . . , m and any permutation Q of the consecutive integers {1, 2, . . . , m}, suppose that an arbitrary target posterior 0 ≤ P ̄kj ≤ 1 is specified for every adjacent pair k = Q(i),j = Q(i+1), i = 1,...,m−1. Denote the set of such P ̄’s, for a given choice of Q, a set of ’adjacency posteriors’. Then specifying any set of adjacency posteriors is necessary and sufficient to uniquely identify a target posterior 0 ≤ P ̄ij ≤ 1 for every pair of samples xi, xj. 


[视频](http://videolectures.net/icml2015_burges_learning_to_rank/)
