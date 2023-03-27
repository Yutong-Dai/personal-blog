---
title: "A Variance-Reduced and Stabilized Proximal Stochastic Gradient Method with Support Identification Guarantees for Structured Optimization (AISTATS, 2023)"

authors:
- Yutong Dai
- Guanyi Wang
- Frank E. Curtis
- Daniel P. Robinson

date: "2023-01-18"

# Publication type.
# Legend: 0 = Uncategorized; 1 = Conference paper; 2 = Journal article;
# 3 = Preprint / Working Paper; 4 = Report; 5 = Book; 6 = Book section;
# 7 = Thesis; 8 = Patent
publication_types: ["1"]

# Publication name and optional abbreviated publication name.
publication: "Artificial Intelligence and Statistics "
publication_short: "AISTATS2023"

abstract: 

# Summary. An optional shortened abstract.
summary: "This paper introduces a new proximal stochastic gradient method with variance reduction and stabilization for minimizing the sum of a convex stochastic function and a group sparsity-inducing regularization function. Since the method may be viewed as a stabilized version of the recently proposed algorithm PStorm, we call our algorithm S-PStorm. Our analysis shows that S-PStorm has strong convergence results. In particular, we prove an upper bound on the number of iterations required by S-PStorm before its iterates correctly identify (with high probability) an optimal support (i.e., the zero and nonzero structure of an optimal solution). Most algorithms in the literature with such a support identification property use variance reduction techniques that require either periodically evaluating an exact gradient or storing a history of stochastic gradients. Unlike these methods, S-PStorm achieves variance reduction without requiring either of these, which is advantageous. Moreover, our support-identification result for S-PStorm shows that, with high probability, an optimal support will be identified correctly in all iterations with the index above a threshold. We believe that this type of result is new to the literature since the few existing other results prove that the optimal support is identified with high probability at each iteration with a sufficiently large index (meaning that the optimal support might be identified in some iterations, but not in others). Numerical experiments on regularized logistic loss problems show that S-PStorm outperforms existing methods in various metrics that measure how efficiently and robustly iterates of an algorithm identify an optimal support."

# Is this a selected publication? (true/false)
tags:
- Variance Reduction
- Support Identification
- Nonsmooth Optimizaiton

featured: true

links:
url_arxiv: https://arxiv.org/abs/2302.06790
url_code: https://github.com/Yutong-Dai/S-PStorm
url_poster: "Poster_SPSTORM.pdf"
# url_slides: "Slides_FedNH.pdf"
# url_video: "https://drive.google.com/file/d/12W5ImDBhcYEk52FXJWVH13uZFWzY85Kk/view?usp=share_link"

# Custom links (optional).
#   Uncomment line below to enable. For multiple links, use the form `[{...}, {...}, {...}]`.
# url_custom = [{name = "Custom Link", url = "http://example.org"}]


# Does this page contain LaTeX math? (true/false)
math: true
---
