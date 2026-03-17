---
layout: single
sitemap: false
permalink: /pages/Econ_390_SP26_L15/
title: Econ 390 Lecture 15
---

[Download Jupyter Notebook Empty](https://m-mcmain.github.io/files/Econ390SP26/Lectures/Lecture15_StylesheetsandSeaborn_empty.ipynb)

[Download Jupyter Notebook Completed](https://m-mcmain.github.io/files/Econ390SP26/Lectures/Lecture15_StylesheetsandSeaborn_full.ipynb)

# Econ 390 - Lecture 15: Matplotlib Stylesheets and Seaborn
Today we will be going over stylesheets and Seaborn. You'll see Seaborn around both [McKinney](https://wesmckinney.com/book/plotting-and-visualization#vis_pandas) and [Turrell](https://aeturrell.github.io/coding-for-economists/vis-common-plots-one.html).

## Matplotlib Stylesheets


```python
# Imports and data
import pandas as pd
import matplotlib.pyplot as plt
from datetime import datetime

url = "https://m-mcmain.github.io/files/Econ390SP26/"

cpi = pd.read_csv(url + 'CPI_10year.csv', index_col=0, parse_dates = True)
cpi
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
      <th>CPIAUCSL_PC1</th>
      <th>CORESTICKM159SFRBATL</th>
    </tr>
    <tr>
      <th>observation_date</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2015-09-01</th>
      <td>0.00884</td>
      <td>2.268536</td>
    </tr>
    <tr>
      <th>2015-10-01</th>
      <td>0.12762</td>
      <td>2.335492</td>
    </tr>
    <tr>
      <th>2015-11-01</th>
      <td>0.43632</td>
      <td>2.394625</td>
    </tr>
    <tr>
      <th>2015-12-01</th>
      <td>0.63872</td>
      <td>2.437497</td>
    </tr>
    <tr>
      <th>2016-01-01</th>
      <td>1.23750</td>
      <td>2.460879</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>2025-05-01</th>
      <td>2.37593</td>
      <td>3.159131</td>
    </tr>
    <tr>
      <th>2025-06-01</th>
      <td>2.67268</td>
      <td>3.288774</td>
    </tr>
    <tr>
      <th>2025-07-01</th>
      <td>2.73180</td>
      <td>3.419811</td>
    </tr>
    <tr>
      <th>2025-08-01</th>
      <td>2.93922</td>
      <td>3.400000</td>
    </tr>
    <tr>
      <th>2025-09-01</th>
      <td>3.02270</td>
      <td>3.326080</td>
    </tr>
  </tbody>
</table>
<p>121 rows × 2 columns</p>
</div>




```python
# Rename columns
cpi = cpi.rename(columns={"CPIAUCSL_PC1":"CPI Growth","CORESTICKM159SFRBATL":"Core CPI Growth"})
cpi
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
      <th>CPI Growth</th>
      <th>Core CPI Growth</th>
    </tr>
    <tr>
      <th>observation_date</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2015-09-01</th>
      <td>0.00884</td>
      <td>2.268536</td>
    </tr>
    <tr>
      <th>2015-10-01</th>
      <td>0.12762</td>
      <td>2.335492</td>
    </tr>
    <tr>
      <th>2015-11-01</th>
      <td>0.43632</td>
      <td>2.394625</td>
    </tr>
    <tr>
      <th>2015-12-01</th>
      <td>0.63872</td>
      <td>2.437497</td>
    </tr>
    <tr>
      <th>2016-01-01</th>
      <td>1.23750</td>
      <td>2.460879</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>2025-05-01</th>
      <td>2.37593</td>
      <td>3.159131</td>
    </tr>
    <tr>
      <th>2025-06-01</th>
      <td>2.67268</td>
      <td>3.288774</td>
    </tr>
    <tr>
      <th>2025-07-01</th>
      <td>2.73180</td>
      <td>3.419811</td>
    </tr>
    <tr>
      <th>2025-08-01</th>
      <td>2.93922</td>
      <td>3.400000</td>
    </tr>
    <tr>
      <th>2025-09-01</th>
      <td>3.02270</td>
      <td>3.326080</td>
    </tr>
  </tbody>
</table>
<p>121 rows × 2 columns</p>
</div>




```python
# Reminder of Basic Plotting
fig, ax = plt.subplots()

ax.plot(cpi.index, cpi['CPI Growth'], label="CPI Inflation")
ax.plot(cpi.index, cpi["Core CPI Growth"], label="Core CPI Inflation")

ax.set_ylabel("% Change from Year Ago")
ax.legend()
plt.show()
```


    
![png](output_4_0.png)
    



```python
# Making use of the style method
plt.style.use("dark_background")

fig, ax = plt.subplots()

ax.plot(cpi.index, cpi['CPI Growth'], label="CPI Inflation")
ax.plot(cpi.index, cpi["Core CPI Growth"], label="Core CPI Inflation")

ax.set_ylabel("% Change from Year Ago")
ax.legend()
plt.show()
```


    
![png](output_5_0.png)
    



```python
# Going back to defaults
plt.rcdefaults()

fig, ax = plt.subplots()

ax.plot(cpi.index, cpi['CPI Growth'], label="CPI Inflation")
ax.plot(cpi.index, cpi["Core CPI Growth"], label="Core CPI Inflation")

ax.set_ylabel("% Change from Year Ago")
ax.legend()
plt.show()
```


    
![png](output_6_0.png)
    



```python
# Use "with"
with plt.style.context("dark_background"):
    fig, ax = plt.subplots()

    ax.plot(cpi.index, cpi['CPI Growth'], label="CPI Inflation")
    ax.plot(cpi.index, cpi["Core CPI Growth"], label="Core CPI Inflation")
    
    ax.set_ylabel("% Change from Year Ago")
    ax.legend()
    
plt.show()    
```


    
![png](output_7_0.png)
    



```python
# Don't need to change any settings to go back
fig, ax = plt.subplots()

ax.plot(cpi.index, cpi['CPI Growth'], label="CPI Inflation")
ax.plot(cpi.index, cpi["Core CPI Growth"], label="Core CPI Inflation")

ax.set_ylabel("% Change from Year Ago")
ax.legend()
plt.show()
```


    
![png](output_8_0.png)
    



```python
# What styles are there?
plt.style.available
```




    ['Solarize_Light2',
     '_classic_test_patch',
     '_mpl-gallery',
     '_mpl-gallery-nogrid',
     'bmh',
     'classic',
     'dark_background',
     'fast',
     'fivethirtyeight',
     'ggplot',
     'grayscale',
     'petroff10',
     'seaborn-v0_8',
     'seaborn-v0_8-bright',
     'seaborn-v0_8-colorblind',
     'seaborn-v0_8-dark',
     'seaborn-v0_8-dark-palette',
     'seaborn-v0_8-darkgrid',
     'seaborn-v0_8-deep',
     'seaborn-v0_8-muted',
     'seaborn-v0_8-notebook',
     'seaborn-v0_8-paper',
     'seaborn-v0_8-pastel',
     'seaborn-v0_8-poster',
     'seaborn-v0_8-talk',
     'seaborn-v0_8-ticks',
     'seaborn-v0_8-white',
     'seaborn-v0_8-whitegrid',
     'tableau-colorblind10']




```python
# Multiple styles
with plt.style.context(["dark_background", "ggplot"]):
    fig, ax = plt.subplots()

    ax.plot(cpi.index, cpi['CPI Growth'], label="CPI Inflation")
    ax.plot(cpi.index, cpi["Core CPI Growth"], label="Core CPI Inflation")
    
    ax.set_ylabel("% Change from Year Ago")
    ax.legend()
plt.show()
```


    
![png](output_10_0.png)
    



```python
# Order?
with plt.style.context(["ggplot", "dark_background"]):
    fig, ax = plt.subplots()

    ax.plot(cpi.index, cpi['CPI Growth'], label="CPI Inflation")
    ax.plot(cpi.index, cpi["Core CPI Growth"], label="Core CPI Inflation")
    
    ax.set_ylabel("% Change from Year Ago")
    ax.legend()
plt.show()
```


    
![png](output_11_0.png)
    



```python
# Let's make our plot how we want to
fig, ax = plt.subplots(figsize = (8,6))

ax.plot(cpi.index, cpi['CPI Growth'], label="CPI Inflation", color="black")
ax.plot(cpi.index, cpi["Core CPI Growth"], label="Core CPI Inflation", color="blue")

ax.set_ylabel("% Change from Year Ago")
ax.legend(frameon=False)
ax.spines[["top", "right"]].set_visible(False)
plt.show()
```


    
![png](output_12_0.png)
    



```python
# create a file containing 'hello world!'
my_file = open("test_file.txt", "w")
my_file.write("hello world!")
my_file.close() # always remember to close!
# print the contents of the file
my_file = open("test_file.txt")
print(my_file.read())
my_file.close() # Close!
```

    hello world!
    


```python
# Create our own mplstyle sheet!
# Easiest to just manually do so.
```


```python
# Use our new style
with plt.style.context("notebook.mplstyle"):
    fig, ax = plt.subplots()

    ax.plot(cpi.index, cpi['CPI Growth'], label="CPI Inflation")
    ax.plot(cpi.index, cpi["Core CPI Growth"], label="Core CPI Inflation")
    
    ax.set_ylabel("% Change from Year Ago")
    ax.legend()

plt.show()
```


    
![png](output_15_0.png)
    


## Practice - Stylesheets
I named the stylesheet provided "notebook" because that's the style I like in my notebooks. Imagine you want to change the style to fit something requested from your boss or a journal.
1. Start by making a copy of notebook.mplstyle and opening it in any text editor.
2. Update the aspect ratio to be 5:4, line width to 1, and tick label sizes to 12
3. You'll still have an issue with accessibility that we talked about before. What is it? *Hint: You're looking for a line already in there. To add another cycler for linestyle do + copying the existing one with updates that make sense.*
### Having Trouble? Ask people around you or raise your hand!


```python
# Use our new style
with plt.style.context("paper.mplstyle"):
    fig, ax = plt.subplots()

    ax.plot(cpi.index, cpi['CPI Growth'], label="CPI Inflation")
    ax.plot(cpi.index, cpi["Core CPI Growth"], label="Core CPI Inflation")
    
    ax.set_ylabel("% Change from Year Ago")
    ax.legend()

# Create a png and save to cwd
plt.savefig("CPI.png")
# Create a pdf and save to cwd 
plt.savefig("CPI.pdf")
```


    
![png](output_17_0.png)
    


## Saving Figures and Seaborn


```python
# New package! Very situational for us.
import seaborn as sns
```


```python
# Getting rid of spines as we know it
ax = cpi["CPI Growth"].plot()

ax.spines[["right","top"]].set_visible(False)
```


    
![png](output_20_0.png)
    



```python
# Despine function
cpi["CPI Growth"].plot()
sns.despine()
```


    
![png](output_21_0.png)
    



```python
# CO Import Data
CO_imports = pd.read_csv(url + "CO_import_val_ym.csv")
CO_imports.head()
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
      <th>year</th>
      <th>month</th>
      <th>import_value</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2009</td>
      <td>1</td>
      <td>3647430912</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2009</td>
      <td>2</td>
      <td>3182016000</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2009</td>
      <td>3</td>
      <td>3199911168</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2009</td>
      <td>4</td>
      <td>3440155136</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2009</td>
      <td>5</td>
      <td>6793028608</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Divide for reading ease
CO_imports["import_value"] = CO_imports["import_value"].div(10e8)
CO_imports.head()
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
      <th>year</th>
      <th>month</th>
      <th>import_value</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2009</td>
      <td>1</td>
      <td>3.647431</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2009</td>
      <td>2</td>
      <td>3.182016</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2009</td>
      <td>3</td>
      <td>3.199911</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2009</td>
      <td>4</td>
      <td>3.440155</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2009</td>
      <td>5</td>
      <td>6.793029</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Pivot and transpose
CO_imports = CO_imports.pivot(index = "month", columns = "year", values="import_value").T
CO_imports.head()
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
      <th>month</th>
      <th>1</th>
      <th>2</th>
      <th>3</th>
      <th>4</th>
      <th>5</th>
      <th>6</th>
      <th>7</th>
      <th>8</th>
      <th>9</th>
      <th>10</th>
      <th>11</th>
      <th>12</th>
    </tr>
    <tr>
      <th>year</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2009</th>
      <td>3.647431</td>
      <td>3.182016</td>
      <td>3.199911</td>
      <td>3.440155</td>
      <td>6.793029</td>
      <td>3.219196</td>
      <td>4.334389</td>
      <td>3.272593</td>
      <td>4.907628</td>
      <td>5.628341</td>
      <td>3.474514</td>
      <td>3.861137</td>
    </tr>
    <tr>
      <th>2010</th>
      <td>3.713896</td>
      <td>1.422861</td>
      <td>7.454151</td>
      <td>3.920450</td>
      <td>NaN</td>
      <td>4.993326</td>
      <td>4.507822</td>
      <td>4.783609</td>
      <td>6.426123</td>
      <td>6.523875</td>
      <td>4.613500</td>
      <td>4.846142</td>
    </tr>
    <tr>
      <th>2011</th>
      <td>4.502713</td>
      <td>4.416490</td>
      <td>5.367905</td>
      <td>5.209814</td>
      <td>5.873095</td>
      <td>5.624487</td>
      <td>5.217577</td>
      <td>5.965531</td>
      <td>5.924395</td>
      <td>5.453697</td>
      <td>6.001748</td>
      <td>5.538829</td>
    </tr>
    <tr>
      <th>2012</th>
      <td>4.832634</td>
      <td>4.763703</td>
      <td>5.478213</td>
      <td>5.075103</td>
      <td>5.991373</td>
      <td>5.737782</td>
      <td>5.502643</td>
      <td>5.704230</td>
      <td>5.203102</td>
      <td>5.731619</td>
      <td>5.940194</td>
      <td>4.851504</td>
    </tr>
    <tr>
      <th>2013</th>
      <td>5.425975</td>
      <td>5.283735</td>
      <td>5.534824</td>
      <td>6.043760</td>
      <td>5.327097</td>
      <td>5.498366</td>
      <td>5.763153</td>
      <td>5.002408</td>
      <td>5.157432</td>
      <td>6.191825</td>
      <td>5.903069</td>
      <td>5.274578</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Heatmap
ax = sns.heatmap(CO_imports)
```


    
![png](output_25_0.png)
    



```python
# Seaborn Options
ax = sns.heatmap(CO_imports, cmap="YlGnBu")

ax.set(ylabel="Year",
       xlabel="Month",
       title="CO Imports by Year Month");
```


    
![png](output_26_0.png)
    



```python
# Joint Plots in Seaborn
wage1 = pd.read_stata(url + "wage1.dta")

ax = sns.jointplot(y = "wage", x = "educ", data=wage1)
```


    
![png](output_27_0.png)
    



```python
# Update axes labels?
ax = sns.jointplot(y = "wage", x = "educ", data=wage1)
ax.set(ylabel="Wage", xlabel="Education")
```


    ---------------------------------------------------------------------------

    AttributeError                            Traceback (most recent call last)

    Cell In[25], line 3
          1 # Update axes labels?
          2 ax = sns.jointplot(y = "wage", x = "educ", data=wage1)
    ----> 3 ax.set(ylabel="Wage", xlabel="Education")
    

    File ~\anaconda3\Lib\site-packages\seaborn\axisgrid.py:42, in _BaseGrid.set(self, **kwargs)
         40 def set(self, **kwargs):
         41     """Set attributes on each subplot Axes."""
    ---> 42     for ax in self.axes.flat:
         43         if ax is not None:  # Handle removed axes
         44             ax.set(**kwargs)
    

    AttributeError: 'JointGrid' object has no attribute 'axes'



    
![png](output_28_1.png)
    



```python
# It has it's own structure
ax = sns.jointplot(y = "wage", x = "educ", data=wage1, color="green", height=5)
ax.set_axis_labels("Education (years)", "Wage (dollars per hour)");

```


    
![png](output_29_0.png)
    



```python
# what are their types?
print(type(ax))
print(type(ax.ax_joint))
```

    <class 'seaborn.axisgrid.JointGrid'>
    <class 'matplotlib.axes._axes.Axes'>
    
