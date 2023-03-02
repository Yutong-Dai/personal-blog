---
title: Tackling Data Heterogeneity in Federated Learning with Class Prototypes
event: AAAI'2023
# event_url: https://www.abstractsonline.com/pp8/#!/10693/presentation/6549
location: Washington, DC, United States
summary: Talk about how to tackle data heterogeneity in federated learning by leveraging the class prototypes.
abstract: "Data heterogeneity across clients in federated learning (FL) settings is a widely acknowledged challenge. In response, personalized federated learning (PFL) emerged as a framework to curate local models for clients’ tasks. In PFL, a common strategy is to develop local and global models jointly - the global model (for generalization) informs the local models, and the local models (for personalization) are aggregated to update the global model. A key observation is that if we can improve the generalization ability of local models, then we can improve the generalization of global models, which in turn builds better personalized models. In this work, we consider class imbalance, an overlooked type of data heterogeneity, in the classification setting. We propose FedNH, a novel method that improves the local models’ performance for both personalization and generalization by combining the uniformity and semantics of class prototypes. FedNH initially distributes class prototypes uniformly in the latent space and smoothly infuses the class semantics into class prototypes. We show that imposing uniformity helps to combat prototype collapse while infusing class semantics improves local models. Extensive experiments were conducted on popular classification datasets under the cross-device setting. Our results demonstrate the effectiveness and stability of our method over recent works."

# Talk start and end times.
#   End time can optionally be hidden by prefixing the line with `#`.
date: "2023-02-11T18:15:00Z"
date_end: "2022-02-11T20:15:00Z"
all_day: false

# Schedule page publish date (NOT talk date).
publishDate: "2017-01-01T00:00:00Z"

authors: []
tags: []

# Is this a featured talk? (true/false)
featured: true

# image:
#   caption: 'Image credit: [**Unsplash**](https://unsplash.com/photos/bzdhc5b3Bxs)'
#   focal_point: Right

# links:
# - icon: twitter
#   icon_pack: fab
#   name: Follow
#   url: https://twitter.com/georgecushen
# url_code: ""
url_pdf: ""
url_slides: "main.pdf"
url_video: ""

# Markdown Slides (optional).
#   Associate this talk with Markdown slides.
#   Simply enter your slide deck's filename without extension.
#   E.g. `slides = "example-slides"` references `content/slides/example-slides.md`.
#   Otherwise, set `slides = ""`.
# slides: example

# Projects (optional).
#   Associate this post with one or more of your projects.
#   Simply enter your project's folder or file name without extension.
#   E.g. `projects = ["internal-project"]` references `content/project/deep-learning/index.md`.
#   Otherwise, set `projects = []`.
# projects:
# - internal-project

# Enable math on this page?
math: true
---

