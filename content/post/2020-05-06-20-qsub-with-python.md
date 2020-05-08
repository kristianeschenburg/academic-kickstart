---
title:  "qsub and Python Scripts"
layout: post
math: true
date:   2020-05-05 14:24:17 -0700
mathjax: true
---

I'm fortunate enought to work in a lab with some high-level computing infrastructure.  We have a clusters of machines using the [Sun Grid Engine](http://bioinformatics.mdc-berlin.de/intro2UnixandSGE/sun_grid_engine_for_beginners/README.html) (SGE) cluster software system.  The other day I found myself, searching for how to wrap my Python scripts so that I can use ```qsub``` to submit a batch of jobs to our cluster.  Eventually, I want to be able to submit jobs with dependencies between them, but we'll start here.  

Let's create an example script that computes the mean of an MRI image.  Let's call the script ```compute_mean.py```:

```python
#!/usr/bin/env python

import argparse
import nibabel as nb
import numpy as np
import pandas as pd


parser = ArgumentParser('Compute the mean of MRI, and save to CSV file.')
parser.add_argument('-i', '--input_image', help='Path to MRI image.',
    required=True, type=str)
parser.add_argument('-o', '--output_csv', help='Output CSV file.',
    required=True, type=str)

args = parser.parse_args()

# read in image
img = nb.load(args.input_image)
# get voxel-wise data
data = img.get_data()

# compute mean
mu = np.mean(data)

# save to csv
df = pd.DataFrame({'mean': [mu]})
df.to_csv(args.output_csv)
```

The first line of this script, ```#!/usr/bin/env python``` tells the script to use the local ```python``` environment.  In my case, I have a customized installation of Python, along with a bunch packages and libraries that I've written and installed that are not available for the rest of my lab (since they're still in the testing phase or just something I'm experimenting with).  This line tells the script to use *my* Python environment, rather than the default version on our servers.

We can then create a bash wrapper, let's call in ```mean_wrapper.sh``` for a single subject

```bash
#!/bin/bash
#$ -M keschenb@uw.edu
#$ -m abe
#$ -r y
#$ -o tmp.out
#$ -e tmp.err

# Compute mean of image
image=$1
output=$2

python compute_mean.py ${image} ${output}
```

The second and third line here, with the ```M``` and ```m``` parameters, tell the script to email me once it completes the processing (or if there are any errors).  And finally, we can create a wrapper that takes in a list of subjects to process, and the input and output directories, and submits each individual job to the queue using ```qsub```:


```bash
#!/bin/bash

subjects=$1
image_dir=$2
output_dir=$3

# we create a variable, as our cluster has 2 different queues to use
# this could be hardcoded though
queue_name=$4 

while read subj
do

    image_file=${image_dir}${subj}.nii.gz
    output_file=${output_dir}${subj}.csv

    qsub -q ${queue_name}.q mean_wrapper.sh ${input_image} ${output_file}

done <${subjects}
```
