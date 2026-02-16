---
layout: single
sitemap: false
permalink: /pages/Econ_390_SP26_L10_teaching/
---

[Download Jupyter Notebook Empty](https://m-mcmain.github.io/files/Econ390SP26/Lectures/Lecture10_PandasDataStructures_empty.ipynb)

Download Jupyter Notebook Completed

# Econ 390 - Lecture 10: Pandas Series and Data Frames

Today we will be going over the incredibly popular package Pandas and how to utilize the data structures that they bring to Python. You can find good chapters in both [McKinney](https://wesmckinney.com/book/pandas-basics#pandas_construction) and [Turrell](https://aeturrell.github.io/coding-for-economists/data-intro.html#working-with-data) dedicated to this.

## Series


```python
# First you always need to import Pandas
```


```python
# Creating a series
```


```python
# What does it look like?
```


```python
# Mutable?
```


```python
# You can change the index after the fact
```


```python
# Accessing with new index?
```


```python
# Locate by raw index or by label
```


```python
# Slicing series
```


```python
# Conditionals?
```

## Practice - Series
1. Create a series of inflation where the index is country.
2. Print out entries that only have inflation above 3%
3. Create another series where the index is country but the values are "Low Inflation" if inflation is <= 2, "High Inflation" if inflation is between 2 and 50, and "Hyper Inflation" if inflation is above 50.


```python
inflation_dict = {'United States':2.9, 'United Arab Emirates':1.7, 'Angola':4.0, 'Venezuela':219.9}
```

## Dataframes
Real data from [FRED](https://fred.stlouisfed.org/series/PAPOP)


```python
# Create your first dataframe!
```


```python
# Just look at the first five
```


```python
# Or the last five
```


```python
# Selecting columns by name
```


```python
# Subsetting
```


```python
# Changing column order
```


```python
# You can create new variables
```


```python
# Rename columns
```


```python
# Locating Rows
```


```python
# Columns
```


```python
# Subsetting based on a condition
```


```python
# Reset index after subsetting
```


```python
# Drop old index
```


```python
# Setting index to something that makes sense
```


```python
# loc works as expected
```

## Practice - Dataframes
1. Create a Dataframe of inflation and inflation type with index country.
   - Hint: What happens if you call DataFrame on a series?
   - Hint: How might you create a new variable that is a different series?
3. In `frame`, replace Pennsylvania with PA.


```python

```
