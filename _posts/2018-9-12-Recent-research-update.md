---
layout: post
title: Research update- QP and ecology [to-be-finished]
mathjax: true
comments: true
---

Recently we posted an article on arxiv about a suprising duality between optimization problem with inequality constraints, particularly quadratic programming (QP), and one of the most famous models of ecological dynamics, MacArthur's Consumer Resource Model (MCRM). Here I want to provide a very gentle introduction to some basic ideas in optimization and convex duality, which we invoked upon in this paper, appease physicsists who might get annoyed by these jargons.  


## Definition of QP

Simply put, optimization problems involve finding the extreme values (maximum of minimum) of a given (real) function $f(x)$ within an allow set of $x$. It formally takes the following form:

$$ 
\begin{equation}
\begin{aligned}
& \underset{x\in D}{\text{min}}
& & f(x) \\
& \text{subject to}
& & h_i(x) \leq 0, \; i = 1, \ldots, m\\
&&& l_j(x) =0, \; j=1, \ldots, r,
\end{aligned}
\end{equation}$$

where $D = \text{dom}(f)\cap\bigcap_{i=1}^m \text{dom}(h_i)\bigcap_{j=1}^r \text{dom}(l_j)$. The function $f$ is called the objective function while $h_i$ and $l_j$ are the constraints. We call a problem convex when $f$ and $h_i$ are all convex functions of $x$ and $l_j$ is an affine (therefore convex) function of $x$. In this paper, we're concerned with a particular type of convex optimization called the (convex) quadratic programming (QP) where $f(x)=c^T x+ \frac{1}{2}x^T Q x$ with $Q\succeq 0$ being a positive semi-definite matrix. Formally, a convex QP is defined as:

$$ 
\begin{equation}
\begin{aligned}
& \underset{x}{\text{min}}
& & c^T x+ \frac{1}{2}x^T Q x \\
& \text{subject to}
& & D_i x \leq d_i, \; i = 1, \ldots, m\\
&&& A_j(x) =b_j, \; j=1, \ldots, r,
\end{aligned}
\end{equation}$$


### Examples of QP

QP has applications across disciplines. For in example, one can formulate **portfolio optimization** as QP:


$$ 
\begin{equation}
\begin{aligned}
& \underset{x}{\text{min}}
& & \mu^T x -\frac{\gamma}{2}x^TQx \\
& \text{subject to}
& & x\ge 0\\
&&& 1^T x =1,
\end{aligned}
\end{equation}
$$

with the following interpretation:

  * $\mu$: expected assets' return
  * $Q$: covariance matrix between assets' return
  * $\gamma$: risk aversion
  * $x$: percentage portfolio holdings

Another notable example is the [Support Vector Machine](https://en.wikipedia.org/wiki/Support_vector_machine):

 Given $y\in\{-1,1\}, X \in \mathbb{R}^{n\times p}$ with rows $x_1,\cdots, x_n$. A support vector machine (SVM) problem is defined as:

 $$ 
\begin{equation}
\begin{aligned}
& \underset{\beta, \beta_0,\xi}{\text{min}}
& & \frac{1}{2}||\beta||_2^2 + C\sum_{i=1}^n \xi_i \\
& \text{subject to}
& & \xi_i\ge 0,\; i = 1, \ldots, n\\
&&& y_i(x_i^T\beta+\beta_0)\ge 1-\xi_i, \; i = 1, \ldots, n
\end{aligned}
\end{equation}
$$


## Convex Duality
