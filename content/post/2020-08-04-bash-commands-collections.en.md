---
title: bash commands collection
author: Yutong Dai
date: '2020-08-04'
slug: bash-commands-collection
categories:
  - shell
tags: []
subtitle: ''
summary: ''
authors: []
lastmod: '2020-08-04T11:51:43-04:00'
toc: true
---

### Find files with specific patterns

```bash
# This command find files with name has `news20` in the current directory and all of its sub-directories.
find . -name '*news20*'
# This command find and delete files with name has `news20` in the current directory and all of its sub-directories.
find . -name '*news20*' -delete
```

### Show file size

```bash
ls -l --block-size=M
```
