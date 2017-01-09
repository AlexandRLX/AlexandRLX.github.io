---
title: Listwise Approach to Learning to Rank - Theory and Algorithm
author: c cm
layout: post
permalink: /listwise_approach_to_learning_to_rank_theory_and_algorithm/
categories: paper
tags: L2R RankCosine ListNet ListMLE
description:
---

## Listwise定义

1. In ranking, the input is a set of objects, the output is a permutation of the objects, the model is a ranking function which maps a given input to an output. 
$$ X: input\ space;\ x: sets\ of\ objects\ to\ be\ ranked \\
Y: output\ space;\ y: permutations\ of\ objects \\
P_{XY}: joint\ probability\ distribution\\
H: hypothesis\ space;\ h: X \to Y \ ranking\ function $$  

2. In learning, the training data $S = \{(x^{(i)}), y^{(i)})\}_{i=1}^m$ is drawn i.i.d. according to an unknown but fixed joint probability distribution between input and output $ P(x, y)$.
  
    for pointwise approach:  
    $$S = \{(x_i, y_i)\}_{i=1}^m, l = \sum_{i=1}^m l(f; x_i, y_i)$$ 
    for pairwise approach:  
    $$S = \{(x_i, x_j): y_i > y_j\}, l = \sum_{(x_i, x_j) \in S} l(f; x_i, x_j, y_i, y_j)$$  
    for listwise approach:  
    $$S = \{(x_1, ..., x_m, \overset{permutation}y)\}, l = \sum_{(x_i, x_j) \in S} l(f; x_1, ..., x_m, y)$$  


3. Ideally we would minimize the expected 0 − 1 loss defined on the predicted list and the ground truth list.  
$$minimize\ R(h) = \int_{X \times Y} l(h(x), y) dP(x, y) \\
h_{BEST}(x) = \underset{y \in Y}{argmax}\ P(y|x)$$
Practically we instead manage to minimize an empirical surrogate loss with respect to the training data.

$$empirical\ R_S(h) = \frac 1 m \sum_{i=1}^m  l(h(x^{(i)}), y^{(i)}) \\
h(x^{(i)}) = sort(g(x_1^{(i)}), ..., g(x_{n_i}^{(i)}));\ g: scoring\ function$$

$$surrogate R_S^\phi(g) = \frac 1 m \sum_{i=1}^m  \phi(g(x^{(i)}), y^{(i)})$$


## 三种surrogate loss:

1. Cross Entropy Loss (ListNet, ICML 2007)  
    the listwise loss function is defined as cross entropy between two parameterized probability distributions of permutations; one is obtained from the predicted result and the other is from the ground truth.
    $$l(f; z, y) = -\sum_{\forall\pi\in Y}P(\pi|z; g_y) logP(\pi|z;f) \\
    P(\pi|z; g_y) = \prod_{i=1}^m\frac{\phi(g_y(x_{\pi(i)}))}{\sum_{j=1}^m\phi(g_y(x_{\pi(i)}))}\\
    P(\pi|z;f) = \prod_{i=1}^m\frac{\phi(f(x_{\pi(i)}))}{\sum_{j=1}^m\phi(f(x_{\pi(i)}))}
    $$

2. Cosine Loss(RankCosine, IPM 2007)  
    the listwise loss function is defined on the basis of cosine similarity between two score vectors from the predicted result and the ground truth.
    $$l(f; z, y) = \frac 1 2 (1 - \frac{\phi(g_y(z))^T\phi(f(z))}{\|\phi(g_y(z))\|\ \|\phi(f(z))\|})$$
    [wiki: cosine similarity](https://en.wikipedia.org/wiki/Cosine_similarity)


3. Likelihood loss (ListMLE, this paper)
    $$l(f; z, y) = -log P(y|z; f) \\
    P(y|z; f) = \prod_{i=1}^m\frac{\phi(f(x_{y(i)}))}{\sum_{j=1}^m\phi(f(x_{y(i)}))}$$


## 评价Surrogate Loss Function

1. **consistency**  
    obtained ranking function can converge to the optimal one, when the training sample size goes to infinity. 

2. **soundness**  
    the loss can represent well the targeted learning problem. That is, an incorrect prediction should receive a larger penalty than a correct prediction, and the penalty should reflect the confidence of prediction.
    
3. **continuity, differentiability, and convexity**

4. **computational efficiency**

Loss|Continuity|Differentiability|Convexity|Efficiency
---|---|---|---|---
Cosine Loss (RankCosine)    |√|√|X|O(n)Cross-entropy loss (ListNet)|√|√|√|O(n·n!)Likelihood loss (ListMLE)   |√|√|√|O(n)

