---
layout: single
sitemap: false
permalink: /pages/Econ_390_SP26_L22/
title: Econ 390 Lecture 22
---

[Download Jupyter Notebook Empty](https://m-mcmain.github.io/files/Econ390SP26/Lectures/Lecture22_CategoricalVariables_empty.ipynb)

[Download Jupyter Notebook Completed](https://m-mcmain.github.io/files/Econ390SP26/Lectures/Lecture22_CategoricalVariables_full.ipynb)

# Econ 390 - Lecture 22: Categorical Variables
Today we will be going over category type variables and use them to do comparisons across groups. You can find readings in [McKinney](https://wesmckinney.com/book/data-cleaning#pandas-categorical) and [Turrell](https://aeturrell.github.io/coding-for-economists/data-categorical.html#categorical-data)

![image](https://m-mcmain.github.io/files/Econ390SP26/announcements/CROWE_Neal_4-16-26.jpg)

## Course Evaluations Open Tomorrow
You should be getting an email tomorrow about Course Evaluations! I would **really** appreciate if you could take 5-10 minutes filling it out honestly and constructively so I can improve the course for the next generation of *Intro to Coding for Economists* Students!

You should be able to find the survey starting tomorrow morning [here](https://heliocampusac.wisc.edu/index.cfm/page/AefisDashboard.home?action=openSurveyForm) or you can keep an eye out for emails from `learningassessment@provost.wisc.edu`! The survey will be open until 11:59pm on Friday May 1st.


```python
import pandas as pd
auto = pd.read_csv("https://www.statlearning.com/s/Auto.csv")
auto
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
      <th>mpg</th>
      <th>cylinders</th>
      <th>displacement</th>
      <th>horsepower</th>
      <th>weight</th>
      <th>acceleration</th>
      <th>year</th>
      <th>origin</th>
      <th>name</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>18.0</td>
      <td>8</td>
      <td>307.0</td>
      <td>130</td>
      <td>3504</td>
      <td>12.0</td>
      <td>70</td>
      <td>1</td>
      <td>chevrolet chevelle malibu</td>
    </tr>
    <tr>
      <th>1</th>
      <td>15.0</td>
      <td>8</td>
      <td>350.0</td>
      <td>165</td>
      <td>3693</td>
      <td>11.5</td>
      <td>70</td>
      <td>1</td>
      <td>buick skylark 320</td>
    </tr>
    <tr>
      <th>2</th>
      <td>18.0</td>
      <td>8</td>
      <td>318.0</td>
      <td>150</td>
      <td>3436</td>
      <td>11.0</td>
      <td>70</td>
      <td>1</td>
      <td>plymouth satellite</td>
    </tr>
    <tr>
      <th>3</th>
      <td>16.0</td>
      <td>8</td>
      <td>304.0</td>
      <td>150</td>
      <td>3433</td>
      <td>12.0</td>
      <td>70</td>
      <td>1</td>
      <td>amc rebel sst</td>
    </tr>
    <tr>
      <th>4</th>
      <td>17.0</td>
      <td>8</td>
      <td>302.0</td>
      <td>140</td>
      <td>3449</td>
      <td>10.5</td>
      <td>70</td>
      <td>1</td>
      <td>ford torino</td>
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
    </tr>
    <tr>
      <th>392</th>
      <td>27.0</td>
      <td>4</td>
      <td>140.0</td>
      <td>86</td>
      <td>2790</td>
      <td>15.6</td>
      <td>82</td>
      <td>1</td>
      <td>ford mustang gl</td>
    </tr>
    <tr>
      <th>393</th>
      <td>44.0</td>
      <td>4</td>
      <td>97.0</td>
      <td>52</td>
      <td>2130</td>
      <td>24.6</td>
      <td>82</td>
      <td>2</td>
      <td>vw pickup</td>
    </tr>
    <tr>
      <th>394</th>
      <td>32.0</td>
      <td>4</td>
      <td>135.0</td>
      <td>84</td>
      <td>2295</td>
      <td>11.6</td>
      <td>82</td>
      <td>1</td>
      <td>dodge rampage</td>
    </tr>
    <tr>
      <th>395</th>
      <td>28.0</td>
      <td>4</td>
      <td>120.0</td>
      <td>79</td>
      <td>2625</td>
      <td>18.6</td>
      <td>82</td>
      <td>1</td>
      <td>ford ranger</td>
    </tr>
    <tr>
      <th>396</th>
      <td>31.0</td>
      <td>4</td>
      <td>119.0</td>
      <td>82</td>
      <td>2720</td>
      <td>19.4</td>
      <td>82</td>
      <td>1</td>
      <td>chevy s-10</td>
    </tr>
  </tbody>
</table>
<p>397 rows × 9 columns</p>
</div>



## Categorical Data


```python
# Check out origin
auto["origin"].value_counts()
```




    origin
    1    248
    3     79
    2     70
    Name: count, dtype: int64




```python
# Create a new variable
auto["foreign"] = (auto["origin"] != 1).astype("int")
auto
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
      <th>mpg</th>
      <th>cylinders</th>
      <th>displacement</th>
      <th>horsepower</th>
      <th>weight</th>
      <th>acceleration</th>
      <th>year</th>
      <th>origin</th>
      <th>name</th>
      <th>foreign</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>18.0</td>
      <td>8</td>
      <td>307.0</td>
      <td>130</td>
      <td>3504</td>
      <td>12.0</td>
      <td>70</td>
      <td>1</td>
      <td>chevrolet chevelle malibu</td>
      <td>0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>15.0</td>
      <td>8</td>
      <td>350.0</td>
      <td>165</td>
      <td>3693</td>
      <td>11.5</td>
      <td>70</td>
      <td>1</td>
      <td>buick skylark 320</td>
      <td>0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>18.0</td>
      <td>8</td>
      <td>318.0</td>
      <td>150</td>
      <td>3436</td>
      <td>11.0</td>
      <td>70</td>
      <td>1</td>
      <td>plymouth satellite</td>
      <td>0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>16.0</td>
      <td>8</td>
      <td>304.0</td>
      <td>150</td>
      <td>3433</td>
      <td>12.0</td>
      <td>70</td>
      <td>1</td>
      <td>amc rebel sst</td>
      <td>0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>17.0</td>
      <td>8</td>
      <td>302.0</td>
      <td>140</td>
      <td>3449</td>
      <td>10.5</td>
      <td>70</td>
      <td>1</td>
      <td>ford torino</td>
      <td>0</td>
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
    </tr>
    <tr>
      <th>392</th>
      <td>27.0</td>
      <td>4</td>
      <td>140.0</td>
      <td>86</td>
      <td>2790</td>
      <td>15.6</td>
      <td>82</td>
      <td>1</td>
      <td>ford mustang gl</td>
      <td>0</td>
    </tr>
    <tr>
      <th>393</th>
      <td>44.0</td>
      <td>4</td>
      <td>97.0</td>
      <td>52</td>
      <td>2130</td>
      <td>24.6</td>
      <td>82</td>
      <td>2</td>
      <td>vw pickup</td>
      <td>1</td>
    </tr>
    <tr>
      <th>394</th>
      <td>32.0</td>
      <td>4</td>
      <td>135.0</td>
      <td>84</td>
      <td>2295</td>
      <td>11.6</td>
      <td>82</td>
      <td>1</td>
      <td>dodge rampage</td>
      <td>0</td>
    </tr>
    <tr>
      <th>395</th>
      <td>28.0</td>
      <td>4</td>
      <td>120.0</td>
      <td>79</td>
      <td>2625</td>
      <td>18.6</td>
      <td>82</td>
      <td>1</td>
      <td>ford ranger</td>
      <td>0</td>
    </tr>
    <tr>
      <th>396</th>
      <td>31.0</td>
      <td>4</td>
      <td>119.0</td>
      <td>82</td>
      <td>2720</td>
      <td>19.4</td>
      <td>82</td>
      <td>1</td>
      <td>chevy s-10</td>
      <td>0</td>
    </tr>
  </tbody>
</table>
<p>397 rows × 10 columns</p>
</div>




```python
# pd.Categorical
pd.Categorical.from_codes(auto["foreign"], ["Domestic", "Foreign"])
```




    ['Domestic', 'Domestic', 'Domestic', 'Domestic', 'Domestic', ..., 'Domestic', 'Foreign', 'Domestic', 'Domestic', 'Domestic']
    Length: 397
    Categories (2, object): ['Domestic', 'Foreign']




```python
# Convert the variable
auto["foreign"] = pd.Categorical.from_codes(auto["foreign"], ["Domestic", "Foreign"])
```


```python
# cat method
auto["foreign"].cat
```




    <pandas.core.arrays.categorical.CategoricalAccessor object at 0x000002AF1B1BE270>




```python
# Categories
auto["foreign"].cat.categories
```




    Index(['Domestic', 'Foreign'], dtype='object')




```python
# Codes
auto["foreign"].cat.codes
```




    0      0
    1      0
    2      0
    3      0
    4      0
          ..
    392    0
    393    1
    394    0
    395    0
    396    0
    Length: 397, dtype: int8




```python
# Alternative Method
category_mapping = {1:"Domestic",2:"Foreign",3:"Foreign"}
auto["foreign_alt"] = auto["origin"].map(category_mapping).astype("category")
auto
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
      <th>mpg</th>
      <th>cylinders</th>
      <th>displacement</th>
      <th>horsepower</th>
      <th>weight</th>
      <th>acceleration</th>
      <th>year</th>
      <th>origin</th>
      <th>name</th>
      <th>foreign</th>
      <th>foreign_alt</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>18.0</td>
      <td>8</td>
      <td>307.0</td>
      <td>130</td>
      <td>3504</td>
      <td>12.0</td>
      <td>70</td>
      <td>1</td>
      <td>chevrolet chevelle malibu</td>
      <td>Domestic</td>
      <td>Domestic</td>
    </tr>
    <tr>
      <th>1</th>
      <td>15.0</td>
      <td>8</td>
      <td>350.0</td>
      <td>165</td>
      <td>3693</td>
      <td>11.5</td>
      <td>70</td>
      <td>1</td>
      <td>buick skylark 320</td>
      <td>Domestic</td>
      <td>Domestic</td>
    </tr>
    <tr>
      <th>2</th>
      <td>18.0</td>
      <td>8</td>
      <td>318.0</td>
      <td>150</td>
      <td>3436</td>
      <td>11.0</td>
      <td>70</td>
      <td>1</td>
      <td>plymouth satellite</td>
      <td>Domestic</td>
      <td>Domestic</td>
    </tr>
    <tr>
      <th>3</th>
      <td>16.0</td>
      <td>8</td>
      <td>304.0</td>
      <td>150</td>
      <td>3433</td>
      <td>12.0</td>
      <td>70</td>
      <td>1</td>
      <td>amc rebel sst</td>
      <td>Domestic</td>
      <td>Domestic</td>
    </tr>
    <tr>
      <th>4</th>
      <td>17.0</td>
      <td>8</td>
      <td>302.0</td>
      <td>140</td>
      <td>3449</td>
      <td>10.5</td>
      <td>70</td>
      <td>1</td>
      <td>ford torino</td>
      <td>Domestic</td>
      <td>Domestic</td>
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
    </tr>
    <tr>
      <th>392</th>
      <td>27.0</td>
      <td>4</td>
      <td>140.0</td>
      <td>86</td>
      <td>2790</td>
      <td>15.6</td>
      <td>82</td>
      <td>1</td>
      <td>ford mustang gl</td>
      <td>Domestic</td>
      <td>Domestic</td>
    </tr>
    <tr>
      <th>393</th>
      <td>44.0</td>
      <td>4</td>
      <td>97.0</td>
      <td>52</td>
      <td>2130</td>
      <td>24.6</td>
      <td>82</td>
      <td>2</td>
      <td>vw pickup</td>
      <td>Foreign</td>
      <td>Foreign</td>
    </tr>
    <tr>
      <th>394</th>
      <td>32.0</td>
      <td>4</td>
      <td>135.0</td>
      <td>84</td>
      <td>2295</td>
      <td>11.6</td>
      <td>82</td>
      <td>1</td>
      <td>dodge rampage</td>
      <td>Domestic</td>
      <td>Domestic</td>
    </tr>
    <tr>
      <th>395</th>
      <td>28.0</td>
      <td>4</td>
      <td>120.0</td>
      <td>79</td>
      <td>2625</td>
      <td>18.6</td>
      <td>82</td>
      <td>1</td>
      <td>ford ranger</td>
      <td>Domestic</td>
      <td>Domestic</td>
    </tr>
    <tr>
      <th>396</th>
      <td>31.0</td>
      <td>4</td>
      <td>119.0</td>
      <td>82</td>
      <td>2720</td>
      <td>19.4</td>
      <td>82</td>
      <td>1</td>
      <td>chevy s-10</td>
      <td>Domestic</td>
      <td>Domestic</td>
    </tr>
  </tbody>
</table>
<p>397 rows × 11 columns</p>
</div>




```python
# Aggregation
auto.groupby("foreign").mean(numeric_only=True)
```

    C:\Users\micha\AppData\Local\Temp\ipykernel_10968\2512806637.py:2: FutureWarning: The default of observed=False is deprecated and will be changed to True in a future version of pandas. Pass observed=False to retain current behavior or observed=True to adopt the future default and silence this warning.
      auto.groupby("foreign").mean(numeric_only=True)
    




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
      <th>mpg</th>
      <th>cylinders</th>
      <th>displacement</th>
      <th>weight</th>
      <th>acceleration</th>
      <th>year</th>
      <th>origin</th>
    </tr>
    <tr>
      <th>foreign</th>
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
      <th>Domestic</th>
      <td>20.071774</td>
      <td>6.258065</td>
      <td>246.284274</td>
      <td>3363.250000</td>
      <td>15.011694</td>
      <td>75.584677</td>
      <td>1.000000</td>
    </tr>
    <tr>
      <th>Foreign</th>
      <td>29.248322</td>
      <td>4.127517</td>
      <td>105.731544</td>
      <td>2316.161074</td>
      <td>16.461074</td>
      <td>76.677852</td>
      <td>2.530201</td>
    </tr>
  </tbody>
</table>
</div>



## Regression Models with Categories


```python
# Import seaborn and smf
import seaborn as sns
import statsmodels.formula.api as smf
```


```python
# lmplot with weight and mpg
sns.lmplot(x="weight",y="mpg",data=auto);
```


    
![png](output_16_0.png)
    



```python
# lmplot with customization
sns.lmplot(x="weight",y="mpg",data=auto);
```


    
![png](output_17_0.png)
    



```python
# lmplot with customization
sns.lmplot(x="weight",y="mpg", hue="origin", data=auto, scatter_kws={"alpha":0.2,"s":5});
```


    
![png](output_18_0.png)
    



```python
# model using smf
model1 = smf.ols("mpg ~ weight", data=auto).fit(cov_type="HC1")
print(model1.summary())
```

                                OLS Regression Results                            
    ==============================================================================
    Dep. Variable:                    mpg   R-squared:                       0.692
    Model:                            OLS   Adj. R-squared:                  0.691
    Method:                 Least Squares   F-statistic:                     1072.
    Date:                Thu, 16 Apr 2026   Prob (F-statistic):          1.27e-114
    Time:                        15:01:33   Log-Likelihood:                -1146.0
    No. Observations:                 397   AIC:                             2296.
    Df Residuals:                     395   BIC:                             2304.
    Df Model:                           1                                         
    Covariance Type:                  HC1                                         
    ==============================================================================
                     coef    std err          z      P>|z|      [0.025      0.975]
    ------------------------------------------------------------------------------
    Intercept     46.3174      0.823     56.269      0.000      44.704      47.931
    weight        -0.0077      0.000    -32.748      0.000      -0.008      -0.007
    ==============================================================================
    Omnibus:                       40.133   Durbin-Watson:                   0.797
    Prob(Omnibus):                  0.000   Jarque-Bera (JB):               56.057
    Skew:                           0.712   Prob(JB):                     6.72e-13
    Kurtosis:                       4.166   Cond. No.                     1.13e+04
    ==============================================================================
    
    Notes:
    [1] Standard Errors are heteroscedasticity robust (HC1)
    [2] The condition number is large, 1.13e+04. This might indicate that there are
    strong multicollinearity or other numerical problems.
    


```python
# Comparing across models
from statsmodels.iolib.summary2 import summary_col
model1 = smf.ols("mpg ~ weight", data=auto[auto["foreign"]=="Domestic"]).fit(cov_type="HC1")
model2 = smf.ols("mpg ~ weight", data=auto[auto["foreign"]=="Foreign"]).fit(cov_type="HC1")
print(summary_col([model1,model2],stars=True,float_format="%0.3f",
                  model_names=["Domestic","Foreign"]))
```

    
    ==================================
                    Domestic  Foreign 
    ----------------------------------
    Intercept      42.985*** 49.184***
                   (1.121)   (2.342)  
    weight         -0.007*** -0.009***
                   (0.000)   (0.001)  
    R-squared      0.715     0.309    
    R-squared Adj. 0.714     0.304    
    ==================================
    Standard errors in parentheses.
    * p<.1, ** p<.05, ***p<.01
    


```python
# Categorical in the Model
model3 = smf.ols("mpg ~ weight + foreign + weight:foreign", data=auto).fit(cov_type="HC1")
print(model3.summary())
```

                                OLS Regression Results                            
    ==============================================================================
    Dep. Variable:                    mpg   R-squared:                       0.703
    Model:                            OLS   Adj. R-squared:                  0.700
    Method:                 Least Squares   F-statistic:                     399.5
    Date:                Thu, 16 Apr 2026   Prob (F-statistic):          5.95e-119
    Time:                        15:18:45   Log-Likelihood:                -1139.0
    No. Observations:                 397   AIC:                             2286.
    Df Residuals:                     393   BIC:                             2302.
    Df Model:                           3                                         
    Covariance Type:                  HC1                                         
    =============================================================================================
                                    coef    std err          z      P>|z|      [0.025      0.975]
    ---------------------------------------------------------------------------------------------
    Intercept                    42.9846      1.122     38.310      0.000      40.786      45.184
    foreign[T.Foreign]            6.1996      2.593      2.391      0.017       1.117      11.282
    weight                       -0.0068      0.000    -22.983      0.000      -0.007      -0.006
    weight:foreign[T.Foreign]    -0.0018      0.001     -1.729      0.084      -0.004       0.000
    ==============================================================================
    Omnibus:                       35.670   Durbin-Watson:                   0.787
    Prob(Omnibus):                  0.000   Jarque-Bera (JB):               47.765
    Skew:                           0.667   Prob(JB):                     4.25e-11
    Kurtosis:                       4.053   Cond. No.                     3.54e+04
    ==============================================================================
    
    Notes:
    [1] Standard Errors are heteroscedasticity robust (HC1)
    [2] The condition number is large, 3.54e+04. This might indicate that there are
    strong multicollinearity or other numerical problems.
    


```python
# Alternate way of typing it
model3 = smf.ols("mpg ~ weight*origin", data=auto).fit(cov_type="HC1")
print(model3.summary())
```

                                OLS Regression Results                            
    ==============================================================================
    Dep. Variable:                    mpg   R-squared:                       0.705
    Model:                            OLS   Adj. R-squared:                  0.703
    Method:                 Least Squares   F-statistic:                     397.2
    Date:                Thu, 16 Apr 2026   Prob (F-statistic):          1.41e-118
    Time:                        15:20:17   Log-Likelihood:                -1137.4
    No. Observations:                 397   AIC:                             2283.
    Df Residuals:                     393   BIC:                             2299.
    Df Model:                           3                                         
    Covariance Type:                  HC1                                         
    =================================================================================
                        coef    std err          z      P>|z|      [0.025      0.975]
    ---------------------------------------------------------------------------------
    Intercept        38.7749      2.227     17.415      0.000      34.411      43.139
    weight           -0.0055      0.001     -6.946      0.000      -0.007      -0.004
    origin            4.2925      1.606      2.672      0.008       1.144       7.441
    weight:origin    -0.0013      0.001     -1.953      0.051      -0.003    4.99e-06
    ==============================================================================
    Omnibus:                       43.600   Durbin-Watson:                   0.823
    Prob(Omnibus):                  0.000   Jarque-Bera (JB):               65.160
    Skew:                           0.730   Prob(JB):                     7.09e-15
    Kurtosis:                       4.344   Cond. No.                     6.53e+04
    ==============================================================================
    
    Notes:
    [1] Standard Errors are heteroscedasticity robust (HC1)
    [2] The condition number is large, 6.53e+04. This might indicate that there are
    strong multicollinearity or other numerical problems.
    

## Binning Data
We did a little bit of this all the way back in [Lecture 12](https://m-mcmain.github.io/pages/Econ_390_SP26_L12/)!


```python
# Distribution of years
auto["year"].value_counts().sort_index()
```




    year
    70    29
    71    28
    72    28
    73    40
    74    27
    75    30
    76    34
    77    28
    78    36
    79    29
    80    29
    81    29
    82    30
    Name: count, dtype: int64




```python
# Means across years
auto[["year","mpg"]].groupby("year").mean()
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
      <th>mpg</th>
    </tr>
    <tr>
      <th>year</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>70</th>
      <td>17.689655</td>
    </tr>
    <tr>
      <th>71</th>
      <td>21.250000</td>
    </tr>
    <tr>
      <th>72</th>
      <td>18.714286</td>
    </tr>
    <tr>
      <th>73</th>
      <td>17.100000</td>
    </tr>
    <tr>
      <th>74</th>
      <td>22.703704</td>
    </tr>
    <tr>
      <th>75</th>
      <td>20.266667</td>
    </tr>
    <tr>
      <th>76</th>
      <td>21.573529</td>
    </tr>
    <tr>
      <th>77</th>
      <td>23.375000</td>
    </tr>
    <tr>
      <th>78</th>
      <td>24.061111</td>
    </tr>
    <tr>
      <th>79</th>
      <td>25.093103</td>
    </tr>
    <tr>
      <th>80</th>
      <td>33.696552</td>
    </tr>
    <tr>
      <th>81</th>
      <td>30.334483</td>
    </tr>
    <tr>
      <th>82</th>
      <td>32.000000</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Using cut
auto["year_bin"] = pd.cut(auto["year"], bins = [69, 73, 77, 82], right=True, 
                          labels = ["Early 70s", "Mid 70s", "Late 70s-Early 80s"])
auto
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
      <th>mpg</th>
      <th>cylinders</th>
      <th>displacement</th>
      <th>horsepower</th>
      <th>weight</th>
      <th>acceleration</th>
      <th>year</th>
      <th>origin</th>
      <th>name</th>
      <th>foreign</th>
      <th>foreign_alt</th>
      <th>year_bin</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>18.0</td>
      <td>8</td>
      <td>307.0</td>
      <td>130</td>
      <td>3504</td>
      <td>12.0</td>
      <td>70</td>
      <td>1</td>
      <td>chevrolet chevelle malibu</td>
      <td>Domestic</td>
      <td>Domestic</td>
      <td>Early 70s</td>
    </tr>
    <tr>
      <th>1</th>
      <td>15.0</td>
      <td>8</td>
      <td>350.0</td>
      <td>165</td>
      <td>3693</td>
      <td>11.5</td>
      <td>70</td>
      <td>1</td>
      <td>buick skylark 320</td>
      <td>Domestic</td>
      <td>Domestic</td>
      <td>Early 70s</td>
    </tr>
    <tr>
      <th>2</th>
      <td>18.0</td>
      <td>8</td>
      <td>318.0</td>
      <td>150</td>
      <td>3436</td>
      <td>11.0</td>
      <td>70</td>
      <td>1</td>
      <td>plymouth satellite</td>
      <td>Domestic</td>
      <td>Domestic</td>
      <td>Early 70s</td>
    </tr>
    <tr>
      <th>3</th>
      <td>16.0</td>
      <td>8</td>
      <td>304.0</td>
      <td>150</td>
      <td>3433</td>
      <td>12.0</td>
      <td>70</td>
      <td>1</td>
      <td>amc rebel sst</td>
      <td>Domestic</td>
      <td>Domestic</td>
      <td>Early 70s</td>
    </tr>
    <tr>
      <th>4</th>
      <td>17.0</td>
      <td>8</td>
      <td>302.0</td>
      <td>140</td>
      <td>3449</td>
      <td>10.5</td>
      <td>70</td>
      <td>1</td>
      <td>ford torino</td>
      <td>Domestic</td>
      <td>Domestic</td>
      <td>Early 70s</td>
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
      <th>392</th>
      <td>27.0</td>
      <td>4</td>
      <td>140.0</td>
      <td>86</td>
      <td>2790</td>
      <td>15.6</td>
      <td>82</td>
      <td>1</td>
      <td>ford mustang gl</td>
      <td>Domestic</td>
      <td>Domestic</td>
      <td>Late 70s-Early 80s</td>
    </tr>
    <tr>
      <th>393</th>
      <td>44.0</td>
      <td>4</td>
      <td>97.0</td>
      <td>52</td>
      <td>2130</td>
      <td>24.6</td>
      <td>82</td>
      <td>2</td>
      <td>vw pickup</td>
      <td>Foreign</td>
      <td>Foreign</td>
      <td>Late 70s-Early 80s</td>
    </tr>
    <tr>
      <th>394</th>
      <td>32.0</td>
      <td>4</td>
      <td>135.0</td>
      <td>84</td>
      <td>2295</td>
      <td>11.6</td>
      <td>82</td>
      <td>1</td>
      <td>dodge rampage</td>
      <td>Domestic</td>
      <td>Domestic</td>
      <td>Late 70s-Early 80s</td>
    </tr>
    <tr>
      <th>395</th>
      <td>28.0</td>
      <td>4</td>
      <td>120.0</td>
      <td>79</td>
      <td>2625</td>
      <td>18.6</td>
      <td>82</td>
      <td>1</td>
      <td>ford ranger</td>
      <td>Domestic</td>
      <td>Domestic</td>
      <td>Late 70s-Early 80s</td>
    </tr>
    <tr>
      <th>396</th>
      <td>31.0</td>
      <td>4</td>
      <td>119.0</td>
      <td>82</td>
      <td>2720</td>
      <td>19.4</td>
      <td>82</td>
      <td>1</td>
      <td>chevy s-10</td>
      <td>Domestic</td>
      <td>Domestic</td>
      <td>Late 70s-Early 80s</td>
    </tr>
  </tbody>
</table>
<p>397 rows × 12 columns</p>
</div>




```python
# groupby again
auto[["year_bin","mpg"]].groupby("year_bin").mean()
```

    C:\Users\micha\AppData\Local\Temp\ipykernel_10968\3944153947.py:2: FutureWarning: The default of observed=False is deprecated and will be changed to True in a future version of pandas. Pass observed=False to retain current behavior or observed=True to adopt the future default and silence this warning.
      auto[["year_bin","mpg"]].groupby("year_bin").mean()
    




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
      <th>mpg</th>
    </tr>
    <tr>
      <th>year_bin</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Early 70s</th>
      <td>18.528000</td>
    </tr>
    <tr>
      <th>Mid 70s</th>
      <td>21.924370</td>
    </tr>
    <tr>
      <th>Late 70s-Early 80s</th>
      <td>28.828758</td>
    </tr>
  </tbody>
</table>
</div>




```python
# ols on bins
model4 = smf.ols("mpg ~ year_bin",data=auto).fit(cov_type="HC1")
print(model4.summary())
```

                                OLS Regression Results                            
    ==============================================================================
    Dep. Variable:                    mpg   R-squared:                       0.319
    Model:                            OLS   Adj. R-squared:                  0.315
    Method:                 Least Squares   F-statistic:                     87.69
    Date:                Thu, 16 Apr 2026   Prob (F-statistic):           3.15e-32
    Time:                        15:32:52   Log-Likelihood:                -1303.4
    No. Observations:                 397   AIC:                             2613.
    Df Residuals:                     394   BIC:                             2625.
    Df Model:                           2                                         
    Covariance Type:                  HC1                                         
    ==================================================================================================
                                         coef    std err          z      P>|z|      [0.025      0.975]
    --------------------------------------------------------------------------------------------------
    Intercept                         18.5280      0.504     36.752      0.000      17.540      19.516
    year_bin[T.Mid 70s]                3.3964      0.748      4.541      0.000       1.931       4.862
    year_bin[T.Late 70s-Early 80s]    10.3008      0.782     13.177      0.000       8.769      11.833
    ==============================================================================
    Omnibus:                       24.640   Durbin-Watson:                   0.736
    Prob(Omnibus):                  0.000   Jarque-Bera (JB):               12.595
    Skew:                           0.248   Prob(JB):                      0.00184
    Kurtosis:                       2.282   Cond. No.                         3.84
    ==============================================================================
    
    Notes:
    [1] Standard Errors are heteroscedasticity robust (HC1)
    


```python
# qcut
auto["year_quantile"] = pd.qcut(auto["year"], 2, labels=["70-76", "77-82"])
auto
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
      <th>mpg</th>
      <th>cylinders</th>
      <th>displacement</th>
      <th>horsepower</th>
      <th>weight</th>
      <th>acceleration</th>
      <th>year</th>
      <th>origin</th>
      <th>name</th>
      <th>foreign</th>
      <th>foreign_alt</th>
      <th>year_bin</th>
      <th>year_quantile</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>18.0</td>
      <td>8</td>
      <td>307.0</td>
      <td>130</td>
      <td>3504</td>
      <td>12.0</td>
      <td>70</td>
      <td>1</td>
      <td>chevrolet chevelle malibu</td>
      <td>Domestic</td>
      <td>Domestic</td>
      <td>Early 70s</td>
      <td>70-76</td>
    </tr>
    <tr>
      <th>1</th>
      <td>15.0</td>
      <td>8</td>
      <td>350.0</td>
      <td>165</td>
      <td>3693</td>
      <td>11.5</td>
      <td>70</td>
      <td>1</td>
      <td>buick skylark 320</td>
      <td>Domestic</td>
      <td>Domestic</td>
      <td>Early 70s</td>
      <td>70-76</td>
    </tr>
    <tr>
      <th>2</th>
      <td>18.0</td>
      <td>8</td>
      <td>318.0</td>
      <td>150</td>
      <td>3436</td>
      <td>11.0</td>
      <td>70</td>
      <td>1</td>
      <td>plymouth satellite</td>
      <td>Domestic</td>
      <td>Domestic</td>
      <td>Early 70s</td>
      <td>70-76</td>
    </tr>
    <tr>
      <th>3</th>
      <td>16.0</td>
      <td>8</td>
      <td>304.0</td>
      <td>150</td>
      <td>3433</td>
      <td>12.0</td>
      <td>70</td>
      <td>1</td>
      <td>amc rebel sst</td>
      <td>Domestic</td>
      <td>Domestic</td>
      <td>Early 70s</td>
      <td>70-76</td>
    </tr>
    <tr>
      <th>4</th>
      <td>17.0</td>
      <td>8</td>
      <td>302.0</td>
      <td>140</td>
      <td>3449</td>
      <td>10.5</td>
      <td>70</td>
      <td>1</td>
      <td>ford torino</td>
      <td>Domestic</td>
      <td>Domestic</td>
      <td>Early 70s</td>
      <td>70-76</td>
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
    </tr>
    <tr>
      <th>392</th>
      <td>27.0</td>
      <td>4</td>
      <td>140.0</td>
      <td>86</td>
      <td>2790</td>
      <td>15.6</td>
      <td>82</td>
      <td>1</td>
      <td>ford mustang gl</td>
      <td>Domestic</td>
      <td>Domestic</td>
      <td>Late 70s-Early 80s</td>
      <td>77-82</td>
    </tr>
    <tr>
      <th>393</th>
      <td>44.0</td>
      <td>4</td>
      <td>97.0</td>
      <td>52</td>
      <td>2130</td>
      <td>24.6</td>
      <td>82</td>
      <td>2</td>
      <td>vw pickup</td>
      <td>Foreign</td>
      <td>Foreign</td>
      <td>Late 70s-Early 80s</td>
      <td>77-82</td>
    </tr>
    <tr>
      <th>394</th>
      <td>32.0</td>
      <td>4</td>
      <td>135.0</td>
      <td>84</td>
      <td>2295</td>
      <td>11.6</td>
      <td>82</td>
      <td>1</td>
      <td>dodge rampage</td>
      <td>Domestic</td>
      <td>Domestic</td>
      <td>Late 70s-Early 80s</td>
      <td>77-82</td>
    </tr>
    <tr>
      <th>395</th>
      <td>28.0</td>
      <td>4</td>
      <td>120.0</td>
      <td>79</td>
      <td>2625</td>
      <td>18.6</td>
      <td>82</td>
      <td>1</td>
      <td>ford ranger</td>
      <td>Domestic</td>
      <td>Domestic</td>
      <td>Late 70s-Early 80s</td>
      <td>77-82</td>
    </tr>
    <tr>
      <th>396</th>
      <td>31.0</td>
      <td>4</td>
      <td>119.0</td>
      <td>82</td>
      <td>2720</td>
      <td>19.4</td>
      <td>82</td>
      <td>1</td>
      <td>chevy s-10</td>
      <td>Domestic</td>
      <td>Domestic</td>
      <td>Late 70s-Early 80s</td>
      <td>77-82</td>
    </tr>
  </tbody>
</table>
<p>397 rows × 13 columns</p>
</div>




```python
# groupby again, qcut
auto[["year_quantile","mpg"]].groupby("year_quantile").mean()
```

    C:\Users\micha\AppData\Local\Temp\ipykernel_10968\1716184374.py:2: FutureWarning: The default of observed=False is deprecated and will be changed to True in a future version of pandas. Pass observed=False to retain current behavior or observed=True to adopt the future default and silence this warning.
      auto[["year_quantile","mpg"]].groupby("year_quantile").mean()
    




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
      <th>mpg</th>
    </tr>
    <tr>
      <th>year_quantile</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>70-76</th>
      <td>19.770833</td>
    </tr>
    <tr>
      <th>77-82</th>
      <td>27.985083</td>
    </tr>
  </tbody>
</table>
</div>




```python
# ols on quantiles
model5 = smf.ols("mpg ~ year_quantile",data=auto).fit(cov_type="HC1")
print(model5.summary())
```

                                OLS Regression Results                            
    ==============================================================================
    Dep. Variable:                    mpg   R-squared:                       0.274
    Model:                            OLS   Adj. R-squared:                  0.272
    Method:                 Least Squares   F-statistic:                     142.8
    Date:                Thu, 16 Apr 2026   Prob (F-statistic):           2.62e-28
    Time:                        15:39:07   Log-Likelihood:                -1316.1
    No. Observations:                 397   AIC:                             2636.
    Df Residuals:                     395   BIC:                             2644.
    Df Model:                           1                                         
    Covariance Type:                  HC1                                         
    ==========================================================================================
                                 coef    std err          z      P>|z|      [0.025      0.975]
    ------------------------------------------------------------------------------------------
    Intercept                 19.7708      0.399     49.490      0.000      18.988      20.554
    year_quantile[T.77-82]     8.2142      0.687     11.950      0.000       6.867       9.561
    ==============================================================================
    Omnibus:                       23.918   Durbin-Watson:                   0.695
    Prob(Omnibus):                  0.000   Jarque-Bera (JB):               12.145
    Skew:                           0.237   Prob(JB):                      0.00231
    Kurtosis:                       2.286   Cond. No.                         2.53
    ==============================================================================
    
    Notes:
    [1] Standard Errors are heteroscedasticity robust (HC1)
    

## Practice Binning
1. Create a variable called `horsepower_tercile` that splits the `horsepower` variable into thirds, label them appropriately. *Hint: What type is `horsepower`? Sort by index to see the range.*
2. Create a variable called `horsepower_bins` that splits `horsepower` into three equally sized bins
3. Are these different?


```python
# Question marks show up... Must be NA?
auto["horsepower"].sort_values()
```




    133    100
    98     100
    256    100
    107    100
    334    100
          ... 
    336      ?
    126      ?
    354      ?
    32       ?
    330      ?
    Name: horsepower, Length: 397, dtype: object




```python
# Treated as a string
type(auto["horsepower"][1])
```




    str




```python
# Drop the question marks and convert to int
auto = auto.drop(auto[auto["horsepower"] == "?"].index)
auto["horsepower"] = auto["horsepower"].astype(int)
auto
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
      <th>mpg</th>
      <th>cylinders</th>
      <th>displacement</th>
      <th>horsepower</th>
      <th>weight</th>
      <th>acceleration</th>
      <th>year</th>
      <th>origin</th>
      <th>name</th>
      <th>foreign</th>
      <th>foreign_alt</th>
      <th>year_bin</th>
      <th>year_quantile</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>18.0</td>
      <td>8</td>
      <td>307.0</td>
      <td>130</td>
      <td>3504</td>
      <td>12.0</td>
      <td>70</td>
      <td>1</td>
      <td>chevrolet chevelle malibu</td>
      <td>Domestic</td>
      <td>Domestic</td>
      <td>Early 70s</td>
      <td>70-76</td>
    </tr>
    <tr>
      <th>1</th>
      <td>15.0</td>
      <td>8</td>
      <td>350.0</td>
      <td>165</td>
      <td>3693</td>
      <td>11.5</td>
      <td>70</td>
      <td>1</td>
      <td>buick skylark 320</td>
      <td>Domestic</td>
      <td>Domestic</td>
      <td>Early 70s</td>
      <td>70-76</td>
    </tr>
    <tr>
      <th>2</th>
      <td>18.0</td>
      <td>8</td>
      <td>318.0</td>
      <td>150</td>
      <td>3436</td>
      <td>11.0</td>
      <td>70</td>
      <td>1</td>
      <td>plymouth satellite</td>
      <td>Domestic</td>
      <td>Domestic</td>
      <td>Early 70s</td>
      <td>70-76</td>
    </tr>
    <tr>
      <th>3</th>
      <td>16.0</td>
      <td>8</td>
      <td>304.0</td>
      <td>150</td>
      <td>3433</td>
      <td>12.0</td>
      <td>70</td>
      <td>1</td>
      <td>amc rebel sst</td>
      <td>Domestic</td>
      <td>Domestic</td>
      <td>Early 70s</td>
      <td>70-76</td>
    </tr>
    <tr>
      <th>4</th>
      <td>17.0</td>
      <td>8</td>
      <td>302.0</td>
      <td>140</td>
      <td>3449</td>
      <td>10.5</td>
      <td>70</td>
      <td>1</td>
      <td>ford torino</td>
      <td>Domestic</td>
      <td>Domestic</td>
      <td>Early 70s</td>
      <td>70-76</td>
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
    </tr>
    <tr>
      <th>392</th>
      <td>27.0</td>
      <td>4</td>
      <td>140.0</td>
      <td>86</td>
      <td>2790</td>
      <td>15.6</td>
      <td>82</td>
      <td>1</td>
      <td>ford mustang gl</td>
      <td>Domestic</td>
      <td>Domestic</td>
      <td>Late 70s-Early 80s</td>
      <td>77-82</td>
    </tr>
    <tr>
      <th>393</th>
      <td>44.0</td>
      <td>4</td>
      <td>97.0</td>
      <td>52</td>
      <td>2130</td>
      <td>24.6</td>
      <td>82</td>
      <td>2</td>
      <td>vw pickup</td>
      <td>Foreign</td>
      <td>Foreign</td>
      <td>Late 70s-Early 80s</td>
      <td>77-82</td>
    </tr>
    <tr>
      <th>394</th>
      <td>32.0</td>
      <td>4</td>
      <td>135.0</td>
      <td>84</td>
      <td>2295</td>
      <td>11.6</td>
      <td>82</td>
      <td>1</td>
      <td>dodge rampage</td>
      <td>Domestic</td>
      <td>Domestic</td>
      <td>Late 70s-Early 80s</td>
      <td>77-82</td>
    </tr>
    <tr>
      <th>395</th>
      <td>28.0</td>
      <td>4</td>
      <td>120.0</td>
      <td>79</td>
      <td>2625</td>
      <td>18.6</td>
      <td>82</td>
      <td>1</td>
      <td>ford ranger</td>
      <td>Domestic</td>
      <td>Domestic</td>
      <td>Late 70s-Early 80s</td>
      <td>77-82</td>
    </tr>
    <tr>
      <th>396</th>
      <td>31.0</td>
      <td>4</td>
      <td>119.0</td>
      <td>82</td>
      <td>2720</td>
      <td>19.4</td>
      <td>82</td>
      <td>1</td>
      <td>chevy s-10</td>
      <td>Domestic</td>
      <td>Domestic</td>
      <td>Late 70s-Early 80s</td>
      <td>77-82</td>
    </tr>
  </tbody>
</table>
<p>392 rows × 13 columns</p>
</div>




```python
# 1.
auto["horsepower_tercile"] = pd.qcut(auto["horsepower"],3, labels=["lower","mid", "upper"])
# 2.
auto["horsepower_bins"] = pd.cut(auto["horsepower"], 3, labels=["lower","mid", "upper"])
auto
# 3.
# They are different! quantile is based on the data itself and should be approximately 1/3 in each category
# cut makes the bin sizes the same, so it just splits the min to max into thirds and however much data is in each bin doesn't matter
print(auto["horsepower_tercile"].value_counts())
print(auto["horsepower_bins"].value_counts())
```

    horsepower_tercile
    mid      144
    lower    132
    upper    116
    Name: count, dtype: int64
    horsepower_bins
    lower    257
    mid      103
    upper     32
    Name: count, dtype: int64
    
