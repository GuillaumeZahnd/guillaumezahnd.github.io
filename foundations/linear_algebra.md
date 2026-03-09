---
layout: default
title: Linear algebra
nav_order: 3
parent: Foundations
grand_parent: Home
has_children: false
---

# Linear algebra

## Dot product

The dot product of two vectors $$\mathbf{a} = [a_1, a_2, \cdots, a_n]$$ and $$\mathbf{b} = [b_1, b_2, \cdots, b_n]$$ is defined as:

$$\begin{align}
\mathbf{a} \cdot \mathbf{b} &:= \sum_{i=1}^{n} a_i b_i \\
&=\left\|\mathbf{a}\right\| \left\|\mathbf{b}\right\| \cos\theta \quad \text{where } \theta \text{ is the angle between } \mathbf{a} \text{ and } \mathbf{b}
\end{align}$$

> [!NOTE]
> - The dot product is a scalar value that measures the extent to which one vector aligns with another.

## Eigenvector and eigenvalues

Let $$A$$ be a square matrix. A non-zero vector $$\mathbf{v}$$ is an eigenvector of $$A$$ if there exists a scalar $$\lambda$$ (an eigenvalue) such that $$A\mathbf{v} = \lambda \mathbf{v}$$. 

- An eigenvector $$\mathbf{v}$$ preserves its line of action under the linear transformation $$A$$ (it is only scaled).
- An eigenvalue $$\lambda$$ represents the scaling factor of the corresponding eigenvector under the linear transformation $$A$$.

> [!NOTE]
> - A matrix $$A \in \mathbb{K}^{n \times n}$$ has exactly $$n$$ eigenvalues (counted with multiplicity) in $$\mathbb{C}$$, and at most $$n$$ distinct ones.
> - Eigenvalues are the roots of the *characteristic equation* $$\det(A - \lambda I) = 0$$.
> - Diagonalization theorem: $$A \in \mathbb{K}^{n \times n}$$ is diagonalizable if and only if
it has $$n$$ linearly independent eigenvectors (that is, they form a basis of $$\mathbb{K}^{n}$$).

## Trace

The trace of a $$n \times n$$ square matrix $$A$$ is the sum of its diagonal elements.

$$tr(A) := \sum_{i=1}^n a_{ii}$$
