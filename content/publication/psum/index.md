---
title: "Synchronous Parallel Block Coordinate Descent Method for Nonsmooth Convex Function Minimization (JSSC, 2019)"

authors:
- Yutong Dai
- Yang Weng

date: "2019-04-01"

# Publication type.
# Legend: 0 = Uncategorized; 1 = Conference paper; 2 = Journal article;
# 3 = Preprint / Working Paper; 4 = Report; 5 = Book; 6 = Book section;
# 7 = Thesis; 8 = Patent
publication_types: ["2"]

# Publication name and optional abbreviated publication name.
publication: "*Journal of Systems Science and Complexity*."
publication_short: "JSSC"

abstract: "In this paper, we propose a synchronous parallel block coordinate descent algorithm(PSUM) for minimizing a composite function, which consists of a smooth convex function plus a non-smooth but separable convex function. Due to the generalization of our method, some existing synchronous parallel algorithms can be considered as special cases. To tackle high dimensional problems, we further develop a randomized variant, which randomly update some blocks of coordinates at each round of computation. Both proposed parallel algorithms are proven to have sub-linear convergence rate under rather mild assumptions. The numerical experiments on solving the large scale regularized logistic regression with $l_1$ norm penalty show that the implementation is quite efficient. We conclude with explanation on the observed experimental results and discussion on the potential improvements."

# Summary. An optional shortened abstract.
summary: ""

# Is this a selected publication? (true/false)
tags:
- Convex Optimization
- Block Cooridinate Descent
featured: true

links:
url_pdf: https://link.springer.com/content/pdf/10.1007/s11424-020-8313-y.pdf

# Custom links (optional).
#   Uncomment line below to enable. For multiple links, use the form `[{...}, {...}, {...}]`.
# url_custom = [{name = "Custom Link", url = "http://example.org"}]


# Does this page contain LaTeX math? (true/false)
math: true
---
