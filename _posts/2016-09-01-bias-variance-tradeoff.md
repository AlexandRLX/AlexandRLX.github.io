---
title: 偏差方差权衡
author: c cm
layout: post
permalink: /bias_variance_tradeoff/
categories: 机器学习
tags:
description:
---
中文有些奇怪，实际是我们非常熟悉的bias variance tradeoff。是指

$$expected loss = bias^2 + variance + noise$$

其中，

$$bias^2 = \int \{E_D[y(x;D)] - h(x)\}^2p(x)dx$$

$$variance = \int E_D[\{y(x;D) - E_D[y(x;D)]\}^2]p(x)dx$$

$$noise = \int \{h(x) -t\}^2p(x,t)dxdt$$


noise是即使我们知道“真实”的模型，也由于数据噪音导致的不能减少的误差。


注意不要和统计学中的TSS = ESS + RSS搞混，和上面的对应关系是： 

    TSS = expected loss
    ESS = bias^2 + variance
    RSS = noise

![img](http://www.kdnuggets.com/wp-content/uploads/bias-and-variance.jpg)
