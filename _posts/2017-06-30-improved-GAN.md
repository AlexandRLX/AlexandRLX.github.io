---
title: Improved GAN
author: c cm
layout: post
permalink: /improved_gan/
categories:
tags: paper
description:
---

# Convergent GAN

## 1. feature matching ~= maximum mean discrepancy

Feature matching addresses the instability of GANs by specifying a new objective for the generator that prevents it from overtraining on the current discriminator.


p.2: we train the generator to match the expected value of the features on an intermediate layer of the discriminator. 

p.2: Letting f (x) denote activations on an intermediate layer of the discriminator, our new objective for the generator is defined as: ||Ex∼pdata f(x) − Ez∼pz(z)f(G(z))||2. The discriminator, and hence f(x)


## 2. mini batch features ~= batch normalization

p.3: One of the main failure modes for GAN is for the generator to collapse to a parameter setting where it always emits the same point. 

p.3: The concept of minibatch discrimination is quite general: any discriminator model that looks at multiple examples in combination, rather than in isolation, could potentially help avoid collapse of the generator. 

one example:

## 3. historical averaging

p.3: When applying this technique, we modify each player’s cost to include a term ||θ − 1  t θ[i]||2, t i=1where θ[i] is the value of the parameters at past time i.

[fictitious play](https://en.wikipedia.org/wiki/Fictitious_play)

## 4. one-sided label smoothing

0/1->0/0.9

## 5. virtual batch normalization

p.4: normalized based on the statistics collected on a reference batch of examples that are chosen once and fixed at the start of training

# Assessment of image quality

# semi-supervised learning
