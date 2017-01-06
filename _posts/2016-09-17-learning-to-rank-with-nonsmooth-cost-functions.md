---
title: Learning to Rank with Nonsmooth Cost Functions
author: c cm
layout: post
permalink: /learning_to_rank_with_nonsmooth_cost_functions/
categories: paper
tags: LambdaRank
description:
---

机器学习任务中的两种cost:  
    1. target cost
    2. optimization cost应该让解决问题变得更简单，并尽量接近于target cost

本文中的optimization cost对每一个item在排序**后**定义一个虚拟梯度，绕过由排序带来的问题。

--
Notation  
$s_{ij}$ score of ranking function, i=index of query, j=index of doc returned  
$C(s_{ij}, l_{ij})$ l=label

## LambdaRank
$$\frac{\partial C}{\partial s_j} = -\lambda_j(s_1, l_1, ..., s_{n_i}, l_{n_i})$$
对于i个查询，doc的排序位置j，如果$\lambda$为正，则应该提高排名来降低C。可见，$\lambda$取决于根据score function排序后的位置。

现在我们需要确定$\lambda$，使得：  
    1. 对于该$\lambda$，能找到C使得上述梯度式子成立  
    2. C convex

根据
`
Theorem (Poincare ́ Lemma): If S ⊂ Rn is an open set that is star-shaped with respect to the origin, then every closed form on S is exact.
`
$\lambda$只需要满足：
$$\sum_j \lambda_j dx^j = 0 \\
\frac{\partial\lambda_j}{\partial s_k} = \frac{\partial\lambda_k}{\partial s_j} \  \forall j,k \in \{1, 2, ..., n_i\}
$$

## LambdaRank应用至RankNet
给定一对文档，对于其中一个文档，cost为两者的乘积：

1. RankNet Cost:
$$C_{i, j}^R = s_j - s_i + log(1+e^{s_i-s_j})\\
\partial C_{ij} / \partial o_{ij} = -1/(1+e^{o_{ij}})
$$
该计算为pairwise的，只基于该对文档的信息。无论之前排序是否正确，只要$s_j － s_i$增大（如果$s_j$ < $s_i$），cost就会减少。
2. 假设两个文档排序互换能得到的NDCG gain，$\triangle NDCG$

$$N_i = n_i\sum_{j=1}^L (2^{rel(j)} - 1)/log(1+j) \\
\triangle N_i = n_i (2^{l_i} - 2^{l_j})
(\frac{1}{log(1+i)} - \frac{1}{log(1+j)})$$
该计算基于整个查询的返回结果。

两个gradient相乘得到$\lambda$
$$\lambda = N(\frac{1}{1+e^{s_i-s_j}})
(2^{l_i} - 2^{l_j})
(\frac{1}{log(1+i)} - \frac{1}{log(1+j)})$$

