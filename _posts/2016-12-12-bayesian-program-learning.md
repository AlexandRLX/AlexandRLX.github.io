---
title: 贝叶斯规划学习
author: c cm
layout: post
permalink: /bayesian_program_learning/
categories: 机器学习
tags:贝叶斯
description:
---

最新一期的《环球科学》将贝叶斯规划学习（Bayesian program learning，简称BPL）评为2016年十大创新之一。找到其源头[Human-level concept learning through probabilistic program induction](http://web.mit.edu/cocosci/Papers/Science-2015-Lake-1332-8.pdf)科普一下。

人类学习的两个特点还没有被现在state-of-art的机器学习获得：
1. 大多数算法还是data-hungry的
2. 基于少数样本的强大推断能力：
    * 创建新样本
    * 将整体分为部分，获得部分间联系
    * 根据已有类别创建新的抽象
