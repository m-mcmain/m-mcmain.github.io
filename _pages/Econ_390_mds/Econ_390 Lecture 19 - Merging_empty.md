---
layout: single
sitemap: false
permalink: /pages/Econ_390_SP26_L19_empty/
title: Econ 390 Lecture 19
---

[Download Jupyter Notebook Empty](https://m-mcmain.github.io/files/Econ390SP26/Lectures/Lecture19_Merging_empty.ipynb)

Download Jupyter Notebook Completed

# Econ 390 - Lecture 19: Merging
Today we will go over how to merge datasets. We will be covering much of [8.1 and 8.2 from McKinney](https://wesmckinney.com/book/data-wrangling) and [Joins in Turrell](https://aeturrell.github.io/coding-for-economists/data-joining-data.html#joins).


```python
import pandas as pd

econ390path = "https://m-mcmain.github.io/files/Econ390SP26/"
```

## Concatenate


```python
# Read in the data

```


```python
# concat method

```


```python
# Now specify the type for Year in the telework 2023 data

```


```python
# This is still Bad

```


```python
# Now we can have concat do even more work for us

```

## Hierarchical Indexing


```python
# Reset to just State as index

```


```python
# Set two indices?

```


```python
# Change the order?

```


```python
# Setting the index with options

```


```python
# What *is* the index?

```


```python
# How does sort work

```


```python
# Sort in descending order

```


```python
# Sorting on index?

```


```python
# Specify different levels and ascending

```


```python
# Alternative options for sort_index

```


```python
# Basic

```


```python
# Finding specific entries for one index

```


```python
# Finding specific entries for both index

```


```python
# Comparison

```


```python
# Stacked loc

```


```python
# xs turns the dataframe into a cross section for the specified index

```


```python
# Different process, same result

```


```python
# Keep the level

```


```python
# Multiple states?

```


```python
# Work around that with concat

```


```python
# loc still works

```


```python
# Send it to a csv

```


```python
# Read it in with multiple indices

```

## Practice - Hierarchical Indexing
1. Find the telework data for D.C.
2. Find the telework data for D.C. in 2023
3. Find the percent of workers who entirely teleworked in D.C. in 2023
4. Get all of the data for teleworking in 2023


```python

```

## Merging


```python
# Merge Method

```


```python
# Gotta specify "on"

```


```python
# Suffixes and dropping

```
