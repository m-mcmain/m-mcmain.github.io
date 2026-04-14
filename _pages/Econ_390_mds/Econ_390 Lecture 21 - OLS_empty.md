---
layout: single
sitemap: false
permalink: /pages/Econ_390_SP26_L21_empty/
title: Econ 390 Lecture 21
---

[Download Jupyter Notebook Empty](https://m-mcmain.github.io/files/Econ390SP26/Lectures/Lecture21_OLS_empty.ipynb)

Download Jupyter Notebook Completed

# Econ 390 - Lecture 21: OLS
Today we will be looking at examining the relationships between variables using visualizations and Ordinary Least Squares in Python. You can find the relevant info from [McKinney](https://wesmckinney.com/book/modeling#modeling-statsmodels) and a similar but different package in [Turrell](https://aeturrell.github.io/coding-for-economists/econmt-regression.html#regression-basics).


```python
import seaborn as sns
import matplotlib.pyplot as plt 
```

## Visualization


```python
# Load seaborn dataset

```


```python
# Scatterplot of fare and tip

```


```python
# Basic plot

```


```python
# Customizing

```


```python
# Convert tip into a percentage of fair and plot that

```


```python
# Seaborn default scatterplot

```


```python
# Seaborn with customization

```


```python
# Jointplot

```


```python
# Customize Joint Plot?

```


```python
# What are they

```


```python
# Use .set on ax_joint

```

## Practice - Visualization
1. Produce a similar joint plot but for payment instead of total bill.
2. With this in mind, remake the plot above but getting rid of the data that doesn't make sense to include. Hint: Subset the data in the jointplot function


```python

```

## Regression Analysis


```python
# Update dataset to drop cash

```


```python
# Correlations

```


```python
# New package!
import statsmodels.formula.api as smf 
```


```python
# Regression

```


```python
# Print the results

```


```python
# Bias correct the variances

```


```python
# Print results

```


```python
# Add fitted values to the DataFrame

```


```python
# lmplot

```


```python
# lmplot customized

```


```python
# Another regression

```


```python
# New function
from statsmodels.iolib.summary2 import summary_col
```


```python
# Prettier printing

```


```python
# Options

```

## Practice - Regression Analysis
1. The results for a linear relationship between tip_pct and fare looks pretty bad. What if it's quadratic? How do we add that? Hint: There are multiple ways of doing this.
2. Make a nice regression table using summary_col comparing the linear and the quadratic models
3. Now, how can we get that onto the lmplot? Hint: Check out the "order" argument. What does order mean in the context of equations?


```python

```
