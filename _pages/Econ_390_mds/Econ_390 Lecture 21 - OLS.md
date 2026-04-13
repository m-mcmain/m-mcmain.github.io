---
layout: single
sitemap: false
permalink: /pages/Econ_390_SP26_L21_teaching/
title: Econ 390 Lecture 21
---

[Download Jupyter Notebook Empty](https://m-mcmain.github.io/files/Econ390SP26/Lectures/Lecture21_OLS_empty.ipynb)

Download Jupyter Notebook Completed

# Econ 390 - Lecture 21: OLS
Today we will be looking at examining the relationships between variables using visualizations and Ordinary Least Squares in Python. You can find the relevant info from [McKinney](https://wesmckinney.com/book/modeling#modeling-statsmodels) and a similar but different package in [Turrell](https://aeturrell.github.io/coding-for-economists/econmt-regression.html#regression-basics).


```python
import seaborn as sns
import matplotlib.pyplot as plt 
```

## Visualization


```python
# Load seaborn dataset
taxi = sns.load_dataset("taxis")
taxi
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
      <th>pickup</th>
      <th>dropoff</th>
      <th>passengers</th>
      <th>distance</th>
      <th>fare</th>
      <th>tip</th>
      <th>tolls</th>
      <th>total</th>
      <th>color</th>
      <th>payment</th>
      <th>pickup_zone</th>
      <th>dropoff_zone</th>
      <th>pickup_borough</th>
      <th>dropoff_borough</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2019-03-23 20:21:09</td>
      <td>2019-03-23 20:27:24</td>
      <td>1</td>
      <td>1.60</td>
      <td>7.0</td>
      <td>2.15</td>
      <td>0.0</td>
      <td>12.95</td>
      <td>yellow</td>
      <td>credit card</td>
      <td>Lenox Hill West</td>
      <td>UN/Turtle Bay South</td>
      <td>Manhattan</td>
      <td>Manhattan</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2019-03-04 16:11:55</td>
      <td>2019-03-04 16:19:00</td>
      <td>1</td>
      <td>0.79</td>
      <td>5.0</td>
      <td>0.00</td>
      <td>0.0</td>
      <td>9.30</td>
      <td>yellow</td>
      <td>cash</td>
      <td>Upper West Side South</td>
      <td>Upper West Side South</td>
      <td>Manhattan</td>
      <td>Manhattan</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2019-03-27 17:53:01</td>
      <td>2019-03-27 18:00:25</td>
      <td>1</td>
      <td>1.37</td>
      <td>7.5</td>
      <td>2.36</td>
      <td>0.0</td>
      <td>14.16</td>
      <td>yellow</td>
      <td>credit card</td>
      <td>Alphabet City</td>
      <td>West Village</td>
      <td>Manhattan</td>
      <td>Manhattan</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2019-03-10 01:23:59</td>
      <td>2019-03-10 01:49:51</td>
      <td>1</td>
      <td>7.70</td>
      <td>27.0</td>
      <td>6.15</td>
      <td>0.0</td>
      <td>36.95</td>
      <td>yellow</td>
      <td>credit card</td>
      <td>Hudson Sq</td>
      <td>Yorkville West</td>
      <td>Manhattan</td>
      <td>Manhattan</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2019-03-30 13:27:42</td>
      <td>2019-03-30 13:37:14</td>
      <td>3</td>
      <td>2.16</td>
      <td>9.0</td>
      <td>1.10</td>
      <td>0.0</td>
      <td>13.40</td>
      <td>yellow</td>
      <td>credit card</td>
      <td>Midtown East</td>
      <td>Yorkville West</td>
      <td>Manhattan</td>
      <td>Manhattan</td>
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
      <th>6428</th>
      <td>2019-03-31 09:51:53</td>
      <td>2019-03-31 09:55:27</td>
      <td>1</td>
      <td>0.75</td>
      <td>4.5</td>
      <td>1.06</td>
      <td>0.0</td>
      <td>6.36</td>
      <td>green</td>
      <td>credit card</td>
      <td>East Harlem North</td>
      <td>Central Harlem North</td>
      <td>Manhattan</td>
      <td>Manhattan</td>
    </tr>
    <tr>
      <th>6429</th>
      <td>2019-03-31 17:38:00</td>
      <td>2019-03-31 18:34:23</td>
      <td>1</td>
      <td>18.74</td>
      <td>58.0</td>
      <td>0.00</td>
      <td>0.0</td>
      <td>58.80</td>
      <td>green</td>
      <td>credit card</td>
      <td>Jamaica</td>
      <td>East Concourse/Concourse Village</td>
      <td>Queens</td>
      <td>Bronx</td>
    </tr>
    <tr>
      <th>6430</th>
      <td>2019-03-23 22:55:18</td>
      <td>2019-03-23 23:14:25</td>
      <td>1</td>
      <td>4.14</td>
      <td>16.0</td>
      <td>0.00</td>
      <td>0.0</td>
      <td>17.30</td>
      <td>green</td>
      <td>cash</td>
      <td>Crown Heights North</td>
      <td>Bushwick North</td>
      <td>Brooklyn</td>
      <td>Brooklyn</td>
    </tr>
    <tr>
      <th>6431</th>
      <td>2019-03-04 10:09:25</td>
      <td>2019-03-04 10:14:29</td>
      <td>1</td>
      <td>1.12</td>
      <td>6.0</td>
      <td>0.00</td>
      <td>0.0</td>
      <td>6.80</td>
      <td>green</td>
      <td>credit card</td>
      <td>East New York</td>
      <td>East Flatbush/Remsen Village</td>
      <td>Brooklyn</td>
      <td>Brooklyn</td>
    </tr>
    <tr>
      <th>6432</th>
      <td>2019-03-13 19:31:22</td>
      <td>2019-03-13 19:48:02</td>
      <td>1</td>
      <td>3.85</td>
      <td>15.0</td>
      <td>3.36</td>
      <td>0.0</td>
      <td>20.16</td>
      <td>green</td>
      <td>credit card</td>
      <td>Boerum Hill</td>
      <td>Windsor Terrace</td>
      <td>Brooklyn</td>
      <td>Brooklyn</td>
    </tr>
  </tbody>
</table>
<p>6433 rows × 14 columns</p>
</div>




```python
# Scatterplot of fare and tip
fig, ax = plt.subplots()
ax.scatter(taxi["fare"],tips["tip"]);
```


    ---------------------------------------------------------------------------

    NameError                                 Traceback (most recent call last)

    Cell In[3], line 3
          1 # Scatterplot of fare and tip
          2 fig, ax = plt.subplots()
    ----> 3 ax.scatter(taxi["fare"],tips["tip"]);
    

    NameError: name 'tips' is not defined



    
![png](output_4_1.png)
    



```python
# Basic plot
taxi.plot.scatter("fare","tip");
```


    
![png](output_5_0.png)
    



```python
# Customizing
fig, ax = plt.subplots(figsize = (12, 6))
ax.scatter(taxi["fare"],taxi["tip"])
ax.set(xlabel = "Total Fare (Dollars)", ylabel = "Tip Amount (Dollars)")
sns.despine(ax=ax)
plt.show()
```


    
![png](output_6_0.png)
    



```python
# Convert tip into a percentage of fair and plot that
taxi['tip_pct'] = 100 * taxi["tip"] / taxi["fare"]

fig, ax = plt.subplots(figsize=(12,6))
ax.scatter(taxi['fare'],taxi['tip_pct'])
ax.set(xlabel='Total Fare (Dollars)', ylabel='Tip Amount (% of Fare)')
sns.despine()
plt.show()
```


    
![png](output_7_0.png)
    



```python
# Seaborn default scatterplot
sns.scatterplot(x="fare", y = "tip_pct", data = taxi);
```


    
![png](output_8_0.png)
    



```python
# Seaborn with customization
fig, ax = plt.subplots(figsize=(12,6)) 

ax = sns.scatterplot(x='fare', y='tip_pct', data=taxi)

ax.set(xlabel='Total Fare (Dollars)', ylabel='Tip Amount (% of Fare)')
sns.despine()
plt.show()
```


    
![png](output_9_0.png)
    



```python
# Jointplot
sns.jointplot(x='fare', y='tip_pct', data=taxi);
```


    
![png](output_10_0.png)
    



```python
# Customize Joint Plot?
ax = sns.jointplot(x='fare', y='tip_pct', data=taxi)
ax.set(xlabel='Total Fare (Dollars)', ylabel='Tip Amount (% of Fare)')
sns.despine()
plt.show()
```


    ---------------------------------------------------------------------------

    AttributeError                            Traceback (most recent call last)

    Cell In[10], line 3
          1 # Customize Joint Plot?
          2 ax = sns.jointplot(x='fare', y='tip_pct', data=taxi)
    ----> 3 ax.set(xlabel='Total Fare (Dollars)', ylabel='Tip Amount (% of Fare)')
          4 sns.despine()
          5 plt.show()
    

    File ~\anaconda3\Lib\site-packages\seaborn\axisgrid.py:42, in _BaseGrid.set(self, **kwargs)
         40 def set(self, **kwargs):
         41     """Set attributes on each subplot Axes."""
    ---> 42     for ax in self.axes.flat:
         43         if ax is not None:  # Handle removed axes
         44             ax.set(**kwargs)
    

    AttributeError: 'JointGrid' object has no attribute 'axes'



    
![png](output_11_1.png)
    



```python
# What are they
print(type(ax))
print(type(ax.ax_joint))
```

    <class 'seaborn.axisgrid.JointGrid'>
    <class 'matplotlib.axes._axes.Axes'>
    


```python
# Use .set on ax_joint
ax = sns.jointplot(x='fare', y='tip_pct', data=taxi)
ax.ax_joint.set(xlabel='Total Fare (Dollars)', ylabel='Tip Amount (% of Fare)');
```


    
![png](output_13_0.png)
    


## Practice - Visualization
1. Produce a similar joint plot but for payment instead of total bill.
2. With this in mind, remake the plot above but getting rid of the data that doesn't make sense to include. Hint: Subset the data in the jointplot function


```python
# Results:
ax = sns.jointplot(x='payment', y='tip_pct', data=taxi)
ax.ax_joint.set(xlabel='Payment Type', ylabel='Tip Amount (% of Fare)');

ax = sns.jointplot(x='fare', y='tip_pct', data=taxi[taxi["payment"] != "cash"])
ax.ax_joint.set(xlabel='Fare', ylabel='Tip Amount (% of Fare)');
```


    
![png](output_15_0.png)
    



    
![png](output_15_1.png)
    


## Regression Analysis


```python
# Update dataset to drop cash
taxi_noCash = taxi[taxi["payment"] != "cash"]
```


```python
# Correlations
taxi_noCash.corr(numeric_only = True)
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
      <th>passengers</th>
      <th>distance</th>
      <th>fare</th>
      <th>tip</th>
      <th>tolls</th>
      <th>total</th>
      <th>tip_pct</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>passengers</th>
      <td>1.000000</td>
      <td>-0.008417</td>
      <td>-0.014921</td>
      <td>0.033359</td>
      <td>-0.015673</td>
      <td>-0.002453</td>
      <td>0.059385</td>
    </tr>
    <tr>
      <th>distance</th>
      <td>-0.008417</td>
      <td>1.000000</td>
      <td>0.911750</td>
      <td>0.548785</td>
      <td>0.639564</td>
      <td>0.898474</td>
      <td>-0.308866</td>
    </tr>
    <tr>
      <th>fare</th>
      <td>-0.014921</td>
      <td>0.911750</td>
      <td>1.000000</td>
      <td>0.608724</td>
      <td>0.603518</td>
      <td>0.975890</td>
      <td>-0.339081</td>
    </tr>
    <tr>
      <th>tip</th>
      <td>0.033359</td>
      <td>0.548785</td>
      <td>0.608724</td>
      <td>1.000000</td>
      <td>0.499962</td>
      <td>0.745239</td>
      <td>0.320342</td>
    </tr>
    <tr>
      <th>tolls</th>
      <td>-0.015673</td>
      <td>0.639564</td>
      <td>0.603518</td>
      <td>0.499962</td>
      <td>1.000000</td>
      <td>0.684531</td>
      <td>-0.092381</td>
    </tr>
    <tr>
      <th>total</th>
      <td>-0.002453</td>
      <td>0.898474</td>
      <td>0.975890</td>
      <td>0.745239</td>
      <td>0.684531</td>
      <td>1.000000</td>
      <td>-0.197170</td>
    </tr>
    <tr>
      <th>tip_pct</th>
      <td>0.059385</td>
      <td>-0.308866</td>
      <td>-0.339081</td>
      <td>0.320342</td>
      <td>-0.092381</td>
      <td>-0.197170</td>
      <td>1.000000</td>
    </tr>
  </tbody>
</table>
</div>




```python
# New package!
import statsmodels.formula.api as smf 
```


```python
# Regression
reg_results = smf.ols("tip_pct ~ fare", data = taxi_noCash).fit()
reg_results
```




    <statsmodels.regression.linear_model.RegressionResultsWrapper at 0x272b408c440>




```python
# Print the results
print(reg_results.summary())
```

                                OLS Regression Results                            
    ==============================================================================
    Dep. Variable:                tip_pct   R-squared:                       0.115
    Model:                            OLS   Adj. R-squared:                  0.115
    Method:                 Least Squares   F-statistic:                     600.1
    Date:                Sun, 05 Apr 2026   Prob (F-statistic):          1.07e-124
    Time:                        18:12:36   Log-Likelihood:                -17698.
    No. Observations:                4621   AIC:                         3.540e+04
    Df Residuals:                    4619   BIC:                         3.541e+04
    Df Model:                           1                                         
    Covariance Type:            nonrobust                                         
    ==============================================================================
                     coef    std err          t      P>|t|      [0.025      0.975]
    ------------------------------------------------------------------------------
    Intercept     28.2847      0.253    111.659      0.000      27.788      28.781
    fare          -0.3458      0.014    -24.496      0.000      -0.373      -0.318
    ==============================================================================
    Omnibus:                      183.054   Durbin-Watson:                   1.828
    Prob(Omnibus):                  0.000   Jarque-Bera (JB):              354.345
    Skew:                          -0.293   Prob(JB):                     1.13e-77
    Kurtosis:                       4.224   Cond. No.                         27.8
    ==============================================================================
    
    Notes:
    [1] Standard Errors assume that the covariance matrix of the errors is correctly specified.
    


```python
# Bias correct the variances
reg_results = smf.ols("tip_pct ~ fare", data = taxi_noCash).fit(cov_type="HC1")
print(reg_results.summary())
```

                                OLS Regression Results                            
    ==============================================================================
    Dep. Variable:                tip_pct   R-squared:                       0.115
    Model:                            OLS   Adj. R-squared:                  0.115
    Method:                 Least Squares   F-statistic:                     385.3
    Date:                Sun, 05 Apr 2026   Prob (F-statistic):           1.84e-82
    Time:                        18:12:36   Log-Likelihood:                -17698.
    No. Observations:                4621   AIC:                         3.540e+04
    Df Residuals:                    4619   BIC:                         3.541e+04
    Df Model:                           1                                         
    Covariance Type:                  HC1                                         
    ==============================================================================
                     coef    std err          z      P>|z|      [0.025      0.975]
    ------------------------------------------------------------------------------
    Intercept     28.2847      0.287     98.523      0.000      27.722      28.847
    fare          -0.3458      0.018    -19.629      0.000      -0.380      -0.311
    ==============================================================================
    Omnibus:                      183.054   Durbin-Watson:                   1.828
    Prob(Omnibus):                  0.000   Jarque-Bera (JB):              354.345
    Skew:                          -0.293   Prob(JB):                     1.13e-77
    Kurtosis:                       4.224   Cond. No.                         27.8
    ==============================================================================
    
    Notes:
    [1] Standard Errors are heteroscedasticity robust (HC1)
    


```python
# Print results
print('Parameters: ', reg_results.params, '\n')
print('Standard Errors: ', reg_results.bse, '\n')
print('R^2: ', reg_results.rsquared)
```

    Parameters:  Intercept    28.284693
    fare         -0.345767
    dtype: float64 
    
    Standard Errors:  Intercept    0.287088
    fare         0.017615
    dtype: float64 
    
    R^2:  0.11497593631204905
    


```python
# Add fitted values to the DataFrame
taxi_noCash["fitted_values"] = reg_results.fittedvalues
taxi_noCash
```

    C:\Users\micha\AppData\Local\Temp\ipykernel_16192\1136982121.py:2: SettingWithCopyWarning: 
    A value is trying to be set on a copy of a slice from a DataFrame.
    Try using .loc[row_indexer,col_indexer] = value instead
    
    See the caveats in the documentation: https://pandas.pydata.org/pandas-docs/stable/user_guide/indexing.html#returning-a-view-versus-a-copy
      taxi_noCash["fitted_values"] = reg_results.fittedvalues
    




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
      <th>pickup</th>
      <th>dropoff</th>
      <th>passengers</th>
      <th>distance</th>
      <th>fare</th>
      <th>tip</th>
      <th>tolls</th>
      <th>total</th>
      <th>color</th>
      <th>payment</th>
      <th>pickup_zone</th>
      <th>dropoff_zone</th>
      <th>pickup_borough</th>
      <th>dropoff_borough</th>
      <th>tip_pct</th>
      <th>fitted_values</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2019-03-23 20:21:09</td>
      <td>2019-03-23 20:27:24</td>
      <td>1</td>
      <td>1.60</td>
      <td>7.0</td>
      <td>2.15</td>
      <td>0.0</td>
      <td>12.95</td>
      <td>yellow</td>
      <td>credit card</td>
      <td>Lenox Hill West</td>
      <td>UN/Turtle Bay South</td>
      <td>Manhattan</td>
      <td>Manhattan</td>
      <td>30.714286</td>
      <td>25.864326</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2019-03-27 17:53:01</td>
      <td>2019-03-27 18:00:25</td>
      <td>1</td>
      <td>1.37</td>
      <td>7.5</td>
      <td>2.36</td>
      <td>0.0</td>
      <td>14.16</td>
      <td>yellow</td>
      <td>credit card</td>
      <td>Alphabet City</td>
      <td>West Village</td>
      <td>Manhattan</td>
      <td>Manhattan</td>
      <td>31.466667</td>
      <td>25.691442</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2019-03-10 01:23:59</td>
      <td>2019-03-10 01:49:51</td>
      <td>1</td>
      <td>7.70</td>
      <td>27.0</td>
      <td>6.15</td>
      <td>0.0</td>
      <td>36.95</td>
      <td>yellow</td>
      <td>credit card</td>
      <td>Hudson Sq</td>
      <td>Yorkville West</td>
      <td>Manhattan</td>
      <td>Manhattan</td>
      <td>22.777778</td>
      <td>18.948990</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2019-03-30 13:27:42</td>
      <td>2019-03-30 13:37:14</td>
      <td>3</td>
      <td>2.16</td>
      <td>9.0</td>
      <td>1.10</td>
      <td>0.0</td>
      <td>13.40</td>
      <td>yellow</td>
      <td>credit card</td>
      <td>Midtown East</td>
      <td>Yorkville West</td>
      <td>Manhattan</td>
      <td>Manhattan</td>
      <td>12.222222</td>
      <td>25.172792</td>
    </tr>
    <tr>
      <th>5</th>
      <td>2019-03-11 10:37:23</td>
      <td>2019-03-11 10:47:31</td>
      <td>1</td>
      <td>0.49</td>
      <td>7.5</td>
      <td>2.16</td>
      <td>0.0</td>
      <td>12.96</td>
      <td>yellow</td>
      <td>credit card</td>
      <td>Times Sq/Theatre District</td>
      <td>Midtown East</td>
      <td>Manhattan</td>
      <td>Manhattan</td>
      <td>28.800000</td>
      <td>25.691442</td>
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
      <td>...</td>
    </tr>
    <tr>
      <th>6426</th>
      <td>2019-03-28 08:04:47</td>
      <td>2019-03-28 08:07:46</td>
      <td>1</td>
      <td>0.71</td>
      <td>4.5</td>
      <td>0.50</td>
      <td>0.0</td>
      <td>5.80</td>
      <td>green</td>
      <td>credit card</td>
      <td>Central Park</td>
      <td>Upper West Side North</td>
      <td>Manhattan</td>
      <td>Manhattan</td>
      <td>11.111111</td>
      <td>26.728743</td>
    </tr>
    <tr>
      <th>6428</th>
      <td>2019-03-31 09:51:53</td>
      <td>2019-03-31 09:55:27</td>
      <td>1</td>
      <td>0.75</td>
      <td>4.5</td>
      <td>1.06</td>
      <td>0.0</td>
      <td>6.36</td>
      <td>green</td>
      <td>credit card</td>
      <td>East Harlem North</td>
      <td>Central Harlem North</td>
      <td>Manhattan</td>
      <td>Manhattan</td>
      <td>23.555556</td>
      <td>26.728743</td>
    </tr>
    <tr>
      <th>6429</th>
      <td>2019-03-31 17:38:00</td>
      <td>2019-03-31 18:34:23</td>
      <td>1</td>
      <td>18.74</td>
      <td>58.0</td>
      <td>0.00</td>
      <td>0.0</td>
      <td>58.80</td>
      <td>green</td>
      <td>credit card</td>
      <td>Jamaica</td>
      <td>East Concourse/Concourse Village</td>
      <td>Queens</td>
      <td>Bronx</td>
      <td>0.000000</td>
      <td>8.230219</td>
    </tr>
    <tr>
      <th>6431</th>
      <td>2019-03-04 10:09:25</td>
      <td>2019-03-04 10:14:29</td>
      <td>1</td>
      <td>1.12</td>
      <td>6.0</td>
      <td>0.00</td>
      <td>0.0</td>
      <td>6.80</td>
      <td>green</td>
      <td>credit card</td>
      <td>East New York</td>
      <td>East Flatbush/Remsen Village</td>
      <td>Brooklyn</td>
      <td>Brooklyn</td>
      <td>0.000000</td>
      <td>26.210092</td>
    </tr>
    <tr>
      <th>6432</th>
      <td>2019-03-13 19:31:22</td>
      <td>2019-03-13 19:48:02</td>
      <td>1</td>
      <td>3.85</td>
      <td>15.0</td>
      <td>3.36</td>
      <td>0.0</td>
      <td>20.16</td>
      <td>green</td>
      <td>credit card</td>
      <td>Boerum Hill</td>
      <td>Windsor Terrace</td>
      <td>Brooklyn</td>
      <td>Brooklyn</td>
      <td>22.400000</td>
      <td>23.098191</td>
    </tr>
  </tbody>
</table>
<p>4621 rows × 16 columns</p>
</div>




```python
# lmplot
sns.lmplot(x="fare", y="tip_pct", data=taxi_noCash);
```


    
![png](output_25_0.png)
    



```python
# lmplot customized
ax = sns.lmplot(x="fare", y="tip_pct", data=taxi_noCash, markers='.', line_kws={'color': 'orange'})
ax.set(xlabel='Total Fare (Dollars)', ylabel='Tip Amount (% of Fare)',)
sns.despine()
plt.show()
```


    
![png](output_26_0.png)
    



```python
# Another regression
reg_results2 = smf.ols('tip_pct ~ fare + passengers', data=taxi_noCash).fit(cov_type='HC1')
print(reg_results2.summary())
```

                                OLS Regression Results                            
    ==============================================================================
    Dep. Variable:                tip_pct   R-squared:                       0.118
    Model:                            OLS   Adj. R-squared:                  0.118
    Method:                 Least Squares   F-statistic:                     206.3
    Date:                Sun, 05 Apr 2026   Prob (F-statistic):           1.47e-86
    Time:                        18:12:38   Log-Likelihood:                -17690.
    No. Observations:                4621   AIC:                         3.539e+04
    Df Residuals:                    4618   BIC:                         3.541e+04
    Df Model:                           2                                         
    Covariance Type:                  HC1                                         
    ==============================================================================
                     coef    std err          z      P>|z|      [0.025      0.975]
    ------------------------------------------------------------------------------
    Intercept     27.4592      0.355     77.281      0.000      26.763      28.156
    fare          -0.3449      0.018    -19.687      0.000      -0.379      -0.311
    passengers     0.5307      0.125      4.259      0.000       0.287       0.775
    ==============================================================================
    Omnibus:                      176.058   Durbin-Watson:                   1.832
    Prob(Omnibus):                  0.000   Jarque-Bera (JB):              339.034
    Skew:                          -0.283   Prob(JB):                     2.40e-74
    Kurtosis:                       4.200   Cond. No.                         37.5
    ==============================================================================
    
    Notes:
    [1] Standard Errors are heteroscedasticity robust (HC1)
    


```python
# New function
from statsmodels.iolib.summary2 import summary_col
```


```python
# Prettier printing
model1 = smf.ols('tip_pct ~ fare', data=taxi_noCash).fit(cov_type='HC1')
model2 = smf.ols('tip_pct ~ fare + passengers', data=taxi_noCash).fit(cov_type='HC1')

print(summary_col([model1, model2]))
```

    
    ===================================
                   tip_pct I tip_pct II
    -----------------------------------
    Intercept      28.2847   27.4592   
                   (0.2871)  (0.3553)  
    fare           -0.3458   -0.3449   
                   (0.0176)  (0.0175)  
    passengers               0.5307    
                             (0.1246)  
    R-squared      0.1150    0.1179    
    R-squared Adj. 0.1148    0.1175    
    ===================================
    Standard errors in parentheses.
    


```python
# Options
print(summary_col([model1,model2], stars=True, float_format='%0.2f',
                  regressor_order=['Intercept','fare','passengers'],
                  model_names=['(1)','(2)']))
```

    
    ================================
                     (1)      (2)   
    --------------------------------
    Intercept      28.28*** 27.46***
                   (0.29)   (0.36)  
    fare           -0.35*** -0.34***
                   (0.02)   (0.02)  
    passengers              0.53*** 
                            (0.12)  
    R-squared      0.11     0.12    
    R-squared Adj. 0.11     0.12    
    ================================
    Standard errors in parentheses.
    * p<.1, ** p<.05, ***p<.01
    

## Practice - Regression Analysis
1. The results for a linear relationship between tip_pct and fare looks pretty bad. What if it's quadratic? How do we add that? Hint: There are multiple ways of doing this.
2. Make a nice regression table using summary_col comparing the linear and the quadratic models
3. Now, how can we get that onto the lmplot? Hint: Check out the "order" argument. What does order mean in the context of equations?


```python
# Results:

model1 = smf.ols('tip_pct ~ fare', data=taxi_noCash).fit(cov_type='HC1')
model2 = smf.ols('tip_pct ~ fare + I(fare**2)', data=taxi_noCash).fit(cov_type='HC1')

print(summary_col([model1,model2], stars=True, float_format='%0.2f',
                  regressor_order=['Intercept','fare'],
                  model_names=['(1)','(2)']))

ax = sns.lmplot(x="fare", y="tip_pct", data=taxi_noCash, markers='.', line_kws={'color': 'orange'}, order = 2)
ax.set(xlabel='Total Fare (Dollars)', ylabel='Tip Amount (% of Fare)',)
sns.despine()
plt.show()
```

    
    ================================
                     (1)      (2)   
    --------------------------------
    Intercept      28.28*** 31.82***
                   (0.29)   (0.45)  
    fare           -0.35*** -0.79***
                   (0.02)   (0.05)  
    I(fare ** 2)            0.01*** 
                            (0.00)  
    R-squared      0.11     0.15    
    R-squared Adj. 0.11     0.15    
    ================================
    Standard errors in parentheses.
    * p<.1, ** p<.05, ***p<.01
    


    
![png](output_32_1.png)
    

