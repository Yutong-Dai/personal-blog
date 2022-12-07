---
title: "Tackling Data Heterogeneity in Federated Learning with Class Prototypes"

authors:
- Yutong Dai
- Zeyuan Chen
- Junnan Li
- Shelby Heinecke
- Lichao Sun
- Ran Xu

date: "2022-12-06"

# Publication type.
# Legend: 0 = Uncategorized; 1 = Conference paper; 2 = Journal article;
# 3 = Preprint / Working Paper; 4 = Report; 5 = Book; 6 = Book section;
# 7 = Thesis; 8 = Patent
publication_types: ["1"]

# Publication name and optional abbreviated publication name.
publication: "Association for the Advancement of Artificial Intelligence"
publication_short: "AAAI2023"

abstract: Data heterogeneity across clients in federated learning (FL) settings is a widely acknowledged challenge. In response, personalized federated learning (PFL) emerged as a framework to curate local models for clients' tasks. In PFL, a common strategy is to develop local and global models jointly - the global model (for generalization) informs the local models, and the local models (for personalization) are aggregated to update the global model. A key observation is that if we can improve the generalization ability of local models, then we can improve the generalization of global models, which in turn builds better personalized models. In this work, we consider class imbalance, an overlooked type of data heterogeneity, in the classification setting. We propose FedNH, a novel method that improves the local models' performance for both personalization and generalization by combining the uniformity and semantics of class prototypes. FedNH initially distributes class prototypes uniformly in the latent space and smoothly infuses the class semantics into class prototypes. We show that imposing uniformity helps to combat prototype collapse while infusing class semantics improves local models. Extensive experiments were conducted on popular classification datasets under the cross-device setting. Our results demonstrate the effectiveness and stability of our method over recent works.

# Summary. An optional shortened abstract.
summary: ""

# Is this a selected publication? (true/false)
tags:
- Federated Learning
- Data Heterogeneity
- Class Imbalance
- Prototype

featured: true

links:
url_pdf: https://arxiv.org/abs/2212.02758

# Custom links (optional).
#   Uncomment line below to enable. For multiple links, use the form `[{...}, {...}, {...}]`.
# url_custom = [{name = "Custom Link", url = "http://example.org"}]


# Does this page contain LaTeX math? (true/false)
math: true
---
