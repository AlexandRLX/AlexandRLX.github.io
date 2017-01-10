---
title: Jacobian矩阵
author: c cm
layout: post
permalink: /jacobian_matrix/
categories: Calculus
tags: 
description:
---
$$y = f(x)$$

**Jacobian matrix** describing the amount of "stretching", "rotating" or "transforming" that a transformation imposes locally.

$$J_{x\to y} 
\triangleq \frac{\partial(y_1, ..., y_n)}{\partial(x_1, ..., x_n)} 
\triangleq
\begin{equation}       
\left(                 
  \begin{array}{ccc} 
    \partial y_1/\partial x_1 & ... & \partial y_1/\partial x_n\\  
    ... & ... & ...\\
    \partial y_n/\partial x_1 & ... & \partial y_n/\partial x_n\\  
  \end{array}
\right)                
\end{equation}
$$

**Jacobian determinant**衡量apply f后，单位x有多少改变
$$J = |det J_{x \to y}|$$

如果f可逆，
$$p_y(y) = p_x(x) |det \frac{\partial x}{\partial y}|   = p_x(x)|det J_{x \to y}|$$

示例 polar-Cartesian transformation
$$\mathbf{x} = (x_1, x_2) \ \mathbf{y} = (r, \theta) \\
 x_1 = r cos\theta\ x_2 = r sin \theta$$
 then
 $$J_{y \to x} = 
     \begin{equation}       
    \left(                 
      \begin{array}{c} 
        cos\theta & -rsin\theta \\
        sin\theta & rcos\theta \\
      \end{array}
    \right)                
    \end{equation}
 $$

$$|det J_{y \to x}| = |r|$$

$$p_y(y) = p_x(x) |det J_{y \to x}| = p_x(x) r \\
p_{r, \theta}(r, \theta) = p_{x_1, x_2}(x_1, x_2)r = p_{x_1, x_2}(rcos\theta, rsin\theta)r$$

[wiki](https://en.wikipedia.org/wiki/Jacobian_matrix_and_determinant)
[Hessian matrix](https://en.wikipedia.org/wiki/Jacobian_matrix_and_determinant)


