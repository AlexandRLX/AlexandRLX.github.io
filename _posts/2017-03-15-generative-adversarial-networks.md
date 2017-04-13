---
title: Generative Adversarial Networks
author: c cm
layout: post
permalink: /generative_adversarial_networks/
categories:
tags:
description:
---

生成模型：用从分布$p_{data}$采样得到的训练集，学习估计出该分布的模型。形式可以是估计出分布$p_{model}$，也可以是学会生成$p_{model}$的样本。

## 1 生成模型优点

* 生成模型和强化学习关系密切。model-based强化学习中就包含生成模型。比如可用来学习根据现在state和action，生成未来state的分布；使用生成学习来模拟，还能减少因为错误action导致的实际惩罚；GAN可以用来做inverse reinforcement learning。
* 生成模型对缺失值友好，并可以对缺失值提供估计。生成模型可以用来semi-supervised learning。
* 生成模型，特别是GAN，使得机器学习可能输出multi-modal结果。


## 2 生成模型简介
Maximum likelihood estimation  

### 1. Explicit density models  

#### Tractable density
* Fully visible belief networks 缺点效率不高，生成样本时不能并行
$$p_{model}(\textbf{x}) = \prod_{i=1}^np_{model}(x_i|x_1, ..., x_{i-1})$$

* nonlinear independent components analysis 缺点对g限制过多
$$p_x = p_z(g^{-1}(x))|det\frac{\partial g^{-1}(x)}{\partial x}|$$

#### Approximate density
* Variational
    Variational autoencoder
    Lower bound $$L(x; \theta) \le log p_{model} (x;\theta)$$
    缺点：approximate posterior distribution或者prior distribution比较弱的时候，即使优化再好，$p_{model}$和$p_{data}$中间的差距也较大。

* Markov Chain
    eg. Boltzmann machine
    缺点：1. 收敛较慢 2. 高维情况下，效率不高；即使非高维，比one-step的生成模型的计算成本也更高
    

### 2. Implicity density 

* Markov Chain, eg.generative stochastic network
* Direct, eg.GAN

## 3 GANs与其他生成模型对比

优点  
* 并行产生sample，vs FVBN
* 生成函数的假设较少, vs Boltzmann machine, ICA
* 不需要Markov chains, vs Boltzmann machine, GSN
* 没有variational bound, vs VAE

缺点
* 需要找到博弈的纳什均衡，比直接优化目标函数要难


## 4 GANs简介
### 1 框架
两个player的博弈：1. generator, 2. discriminator


## 5 research frontiers in GANs

## 6 state-of-the-art image models that combine GANs with other methods
