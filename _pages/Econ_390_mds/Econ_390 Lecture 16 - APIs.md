---
layout: single
sitemap: false
permalink: /pages/Econ_390_SP26_L16_teaching/
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
codes = {'CPIAUCSL' : 'CPI', 'CPILFESL' :'Core CPI'}
fred_CPI = web.DataReader(codes.keys(), 'fred', start='2010-01-01')

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
      <th>CPILFESL</th>
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
      <td>220.633</td>
    </tr>
    <tr>
      <th>2010-02-01</th>
      <td>217.281</td>
      <td>220.731</td>
    </tr>
    <tr>
      <th>2010-03-01</th>
      <td>217.353</td>
      <td>220.783</td>
    </tr>
    <tr>
      <th>2010-04-01</th>
      <td>217.403</td>
      <td>220.822</td>
    </tr>
    <tr>
      <th>2010-05-01</th>
      <td>217.290</td>
      <td>220.962</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>2025-10-01</th>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2025-11-01</th>
      <td>325.063</td>
      <td>331.043</td>
    </tr>
    <tr>
      <th>2025-12-01</th>
      <td>326.031</td>
      <td>331.814</td>
    </tr>
    <tr>
      <th>2026-01-01</th>
      <td>326.588</td>
      <td>332.793</td>
    </tr>
    <tr>
      <th>2026-02-01</th>
      <td>327.460</td>
      <td>333.512</td>
    </tr>
  </tbody>
</table>
<p>194 rows × 2 columns</p>
</div>




```python
# Default Index?
fred_CPI.index
```




    DatetimeIndex(['2010-01-01', '2010-02-01', '2010-03-01', '2010-04-01',
                   '2010-05-01', '2010-06-01', '2010-07-01', '2010-08-01',
                   '2010-09-01', '2010-10-01',
                   ...
                   '2025-05-01', '2025-06-01', '2025-07-01', '2025-08-01',
                   '2025-09-01', '2025-10-01', '2025-11-01', '2025-12-01',
                   '2026-01-01', '2026-02-01'],
                  dtype='datetime64[ns]', name='DATE', length=194, freq=None)




```python
# Rename variables and update to percent change
fred_CPI = fred_CPI.rename(columns=codes).pct_change(periods=12)*100
fred_CPI
```

    C:\Users\micha\AppData\Local\Temp\ipykernel_22580\3934747043.py:2: FutureWarning: The default fill_method='pad' in DataFrame.pct_change is deprecated and will be removed in a future version. Either fill in any non-leading NA values prior to calling pct_change or specify 'fill_method=None' to not fill NA values.
      fred_CPI = fred_CPI.rename(columns=codes).pct_change(periods=12)*100
    




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
      <th>2025-10-01</th>
      <td>2.729136</td>
      <td>2.700082</td>
    </tr>
    <tr>
      <th>2025-11-01</th>
      <td>2.696444</td>
      <td>2.599045</td>
    </tr>
    <tr>
      <th>2025-12-01</th>
      <td>2.653304</td>
      <td>2.646485</td>
    </tr>
    <tr>
      <th>2026-01-01</th>
      <td>2.391201</td>
      <td>2.512029</td>
    </tr>
    <tr>
      <th>2026-02-01</th>
      <td>2.434004</td>
      <td>2.472462</td>
    </tr>
  </tbody>
</table>
<p>194 rows × 2 columns</p>
</div>




```python
# Now we can easily plot with our paper stylesheet!
with plt.style.context('paper.mplstyle'):
    fig, ax = plt.subplots()
    ax.plot(fred_CPI.index, fred_CPI['CPI'], label='CPI')
    ax.plot(fred_CPI.index, fred_CPI['Core CPI'], label='Core CPI')
    ax.set_ylabel('% Change from Year Ago')
    ax.set_title('CPI and Core CPI Inflation, 2011-2025')
    ax.legend()

plt.show()
```


    
![png](output_8_0.png)
    



```python
# Make it easily updateable
with plt.style.context('paper.mplstyle'):
    fig, ax = plt.subplots()
    ax.plot(fred_CPI.index, fred_CPI['CPI'], label='CPI')
    ax.plot(fred_CPI.index, fred_CPI['Core CPI'], label='Core CPI')
    ax.set_ylabel('% Change from Year Ago')
    ax.set_title('CPI and Core CPI Inflation, 2011-{}'.format(fred_CPI.index[-1].strftime('%Y')))
    ax.legend()

plt.show()
```


    
![png](output_9_0.png)
    


## Stooq


```python
# Dow Jones using Stooq
dj = web.DataReader('^DJI', 'stooq')

dj
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
      <th>2026-03-11</th>
      <td>47690.76</td>
      <td>47711.26</td>
      <td>47185.89</td>
      <td>47417.27</td>
      <td>332181934.0</td>
    </tr>
    <tr>
      <th>2026-03-10</th>
      <td>47771.43</td>
      <td>48220.54</td>
      <td>47444.23</td>
      <td>47706.51</td>
      <td>387461423.0</td>
    </tr>
    <tr>
      <th>2026-03-09</th>
      <td>47371.28</td>
      <td>47876.06</td>
      <td>46615.52</td>
      <td>47740.80</td>
      <td>441826180.0</td>
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
      <th>2021-03-22</th>
      <td>32601.82</td>
      <td>32810.35</td>
      <td>32512.53</td>
      <td>32731.20</td>
      <td>452080903.0</td>
    </tr>
    <tr>
      <th>2021-03-19</th>
      <td>32858.36</td>
      <td>32858.36</td>
      <td>32505.07</td>
      <td>32627.97</td>
      <td>977294552.0</td>
    </tr>
    <tr>
      <th>2021-03-18</th>
      <td>32928.16</td>
      <td>33227.78</td>
      <td>32831.25</td>
      <td>32862.30</td>
      <td>479266434.0</td>
    </tr>
    <tr>
      <th>2021-03-17</th>
      <td>32825.52</td>
      <td>33047.58</td>
      <td>32782.18</td>
      <td>33015.37</td>
      <td>456961442.0</td>
    </tr>
    <tr>
      <th>2021-03-16</th>
      <td>32966.75</td>
      <td>32966.75</td>
      <td>32778.23</td>
      <td>32825.95</td>
      <td>439929862.0</td>
    </tr>
  </tbody>
</table>
<p>1255 rows × 5 columns</p>
</div>




```python
# Plot the Dow Jones
with plt.style.context('paper.mplstyle'):
    fig, ax = plt.subplots()
    ax.plot(dj.index, dj['Close'])
    ax.set_ylabel('Closing Price')
    ax.set_title('Dow Jones Industrial Average\n'
                 '{0} to {1}'.format(dj.index[-1].strftime('%b %Y'),
                                     dj.index[1].strftime('%b %Y')))
    
plt.show()
```


    
![png](output_12_0.png)
    


## World Bank


```python
from pandas_datareader import wb

# Define parameters
indicators={'SL.AGR.EMPL.ZS':'Employment in Agriculture'}
countries = ['ALL']
year = 2023

# Get data from World Bank
wb_AGEMP = wb.download(indicator=indicators.keys(), 
                     country=countries,
                     start=year,
                     end=year)

wb_AGEMP
```

    C:\Users\micha\AppData\Local\Temp\ipykernel_22580\1917177683.py:9: FutureWarning: errors='ignore' is deprecated and will raise in a future version. Use to_numeric without passing `errors` and catch exceptions explicitly instead
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
      <th>2023</th>
      <td>57.217894</td>
    </tr>
    <tr>
      <th>Africa Western and Central</th>
      <th>2023</th>
      <td>42.140857</td>
    </tr>
    <tr>
      <th>Arab World</th>
      <th>2023</th>
      <td>13.898781</td>
    </tr>
    <tr>
      <th>Caribbean small states</th>
      <th>2023</th>
      <td>7.019453</td>
    </tr>
    <tr>
      <th>Central Europe and the Baltics</th>
      <th>2023</th>
      <td>7.097861</td>
    </tr>
    <tr>
      <th>...</th>
      <th>...</th>
      <td>...</td>
    </tr>
    <tr>
      <th>Virgin Islands (U.S.)</th>
      <th>2023</th>
      <td>1.673265</td>
    </tr>
    <tr>
      <th>West Bank and Gaza</th>
      <th>2023</th>
      <td>NaN</td>
    </tr>
    <tr>
      <th>Yemen, Rep.</th>
      <th>2023</th>
      <td>31.962620</td>
    </tr>
    <tr>
      <th>Zambia</th>
      <th>2023</th>
      <td>55.968834</td>
    </tr>
    <tr>
      <th>Zimbabwe</th>
      <th>2023</th>
      <td>55.449432</td>
    </tr>
  </tbody>
</table>
<p>266 rows × 1 columns</p>
</div>




```python
# Rename
wb_AGEMP = wb_AGEMP.rename(columns = indicators)
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
      <th>2023</th>
      <td>57.217894</td>
    </tr>
    <tr>
      <th>Africa Western and Central</th>
      <th>2023</th>
      <td>42.140857</td>
    </tr>
    <tr>
      <th>Arab World</th>
      <th>2023</th>
      <td>13.898781</td>
    </tr>
    <tr>
      <th>Caribbean small states</th>
      <th>2023</th>
      <td>7.019453</td>
    </tr>
    <tr>
      <th>Central Europe and the Baltics</th>
      <th>2023</th>
      <td>7.097861</td>
    </tr>
    <tr>
      <th>...</th>
      <th>...</th>
      <td>...</td>
    </tr>
    <tr>
      <th>Virgin Islands (U.S.)</th>
      <th>2023</th>
      <td>1.673265</td>
    </tr>
    <tr>
      <th>West Bank and Gaza</th>
      <th>2023</th>
      <td>NaN</td>
    </tr>
    <tr>
      <th>Yemen, Rep.</th>
      <th>2023</th>
      <td>31.962620</td>
    </tr>
    <tr>
      <th>Zambia</th>
      <th>2023</th>
      <td>55.968834</td>
    </tr>
    <tr>
      <th>Zimbabwe</th>
      <th>2023</th>
      <td>55.449432</td>
    </tr>
  </tbody>
</table>
<p>266 rows × 1 columns</p>
</div>




```python
# Using our paper stylesheet
with plt.style.context('paper.mplstyle'):

    # Histogram of Employment in Agriculture
    fig, ax = plt.subplots()
    ax.hist(wb_AGEMP['Employment in Agriculture'])
    
plt.show()
```


    
![png](output_16_0.png)
    



```python
# What is the US?
wb_AGEMP.loc['United States']
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
      <th>2023</th>
      <td>1.56961</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Highlight the US
with plt.style.context('paper.mplstyle'):

    # Histogram of Employment in Agriculture
    fig, ax = plt.subplots()
    ax.hist(wb_AGEMP['Employment in Agriculture'])
    ax.set(xlabel='% of Emplyment in Agriculture',
           title='Distribution of Employment in Agriculture\n{}'.format(year))
    ax.axvline(x=1.56961, color='red')
    ax.text(3,79, 'United States', color='red')
    
plt.show()
```


    
![png](output_18_0.png)
    


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
    ax.set_title('CPI and Core CPI Inflation, 2011-{}'.format(fred_CPI.index[-1].strftime('%Y')))
    ax.legend()

plt.show()
```

    C:\Users\micha\AppData\Local\Temp\ipykernel_22580\449419214.py:3: FutureWarning: The default fill_method='pad' in DataFrame.pct_change is deprecated and will be removed in a future version. Either fill in any non-leading NA values prior to calling pct_change or specify 'fill_method=None' to not fill NA values.
      fred_CPI = fred_CPI.rename(columns=codes).pct_change(periods=12)*100
    


    
![png](output_20_1.png)
    



```python
# Results
codes = {'LFWA64TTUSA647N': 'working age pop', 'GDPCA': 'gdp'}
fred = web.DataReader(codes.keys(), 'fred', start='1960-01-01')
fred = fred.rename(columns=codes)           
fred['gdp_per_capita'] = fred['gdp']*1000000000/fred['working age pop']

with plt.style.context('paper.mplstyle'):
    fig, ax = plt.subplots()
    ax.plot(fred.index, fred['gdp_per_capita'])
    ax.set_ylabel('2012 dollars')
    ax.set_title('U.S. real GDP per working-age person, 1960-{}'.format(fred.index[-1].strftime('%Y')))

plt.show()
```


    
![png](output_21_0.png)
    

