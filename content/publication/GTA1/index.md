---
title: "GTA1: GUI Test-time Scaling Agent (arixv, 2025)"

authors:
- Yan Yang
- Dongxu Li
- Yutong Dai
- Yuhao Yang
- Ziyang Luo
- Zirui Zhao
- Zhiyuan Hu
- Junzhe Huang
- Amrita Saha
- Zeyuan Chen
- Ran Xu
- Liyuan Pan
- Silvio Savarese
- Caiming Xiong
- Junnan Li

date: "2025-07-08"

# Publication type.
# Legend: 0 = Uncategorized; 1 = Conference paper; 2 = Journal article;
# 3 = Preprint / Working Paper; 4 = Report; 5 = Book; 6 = Book section;
# 7 = Thesis; 8 = Patent
publication_types: ["3"]

# Publication name and optional abbreviated publication name.
publication: "arXiv."
publication_short: "arXiv"

abstract: "Graphical user interface (GUI) agents autonomously complete tasks across platforms (e.g., Linux) by sequentially decomposing user instructions into action proposals that iteratively interact with visual elements in the evolving environment. However, two main challenges arise: i) planning (i.e., the action proposal sequence) under expansive action space, where selecting an appropriate plan is nontrivial, as many valid ones may exist; ii) accurately grounding actions in complex and high-resolution interfaces, i.e., precisely interacting with visual targets. This paper investigates the aforementioned
challenges with our GUI Test-time Scaling Agent, namely GTA1. First, we conduct test-time scaling to select the most appropriate action proposal: at each step, multiple candidate proposals are sampled and evaluated and selected by a judge model. It trades off computation for better decision quality by concurrent sampling. Second, we propose a model that improves grounding of the selected action proposals to its corresponding visual elements. Our key insight is that reinforcement learning (RL) facilitates grounding through inherent objective alignments, rewarding successful clicks on interface elements. Experimentally, GTA1 achieves state-of-the-art performance on both grounding and agent task execution benchmarks."

# Summary. An optional shortened abstract.
summary: ""

# Is this a selected publication? (true/false)
tags:
- Benchmark
- Computer Use Agents
featured: false

links:
url_code: https://github.com/Yan98/GTA1
url_pdf: https://arxiv.org/pdf/2507.05791


# Custom links (optional).
#   Uncomment line below to enable. For multiple links, use the form `[{...}, {...}, {...}]`.
# url_custom = [{name = "Custom Link", url = "http://example.org"}]


# Does this page contain LaTeX math? (true/false)
math: false
---
