+++
title = "Synchronous Parallel Block Coordinate Descent Method for Nonsmooth Convex Function Minimization (To appear.)"
date = 2019-01-01T00:00:00
draft = false

# Authors. Comma separated list, e.g. `["Bob Smith", "David Jones"]`.
authors = ["Dai, Yutong", "Weng, Yang"]

# Publication type.
# Legend:
# 0 = Uncategorized
# 1 = Conference paper
# 2 = Journal article
# 3 = Manuscript
# 4 = Report
# 5 = Book
# 6 = Book section
publication_types = ["2"]

# Publication name and optional abbreviated version.
publication = "In *Journal of Systems Science and Complexity*, JSSC."

# Abstract and optional shortened version.
abstract = "In this paper, we propose a synchronous parallel block coordinate descent algorithm(PSUM) for minimizing a composite function, which consists of a smooth convex function plus a non-smooth but separable convex function. Due to the generalization of our method, some existing synchronous parallel algorithms can be considered as special cases. To tackle high dimensional problems, we further develop a randomized variant, which randomly update some blocks of coordinates at each round of computation. Both proposed parallel algorithms are proven to have sub-linear convergence rate under rather mild assumptions. The numerical experiments on solving the large scale regularized logistic regression with $l_1$ norm penalty show that the implementation is quite efficient. We conclude with explanation on the observed experimental results and discussion on the potential improvements."

# Is this a selected publication? (true/false)
selected = true

# Projects (optional).
#   Associate this publication with one or more of your projects.
#   Simply enter your project's folder or file name without extension.
#   E.g. `projects = ["deep-learning"]` references 
#   `content/project/deep-learning/index.md`.
#   Otherwise, set `projects = []`.
projects = []

# Tags (optional).
#   Set `tags = []` for no tags, or use the form `tags = ["A Tag", "Another Tag"]` for one or more tags.
tags = []

# Links (optional).
# url_pdf = "http://eprints.soton.ac.uk/352095/1/Cushen-IMV2013.pdf"
url_preprint = "https://github.com/Rothdyt/Projects/blob/master/Thesis-Collection/psum.pdf"
# url_code = "#"
# url_dataset = "#"
# url_project = ""
# url_slides = "#"
# url_video = "#"
# url_poster = "#"
# url_source = "#"

# Custom links (optional).
#   Uncomment line below to enable. For multiple links, use the form `[{...}, {...}, {...}]`.
# url_custom = [{name = "Custom Link", url = "http://example.org"}]

# Digital Object Identifier (DOI)
doi = ""

# Does this page contain LaTeX math? (true/false)
math = true

# Featured image
# To use, add an image named `featured.jpg/png` to your page's folder. 
[image]
  # Caption (optional)
  # caption = "Image credit: [**Unsplash**](https://unsplash.com/photos/pLCdAaMFLTE)"

  # Focal point (optional)
  # Options: Smart, Center, TopLeft, Top, TopRight, Left, Right, BottomLeft, Bottom, BottomRight
  # focal_point = ""
+++

More detail can easily be written here using *Markdown* and $\rm \LaTeX$ math code.
