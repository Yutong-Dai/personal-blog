---
title: Using the right kernel for Jupyter Notebook
author: Yutong Dai
date: '2020-03-28'
slug: using-the-right-kernel-for-jupyter-notebook
categories:
  - Python-Programming
tags:
  - jupyter
  - kernel
subtitle: ''
summary: ''
authors: []
lastmod: '2020-03-28T17:22:55-04:00'
featured: no
image:
  caption: ''
  focal_point: ''
  preview_only: no
projects: []
---

```
# create virtual env with python 3.7.7, whose name is cuppy
conda create -n cuppy numpy scipy pandas notebook matplotlib python=3.7.7 
# activate cuppy
conda activate cuppy
# I am using zsh, you may change to bash
conda init zsh 
# activate virtual env
cond activate cuppy
# point this verison of Python to jupyter
ipython kernel install --name "cuppy" --user
```