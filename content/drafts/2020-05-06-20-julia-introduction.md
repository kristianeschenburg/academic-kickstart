---
title:  "Self-Teaching: Julia"
layout: post
math: true
date:   2020-05-05 14:24:17 -0700
mathjax: true
draft: true
---

I've been meaning to teach myself [Julia](https://docs.julialang.org/en/v1/) and decided to document some conventional tools, functions, and steps that I might run into on a day-to-day basis.  I'm assuming that you've added the Julia binary to your ```${PATH}``` variable, and can call the Julia prompt by typing ```julia``` in the terminal.

# Installing Packages

```bash
julia
using Pkg
Pkg.add('LinearAlgebra')
```

installs the package "LinearAlgebra" 

# Using vs. Importing Packages
There s

# Indexing into Arrays
More information for arrays can be found [here](https://docs.julialang.org/en/v1/manual/arrays/).

```julia
# initilize empty Int64 array 
temp = Array{Int64}(undef, (2,3))

# return index [1, 1]
temp[1, 1]

# assign entire row or column a value
# the .= operator operates on the entire range of indices specified by (:)
# the = operator would produce an error here
temp[1, :] .= 10
temp[:, 1] .= 5

# assign entire row or column a vector
temp[1, :] = [1, 2, 3]
```