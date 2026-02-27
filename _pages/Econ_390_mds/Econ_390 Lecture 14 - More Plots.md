---
layout: single
sitemap: false
permalink: /pages/Econ_390_SP26_L14_teaching/
---

[Download Jupyter Notebook Empty](https://m-mcmain.github.io/files/Econ390SP26/Lectures/Lecture14_MorePlots_empty.ipynb)

Download Jupyter Notebook Completed

# Econ 390 - Lecture 14: More Plots
Today we will be going over making plots with Matplotlib that aren't line plots. Appropriate material is [the rest of Chapter 9 that is not about line plots in McKinney](https://wesmckinney.com/book/plotting-and-visualization) and similar for [Turrell](https://aeturrell.github.io/coding-for-economists/vis-matplotlib.html).

## Subplots


```python
# As always
import pandas as pd, matplotlib.pyplot as plt
from datetime import datetime
USD_ER = pd.read_csv('https://m-mcmain.github.io/files/Econ390SP26/USD_ERs.csv', index_col = 0, parse_dates = True)
USD_ER = USD_ER.rename(columns={"DEXUSEU_NBD20060101":"USD_EU", "DEXCHUS_NBD20060101":"CHY_USD", "DTWEXBGS_NBD20060101":"USD_Broad"})
USD_ER
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
      <th>USD_Broad</th>
      <th>CHY_USD</th>
      <th>USD_EU</th>
    </tr>
    <tr>
      <th>observation_date</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2006-01-01</th>
      <td>100.00000</td>
      <td>100.00000</td>
      <td>100.00000</td>
    </tr>
    <tr>
      <th>2006-02-01</th>
      <td>100.21117</td>
      <td>99.82489</td>
      <td>98.46800</td>
    </tr>
    <tr>
      <th>2006-03-01</th>
      <td>100.42808</td>
      <td>99.62384</td>
      <td>99.19950</td>
    </tr>
    <tr>
      <th>2006-04-01</th>
      <td>99.74348</td>
      <td>99.36736</td>
      <td>101.21851</td>
    </tr>
    <tr>
      <th>2006-05-01</th>
      <td>97.51177</td>
      <td>99.35193</td>
      <td>105.29425</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>2025-07-01</th>
      <td>120.52656</td>
      <td>88.94931</td>
      <td>96.25020</td>
    </tr>
    <tr>
      <th>2025-08-01</th>
      <td>120.98444</td>
      <td>88.93206</td>
      <td>96.05770</td>
    </tr>
    <tr>
      <th>2025-09-01</th>
      <td>120.45339</td>
      <td>88.32157</td>
      <td>96.81015</td>
    </tr>
    <tr>
      <th>2025-10-01</th>
      <td>121.17118</td>
      <td>88.27831</td>
      <td>96.00204</td>
    </tr>
    <tr>
      <th>2025-11-01</th>
      <td>121.80375</td>
      <td>88.11608</td>
      <td>95.32070</td>
    </tr>
  </tbody>
</table>
<p>239 rows × 3 columns</p>
</div>




```python
# Initialize our figure
fig = plt.figure()
```


    <Figure size 640x480 with 0 Axes>



```python
# Add Subplot method
ax1 = fig.add_subplot(2,2,1)
fig
```




    
![png](output_4_0.png)
    




```python
# More?
ax2 = fig.add_subplot(2,2,2)
ax3 = fig.add_subplot(2,2,3)
fig
```




    
![png](output_5_0.png)
    




```python
# Fill out one of the subplots
ax3.plot(USD_ER.index, USD_ER['USD_Broad'], color = "black", linestyle = ':')
fig
```




    
![png](output_6_0.png)
    




```python
# And the others
ax1.plot(USD_ER.index, USD_ER['CHY_USD'], linestyle = ':')
ax2.plot(USD_ER.index, USD_ER['USD_EU'], linestyle = ':')
fig
```




    
![png](output_7_0.png)
    




```python
# Reshape to move panels around and access like a list
fig, ax = plt.subplots(2,2)
ax = ax.reshape(-1)
ax[2].plot([1, 10], [10, 1])
```




    [<matplotlib.lines.Line2D at 0x1fa056ae490>]




    
![png](output_8_1.png)
    



```python
# Side by side subplots
plot_color = 'blue'

fig,ax = plt.subplots(1,2)

ax[0].plot(USD_ER.index, USD_ER['CHY_USD'], color=plot_color)
ax[0].set(ylim=(75,130),
          title=('Chinese Yuan to USD'),
          xlabel=('Year'),
          ylabel=('Exchange Rate Index'))
ax[0].spines[['top','right']].set_visible(False)

ax[1].plot(USD_ER.index, USD_ER['USD_Broad'], color=plot_color)
ax[1].set(ylim=(75,130),
          title=('Broad USD'),
          xlabel=('Year'),
          ylabel=('Exchange Rate Index'))
ax[1].spines[['top','right']].set_visible(False)

plt.show()
```


    
![png](output_9_0.png)
    



```python
# Making it look a bit nicer
plot_color = 'blue'

fig,ax = plt.subplots(1,2, figsize=(16,9))

ax[0].plot(USD_ER.index, USD_ER['CHY_USD'], color=plot_color)
ax[0].set(ylim=(75,130),
          title=('Chinese Yuan to USD'),
          xlabel=('Year'),
          ylabel=('Exchange Rate Index'))
ax[0].spines[['top','right']].set_visible(False)

ax[1].plot(USD_ER.index, USD_ER['USD_Broad'], color=plot_color)
ax[1].set(ylim=(75,130),
          title=('Broad USD'),
          xlabel=('Year'))
ax[1].spines[['top','right']].set_visible(False)

plt.show()
```


    
![png](output_10_0.png)
    



```python
# Let's utilize a loop to be more efficient
fig,ax = plt.subplots(1,2, figsize=(16,9))

# To do so, we need a subset that only has CHY_USD and USD_Broad
USD_ER_CHYBroad = USD_ER.drop('USD_EU', axis=1)

for i, ER in enumerate(USD_ER_CHYBroad.columns):
    ax[i].plot(USD_ER.index, USD_ER[ER], color=plot_color)
    ax[i].set(ylim=(75,130),
              title=(ER),
              xlabel=('Year'))
    ax[i].spines[['top','right']].set_visible(False)

ax[0].set(ylabel=('Exchange Rate Index'))

plt.show()
```


    
![png](output_11_0.png)
    



```python
# Generate World Plot
fig, ax = plt.subplots(figsize=(16,9)) 
ax.plot(USD_ER.index, USD_ER['USD_Broad'])
ax.set(ylim=(75,132), title='Broad USD',
       xlabel='Year', ylabel='Exchange Rate Index')
ax.spines[['top','right']].set_visible(False)

# Generate Regional Plots
fig, ax = plt.subplots(1, 2, figsize=(16,9), sharex=True, sharey=True)
ax = ax.reshape(-1)
for i, ER in enumerate(USD_ER.columns[USD_ER.columns != "USD_Broad"]):     
        ax[i].plot(USD_ER.index, USD_ER[ER], label=ER)
        ax[i].set(title=ER, ylim=(75,132))
        ax[i].spines[['top','right']].set_visible(False)

# Label Regional Graph Axes
ax[0].set_ylabel('Exchange Rate Index')
ax[0].set_xlabel('Year')
ax[1].set_xlabel('Year')
plt.show()
```


    
![png](output_12_0.png)
    



    
![png](output_12_1.png)
    


## Histograms


```python
# Calculating percent growth of variables
USD_ER['USD_Broad_growth'] = USD_ER['USD_Broad'].pct_change()*100
USD_ER
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
      <th>USD_Broad</th>
      <th>CHY_USD</th>
      <th>USD_EU</th>
      <th>USD_Broad_growth</th>
    </tr>
    <tr>
      <th>observation_date</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2006-01-01</th>
      <td>100.00000</td>
      <td>100.00000</td>
      <td>100.00000</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2006-02-01</th>
      <td>100.21117</td>
      <td>99.82489</td>
      <td>98.46800</td>
      <td>0.211170</td>
    </tr>
    <tr>
      <th>2006-03-01</th>
      <td>100.42808</td>
      <td>99.62384</td>
      <td>99.19950</td>
      <td>0.216453</td>
    </tr>
    <tr>
      <th>2006-04-01</th>
      <td>99.74348</td>
      <td>99.36736</td>
      <td>101.21851</td>
      <td>-0.681682</td>
    </tr>
    <tr>
      <th>2006-05-01</th>
      <td>97.51177</td>
      <td>99.35193</td>
      <td>105.29425</td>
      <td>-2.237450</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>2025-07-01</th>
      <td>120.52656</td>
      <td>88.94931</td>
      <td>96.25020</td>
      <td>-0.370449</td>
    </tr>
    <tr>
      <th>2025-08-01</th>
      <td>120.98444</td>
      <td>88.93206</td>
      <td>96.05770</td>
      <td>0.379900</td>
    </tr>
    <tr>
      <th>2025-09-01</th>
      <td>120.45339</td>
      <td>88.32157</td>
      <td>96.81015</td>
      <td>-0.438941</td>
    </tr>
    <tr>
      <th>2025-10-01</th>
      <td>121.17118</td>
      <td>88.27831</td>
      <td>96.00204</td>
      <td>0.595907</td>
    </tr>
    <tr>
      <th>2025-11-01</th>
      <td>121.80375</td>
      <td>88.11608</td>
      <td>95.32070</td>
      <td>0.522047</td>
    </tr>
  </tbody>
</table>
<p>239 rows × 4 columns</p>
</div>




```python
# Plotting growth rates
fig, ax = plt.subplots() 

ax.plot(USD_ER.index, USD_ER['USD_Broad_growth'], color='red')  
ax.set(ylabel='Monthly Percent Growth', title='Broad USD Growth Rates')
ax.spines[['right', 'top']].set_visible(False)

# Add a horizontal line at y=0 for reference
ax.axhline(y=0, color='black', linewidth=0.75)  

plt.show()
```


    
![png](output_15_0.png)
    



```python
# Histogram is more suitable
fig, ax = plt.subplots() 

ax.hist(USD_ER['USD_Broad_growth'])       

plt.show()
```


    
![png](output_16_0.png)
    



```python
# Default methods
ax = USD_ER['USD_Broad_growth'].plot.hist()
```


    
![png](output_17_0.png)
    



```python
# Adding our usuals
fig, ax = plt.subplots() 

ax.hist(USD_ER['USD_Broad_growth'], bins=20)
ax.set(ylabel='Frequency',
       xlabel='Monthly growth rate (%)',
       title='Frequency of Broad USD growth rates (2006-2025)')

ax.spines[['right','top']].set_visible(False)

plt.show()
```


    
![png](output_18_0.png)
    


## Practice - Histograms
Try the following changes:
1. Change the year range to 1929–1985. HINT: Take a slice with .loc[ ]
2. Make a plot with two subplots (side-by-side), where the first shows the data from 2006-2012 and the second shows the data 2013–2024
3. Change the figsize, bin, alpha, and color arguments to whatever you like!
4. Add a vertical line at zero. *Hint: Knowing how to do a horizontal line, how would you make it vertical?*
5. Challenging: For each of the two plots, compute the mean annual percent growth rate for that time period and put the vertical line there instead of at zero


```python
# Reference Code
fig, ax1 = plt.subplots(figsize=(16,9))
ax1.hist(USD_ER['USD_Broad_growth'], bins=20, alpha=1, color='navy')
ax1.set(ylabel='Frequency',
        xlabel='Monthly growth rate (%)',
        title='Frequency of Broad USD growth rates (2006-2025)')
ax1.spines[['right','top']].set_visible(False)
plt.show()
```


    
![png](output_20_0.png)
    



```python
# Results:
avg_USD_growth_early = USD_ER['USD_Broad_growth'].loc[USD_ER.index <= datetime(2012,12,1)].mean()
avg_USD_growth_late = USD_ER['USD_Broad_growth'].loc[USD_ER.index > datetime(2012,12,1)].mean()

fig, ax1 = plt.subplots(1, 2, figsize=(16,9))

ax1[0].hist(USD_ER['USD_Broad_growth'].loc[USD_ER.index <= datetime(2012,12,1)], bins=20, alpha=0.8, color='green')
ax1[0].set(ylabel='Frequency',
        xlabel='Monthly growth rate (%)',
        title='Frequency of Broad USD growth rates (2006-2012)')
ax1[0].spines[['right','top']].set_visible(False)
ax1[0].axvline(x=avg_USD_growth_early, color='red')

ax1[1].hist(USD_ER['USD_Broad_growth'].loc[USD_ER.index > datetime(2012,12,1)], bins=20, alpha=0.8, color='green')
ax1[1].set(ylabel='Frequency',
        xlabel='Monthly growth rate (%)',
        title='Frequency of Broad USD growth rates (2012-2025)')
ax1[1].spines[['right','top']].set_visible(False)
ax1[1].axvline(x=avg_USD_growth_late, color='red')

plt.show()
```


    
![png](output_21_0.png)
    


## Bar Plots


```python
# Tally the number of times each percent growth rate occurs
Broad_USD_counts = pd.crosstab(USD_ER['USD_Broad_growth'], 'Frequency') 

# Generate a bar chart
fig, ax = plt.subplots() 
ax.bar(x=Broad_USD_counts.index,height=Broad_USD_counts['Frequency'])
plt.show()
```


    
![png](output_23_0.png)
    



```python
# Go back to our manufacturing data
ENIA_emp = pd.read_stata('https://m-mcmain.github.io/files/Econ390SP26/FUSION_annual_1995_EMP.dta')
ENIA_emp
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
      <th>NUI</th>
      <th>REGION</th>
      <th>CIIU3</th>
      <th>TOTHOM</th>
      <th>TOTMUJ</th>
      <th>REMEMP</th>
      <th>REGEMP</th>
      <th>REMCOM</th>
      <th>REGCOM</th>
      <th>REMOBR</th>
      <th>REGOBR</th>
      <th>TOHSC</th>
      <th>TOMSC</th>
      <th>EXPORTADOS</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>10082.0</td>
      <td>2</td>
      <td>3610</td>
      <td>14</td>
      <td>1</td>
      <td>7466</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>20174</td>
      <td>600</td>
      <td>0</td>
      <td>0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>10101.0</td>
      <td>2</td>
      <td>2720</td>
      <td>427</td>
      <td>25</td>
      <td>2046170</td>
      <td>184590</td>
      <td>0</td>
      <td>0</td>
      <td>810717</td>
      <td>216003</td>
      <td>0</td>
      <td>0</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>10103.0</td>
      <td>2</td>
      <td>1531</td>
      <td>46</td>
      <td>6</td>
      <td>135873</td>
      <td>3426</td>
      <td>69814</td>
      <td>2912</td>
      <td>37037</td>
      <td>3848</td>
      <td>0</td>
      <td>0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>10178.0</td>
      <td>4</td>
      <td>1512</td>
      <td>39</td>
      <td>35</td>
      <td>22958</td>
      <td>1886</td>
      <td>0</td>
      <td>0</td>
      <td>40257</td>
      <td>4394</td>
      <td>0</td>
      <td>0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>10220.0</td>
      <td>5</td>
      <td>3312</td>
      <td>481</td>
      <td>15</td>
      <td>554636</td>
      <td>187853</td>
      <td>0</td>
      <td>0</td>
      <td>858571</td>
      <td>290794</td>
      <td>0</td>
      <td>0</td>
      <td>1.0</td>
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
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>95</th>
      <td>23429.0</td>
      <td>13</td>
      <td>2520</td>
      <td>39</td>
      <td>0</td>
      <td>7990</td>
      <td>790</td>
      <td>0</td>
      <td>0</td>
      <td>25334</td>
      <td>3874</td>
      <td>2</td>
      <td>0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>96</th>
      <td>23437.0</td>
      <td>13</td>
      <td>2520</td>
      <td>81</td>
      <td>6</td>
      <td>88656</td>
      <td>1432</td>
      <td>3284</td>
      <td>0</td>
      <td>117469</td>
      <td>9895</td>
      <td>9</td>
      <td>0</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>97</th>
      <td>23449.0</td>
      <td>6</td>
      <td>2924</td>
      <td>145</td>
      <td>0</td>
      <td>914130</td>
      <td>54126</td>
      <td>0</td>
      <td>0</td>
      <td>267928</td>
      <td>31246</td>
      <td>0</td>
      <td>0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>98</th>
      <td>40088.0</td>
      <td>8</td>
      <td>3693</td>
      <td>3</td>
      <td>3</td>
      <td>13495</td>
      <td>271</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>99</th>
      <td>40172.0</td>
      <td>1</td>
      <td>2022</td>
      <td>31</td>
      <td>5</td>
      <td>6205</td>
      <td>1284</td>
      <td>2634</td>
      <td>545</td>
      <td>64776</td>
      <td>484</td>
      <td>0</td>
      <td>0</td>
      <td>0.0</td>
    </tr>
  </tbody>
</table>
<p>100 rows × 14 columns</p>
</div>




```python
# Convert Data
ENIA_emp['EXPORTADOS'] = ENIA_emp['EXPORTADOS'].astype(str)
ENIA_emp.loc[ENIA_emp['EXPORTADOS']=="0.0", 'EXPORTADOS'] = "No Exports"
ENIA_emp.loc[ENIA_emp['EXPORTADOS']=="1.0", 'EXPORTADOS'] = "Exported"
ENIA_emp
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
      <th>NUI</th>
      <th>REGION</th>
      <th>CIIU3</th>
      <th>TOTHOM</th>
      <th>TOTMUJ</th>
      <th>REMEMP</th>
      <th>REGEMP</th>
      <th>REMCOM</th>
      <th>REGCOM</th>
      <th>REMOBR</th>
      <th>REGOBR</th>
      <th>TOHSC</th>
      <th>TOMSC</th>
      <th>EXPORTADOS</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>10082.0</td>
      <td>2</td>
      <td>3610</td>
      <td>14</td>
      <td>1</td>
      <td>7466</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>20174</td>
      <td>600</td>
      <td>0</td>
      <td>0</td>
      <td>No Exports</td>
    </tr>
    <tr>
      <th>1</th>
      <td>10101.0</td>
      <td>2</td>
      <td>2720</td>
      <td>427</td>
      <td>25</td>
      <td>2046170</td>
      <td>184590</td>
      <td>0</td>
      <td>0</td>
      <td>810717</td>
      <td>216003</td>
      <td>0</td>
      <td>0</td>
      <td>Exported</td>
    </tr>
    <tr>
      <th>2</th>
      <td>10103.0</td>
      <td>2</td>
      <td>1531</td>
      <td>46</td>
      <td>6</td>
      <td>135873</td>
      <td>3426</td>
      <td>69814</td>
      <td>2912</td>
      <td>37037</td>
      <td>3848</td>
      <td>0</td>
      <td>0</td>
      <td>No Exports</td>
    </tr>
    <tr>
      <th>3</th>
      <td>10178.0</td>
      <td>4</td>
      <td>1512</td>
      <td>39</td>
      <td>35</td>
      <td>22958</td>
      <td>1886</td>
      <td>0</td>
      <td>0</td>
      <td>40257</td>
      <td>4394</td>
      <td>0</td>
      <td>0</td>
      <td>No Exports</td>
    </tr>
    <tr>
      <th>4</th>
      <td>10220.0</td>
      <td>5</td>
      <td>3312</td>
      <td>481</td>
      <td>15</td>
      <td>554636</td>
      <td>187853</td>
      <td>0</td>
      <td>0</td>
      <td>858571</td>
      <td>290794</td>
      <td>0</td>
      <td>0</td>
      <td>Exported</td>
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
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>95</th>
      <td>23429.0</td>
      <td>13</td>
      <td>2520</td>
      <td>39</td>
      <td>0</td>
      <td>7990</td>
      <td>790</td>
      <td>0</td>
      <td>0</td>
      <td>25334</td>
      <td>3874</td>
      <td>2</td>
      <td>0</td>
      <td>No Exports</td>
    </tr>
    <tr>
      <th>96</th>
      <td>23437.0</td>
      <td>13</td>
      <td>2520</td>
      <td>81</td>
      <td>6</td>
      <td>88656</td>
      <td>1432</td>
      <td>3284</td>
      <td>0</td>
      <td>117469</td>
      <td>9895</td>
      <td>9</td>
      <td>0</td>
      <td>Exported</td>
    </tr>
    <tr>
      <th>97</th>
      <td>23449.0</td>
      <td>6</td>
      <td>2924</td>
      <td>145</td>
      <td>0</td>
      <td>914130</td>
      <td>54126</td>
      <td>0</td>
      <td>0</td>
      <td>267928</td>
      <td>31246</td>
      <td>0</td>
      <td>0</td>
      <td>No Exports</td>
    </tr>
    <tr>
      <th>98</th>
      <td>40088.0</td>
      <td>8</td>
      <td>3693</td>
      <td>3</td>
      <td>3</td>
      <td>13495</td>
      <td>271</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>No Exports</td>
    </tr>
    <tr>
      <th>99</th>
      <td>40172.0</td>
      <td>1</td>
      <td>2022</td>
      <td>31</td>
      <td>5</td>
      <td>6205</td>
      <td>1284</td>
      <td>2634</td>
      <td>545</td>
      <td>64776</td>
      <td>484</td>
      <td>0</td>
      <td>0</td>
      <td>No Exports</td>
    </tr>
  </tbody>
</table>
<p>100 rows × 14 columns</p>
</div>




```python
# Gen total employment
ENIA_emp['TOTEMP'] = ENIA_emp['TOTHOM']+ENIA_emp['TOTMUJ']+ENIA_emp['TOHSC']+ENIA_emp['TOMSC']
ENIA_emp
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
      <th>NUI</th>
      <th>REGION</th>
      <th>CIIU3</th>
      <th>TOTHOM</th>
      <th>TOTMUJ</th>
      <th>REMEMP</th>
      <th>REGEMP</th>
      <th>REMCOM</th>
      <th>REGCOM</th>
      <th>REMOBR</th>
      <th>REGOBR</th>
      <th>TOHSC</th>
      <th>TOMSC</th>
      <th>EXPORTADOS</th>
      <th>TOTEMP</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>10082.0</td>
      <td>2</td>
      <td>3610</td>
      <td>14</td>
      <td>1</td>
      <td>7466</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>20174</td>
      <td>600</td>
      <td>0</td>
      <td>0</td>
      <td>No Exports</td>
      <td>15</td>
    </tr>
    <tr>
      <th>1</th>
      <td>10101.0</td>
      <td>2</td>
      <td>2720</td>
      <td>427</td>
      <td>25</td>
      <td>2046170</td>
      <td>184590</td>
      <td>0</td>
      <td>0</td>
      <td>810717</td>
      <td>216003</td>
      <td>0</td>
      <td>0</td>
      <td>Exported</td>
      <td>452</td>
    </tr>
    <tr>
      <th>2</th>
      <td>10103.0</td>
      <td>2</td>
      <td>1531</td>
      <td>46</td>
      <td>6</td>
      <td>135873</td>
      <td>3426</td>
      <td>69814</td>
      <td>2912</td>
      <td>37037</td>
      <td>3848</td>
      <td>0</td>
      <td>0</td>
      <td>No Exports</td>
      <td>52</td>
    </tr>
    <tr>
      <th>3</th>
      <td>10178.0</td>
      <td>4</td>
      <td>1512</td>
      <td>39</td>
      <td>35</td>
      <td>22958</td>
      <td>1886</td>
      <td>0</td>
      <td>0</td>
      <td>40257</td>
      <td>4394</td>
      <td>0</td>
      <td>0</td>
      <td>No Exports</td>
      <td>74</td>
    </tr>
    <tr>
      <th>4</th>
      <td>10220.0</td>
      <td>5</td>
      <td>3312</td>
      <td>481</td>
      <td>15</td>
      <td>554636</td>
      <td>187853</td>
      <td>0</td>
      <td>0</td>
      <td>858571</td>
      <td>290794</td>
      <td>0</td>
      <td>0</td>
      <td>Exported</td>
      <td>496</td>
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
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>95</th>
      <td>23429.0</td>
      <td>13</td>
      <td>2520</td>
      <td>39</td>
      <td>0</td>
      <td>7990</td>
      <td>790</td>
      <td>0</td>
      <td>0</td>
      <td>25334</td>
      <td>3874</td>
      <td>2</td>
      <td>0</td>
      <td>No Exports</td>
      <td>41</td>
    </tr>
    <tr>
      <th>96</th>
      <td>23437.0</td>
      <td>13</td>
      <td>2520</td>
      <td>81</td>
      <td>6</td>
      <td>88656</td>
      <td>1432</td>
      <td>3284</td>
      <td>0</td>
      <td>117469</td>
      <td>9895</td>
      <td>9</td>
      <td>0</td>
      <td>Exported</td>
      <td>96</td>
    </tr>
    <tr>
      <th>97</th>
      <td>23449.0</td>
      <td>6</td>
      <td>2924</td>
      <td>145</td>
      <td>0</td>
      <td>914130</td>
      <td>54126</td>
      <td>0</td>
      <td>0</td>
      <td>267928</td>
      <td>31246</td>
      <td>0</td>
      <td>0</td>
      <td>No Exports</td>
      <td>145</td>
    </tr>
    <tr>
      <th>98</th>
      <td>40088.0</td>
      <td>8</td>
      <td>3693</td>
      <td>3</td>
      <td>3</td>
      <td>13495</td>
      <td>271</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>No Exports</td>
      <td>6</td>
    </tr>
    <tr>
      <th>99</th>
      <td>40172.0</td>
      <td>1</td>
      <td>2022</td>
      <td>31</td>
      <td>5</td>
      <td>6205</td>
      <td>1284</td>
      <td>2634</td>
      <td>545</td>
      <td>64776</td>
      <td>484</td>
      <td>0</td>
      <td>0</td>
      <td>No Exports</td>
      <td>36</td>
    </tr>
  </tbody>
</table>
<p>100 rows × 15 columns</p>
</div>




```python
# Calculate number of times each outcome occurs
exported_counts = pd.crosstab(ENIA_emp['EXPORTADOS'], 'Frequency') 
```


```python
exported_counts
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
      <th>col_0</th>
      <th>Frequency</th>
    </tr>
    <tr>
      <th>EXPORTADOS</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Exported</th>
      <td>23</td>
    </tr>
    <tr>
      <th>No Exports</th>
      <td>77</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Generate bar chart
fig, ax = plt.subplots() 
ax.bar(exported_counts.index, exported_counts['Frequency'])
plt.show()
```


    
![png](output_29_0.png)
    



```python
# We can use similar options as before
fig, ax = plt.subplots()
ax.bar(exported_counts.index, 
       exported_counts['Frequency'], 
       color='green', 
       width=0.5)

ax.set(ylabel='Frequency',
       xlabel='Export Decision',
       title='Number of Chilean Manufacturing Firms by Export Status')

ax.spines[['right','top']].set_visible(False)

plt.show()
```


    
![png](output_30_0.png)
    



```python
ax = exported_counts.plot.bar(color='green',
                             width=0.5,
                             legend=False)

ax.set(ylabel='Frequency',
       xlabel='Export Decision',
       title='Number of Chilean Manufacturing Firms by Export Status')

ax.spines[['right','top']].set_visible(False)
```


    
![png](output_31_0.png)
    


## Practice - Bar Plots
Try the following changes:
1. Try displaying percentages instead of counts. *Hint: You only need to change the crosstab statement. Look back to Lecture 12 if you've forgotten.*
2. Can we make this a horizontal bar chart? It’s pretty easy actually. Instead of the bar method, try the barh method. Do we get an error? Why?


```python
# Results:
exported_counts = pd.crosstab(ENIA_emp['EXPORTADOS'], 'percent', normalize='columns') 

# Generate bar chart
fig, ax = plt.subplots()
ax.barh(exported_counts.index, exported_counts['percent'], height=0.5)
plt.show()
```


    
![png](output_33_0.png)
    

