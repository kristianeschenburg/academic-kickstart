---
title: parcellearning
summary: package of neural network modules for learning cortical architectures from brain connectivity data
tags:
- image processing
- artificial intelligence
- neural networks
- segmentation
date: "2020-12-25T00:00:00Z"

# Optional external URL for project (replaces project detail page).
external_link: ""

image:
  caption: 
  focal_point: Smart

links:
- icon: github
  icon_pack: fab
  name: Code
  url: https://github.com/kristianeschenburg/parcellearning.git
url_code: ""
url_pdf: ""
url_slides: ""
url_video: ""

# Slides (optional).
#   Associate this project with Markdown slides.
#   Simply enter your slide deck's filename without extension.
#   E.g. `slides = "example-slides"` references `content/slides/example-slides.md`.
#   Otherwise, set `slides = ""`.
slides: ""
---

This is a python package to apply various graph neural network models to brain connectivity data to learn cortical brain maps.  These models address the issue of node classification, as commonly seen in the graph representation learning community.  These models are based on the [Deep Graph Library](https://www.dgl.ai/).

Current models include the following:
  1. Graph Convolution Network ([paper](https://arxiv.org/abs/1609.02907))
  2. Graph Attention Network ([paper](https://arxiv.org/abs/1710.10903))
  3. Gaussian Kernel Graph Convolution Network ([paper](http://arxiv.org/abs/1803.10336))
  4. Constrained Graph Attention Network ([paper](https://arxiv.org/abs/1910.11945))