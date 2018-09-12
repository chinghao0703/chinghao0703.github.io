---
layout: post
title: Research update- QP and ecology
mathjax: true
comments: true
---

Recently we posted an article on arxiv about a suprising duality between optimization problem with inequality constraints, particularly quadratic programming (QP), and one of the most famous models of ecological dynamics, MacArthur's Consumer Resource Model (MCRM). Here I want to provide a very gentle introduction to some basic ideas in optimization and convex duality, which we invoked upon in this paper, appease physicsists who might get annoyed by these jargons.  

Simply put, optimization problems involve finding the extreme values (maximum of minimum) of a given (real) function $f(x)$ within an allow set of $x$. Formally, the geric form of optimization is as follows:

$$ 
\begin{equation}
\begin{aligned}
& \underset{x\in D}{\text{min}}
& & f(x) \\
& \text{subject to}
& & h_i(x) \leq 0, \; i = 1, \ldots, m.\\
&&& l_j(x) =0, \; j=1, \ldots, r,
\end{aligned}
\end{equation}$$

where $D = \text{dom}(f)\cap\bigcap_{i=1}^m \text{dom}(h_i)$. The function $f$ is called the objective function. This problem is convex when $f$ and $h_i$ are all convex functions of $x$ and $l_j$ is an affine (therefore convex) function of $x$. In this paper, we're concerned with a particular type of convex optimization called the (convex) quadratic programming (QP) where $f(x)=c^T x+ \frac{1}{2}x^T Q x$ with $Q\succeq 0$ being a positive semi-definite matrix. Formally, a convex QP is defined as:

$$ 
\begin{equation}
\begin{aligned}
& \underset{x}{\text{min}}
& & c^T x+ \frac{1}{2}x^T Q x \\
& \text{subject to}
& & D_i x \leq d_i, \; i = 1, \ldots, m.\\
&&& A_j(x) =b_j, \; j=1, \ldots, r,
\end{aligned}
\end{equation}$$
