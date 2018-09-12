---
layout: post
title: Research update- QP and ecology [to-be-finished]
mathjax: true
comments: true
---

Recently we posted an article on arxiv about a suprising duality between optimization problem with inequality constraints, particularly [quadratic programming (QP)](https://en.wikipedia.org/wiki/Quadratic_programming), and one of the most famous models of ecological dynamics, MacArthur's Consumer Resource Model (MCRM). Here I want to provide a very gentle introduction to some basic ideas in optimization and convex duality, which we invoked upon in this paper, appease physicsists who might get annoyed by these jargons.  


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

One might wonder why convexity matter? One obvious answer from both theoretical and algorithmic viewpoint stems from the fact that for **a convex problem, any local minimizer is a global minimizer**. This means that in the optimization procedure, as long as we're *going down the hill* and agree to stop when we can't go any further, then we've hit the global minimum. There are of course gazillions of nice property of convex problems which I refer readers to [Stephen Boyd's](https://web.stanford.edu/~boyd) book and course on [Convex Optimization](https://web.stanford.edu/~boyd/cvxbook/). 

Now having defined QP, I want to switch gear to talk about another concept that was invoked upon in this paper: convex duality.

## Convex Duality

Physicists are not that unfamiliar with the concept of duality (e.g.  AdS/CFT correspondence or gauge/gravity duality). Like many such problems, duality allows us to map a problem to its dual where solutions are more easily found. Convex duality is no exception! Recall that we just stated one simple but powerful attribute of convex problems: every local minimizer is a global minimizer. One intuitive application lies in finding the set of parameters (e.g. coupling constants) that gives rise to the ground state of a physical system. If such problem is convex, this property immediately implies that no matter what dimensionality the problem is defined in, one would never get stuck by local minima or saddales (since there's no such thing at all!) In the language of convex optimization, one similar property is: **the Lagrange dual of an optimization problem is alway convex**! As one shall see, duality also allows us to explore the property of solutions even without solving the problem itself!

### Lagrange dual