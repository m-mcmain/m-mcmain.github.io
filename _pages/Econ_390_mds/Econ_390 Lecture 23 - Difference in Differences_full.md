---
layout: single
sitemap: false
permalink: /pages/Econ_390_SP26_L23/
title: Econ 390 Lecture 23
---

[Download Jupyter Notebook Empty](https://m-mcmain.github.io/files/Econ390SP26/Lectures/Lecture23_DifferenceinDifferences_empty.ipynb)

[Download Jupyter Notebook Completed](https://m-mcmain.github.io/files/Econ390SP26/Lectures/Lecture23_DifferenceinDifferences_full.ipynb)

# Econ 390: Lecture 23 - Difference in Differences
Today we will be going over how to visualize and conduct the econometric method called Difference in Differences (DiD). DiD at its core is very simple, there is a point in time where something changes and we want to understand what that change caused. We can't just assume everything after the change is due to the change alone, so we find a comparison group to disentangle the change and time itself. Inspiration for this lecture can be found [here](https://www.pymc.io/projects/examples/en/latest/causal_inference/difference_in_differences.html) and [here](https://aaronmams.github.io/Card-Krueger-Replication/).

![Simple Diff-in-Diff Example](https://www.pymc.io/projects/examples/en/latest/_images/8f0282bc3fafdc3f95d353ed712496d5fab4d0c009f5c0d8ecaf42f7a8626b37.png)

## Parallel Trends
Parallel trends are *paramount* to our assumption of Difference-in-Differences analysis! It must be the case that these two groups are **actually comparable**. This analysis is all about what would have happened if the treatment group was not treated. We must be confident that we can actually extract that using the information on the control group!

## Card and Krueger (1994)
One of the most famous example of DiD is from the 1994 American Economic Review (AER) paper "Minimum Wages and Employment: A Case Study of the Fast-Food Industry in New Jersey and Pennsylvania" by David Card and Alan Krueger (you can find the paper and data on Card's website [here](https://davidcard.berkeley.edu/data_sets)).


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
ck = pd.read_csv(econ390path + "card_krueger_public.dat", sep="\s+", header= None, names = names)
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
ck["EMP_TOT"] = pd.to_numeric(ck["EMPFT"], errors="coerce") + pd.to_numeric(ck["EMPPT"],errors="coerce")*0.5 + pd.to_numeric(ck["NMGRS"],errors="coerce")
ck["EMP_TOT2"] = pd.to_numeric(ck["EMPFT2"], errors="coerce") + pd.to_numeric(ck["EMPPT2"],errors="coerce")*0.5 + pd.to_numeric(ck["NMGRS2"],errors="coerce")
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
ck["STATEr"] = pd.Categorical.from_codes(ck["STATEr"], ["PA", "NJ"])
```

## Wage Visualizations


```python
# Basic Visualization of Wages
plt.hist(ck["WAGE_ST"][ck["STATEr"]=="NJ"], density=True, alpha=0.5, label="NJ")
plt.hist(ck["WAGE_ST"][ck["STATEr"]=="PA"], density=True, alpha=0.5, label="PA")
plt.legend(loc='upper right')
plt.show()
```


    
![png](output_9_0.png)
    



```python
# Force the Same Bins
count, hist1_bins, patches = plt.hist(ck["WAGE_ST"][ck["STATEr"]=="NJ"], density=True, alpha=0.5, label="NJ")
plt.hist(ck["WAGE_ST"][ck["STATEr"]=="PA"], bins=hist1_bins, density=True, alpha=0.5, label="PA")
plt.legend(loc='upper right')
plt.show()
```


    
![png](output_10_0.png)
    



```python
# Second Period same bins
count, hist1_bins, patches = plt.hist(ck["WAGE_ST2"][ck["STATEr"]=="NJ"], density=True, alpha=0.5, label="NJ")
plt.hist(ck["WAGE_ST2"][ck["STATEr"]=="PA"], bins=hist1_bins, density=True, alpha=0.5, label="PA")
plt.legend(loc='upper right')
plt.show()
```


    
![png](output_11_0.png)
    



```python
# Good reason to not have the same bins!
plt.hist(ck["WAGE_ST2"][ck["STATEr"]=="NJ"], density=True, alpha=0.5, label="NJ")
plt.hist(ck["WAGE_ST2"][ck["STATEr"]=="PA"], density=True, alpha=0.5, label="PA")
plt.legend(loc='upper right')
plt.show()
```


    
![png](output_12_0.png)
    



```python
# Compare within NJ before and after
plt.hist(ck["WAGE_ST"][ck["STATEr"]=="NJ"], density=True, alpha=0.5, label="Pre")
plt.hist(ck["WAGE_ST2"][ck["STATEr"]=="NJ"], density=True, alpha=0.5, label="Post")
plt.legend(loc='upper right')
plt.show()
```


    
![png](output_13_0.png)
    



```python
# What happens in PA?
plt.hist(ck["WAGE_ST"][ck["STATEr"]=="PA"], density=True, alpha=0.5, label="Pre")
plt.hist(ck["WAGE_ST2"][ck["STATEr"]=="PA"], density=True, alpha=0.5, label="Post")
plt.legend(loc='upper right')
plt.show()
```


    
![png](output_14_0.png)
    



```python
# Classic DiD Plot on Wage:
wage_before = ck[["STATEr","WAGE_ST"]].groupby("STATEr").mean()
wage_after = ck[["STATEr","WAGE_ST2"]].groupby("STATEr").mean()
avg_wage_df = pd.DataFrame({"Time":[0,1],
                            "Wage_NJ":[wage_before.iloc[1,0], wage_after.iloc[1,0]],
                            "Wage_PA":[wage_before.iloc[0,0], wage_after.iloc[0,0]]})
print(avg_wage_df)                            
```

       Time   Wage_NJ   Wage_PA
    0     0  4.612134  4.630132
    1     1  5.080849  4.617465
    

    C:\Users\micha\AppData\Local\Temp\ipykernel_19640\3819204349.py:2: FutureWarning: The default of observed=False is deprecated and will be changed to True in a future version of pandas. Pass observed=False to retain current behavior or observed=True to adopt the future default and silence this warning.
      wage_before = ck[["STATEr","WAGE_ST"]].groupby("STATEr").mean()
    C:\Users\micha\AppData\Local\Temp\ipykernel_19640\3819204349.py:3: FutureWarning: The default of observed=False is deprecated and will be changed to True in a future version of pandas. Pass observed=False to retain current behavior or observed=True to adopt the future default and silence this warning.
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
count, hist1_bins, patches = plt.hist(ck["EMP_TOT"][ck["STATEr"]=="NJ"], density=True, alpha=0.5, label="Before")
plt.hist(ck["EMP_TOT2"][ck["STATEr"]=="NJ"], bins=hist1_bins, density=True, alpha=0.5, label="After")
plt.legend(loc='upper right')
plt.show()
```


    
![png](output_18_0.png)
    



```python
# Employment Across Time in PA
count, hist1_bins, patches = plt.hist(ck["EMP_TOT"][ck["STATEr"]=="PA"], density=True, alpha=0.5, label="Before")
plt.hist(ck["EMP_TOT2"][ck["STATEr"]=="PA"], bins=hist1_bins, density=True, alpha=0.5, label="After")
plt.legend(loc='upper right')
plt.show()
```


    
![png](output_19_0.png)
    



```python
# Classic DiD Plot on Employment:
# Classic DiD Plot on Wage:
EMP_before = ck[["STATEr","EMP_TOT"]].groupby("STATEr").mean()
EMP_after = ck[["STATEr","EMP_TOT2"]].groupby("STATEr").mean()
avg_EMP_df = pd.DataFrame({"Time":[0,1],
                            "EMP_NJ":[EMP_before.iloc[1,0], EMP_after.iloc[1,0]],
                            "EMP_PA":[EMP_before.iloc[0,0], EMP_after.iloc[0,0]]})
print(avg_EMP_df)                            
```

       Time     EMP_NJ     EMP_PA
    0     0  20.439408  23.331169
    1     1  21.027429  21.165584
    

    C:\Users\micha\AppData\Local\Temp\ipykernel_19640\3758376572.py:3: FutureWarning: The default of observed=False is deprecated and will be changed to True in a future version of pandas. Pass observed=False to retain current behavior or observed=True to adopt the future default and silence this warning.
      EMP_before = ck[["STATEr","EMP_TOT"]].groupby("STATEr").mean()
    C:\Users\micha\AppData\Local\Temp\ipykernel_19640\3758376572.py:4: FutureWarning: The default of observed=False is deprecated and will be changed to True in a future version of pandas. Pass observed=False to retain current behavior or observed=True to adopt the future default and silence this warning.
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


    
![png](output_21_0.png)
    


## DiD Regression


```python
# Basic Regressions
ck["CHANGE_EMP"] =ck["EMP_TOT2"] - ck["EMP_TOT"]
model1 = smf.ols("CHANGE_EMP ~ STATEr",data=ck).fit(cov_type="HC1")
print(model1.summary())
```

                                OLS Regression Results                            
    ==============================================================================
    Dep. Variable:             CHANGE_EMP   R-squared:                       0.015
    Model:                            OLS   Adj. R-squared:                  0.012
    Method:                 Least Squares   F-statistic:                     4.226
    Date:                Tue, 21 Apr 2026   Prob (F-statistic):             0.0405
    Time:                        15:34:40   Log-Likelihood:                -1386.2
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
    

The effect of the minimum wage increasing was that employment in New Jersey increased by 2.75 labor units on average **relative** to Pennsylvania


```python
# More Elaborate Regressions
ck["CHAINr"] = pd.to_numeric(ck["CHAINr"],errors="coerce")-1
ck["CHAINr"] = pd.Categorical.from_codes(ck["CHAINr"],["Burger King", "KFC", "Roys", "Wendys"])
model2 = smf.ols("CHANGE_EMP ~ STATEr + CHAINr",data=ck).fit(cov_type="HC1")
print(model2.summary())
```

                                OLS Regression Results                            
    ==============================================================================
    Dep. Variable:             CHANGE_EMP   R-squared:                       0.029
    Model:                            OLS   Adj. R-squared:                  0.018
    Method:                 Least Squares   F-statistic:                     3.290
    Date:                Tue, 21 Apr 2026   Prob (F-statistic):             0.0114
    Time:                        15:34:45   Log-Likelihood:                -1383.5
    No. Observations:                 384   AIC:                             2777.
    Df Residuals:                     379   BIC:                             2797.
    Df Model:                           4                                         
    Covariance Type:                  HC1                                         
    ====================================================================================
                           coef    std err          z      P>|z|      [0.025      0.975]
    ------------------------------------------------------------------------------------
    Intercept           -1.7659      1.501     -1.177      0.239      -4.707       1.176
    STATEr[T.NJ]         2.7757      1.337      2.077      0.038       0.156       5.395
    CHAINr[T.KFC]        0.3518      1.058      0.332      0.740      -1.723       2.426
    CHAINr[T.Roys]      -2.3960      1.096     -2.186      0.029      -4.545      -0.248
    CHAINr[T.Wendys]    -0.1764      1.701     -0.104      0.917      -3.511       3.158
    ==============================================================================
    Omnibus:                       37.536   Durbin-Watson:                   2.197
    Prob(Omnibus):                  0.000   Jarque-Bera (JB):              108.883
    Skew:                          -0.422   Prob(JB):                     2.27e-24
    Kurtosis:                       5.468   Cond. No.                         5.34
    ==============================================================================
    
    Notes:
    [1] Standard Errors are heteroscedasticity robust (HC1)
    


```python
# This is kind of a non-standard way to do DiD
idvars = ["CHAINr", "STATEr", "CO_OWNED", "SOUTHJ", "CENTRALJ","NORTHJ","PA1","PA2","SHORE","NCALLS"]
allvars = idvars + ["EMP_TOT", "EMP_TOT2"]
ck_long = pd.melt(ck[allvars], id_vars = idvars,
                  var_name="Period", value_name = "EMP_TOTS")
ck_long["Period"] = pd.Categorical.from_codes(ck_long["Period"].replace(["EMP_TOT","EMP_TOT2"],[0,1]),["Before","After"])
ck_long
```

    C:\Users\micha\AppData\Local\Temp\ipykernel_19640\2052397396.py:6: FutureWarning: Downcasting behavior in `replace` is deprecated and will be removed in a future version. To retain the old behavior, explicitly call `result.infer_objects(copy=False)`. To opt-in to the future behavior, set `pd.set_option('future.no_silent_downcasting', True)`
      ck_long["Period"] = pd.Categorical.from_codes(ck_long["Period"].replace(["EMP_TOT","EMP_TOT2"],[0,1]),["Before","After"])
    




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
      <th>STATEr</th>
      <th>CO_OWNED</th>
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
      <td>PA</td>
      <td>0</td>
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
      <td>PA</td>
      <td>0</td>
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
      <td>PA</td>
      <td>1</td>
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
      <td>PA</td>
      <td>1</td>
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
      <td>PA</td>
      <td>1</td>
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
      <td>NJ</td>
      <td>1</td>
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
      <td>NJ</td>
      <td>1</td>
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
      <td>NJ</td>
      <td>1</td>
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
      <td>NJ</td>
      <td>0</td>
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
      <td>NJ</td>
      <td>0</td>
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
model3 = smf.ols("EMP_TOTS ~ STATEr*Period",ck_long).fit(cov_type="HC1")
print(model3.summary())
```

                                OLS Regression Results                            
    ==============================================================================
    Dep. Variable:               EMP_TOTS   R-squared:                       0.007
    Model:                            OLS   Adj. R-squared:                  0.004
    Method:                 Least Squares   F-statistic:                     1.404
    Date:                Tue, 21 Apr 2026   Prob (F-statistic):              0.240
    Time:                        15:40:43   Log-Likelihood:                -2904.2
    No. Observations:                 794   AIC:                             5816.
    Df Residuals:                     790   BIC:                             5835.
    Df Model:                           3                                         
    Covariance Type:                  HC1                                         
    ================================================================================================
                                       coef    std err          z      P>|z|      [0.025      0.975]
    ------------------------------------------------------------------------------------------------
    Intercept                       23.3312      1.346     17.337      0.000      20.694      25.969
    STATEr[T.NJ]                    -2.8918      1.439     -2.010      0.044      -5.712      -0.072
    Period[T.After]                 -2.1656      1.641     -1.320      0.187      -5.382       1.051
    STATEr[T.NJ]:Period[T.After]     2.7536      1.795      1.534      0.125      -0.765       6.273
    ==============================================================================
    Omnibus:                      218.742   Durbin-Watson:                   1.840
    Prob(Omnibus):                  0.000   Jarque-Bera (JB):              804.488
    Skew:                           1.268   Prob(JB):                    2.03e-175
    Kurtosis:                       7.229   Cond. No.                         11.3
    ==============================================================================
    
    Notes:
    [1] Standard Errors are heteroscedasticity robust (HC1)
    
