---
layout: single
sitemap: false
permalink: /pages/Econ_390_SP26_L16/
title: Econ 390 Lecture 16
---

[Download Jupyter Notebook Empty](https://m-mcmain.github.io/files/Econ390SP26/Lectures/Lecture16_APIs_empty.ipynb)

[Download Jupyter Notebook Completed](https://m-mcmain.github.io/files/Econ390SP26/Lectures/Lecture16_APIs_full.ipynb)

# Econ 390 - Lecture 16: APIs
Today we will go over Application Programming Interfaces (APIs), which are a very powerful tool but also one that must be used carefully. Turrell goes over it [here](https://aeturrell.github.io/coding-for-economists/data-extraction.html#obtaining-data-using-apis) and provides other methods of using APIs not covered in this class.


```python
import pandas_datareader
# We have to install it!
```

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
codes = {"CPIAUCSL":"CPI", "CUSR0000SACL1E":"Core CPI"}
fred_CPI = web.DataReader(codes.keys(), 'fred', start="2010-01-01", end="2025-01-01")

fred_CPI
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
      <th>CPIAUCSL</th>
      <th>CUSR0000SACL1E</th>
    </tr>
    <tr>
      <th>DATE</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2010-01-01</th>
      <td>217.488</td>
      <td>144.114</td>
    </tr>
    <tr>
      <th>2010-02-01</th>
      <td>217.281</td>
      <td>144.055</td>
    </tr>
    <tr>
      <th>2010-03-01</th>
      <td>217.353</td>
      <td>143.879</td>
    </tr>
    <tr>
      <th>2010-04-01</th>
      <td>217.403</td>
      <td>143.454</td>
    </tr>
    <tr>
      <th>2010-05-01</th>
      <td>217.290</td>
      <td>143.304</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>2024-09-01</th>
      <td>314.732</td>
      <td>164.634</td>
    </tr>
    <tr>
      <th>2024-10-01</th>
      <td>315.631</td>
      <td>164.698</td>
    </tr>
    <tr>
      <th>2024-11-01</th>
      <td>316.528</td>
      <td>165.018</td>
    </tr>
    <tr>
      <th>2024-12-01</th>
      <td>317.604</td>
      <td>165.006</td>
    </tr>
    <tr>
      <th>2025-01-01</th>
      <td>318.961</td>
      <td>165.508</td>
    </tr>
  </tbody>
</table>
<p>181 rows × 2 columns</p>
</div>




```python
# Default Index?
fred_CPI.index
```




    DatetimeIndex(['2010-01-01', '2010-02-01', '2010-03-01', '2010-04-01',
                   '2010-05-01', '2010-06-01', '2010-07-01', '2010-08-01',
                   '2010-09-01', '2010-10-01',
                   ...
                   '2024-04-01', '2024-05-01', '2024-06-01', '2024-07-01',
                   '2024-08-01', '2024-09-01', '2024-10-01', '2024-11-01',
                   '2024-12-01', '2025-01-01'],
                  dtype='datetime64[ns]', name='DATE', length=181, freq=None)




```python
# Rename variables and update to percent change
fred_CPI = fred_CPI.rename(columns=codes).pct_change(periods=12)*100
fred_CPI
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
      <th>CPI</th>
      <th>Core CPI</th>
    </tr>
    <tr>
      <th>DATE</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2010-01-01</th>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2010-02-01</th>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2010-03-01</th>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2010-04-01</th>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2010-05-01</th>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>2024-09-01</th>
      <td>2.426483</td>
      <td>-1.155153</td>
    </tr>
    <tr>
      <th>2024-10-01</th>
      <td>2.578844</td>
      <td>-1.199182</td>
    </tr>
    <tr>
      <th>2024-11-01</th>
      <td>2.719472</td>
      <td>-0.743441</td>
    </tr>
    <tr>
      <th>2024-12-01</th>
      <td>2.870691</td>
      <td>-0.668806</td>
    </tr>
    <tr>
      <th>2025-01-01</th>
      <td>2.990978</td>
      <td>-0.077881</td>
    </tr>
  </tbody>
</table>
<p>181 rows × 2 columns</p>
</div>




```python
# Now we can easily plot with our paper stylesheet!
with plt.style.context("paper.mplstyle"):
    fig, ax = plt.subplots()
    ax.plot(fred_CPI.index, fred_CPI["CPI"], label="CPI")
    ax.plot(fred_CPI.index, fred_CPI["Core CPI"], label="Core CPI")
    ax.set_ylabel("% change from Year Ago")
    ax.set_title("CPI and Core CPI Inflation, 2011-2026")
    ax.legend()

plt.show()    
```


    
![png](output_8_0.png)
    



```python
fred_CPI.index[-1].strftime("%Y")
```




    '2025'




```python
# Make it easily updateable
with plt.style.context("paper.mplstyle"):
    fig, ax = plt.subplots()
    ax.plot(fred_CPI.index, fred_CPI["CPI"], label="CPI")
    ax.plot(fred_CPI.index, fred_CPI["Core CPI"], label="Core CPI")
    ax.set_ylabel("% change from Year Ago")
    ax.set_title("CPI and Core CPI Inflation, 2011-{}".format(fred_CPI.index[-1].strftime("%Y")))
    ax.legend()

plt.show()    
```


    
![png](output_10_0.png)
    


## Stooq


```python
# Dow Jones using Stooq
dowjones = web.DataReader("^DJI", "stooq")

dowjones
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
      <th>Open</th>
      <th>High</th>
      <th>Low</th>
      <th>Close</th>
      <th>Volume</th>
    </tr>
    <tr>
      <th>Date</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2026-03-18</th>
      <td>46913.93</td>
      <td>46913.93</td>
      <td>46193.06</td>
      <td>46225.15</td>
      <td>374362046.0</td>
    </tr>
    <tr>
      <th>2026-03-17</th>
      <td>47085.53</td>
      <td>47428.12</td>
      <td>46975.52</td>
      <td>46993.26</td>
      <td>365216860.0</td>
    </tr>
    <tr>
      <th>2026-03-16</th>
      <td>46707.40</td>
      <td>47176.14</td>
      <td>46707.40</td>
      <td>46946.41</td>
      <td>382305552.0</td>
    </tr>
    <tr>
      <th>2026-03-13</th>
      <td>46689.24</td>
      <td>47123.99</td>
      <td>46494.63</td>
      <td>46558.47</td>
      <td>343069925.0</td>
    </tr>
    <tr>
      <th>2026-03-12</th>
      <td>47242.52</td>
      <td>47242.52</td>
      <td>46662.23</td>
      <td>46677.85</td>
      <td>448812175.0</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>2021-03-26</th>
      <td>32681.07</td>
      <td>33098.83</td>
      <td>32681.07</td>
      <td>33072.88</td>
      <td>440533072.0</td>
    </tr>
    <tr>
      <th>2021-03-25</th>
      <td>32346.81</td>
      <td>32672.69</td>
      <td>32071.41</td>
      <td>32619.48</td>
      <td>463916838.0</td>
    </tr>
    <tr>
      <th>2021-03-24</th>
      <td>32470.88</td>
      <td>32787.99</td>
      <td>32418.15</td>
      <td>32420.06</td>
      <td>456858883.0</td>
    </tr>
    <tr>
      <th>2021-03-23</th>
      <td>32691.50</td>
      <td>32753.77</td>
      <td>32356.28</td>
      <td>32423.15</td>
      <td>453064617.0</td>
    </tr>
    <tr>
      <th>2021-03-22</th>
      <td>32601.82</td>
      <td>32810.35</td>
      <td>32512.53</td>
      <td>32731.20</td>
      <td>452080903.0</td>
    </tr>
  </tbody>
</table>
<p>1254 rows × 5 columns</p>
</div>




```python
# Plot the Dow Jones
with plt.style.context("paper.mplstyle"):
    fig, ax = plt.subplots()
    ax.plot(dowjones.index, dowjones["Close"])
    ax.set_ylabel("Closing Price")
    ax.set_title("Dow Jones Industrial Average\n"
                 '{0} to {1}'.format(dowjones.index[-1].strftime("%B %Y"),
                                     dowjones.index[1].strftime("%B %Y")))

plt.show()
```


    
![png](output_13_0.png)
    


## World Bank


```python
from pandas_datareader import wb
# Define parameters
indicators={"SL.AGR.EMPL.ZS":"Employment in Agriculture"}
countries = ["ALL"]
year = 2000

# Get data from World Bank
wb_AGEMP = wb.download(indicator=indicators.keys(),
                       country=countries,
                       start=year,
                       end=year)

wb_AGEMP
```

    C:\Users\micha\AppData\Local\Temp\ipykernel_22184\805732853.py:8: FutureWarning: errors='ignore' is deprecated and will raise in a future version. Use to_numeric without passing `errors` and catch exceptions explicitly instead
      wb_AGEMP = wb.download(indicator=indicators.keys(),
    




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
      <th></th>
      <th>SL.AGR.EMPL.ZS</th>
    </tr>
    <tr>
      <th>country</th>
      <th>year</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Africa Eastern and Southern</th>
      <th>2000</th>
      <td>61.819233</td>
    </tr>
    <tr>
      <th>Africa Western and Central</th>
      <th>2000</th>
      <td>57.017447</td>
    </tr>
    <tr>
      <th>Arab World</th>
      <th>2000</th>
      <td>28.764743</td>
    </tr>
    <tr>
      <th>Caribbean small states</th>
      <th>2000</th>
      <td>12.877604</td>
    </tr>
    <tr>
      <th>Central Europe and the Baltics</th>
      <th>2000</th>
      <td>17.877201</td>
    </tr>
    <tr>
      <th>...</th>
      <th>...</th>
      <td>...</td>
    </tr>
    <tr>
      <th>Virgin Islands (U.S.)</th>
      <th>2000</th>
      <td>2.941990</td>
    </tr>
    <tr>
      <th>West Bank and Gaza</th>
      <th>2000</th>
      <td>12.481793</td>
    </tr>
    <tr>
      <th>Yemen, Rep.</th>
      <th>2000</th>
      <td>54.769359</td>
    </tr>
    <tr>
      <th>Zambia</th>
      <th>2000</th>
      <td>76.009971</td>
    </tr>
    <tr>
      <th>Zimbabwe</th>
      <th>2000</th>
      <td>49.732588</td>
    </tr>
  </tbody>
</table>
<p>266 rows × 1 columns</p>
</div>




```python
# Rename
wb_AGEMP = wb_AGEMP.rename(columns=indicators)
wb_AGEMP
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
      <th></th>
      <th>Employment in Agriculture</th>
    </tr>
    <tr>
      <th>country</th>
      <th>year</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Africa Eastern and Southern</th>
      <th>2000</th>
      <td>61.819233</td>
    </tr>
    <tr>
      <th>Africa Western and Central</th>
      <th>2000</th>
      <td>57.017447</td>
    </tr>
    <tr>
      <th>Arab World</th>
      <th>2000</th>
      <td>28.764743</td>
    </tr>
    <tr>
      <th>Caribbean small states</th>
      <th>2000</th>
      <td>12.877604</td>
    </tr>
    <tr>
      <th>Central Europe and the Baltics</th>
      <th>2000</th>
      <td>17.877201</td>
    </tr>
    <tr>
      <th>...</th>
      <th>...</th>
      <td>...</td>
    </tr>
    <tr>
      <th>Virgin Islands (U.S.)</th>
      <th>2000</th>
      <td>2.941990</td>
    </tr>
    <tr>
      <th>West Bank and Gaza</th>
      <th>2000</th>
      <td>12.481793</td>
    </tr>
    <tr>
      <th>Yemen, Rep.</th>
      <th>2000</th>
      <td>54.769359</td>
    </tr>
    <tr>
      <th>Zambia</th>
      <th>2000</th>
      <td>76.009971</td>
    </tr>
    <tr>
      <th>Zimbabwe</th>
      <th>2000</th>
      <td>49.732588</td>
    </tr>
  </tbody>
</table>
<p>266 rows × 1 columns</p>
</div>




```python
# Using our paper stylesheet
with plt.style.context("paper.mplstyle"):
    # Histogram of employment in agriculture
    fig, ax = plt.subplots()
    ax.hist(wb_AGEMP["Employment in Agriculture"])
    ax.set(xlabel="% of Employment in Agriculture",
          title="Distribution of Employment in Agriculture\n In {}".format(year))

plt.show()
```


    
![png](output_17_0.png)
    



```python
# What is the US?
wb_AGEMP.loc["United States"]
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
      <th>Employment in Agriculture</th>
    </tr>
    <tr>
      <th>year</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2000</th>
      <td>2.396546</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Highlight the US
with plt.style.context("paper.mplstyle"):
    # Histogram of employment in agriculture
    fig, ax = plt.subplots()
    ax.hist(wb_AGEMP["Employment in Agriculture"])
    ax.set(xlabel="% of Employment in Agriculture",
          title="Distribution of Employment in Agriculture\n In {}".format(year))
    ax.axvline(x = 2.4, color="red")
    ax.text(3.5, 60,"United States", color="red")

plt.show()
```


    
![png](output_19_0.png)
    


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
codes = {'LFWA64TTUSA647N': 'working age pop', 'GDPCA': 'gdp'}
fred = web.DataReader(codes.keys(), 'fred', start='1960-01-01')
fred = fred.rename(columns=codes)           
fred['gdp_per_capita'] = fred['gdp']*1000000000/fred['working age pop']

with plt.style.context('paper.mplstyle'):
    fig, ax = plt.subplots()
    ax.plot(fred.index, fred['gdp_per_capita'])
    ax.set_ylabel('2012 Dollars')
    ax.set_title('U.S. real GDP per working-age person, 1960-{}'.format(fred.index[-1].strftime('%Y')))

plt.show()
```


    
![png](output_22_0.png)
    

