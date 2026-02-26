---
layout: single
sitemap: false
permalink: /pages/Econ_390_SP26_L12_empty/
---

[Download Jupyter Notebook Empty](https://m-mcmain.github.io/files/Econ390SP26/Lectures/Lecture12_PandasCalculations_empty.ipynb)

Download Jupyter Notebook Completed

# Econ 390 - Lecture 12: Pandas Calculations
Today we will start applying all of the knowledge we've accumulated since the beginning of the semester to actually get our hands dirty and work with the data! The [Working With Data Chapter from Turrell](https://aeturrell.github.io/coding-for-economists/data-intro.html#) and [5.2](https://wesmckinney.com/book/pandas-basics#pandas_frame)-[5.3](https://wesmckinney.com/book/pandas-basics#pandas_summarize) in McKinney are what is closest to this topic among the textbooks. We will be expanding on the Chilean Manufacturing Survey data from last time.

## Setting up the Data


```python
# Import packages
```


```python
# Read in df
```


```python
# Or set the index
```


```python
# Subset just the columns of interest
```

## Operations


```python
# Looping through to get total employment
```


```python
# Or use a method
```


```python

# Test efficiency of the cell

```


```python

# Compare it to this

```


```python
# All in one line
```


```python
# Create a new column in the original dataset
```


```python
# Similar for wages paid
```


```python
# Convert to USD
```


```python
# Calculate average wages in USD
```


```python
# All employees in data?
```


```python
# Another way
```


```python
# Suppose we don't want to count 0's towards any measures
```


```python
# Notice patterns
```


```python
# skipna option
```


```python
# May make sense more for some than others
```


```python
# Can take the mean across columns
```


```python
# Maximum
```


```python
# Location of the max
```


```python
# Cumulative Sum
```

## Practice - Additional Calculations
1. Check out var, std, rank, quantile, mode in `ENIA_1995`


```python

```

## Descriptive Statistics and Tables


```python
# Convert to string
```


```python
# the describe method
```


```python
# Find counts of values
```


```python
# Make it a DataFrame
```


```python
# Or as a percent
```


```python
# Cumulative sum
```


```python
# Create a new df with all of these
```


```python
# Crosstab multiple variables
```


```python
# Normalize by column
```


```python
# Make it percent
```

## Practice - Additional Calculations on DFs
1. What happens if you describe the entire dataframe?
    - What's the maximum contracted men? The maximum total wages?
2. There’s a few more variables that you could be interested in.
    - Make a tabulation looking at `EXPORTADOS` to see how many firms export.
    - Create a variable called `emp_type` that separates firms by < 25 employees, 25-100 employees, 101-499 employees, and 500+ employees. Hint: Check out the function `cut`.
    - Try making your own cross tab of `EXPORTADOS` and `emp_type`.
    - Which one do you want in the columns and which one do you want in the rows?
3. How do you control this with the crosstab method?
    - Do you want counts, percentages that add to one over the entire table, over the row, or over the column — discuss syntax of each.


```python

```
