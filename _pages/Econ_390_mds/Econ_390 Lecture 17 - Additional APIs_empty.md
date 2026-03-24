---
layout: single
sitemap: false
permalink: /pages/Econ_390_SP26_L17_empty/
title: Econ 390 Lecture 17
---

[Download Jupyter Notebook Empty](https://m-mcmain.github.io/files/Econ390SP26/Lectures/Lecture17_AdditionalAPIs_empty.ipynb)

Download Jupyter Notebook Completed

# Econ 390 - Lecture 17: APIs using Requests Package
Today we will be looking at a more "manual" method of using APIs in Python using the `requests` package. This package is mentioned in [6.3 of McKinney](https://wesmckinney.com/book/accessing-data#io_web_apis) and in [Turrell](https://aeturrell.github.io/coding-for-economists/data-extraction.html#obtaining-data-using-apis).


```python
import requests
import pandas as pd
import matplotlib.pyplot as plt
from io import StringIO
import io
```

## OECD API

The [OECD website](https://www.oecd.org/en/data/insights/data-explainers/2024/09/api.html) goes through their API! You'll also find a link to a PDF with more details on how to use the API.


```python
# Define API query URL (CSV with labels format)

# Fetch data
```


```python
# Type?
```


```python
# Status Code
```


```python
# What does it look like?
```


```python
# Load into pandas DataFrame

# Look through the DF
```


```python
# Subset just what we need
```


```python
# Create Histogram
```

## Practice: OECD API
1. Use the [OECD Data Explorer](https://data-explorer.oecd.org/) to find a dataset you'd be interested in downloading.
2. Get the API URL.
3. Display the first five rows. Does this immediately work if you just copy the URL from the API? *Hint: Make sure that you specify the format*


```python
url_practice = ""
response_practice = 
# Load into pandas DataFrame
df_practice = 
# Display first few rows
print(df_practice.head())
```


```python
# Results:
```

## Census API
We'll be focusing on the [International Trade API](https://www.census.gov/data/developers/data-sets/international-trade.html)


```python
# Base URL
```


```python
# Systematic components
```


```python
# Formulate full URL
```


```python
# All Together!
```


```python
# Content of the request
```


```python
# Using json method
```


```python
# First entry
```


```python
# First row?
```


```python
# Turn into DF
```


```python
# If/else
```

## Practice - Census API
1. Instead of US Oil Exports to Canada, find US Oil Imports from Russia
2. Start from January 2016 to now
3. Create a line plot of imports over time. Does anything stand out?


```python
# Results:
# Set query parameters
base_url = ''
variables = ''
country = ''
dates = ''

# Formula full URL
full_url = (base_url
            + '?get=' + variables 
            + '&CTY_CODE=' + country
            + '&time=' + dates)

# Submit query
response = requests.get(full_url)

# Clean up resulting data frame 
```
