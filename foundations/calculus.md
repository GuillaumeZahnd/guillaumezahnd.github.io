---
layout: default
title: Calculus
nav_order: 3
parent: Foundations
grand_parent: Home
has_children: false
---

# Calculus

## Gradient

Given a scalar-valued function $$f:\mathbb{R}^n \rightarrow \mathbb{R}$$, the gradient $$\nabla_\mathbf{x} f(\mathbf{x})$$ is defined as:

$$\nabla_\mathbf{x} f(\mathbf{x}) = \frac{\partial f}{\partial \mathbf{x}}$$

{: .note-title }
> Note
>
> - The gradient of a function $$f$$ with respect to a vector $$\mathbf{x} \in \mathbb{R}^n$$ is the vector of its partial derivatives, representing the direction of steepest ascent and the magnitude of that rate of change at a given point.

## Jacobian

Given a vector-valued function $$\mathbf{f} : \mathbb{R}^n \rightarrow \mathbb{R}^m$$, the Jacobian is the $$m \times n$$ matrix $$J$$ that captures how every component of the output $$(f_1​,f_2, \cdots,f_m​)$$ changes with respect to every component of the input $$(x_1​, x_2, \cdots,x_n​)$$.

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

$$\frac{\partial f_j}{\partial x_i} = \frac{\partial f_j(x_1, x_2, \dots, x_j, \dots, x_n)}{\partial x_i}$$

## Derivative

| Type | Function | Derivative |
| --- | --- | --- |
| **Power rule** | $$f(x) = x^n$$ | $$f'(x) = nx^{n-1}$$ |
| **Exponential** | $$f(x) = e^{x}$$ | $$f'(x) = e^x$$ |
| **Natural log** | $$f(x) = \ln(x)$$ | $$f'(x) = \frac{1}{x}$$ |
| **Inverse** | $$x = f(y)$$ | $$\frac{dy}{dx} = \frac{1}{f'(y)}$$ |
| **Absolute** | $$f(x) = \mid x \mid$$ | $$f'(x) = \text{sign}(x)$$ |
| **Generalized power** | $$h(x) = [f(x)]^n$$ | $$h'(x) = n[f(x)]^{n-1} \cdot f'(x)$$ |
| **Composition** | $$h(x) = f\Big(g(x)\Big) = (f \circ g)(x)$$ | Chain rule:<br><br>$$h'(x) = f'\Big(g(x)\Big)\cdot g'(x)$$ |
| **Product** | $$h(x) = f(x)g(x)$$ | $$h'(x) = f'(x)g(x) + f(x)g'(x)$$|
| **Quotient** | $$f(x) = \frac{a(x)}{b(x)}$$ | $$f'(x) = \frac{a'(x)b(x) - a(x)b'(x)}{b(x)^2}$$ |
| **Sigmoid** | $$S(x) = \frac{1}{1 + e^{-x}}$$ | $$S'(x) = S(x) \cdot \Big(1 - S(x)\Big)$$ |
| **Softmax** | $$\sigma(\mathbf{z})\_i = \frac{e^{z_i}}{\sum_{k=1}^{K} e^{z_k}}$$ | Case 1, $$i=j$$ (diagonal):<br><br>$$\frac{\partial \sigma(z)_i}{\partial z_i} = \sigma(z)_i\Big(1 - \sigma(z)_i\Big)$$<br><br>Case 2, $$i \neq j$$ (off-diagonal):<br><br>$$\frac{\partial \sigma(z)_i}{\partial z_j} = -\sigma(z)_i \sigma(z)_j$$ |

## Single-variable chain rule

Given:

$$y = (g \circ f)(x) = g(f(x))$$

### Leibnitz notation

$$\frac{dy}{dx} = \frac{dy}{du} \cdot \frac{du}{dx}\quad\text{with}~y=g(u)~\text{and}~u=f(x)$$

### Functional notation

$$(g \circ f)'(x) = g'(f(x)) \cdot f'(x)$$

### Matrix notation

$$J_{g \circ f} = J_g \cdot J_f$$

{: .important-title }
> Important
>
> - The single-variable chain rule applies under the condition that there is a single path of dependency from $$x$$ to $$y$$ (e.g., $$x \rightarrow u \rightarrow y$$). In other words, changes in the input $$x$$ can influence the output $$y$$ in only one way, none of the intermediate subexpression functions (e.g., $$u(x)$$ and $$y(u)$$) have more than one parameter.

## Taylor series

A function $$f$$ can be approximated to order $$n$$ around $$x=a$$ using the $$n$$-th degree Taylor polynomial $$P_n​(x)$$:

$$f(x) \approx P_n​(x) = \sum_{k=0}^{n} \frac{f^{(k)}(a)}{k!} (x-a)^k$$
