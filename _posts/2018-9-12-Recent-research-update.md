---
layout: post
title: Research update- QP and ecology
mathjax: true
comments: true
---

Recently we posted an article on arxiv about a suprising duality between optimization problem with inequality constraints, particularly quadratic programming (QP), and one of the most famous models of ecological dynamics, MacArthur's Consumer Resource Model (MCRM). Here I want to provide a very gentle introduction to some basic ideas in optimization and convex duality, which we invoked upon in this paper, appease physicsists who might get annoyed by these jargons.  

Simply put, optimization problems involve finding the extreme values (maximum of minimum) of a given (real) function $f(x)$ within an allow set of $x$. Formally, the geric form of optimization is as follows:

$$ & \underset{x}{\text{min}}
& & f(x) \\
& \text{subject to}
& & h_i(x) \leq 0, \; i = 1, \ldots, m.\\
&&& l_j(x) =0, \; j=1, \ldots, r.$$