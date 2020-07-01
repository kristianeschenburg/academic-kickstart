---
title: submet
summary: package to compute various distance metrics between subspaces
tags:
- linear subspaces
- geodesics
- metrics
date: "2020-06-29T00:00:00Z"

# Optional external URL for project (replaces project detail page).
external_link: ""

image:
  caption: 
  focal_point: 

links:
- icon: github
  icon_pack: fab
  name: Code
  url: https://github.com/kristianeschenburg/submet
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

See my [post]( {{< relref "/post/comparing-subspaces/index.md" >}} ) with a brief algorithmic introduction for computing distances between pairs of subspaces.  Featured image from [Melissa Nealy](https://www.simonsfoundation.org/2019/04/02/brain-areas-may-use-subspace-communication-to-talk-to-one-another/).

```submet``` is a Python package for computing pairwise distances between equidimensional subspaces.  All of these subspace metrics are dependent on the principle angles between the two subspaces.  ```submet``` implements an [sklearn]()-styled interface with a fitting method via a class called ```SubspaceDistance```, along with a variety of metrics in a class called ```Metric```.

```python
import numpy as np
import submet

# generate random subspaces
s1 = np.random.rand((10, 2))
s2 = np.random.rand((10, 2))

# instantiate SubspaceDistance object, using the Grassmann distance metric
S = submet.subspaces.SubspaceDistance(metric='Grassmann')

# compute the distance between two subspaces
S.fit(s1, s2)

# print computed distance
print(S.distance_)
```

```Metric``` implements the following distance metrics:
 * Asimov
 * Binet-Cauchy
 * Chordal
 * Fubini-Study
 * Martin
 * Procrustes
 * Projection
 * Spectral


```SubspaceDistance``` does not currently support pairwise distance computations between more than a single pair of subspaces, in an analogous way to [Scipy's](https://docs.scipy.org/doc/scipy/reference/index.html) [pdist](https://docs.scipy.org/doc/scipy/reference/generated/scipy.spatial.distance.pdist.html#scipy.spatial.distance.pdist) or [cdist](https://docs.scipy.org/doc/scipy/reference/generated/scipy.spatial.distance.cdist.html#scipy.spatial.distance.cdist) methods.  I am working on allowing pairwise computations using [numba](https://numba.pydata.org/numba-doc/0.11/index.html).


**Update as of 6/30/2020: the above issue has been fixed and ```submet``` now allows for pairwise distance matrix computations, rather than only single subspace pair comparisons.  See this [pull request](https://github.com/kristianeschenburg/submet/pull/2)**
