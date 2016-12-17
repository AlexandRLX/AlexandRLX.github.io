---
title: Optimizing Search Engines using Clickthrough Data
author: c cm
layout: post
permalink: /optimizing_search_engines_using_clickthrough_data/
categories: 机器学习
tags: 论文
description:
---

2002 by Thorsten Joachims
关键词：ranking, CTR, SVM

问题表述为：给定查询q和文档集$D = \{d_1, ..., d_m \}$，找到最优的retrieval system，其应该根据文档和查询的相关性给出最佳排序$r^*$。本文提出利用CTR数据和SVM方法，在risk minimization框架下学习retrival functions。

CTR数据由三部分组成(q, r, c)。
q为查询，可以理解为关键字的组合，更广义可以将用户偏好及信息状态包含进来。
r为向用户展示的排名，c为用户的点击行为。要注意，c是基于r的。一般用户可能只会点击排名前十的链接，排名靠后且未被点击未必代表其与q无关。

CTR信息中虽然推断不出绝对的相关度排名，但是能让我们了解相对的相关度关系。比如总共展示了1－5，5个链接。用户点击了链接2，4。虽然不知道2和4谁应该排名较高，但是我们知道（一个从前往后看的）用户应该看到了链接1-4，据此得出$r_2 < r_1$, $r_4 < r_1, r_4 < r_3$。

正式的，
p.3: Algorithm 1. (Extracting Preference Feedback from Clickthrough)
For a ranking $(link_1 , link_2 , link_3 , ...)$ and a set C containing the ranks of the clicked-on links, extract a preference example $$link_i <_{r^*} link_j \\ for\ all\ pairs\ 1 ≤ j < i, with\ i \in C \ and\ j\notin C$$



