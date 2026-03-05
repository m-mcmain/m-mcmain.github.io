---
layout: single
sitemap: false
permalink: /pages/Econ_390_SP26_L13/
---

[Download Jupyter Notebook Empty](https://m-mcmain.github.io/files/Econ390SP26/Lectures/Lecture13_MatplotlibLinePlots_empty.ipynb)

[Download Jupyter Notebook Completed](https://m-mcmain.github.io/files/Econ390SP26/Lectures/Lecture13_MatplotlibLinePlots_full.ipynb)

# Econ 390 - Lecture 13: Matplotlib Line Plots
Today we will begin learning how to create plots in Python using Matplotlib. You can find the relevant textbook chapters for [McKinney](https://wesmckinney.com/book/plotting-and-visualization) and [Turrell](https://aeturrell.github.io/coding-for-economists/vis-matplotlib.html#understanding-matplotlib).

## Mid-Semester Course Evaluation
Tomorrow is the final day to complete the mid-semester course evaluation! Completing the survey will give me active feedback to improve your experience in the class and will help me out a ton moving forward. Look for an email from `learningassessment@provost.wisc.edu` or head to [this](https://heliocampusac.wisc.edu/index.cfm/page/AefisDashboard.home?Login=1) link and look for the Econ 390 - 001 course survey. Thank you! 

## Essay Competition
There is an [Undergraduate Essay Competition](https://csld.wisc.edu/2026/02/27/announcing-the-2026-undergraduate-essay-competition/) being run by the Center for the Study of Liberal Democracy here at UW Madison. ~1000 word essays due on March 30th.

## Data


```python
# Load Exchange Rate Data into a DataFrame
url = "https://m-mcmain.github.io/files/Econ390SP26/"
USD_ER = pd.read_csv(url + "USD_ERs.csv", index_col = 0)
USD_ER = USD_ER.rename(columns={"DEXUSEU_NBD20060101":"USD_EU", "DEXCHUS_NBD20060101":"CHY_USD", "DTWEXBGS_NBD20060101":"Broad USD"})
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
      <th>Broad USD</th>
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
      <th>1/1/2006</th>
      <td>100.00000</td>
      <td>100.00000</td>
      <td>100.00000</td>
    </tr>
    <tr>
      <th>2/1/2006</th>
      <td>100.21117</td>
      <td>99.82489</td>
      <td>98.46800</td>
    </tr>
    <tr>
      <th>3/1/2006</th>
      <td>100.42808</td>
      <td>99.62384</td>
      <td>99.19950</td>
    </tr>
    <tr>
      <th>4/1/2006</th>
      <td>99.74348</td>
      <td>99.36736</td>
      <td>101.21851</td>
    </tr>
    <tr>
      <th>5/1/2006</th>
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
      <th>7/1/2025</th>
      <td>120.52656</td>
      <td>88.94931</td>
      <td>96.25020</td>
    </tr>
    <tr>
      <th>8/1/2025</th>
      <td>120.98444</td>
      <td>88.93206</td>
      <td>96.05770</td>
    </tr>
    <tr>
      <th>9/1/2025</th>
      <td>120.45339</td>
      <td>88.32157</td>
      <td>96.81015</td>
    </tr>
    <tr>
      <th>10/1/2025</th>
      <td>121.17118</td>
      <td>88.27831</td>
      <td>96.00204</td>
    </tr>
    <tr>
      <th>11/1/2025</th>
      <td>121.80375</td>
      <td>88.11608</td>
      <td>95.32070</td>
    </tr>
  </tbody>
</table>
<p>239 rows × 3 columns</p>
</div>



## Intro to Matplotlib


```python
# New imports
import pandas as pd, matplotlib.pyplot as plt
```


```python
# Defining your first plot
fig, ax = plt.subplots()
```


    
![png](output_7_0.png)
    



```python
# What types are these new objects?
print(type(fig))
print(type(ax))
```

    <class 'matplotlib.figure.Figure'>
    <class 'matplotlib.axes._axes.Axes'>
    


```python
# Using plot to make lines
ax.plot([1,10],[1,10])
ax.plot([1,10],[10,1])
fig
```




    
![png](output_9_0.png)
    




```python
# Plotting from our DataFrame
fig, ax = plt.subplots()

ax.plot(USD_ER.index, USD_ER["Broad USD"]);
```


    
![png](output_10_0.png)
    



```python
# ANOTHER new package
from datetime import datetime

# New option to read_csv
USD_ER = pd.read_csv(url + "USD_ERs.csv", index_col=0, parse_dates=True)
USD_ER = USD_ER.rename(columns={"DEXUSEU_NBD20060101":"USD_EU", "DEXCHUS_NBD20060101":"CHY_USD", "DTWEXBGS_NBD20060101":"Broad USD"})
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
      <th>Broad USD</th>
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
# Try it now
# Plotting from our DataFrame
fig, ax = plt.subplots()

ax.plot(USD_ER.index, USD_ER["Broad USD"]);
```


    
![png](output_12_0.png)
    



```python
# Set limits on the axes
ax.set_xlim([datetime(2006,1,1),datetime(2012,12,1)])
ax.set_ylim([85,105])
fig
```




    
![png](output_13_0.png)
    




```python
# Just do it all in one line
fig, ax = plt.subplots()

ax.plot(USD_ER.index, USD_ER["Broad USD"]);

ax.set(xlim = (datetime(2006,1,1),datetime(2012,12,1)), ylim = (85,105), title = "Broad USD Over Time", xlabel = "Time", ylabel = "US Broad Exchange Rate");
```


    
![png](output_14_0.png)
    



```python
# When that one line gets really long you can make it more readable
fig, ax = plt.subplots()

ax.plot(USD_ER.index, USD_ER["Broad USD"]);

ax.set(xlim = (datetime(2006,1,1), datetime(2012,12,1)), 
       ylim = (85,105), 
       title = "Broad USD Over Time", 
       xlabel = "Time", 
       ylabel = "US Broad Exchange Rate");
```


    
![png](output_15_0.png)
    



```python
# Options
ax.spines[['top','right']].set_visible(False)
fig
```




    
![png](output_16_0.png)
    



## Practice - Line Plots
1. Is there a better way to deal with the axes? What is a way to do it to not manually change xlim and ylim?
2. Copy and paste the previous plot below and add the line for the Chinese Yuan RMB to USD. If you did the previous part right, you still shouldn't need to manually update xlim and ylim!
3. Modify the code to change the color of the Chinese Yuan RMB to USD line.
4. Modify your code and add the argument alpha=0.3 as a line style option for the Chinese Yuan RMB to USD line. What does this change?
5. Modify the code to make one of the lines dashed. Or try out `linestyle = '--'` `linestyle = '-.'` `linestyle = ':'`
6. With all of these changes, how do you feel about the plot? Any concerns?


```python
# Results:
fig, ax = plt.subplots()

# 1.
USD_ER = USD_ER.loc[USD_ER.index < datetime(2013,1,1),:]
# 2-6.
ax.plot(USD_ER.index, USD_ER["Broad USD"])
ax.plot(USD_ER.index, USD_ER["CHY_USD"], color = "Green", linestyle = "-")

ax.set(title = "Broad USD Over Time", 
       xlabel = "Time", 
       ylabel = "US Broad Exchange Rate");

ax.spines[['top','right']].set_visible(False)
```


    
![png](output_18_0.png)
    


## Line Plots with Multiple Lines


```python
# Multiple lines?
fig, ax = plt.subplots()

USD_ER = USD_ER.loc[USD_ER.index < datetime(2013,1,1),:]

ax.plot(USD_ER.index, USD_ER["Broad USD"], label = "Broad USD")
ax.plot(USD_ER.index, USD_ER["CHY_USD"], color = "Green", linestyle = "-", label = "Yuan to USD")
ax.plot(USD_ER.index, USD_ER["USD_EU"], color = "Orange", linestyle = "-", label = "USD to Euro")

ax.set(title = "Broad USD Over Time", 
       xlabel = "Time", 
       ylabel = "US Broad Exchange Rate");

ax.spines[['top','right']].set_visible(False)
ax.legend();
```




    <matplotlib.legend.Legend at 0x20280409940>




    
![png](output_20_1.png)
    



```python
# Let's fix one of these
fig, ax = plt.subplots()

USD_ER["EU_USD"] = 100 + (100-USD_ER['USD_EU'])

USD_ER = USD_ER.loc[USD_ER.index < datetime(2013,1,1),:]

ax.plot(USD_ER.index, USD_ER["Broad USD"], label = "Broad USD")
ax.plot(USD_ER.index, USD_ER["CHY_USD"], color = "Green", linestyle = "-", label = "Yuan to USD")
ax.plot(USD_ER.index, USD_ER["EU_USD"], color = "Orange", linestyle = "-", label = "Euro to USD")

ax.set(title = "Broad USD Over Time", 
       xlabel = "Time", 
       ylabel = "US Broad Exchange Rate");

ax.spines[['top','right']].set_visible(False)
ax.legend(frameon=False);
```


    
![png](output_21_0.png)
    



```python
# Manually include text
fig, ax = plt.subplots()

USD_ER["EU_USD"] = 100 + (100-USD_ER['USD_EU'])

USD_ER = USD_ER.loc[USD_ER.index < datetime(2013,1,1),:]

ax.plot(USD_ER.index, USD_ER["Broad USD"], label = "Broad USD")
ax.plot(USD_ER.index, USD_ER["CHY_USD"], color = "Green", linestyle = "-", label = "Yuan to USD")
ax.plot(USD_ER.index, USD_ER["EU_USD"], color = "Orange", linestyle = "-", label = "Euro to USD")

ax.set(title = "Broad USD Over Time", 
       xlabel = "Time", 
       ylabel = "US Broad Exchange Rate");

ax.spines[['top','right']].set_visible(False)
ax.text(datetime(2010,5,1), 100, "USD to Euro", color = "Orange")
```




    Text(2010-05-01 00:00:00, 100, 'USD to Euro')




    
![png](output_22_1.png)
    



```python
# Plot alone works, but it makes assumptions about what you want!
fig, ax = plt.subplots()

ax = USD_ER.plot()

ax.set(title = "Broad USD Over Time", 
       xlabel = "Time", 
       ylabel = "US Broad Exchange Rate");

ax.spines[['top','right']].set_visible(False)
ax.legend(frameon=False)
plt.show()
```


    
![png](output_23_0.png)
    



    
![png](output_23_1.png)
    



```python
# Let's drop the USD to EU ER and go again
USD_ER = USD_ER.drop("USD_EU", axis=1)

ax = USD_ER.plot()

ax.set(title = "Broad USD Over Time", 
       xlabel = "Time", 
       ylabel = "US Broad Exchange Rate");

ax.spines[['top','right']].set_visible(False)
ax.legend(frameon=False)
plt.show()
```


    
![png](output_24_0.png)
    



```python
# If you want to have similar styles for many different lines, you can loop through them
fig, ax = plt.subplots()

for ER in USD_ER.columns:
    ax.plot(USD_ER.index,
            USD_ER[ER],
            label = ER,
            marker = ".",
            markersize = 5)

ax.set(title = "Broad USD Over Time", 
       xlabel = "Time", 
       ylabel = "US Broad Exchange Rate");

ax.spines[['top','right']].set_visible(False)
ax.legend(frameon=False)
plt.show()
```


    
![png](output_25_0.png)
    

