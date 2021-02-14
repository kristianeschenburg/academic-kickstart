---
# Documentation: https://sourcethemes.com/academic/docs/managing-content/

title: "Jumping-Knowledge Representation Learning in Medical Imaging"
subtitle: ""
summary: ""
authors: []
tags: [pytorch, AI, graph neural networks]
categories: []
date:   2021-01-25T23:24:17-07:00
lastmod: 2021-01-25T23:24:17-07:00
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
projects: [parcellearning]
---

As I mentioned in my previous post on constrained Graph Attention Networks, [constrained graph attention networks]( {{< relref "/post/constrained-gat/index.md" >}} ), graph neural networks suffer from overfitting and oversmoothing as network depth increases.  These issues can ultimately be linked to the local topologies of the graph.

If we consider 2d image as a graph (i.e. pixels become nodes) and reframe our pixels as nodes, images are highly [regular]() -- that is, each node has the same number of neighbors, expect for those at the border.  When we apply convolution kernels over these node signals, we can be sure that filters applied to nodes at any given layer are aggregating information from the same sized neighborhod (after accounting for zero-padding in the image).  However, if we consider a graph, there is no guarantee that the graph will be regular.  In fact, in many situations, graphs are highly *irregular*, and are characterized by unique topological neighborhood properties such as tree-like structures or expander nodes, whose neighborhood size grows exponentially as we move away from it.  If we compare an expander node to a node whose local topoloy is more regular, we can see that the number signals that each node convolves will vary considerably, at each layer in the graph.  These topological discrepancies have important implications when we begin to consder problems like node and graph classification, as well as edge prediction.  The problem ultimately boils down to one of flexibility -- i.e. can we optimally combine local signals on a node-by-node basis, such that we account for the unique local topologies of the graph?

In their [paper](), the authors propose one approach to address this question, which they call "Jumping Knowledge Representation Learning".

{{< figure src="./InfluenceRadius.png" title="" caption="Node aggregation at increasing depths.  At each layer, the neural network implicitly aggregates signals over an increasingly-larger neighborhood." lightbox="true" >}}

{{< figure src="./JKGAT_LSTM.png" title="" caption="Schematic of jumping-knowledge representation learning.  The neural network pushes input signals $X$ through the network, generating an embedding for each hidden layer.  The aggregator function then optimally combines these hidden embeddinggs to learn the optimal abstraction of input information.  Some alternative aggregation functions include max-pooling, concatenation, and an LSTM layer.  In the case of an LSTM layer coupled with an attention mechanism, the aggregator is a convex combination of hidden embedding." lightbox="true" >}}