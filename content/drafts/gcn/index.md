---
# Documentation: https://sourcethemes.com/academic/docs/managing-content/

title: "Cortical Segmentation Using Graph Convolutional Networks"
subtitle: ""
summary: ""
authors: []
tags: []
categories: []
date: 2020-11-4T8:12:32-07:00
lastmod: 2020-11-5T8:12:32-07:00
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

Installing Pytorch Geometric:

```bash
python -c "import torch; print(torch.__version__)"

# I have the CPU version of Pytorch installed
# User whichever version you have.
export CUDA=cpu

pip install torch-scatter==latest+${CUDA} -f https://pytorch-geometric.com/whl/torch-${TORCH}.html
pip install torch-sparse==latest+${CUDA} -f https://pytorch-geometric.com/whl/torch-${TORCH}.html
pip install torch-cluster==latest+${CUDA} -f https://pytorch-geometric.com/whl/torch-${TORCH}.html
pip install torch-spline-conv==latest+${CUDA} -f https://pytorch-geometric.com/whl/torch-${TORCH}.html
pip install torch-geometric
```