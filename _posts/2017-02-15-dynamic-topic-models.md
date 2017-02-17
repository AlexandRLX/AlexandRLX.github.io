---
title: Dynamic Topic Models
author: c cm
layout: post
permalink: /dynamic_topic_models/
categories: paper
tags:
description:
---
## 1. Dynamic Topic Model

### 1. Static Topic Model

eg. LDA  
$\beta_{1:K}$ K topics, multinomial distribution of fixed volcabulary

Generative Process:

1. Choose topic proportions θ from a distribution over the (K − 1)-simplex, such as a Dirichlet.
2. For each word:
    1. Choose a topic assignment $Z ∼ Mult(\theta)$  
    2. Choose a word $W ∼ Mult(\beta_z)$. 
    
assumption:
documents are drawn exchangeably from the same set of topics.

### 2. Dynamic Topic Model

assumption: 
    topics evolve from last time period topics

Generative Process:

1. Draw topics in a state space model that evolves with Gaussian noise $$\beta_t|\beta_{t−1} ∼ N (\beta_{t−1}, \sigma^2I)$$
2. Draw document specific topic proportion $$\alpha_t|\alpha_{t−1} ∼ N (\alpha_{t−1}, \delta^2I) $$
3. For each document:
    1. Draw $\eta∼N(\alpha_t, a^2I)$
    2. For each word:
        1. Draw $Z ∼ Mult(\pi(\eta))$.
        2. Draw $W_{t,d,n} ∼ Mult(\pi(\beta_{t,z}))$.
        * ($pi(x) = \frac{exp(x)}{\sum exp(x)}$)

## 2. Approximate Inference

### 1. Static Topic Model

Gibbs Sampling

### 2. Dynamic Topic Model

Con: nonconjugacy of the Gaussian and multinomial models

**variational methods**:  
optimize the free parameters of a distribution over the latent variables so that the distribution is close in Kullback-Liebler (KL) divergence to the true posterior; this distribution can then be used as a substitute for the true posterior.

#### 1. Kalman Filter

TBC

#### 2. Wavelet Regression

TBC
