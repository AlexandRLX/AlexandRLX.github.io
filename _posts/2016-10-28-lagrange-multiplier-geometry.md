---
title: 拉格朗日乘子法的几何意义
author: c cm
layout: post
permalink: /lagrange_multiplier_geometry/
categories: 
tags: 机器学习
description:
---
optimize: $f(x)$
s.t.: $g(x)=0$

两点结论：
    1. 将$g(x)＝0$看做D-1维surface，那么$\nabla g(x)$垂直于该surface。
    2. 在约束surface上寻找最优点$x^*$，那么在该点$\nabla f(x)$也垂直于该surface。

基于以上两点，可知$\nabla g(x)$和$\nabla f(x)$平行，所以存在$\lambda$，使得$\nabla f(x) + \lambda \nabla g(x) = 0$

![img](http://mathworld.wolfram.com/images/eps-gif/LagrangeMultipliers_1000.gif)