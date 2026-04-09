---
layout: single
sitemap: false
permalink: /pages/Econ_390_SP26_L20/
title: Econ 390 Lecture 20
---

[Download Jupyter Notebook Empty](https://m-mcmain.github.io/files/Econ390SP26/Lectures/Lecture20_MoreMerging_empty.ipynb)

[Download Jupyter Notebook Completed](https://m-mcmain.github.io/files/Econ390SP26/Lectures/Lecture20_MoreMerging_full.ipynb)

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
final_four
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
      <th>Points</th>
      <th>Assists</th>
      <th>Rebounds</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Michigan</td>
      <td>91</td>
      <td>22</td>
      <td>40</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Arizona</td>
      <td>73</td>
      <td>5</td>
      <td>44</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Illinois</td>
      <td>62</td>
      <td>3</td>
      <td>44</td>
    </tr>
    <tr>
      <th>3</th>
      <td>UConn</td>
      <td>71</td>
      <td>14</td>
      <td>37</td>
    </tr>
  </tbody>
</table>
</div>




```python
# "Melt" to go from Wide to Long
final_four_melted = pd.melt(final_four, id_vars = "Team")
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
final_four_reshape = final_four_melted.pivot(index = "Team", columns = "variable", values = "value")
final_four_reshape
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
final_four_reshape.reset_index()
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
pd.melt(final_four, id_vars="Team", value_vars = ["Points", "Assists"])
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
print(ffr_cleaned.tail())
print(rd_BEA.tail())
```

          FEDFUNDS
    Year          
    2020      0.38
    2021      0.08
    2022      1.68
    2023      5.02
    2024      5.14
            State     RD
    Date                
    2019  Wyoming  150.7
    2020  Wyoming  179.9
    2021  Wyoming  182.2
    2022  Wyoming  175.8
    2023  Wyoming  160.4
    


```python
# How should we merge them? Concat? Do resulting rows make sense?
rd_merged = pd.merge(ffr_cleaned, rd_BEA, how = "inner", left_index = True, right_index = True)
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
rd_merged_outer = pd.merge(ffr_cleaned, rd_BEA, how = "right", left_index = True, right_index = True, indicator = True) 
print(rd_merged_outer.head())
print(rd_merged_outer.tail())
```

          FEDFUNDS    State      RD _merge
    Year                                  
    2012      0.14  Alabama  2176.2   both
    2013      0.11  Alabama  2328.3   both
    2014      0.09  Alabama  2717.8   both
    2015      0.13  Alabama  2480.0   both
    2016      0.40  Alabama  3089.6   both
          FEDFUNDS    State     RD _merge
    Year                                 
    2019      2.16  Wyoming  150.7   both
    2020      0.38  Wyoming  179.9   both
    2021      0.08  Wyoming  182.2   both
    2022      1.68  Wyoming  175.8   both
    2023      5.02  Wyoming  160.4   both
    

## Merging Variable Type


```python
# Set random seed (for reproducibility), ID length, and number of observations
np.random.seed(1)
digits_in_id = 16
n_obs = 100
```


```python
# Generate string ID of the specified length, convert to float, then back to string
random = np.random.randint(1,10,size=(n_obs, digits_in_id))
id_before = pd.DataFrame(random).astype(str).sum(axis=1)
id_float = id_before.astype(float)
id_after = id_float.astype(str).str[:-2]
```


```python
# Display results in a DataFrame
id_combined = pd.DataFrame({'id_before': id_before,
                            'id_float':id_float,
                            'id_after':id_after})
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
      <th>16</th>
      <td>9322541199354739</td>
      <td>9.322541e+15</td>
      <td>9322541199354740</td>
    </tr>
    <tr>
      <th>40</th>
      <td>9157291833439925</td>
      <td>9.157292e+15</td>
      <td>9157291833439924</td>
    </tr>
    <tr>
      <th>42</th>
      <td>9925796753479323</td>
      <td>9.925797e+15</td>
      <td>9925796753479324</td>
    </tr>
    <tr>
      <th>78</th>
      <td>9331919189715753</td>
      <td>9.331919e+15</td>
      <td>9331919189715752</td>
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
fusion_1996.head()
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
      <td>18784.0</td>
      <td>8</td>
      <td>1513</td>
      <td>88</td>
      <td>5</td>
      <td>10153</td>
      <td>1773</td>
      <td>0</td>
      <td>0</td>
      <td>72243</td>
      <td>12614</td>
      <td>0</td>
      <td>0</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>13452.0</td>
      <td>13</td>
      <td>1920</td>
      <td>11</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>24271</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>12601.0</td>
      <td>13</td>
      <td>3311</td>
      <td>21</td>
      <td>3</td>
      <td>36210</td>
      <td>1350</td>
      <td>2800</td>
      <td>210</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>11935.0</td>
      <td>13</td>
      <td>2519</td>
      <td>16</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>12596</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>12335.0</td>
      <td>13</td>
      <td>3610</td>
      <td>39</td>
      <td>10</td>
      <td>117964</td>
      <td>6752</td>
      <td>14963</td>
      <td>562</td>
      <td>74800</td>
      <td>3938</td>
      <td>0</td>
      <td>0</td>
      <td>1.0</td>
    </tr>
  </tbody>
</table>
</div>




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

```


```python
# Merge using validate, expecting 1:1
fusion_merged = pd.merge(fusion_1995, fusion_1996, on="NUI", suffixes = ("_1995", "_1996"), how = "outer", validate = "1:1")
```


    ---------------------------------------------------------------------------

    MergeError                                Traceback (most recent call last)

    Cell In[42], line 2
          1 # Merge using validate, expecting 1:1
    ----> 2 fusion_merged = pd.merge(fusion_1995, fusion_1996, on="NUI", suffixes = ("_1995", "_1996"), how = "outer", validate = "1:1")
    

    File ~\anaconda3\Lib\site-packages\pandas\core\reshape\merge.py:170, in merge(left, right, how, on, left_on, right_on, left_index, right_index, sort, suffixes, copy, indicator, validate)
        155     return _cross_merge(
        156         left_df,
        157         right_df,
       (...)
        167         copy=copy,
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
    

    File ~\anaconda3\Lib\site-packages\pandas\core\reshape\merge.py:1657, in _MergeOperation._validate_validate_kwd(self, validate)
       1653         raise MergeError(
       1654             "Merge keys are not unique in left dataset; not a one-to-one merge"
       1655         )
       1656     if not right_unique:
    -> 1657         raise MergeError(
       1658             "Merge keys are not unique in right dataset; not a one-to-one merge"
       1659         )
       1661 elif validate in ["one_to_many", "1:m"]:
       1662     if not left_unique:
    

    MergeError: Merge keys are not unique in right dataset; not a one-to-one merge



```python
# Try Except to save ourselves
try:
    fusion_merged = pd.merge(fusion_1995, fusion_1996, on="NUI", suffixes = ("_1995", "_1996"), how = "outer", validate = "1:1")
except pd.errors.MergeError as e:
    print('WARNING:', e, '-> NUI duplicates dropped\n')
    fusion_merged = pd.merge(fusion_1995, fusion_1996, how="outer", on = "NUI", suffixes = ("_1995", "_1996"))
    fusion_merged = fusion_merged.drop_duplicates(subset="NUI", keep = False)

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
      <th>103</th>
      <td>23429.0</td>
      <td>13.0</td>
      <td>2520.0</td>
      <td>39.0</td>
      <td>0.0</td>
      <td>7990.0</td>
      <td>790.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>25334.0</td>
      <td>...</td>
      <td>0.0</td>
      <td>10931.0</td>
      <td>869.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>58519.0</td>
      <td>4261.0</td>
      <td>2.0</td>
      <td>0.0</td>
      <td>0.0</td>
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
<p>108 rows × 27 columns</p>
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
print(movies.head())
print(ratings.head())
```

       movieId                               title  \
    0        1                    Toy Story (1995)   
    1        2                      Jumanji (1995)   
    2        3             Grumpier Old Men (1995)   
    3        4            Waiting to Exhale (1995)   
    4        5  Father of the Bride Part II (1995)   
    
                                            genres  
    0  Adventure|Animation|Children|Comedy|Fantasy  
    1                   Adventure|Children|Fantasy  
    2                               Comedy|Romance  
    3                         Comedy|Drama|Romance  
    4                                       Comedy  
       userId  movieId  rating  timestamp
    0       1        1     4.0  964982703
    1       1        3     4.0  964981247
    2       1        6     4.0  964982224
    3       1       47     5.0  964983815
    4       1       50     5.0  964982931
    


```python
# Merge to create ratings and genre, using validate
ratings_with_genre = pd.merge(movies, ratings, on="movieId", validate="1:m", how="outer", indicator=True)
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
      <th>movieId</th>
      <th>title</th>
      <th>genres</th>
      <th>userId</th>
      <th>rating</th>
      <th>timestamp</th>
      <th>_merge</th>
    </tr>
  </thead>
  <tbody>
  </tbody>
</table>
</div>




```python
# Check out which entries are left or right only
ratings_with_genre[ratings_with_genre["_merge"] == "right_only"]
ratings_with_genre[ratings_with_genre["_merge"] == "left_only"]
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
      <th>movieId</th>
      <th>title</th>
      <th>genres</th>
      <th>userId</th>
      <th>rating</th>
      <th>timestamp</th>
      <th>_merge</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>22820</th>
      <td>1076</td>
      <td>Innocents, The (1961)</td>
      <td>Drama|Horror|Thriller</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>left_only</td>
    </tr>
    <tr>
      <th>49539</th>
      <td>2939</td>
      <td>Niagara (1953)</td>
      <td>Drama|Thriller</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>left_only</td>
    </tr>
    <tr>
      <th>53555</th>
      <td>3338</td>
      <td>For All Mankind (1989)</td>
      <td>Documentary</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>left_only</td>
    </tr>
    <tr>
      <th>54467</th>
      <td>3456</td>
      <td>Color of Paradise, The (Rang-e khoda) (1999)</td>
      <td>Drama</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>left_only</td>
    </tr>
    <tr>
      <th>60535</th>
      <td>4194</td>
      <td>I Know Where I'm Going! (1945)</td>
      <td>Drama|Romance|War</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>left_only</td>
    </tr>
    <tr>
      <th>68396</th>
      <td>5721</td>
      <td>Chosen, The (1981)</td>
      <td>Drama</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>left_only</td>
    </tr>
    <tr>
      <th>71896</th>
      <td>6668</td>
      <td>Road Home, The (Wo de fu qin mu qin) (1999)</td>
      <td>Drama|Romance</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>left_only</td>
    </tr>
    <tr>
      <th>72428</th>
      <td>6849</td>
      <td>Scrooge (1970)</td>
      <td>Drama|Fantasy|Musical</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>left_only</td>
    </tr>
    <tr>
      <th>73354</th>
      <td>7020</td>
      <td>Proof (1991)</td>
      <td>Comedy|Drama|Romance</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>left_only</td>
    </tr>
    <tr>
      <th>75450</th>
      <td>7792</td>
      <td>Parallax View, The (1974)</td>
      <td>Thriller</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>left_only</td>
    </tr>
    <tr>
      <th>76859</th>
      <td>8765</td>
      <td>This Gun for Hire (1942)</td>
      <td>Crime|Film-Noir|Thriller</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>left_only</td>
    </tr>
    <tr>
      <th>77983</th>
      <td>25855</td>
      <td>Roaring Twenties, The (1939)</td>
      <td>Crime|Drama|Thriller</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>left_only</td>
    </tr>
    <tr>
      <th>78026</th>
      <td>26085</td>
      <td>Mutiny on the Bounty (1962)</td>
      <td>Adventure|Drama|Romance</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>left_only</td>
    </tr>
    <tr>
      <th>79080</th>
      <td>30892</td>
      <td>In the Realms of the Unreal (2004)</td>
      <td>Animation|Documentary</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>left_only</td>
    </tr>
    <tr>
      <th>79426</th>
      <td>32160</td>
      <td>Twentieth Century (1934)</td>
      <td>Comedy</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>left_only</td>
    </tr>
    <tr>
      <th>79459</th>
      <td>32371</td>
      <td>Call Northside 777 (1948)</td>
      <td>Crime|Drama|Film-Noir</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>left_only</td>
    </tr>
    <tr>
      <th>80506</th>
      <td>34482</td>
      <td>Browning Version, The (1951)</td>
      <td>Drama</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>left_only</td>
    </tr>
    <tr>
      <th>92639</th>
      <td>85565</td>
      <td>Chalet Girl (2011)</td>
      <td>Comedy|Romance</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>left_only</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Re-run to exclude unmatched observations
ratings_with_genre = pd.merge(movies, ratings, on="movieId", validate="1:m", how="inner")
ratings_with_genre
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
      <th>movieId</th>
      <th>title</th>
      <th>genres</th>
      <th>userId</th>
      <th>rating</th>
      <th>timestamp</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>Toy Story (1995)</td>
      <td>Adventure|Animation|Children|Comedy|Fantasy</td>
      <td>1</td>
      <td>4.0</td>
      <td>964982703</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>Toy Story (1995)</td>
      <td>Adventure|Animation|Children|Comedy|Fantasy</td>
      <td>5</td>
      <td>4.0</td>
      <td>847434962</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1</td>
      <td>Toy Story (1995)</td>
      <td>Adventure|Animation|Children|Comedy|Fantasy</td>
      <td>7</td>
      <td>4.5</td>
      <td>1106635946</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1</td>
      <td>Toy Story (1995)</td>
      <td>Adventure|Animation|Children|Comedy|Fantasy</td>
      <td>15</td>
      <td>2.5</td>
      <td>1510577970</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1</td>
      <td>Toy Story (1995)</td>
      <td>Adventure|Animation|Children|Comedy|Fantasy</td>
      <td>17</td>
      <td>4.5</td>
      <td>1305696483</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>100831</th>
      <td>193581</td>
      <td>Black Butler: Book of the Atlantic (2017)</td>
      <td>Action|Animation|Comedy|Fantasy</td>
      <td>184</td>
      <td>4.0</td>
      <td>1537109082</td>
    </tr>
    <tr>
      <th>100832</th>
      <td>193583</td>
      <td>No Game No Life: Zero (2017)</td>
      <td>Animation|Comedy|Fantasy</td>
      <td>184</td>
      <td>3.5</td>
      <td>1537109545</td>
    </tr>
    <tr>
      <th>100833</th>
      <td>193585</td>
      <td>Flint (2017)</td>
      <td>Drama</td>
      <td>184</td>
      <td>3.5</td>
      <td>1537109805</td>
    </tr>
    <tr>
      <th>100834</th>
      <td>193587</td>
      <td>Bungo Stray Dogs: Dead Apple (2018)</td>
      <td>Action|Animation</td>
      <td>184</td>
      <td>3.5</td>
      <td>1537110021</td>
    </tr>
    <tr>
      <th>100835</th>
      <td>193609</td>
      <td>Andrew Dice Clay: Dice Rules (1991)</td>
      <td>Comedy</td>
      <td>331</td>
      <td>4.0</td>
      <td>1537157606</td>
    </tr>
  </tbody>
</table>
<p>100836 rows × 6 columns</p>
</div>




```python
# Ratings by Genre - does this make sense?
print("Descriptive Statistics for Comedies:")
print(ratings_with_genre[ratings_with_genre['genres']=="Comedy"]['rating'].describe())
print("Descriptive Statistics for Drama:")
print(ratings_with_genre[ratings_with_genre['genres']=="Drama"]['rating'].describe())
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
    Descriptive Statistics for Drama:
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
print("Descriptive Statistics for Comedies:")
print(ratings_with_genre[ratings_with_genre['genres'].str.contains("Comedy")]['rating'].describe())
print("Descriptive Statistics for Drama:")
print(ratings_with_genre[ratings_with_genre['genres'].str.contains("Drama")]['rating'].describe())
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
    Descriptive Statistics for Drama:
    count    41928.000000
    mean         3.656184
    std          0.979133
    min          0.500000
    25%          3.000000
    50%          4.000000
    75%          4.500000
    max          5.000000
    Name: rating, dtype: float64
    
