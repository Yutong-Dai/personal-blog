---
title: "Inexact Proximal-Gradient Methods with Support Identification"

authors:
- Yutong Dai
- Daniel P. Robinson

date: "2022-11-04"

# Publication type.
# Legend: 0 = Uncategorized; 1 = Conference paper; 2 = Journal article;
# 3 = Preprint / Working Paper; 4 = Report; 5 = Book; 6 = Book section;
# 7 = Thesis; 8 = Patent
publication_types: ["3"]

# Publication name and optional abbreviated publication name.
publication: ""
publication_short: ""

abstract: We consider the proximal-gradient method for minimizing an objective function that is the sum of a smooth function and a non-smooth convex function. A feature that distinguishes our work from most in the literature is that we assume that the associated proximal operator does not admit a closed-form solution. To address this challenge, we study two adaptive and implementable termination conditions that dictate how accurately the proximal-gradient subproblem is solved. We prove that the number of iterations required for the inexact proximal-gradient method to reach a $\tau>0$ approximate first-order stationary point is $\mathcal{O}(\tau^{-2})$, which matches the similar result that holds when exact subproblem solutions are computed. Also, by focusing on the overlapping group regularizer, we propose an algorithm for approximately solving the proximal-gradient subproblem, and then prove that its iterates identify (asymptotically) the support of an optimal solution. If one imposes additional control over the accuracy to which each subproblem is solved, we give an upper bound on the maximum number of iterations before the support of an optimal solution is obtained.

# Summary. An optional shortened abstract.
summary: ""

# Is this a selected publication? (true/false)
tags:
- Inexact Proximal Gradient Methods
- Overlapping Group Regularizer
- Support Identification

featured: true

links:
url_preprint: https://arxiv.org/pdf/2211.02214.pdf

# Custom links (optional).
#   Uncomment line below to enable. For multiple links, use the form `[{...}, {...}, {...}]`.
# url_custom = [{name = "Custom Link", url = "http://example.org"}]


# Does this page contain LaTeX math? (true/false)
math: true
---
