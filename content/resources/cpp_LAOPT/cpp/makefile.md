---
title: Compile your program
linktitle: Compile your program
toc: true
type: docs
date: "2020-08-16"
lastmod: "{{ .Lastmod }}"
draft: false
menu:
  cpp_LAOPT:
    parent: Elements of C++
    weight: 2
# Prev/next pager order (if `docs_section_pager` enabled in `params.toml`)
weight: 1
---

# Compile your code in command line


> Reference: Pitt-Francis, J., & Whiteley, J. (2017). Guide to Scientific Computing in C++ Secon Edition. Springer.

```
compiler [-flag1 -flag2 ...] -o excutableFileName sourceCodeFile
```

* Compiler: `g++`
* Compiler flags:
    - `-Wall`: list out anything unexpected that is not actually an error, but will still create an executable file.
    - `-O`: (upper case `o`): optimize the executable file at the cost of longer compilation time
    - `-g`: compile code with debugging information preserved
    - `-o`: use this to allow name the excutable file name

* Inputs:
    - `excutableFileName`: the parameter provided to the flag `-o`
    - `sourceCodeFile`: the `cpp` file which you want to compile
    
```bash
g++ -Wall -O -o addTwoNumbers addTwoNumbers.cpp
```
