---
layout: single
sitemap: false
permalink: /pages/Econ_390_SP26_L18/
title: Econ 390 Lecture 18
---

[Download Jupyter Notebook Empty](https://m-mcmain.github.io/files/Econ390SP26/Lectures/Lecture18_Aggregation_empty.ipynb)

Download Jupyter Notebook Completed

# Econ 390 - Lecture 18: Groupby and Aggregation
Today we will be going over how to aggregate data and apply the Split-Apply-Combine method using Python. All of [Chapter 10 of McKinney](https://wesmckinney.com/book/data-aggregation) and much of [Data Transformation of Turrell](https://aeturrell.github.io/coding-for-economists/data-transformation.html) are applicable here, though we will not be going over all of what they cover.


```python
import pandas as pd

url = "https://m-mcmain.github.io/files/Econ390SP26/"
```

## Split-Apply-Combine
The Split-Apply-Combine method is so common there are different images describing how to use it in both of the textbooks:

![McKinney SAC](https://wesmckinney.com/book/images/pda3_1001.png)
![Turrell SAC](https://jakevdp.github.io/PythonDataScienceHandbook/figures/03.08-split-apply-combine.png)


```python
# NLSY variables
```


```python
# Read in data
```


```python
# Info
```


```python
# Counts of different groups
```


```python
# Translating codes to what they mean
```


```python
# Set the index and groupby
```


```python
# Get Group method
```


```python
# Mean
```


```python
# Mean of grouped
```


```python
# Limit to just people working
```


```python
# Not grouped
```


```python
# Cleaning and new Value
```


```python
# Medians
```

Common aggregation methods are:
- `.mean()`
- `.sum()`
- `.std()`
- `.describe()`
- `.min()`
- `.max()`

## Practice: Split-Apply-Combine
Let's figure out how to get some measure of how variable annual income of workers are by education attainment.
1. Calculate the 75th percentile of Income for each new education type, storing the result in a DataFrame called q75 (So we split on what? And then apply what method?) *Hint: The .quantile() method computes percentiles.*
3. Calculate the 25th percentile for each type and store it in q25
4. Take the difference between these q75 and q25
5. Based on the IQR, which education type has the least amount of variation?


```python
# Results:
```

## Multiple Groups


```python
# List in groupby
```


```python
# xs method
```


```python
# Count
```


```python
# Agg
```


```python
# Multiple agg
```


```python
# Multiple variables
```
