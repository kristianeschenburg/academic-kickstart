---
title: "Extracting Reproducible Time-Resolved Resting State Networks Using Dynamic Mode Decomposition"
authors:
- James M. Kunert-Graf
- Kristian M. Eschenburg
- David J. Galas
- J. Nathan Kutz
- Swati D. Rane
- Bingni W. Brunton
date: "2019-10-31"
doi: ""

# Schedule page publish date (NOT publication's date).
publishDate: "2019-10-31"

# Publication type.
# Legend: 0 = Uncategorized; 1 = Conference paper; 2 = Journal article;
# 3 = Preprint / Working Paper; 4 = Report; 5 = Book; 6 = Book section;
# 7 = Thesis; 8 = Patent
publication_types: ["2"]

# Publication name and optional abbreviated publication name.
publication: ""
publication_short: ""

abstract: "Resting state networks (RSNs) extracted from functional magnetic resonance imaging (fMRI) scans are believed to reflect the intrinsic organization and network structure of brain regions. Most traditional methods for computing RSNs typically assume these functional networks are static throughout the duration of a scan lasting 5–15 min. However, they are known to vary on timescales ranging from seconds to years; in addition, the dynamic properties of RSNs are affected in a wide variety of neurological disorders. Recently, there has been a proliferation of methods for characterizing RSN dynamics, yet it remains a challenge to extract reproducible time-resolved networks. In this paper, we develop a novel method based on dynamic mode decomposition (DMD) to extract networks from short windows of noisy, high-dimensional fMRI data, allowing RSNs from single scans to be resolved robustly at a temporal resolution of seconds. After validating the method on a synthetic dataset, we analyze data from 120 individuals from the Human Connectome Project and show that unsupervised clustering of DMD modes discovers RSNs at both the group (gDMD) and the single subject (sDMD) levels. The gDMD modes closely resemble canonical RSNs. Compared to established methods, sDMD modes capture individualized RSN structure that both better resembles the population RSN and better captures subject-level variation. We further leverage this time-resolved sDMD analysis to infer occupancy and transitions among RSNs with high reproducibility. This automated DMD-based method is a powerful tool to characterize spatial and temporal structures of RSNs in individual subjects."

# Summary. An optional shortened abstract.
summary:  In this paper, we develop a novel method based on dynamic mode decomposition (DMD) to extract resting-state networks from short windows of noisy, high-dimensional fMRI data, allowing RSNs from single scans to be resolved robustly at a temporal resolution of seconds.  This automated DMD-based method is a powerful tool to characterize spatial and temporal structures of RSNs in individual subjects.

tags:
- dynamic networks
- modal decomposition
- fMRI
- independent component analysis
- Human Connectome Project
featured: true

links:
- name: Paper
  url: https://www.frontiersin.org/articles/10.3389/fncom.2019.00075/full
url_pdf: ''
url_code: 'https://github.com/kristianeschenburg/dmd'
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