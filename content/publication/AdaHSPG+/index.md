---
title: "An Adaptive Half-Space Projection Method for Stochastic Optimization Problems with Group Sparse Regularization (TMLR, 2023)"

authors:
- Yutong Dai
- Tianyi Chen
- Guanyi Wang
- Daniel P. Robinson

date: "2023-06-01"

# Publication type.
# Legend: 0 = Uncategorized; 1 = Conference paper; 2 = Journal article;
# 3 = Preprint / Working Paper; 4 = Report; 5 = Book; 6 = Book section;
# 7 = Thesis; 8 = Patent
publication_types: ["2"]

# Publication name and optional abbreviated publication name.
publication: "*Transactions on Machine Learning Research*."
publication_short: "TMLR"

abstract: "Optimization problems with group sparse regularization are ubiquitous in various popular downstream applications, such as feature selection and compression for Deep Neural Networks (DNNs). Nonetheless, the existing methods in the literature do not perform particularly well when such regularization is used in combination with a stochastic loss function. In particular, it is challenging to design an algorithm that is computationally efficient, has a convergence guarantee, and is able to compute group-sparse solutions. Recently, a half-space stochastic projected gradient (HSPG)  method was proposed that partly addressed these challenges. In this paper, we present a substantially enhanced version of  HSPG that we call~ AdaHSPG+ that makes two noticeable advances. First,  AdaHSPG+ is shown to have a stronger convergence result under significantly looser assumptions than those required by  HSPG. This improvement in convergence is achieved by integrating variance reduction techniques with a new adaptive strategy for iteratively predicting the support of a solution. Second,  AdaHSPG+ requires significantly less parameter tuning compared to  HSPG, thus making it more practical and user friendly. This advance is achieved by designing automatic and adaptive strategies for choosing the type of step employed at each iteration and for updating key hyperparameters. The numerical effectiveness of our proposed  AdaHSPG+ algorithm is demonstrated on both convex and non-convex benchmark problems."

# Summary. An optional shortened abstract.
summary: ""

# Is this a selected publication? (true/false)
tags:
- Nonconvex Sparse Optimization
- Neural Network Compression
featured: true

links:
url_pdf: https://openreview.net/forum?id=KBhSyBBeeO

# Custom links (optional).
#   Uncomment line below to enable. For multiple links, use the form `[{...}, {...}, {...}]`.
# url_custom = [{name = "Custom Link", url = "http://example.org"}]


# Does this page contain LaTeX math? (true/false)
math: true
---
