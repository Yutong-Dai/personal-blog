---
title: Cornell Notes Template
linktitle: Cornellnotes
toc: true
type: docs
date: "2020-08-06"
lastmod: "{{ .Lastmod }}"
draft: false
menu:
  tex-rmd:
    parent: Overview
    weight: 1
# Prev/next pager order (if `docs_section_pager` enabled in `params.toml`)
weight: 1
---

## Demo

{{< figure src="cornell-standalone.png"  width="50%">}}

## Install
You can obtain all source code from my github [repo](https://github.com/Rothdyt/templates-for-LaTex-and-Rmd/tree/master/%5BTex%5DCornellnotes).


## Usage
Put `standalone.tex` and `note.cls` in the same folder and complie.

### Minimal Example

```tex
% in your .tex file
\documentclass[doctype=s]{note}

\title{Put your note title here.}
\author{Yutong Dai}
\date{Last Update: \today}

\usepackage{lipsum}
\usepackage[margin=1.5cm, portrait]{geometry}
\begin{document}
% \maketitle
\pre{Questions}
    {
        \begin{enumerate}
            \item{What's the first question this section will answer?}
            \item{What's the second question?}
        \end{enumerate}
    }
\note[key term 1]
    {
        \begin{itemize} 
            \item{A cool thing}
            \item{Another cool thing}
            \item{Not all things are cool}
        \end{itemize}
    }
\note[key term 2]
    {
        \lipsum[4]
    }

\note[Very very very very very very very very long head]
    {
        \lipsum[5]
    }

\summary{Summary}{A fabulous summary}
\end{document}
```

### Key components

* `\title{}`: the title for your document. If you want to leave it blank, please use `\title{}`; otherwise use `\title{your title}`.

* `\author{}`: the author for your document. If you want to leave it blank, please use `\author{}`; otherwise use `\author{your name}`.

* `\date{}`: the last modified date for your document. If you want to leave it blank, please use `\date{}`; otherwise use `\date{Last Update: \today}`.

* `\pre{}{}`: a pre read block. The first argument is the title for this block and the second argument fills in the block.

* `\note{}{}` a note bolck. The first argument records the keyword and the second argument fills the note content.

* `\summary{}{}`: a summary block. see `\pre{}{}`.

### Modes

Two modes are provided for this template,

* `standalone` mode[default]: renders the file as a stand-alone file, the one showed in demo. In this mode, when providing `title`/`author`/`date`, please do not use `\maketitle` command. These information will be automatically rendered.

* `collection` mode: Use this note as a widget, which can be direcrly incorporated in your article. Since `note` class directly inherit from the `article` class. To use `collection` mode just pass `doctype=c` to the `\documnetclass` as the demo code indicates.


  ```tex
  % in your .tex file
    \documentclass[doctype=c]{note}
    \title{Put your note title here.}
    \author{Yutong Dai}
    \date{Last Update: \today}
    \usepackage{lipsum}
    \usepackage[margin=1.5cm, portrait]{geometry}
    \begin{document}
    
    \maketitle
    \tableofcontents
    \newpage
    \section{First section}
    \pre{Questions}
        {
            \begin{enumerate}
                \item{What's the first question this section will answer?}
                \item{What's the second question?}
            \end{enumerate}
        }
    \note[key term 1]
        {
            \begin{itemize} 
                \item{A cool thing}
                \item{Another cool thing}
                \item{Not all things are cool}
            \end{itemize}
        }
    \note[key term 2]
        {
            \lipsum[4]
        }
    
    \note[Very very very very very very very very long head]
        {
            \lipsum[5]
        }
    
    \summary{Summary}{A fabulous summary}
  ```





### Change the layout
The default layout is *portrait*, if you would like to switch to *landscape*, just use `\usepackage[landscape]{geometry}`.


