---
title: 逻辑回归
author: c cm
layout: post
permalink: /logistic_regression/
categories: 机器学习
tags:
description:
---


1. 基本模型（二元）
对条件概率建模：$$P(y=1|x) = \frac{exp(w \cdot x)}{1 + exp(w \cdot x)} $$
y=1的对数几率(log odds/logit)为 $log \frac{p}{1 - p}＝w \cdot x$


2. 参数估计方法
    一般fit方式为极大似然法maximum likelihood，对其负对数似然函数（cross-entropy error）求极小值，就能得到参数$w$的估计值。具体求解可用梯度下降法（一阶偏导）／牛顿法（二阶偏导）／拟牛顿法来求解，见后。
    似然函数为$$L=\prod p(x_i)^{y_i} \cdot (1 - p(x_i))^{1- y_i}$$
    
    一阶偏导
    $$\nabla E(w) = \sum(y_n - t_n) \phi_n = \Phi^T(y-t)$$
    海赛矩阵$$H(x) = [\frac{\partial^2f}{\partial x_i\partial x_j}]_{n\times n} = \nabla\nabla E(w) = \Phi^TR\Phi$$
    其中$R_{nn} = diag(y_n(1-y_n))$。
    
    加入惩罚项后，$$L(w) = E(w) + P(w) = E(w) + \lambda w^Tw$$
    一阶偏导$$\nabla E(w) = \nabla E(w) ＋ \lambda w$$
    海赛矩阵$$H(x) = H(x) + \lambda I$$
    极大似然法是频率学派distriminative approach的主要方法，比bayesian approach：
    * 优点：要fit的参数更少；在generative approach中密度函数估计错误的情况下预测效果更好
    * 缺点：训练数据线性可分时会过拟，通过加入先验或惩罚项可以避免

    1. 梯度下降
    2. 牛顿法 [wiki](https://en.wikipedia.org/wiki/Newton's_method_in_optimization)
    假设：目标函数为凸函数有二阶连续偏导数，海赛矩阵必须正定，那么每次迭代：
    $w^{(new)} = w^{old} - H^{-1}\nabla E(w)$
    推导主要用了二阶泰勒展开及$E(w)$极值处一阶导为0的性质。  
    对逻辑回归，代入后得$w^{(new)} = w^{old} - (\Phi^TR\Phi)^{-1}\Phi^T(y-t)
                    = (\Phi^TR\Phi)^{-1}\Phi^TRz$，
    其中$z = \Phi w^{old} - R^{-1}(y-t)$  
     * 因为上式中R需要根据w而更新，所以此算法被称为IRLS(iterative reweighted least squares)。  
     * 对比线性回归模型中，$w^{(new)}= (\Phi^T\Phi)^{-1}\Phi^Tt$，可以认为IRLS是在空间$w^T\phi$中，预测有效target $z$ 的线性问题。  
    
    
    3. 拟牛顿法
    牛顿法的缺点是：每次迭代都需要计算海赛矩阵的逆矩阵$H^{-1}$，计算比较复杂。拟牛顿法寻找$H^{-1}$或$H$的近似矩阵来简化运算。
    近似矩阵需要满足拟牛顿条件：
    $$\nabla E(w)_{k+1} - \nabla E(w)_k = H_k (w_{k+1} - w_k)$$
    记$y_k=\nabla E(w)_{k+1} - \nabla E(w)_k$, $s_k=w_{k+1} - w_k$，上式可写为：$$y_k = H_{k+1}s_k$$或$$s_k = H^{-1}y_k$$
    DFP算法对海赛矩阵逆矩阵做估计，记为$G_k$，找到了迭代方式G_{k+1} ＝ f(G_k, s_k, y_k)。
    更常用的是BFGS/L-BFGS算法，对海赛矩阵直接做估计，记为$B_k$，找到了迭代方式$B_{k+1} ＝ f(B_k, s_k, y_k)$。
    BFGS也可以看作是对海赛矩阵做"diagonal plus low-rank"[Low-rank approximation例子](https://inst.eecs.berkeley.edu/~ee127a/book/login/exa_low_rank_4by5.html)近似。
    L-BFGS的L是指limited memory，不保存海赛矩阵的近似矩阵，保留m个迭代中产生的向量。可以这么
    拟牛顿法假设可导，所以只适应于$l_2$惩罚项。由于$l_1$惩罚在0点处不可导，所以微软利用其在各象限可导的性质，提出了OWL-QN(Orthant-Wise Limited-memory Quasi-Newton)。和L-BFGS比，主要有4点不同：
     1. The pseudo-gradient ⋄f (xk ) of the regularized objective is used in place of the gradient.
     2. The resulting search direction is constrained to match the sign pattern of vk = − ⋄ f(xk). This is the projection step of Equation 3.
     3. During the line search, each search point is projected onto the orthant of the previous point.
     4. The gradient of the unregularized loss alone is used to construct the vectors yk used to approximate the inverse Hessian.
    

3. 和其他模型对比  
逻辑回归比线性回归的优点是：预测永远在0～1之间，作为概率更合理。 
逻辑回归和LDA(linear discriminant analysis)比较类似，一般在这些情况下选LDA，会比逻辑回归结果更稳定:
 * classes分的比较开的时候
 * n比较小而且x服从正态分布时
 * 多分类问题更常用

