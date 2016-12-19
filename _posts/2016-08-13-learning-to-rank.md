---
title: 排序模型L2R
author: c cm
layout: post
permalink: /learning_to_rank/
categories: 机器学习
tags:
description:
---
排序模型(learning to rank)在信息检索（information retrieval）、协同过滤（collabrative filtering）中应用广泛。和之前博客中的对参赛选手排名问题不太一样。

一般把这个问题描述为：对查询query q和一组文档documents di，对di对q的相关程度排序。

对bag of words模型，我们可以这样衡量相关程度：
$$sim(q, d) \triangleq p(q|d) = \prod_{i=1}^{n}p(q_i|d)$$
其中，$q_i$是query中的第i个词，$p(q_i|d)$是multinoulli分布。

如果用Dirichlet先验，

$$p(t|d) = (1-\lambda)\frac{TF(t, d)}{LEN(d)} + \lambda p(t|background)$$

## pointwize approach
过程：

1. 对每个document $d_j$，构造特征$x(q, d_j)$。
2. 从历史CTR(具体见[*Optimizing Search Engines using Clickthrough Data*](http://iccm.cc/optimizing_search_engines_using_clickthrough_data/))，或其它相关结果中构造目标$y_i$。
3. y可以是二维的（经典分类问题）$p(y=1|x(q,d))$，也可以是有序的$p(y=r|x(q,d))$。
4. 预测出y的分值后，对其进行排序

缺点：
分析与document的位置无关，比较短视（myopical）。

## pairwize approach
比pointwize不同，pairwize比较两个document相关程度哪个更大：
$$p(y_{jk}|x(q, d_j), x(q, d_k))$$
$y_{jk} = 1 \ if \ rel(d_j, q) > rel(d_k, q)\ else\ 0$

如果以下式建模，那么可以看为是神经网络RankNet：
$$p(y_{jk}=1|x_j, x_k) = sigm(f(x_j) - f(x_k))$$

缺点：只两两比较，比较局部。

## listwize approach
首先考虑Plackett-Luce分布：
$$p(\pi|s) = \prod_{j=1}^m\frac{s_j}{\sum_{u=j}^m s_u}$$

其中$s_j = s(\pi^{-1}(j))$是排在第j位的分数。算法ListNet的思路中，将$s(d) = f(x(q, d)) = w^Tx$

## L2R模型评价指标
1. Mean reciprocal rank(MRR)
    定义query最相关文档的排序为r(q)，MRR = 1/r(q)。
        
2. Mean average precision(MAP)
    定义k处的精度P为：
    $$P@k(\pi)\triangleq \frac{num.\ relevant\ documents\ in\ the\ top k\ positions\ of \pi}{k}$$
    平均精度为AP：
    $$AP(\pi)\triangleq\frac{\sum_k P@k(\pi) I_k}{num.\ relevant\ documents}$$

3. Normalized discounted cumulative gain(NDCG)
    $$DCG@k(r) = r_1 + \sum_{i=2}^k \frac{r_i}{log_2 i}$$
    其中ri是i的相关程度。
4. Rank correlation
    直接衡量预测排序和实际排序之间的相关程度。多种统计学检验都可以，比如Kendall's $\tau$。
    
## 相关论文推荐
0. Joachims, T. (2002). Optimizing Search Engines using Clickthrough Data, 1–10.
1. Zhai and La erty (2004) Zhai, C. and J. La erty (2004). A study of smoothing methods for language models applied to infor- mation retrieval. ACM Trans. on In- formation Systems 22(2), 179–214.
2. Burges, C. J., T. Shaked, E. Renshaw, A. Lazier, M. Deeds, N. Hamilton, and G. Hullender (2005). Learning to rank using gradient descent. In Intl. Conf. on Machine Learning, pp. 89–96.
3. Cao, Z., T. Qin, T.-Y. Liu, M.-F. Tsai, and H. Li (2007). Learning to rank: From pairwise approach to listwise approach. In Intl. Conf. on MachineLearning, pp. 129âA ̆S ̧136.
4. Xia, F. (2008). Listwise Approach to Learning to Rank - Theory and Algorithm, 1–8.
5. Carterette, B., P. Bennett, D. Chicker- ing, and S. Dumais (2008). Here or There: Preference Judgments for Relevance. In Proc. ECIR.
6. Liu, T.-Y. (2009). Learning to rank for information retrieval. Founda- tions and Trends in Information Retrieval 3(3), 225–331.
7. Usunier, N., D. Bu oni, and P. Galli- nari (2009). Ranking with ordered weighted pairwise classification.
8. Zhang, X., T. Graepel, and R. Herbrich (2010). Bayesian Online Learning for Multi-label and Multi-variate Performance Measures. In AI/Statis- tics.
9. Zheng, Z. (2016). A Regression Framework for Learning Ranking Functions Using Relative Relevance Judgments, 1–8.
 

* http://www.bing.com/community/site_blogs/b/search/archive/2009/06/01/user-needs-f eatures-and-the-science-behind-bing.aspx






[ref]MLAPP 9.7
