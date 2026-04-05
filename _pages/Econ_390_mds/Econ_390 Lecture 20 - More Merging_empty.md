---
layout: single
sitemap: false
permalink: /pages/Econ_390_SP26_L20/
title: Econ 390 Lecture 20
---

[Download Jupyter Notebook Empty](https://m-mcmain.github.io/files/Econ390SP26/Lectures/Lecture20_MoreMerging_empty.ipynb)

Download Jupyter Notebook Completed

# Econ 390: Lecture 20 - More Merging
Today we will be spending some more time merging datasets. Relevant pages are [8.2 in McKinney](https://wesmckinney.com/book/data-wrangling#prep_merge_join), [Merge in Turrell](https://aeturrell.github.io/coding-for-economists/data-joining-data.html#merge), and [this page](https://sscc.wisc.edu/sscc/pubs/dwp/Combining_Data_Sets.html#adding-variables) from the SSCC.

There are three general types of merging you will need to do. In order of how often *I* use them:
1. Creating Panel Data (Same Dataset Across Time)
2. Merging Unrelated Data On Time (Different Datasets Across Time)
3. Merging the Same Data over Multiple Sources (Same Data Across Sources)

We did a little bit of #1 at the end of last lecture. #3 is generally pretty rare and happens when you have high quality restricted data. #2 is very common when you want to control for macro variables that are common among everyone but change over time.


```python
import numpy as np
import pandas as pd

econ390path = "https://m-mcmain.github.io/files/Econ390SP26/"
```

## Wide and Long Data

![Image showing the difference between wide and long data](https://www.statology.org/wp-content/uploads/2021/12/wideLong1-1-768x543.png "Wide vs. Long Data")


```python
# Create the data
final_four = pd.DataFrame({"Team": ["Michigan", "Arizona", "Illinois", "UConn"],
                           "Points": [91, 73, 62, 71],
                           "Assists": [22, 5, 3, 14],
                           "Rebounds": [40, 44, 44, 37]})
```


```python
# "Melt" to go from Wide to Long

```


```python
# Pivot to go back to Wide

```


```python
# Reset Index

```


```python
# Select the vars to melt

```

## Back to Merging


```python
# Read in data
ffr_cleaned = pd.read_csv(econ390path + "ffr_cleaned.csv", index_col = 0)
rd_BEA = pd.read_csv(econ390path + "rd_BEA.csv", index_col = 0)
```


```python
# Check out the data

```


```python
# How should we merge them? Concat? Do resulting rows make sense?

```


```python
# How is outer different?

```

## Merging Variable Type


```python
# Set random seed (for reproducibility), ID length, and number of observations

```


```python
# Generate string ID of the specified length, convert to float, then back to string

```


```python
# Display results in a DataFrame

```

So, if you have data that is read in as Float, you cannot then convert it to a String. It has already done the estimation! So, you'll need to specifically read it in *as* a String by using the `dtype={'var': 'str'}` option in `read_csv`.

Another thing to note when matching with Strings. Make sure that the ID format is consistent across files (e.g. Case Sensitive and Whitespace). If it's not you'll need to do so yourself! Such as `str.lower()` and `str.strip()` respectively.

## Investigating Unmatched Observations

As a reminder, FUSION_annual_1995_EMP is a random sample of 100 Chilean Manufacturing Survey responses from 1995 where each row is one firm that has identifier "NUI" (almost certainly some sort of acronym in Spanish). FUSION_annual_1996_EMP is created similarly, but instead of being a completely random sample, I select the NUI's that show up in both the 1996 Chilean Manufacturing Survey and 1995's, then randomly fill out the rest from 1996 if not all 100 from 1995 are also in 1996. 

Why might not all 100 firms from the random sample in 1995 also be in the 1996 survey responses?


```python
# Read in our data
fusion_1995 = pd.read_stata(econ390path + "FUSION_annual_1995_EMP.dta")
fusion_1996 = pd.read_stata(econ390path + "FUSION_annual_1996_EMP_erroneous.dta")
```


```python
# Merge

```


```python
# Check out a specific NUI

```


```python
# Merge using validate, expecting 1:1

```


```python
# Try Except to save ourselves

```

## [MovieLens Data](https://wesmckinney.com/book/data-analysis-examples#whetting_movielens)
Are Comedies or Dramas better rated on average? Let's find out!


```python
# Read in the data
movies = pd.read_csv(econ390path + "movies.csv")
ratings = pd.read_csv(econ390path + "ratings.csv")
```


```python
# Check out the datasets

```


```python
# Merge to create ratings and genre, using validate

```


```python
# Check out which entries are left or right only

```


```python
# Re-run to exclude unmatched observations

```


```python
# Ratings by Genre - does this make sense?

```


```python
# Properly accommodate genres

```
