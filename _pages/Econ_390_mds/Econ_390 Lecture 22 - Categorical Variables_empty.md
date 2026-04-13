---
layout: single
sitemap: false
permalink: /pages/Econ_390_SP26_L22/
title: Econ 390 Lecture 22
---

[Download Jupyter Notebook Empty](https://m-mcmain.github.io/files/Econ390SP26/Lectures/Lecture22_CategoricalVariables_empty.ipynb)

Download Jupyter Notebook Completed

# Econ 390 - Lecture 22: Categorical Variables
Today we will be going over category type variables and use them to do comparisons across groups. You can find readings in [McKinney](https://wesmckinney.com/book/data-cleaning#pandas-categorical) and [Turrell](https://aeturrell.github.io/coding-for-economists/data-categorical.html#categorical-data)


```python
import pandas as pd
auto = pd.read_csv("https://www.statlearning.com/s/Auto.csv")
auto
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>mpg</th>
      <th>cylinders</th>
      <th>displacement</th>
      <th>horsepower</th>
      <th>weight</th>
      <th>acceleration</th>
      <th>year</th>
      <th>origin</th>
      <th>name</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>18.0</td>
      <td>8</td>
      <td>307.0</td>
      <td>130</td>
      <td>3504</td>
      <td>12.0</td>
      <td>70</td>
      <td>1</td>
      <td>chevrolet chevelle malibu</td>
    </tr>
    <tr>
      <th>1</th>
      <td>15.0</td>
      <td>8</td>
      <td>350.0</td>
      <td>165</td>
      <td>3693</td>
      <td>11.5</td>
      <td>70</td>
      <td>1</td>
      <td>buick skylark 320</td>
    </tr>
    <tr>
      <th>2</th>
      <td>18.0</td>
      <td>8</td>
      <td>318.0</td>
      <td>150</td>
      <td>3436</td>
      <td>11.0</td>
      <td>70</td>
      <td>1</td>
      <td>plymouth satellite</td>
    </tr>
    <tr>
      <th>3</th>
      <td>16.0</td>
      <td>8</td>
      <td>304.0</td>
      <td>150</td>
      <td>3433</td>
      <td>12.0</td>
      <td>70</td>
      <td>1</td>
      <td>amc rebel sst</td>
    </tr>
    <tr>
      <th>4</th>
      <td>17.0</td>
      <td>8</td>
      <td>302.0</td>
      <td>140</td>
      <td>3449</td>
      <td>10.5</td>
      <td>70</td>
      <td>1</td>
      <td>ford torino</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>392</th>
      <td>27.0</td>
      <td>4</td>
      <td>140.0</td>
      <td>86</td>
      <td>2790</td>
      <td>15.6</td>
      <td>82</td>
      <td>1</td>
      <td>ford mustang gl</td>
    </tr>
    <tr>
      <th>393</th>
      <td>44.0</td>
      <td>4</td>
      <td>97.0</td>
      <td>52</td>
      <td>2130</td>
      <td>24.6</td>
      <td>82</td>
      <td>2</td>
      <td>vw pickup</td>
    </tr>
    <tr>
      <th>394</th>
      <td>32.0</td>
      <td>4</td>
      <td>135.0</td>
      <td>84</td>
      <td>2295</td>
      <td>11.6</td>
      <td>82</td>
      <td>1</td>
      <td>dodge rampage</td>
    </tr>
    <tr>
      <th>395</th>
      <td>28.0</td>
      <td>4</td>
      <td>120.0</td>
      <td>79</td>
      <td>2625</td>
      <td>18.6</td>
      <td>82</td>
      <td>1</td>
      <td>ford ranger</td>
    </tr>
    <tr>
      <th>396</th>
      <td>31.0</td>
      <td>4</td>
      <td>119.0</td>
      <td>82</td>
      <td>2720</td>
      <td>19.4</td>
      <td>82</td>
      <td>1</td>
      <td>chevy s-10</td>
    </tr>
  </tbody>
</table>
<p>397 rows × 9 columns</p>
</div>



## Categorical Data


```python
# Check out origin

```


```python
# Create a new variable

```


```python
# pd.Categorical

```


```python
# Convert the variable

```


```python
# cat method

```


```python
# Categories

```


```python
# Codes

```


```python
# Alternative Method

```


```python
# Aggregation

```

## Regression Models with Groups


```python
# Import seaborn and smf
import seaborn as sns
import statsmodels.formula.api as smf
```


```python
# lmplot with weight and mpg

```


```python
# lmplot with customization

```


```python
# lmplot with customization

```


```python
# model using smf

```


```python
# Comparing across models
from statsmodels.iolib.summary2 import summary_col

```


```python
# Categorical in the Model

```


```python
# Alternate way of typing it

```

## Binning Data
We did a little bit of this all the way back in [Lecture 12](https://m-mcmain.github.io/pages/Econ_390_SP26_L12/)!


```python
# Distribution of years

```


```python
# Means across years

```


```python
# Using cut

```


```python
# groupby again

```


```python
# ols on bins

```


```python
# qcut

```


```python
# groupby again, qcut

```


```python
# ols on quantiles

```

## Practice Binning
1. Create a variable called `horsepower_tercile` that splits the `horsepower` variable into thirds, label them appropriately. *Hint: What type is `horsepower`? Sort by index to see the range.*
2. Create a variable called `horsepower_bins` that splits `horsepower` into three equally sized bins
3. Are these different?


```python

```
