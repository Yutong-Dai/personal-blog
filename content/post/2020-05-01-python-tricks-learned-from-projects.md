---
title: Python Tricks Learned From Projects
author: Yutong Dai
date: '2020-05-01'
slug: python-tricks-learned-from-projects
categories:
  - Python-Programming
tags:
  - python
subtitle: ''
summary: ''
authors: []
lastmod: '2020-05-01T12:37:30-04:00'
featured: no
image:
  caption: ''
  focal_point: ''
  preview_only: no
projects: []
---

{{% toc %}}

# Show all submodules

I need to import a particular function `formulate` from a file in the directory `<path-to-the-package>/coinor/dippy/examples/milp/milp_func`.
It's clear that I need to import it from the submodule `coinor.dippy`. But how to do it exactly?
Use following commands, which list all submodules you can import.

```python
import pkgutil
import coinor.dippy
package=coinor.dippy
for importer, modname, ispkg in pkgutil.walk_packages(path=package.__path__,
                                                      prefix=package.__name__+'.',
                                                      onerror=lambda x: None):
    print(modname)
```
Relavant outputs are
```
.....
coinor.dippy.examples.milp
coinor.dippy.examples.milp.__main__
coinor.dippy.examples.milp.milp_func
.....
```

Then I can simply use

```python
from coinor.dippy.examples.milp.milp_func import formulate
```