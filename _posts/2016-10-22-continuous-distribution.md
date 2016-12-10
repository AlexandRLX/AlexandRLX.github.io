---
title: 连续分布
author: c cm
layout: post
permalink: /continuous_distribution/
categories: 
tags: 统计
description:
---
## 高斯分布
$$N(x|\mu, \sigma^2) \triangleq \frac{1}{\sqrt{2\pi\sigma^2}}e^{-\frac{(x-\mu)^2}{2\sigma^2}}$$
优点：
1. 只有两个参数，描述了分布的最基础性质。
2. 根据中心极限定理，随机向量之和趋向于高斯分布。所以其比较适合作为噪声或者残差的模型。l2正则可以看为先验为高斯的map。
3. 给定均值和方差后，高斯分布有最大熵。是假设最少的分布。

缺点：
对数据集中的异常点比较敏感

##学生t分布
$$T(x|\mu, \sigma^2, v) \propto [1 + \frac{1}{v}(\frac{x-\mu}{\sigma})^2]^{-\frac{v+1}{2}}$$
均值和众数是$\mu$，方差为$\frac{v\sigma^2}{v-2}$
$v$为自由度，$v\gg5$时，趋于高斯分布
优点：比高斯分布对异常点更鲁棒
缺点：不是log-concave的

##拉普拉斯分布
$$Lap(x|\mu, b) \triangleq \frac{1}{2b}exp(-\frac{|x-\mu|}{b})$$
其均值和众数为$\mu$, 方差为$2b^2$
优点：
其pdf在0值时很高，容易获得稀疏性。l1正则可以看为先验为拉普拉斯的map。

##gamma分布
$$Ga(T|shape=a, rate=b) \triangleq \frac{b^a}{\Gamma(a)}T^{a-1}e^{-Tb}$$
$$\Gamma(x) \triangleq \int_{0}^\infty u^{x-1}e^{-u}du$$
其均值为a/b，众数为(a-1)/b，方差为a/b^2

##beta分布
$$Beta(x|a,b) = \frac{1}{B(a,b)}x^{a-1}(1-x)^{b-1}$$
$$B(a,b) \triangleq \frac{\Gamma(a)\Gamma(b)}{\Gamma(a+b)}$$

##帕累托分布
$$Pareto(x|k,m) = km^kx^{-(k+1)}I(x\ge m)$$