---
layout: single
sitemap: false
permalink: /pages/Econ_390_SP26_L16/
title: Econ 390 Lecture 16
---

[Download Jupyter Notebook Empty](https://m-mcmain.github.io/files/Econ390SP26/Lectures/Lecture16_APIs_empty.ipynb)

Download Jupyter Notebook Completed

# Econ 390 - Lecture 16: APIs
Today we will go over Application Programming Interfaces (APIs), which are a very powerful tool but also one that must be used carefully. Turrell goes over it [here](https://aeturrell.github.io/coding-for-economists/data-extraction.html#obtaining-data-using-apis) and provides other methods of using APIs not covered in this class.


```python
import pandas_datareader
# We have to install it!
```


    ---------------------------------------------------------------------------

    ModuleNotFoundError                       Traceback (most recent call last)

    Cell In[1], line 1
    ----> 1 import pandas_datareader
    

    ModuleNotFoundError: No module named 'pandas_datareader'


## Installing a New Package
Open up "Anaconda Prompt" either by searching for an app on Windows (Windows Key + type in "Anaconda Prompt", clicking on it) or Mac Key + Space to open spotlight search, type "Terminal", and press return to open (you may need to hit Cmd + N to open a new window).

Assuming you only have one environment (if that's confusing to you - you only have one) it will always work on your base (and only) environment. 

To check if we have it downloaded type `conda list` and search for pandas-datareader. If you don't find it, that's because you don't have it installed!

To make sure we can actually download it this way, search for it by doing `conda search pandas-datareader`. This will show you any versions available to download here. By default it will download the newest version. To actually download, type `conda install pandas-datareader` and type `Y` when prompted.

Now it should be downloaded and you can type `exit` to close out and return here! Though you may need to restart the kernal using the kernal tab above to make use of the newly installed library.

pandas-datareader lets us interact with:
- FRED
- Quandl
- World Bank
- OECD
- Eurostat



```python
# All of our imports
import pandas as pd 
import numpy as np
import matplotlib.pyplot as plt
import pandas_datareader.data as web    
```

## FRED


```python
# Downloading straight from FRED
```


```python
# Default Index?

```


```python
# Rename variables and update to percent change
```


```python
# Now we can easily plot with our paper stylesheet!
```


```python
# Make it easily updateable
```

## Stooq


```python
# Dow Jones using Stooq
```


```python
# Plot the Dow Jones
```

## World Bank


```python

# Define parameters

# Get data from World Bank

```


```python
# Rename
```


```python
# Using our paper stylesheet
```


```python
# What is the US?
```


```python
# Highlight the US
```

## Practice - FRED
1. Go to the FRED website and find the series for "Infra-Annual Labor Statistics: Working-Age Population Total: From 15 to 64 Years for United States" and "Real Gross Domestic Product"
2. First modify the code below plot the Real GDP in the U.S. from 1960-Today. What are the units? Do we need a legend anymore?
3. Modify the code below to calculate and plot the Real GDP per Capita in 2017 dollars.


```python
codes = {'CPIAUCSL' : 'CPI', 'CPILFESL' :'Core CPI'}
fred_CPI = web.DataReader(codes.keys(), 'fred', start='2010-01-01')
fred_CPI = fred_CPI.rename(columns=codes).pct_change(periods=12)*100

# Now we can easily plot with our paper stylesheet!
with plt.style.context('paper.mplstyle'):
    fig, ax = plt.subplots()
    ax.plot(fred_CPI.index, fred_CPI['CPI'], label='CPI')
    ax.plot(fred_CPI.index, fred_CPI['Core CPI'], label='Core CPI')
    ax.set_ylabel('% Change from Year Ago')
    ax.set_title('CPI and Core CPI Inflation, 2011-{}'.format(fred.index[-1].strftime('%Y')))
    ax.legend()

plt.show()
```


```python
# Results
```
