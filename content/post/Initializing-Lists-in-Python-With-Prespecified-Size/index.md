---
# Documentation: https://sourcethemes.com/academic/docs/managing-content/

title: "Initializing Lists in Python With Prespecified Size"
subtitle: ""
summary: ""
authors: []
tags: []
categories: []
date: 2019-08-21T01:12:32-07:00
lastmod: 2019-08-22T01:12:32-07:00
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

I wanted to make a quick note about something I found incredibly helpful the other day.

Lists (or ArrayLists, as new Computer Science students are often taught in their CS 101 courses), as a data strucure are fundamentally based on arrays, but with additional methods associated with them.  Lists are generally filled with an ```append``` method, that fills indices in this array sequentially.  Lists are often useful in the case where the number of intial spots that will be filled is unknown, or if you're working with many objects of different types.

The base arrays are generally associated with a ```size``` or ```length``` parameter, that initializes the array to a certain length.  Under the hood (and generally hidden from the user), however, the ```List``` class also has a ```resize``` method that adds available space to the array when a certain percentage of available indices are occupied, technically allowing the size of the list to grow when more space is needed.

Perpetually applying ```resize``` becomes slow in the case when you're appending a lot of items.  All of the data currently in the ```List``` object will need to be moved into the new, resized array.

I needed to aggregate a large number (couple thousand) of Pandas DataFrame objects, each saved as a single file, into a single DataFrame.  My first thought was to simply incrementally load and append all incoming DataFrames to a list, and then use ```pandas.concat``` to aggregate them all together.  Appending all of these DataFrames together became pretty time consuming (at this point, I remembered the ```resize``` issue).

A quick Google search led me to the following solution, allowing me to predefine how large I wanted my list to be:

```python
# For simplicity assume we have 10 items
known_size = 10
initialized_list = [None]*known_size

print(len(initialized_list))
10
```

Neat, huh?  And ridiculously simple.  Now, rather than append, we can do the following:

```python
for j, temp_file in enumerate(list_of_files):
    loaded_file = load_file(temp_file)
    initialized_list[j] = loaded_file
```

Because the **memory has already been pre-allocated**, the ```resize``` method is never accessed, and we save time.  I also found [this blog post](http://zwmiller.com/blogs/python_data_structure_speed.html) with some information about timing with regards to Numpy arrays, lists, and tuples -- the author shows that indexing into a Numpy array is actually slower than indexing into a list.  Numpy arrays are primarilly useful in the case where operations can be vectorized -- then they're the clear winners in terms of speed.
