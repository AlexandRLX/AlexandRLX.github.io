---
title: Recent Advances in Convolutional Neural Networks
author: c cm
layout: post
permalink: /recent_advances_in_convolutional_neural_networks/
categories: paper
tags: CNN
description:
---

## 1. Introduction
基本结构：

1. input layer
    * first layer
    
2. convolutional layer
    * aims to learn feature representations of the inputs. The activation function introduces nonlinearities to CNN.
    
3. pooling layer  
    * aims to achieve shift-invariance by reducing the resolution of the feature maps.
    * between convolutional layers, 
    
4. fully-connected layer
    * aims to perform high-level reasoning.
    * take all neurons in the previous layer and connect them to every single neuron of current layer to generate global semantic information.

5. output layer
    * last layer

## 2. Improvements

### 1. Convolutional Layer
* Tiled Convolution
* Transposed Convolution
* Dilated Convolution
* Network in Network
* Inception Module

### 2. Pooling Layer
* $L_p$ Pooling  
    Average Pooling和Max Pooling的一般形式
* Mixed Pooling  
    Average Pooling和Max Pooling的加权
* Stochastic Pooling  
    拟合multinomial分布，抽样pooling
* Spectral Pooling
* Spatial Pyramid Pooling
* Multi-scale Orderless Pooling

### 3. Activation Function
* ReLU(Recitified Linear Unit)
    $$a_{i,j,k} = max(z_{i,j,k}, 0)$$
* Leaky ReLU
    $$a_{i,j,k} = max(z_{i,j,k}, 0) + \lambda min(z_{i,j,k}, 0)$$
* Parametric ReLU
    $$a_{i,j,k} = max(z_{i,j,k}, 0) + \lambda_k min(z_{i,j,k}, 0)$$
* Randomized ReLU
    $$a_{i,j,k}^{(n)} = max(z_{i,j,k}^{(n)}, 0) + \lambda_k^{(n)} min(z_{i,j,k}^{(n)}, 0)$$
* ELU(Exponential Linear Unit)
    $$a_{i,j,k} = max(z_{i,j,k}, 0) +  min(\lambda(e^{z_{i,j,k}}-1), 0)$$
* Maxout
    $$a_{i,j,k} = max_{k\in[1,K]}z_{i,j,k}$$
* Probout

### 4. Loss Function
* Hinge Loss
* Softmax Loss／Large-Margin Softmax
* Contrastive Loss
* Triplet Loss  
    anchor/positive/negative pair
    $$L = \frac{1}{n}\sum_{i=1}^N max\{d_{(a,p)}^{(i)} － d_{(a,n)}^{(i)}\}$$
* KL Divergence/JSD

### 5. Regularization
* lp-norm
* Dropout  
    随机将neuron的输出置为0
* DropConnect  
    随机将学习到的weight置为0

### 6. Optimization
* Data Augmentation
* Weight Initialization
* Stochastic Gradient Descent
* Batch Normalization
* Shortcut Connections

## 3. Fast processing of CNN

* FFT
* Structured Transforms
* Low Precision
* Weight Compression
* Sparse Convolution
