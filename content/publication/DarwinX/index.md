---
title: "DarwinX: Evolving Agent Harnesses Through Natural Selection (arXiv, 2026)"

authors:
- Yifan Zhang
- Yutong Dai
- Juntao Tan 
- Luyu Yang
- Rishi Mullur
- Thai Hoang
- Zhiyuan Hu
- James Zhu
- Phil Mui
- Silvio Savarese
- Ran Xu
- Zeyuan Chen

date: "2026-07-31"

# Publication type.
# Legend: 0 = Uncategorized; 1 = Conference paper; 2 = Journal article;
# 3 = Preprint / Working Paper; 4 = Report; 5 = Book; 6 = Book section;
# 7 = Thesis; 8 = Patent
publication_types: ["3"]

# Publication name and optional abbreviated publication name.
publication: "arxiv"
publication_short: "arxiv"

abstract: "An LLM agent's capability depends not only on model weights but on its harness: prompts, tools, skills, and control flow. Self-improvement loops already edit harnesses, yet single-lineage search is path-dependent and local wins often regress other tasks. We introduce DarwinX, which treats self-evolution as selection over a population of harnesses with the model frozen: a preserve-and-extend contract admits only variants that extend coverage without regressing, an archive keeps alternative lineages for recombination, and failure-, teacher-, and self-derived evidence share one edit interface. Fitness comes from each benchmark's own verifier: no gold solutions, no hand-picked winners. Across four benchmarks that progressively separate the evolution signal from the test, one loop adds about 17 points on average: Terminal-Bench 2.1 rises +7.7 to 83.2% on a matched base and to the verified frontier at 84.7% on a stronger one; TerminalWorld's held-out split reaches 68.3%, ahead of every off-the-shelf agent; WebArena-Infinity real-task pass@1 rises from 43.5% to 93.0% audit-clean; and a Terminal-Bench 2.1 harness transfers unchanged to SWE-bench Verified. What evolves is general agent competence, not benchmark-specific patches, so it survives changes of task, verifier, and base model. A frozen model need not be a fixed agent: harness selection turns evaluation compute into durable capability."

# Summary. An optional shortened abstract.
summary: ""

# Is this a selected publication? (true/false)
tags:
- Agent Harness
- Recursive Self Improving
featured: false

links:
url_pdf: https://arxiv.org/pdf/2608.07545
url_code: https://github.com/SalesforceAIResearch/Beagle
url_media: https://venturebeat.com/orchestration/salesforce-researchers-took-an-ai-agent-from-finishing-43-5-of-browser-tasks-to-93-without-touching-the-model


# Custom links (optional).
#   Uncomment line below to enable. For multiple links, use the form `[{...}, {...}, {...}]`.
# url_custom = [{name = "Custom Link", url = "http://example.org"}]


# Does this page contain LaTeX math? (true/false)
math: false
---
