---
title: Adapting Boosting for Information Retrieval Measures
author: c cm
layout: post
permalink: /adapting_boosting_for_information_retrieval_measures/
categories: paper
tags: RankMART, Boosting
description:
---
## RankMART思路
结合LambdaRank和MART(Multiple Additive Regression Trees)思想：

1. 每次boosting迭代只有一棵树，这棵树用LambdaRank中的gradients来训练。优点：比McRank减少训练时间，可以优化NDCG这样的非光滑指标。需要解决的问题：传统MART的cost function是根据一条观测计算的，LambdaRank中cost function是成对计算的。
 
2. 利用boosted trees的相加特性，将第一棵树用一个事先训练好的模型替代，解决model adaptation的问题。

3. 对任意两个排序系统，根据任意IR指标，找到最佳线性组合的方法。

## LambdaSMART algorithm

for i = 0 to N do \\\\N为文档总个数  

for m = 1 to M do \\\\总共迭代M次  
　　　　$γ_{lm} = \frac{\sum_{x_i \in R_{lm}} y_i}{\sum_{x_i \in R_{lm}} w_i}$ \\\\根据牛顿法寻找叶值  
　　for i=0 to N do  
end for

## 排序系统最佳组合

$$s_i = (1-\alpha)s_i^{R_1} + \alpha s_i^{R_2} \\
\alpha \in [0, 1]
$$

NDCG只在下图中2条或2条以上线相交时，才会变化。
我们可以计算出所有使得NDCG变化的$\alpha$，及在每个导致NDCG变化的具体情况。
![combine_ranker](http://iccm.cc/img/combine_ranker.png)


