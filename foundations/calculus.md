---
layout: default
title: Calculus
nav_order: 3
parent: Foundations
grand_parent: Home
has_children: false
---

# Calculus

## Jacobian

Given a vector-valued function $$\mathbf{f} : \mathbb{K}^n \rightarrow \mathbb{K}^m$$, the Jacobian is the $$m \times n$$ matrix $$J$$ that captures how every component of the output $$(f_1​,f_2, \cdots,f_m​)$$ changes with respect to every component of the input $$(x_1​, x_2, \cdots,x_n​)$$.

$$\mathbf{x} = \begin{bmatrix} 
x_1 \\ 
x_2 \\ 
\vdots \\ 
x_n 
\end{bmatrix}$$

$$\mathbf{f}(\mathbf{x}) = \begin{bmatrix} 
f_1(x_1, \dots, x_n) \\ 
f_2(x_1, \dots, x_n) \\ 
\vdots \\ 
f_m(x_1, \dots, x_n) 
\end{bmatrix}
= \begin{bmatrix} 
y_1 \\ 
y_2 \\ 
\vdots \\ 
y_m
\end{bmatrix} = \mathbf{y}$$

$$J = \begin{bmatrix} \nabla f_1 \\ \nabla f_2 \\ \vdots \\ \nabla f_m \end{bmatrix} = \begin{bmatrix} \frac{\partial f_1}{\partial x_1} & \frac{\partial f_1}{\partial x_2} & \cdots & \frac{\partial f_1}{\partial x_n} \\ \frac{\partial f_2}{\partial x_1} & \frac{\partial f_2}{\partial x_2} & \cdots & \frac{\partial f_2}{\partial x_n} \\ \vdots & \vdots & \ddots & \vdots \\ \frac{\partial f_m}{\partial x_1} & \frac{\partial f_m}{\partial x_2} & \cdots & \frac{\partial f_m}{\partial x_n} \end{bmatrix}$$

with

$$\displaystyle \frac{\partial f_j}{\partial x_i} = \frac{\partial f_j(x_1, x_2, \dots, x_j, \dots, x_n)}{\partial x_i}$$
