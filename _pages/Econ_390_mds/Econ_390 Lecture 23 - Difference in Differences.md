---
layout: single
sitemap: false
permalink: /pages/Econ_390_SP26_L23_teaching/
title: Econ 390 Lecture 23
---

[Download Jupyter Notebook Empty](https://m-mcmain.github.io/files/Econ390SP26/Lectures/Lecture23_DifferenceinDifferences_empty.ipynb)

Download Jupyter Notebook Completed

# Econ 390: Lecture 23 - Difference in Differences
Today we will be going over how to visualize and conduct the econometric method called Difference in Differences (DiD). DiD at its core is very simple, there is a point in time where something changes and we want to understand what that change caused. We can't just assume everything after the change is due to the change alone, so we find a comparison group to disentangle the change and time itself. Inspiration for this lecture can be found [here](https://www.pymc.io/projects/examples/en/latest/causal_inference/difference_in_differences.html) and [here](https://aaronmams.github.io/Card-Krueger-Replication/).

![Simple Diff-in-Diff Example](https://www.pymc.io/projects/examples/en/latest/_images/8f0282bc3fafdc3f95d353ed712496d5fab4d0c009f5c0d8ecaf42f7a8626b37.png)

## Parallel Trends
Parallel trends are *paramount* to our assumption of Difference-in-Differences analysis! It must be the case that these two groups are **actually comparable**. This analysis is all about what would have happened if the treatment group was not treated. We must be confident that we can actually extract that using the information on the control group!

## Card and Krueger (1994)
One of the most famous example of DiD is from the 1992 American Economic Review (AER) paper "Minimum Wages and Employment: A Case Study of the Fast-Food Industry in New Jersey and Pennsylvania" by David Card and Alan Krueger (you can find the paper and data on Card's website [here](https://davidcard.berkeley.edu/data_sets)).


```python
import pandas as pd
import matplotlib.pyplot as plt 
import statsmodels.formula.api as smf 

econ390path = "https://m-mcmain.github.io/files/Econ390SP26/"
```


```python
# Data process
names = ["CHAINr", "CO_OWNED", "STATEr", "SOUTHJ", "CENTRALJ", "NORTHJ", "PA1", "PA2", "SHORE", "NCALLS", 
         "EMPFT", "EMPPT", "NMGRS", "WAGE_ST", "INCTIME", "FIRSTINC", "BONUS", "PCTAFF", "MEAL", "OPEN",
         "HRSOPEN", "PSODA", "PFRY", "PENTREE", "NREGS", "NREGS11", "TYPE2", "STATUS2", "DATE2", "NCALLS2",
         "EMPFT2", "EMPPT2", "NMGRS2", "WAGE_ST2", "INCTIME2", "FIRSTIN2", "SPECIAL2", "MEALS2", "OPEN2R",
         "HRSOPEN2", "PSODA2", "PFRY2", "PENTREE2", "NREGS2", "NREGS112"]
ck = pd.read_csv(econ390path + "card_krueger_public.dat", sep="\s+", header = None, names = names)
ck.head()
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
      <th>CHAINr</th>
      <th>CO_OWNED</th>
      <th>STATEr</th>
      <th>SOUTHJ</th>
      <th>CENTRALJ</th>
      <th>NORTHJ</th>
      <th>PA1</th>
      <th>PA2</th>
      <th>SHORE</th>
      <th>NCALLS</th>
      <th>...</th>
      <th>FIRSTIN2</th>
      <th>SPECIAL2</th>
      <th>MEALS2</th>
      <th>OPEN2R</th>
      <th>HRSOPEN2</th>
      <th>PSODA2</th>
      <th>PFRY2</th>
      <th>PENTREE2</th>
      <th>NREGS2</th>
      <th>NREGS112</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>46</th>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>...</td>
      <td>0.08</td>
      <td>1</td>
      <td>2</td>
      <td>6.50</td>
      <td>16.50</td>
      <td>1.03</td>
      <td>.</td>
      <td>0.94</td>
      <td>4</td>
      <td>4</td>
    </tr>
    <tr>
      <th>49</th>
      <td>2</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>...</td>
      <td>0.05</td>
      <td>0</td>
      <td>2</td>
      <td>10.00</td>
      <td>13.00</td>
      <td>1.01</td>
      <td>0.89</td>
      <td>2.35</td>
      <td>4</td>
      <td>4</td>
    </tr>
    <tr>
      <th>506</th>
      <td>2</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>...</td>
      <td>0.25</td>
      <td>.</td>
      <td>1</td>
      <td>11.00</td>
      <td>11.00</td>
      <td>0.95</td>
      <td>0.74</td>
      <td>2.33</td>
      <td>4</td>
      <td>3</td>
    </tr>
    <tr>
      <th>56</th>
      <td>4</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>...</td>
      <td>0.15</td>
      <td>0</td>
      <td>2</td>
      <td>10.00</td>
      <td>12.00</td>
      <td>0.92</td>
      <td>0.79</td>
      <td>0.87</td>
      <td>2</td>
      <td>2</td>
    </tr>
    <tr>
      <th>61</th>
      <td>4</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>...</td>
      <td>0.15</td>
      <td>0</td>
      <td>2</td>
      <td>10.00</td>
      <td>12.00</td>
      <td>1.01</td>
      <td>0.84</td>
      <td>0.95</td>
      <td>2</td>
      <td>2</td>
    </tr>
  </tbody>
</table>
<p>5 rows × 45 columns</p>
</div>




```python
# Measure of employment
ck["EMP_TOT"] = pd.to_numeric(ck["EMPFT"],errors="coerce") + pd.to_numeric(ck["EMPPT"],errors="coerce")*0.5 + pd.to_numeric(ck["NMGRS"], errors="coerce")
ck["EMP_TOT2"] = pd.to_numeric(ck["EMPFT2"],errors="coerce") + pd.to_numeric(ck["EMPPT2"],errors="coerce")*0.5 + pd.to_numeric(ck["NMGRS2"],errors="coerce")
ck.head()
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
      <th>CHAINr</th>
      <th>CO_OWNED</th>
      <th>STATEr</th>
      <th>SOUTHJ</th>
      <th>CENTRALJ</th>
      <th>NORTHJ</th>
      <th>PA1</th>
      <th>PA2</th>
      <th>SHORE</th>
      <th>NCALLS</th>
      <th>...</th>
      <th>MEALS2</th>
      <th>OPEN2R</th>
      <th>HRSOPEN2</th>
      <th>PSODA2</th>
      <th>PFRY2</th>
      <th>PENTREE2</th>
      <th>NREGS2</th>
      <th>NREGS112</th>
      <th>EMP_TOT</th>
      <th>EMP_TOT2</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>46</th>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>...</td>
      <td>2</td>
      <td>6.50</td>
      <td>16.50</td>
      <td>1.03</td>
      <td>.</td>
      <td>0.94</td>
      <td>4</td>
      <td>4</td>
      <td>40.50</td>
      <td>24.0</td>
    </tr>
    <tr>
      <th>49</th>
      <td>2</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>...</td>
      <td>2</td>
      <td>10.00</td>
      <td>13.00</td>
      <td>1.01</td>
      <td>0.89</td>
      <td>2.35</td>
      <td>4</td>
      <td>4</td>
      <td>13.75</td>
      <td>11.5</td>
    </tr>
    <tr>
      <th>506</th>
      <td>2</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>...</td>
      <td>1</td>
      <td>11.00</td>
      <td>11.00</td>
      <td>0.95</td>
      <td>0.74</td>
      <td>2.33</td>
      <td>4</td>
      <td>3</td>
      <td>8.50</td>
      <td>10.5</td>
    </tr>
    <tr>
      <th>56</th>
      <td>4</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>...</td>
      <td>2</td>
      <td>10.00</td>
      <td>12.00</td>
      <td>0.92</td>
      <td>0.79</td>
      <td>0.87</td>
      <td>2</td>
      <td>2</td>
      <td>34.00</td>
      <td>20.0</td>
    </tr>
    <tr>
      <th>61</th>
      <td>4</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>...</td>
      <td>2</td>
      <td>10.00</td>
      <td>12.00</td>
      <td>1.01</td>
      <td>0.84</td>
      <td>0.95</td>
      <td>2</td>
      <td>2</td>
      <td>24.00</td>
      <td>35.5</td>
    </tr>
  </tbody>
</table>
<p>5 rows × 47 columns</p>
</div>




```python
# Convert data we need
ck["WAGE_ST"] = pd.to_numeric(ck["WAGE_ST"],errors="coerce")
ck["WAGE_ST2"] = pd.to_numeric(ck["WAGE_ST2"],errors="coerce")
ck["STATEr"] = pd.Categorical.from_codes(ck["STATEr"], ["PA","NJ"])
```

## Wage Visualizations


```python
# Basic Visualization of Wages
plt.hist(ck["WAGE_ST"][ck["STATEr"]=="NJ"], density=True, alpha=0.5, label='NJ')
plt.hist(ck["WAGE_ST"][ck["STATEr"]=="PA"], density=True, alpha=0.5, label='PA')
plt.legend(loc='upper right')
plt.show()
```


    
![png](output_9_0.png)
    



```python
# Force the Same Bins
counts, bins, patches = plt.hist(ck["WAGE_ST"][ck["STATEr"]=="NJ"], density=True, alpha=0.5, label='NJ')
plt.hist(ck["WAGE_ST"][ck["STATEr"]=="PA"], bins=bins, density=True, alpha=0.5, label='PA')
plt.legend(loc='upper right')
plt.show()
```


    
![png](output_10_0.png)
    



```python
# Second Period same bins
counts, bins, patches = plt.hist(ck["WAGE_ST2"][ck["STATEr"]=="NJ"], density=True, alpha=0.5, label='NJ')
plt.hist(ck["WAGE_ST2"][ck["STATEr"]=="PA"], bins=bins, density=True, alpha=0.5, label='PA')
plt.legend(loc='upper right')
plt.show()
```


    
![png](output_11_0.png)
    



```python
# Good reason to not have the same bins!
plt.hist(ck["WAGE_ST2"][ck["STATEr"]=="NJ"], density=True, alpha=0.5, label='NJ')
plt.hist(ck["WAGE_ST2"][ck["STATEr"]=="PA"], density=True, alpha=0.5, label='PA')
plt.legend(loc='upper right')
plt.show()
```


    
![png](output_12_0.png)
    



```python
# Compare within NJ before and after
plt.hist(ck["WAGE_ST"][ck["STATEr"]=="NJ"], density=True, alpha=0.5, label='Before')
plt.hist(ck["WAGE_ST2"][ck["STATEr"]=="NJ"], density=True, alpha=0.5, label='After')
plt.legend(loc='upper right')
plt.show()
```


    
![png](output_13_0.png)
    



```python
# What happens in PA?
counts, bins, patches = plt.hist(ck["WAGE_ST"][ck["STATEr"]=="PA"], density=True, alpha=0.5, label='Before')
plt.hist(ck["WAGE_ST2"][ck["STATEr"]=="PA"], bins=bins, density=True, alpha=0.5, label='After')
plt.legend(loc='upper right')
plt.show()
```


    
![png](output_14_0.png)
    



```python
# Classic DiD Plot on Wage:
print(ck[["STATEr","WAGE_ST"]].groupby("STATEr").mean())
wage_before = ck[["STATEr","WAGE_ST"]].groupby("STATEr").mean()
print(ck[["STATEr","WAGE_ST2"]].groupby("STATEr").mean())
wage_after = ck[["STATEr","WAGE_ST2"]].groupby("STATEr").mean()
avg_wage_df = pd.DataFrame({"Time":[0,1],
                            "Wage_NJ":[wage_before.iloc[1,0],wage_after.iloc[1,0]],
                            "Wage_PA":[wage_before.iloc[0,0],wage_after.iloc[0,0]]})
print(avg_wage_df)
```

             WAGE_ST
    STATEr          
    PA      4.630132
    NJ      4.612134
            WAGE_ST2
    STATEr          
    PA      4.617465
    NJ      5.080849
       Time   Wage_NJ   Wage_PA
    0     0  4.612134  4.630132
    1     1  5.080849  4.617465
    

    C:\Users\micha\AppData\Local\Temp\ipykernel_13152\3945664568.py:2: FutureWarning: The default of observed=False is deprecated and will be changed to True in a future version of pandas. Pass observed=False to retain current behavior or observed=True to adopt the future default and silence this warning.
      print(ck[["STATEr","WAGE_ST"]].groupby("STATEr").mean())
    C:\Users\micha\AppData\Local\Temp\ipykernel_13152\3945664568.py:3: FutureWarning: The default of observed=False is deprecated and will be changed to True in a future version of pandas. Pass observed=False to retain current behavior or observed=True to adopt the future default and silence this warning.
      wage_before = ck[["STATEr","WAGE_ST"]].groupby("STATEr").mean()
    C:\Users\micha\AppData\Local\Temp\ipykernel_13152\3945664568.py:4: FutureWarning: The default of observed=False is deprecated and will be changed to True in a future version of pandas. Pass observed=False to retain current behavior or observed=True to adopt the future default and silence this warning.
      print(ck[["STATEr","WAGE_ST2"]].groupby("STATEr").mean())
    C:\Users\micha\AppData\Local\Temp\ipykernel_13152\3945664568.py:5: FutureWarning: The default of observed=False is deprecated and will be changed to True in a future version of pandas. Pass observed=False to retain current behavior or observed=True to adopt the future default and silence this warning.
      wage_after = ck[["STATEr","WAGE_ST2"]].groupby("STATEr").mean()
    


```python
# Standard Plot, not necessarily surprising results
fig, ax = plt.subplots()
plt.plot(avg_wage_df["Time"],avg_wage_df["Wage_NJ"],label="NJ")
plt.plot(avg_wage_df["Time"],avg_wage_df["Wage_PA"],label="PA")
plt.axvline(0.5, color="red")
plt.legend()
labels=["Before","After"]
plt.xticks(avg_wage_df["Time"],labels)
plt.show()
```


    
![png](output_16_0.png)
    


## Employment Visualization


```python
# Eployment Across Time in NJ
counts, bins, patches = plt.hist(ck["EMP_TOT"][ck["STATEr"]=="NJ"], density=True, alpha=0.5, label='Before')
plt.hist(ck["EMP_TOT2"][ck["STATEr"]=="NJ"], bins=bins, density=True, alpha=0.5, label='After')
plt.legend(loc='upper right')
plt.show()
```


    
![png](output_18_0.png)
    



```python
# Employment Across States in Post-Period
counts, bins, patches = plt.hist(ck["EMP_TOT2"][ck["STATEr"]=="NJ"], density=True, alpha=0.5, label='NJ')
plt.hist(ck["EMP_TOT2"][ck["STATEr"]=="PA"], bins=bins, density=True, alpha=0.5, label='PA')
plt.legend(loc='upper right')
plt.show()
```


    
![png](output_19_0.png)
    



```python
# Employment Across States in Pre-Period
counts, bins, patches = plt.hist(ck["EMP_TOT"][ck["STATEr"]=="NJ"], density=True, alpha=0.5, label='NJ')
plt.hist(ck["EMP_TOT"][ck["STATEr"]=="PA"], bins=bins, density=True, alpha=0.5, label='PA')
plt.legend(loc='upper right')
plt.show()
```


    
![png](output_20_0.png)
    



```python
# Classic DiD Plot on Employment:
print(ck[["STATEr","EMP_TOT"]].groupby("STATEr").mean())
EMP_before = ck[["STATEr","EMP_TOT"]].groupby("STATEr").mean()
print(ck[["STATEr","EMP_TOT2"]].groupby("STATEr").mean())
EMP_after = ck[["STATEr","EMP_TOT2"]].groupby("STATEr").mean()
avg_EMP_df = pd.DataFrame({"Time":[0,1],
                            "EMP_NJ":[EMP_before.iloc[1,0],EMP_after.iloc[1,0]],
                            "EMP_PA":[EMP_before.iloc[0,0],EMP_after.iloc[0,0]]})
print(avg_EMP_df)
```

              EMP_TOT
    STATEr           
    PA      23.331169
    NJ      20.439408
             EMP_TOT2
    STATEr           
    PA      21.165584
    NJ      21.027429
       Time     EMP_NJ     EMP_PA
    0     0  20.439408  23.331169
    1     1  21.027429  21.165584
    

    C:\Users\micha\AppData\Local\Temp\ipykernel_13152\2401754607.py:2: FutureWarning: The default of observed=False is deprecated and will be changed to True in a future version of pandas. Pass observed=False to retain current behavior or observed=True to adopt the future default and silence this warning.
      print(ck[["STATEr","EMP_TOT"]].groupby("STATEr").mean())
    C:\Users\micha\AppData\Local\Temp\ipykernel_13152\2401754607.py:3: FutureWarning: The default of observed=False is deprecated and will be changed to True in a future version of pandas. Pass observed=False to retain current behavior or observed=True to adopt the future default and silence this warning.
      EMP_before = ck[["STATEr","EMP_TOT"]].groupby("STATEr").mean()
    C:\Users\micha\AppData\Local\Temp\ipykernel_13152\2401754607.py:4: FutureWarning: The default of observed=False is deprecated and will be changed to True in a future version of pandas. Pass observed=False to retain current behavior or observed=True to adopt the future default and silence this warning.
      print(ck[["STATEr","EMP_TOT2"]].groupby("STATEr").mean())
    C:\Users\micha\AppData\Local\Temp\ipykernel_13152\2401754607.py:5: FutureWarning: The default of observed=False is deprecated and will be changed to True in a future version of pandas. Pass observed=False to retain current behavior or observed=True to adopt the future default and silence this warning.
      EMP_after = ck[["STATEr","EMP_TOT2"]].groupby("STATEr").mean()
    


```python
# Standard Plot, not necessarily surprising results
fig, ax = plt.subplots()
plt.plot(avg_EMP_df["Time"],avg_EMP_df["EMP_NJ"],label="NJ")
plt.plot(avg_EMP_df["Time"],avg_EMP_df["EMP_PA"],label="PA")
plt.axvline(0.5, color="red")
plt.legend()
labels=["Before","After"]
plt.xticks(avg_EMP_df["Time"],labels)
plt.show()
```


    
![png](output_22_0.png)
    


## DiD Regression


```python
# Basic Regressions
ck["CHANGE_EMP"] = ck["EMP_TOT2"]-ck["EMP_TOT"]
model1 = smf.ols("CHANGE_EMP ~ STATEr",data=ck).fit(cov_type="HC1")
print(model1.summary())
```

                                OLS Regression Results                            
    ==============================================================================
    Dep. Variable:             CHANGE_EMP   R-squared:                       0.015
    Model:                            OLS   Adj. R-squared:                  0.012
    Method:                 Least Squares   F-statistic:                     4.226
    Date:                Fri, 17 Apr 2026   Prob (F-statistic):             0.0405
    Time:                        16:51:45   Log-Likelihood:                -1386.2
    No. Observations:                 384   AIC:                             2776.
    Df Residuals:                     382   BIC:                             2784.
    Df Model:                           1                                         
    Covariance Type:                  HC1                                         
    ================================================================================
                       coef    std err          z      P>|z|      [0.025      0.975]
    --------------------------------------------------------------------------------
    Intercept       -2.2833      1.248     -1.829      0.067      -4.730       0.163
    STATEr[T.NJ]     2.7500      1.338      2.056      0.040       0.128       5.372
    ==============================================================================
    Omnibus:                       33.136   Durbin-Watson:                   2.201
    Prob(Omnibus):                  0.000   Jarque-Bera (JB):               94.711
    Skew:                          -0.361   Prob(JB):                     2.71e-21
    Kurtosis:                       5.323   Cond. No.                         4.32
    ==============================================================================
    
    Notes:
    [1] Standard Errors are heteroscedasticity robust (HC1)
    

The effect of the minimum wage increasing was that employment increased by 2.75 labor units on average.


```python
# More Elaborate Regressions
ck["CHAINr"] = pd.to_numeric(ck["CHAINr"],errors="coerce") - 1
ck["CHAINr"] = pd.Categorical.from_codes(ck["CHAINr"],["Burger King", "KFC", "Roys", "Wendys"])
model2 = smf.ols("CHANGE_EMP ~ STATEr + CHAINr + CO_OWNED",data=ck).fit(cov_type="HC1")
print(model2.summary())
```

                                OLS Regression Results                            
    ==============================================================================
    Dep. Variable:             CHANGE_EMP   R-squared:                       0.029
    Model:                            OLS   Adj. R-squared:                  0.016
    Method:                 Least Squares   F-statistic:                     2.633
    Date:                Fri, 17 Apr 2026   Prob (F-statistic):             0.0234
    Time:                        16:53:05   Log-Likelihood:                -1383.4
    No. Observations:                 384   AIC:                             2779.
    Df Residuals:                     378   BIC:                             2803.
    Df Model:                           5                                         
    Covariance Type:                  HC1                                         
    ====================================================================================
                           coef    std err          z      P>|z|      [0.025      0.975]
    ------------------------------------------------------------------------------------
    Intercept           -1.8277      1.539     -1.188      0.235      -4.844       1.188
    STATEr[T.NJ]         2.7846      1.341      2.076      0.038       0.155       5.414
    CHAINr[T.KFC]        0.2408      1.047      0.230      0.818      -1.812       2.294
    CHAINr[T.Roys]      -2.5884      1.141     -2.269      0.023      -4.824      -0.353
    CHAINr[T.Wendys]    -0.1910      1.705     -0.112      0.911      -3.534       3.152
    CO_OWNED             0.3625      0.895      0.405      0.685      -1.391       2.116
    ==============================================================================
    Omnibus:                       37.181   Durbin-Watson:                   2.196
    Prob(Omnibus):                  0.000   Jarque-Bera (JB):              108.047
    Skew:                          -0.417   Prob(JB):                     3.45e-24
    Kurtosis:                       5.461   Cond. No.                         5.69
    ==============================================================================
    
    Notes:
    [1] Standard Errors are heteroscedasticity robust (HC1)
    


```python
# This is kind of a non-standard way to do DiD
idvars = ["CHAINr", "CO_OWNED", "STATEr", "SOUTHJ", "CENTRALJ", "NORTHJ", "PA1", "PA2", "SHORE", "NCALLS"]
allvars = idvars + ["EMP_TOT", "EMP_TOT2"] 
ck_long = pd.melt(ck[allvars], id_vars=idvars,
                  var_name="Period", value_name="EMP_TOTS")
ck_long["Period"] = pd.Categorical.from_codes(ck_long["Period"].replace(["EMP_TOT","EMP_TOT2"],[0,1]),["Before", "After"])
ck_long
```

    C:\Users\micha\AppData\Local\Temp\ipykernel_13152\3890433046.py:6: FutureWarning: Downcasting behavior in `replace` is deprecated and will be removed in a future version. To retain the old behavior, explicitly call `result.infer_objects(copy=False)`. To opt-in to the future behavior, set `pd.set_option('future.no_silent_downcasting', True)`
      ck_long["Period"] = pd.Categorical.from_codes(ck_long["Period"].replace(["EMP_TOT","EMP_TOT2"],[0,1]),["Before", "After"])
    




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
      <th>CHAINr</th>
      <th>CO_OWNED</th>
      <th>STATEr</th>
      <th>SOUTHJ</th>
      <th>CENTRALJ</th>
      <th>NORTHJ</th>
      <th>PA1</th>
      <th>PA2</th>
      <th>SHORE</th>
      <th>NCALLS</th>
      <th>Period</th>
      <th>EMP_TOTS</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Burger King</td>
      <td>0</td>
      <td>PA</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>Before</td>
      <td>40.50</td>
    </tr>
    <tr>
      <th>1</th>
      <td>KFC</td>
      <td>0</td>
      <td>PA</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>Before</td>
      <td>13.75</td>
    </tr>
    <tr>
      <th>2</th>
      <td>KFC</td>
      <td>1</td>
      <td>PA</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>Before</td>
      <td>8.50</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Wendys</td>
      <td>1</td>
      <td>PA</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>Before</td>
      <td>34.00</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Wendys</td>
      <td>1</td>
      <td>PA</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>Before</td>
      <td>24.00</td>
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
    </tr>
    <tr>
      <th>815</th>
      <td>KFC</td>
      <td>1</td>
      <td>NJ</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>3</td>
      <td>After</td>
      <td>23.75</td>
    </tr>
    <tr>
      <th>816</th>
      <td>KFC</td>
      <td>1</td>
      <td>NJ</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>After</td>
      <td>17.50</td>
    </tr>
    <tr>
      <th>817</th>
      <td>Roys</td>
      <td>1</td>
      <td>NJ</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>After</td>
      <td>20.50</td>
    </tr>
    <tr>
      <th>818</th>
      <td>Wendys</td>
      <td>0</td>
      <td>NJ</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>3</td>
      <td>After</td>
      <td>20.50</td>
    </tr>
    <tr>
      <th>819</th>
      <td>Wendys</td>
      <td>0</td>
      <td>NJ</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>2</td>
      <td>After</td>
      <td>25.00</td>
    </tr>
  </tbody>
</table>
<p>820 rows × 12 columns</p>
</div>




```python
# Now do the regression
model3 = smf.ols("EMP_TOTS ~ STATEr*Period + CHAINr + CO_OWNED", ck_long).fit(cov_type="HC1")
print(model3.summary())
```

                                OLS Regression Results                            
    ==============================================================================
    Dep. Variable:               EMP_TOTS   R-squared:                       0.196
    Model:                            OLS   Adj. R-squared:                  0.189
    Method:                 Least Squares   F-statistic:                     48.14
    Date:                Fri, 17 Apr 2026   Prob (F-statistic):           5.96e-57
    Time:                        17:13:19   Log-Likelihood:                -2820.4
    No. Observations:                 794   AIC:                             5657.
    Df Residuals:                     786   BIC:                             5694.
    Df Model:                           7                                         
    Covariance Type:                  HC1                                         
    ================================================================================================
                                       coef    std err          z      P>|z|      [0.025      0.975]
    ------------------------------------------------------------------------------------------------
    Intercept                       25.9512      1.341     19.354      0.000      23.323      28.579
    STATEr[T.NJ]                    -2.3766      1.273     -1.867      0.062      -4.871       0.118
    Period[T.After]                 -2.2236      1.430     -1.555      0.120      -5.026       0.579
    CHAINr[T.KFC]                  -10.4534      0.641    -16.295      0.000     -11.711      -9.196
    CHAINr[T.Roys]                  -1.6250      0.855     -1.901      0.057      -3.300       0.050
    CHAINr[T.Wendys]                -1.0637      0.972     -1.094      0.274      -2.969       0.842
    STATEr[T.NJ]:Period[T.After]     2.8451      1.575      1.806      0.071      -0.243       5.933
    CO_OWNED                        -1.1685      0.635     -1.840      0.066      -2.413       0.076
    ==============================================================================
    Omnibus:                      285.121   Durbin-Watson:                   1.972
    Prob(Omnibus):                  0.000   Jarque-Bera (JB):             1705.112
    Skew:                           1.500   Prob(JB):                         0.00
    Kurtosis:                       9.522   Cond. No.                         12.0
    ==============================================================================
    
    Notes:
    [1] Standard Errors are heteroscedasticity robust (HC1)
    
