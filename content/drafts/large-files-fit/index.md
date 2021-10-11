---
# Documentation: https://sourcethemes.com/academic/docs/managing-content/

title: "Removing large files in Git"
subtitle: ""
summary: ""
authors: []
tags: []
categories: []
date:   2021-09-21T23:24:17-07:00
lastmod: 2021-09-21T23:24:17-07:00
featured: false
draft: false

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

For one reason or another, I'll often find myself running into the following issue:

```bash
remote: error: GH001: Large files detected. You may want to try Git Large File Storage — https://git-lfs.github.com.
remote: error: Trace: b5116d865251981c96d4b32cdf7ef464
remote: error: See http://git.io/iEPt8g for more information.
remote: error: File fixtures/11_user_answer.json is 131.37 MB; this exceeds GitHub’s file size limit of 100.00 MB
```