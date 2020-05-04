---
title: "Watershed by Flooding: Applied Data Structures in Python"
layout: post
date: 2020-05-01 11:12:32
math: true
pagination: 
    enabled: true
---

I'm applying some methods developed in [this paper](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC4677978/pdf/bhu239.pdf) for testing purposes in my own thesis research.  Specifically, I have some vector-valued float data that varies along the cortical surface of the brain.  Visually, I can see that there are areas where these scalar maps change abruplty.  I want to identify this boundary(s) -- eventually, I'll segment out the regions I'm interested in.

The authors use some conventional brain imaging software to compute the gradient of their data.  The domain of this data is a triangulated mesh, described by the graph $G = \\{V, E\\}$, where $V$ are vertices in Euclidean space and $E$ the edges between these vertices.  In short, for a vertex, $v\_{i}$, we first need to compute the gradient vector of the scalar field at $v\_{i}$.  We "unfold" the 3D positions of adjacent vertices onto the tangent plane of $v\_{i}$ -- which we can do by orthogonally projecting the adjacent vertices onto the affine subspace at $v\_{i}$ and then weighting appropriately.  We then regress the graph signal (our scalar field) onto these unfolded positions.  The $L2$ norm of this vector is the gradient at $v\_{i}$.  

The new scalar field of $L2$ norms is our gradient field, which describes how "quickly" our original data changes at each vertex.  We can now apply the [Watershed Algorithm](https://en.wikipedia.org/wiki/Watershed_(image_processing)) to segment our mesh data.  In brief, the watershed algorithm treats the gradient field as a *topographic map*: low-elevation areas (areas with a small gradient) are "water basins".  If we imagine water flooding this map from the bottom up, basins at low elevation will flood first, while areas at higher elevations will fill last.  When water basins meet, the water has reached a "boundary" (or ridgeline, if we're using the topographic map idea).

I've implemented an algorithm variant called ["Priority Flooding"](https://www.sciencedirect.com/science/article/pii/S0098300418307957), using Python's [heapq](https://docs.python.org/2/library/heapq.html) [priority queue](https://en.wikipedia.org/wiki/Priority_queue) data structure.  We utilize the priority queue because it gives us a principled way to iterate over unlabeled vertices, and, with some auxilliary data structures, is guaranteed to converge.  The algorithm proceeds as follows:

 1) Identify local minima, and assign each minima a unique label
 2) Add directly adjacent vertices of local minima to priority queue (lower gradient -> higher priority)
 3) While the queue is not empty, get the highest-priority item

    * If vertices adjacent to this vertex have only one label, assign this vertex to that label
    
    * Else assign this vertex as a boundary vertex
    
    * Add unlabed adjacent vertices to the queue

```python
import numpy as np
from queue import PriorityQueue

class PriorityFlood(object):

    """
    Class to segment a scalar field using the Priority Flooding
    watershed algorithm.
    """

    def __init__(self):

        self.pq = PriorityQueue()

    def fit(self, gradient, A, M):

        """
        Fitting procedure for watershed algorithm.

        Parameters:
        - - - - -
        gradient: float, array
            map of gradient values of scalar field
        A: dict of lists
            adjacency list of data domain
        M: list
            local minima in scalar field used to seed algorithm
        """

        # initialize empty label vector
        labels = np.zeros((gradient.shape))
        labels[:] = np.nan

        # keep track of items in queue
        in_queue = np.zeros((gradient.shape)).astype(np.bool)

        # assign local minima unique labels
        # add their adjacent vertices to heap
        for i, loc_min in enumerate(M):

            # label local minima
            labels[loc_min] = i+1

            # add neighbors of local minima to p-queue
            for nidx in A[loc_min]:
                in_queue[nidx] = True
                self.pq.put((gradient[nidx], nidx))

        # iterate over p-queue items
        # items assigned to a label or
        # assigned as a boundary
        while not self.pq.empty():

            # get highest priority item
            # mark as not in p-queue
            [gr, idx] = self.pq.get()
            in_queue[idx] = False

            # get item neighbors and their labels
            i_neighbors = np.asarray(A[idx])
            i_nlabels = labels[i_neighbors]

            # get labels of adjacent vertices that are not nan
            nans = np.isnan(i_nlabels)
            unique_labels = np.unique(i_nlabels[~nans])

            # if more than one unique label
            # assign current vertex as border vertex
            if len(unique_labels) > 1:
                continue

            # otherwise assign to water basin
            else:

                # basin assignment
                labels[idx] = unique_labels

                # identify neighbors without labels that arent in the p-queue
                gidx = np.where((nans) & (~in_queue[i_neighbors]))[0]

                # add these to p-queue
                for nidx in i_neighbors[gidx]:
                    if not in_queue[nidx]:
                        in_queue[nidx] = True
                        self.pq.put((gradient[nidx], nidx))

        self.labels_ = labels

```

{{< figure library="true" src="WSA.jpg" title="Example of PriorityFlooding algorithm, applied to gradient of inferiorparietal region.  Shown on inflated and flattened cortical surfaces." lightbox="true" >}}

One caveat that came up is that the **PriorityQueue** class does not check for duplicates -- that is, two vertices might share an adjacent vertex, and this vertex might have already been added to the heap.  In this case, we would unnecessarily view the same vertices many times.  To alleviate this, we create a boolean Numpy array, ```in_queue```, that stores whether an item is already in the queue.
