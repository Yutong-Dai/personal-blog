---
title: "Local-Global Knowledge Distillation in Heterogeneous Federated Learning with Non-IID Data"

authors:
- Dezhong Yao 
- Wanning Pan
- Yutong Dai
- Yao Wan
- Xiaofeng Ding
- Hai Jin
- Zheng Xu
- Lichao Sun

date: "2021-09-13"

# Publication type.
# Legend: 0 = Uncategorized; 1 = Conference paper; 2 = Journal article;
# 3 = Preprint / Working Paper; 4 = Report; 5 = Book; 6 = Book section;
# 7 = Thesis; 8 = Patent
publication_types: ["3"]

# Publication name and optional abbreviated publication name.
publication: ""
publication_short: ""

abstract: Federated learning enables multiple clients to collaboratively learn a global model by periodically aggregating the clients' models without transferring the local data. However, due to the heterogeneity of the system and data, many approaches suffer from the "client-drift" issue that could significantly slow down the convergence of the global model training. As clients perform local updates on heterogeneous data through heterogeneous systems, their local models drift apart. To tackle this issue, one intuitive idea is to guide the local model training by the global teachers, i.e., past global models, where each client learns the global knowledge from past global models via adaptive knowledge distillation techniques. Coming from these insights, we propose a novel approach for heterogeneous federated learning, namely FedGKD, which fuses the knowledge from historical global models for local training to alleviate the "client-drift" issue. In this paper, we evaluate FedGKD with extensive experiments on various CV/NLP datasets (i.e., CIFAR-10/100, Tiny-ImageNet, AG News, SST5) and different heterogeneous settings. The proposed method is guaranteed to converge under common assumptions, and achieves superior empirical accuracy in fewer communication runs than five state-of-the-art methods.

# Summary. An optional shortened abstract.
summary: ""

# Is this a selected publication? (true/false)
tags:
- federated learning
- knowledge distillation
- data heterogeneity
featured: false

links:
url_preprint: https://arxiv.org/pdf/2107.00051.pdf

# Custom links (optional).
#   Uncomment line below to enable. For multiple links, use the form `[{...}, {...}, {...}]`.
# url_custom = [{name = "Custom Link", url = "http://example.org"}]


# Does this page contain LaTeX math? (true/false)
math: true
---
