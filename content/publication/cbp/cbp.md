---
title: "Automated Connectivity-Based Cortical Mapping Using Registration-Constrained Classification"
authors:
- Kristian M. Eschenburg
- David Haynor
- Tom Grabowski
date: "2018-03-12"
doi: ""

# Schedule page publish date (NOT publication's date).
publishDate: "2018-03-12"

# Publication type.
# Legend: 0 = Uncategorized; 1 = Conference paper; 2 = Journal article;
# 3 = Preprint / Working Paper; 4 = Report; 5 = Book; 6 = Book section;
# 7 = Thesis; 8 = Patent
publication_types: ["1"]

# Publication name and optional abbreviated publication name.
publication: ""
publication_short: ""

abstract: "An important goal in neuroscience has been to map the surface of the human brain, and many researchers have developed sophisticated methods to parcellate the cortex. However, many of these methods stop short of developing a framework to apply existing cortical maps to new subjects in a consistent fashion. The computationally complex step is often the initial mapping of a large set of brains, and it is inefficient to repeat these processes for every new data sample. In this analysis, we propose the use of a library of training brains to build a statistical model of the parcellated cortical surface and to act as templates for mapping new data. We train classifiers on training data sampled from local neighborhoods on the cortical surface, using features derived from training brain connectivity information, and apply these classifiers to map the surfaces of previously unseen brains. We demonstrate the performance of 3 different classifiers, each trained on 3 different types of training features, to accurately predict the map of new brain surfaces."

# Summary. An optional shortened abstract.
summary: In this analysis, we propose the use of a library of training brains to build a statistical model of the parcellated cortical surface to act as templates for mapping new MRI data.

tags:
- clustering
- deep learning
- segmentation
- Human Connectome Project
featured: true

links:
- name: Paper
  url: https://spie.org/Publications/Proceedings/Paper/10.1117/12.2293968
url_pdf: ''
url_code: ''
url_dataset: ''
url_poster: ''
url_project: ''
url_slides: ''
url_source: ''
url_video: ''

# Featured image
# To use, add an image named `featured.jpg/png` to your page's folder. 
image:
  caption: ""
  focal_point: ""
  preview_only: false

# Associated Projects (optional).
#   Associate this publication with one or more of your projects.
#   Simply enter your project's folder or file name without extension.
#   E.g. `internal-project` references `content/project/internal-project/index.md`.
#   Otherwise, set `projects: []`.
# projects:
# - internal-project

# Slides (optional).
#   Associate this publication with Markdown slides.
#   Simply enter your slide deck's filename without extension.
#   E.g. `slides: "example"` references `content/slides/example/index.md`.
#   Otherwise, set `slides: ""`.
# slides: example
---