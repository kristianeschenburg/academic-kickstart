---
# Documentation: https://sourcethemes.com/academic/docs/managing-content/

title: "Helmholtz Machines: Theory and Implementation"
subtitle: ""
summary: ""
authors: []
tags: []
categories: []
date: 2020-10-15T8:12:32-07:00
lastmod: 2020-10-18T8:12:32-07:00
featured: false
draft: true

# Featured image
# To use, add an image named `featured.jpg/png` to your page's folder.
# Focal points: Smart, Center, TopLeft, Top, TopRight, Left, Right, BottomLeft, Bottom, BottomRight.
image:
  caption: ""
  focal_point: ""
  preview_only: false

# Projects (optional).
#   Associate this post with one or more of your projects.
#   Simply enter your project's folder or file name without extension.
#   E.g. `projects = ["internal-project"]` references `content/project/deep-learning/index.md`.
#   Otherwise, set `projects = []`.
projects: []
---

I'm taking a class (quite possibly the last class I'll ever take (!)) titled "AI and the Brain" -- it's basially a survey course on the current state on artificial intelligence, and on how AI and neuroscience are intimately interwined.  Part of the course requires students to read up on some aspect of historical or model AI and present this work durng one class period.  I was assigned Geoffrey Hinton's seminal 1995 paper ["The Wake-Sleep Algorithm for Unsupervised Neural Networks"](https://www.cs.toronto.edu/~hinton/csc2535/readings/ws.pdf).

 Up until this paper, I was only familiar with Helmholtz machines insofar as I knew they were generative models implemented using neural networks meant to estimate the distribution of a dataset, but I was unaware of the inner workings of the network.  I want to give a brief overview of the theory and infernce procedure i.e. the Wake-Sleep algorithm, of Helmholtz machines and provide some example code to learn these networks.