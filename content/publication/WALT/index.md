---
title: "WALT: Web agents that learn tools (ICLR, 2026)"

authors:
- Viraj Prabhu
- Yutong Dai
- Matthew Fernandez
- Krithika Ramakrishnan
- Jing Gu
- Yanqi Luo
- Caiming Xiong
- Junnan Li
- Zeyuan Chen
- Ran Xu


date: "2025-09-27"

# Publication type.
# Legend: 0 = Uncategorized; 1 = Conference paper; 2 = Journal article;
# 3 = Preprint / Working Paper; 4 = Report; 5 = Book; 6 = Book section;
# 7 = Thesis; 8 = Patent
publication_types: ["1"]

# Publication name and optional abbreviated publication name.
publication: "International Conference on Learning Representations (2026)"
publication_short: "ICLR2026"

abstract: "Web agents promise to automate complex browser tasks, but current methods remain brittle--relying on step-by-step UI interactions and heavy LLM reasoning that break under dynamic layouts and long horizons. Humans, by contrast, exploit website-provided functionality through high-level operations like search, filter, and sort. We introduce WALT (Web Agents that Learn Tools), a framework that reverse-engineers latent website functionality into deterministic, callable tools. Rather than hypothesizing ad-hoc skills, WALT exposes robust implementations of automations already designed into websites, spanning discovery (search, filter, sort), communication (post, comment, upvote), and content management (create, edit, delete). Tools abstract away low-level execution: instead of reasoning about how to click and type, agents simply call search (query) or create (listing). This shifts the computational burden from fragile step-by-step reasoning to reliable tool invocation. On VisualWebArena and WebArena, WALT achieves state-of-the-art success rates (52.9% on VisualWebArena, 50.1% on WebArena) with fewer steps and less LLM-dependent reasoning. On Online-Mind2Web, a benchmark of 139 real-world websites, WALT autonomously discovers 252 tools and improves success rate by 20.5% over a tool-free baseline, establishing a robust and generalizable paradigm for browser automation."

# Summary. An optional shortened abstract.
summary: ""

# Is this a selected publication? (true/false)
tags:
- Computer Use Agents
featured: true

links:
url_code: https://github.com/SalesforceAIResearch/WALT
url_pdf: https://proceedings.iclr.cc/paper_files/paper/2026/file/5b175f9e93873e3a10a6ce43dbb82e05-Paper-Conference.pdf
url_poster: poster_WALT.pdf
url_media: https://www.marktechpost.com/2025/10/24/salesforce-ai-research-introduces-walt-web-agents-that-learn-tools-enabling-llm-agents-to-automatically-discover-reusable-tools-from-any-website/

# Custom links (optional).
#   Uncomment line below to enable. For multiple links, use the form `[{...}, {...}, {...}]`.
# url_custom = [{name = "Custom Link", url = "http://example.org"}]


# Does this page contain LaTeX math? (true/false)
math: false
---
