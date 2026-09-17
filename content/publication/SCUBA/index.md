---
title: "SCUBA: Salesforce Computer Use Benchmark (ICLR, 2026)"

authors:
- Yutong Dai
- Krithika Ramakrishnan
- Jing Gu
- Matthew Fernandez
- Yanqi Luo
- Viraj Prabhu
- Zhenyu Hu
- Silvio Savarese
- Caiming Xiong
- Zeyuan Chen
- Ran Xu

date: "2025-09-30"

# Publication type.
# Legend: 0 = Uncategorized; 1 = Conference paper; 2 = Journal article;
# 3 = Preprint / Working Paper; 4 = Report; 5 = Book; 6 = Book section;
# 7 = Thesis; 8 = Patent
publication_types: ["1"]

# Publication name and optional abbreviated publication name.
publication: "International Conference on Learning Representations"
publication_short: "ICLR2026"

abstract: "We introduce SCUBA, a benchmark designed to evaluate computer-use agents on customer relationship management (CRM) workflows within the Salesforce platform. SCUBA contains 300 task instances derived from real user interviews, spanning three primary personas—platform administrators, sales representatives, and service agents. The tasks test a range of enterprise-critical abilities, including Enterprise Software UI navigation, data manipulation, workflow automation, information retrieval, and troubleshooting. To ensure realism, SCUBA operates in Salesforce sandbox environments with support for parallel execution and fine-grained evaluation metrics to capture milestone progress. We benchmark a diverse set of agents under both zero-shot and demonstration-augmented settings. We observed huge performance gaps in different agent design paradigms and gaps between the open-source model and the closed-source model. In the zero-shot setting, open-source model powered computer-use agents that have strong performance on related benchmarks like OSWorld only have less than 5% success rate on SCUBA, while methods built on closed-source models can still have up to 39% task success rate. In the demonstration-augmented settings, task success rates can be improved to 50% while simultaneously reducing time and costs by 13% and 16%, respectively. These findings highlight both the challenges of enterprise tasks automation and the promise of agentic solutions. By offering a realistic benchmark with interpretable evaluation, SCUBA aims to accelerate progress in building reliable computer-use agents for complex business software ecosystems."

# Summary. An optional shortened abstract.
summary: ""

# Is this a selected publication? (true/false)
tags:
- Benchmark
- Computer Use Agents
featured: false

links:
url_pdf: https://proceedings.iclr.cc/paper_files/paper/2026/file/29c8c615b3187ee995029284702d3f43-Paper-Conference.pdf
url_code: https://sfrcua.github.io/SCUBA/
url_poster: poster_scuba.pdf
url_media: https://hicglobalsolutions.com/blog/salesforce-scuba-agentic-ai-enterprise-automation/


# Custom links (optional).
#   Uncomment line below to enable. For multiple links, use the form `[{...}, {...}, {...}]`.
# url_custom = [{name = "Custom Link", url = "http://example.org"}]


# Does this page contain LaTeX math? (true/false)
math: false
---
