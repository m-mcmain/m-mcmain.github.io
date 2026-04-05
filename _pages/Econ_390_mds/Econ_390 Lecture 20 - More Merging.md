---
layout: single
sitemap: false
permalink: /pages/Econ_390_SP26_L20_teaching/
title: Econ 390 Lecture 20
---

[Download Jupyter Notebook Empty](https://m-mcmain.github.io/files/Econ390SP26/Lectures/Lecture20_MoreMerging_empty.ipynb)

Download Jupyter Notebook Completed

# Econ 390: Lecture 20 - More Merging
Today we will be spending some more time merging datasets. Relevant pages are [8.2 in McKinney](https://wesmckinney.com/book/data-wrangling#prep_merge_join), [Merge in Turrell](https://aeturrell.github.io/coding-for-economists/data-joining-data.html#merge), and [this page](https://sscc.wisc.edu/sscc/pubs/dwp/Combining_Data_Sets.html#adding-variables) from the SSCC.

There are three general types of merging you will need to do. In order of how often *I* use them:
1. Creating Panel Data (Same Dataset Across Time)
2. Merging Unrelated Data On Time (Different Datasets Across Time)
3. Merging the Same Data over Multiple Sources (Same Data Across Sources)

We did a little bit of #1 at the end of last lecture. #3 is generally pretty rare and happens when you have high quality restricted data. #2 is very common when you want to control for macro variables that are common among everyone but change over time.


```python
import numpy as np
import pandas as pd

econ390path = "https://m-mcmain.github.io/files/Econ390SP26/"
```

## Wide and Long Data

![Image showing the difference between wide and long data](https://www.statology.org/wp-content/uploads/2021/12/wideLong1-1-768x543.png "Wide vs. Long Data")


```python
# Create the data
final_four = pd.DataFrame({"Team": ["Michigan", "Arizona", "Illinois", "UConn"],
                           "Points": [91, 73, 62, 71],
                           "Assists": [22, 5, 3, 14],
                           "Rebounds": [40, 44, 44, 37]})
```


```python
# "Melt" to go from Wide to Long
final_four_melted = pd.melt(final_four, id_vars="Team")
final_four_melted
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
      <th>Team</th>
      <th>variable</th>
      <th>value</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Michigan</td>
      <td>Points</td>
      <td>91</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Arizona</td>
      <td>Points</td>
      <td>73</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Illinois</td>
      <td>Points</td>
      <td>62</td>
    </tr>
    <tr>
      <th>3</th>
      <td>UConn</td>
      <td>Points</td>
      <td>71</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Michigan</td>
      <td>Assists</td>
      <td>22</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Arizona</td>
      <td>Assists</td>
      <td>5</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Illinois</td>
      <td>Assists</td>
      <td>3</td>
    </tr>
    <tr>
      <th>7</th>
      <td>UConn</td>
      <td>Assists</td>
      <td>14</td>
    </tr>
    <tr>
      <th>8</th>
      <td>Michigan</td>
      <td>Rebounds</td>
      <td>40</td>
    </tr>
    <tr>
      <th>9</th>
      <td>Arizona</td>
      <td>Rebounds</td>
      <td>44</td>
    </tr>
    <tr>
      <th>10</th>
      <td>Illinois</td>
      <td>Rebounds</td>
      <td>44</td>
    </tr>
    <tr>
      <th>11</th>
      <td>UConn</td>
      <td>Rebounds</td>
      <td>37</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Pivot to go back to Wide
final_four_reshaped = final_four_melted.pivot(index="Team", columns="variable",
                                              values="value")
final_four_reshaped
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
      <th>variable</th>
      <th>Assists</th>
      <th>Points</th>
      <th>Rebounds</th>
    </tr>
    <tr>
      <th>Team</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Arizona</th>
      <td>5</td>
      <td>73</td>
      <td>44</td>
    </tr>
    <tr>
      <th>Illinois</th>
      <td>3</td>
      <td>62</td>
      <td>44</td>
    </tr>
    <tr>
      <th>Michigan</th>
      <td>22</td>
      <td>91</td>
      <td>40</td>
    </tr>
    <tr>
      <th>UConn</th>
      <td>14</td>
      <td>71</td>
      <td>37</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Reset Index
final_four_reshaped = final_four_reshaped.reset_index()
final_four_reshaped
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
      <th>variable</th>
      <th>Team</th>
      <th>Assists</th>
      <th>Points</th>
      <th>Rebounds</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Arizona</td>
      <td>5</td>
      <td>73</td>
      <td>44</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Illinois</td>
      <td>3</td>
      <td>62</td>
      <td>44</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Michigan</td>
      <td>22</td>
      <td>91</td>
      <td>40</td>
    </tr>
    <tr>
      <th>3</th>
      <td>UConn</td>
      <td>14</td>
      <td>71</td>
      <td>37</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Select the vars to melt
pd.melt(final_four, id_vars="Team", value_vars=["Points", "Assists"])
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
      <th>Team</th>
      <th>variable</th>
      <th>value</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Michigan</td>
      <td>Points</td>
      <td>91</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Arizona</td>
      <td>Points</td>
      <td>73</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Illinois</td>
      <td>Points</td>
      <td>62</td>
    </tr>
    <tr>
      <th>3</th>
      <td>UConn</td>
      <td>Points</td>
      <td>71</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Michigan</td>
      <td>Assists</td>
      <td>22</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Arizona</td>
      <td>Assists</td>
      <td>5</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Illinois</td>
      <td>Assists</td>
      <td>3</td>
    </tr>
    <tr>
      <th>7</th>
      <td>UConn</td>
      <td>Assists</td>
      <td>14</td>
    </tr>
  </tbody>
</table>
</div>



## Back to Merging


```python
# Read in data
ffr_cleaned = pd.read_csv(econ390path + "ffr_cleaned.csv", index_col = 0)
rd_BEA = pd.read_csv(econ390path + "rd_BEA.csv", index_col = 0)
```


```python
# Check out the data
print(ffr_cleaned.head())
print(rd_BEA.head())
```

          FEDFUNDS
    Year          
    2008      1.93
    2009      0.16
    2010      0.18
    2011      0.10
    2012      0.14
            State      RD
    Date                 
    2012  Alabama  2176.2
    2013  Alabama  2328.3
    2014  Alabama  2717.8
    2015  Alabama  2480.0
    2016  Alabama  3089.6
    


```python
# How should we merge them? Concat? Do resulting rows make sense?
rd_merged = pd.merge(ffr_cleaned, rd_BEA, left_index = True, right_index = True)
print(rd_merged.head())
print(rd_merged.tail())
```

          FEDFUNDS       State       RD
    Year                               
    2012      0.14     Alabama   2176.2
    2012      0.14      Alaska    186.1
    2012      0.14     Arizona   4265.9
    2012      0.14    Arkansas    439.1
    2012      0.14  California  66602.9
          FEDFUNDS          State       RD
    Year                                  
    2023      5.02       Virginia  10372.0
    2023      5.02     Washington  42498.5
    2023      5.02  West Virginia    550.4
    2023      5.02      Wisconsin   7248.9
    2023      5.02        Wyoming    160.4
    


```python
# How is outer different?
rd_merged = pd.merge(ffr_cleaned, rd_BEA, how = "outer", left_index = True, right_index = True, indicator = True)
print(rd_merged.head())
print(rd_merged.tail())
```

          FEDFUNDS    State      RD     _merge
    Year                                      
    2008      1.93      NaN     NaN  left_only
    2009      0.16      NaN     NaN  left_only
    2010      0.18      NaN     NaN  left_only
    2011      0.10      NaN     NaN  left_only
    2012      0.14  Alabama  2176.2       both
          FEDFUNDS          State       RD     _merge
    Year                                             
    2023      5.02     Washington  42498.5       both
    2023      5.02  West Virginia    550.4       both
    2023      5.02      Wisconsin   7248.9       both
    2023      5.02        Wyoming    160.4       both
    2024      5.14            NaN      NaN  left_only
    

## Merging Variable Type


```python
# Set random seed (for reproducibility), ID length, and number of observations
np.random.seed(1)
digits_in_id=16     # Set a value between 1 and 16 (inclusive)
number_of_obs=100
```


```python
# Generate string ID of the specified length, convert to float, then back to string
random = np.random.randint(1,10,size=(number_of_obs, digits_in_id))
id_before = pd.DataFrame(random).astype(str).sum(axis=1)
id_float = id_before.astype(float)
id_after = id_float.astype(str).str[:-2]
```


```python
# Display results in a DataFrame
id_combined = pd.DataFrame({
    'id_before': id_before,
    'id_float': id_float,
    'id_after': id_after})
id_combined[id_combined['id_before'] != id_combined['id_after']]
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
      <th>id_before</th>
      <th>id_float</th>
      <th>id_after</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>6</th>
      <td>9342383713773881</td>
      <td>9.342384e+15</td>
      <td>9342383713773880</td>
    </tr>
    <tr>
      <th>9</th>
      <td>9692298145314623</td>
      <td>9.692298e+15</td>
      <td>9692298145314624</td>
    </tr>
    <tr>
      <th>21</th>
      <td>9991831822626759</td>
      <td>9.991832e+15</td>
      <td>9991831822626760</td>
    </tr>
    <tr>
      <th>49</th>
      <td>9137947587432667</td>
      <td>9.137948e+15</td>
      <td>9137947587432668</td>
    </tr>
    <tr>
      <th>78</th>
      <td>9726119248623743</td>
      <td>9.726119e+15</td>
      <td>9726119248623744</td>
    </tr>
    <tr>
      <th>94</th>
      <td>9171857237431627</td>
      <td>9.171857e+15</td>
      <td>9171857237431628</td>
    </tr>
    <tr>
      <th>95</th>
      <td>9377217656957167</td>
      <td>9.377218e+15</td>
      <td>9377217656957168</td>
    </tr>
  </tbody>
</table>
</div>



So, if you have data that is read in as Float, you cannot then convert it to a String. It has already done the estimation! So, you'll need to specifically read it in *as* a String by using the `dtype={'var': 'str'}` option in `read_csv`.

Another thing to note when matching with Strings. Make sure that the ID format is consistent across files (e.g. Case Sensitive and Whitespace). If it's not you'll need to do so yourself! Such as `str.lower()` and `str.strip()` respectively.

## Investigating Unmatched Observations

As a reminder, FUSION_annual_1995_EMP is a random sample of 100 Chilean Manufacturing Survey responses from 1995 where each row is one firm that has identifier "NUI" (almost certainly some sort of acronym in Spanish). FUSION_annual_1996_EMP is created similarly, but instead of being a completely random sample, I select the NUI's that show up in both the 1996 Chilean Manufacturing Survey and 1995's, then randomly fill out the rest from 1996 if not all 100 from 1995 are also in 1996. 

Why might not all 100 firms from the random sample in 1995 also be in the 1996 survey responses?


```python
# Read in our data
fusion_1995 = pd.read_stata(econ390path + "FUSION_annual_1995_EMP.dta")
fusion_1996 = pd.read_stata(econ390path + "FUSION_annual_1996_EMP_erroneous.dta")
```


```python
# Merge
fusion_merged = pd.merge(fusion_1995, fusion_1996, on="NUI", suffixes = ("_1995", "_1996"))
fusion_merged
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
      <th>REGION_1995</th>
      <th>CIIU3_1995</th>
      <th>TOTHOM_1995</th>
      <th>TOTMUJ_1995</th>
      <th>REMEMP_1995</th>
      <th>REGEMP_1995</th>
      <th>REMCOM_1995</th>
      <th>REGCOM_1995</th>
      <th>REMOBR_1995</th>
      <th>...</th>
      <th>TOTMUJ_1996</th>
      <th>REMEMP_1996</th>
      <th>REGEMP_1996</th>
      <th>REMCOM_1996</th>
      <th>REGCOM_1996</th>
      <th>REMOBR_1996</th>
      <th>REGOBR_1996</th>
      <th>TOHSC_1996</th>
      <th>TOMSC_1996</th>
      <th>EXPORTADOS_1996</th>
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
      <td>...</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>12601</td>
      <td>935</td>
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
      <td>...</td>
      <td>21</td>
      <td>3193584</td>
      <td>149500</td>
      <td>0</td>
      <td>0</td>
      <td>341581</td>
      <td>95786</td>
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
      <td>...</td>
      <td>6</td>
      <td>179492</td>
      <td>4974</td>
      <td>44424</td>
      <td>744</td>
      <td>48379</td>
      <td>3820</td>
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
      <td>...</td>
      <td>41</td>
      <td>39148</td>
      <td>8618</td>
      <td>0</td>
      <td>0</td>
      <td>47848</td>
      <td>5518</td>
      <td>0</td>
      <td>0</td>
      <td>1.0</td>
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
      <td>...</td>
      <td>12</td>
      <td>700294</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>769546</td>
      <td>533036</td>
      <td>35</td>
      <td>4</td>
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
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>86</th>
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
      <td>...</td>
      <td>7</td>
      <td>116021</td>
      <td>6696</td>
      <td>0</td>
      <td>0</td>
      <td>137961</td>
      <td>11918</td>
      <td>9</td>
      <td>0</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>87</th>
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
      <td>...</td>
      <td>0</td>
      <td>1645479</td>
      <td>137451</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>88</th>
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
      <td>...</td>
      <td>4</td>
      <td>17279</td>
      <td>347</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>89</th>
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
      <td>...</td>
      <td>5</td>
      <td>6823</td>
      <td>1412</td>
      <td>2896</td>
      <td>599</td>
      <td>71229</td>
      <td>532</td>
      <td>0</td>
      <td>0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>90</th>
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
      <td>...</td>
      <td>2</td>
      <td>5296</td>
      <td>225</td>
      <td>11518</td>
      <td>473</td>
      <td>33151</td>
      <td>1355</td>
      <td>0</td>
      <td>0</td>
      <td>0.0</td>
    </tr>
  </tbody>
</table>
<p>91 rows × 27 columns</p>
</div>




```python
# Check out a specific NUI
fusion_merged.loc[fusion_merged["NUI"] == 40172.0, ["CIIU3_1995", "CIIU3_1996"]]
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
      <th>CIIU3_1995</th>
      <th>CIIU3_1996</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>89</th>
      <td>2022</td>
      <td>2022</td>
    </tr>
    <tr>
      <th>90</th>
      <td>2022</td>
      <td>2211</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Merge using validate, expecting 1:1
fusion_merged = pd.merge(fusion_1995, fusion_1996, on="NUI", suffixes = ("_1995", "_1996"), how = "outer", validate="1:1")
fusion_merged
```


    ---------------------------------------------------------------------------

    MergeError                                Traceback (most recent call last)

    Cell In[17], line 2
          1 # Merge using validate, expecting 1:1
    ----> 2 fusion_merged = pd.merge(fusion_1995, fusion_1996, on="NUI", suffixes = ("_1995", "_1996"), how = "outer", validate="1:1")
          3 fusion_merged
    

    File ~\anaconda3\Lib\site-packages\pandas\core\reshape\merge.py:170, in merge(left, right, how, on, left_on, right_on, left_index, right_index, sort, suffixes, copy, indicator, validate)
        155     return _cross_merge(
        156         left_df,
        157         right_df,
       (...)    167         copy=copy,
        168     )
        169 else:
    --> 170     op = _MergeOperation(
        171         left_df,
        172         right_df,
        173         how=how,
        174         on=on,
        175         left_on=left_on,
        176         right_on=right_on,
        177         left_index=left_index,
        178         right_index=right_index,
        179         sort=sort,
        180         suffixes=suffixes,
        181         indicator=indicator,
        182         validate=validate,
        183     )
        184     return op.get_result(copy=copy)
    

    File ~\anaconda3\Lib\site-packages\pandas\core\reshape\merge.py:813, in _MergeOperation.__init__(self, left, right, how, on, left_on, right_on, left_index, right_index, sort, suffixes, indicator, validate)
        809 # If argument passed to validate,
        810 # check if columns specified as unique
        811 # are in fact unique.
        812 if validate is not None:
    --> 813     self._validate_validate_kwd(validate)
    

    File ~\anaconda3\Lib\site-packages\pandas\core\reshape\merge.py:1658, in _MergeOperation._validate_validate_kwd(self, validate)
       1654         raise MergeError(
       1655             "Merge keys are not unique in left dataset; not a one-to-one merge"
       1656         )
       1657     if not right_unique:
    -> 1658         raise MergeError(
       1659             "Merge keys are not unique in right dataset; not a one-to-one merge"
       1660         )
       1662 elif validate in ["one_to_many", "1:m"]:
       1663     if not left_unique:
    

    MergeError: Merge keys are not unique in right dataset; not a one-to-one merge



```python
# Try Except to save ourselves
try:
    fusion_merged = pd.merge(fusion_1995, fusion_1996, how = "outer", on="NUI", suffixes = ("_1995", "_1996"), validate="1:1")
except pd.errors.MergeError as e:
    print('WARNING:', e, '-> NUI duplicates dropped\n')
    fusion_merged = pd.merge(fusion_1995, fusion_1996, how = "outer", on="NUI", suffixes = ("_1995", "_1996"))
    fusion_merged = fusion_merged.drop_duplicates(subset='NUI', keep = "first")

fusion_merged
```

    WARNING: Merge keys are not unique in right dataset; not a one-to-one merge -> NUI duplicates dropped
    
    




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
      <th>REGION_1995</th>
      <th>CIIU3_1995</th>
      <th>TOTHOM_1995</th>
      <th>TOTMUJ_1995</th>
      <th>REMEMP_1995</th>
      <th>REGEMP_1995</th>
      <th>REMCOM_1995</th>
      <th>REGCOM_1995</th>
      <th>REMOBR_1995</th>
      <th>...</th>
      <th>TOTMUJ_1996</th>
      <th>REMEMP_1996</th>
      <th>REGEMP_1996</th>
      <th>REMCOM_1996</th>
      <th>REGCOM_1996</th>
      <th>REMOBR_1996</th>
      <th>REGOBR_1996</th>
      <th>TOHSC_1996</th>
      <th>TOMSC_1996</th>
      <th>EXPORTADOS_1996</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>10082.0</td>
      <td>2.0</td>
      <td>3610.0</td>
      <td>14.0</td>
      <td>1.0</td>
      <td>7466.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>20174.0</td>
      <td>...</td>
      <td>1.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>12601.0</td>
      <td>935.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>10101.0</td>
      <td>2.0</td>
      <td>2720.0</td>
      <td>427.0</td>
      <td>25.0</td>
      <td>2046170.0</td>
      <td>184590.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>810717.0</td>
      <td>...</td>
      <td>21.0</td>
      <td>3193584.0</td>
      <td>149500.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>341581.0</td>
      <td>95786.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>10103.0</td>
      <td>2.0</td>
      <td>1531.0</td>
      <td>46.0</td>
      <td>6.0</td>
      <td>135873.0</td>
      <td>3426.0</td>
      <td>69814.0</td>
      <td>2912.0</td>
      <td>37037.0</td>
      <td>...</td>
      <td>6.0</td>
      <td>179492.0</td>
      <td>4974.0</td>
      <td>44424.0</td>
      <td>744.0</td>
      <td>48379.0</td>
      <td>3820.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>10178.0</td>
      <td>4.0</td>
      <td>1512.0</td>
      <td>39.0</td>
      <td>35.0</td>
      <td>22958.0</td>
      <td>1886.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>40257.0</td>
      <td>...</td>
      <td>41.0</td>
      <td>39148.0</td>
      <td>8618.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>47848.0</td>
      <td>5518.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>10220.0</td>
      <td>5.0</td>
      <td>3312.0</td>
      <td>481.0</td>
      <td>15.0</td>
      <td>554636.0</td>
      <td>187853.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>858571.0</td>
      <td>...</td>
      <td>12.0</td>
      <td>700294.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>769546.0</td>
      <td>533036.0</td>
      <td>35.0</td>
      <td>4.0</td>
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
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>104</th>
      <td>23437.0</td>
      <td>13.0</td>
      <td>2520.0</td>
      <td>81.0</td>
      <td>6.0</td>
      <td>88656.0</td>
      <td>1432.0</td>
      <td>3284.0</td>
      <td>0.0</td>
      <td>117469.0</td>
      <td>...</td>
      <td>7.0</td>
      <td>116021.0</td>
      <td>6696.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>137961.0</td>
      <td>11918.0</td>
      <td>9.0</td>
      <td>0.0</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>105</th>
      <td>23449.0</td>
      <td>6.0</td>
      <td>2924.0</td>
      <td>145.0</td>
      <td>0.0</td>
      <td>914130.0</td>
      <td>54126.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>267928.0</td>
      <td>...</td>
      <td>0.0</td>
      <td>1645479.0</td>
      <td>137451.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>106</th>
      <td>40088.0</td>
      <td>8.0</td>
      <td>3693.0</td>
      <td>3.0</td>
      <td>3.0</td>
      <td>13495.0</td>
      <td>271.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>...</td>
      <td>4.0</td>
      <td>17279.0</td>
      <td>347.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>107</th>
      <td>40172.0</td>
      <td>1.0</td>
      <td>2022.0</td>
      <td>31.0</td>
      <td>5.0</td>
      <td>6205.0</td>
      <td>1284.0</td>
      <td>2634.0</td>
      <td>545.0</td>
      <td>64776.0</td>
      <td>...</td>
      <td>5.0</td>
      <td>6823.0</td>
      <td>1412.0</td>
      <td>2896.0</td>
      <td>599.0</td>
      <td>71229.0</td>
      <td>532.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>109</th>
      <td>40175.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>...</td>
      <td>4.0</td>
      <td>87440.0</td>
      <td>1202.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>58515.0</td>
      <td>21505.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
    </tr>
  </tbody>
</table>
<p>109 rows × 27 columns</p>
</div>



## [MovieLens Data](https://wesmckinney.com/book/data-analysis-examples#whetting_movielens)
Are Comedies or Dramas better rated on average? Let's find out!


```python
# Read in the data
movies = pd.read_csv(econ390path + "movies.csv")
ratings = pd.read_csv(econ390path + "ratings.csv")
```


```python
# Check out the datasets
print(movies.tail())
print(ratings.head())
```

          movieId                                      title  \
    9737   193581  Black Butler: Book of the Atlantic (2017)   
    9738   193583               No Game No Life: Zero (2017)   
    9739   193585                               Flint (2017)   
    9740   193587        Bungo Stray Dogs: Dead Apple (2018)   
    9741   193609        Andrew Dice Clay: Dice Rules (1991)   
    
                                   genres  
    9737  Action|Animation|Comedy|Fantasy  
    9738         Animation|Comedy|Fantasy  
    9739                            Drama  
    9740                 Action|Animation  
    9741                           Comedy  
       userId  movieId  rating  timestamp
    0       1        1     4.0  964982703
    1       1        3     4.0  964981247
    2       1        6     4.0  964982224
    3       1       47     5.0  964983815
    4       1       50     5.0  964982931
    


```python
# Merge to create ratings and genre, using validate
ratings_with_genre = pd.merge(movies, ratings, on="movieId", validate="1:m", indicator=True, how="outer")
```


```python
# Check out which entries are left or right only
print(ratings_with_genre[ratings_with_genre["_merge"] == "left_only"])
print(ratings_with_genre[ratings_with_genre["_merge"] == "right_only"])
```

           movieId                                         title  \
    22820     1076                         Innocents, The (1961)   
    49539     2939                                Niagara (1953)   
    53555     3338                        For All Mankind (1989)   
    54467     3456  Color of Paradise, The (Rang-e khoda) (1999)   
    60535     4194                I Know Where I'm Going! (1945)   
    68396     5721                            Chosen, The (1981)   
    71896     6668   Road Home, The (Wo de fu qin mu qin) (1999)   
    72428     6849                                Scrooge (1970)   
    73354     7020                                  Proof (1991)   
    75450     7792                     Parallax View, The (1974)   
    76859     8765                      This Gun for Hire (1942)   
    77983    25855                  Roaring Twenties, The (1939)   
    78026    26085                   Mutiny on the Bounty (1962)   
    79080    30892            In the Realms of the Unreal (2004)   
    79426    32160                      Twentieth Century (1934)   
    79459    32371                     Call Northside 777 (1948)   
    80506    34482                  Browning Version, The (1951)   
    92639    85565                            Chalet Girl (2011)   
    
                             genres  userId  rating  timestamp     _merge  
    22820     Drama|Horror|Thriller     NaN     NaN        NaN  left_only  
    49539            Drama|Thriller     NaN     NaN        NaN  left_only  
    53555               Documentary     NaN     NaN        NaN  left_only  
    54467                     Drama     NaN     NaN        NaN  left_only  
    60535         Drama|Romance|War     NaN     NaN        NaN  left_only  
    68396                     Drama     NaN     NaN        NaN  left_only  
    71896             Drama|Romance     NaN     NaN        NaN  left_only  
    72428     Drama|Fantasy|Musical     NaN     NaN        NaN  left_only  
    73354      Comedy|Drama|Romance     NaN     NaN        NaN  left_only  
    75450                  Thriller     NaN     NaN        NaN  left_only  
    76859  Crime|Film-Noir|Thriller     NaN     NaN        NaN  left_only  
    77983      Crime|Drama|Thriller     NaN     NaN        NaN  left_only  
    78026   Adventure|Drama|Romance     NaN     NaN        NaN  left_only  
    79080     Animation|Documentary     NaN     NaN        NaN  left_only  
    79426                    Comedy     NaN     NaN        NaN  left_only  
    79459     Crime|Drama|Film-Noir     NaN     NaN        NaN  left_only  
    80506                     Drama     NaN     NaN        NaN  left_only  
    92639            Comedy|Romance     NaN     NaN        NaN  left_only  
    Empty DataFrame
    Columns: [movieId, title, genres, userId, rating, timestamp, _merge]
    Index: []
    


```python
# Re-run to exclude unmatched observations
ratings_with_genre = pd.merge(movies, ratings, on="movieId", validate="1:m")
```


```python
# Ratings by Genre - does this make sense?
print('Descriptive Statistics for Comedies:')
print(ratings_with_genre[ratings_with_genre['genres']=='Comedy']['rating'].describe(),'\n')
print('Descriptive Statistics for Dramas:')
print(ratings_with_genre[ratings_with_genre['genres']=='Drama']['rating'].describe(),'\n')
```

    Descriptive Statistics for Comedies:
    count    7196.000000
    mean        3.197888
    std         1.107383
    min         0.500000
    25%         2.500000
    50%         3.000000
    75%         4.000000
    max         5.000000
    Name: rating, dtype: float64 
    
    Descriptive Statistics for Dramas:
    count    6291.000000
    mean        3.688841
    std         0.920846
    min         0.500000
    25%         3.000000
    50%         4.000000
    75%         4.000000
    max         5.000000
    Name: rating, dtype: float64 
    
    


```python
# Properly accommodate genres
print('Descriptive Statistics for Comedies:')
print(ratings_with_genre[ratings_with_genre['genres'].str.contains('Comedy')]['rating'].describe(),'\n')

print('Descriptive Statistics for Dramas:')
print(ratings_with_genre[ratings_with_genre['genres'].str.contains('Drama')]['rating'].describe())
```

    Descriptive Statistics for Comedies:
    count    39053.000000
    mean         3.384721
    std          1.066541
    min          0.500000
    25%          3.000000
    50%          3.500000
    75%          4.000000
    max          5.000000
    Name: rating, dtype: float64 
    
    Descriptive Statistics for Dramas:
    count    41928.000000
    mean         3.656184
    std          0.979133
    min          0.500000
    25%          3.000000
    50%          4.000000
    75%          4.500000
    max          5.000000
    Name: rating, dtype: float64
    
