---
layout: single
sitemap: false
permalink: /pages/Econ_390_SP26_L12/
---

[Download Jupyter Notebook Empty](https://m-mcmain.github.io/files/Econ390SP26/Lectures/Lecture12_PandasCalculations_empty.ipynb)

[Download Jupyter Notebook Completed](https://m-mcmain.github.io/files/Econ390SP26/Lectures/Lecture12_PandasCalculations_full.ipynb)

# Econ 390 - Lecture 12: Pandas Calculations
Today we will start applying all of the knowledge we've accumulated since the beginning of the semester to actually get our hands dirty and work with the data! The [Working With Data Chapter from Turrell](https://aeturrell.github.io/coding-for-economists/data-intro.html#) and [5.2](https://wesmckinney.com/book/pandas-basics#pandas_frame)-[5.3](https://wesmckinney.com/book/pandas-basics#pandas_summarize) in McKinney are what is closest to this topic among the textbooks. We will be expanding on the Chilean Manufacturing Survey data from last time.

![Econ Exam Prep](https://m-mcmain.github.io/files/Econ390SP26/announcements/ExamPrepforEconStudentsWorkshop.jpg)
![Econ Internship Workshop](https://m-mcmain.github.io/files/Econ390SP26/announcements/InternshipPreparationWorkshop.png)
![CROWE John Sailer](https://m-mcmain.github.io/files/Econ390SP26/announcements/CROWEJohnSailer.jpg)

## Setting up the Data


```python
# Import packages
import os, pandas as pd
website = "https://m-mcmain.github.io/files/Econ390SP26/"
os.getcwd()
```




    'C:\\Users\\micha\\OneDrive\\Documents\\PhD\\Teaching\\Econ 390 - SP26\\Lecture 12'




```python
# Read in df
ENIA_1995 = pd.read_stata(website + "FUSION_annual_1995_EMP.dta", index_col = "NUI")
ENIA_1995.head()
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
    <tr>
      <th>NUI</th>
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
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>10082.0</th>
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
      <th>10101.0</th>
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
      <th>10103.0</th>
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
      <th>10178.0</th>
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
      <th>10220.0</th>
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
  </tbody>
</table>
</div>




```python
# Or set the index
```


```python
# Subset just the columns of interest
ENIA_1995_emps = ENIA_1995.loc[:, ["TOTHOM", "TOTMUJ", "TOHSC", "TOMSC"]]
ENIA_1995_emps.head()
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
      <th>TOTHOM</th>
      <th>TOTMUJ</th>
      <th>TOHSC</th>
      <th>TOMSC</th>
    </tr>
    <tr>
      <th>NUI</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>10082.0</th>
      <td>14</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>10101.0</th>
      <td>427</td>
      <td>25</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>10103.0</th>
      <td>46</td>
      <td>6</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>10178.0</th>
      <td>39</td>
      <td>35</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>10220.0</th>
      <td>481</td>
      <td>15</td>
      <td>0</td>
      <td>0</td>
    </tr>
  </tbody>
</table>
</div>



## Operations


```python
# Looping through to get total employment
ENIA_1995_total_emps = pd.Series(0, index = ENIA_1995_emps.columns)
for emp_type in ENIA_1995_emps.columns:
    for firm in ENIA_1995_emps.index:
        ENIA_1995_total_emps[emp_type] += ENIA_1995_emps.loc[firm, emp_type]

ENIA_1995_total_emps
```




    TOTHOM    7354
    TOTMUJ    2185
    TOHSC       72
    TOMSC       31
    dtype: int64




```python
# Or use a method
ENIA_1995_emps.sum(axis="rows")
```




    TOTHOM    7354
    TOTMUJ    2185
    TOHSC       72
    TOMSC       31
    dtype: int64




```python
%%timeit
# Test efficiency of the cell
ENIA_1995_total_emps = pd.Series(0, index = ENIA_1995_emps.columns)
for emp_type in ENIA_1995_emps.columns:
    for firm in ENIA_1995_emps.index:
        ENIA_1995_total_emps[emp_type] += ENIA_1995_emps.loc[firm, emp_type]
```

    13.2 ms ± 1.35 ms per loop (mean ± std. dev. of 7 runs, 100 loops each)
    


```python
%%timeit
# Compare it to this
ENIA_1995_emps.sum(axis="rows")
```

    159 μs ± 10.8 μs per loop (mean ± std. dev. of 7 runs, 10,000 loops each)
    


```python
# All in one line
ENIA_1995.loc[:, ["TOTHOM", "TOTMUJ", "TOHSC", "TOMSC"]].sum(axis="rows")
```




    TOTHOM    7354
    TOTMUJ    2185
    TOHSC       72
    TOMSC       31
    dtype: int64




```python
# Create a new column in the original dataset
ENIA_1995["total_emps"] = ENIA_1995_emps.sum(axis="columns")
print(ENIA_1995)
print(ENIA_1995_emps)
```

             REGION  CIIU3  TOTHOM  TOTMUJ   REMEMP  REGEMP  REMCOM  REGCOM  \
    NUI                                                                       
    10082.0       2   3610      14       1     7466       0       0       0   
    10101.0       2   2720     427      25  2046170  184590       0       0   
    10103.0       2   1531      46       6   135873    3426   69814    2912   
    10178.0       4   1512      39      35    22958    1886       0       0   
    10220.0       5   3312     481      15   554636  187853       0       0   
    ...         ...    ...     ...     ...      ...     ...     ...     ...   
    23429.0      13   2520      39       0     7990     790       0       0   
    23437.0      13   2520      81       6    88656    1432    3284       0   
    23449.0       6   2924     145       0   914130   54126       0       0   
    40088.0       8   3693       3       3    13495     271       0       0   
    40172.0       1   2022      31       5     6205    1284    2634     545   
    
             REMOBR  REGOBR  TOHSC  TOMSC  EXPORTADOS  total_emps  
    NUI                                                            
    10082.0   20174     600      0      0         0.0          15  
    10101.0  810717  216003      0      0         1.0         452  
    10103.0   37037    3848      0      0         0.0          52  
    10178.0   40257    4394      0      0         0.0          74  
    10220.0  858571  290794      0      0         1.0         496  
    ...         ...     ...    ...    ...         ...         ...  
    23429.0   25334    3874      2      0         0.0          41  
    23437.0  117469    9895      9      0         1.0          96  
    23449.0  267928   31246      0      0         0.0         145  
    40088.0       0       0      0      0         0.0           6  
    40172.0   64776     484      0      0         0.0          36  
    
    [100 rows x 14 columns]
             TOTHOM  TOTMUJ  TOHSC  TOMSC
    NUI                                  
    10082.0      14       1      0      0
    10101.0     427      25      0      0
    10103.0      46       6      0      0
    10178.0      39      35      0      0
    10220.0     481      15      0      0
    ...         ...     ...    ...    ...
    23429.0      39       0      2      0
    23437.0      81       6      9      0
    23449.0     145       0      0      0
    40088.0       3       3      0      0
    40172.0      31       5      0      0
    
    [100 rows x 4 columns]
    


```python
# Similar for wages paid
ENIA_1995["total_wages"] = ENIA_1995.iloc[:,[4,5,6,7,8,9]].sum(axis = "columns")
ENIA_1995
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
      <th>total_emps</th>
      <th>total_wages</th>
    </tr>
    <tr>
      <th>NUI</th>
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
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>10082.0</th>
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
      <td>15</td>
      <td>28240</td>
    </tr>
    <tr>
      <th>10101.0</th>
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
      <td>452</td>
      <td>3257480</td>
    </tr>
    <tr>
      <th>10103.0</th>
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
      <td>52</td>
      <td>252910</td>
    </tr>
    <tr>
      <th>10178.0</th>
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
      <td>74</td>
      <td>69495</td>
    </tr>
    <tr>
      <th>10220.0</th>
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
      <td>496</td>
      <td>1891854</td>
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
      <th>23429.0</th>
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
      <td>41</td>
      <td>37988</td>
    </tr>
    <tr>
      <th>23437.0</th>
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
      <td>96</td>
      <td>220736</td>
    </tr>
    <tr>
      <th>23449.0</th>
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
      <td>145</td>
      <td>1267430</td>
    </tr>
    <tr>
      <th>40088.0</th>
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
      <td>6</td>
      <td>13766</td>
    </tr>
    <tr>
      <th>40172.0</th>
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
      <td>36</td>
      <td>75928</td>
    </tr>
  </tbody>
</table>
<p>100 rows × 15 columns</p>
</div>




```python
# Convert to USD
ENIA_1995["total_wages_dollar"] = ENIA_1995["total_wages"]/396.81
ENIA_1995
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
      <th>total_emps</th>
      <th>total_wages</th>
      <th>total_wages_dollar</th>
    </tr>
    <tr>
      <th>NUI</th>
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
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>10082.0</th>
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
      <td>15</td>
      <td>28240</td>
      <td>71.167561</td>
    </tr>
    <tr>
      <th>10101.0</th>
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
      <td>452</td>
      <td>3257480</td>
      <td>8209.168116</td>
    </tr>
    <tr>
      <th>10103.0</th>
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
      <td>52</td>
      <td>252910</td>
      <td>637.357929</td>
    </tr>
    <tr>
      <th>10178.0</th>
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
      <td>74</td>
      <td>69495</td>
      <td>175.134195</td>
    </tr>
    <tr>
      <th>10220.0</th>
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
      <td>496</td>
      <td>1891854</td>
      <td>4767.657065</td>
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
      <th>23429.0</th>
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
      <td>41</td>
      <td>37988</td>
      <td>95.733474</td>
    </tr>
    <tr>
      <th>23437.0</th>
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
      <td>96</td>
      <td>220736</td>
      <td>556.276304</td>
    </tr>
    <tr>
      <th>23449.0</th>
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
      <td>145</td>
      <td>1267430</td>
      <td>3194.047529</td>
    </tr>
    <tr>
      <th>40088.0</th>
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
      <td>6</td>
      <td>13766</td>
      <td>34.691666</td>
    </tr>
    <tr>
      <th>40172.0</th>
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
      <td>36</td>
      <td>75928</td>
      <td>191.345984</td>
    </tr>
  </tbody>
</table>
<p>100 rows × 16 columns</p>
</div>




```python
# Calculate average wages in USD
ENIA_1995["avg_wages_dollar"] = ENIA_1995["total_wages_dollar"]/ENIA_1995["total_emps"]
ENIA_1995
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
      <th>total_emps</th>
      <th>total_wages</th>
      <th>total_wages_dollar</th>
      <th>avg_wages_dollar</th>
    </tr>
    <tr>
      <th>NUI</th>
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
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>10082.0</th>
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
      <td>15</td>
      <td>28240</td>
      <td>71.167561</td>
      <td>4.744504</td>
    </tr>
    <tr>
      <th>10101.0</th>
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
      <td>452</td>
      <td>3257480</td>
      <td>8209.168116</td>
      <td>18.161876</td>
    </tr>
    <tr>
      <th>10103.0</th>
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
      <td>52</td>
      <td>252910</td>
      <td>637.357929</td>
      <td>12.256883</td>
    </tr>
    <tr>
      <th>10178.0</th>
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
      <td>74</td>
      <td>69495</td>
      <td>175.134195</td>
      <td>2.366678</td>
    </tr>
    <tr>
      <th>10220.0</th>
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
      <td>496</td>
      <td>1891854</td>
      <td>4767.657065</td>
      <td>9.612212</td>
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
    </tr>
    <tr>
      <th>23429.0</th>
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
      <td>41</td>
      <td>37988</td>
      <td>95.733474</td>
      <td>2.334963</td>
    </tr>
    <tr>
      <th>23437.0</th>
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
      <td>96</td>
      <td>220736</td>
      <td>556.276304</td>
      <td>5.794545</td>
    </tr>
    <tr>
      <th>23449.0</th>
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
      <td>145</td>
      <td>1267430</td>
      <td>3194.047529</td>
      <td>22.027914</td>
    </tr>
    <tr>
      <th>40088.0</th>
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
      <td>6</td>
      <td>13766</td>
      <td>34.691666</td>
      <td>5.781944</td>
    </tr>
    <tr>
      <th>40172.0</th>
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
      <td>36</td>
      <td>75928</td>
      <td>191.345984</td>
      <td>5.315166</td>
    </tr>
  </tbody>
</table>
<p>100 rows × 17 columns</p>
</div>




```python
# All employees in data?
ENIA_1995["total_emps"].sum()
```




    np.int64(9642)




```python
# Another way
ENIA_1995_emps.sum().sum()
```




    np.int64(9642)




```python
# Suppose we don't want to count 0's towards any measures
import numpy as np
ENIA_1995_cleaned = ENIA_1995.replace(0, np.nan)
ENIA_1995_cleaned
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
      <th>total_emps</th>
      <th>total_wages</th>
      <th>total_wages_dollar</th>
      <th>avg_wages_dollar</th>
    </tr>
    <tr>
      <th>NUI</th>
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
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>10082.0</th>
      <td>2</td>
      <td>3610</td>
      <td>14</td>
      <td>1.0</td>
      <td>7466.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>20174.0</td>
      <td>600.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>15</td>
      <td>28240</td>
      <td>71.167561</td>
      <td>4.744504</td>
    </tr>
    <tr>
      <th>10101.0</th>
      <td>2</td>
      <td>2720</td>
      <td>427</td>
      <td>25.0</td>
      <td>2046170.0</td>
      <td>184590.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>810717.0</td>
      <td>216003.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>452</td>
      <td>3257480</td>
      <td>8209.168116</td>
      <td>18.161876</td>
    </tr>
    <tr>
      <th>10103.0</th>
      <td>2</td>
      <td>1531</td>
      <td>46</td>
      <td>6.0</td>
      <td>135873.0</td>
      <td>3426.0</td>
      <td>69814.0</td>
      <td>2912.0</td>
      <td>37037.0</td>
      <td>3848.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>52</td>
      <td>252910</td>
      <td>637.357929</td>
      <td>12.256883</td>
    </tr>
    <tr>
      <th>10178.0</th>
      <td>4</td>
      <td>1512</td>
      <td>39</td>
      <td>35.0</td>
      <td>22958.0</td>
      <td>1886.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>40257.0</td>
      <td>4394.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>74</td>
      <td>69495</td>
      <td>175.134195</td>
      <td>2.366678</td>
    </tr>
    <tr>
      <th>10220.0</th>
      <td>5</td>
      <td>3312</td>
      <td>481</td>
      <td>15.0</td>
      <td>554636.0</td>
      <td>187853.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>858571.0</td>
      <td>290794.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>496</td>
      <td>1891854</td>
      <td>4767.657065</td>
      <td>9.612212</td>
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
    </tr>
    <tr>
      <th>23429.0</th>
      <td>13</td>
      <td>2520</td>
      <td>39</td>
      <td>NaN</td>
      <td>7990.0</td>
      <td>790.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>25334.0</td>
      <td>3874.0</td>
      <td>2.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>41</td>
      <td>37988</td>
      <td>95.733474</td>
      <td>2.334963</td>
    </tr>
    <tr>
      <th>23437.0</th>
      <td>13</td>
      <td>2520</td>
      <td>81</td>
      <td>6.0</td>
      <td>88656.0</td>
      <td>1432.0</td>
      <td>3284.0</td>
      <td>NaN</td>
      <td>117469.0</td>
      <td>9895.0</td>
      <td>9.0</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>96</td>
      <td>220736</td>
      <td>556.276304</td>
      <td>5.794545</td>
    </tr>
    <tr>
      <th>23449.0</th>
      <td>6</td>
      <td>2924</td>
      <td>145</td>
      <td>NaN</td>
      <td>914130.0</td>
      <td>54126.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>267928.0</td>
      <td>31246.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>145</td>
      <td>1267430</td>
      <td>3194.047529</td>
      <td>22.027914</td>
    </tr>
    <tr>
      <th>40088.0</th>
      <td>8</td>
      <td>3693</td>
      <td>3</td>
      <td>3.0</td>
      <td>13495.0</td>
      <td>271.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>6</td>
      <td>13766</td>
      <td>34.691666</td>
      <td>5.781944</td>
    </tr>
    <tr>
      <th>40172.0</th>
      <td>1</td>
      <td>2022</td>
      <td>31</td>
      <td>5.0</td>
      <td>6205.0</td>
      <td>1284.0</td>
      <td>2634.0</td>
      <td>545.0</td>
      <td>64776.0</td>
      <td>484.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>36</td>
      <td>75928</td>
      <td>191.345984</td>
      <td>5.315166</td>
    </tr>
  </tbody>
</table>
<p>100 rows × 17 columns</p>
</div>




```python
# Notice patterns
ENIA_1995.loc[:,ENIA_1995.columns.str.startswith("TO")].sum(axis="columns")
```




    NUI
    10082.0     15
    10101.0    452
    10103.0     52
    10178.0     74
    10220.0    496
              ... 
    23429.0     41
    23437.0     96
    23449.0    145
    40088.0      6
    40172.0     36
    Length: 100, dtype: int64




```python
# skipna option
ENIA_1995_cleaned.loc[:,ENIA_1995.columns.str.startswith("TO")].sum(axis="columns", skipna=False)
```




    NUI
    10082.0   NaN
    10101.0   NaN
    10103.0   NaN
    10178.0   NaN
    10220.0   NaN
               ..
    23429.0   NaN
    23437.0   NaN
    23449.0   NaN
    40088.0   NaN
    40172.0   NaN
    Length: 100, dtype: float64




```python
# May make sense more for some than others
```


```python
# Can take the mean across columns
print(ENIA_1995.iloc[:,2:].mean(axis="columns"),'\n')
# same for rows
print(ENIA_1995.mean(axis="rows"),'\n')

```

    NUI
    10082.0      3772.394138
    10101.0    434939.488666
    10103.0     33771.574321
    10178.0      9287.700058
    10220.0    252631.884618
                   ...      
    23429.0      5077.071229
    23437.0     29481.804723
    23449.0    169224.405030
    40088.0      1838.964907
    40172.0     10141.644077
    Length: 100, dtype: float64 
    
    REGION                     9.870000
    CIIU3                   2299.330000
    TOTHOM                    73.540000
    TOTMUJ                    21.850000
    REMEMP                132773.340000
    REGEMP                 13148.190000
    REMCOM                 12120.290000
    REGCOM                    93.190000
    REMOBR                124427.260000
    REGOBR                 15415.120000
    TOHSC                      0.720000
    TOMSC                      0.310000
    EXPORTADOS                 0.230000
    total_emps                96.420000
    total_wages           297977.390000
    total_wages_dollar       750.932159
    avg_wages_dollar           5.557475
    dtype: float64 
    
    


```python
# Maximum
ENIA_1995.max(axis="rows")
```




    REGION                1.300000e+01
    CIIU3                 3.699000e+03
    TOTHOM                6.970000e+02
    TOTMUJ                5.360000e+02
    REMEMP                2.824713e+06
    REGEMP                5.385980e+05
    REMCOM                8.398000e+05
    REGCOM                2.912000e+03
    REMOBR                1.153054e+06
    REGOBR                2.907940e+05
    TOHSC                 9.000000e+00
    TOMSC                 1.300000e+01
    EXPORTADOS            1.000000e+00
    total_emps            9.600000e+02
    total_wages           3.822586e+06
    total_wages_dollar    9.633290e+03
    avg_wages_dollar      2.202791e+01
    dtype: float64




```python
# Location of the max
ENIA_1995.loc[ENIA_1995.idxmax(axis="rows"),:]

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
      <th>total_emps</th>
      <th>total_wages</th>
      <th>total_wages_dollar</th>
      <th>avg_wages_dollar</th>
    </tr>
    <tr>
      <th>NUI</th>
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
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>11370.0</th>
      <td>13</td>
      <td>2211</td>
      <td>25</td>
      <td>4</td>
      <td>31415</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>17585</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0.0</td>
      <td>29</td>
      <td>49000</td>
      <td>123.484791</td>
      <td>4.258096</td>
    </tr>
    <tr>
      <th>18060.0</th>
      <td>8</td>
      <td>3699</td>
      <td>11</td>
      <td>1</td>
      <td>3965</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>6975</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0.0</td>
      <td>12</td>
      <td>10940</td>
      <td>27.569870</td>
      <td>2.297489</td>
    </tr>
    <tr>
      <th>12860.0</th>
      <td>13</td>
      <td>1541</td>
      <td>697</td>
      <td>124</td>
      <td>2824713</td>
      <td>538598</td>
      <td>0</td>
      <td>0</td>
      <td>423112</td>
      <td>36163</td>
      <td>0</td>
      <td>0</td>
      <td>0.0</td>
      <td>821</td>
      <td>3822586</td>
      <td>9633.290492</td>
      <td>11.733606</td>
    </tr>
    <tr>
      <th>11514.0</th>
      <td>13</td>
      <td>2424</td>
      <td>424</td>
      <td>536</td>
      <td>543084</td>
      <td>30465</td>
      <td>839800</td>
      <td>0</td>
      <td>1153054</td>
      <td>156739</td>
      <td>0</td>
      <td>0</td>
      <td>1.0</td>
      <td>960</td>
      <td>2723142</td>
      <td>6862.584108</td>
      <td>7.148525</td>
    </tr>
    <tr>
      <th>12860.0</th>
      <td>13</td>
      <td>1541</td>
      <td>697</td>
      <td>124</td>
      <td>2824713</td>
      <td>538598</td>
      <td>0</td>
      <td>0</td>
      <td>423112</td>
      <td>36163</td>
      <td>0</td>
      <td>0</td>
      <td>0.0</td>
      <td>821</td>
      <td>3822586</td>
      <td>9633.290492</td>
      <td>11.733606</td>
    </tr>
    <tr>
      <th>12860.0</th>
      <td>13</td>
      <td>1541</td>
      <td>697</td>
      <td>124</td>
      <td>2824713</td>
      <td>538598</td>
      <td>0</td>
      <td>0</td>
      <td>423112</td>
      <td>36163</td>
      <td>0</td>
      <td>0</td>
      <td>0.0</td>
      <td>821</td>
      <td>3822586</td>
      <td>9633.290492</td>
      <td>11.733606</td>
    </tr>
    <tr>
      <th>11514.0</th>
      <td>13</td>
      <td>2424</td>
      <td>424</td>
      <td>536</td>
      <td>543084</td>
      <td>30465</td>
      <td>839800</td>
      <td>0</td>
      <td>1153054</td>
      <td>156739</td>
      <td>0</td>
      <td>0</td>
      <td>1.0</td>
      <td>960</td>
      <td>2723142</td>
      <td>6862.584108</td>
      <td>7.148525</td>
    </tr>
    <tr>
      <th>10103.0</th>
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
      <td>52</td>
      <td>252910</td>
      <td>637.357929</td>
      <td>12.256883</td>
    </tr>
    <tr>
      <th>11514.0</th>
      <td>13</td>
      <td>2424</td>
      <td>424</td>
      <td>536</td>
      <td>543084</td>
      <td>30465</td>
      <td>839800</td>
      <td>0</td>
      <td>1153054</td>
      <td>156739</td>
      <td>0</td>
      <td>0</td>
      <td>1.0</td>
      <td>960</td>
      <td>2723142</td>
      <td>6862.584108</td>
      <td>7.148525</td>
    </tr>
    <tr>
      <th>10220.0</th>
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
      <td>496</td>
      <td>1891854</td>
      <td>4767.657065</td>
      <td>9.612212</td>
    </tr>
    <tr>
      <th>23437.0</th>
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
      <td>96</td>
      <td>220736</td>
      <td>556.276304</td>
      <td>5.794545</td>
    </tr>
    <tr>
      <th>16804.0</th>
      <td>13</td>
      <td>2520</td>
      <td>136</td>
      <td>107</td>
      <td>299957</td>
      <td>14189</td>
      <td>0</td>
      <td>0</td>
      <td>265916</td>
      <td>38777</td>
      <td>4</td>
      <td>13</td>
      <td>1.0</td>
      <td>260</td>
      <td>618839</td>
      <td>1559.534790</td>
      <td>5.998211</td>
    </tr>
    <tr>
      <th>10101.0</th>
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
      <td>452</td>
      <td>3257480</td>
      <td>8209.168116</td>
      <td>18.161876</td>
    </tr>
    <tr>
      <th>11514.0</th>
      <td>13</td>
      <td>2424</td>
      <td>424</td>
      <td>536</td>
      <td>543084</td>
      <td>30465</td>
      <td>839800</td>
      <td>0</td>
      <td>1153054</td>
      <td>156739</td>
      <td>0</td>
      <td>0</td>
      <td>1.0</td>
      <td>960</td>
      <td>2723142</td>
      <td>6862.584108</td>
      <td>7.148525</td>
    </tr>
    <tr>
      <th>12860.0</th>
      <td>13</td>
      <td>1541</td>
      <td>697</td>
      <td>124</td>
      <td>2824713</td>
      <td>538598</td>
      <td>0</td>
      <td>0</td>
      <td>423112</td>
      <td>36163</td>
      <td>0</td>
      <td>0</td>
      <td>0.0</td>
      <td>821</td>
      <td>3822586</td>
      <td>9633.290492</td>
      <td>11.733606</td>
    </tr>
    <tr>
      <th>12860.0</th>
      <td>13</td>
      <td>1541</td>
      <td>697</td>
      <td>124</td>
      <td>2824713</td>
      <td>538598</td>
      <td>0</td>
      <td>0</td>
      <td>423112</td>
      <td>36163</td>
      <td>0</td>
      <td>0</td>
      <td>0.0</td>
      <td>821</td>
      <td>3822586</td>
      <td>9633.290492</td>
      <td>11.733606</td>
    </tr>
    <tr>
      <th>23449.0</th>
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
      <td>145</td>
      <td>1267430</td>
      <td>3194.047529</td>
      <td>22.027914</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Cumulative Sum
ENIA_1995.cumsum(axis="rows")
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
      <th>total_emps</th>
      <th>total_wages</th>
      <th>total_wages_dollar</th>
      <th>avg_wages_dollar</th>
    </tr>
    <tr>
      <th>NUI</th>
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
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>10082.0</th>
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
      <td>15</td>
      <td>28240</td>
      <td>71.167561</td>
      <td>4.744504</td>
    </tr>
    <tr>
      <th>10101.0</th>
      <td>4</td>
      <td>6330</td>
      <td>441</td>
      <td>26</td>
      <td>2053636</td>
      <td>184590</td>
      <td>0</td>
      <td>0</td>
      <td>830891</td>
      <td>216603</td>
      <td>0</td>
      <td>0</td>
      <td>1.0</td>
      <td>467</td>
      <td>3285720</td>
      <td>8280.335677</td>
      <td>22.906380</td>
    </tr>
    <tr>
      <th>10103.0</th>
      <td>6</td>
      <td>7861</td>
      <td>487</td>
      <td>32</td>
      <td>2189509</td>
      <td>188016</td>
      <td>69814</td>
      <td>2912</td>
      <td>867928</td>
      <td>220451</td>
      <td>0</td>
      <td>0</td>
      <td>1.0</td>
      <td>519</td>
      <td>3538630</td>
      <td>8917.693607</td>
      <td>35.163264</td>
    </tr>
    <tr>
      <th>10178.0</th>
      <td>10</td>
      <td>9373</td>
      <td>526</td>
      <td>67</td>
      <td>2212467</td>
      <td>189902</td>
      <td>69814</td>
      <td>2912</td>
      <td>908185</td>
      <td>224845</td>
      <td>0</td>
      <td>0</td>
      <td>1.0</td>
      <td>593</td>
      <td>3608125</td>
      <td>9092.827802</td>
      <td>37.529942</td>
    </tr>
    <tr>
      <th>10220.0</th>
      <td>15</td>
      <td>12685</td>
      <td>1007</td>
      <td>82</td>
      <td>2767103</td>
      <td>377755</td>
      <td>69814</td>
      <td>2912</td>
      <td>1766756</td>
      <td>515639</td>
      <td>0</td>
      <td>0</td>
      <td>2.0</td>
      <td>1089</td>
      <td>5499979</td>
      <td>13860.484867</td>
      <td>47.142154</td>
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
    </tr>
    <tr>
      <th>23429.0</th>
      <td>959</td>
      <td>218774</td>
      <td>7094</td>
      <td>2171</td>
      <td>12254848</td>
      <td>1257706</td>
      <td>1206111</td>
      <td>8774</td>
      <td>11992553</td>
      <td>1499887</td>
      <td>63</td>
      <td>31</td>
      <td>22.0</td>
      <td>9359</td>
      <td>28219879</td>
      <td>71116.854414</td>
      <td>516.827962</td>
    </tr>
    <tr>
      <th>23437.0</th>
      <td>972</td>
      <td>221294</td>
      <td>7175</td>
      <td>2177</td>
      <td>12343504</td>
      <td>1259138</td>
      <td>1209395</td>
      <td>8774</td>
      <td>12110022</td>
      <td>1509782</td>
      <td>72</td>
      <td>31</td>
      <td>23.0</td>
      <td>9455</td>
      <td>28440615</td>
      <td>71673.130717</td>
      <td>522.622506</td>
    </tr>
    <tr>
      <th>23449.0</th>
      <td>978</td>
      <td>224218</td>
      <td>7320</td>
      <td>2177</td>
      <td>13257634</td>
      <td>1313264</td>
      <td>1209395</td>
      <td>8774</td>
      <td>12377950</td>
      <td>1541028</td>
      <td>72</td>
      <td>31</td>
      <td>23.0</td>
      <td>9600</td>
      <td>29708045</td>
      <td>74867.178247</td>
      <td>544.650420</td>
    </tr>
    <tr>
      <th>40088.0</th>
      <td>986</td>
      <td>227911</td>
      <td>7323</td>
      <td>2180</td>
      <td>13271129</td>
      <td>1313535</td>
      <td>1209395</td>
      <td>8774</td>
      <td>12377950</td>
      <td>1541028</td>
      <td>72</td>
      <td>31</td>
      <td>23.0</td>
      <td>9606</td>
      <td>29721811</td>
      <td>74901.869913</td>
      <td>550.432365</td>
    </tr>
    <tr>
      <th>40172.0</th>
      <td>987</td>
      <td>229933</td>
      <td>7354</td>
      <td>2185</td>
      <td>13277334</td>
      <td>1314819</td>
      <td>1212029</td>
      <td>9319</td>
      <td>12442726</td>
      <td>1541512</td>
      <td>72</td>
      <td>31</td>
      <td>23.0</td>
      <td>9642</td>
      <td>29797739</td>
      <td>75093.215897</td>
      <td>555.747531</td>
    </tr>
  </tbody>
</table>
<p>100 rows × 17 columns</p>
</div>



## Practice - Additional Calculations
1. Check out var, std, rank, quantile, mode in `ENIA_1995`
   - Hint: Standard Devation is the square root of Variance


```python
# Results
print(ENIA_1995.var())
print(ENIA_1995.var()**0.5)
print(ENIA_1995.rank())
print(ENIA_1995.quantile(0.75))
print(ENIA_1995.mode())
```

    REGION                1.455869e+01
    CIIU3                 4.226737e+05
    TOTHOM                1.535795e+04
    TOTMUJ                3.838129e+03
    REMEMP                1.406199e+11
    REGEMP                3.579953e+09
    REMCOM                7.401164e+09
    REGCOM                1.659427e+05
    REMOBR                4.534774e+10
    REGOBR                1.891608e+09
    TOHSC                 3.476364e+00
    TOMSC                 2.801919e+00
    EXPORTADOS            1.788890e-01
    total_emps            2.680798e+04
    total_wages           4.112845e+11
    total_wages_dollar    2.612024e+06
    avg_wages_dollar      1.427533e+01
    dtype: float64
    REGION                     3.815585
    CIIU3                    650.133631
    TOTHOM                   123.927188
    TOTMUJ                    61.952633
    REMEMP                374993.201307
    REGEMP                 59832.708717
    REMCOM                 86030.018852
    REGCOM                   407.360702
    REMOBR                212950.097592
    REGOBR                 43492.624163
    TOHSC                      1.864501
    TOMSC                      1.673893
    EXPORTADOS                 0.422953
    total_emps               163.731437
    total_wages           641314.677257
    total_wages_dollar      1616.175694
    avg_wages_dollar           3.778271
    dtype: float64
             REGION  CIIU3  TOTHOM  TOTMUJ  REMEMP  REGEMP  REMCOM  REGCOM  \
    NUI                                                                      
    10082.0     5.5   95.5    26.5    19.0    30.0    17.0    44.5    46.5   
    10101.0     5.5   73.0    97.0    83.0    99.0    98.0    44.5    46.5   
    10103.0     5.5    9.0    68.0    64.0    81.0    79.0    98.0   100.0   
    10178.0    11.0    5.0    60.5    88.0    63.0    69.0    44.5    46.5   
    10220.0    16.0   92.0    98.0    75.0    96.0    99.0    44.5    46.5   
    ...         ...    ...     ...     ...     ...     ...     ...     ...   
    23429.0    74.0   61.0    60.5     6.5    32.0    53.0    44.5    46.5   
    23437.0    74.0   61.0    79.5    64.0    75.0    61.0    91.0    46.5   
    23449.0    18.0   88.5    88.0     6.5    98.0    96.0    44.5    46.5   
    40088.0    32.5   98.0     2.0    43.5    51.0    44.0    44.5    46.5   
    40172.0     2.0   46.5    57.0    58.5    29.0    60.0    90.0    95.0   
    
             REMOBR  REGOBR  TOHSC  TOMSC  EXPORTADOS  total_emps  total_wages  \
    NUI                                                                          
    10082.0    32.0    42.0   41.0   47.5        39.0        18.5         28.0   
    10101.0    97.0    99.0   41.0   47.5        89.0        96.0         99.0   
    10103.0    53.0    61.0   41.0   47.5        39.0        63.0         77.0   
    10178.0    54.0    64.0   41.0   47.5        39.0        69.0         55.0   
    10220.0    98.0   100.0   41.0   47.5        89.0        97.0         96.0   
    ...         ...     ...    ...    ...         ...         ...          ...   
    23429.0    41.0    62.0   87.5   47.5        39.0        52.5         37.0   
    23437.0    74.0    76.0  100.0   47.5        89.0        77.0         73.0   
    23449.0    89.0    89.0   41.0   47.5        39.0        85.0         95.0   
    40088.0     1.5    15.5   41.0   47.5        39.0         1.5         11.0   
    40172.0    64.0    38.0   41.0   47.5        39.0        48.0         59.0   
    
             total_wages_dollar  avg_wages_dollar  
    NUI                                            
    10082.0                28.0              50.0  
    10101.0                99.0              98.0  
    10103.0                77.0              94.0  
    10178.0                55.0              13.0  
    10220.0                96.0              90.0  
    ...                     ...               ...  
    23429.0                37.0              12.0  
    23437.0                73.0              67.0  
    23449.0                95.0             100.0  
    40088.0                11.0              64.0  
    40172.0                59.0              62.0  
    
    [100 rows x 17 columns]
    REGION                    13.000000
    CIIU3                   2811.000000
    TOTHOM                    66.500000
    TOTMUJ                    15.000000
    REMEMP                 89191.750000
    REGEMP                  2748.000000
    REMCOM                     0.000000
    REGCOM                     0.000000
    REMOBR                132897.750000
    REGOBR                  9401.500000
    TOHSC                      0.000000
    TOMSC                      0.000000
    EXPORTADOS                 0.000000
    total_emps                91.750000
    total_wages           245282.750000
    total_wages_dollar       618.136514
    avg_wages_dollar           6.642960
    Name: 0.75, dtype: float64
        REGION   CIIU3  TOTHOM  TOTMUJ  REMEMP  REGEMP  REMCOM  REGCOM  REMOBR  \
    0     13.0  1541.0    14.0     2.0     0.0     0.0     0.0     0.0     0.0   
    1      NaN     NaN     NaN     NaN     NaN     NaN     NaN     NaN     NaN   
    2      NaN     NaN     NaN     NaN     NaN     NaN     NaN     NaN     NaN   
    3      NaN     NaN     NaN     NaN     NaN     NaN     NaN     NaN     NaN   
    4      NaN     NaN     NaN     NaN     NaN     NaN     NaN     NaN     NaN   
    ..     ...     ...     ...     ...     ...     ...     ...     ...     ...   
    95     NaN     NaN     NaN     NaN     NaN     NaN     NaN     NaN     NaN   
    96     NaN     NaN     NaN     NaN     NaN     NaN     NaN     NaN     NaN   
    97     NaN     NaN     NaN     NaN     NaN     NaN     NaN     NaN     NaN   
    98     NaN     NaN     NaN     NaN     NaN     NaN     NaN     NaN     NaN   
    99     NaN     NaN     NaN     NaN     NaN     NaN     NaN     NaN     NaN   
    
        REGOBR  TOHSC  TOMSC  EXPORTADOS  total_emps  total_wages  \
    0      0.0    0.0    0.0         0.0        13.0         7115   
    1      NaN    NaN    NaN         NaN        15.0         7948   
    2      NaN    NaN    NaN         NaN        17.0         8688   
    3      NaN    NaN    NaN         NaN        21.0         9250   
    4      NaN    NaN    NaN         NaN         NaN        10907   
    ..     ...    ...    ...         ...         ...          ...   
    95     NaN    NaN    NaN         NaN         NaN      1891854   
    96     NaN    NaN    NaN         NaN         NaN      2073025   
    97     NaN    NaN    NaN         NaN         NaN      2723142   
    98     NaN    NaN    NaN         NaN         NaN      3257480   
    99     NaN    NaN    NaN         NaN         NaN      3822586   
    
        total_wages_dollar  avg_wages_dollar  
    0            17.930496          0.973643  
    1            20.029737          1.473063  
    2            21.894610          1.554060  
    3            23.310904          1.563901  
    4            27.486706          1.630045  
    ..                 ...               ...  
    95         4767.657065         13.043251  
    96         5224.225700         13.597048  
    97         6862.584108         18.161876  
    98         8209.168116         21.142532  
    99         9633.290492         22.027914  
    
    [100 rows x 17 columns]
    

## Descriptive Statistics and Tables


```python
# Convert to string
ENIA_1995["REGION"] = ENIA_1995["REGION"].apply(str)
ENIA_1995["CIIU3"] = ENIA_1995["CIIU3"].apply(str)
ENIA_1995
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
      <th>total_emps</th>
      <th>total_wages</th>
      <th>total_wages_dollar</th>
      <th>avg_wages_dollar</th>
    </tr>
    <tr>
      <th>NUI</th>
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
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>10082.0</th>
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
      <td>15</td>
      <td>28240</td>
      <td>71.167561</td>
      <td>4.744504</td>
    </tr>
    <tr>
      <th>10101.0</th>
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
      <td>452</td>
      <td>3257480</td>
      <td>8209.168116</td>
      <td>18.161876</td>
    </tr>
    <tr>
      <th>10103.0</th>
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
      <td>52</td>
      <td>252910</td>
      <td>637.357929</td>
      <td>12.256883</td>
    </tr>
    <tr>
      <th>10178.0</th>
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
      <td>74</td>
      <td>69495</td>
      <td>175.134195</td>
      <td>2.366678</td>
    </tr>
    <tr>
      <th>10220.0</th>
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
      <td>496</td>
      <td>1891854</td>
      <td>4767.657065</td>
      <td>9.612212</td>
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
    </tr>
    <tr>
      <th>23429.0</th>
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
      <td>41</td>
      <td>37988</td>
      <td>95.733474</td>
      <td>2.334963</td>
    </tr>
    <tr>
      <th>23437.0</th>
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
      <td>96</td>
      <td>220736</td>
      <td>556.276304</td>
      <td>5.794545</td>
    </tr>
    <tr>
      <th>23449.0</th>
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
      <td>145</td>
      <td>1267430</td>
      <td>3194.047529</td>
      <td>22.027914</td>
    </tr>
    <tr>
      <th>40088.0</th>
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
      <td>6</td>
      <td>13766</td>
      <td>34.691666</td>
      <td>5.781944</td>
    </tr>
    <tr>
      <th>40172.0</th>
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
      <td>36</td>
      <td>75928</td>
      <td>191.345984</td>
      <td>5.315166</td>
    </tr>
  </tbody>
</table>
<p>100 rows × 17 columns</p>
</div>




```python
# the describe method
ENIA_1995["REGION"].describe()
```




    count     100
    unique     11
    top        13
    freq       53
    Name: REGION, dtype: object




```python
# Find counts of values
ENIA_1995["REGION"].value_counts()
```




    REGION
    13    53
    8     18
    4      7
    7      5
    2      4
    5      3
    9      3
    1      3
    10     2
    12     1
    6      1
    Name: count, dtype: int64




```python
# Make it a DataFrame
pd.crosstab(ENIA_1995["REGION"],"count")
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
      <th>count</th>
    </tr>
    <tr>
      <th>REGION</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>3</td>
    </tr>
    <tr>
      <th>10</th>
      <td>2</td>
    </tr>
    <tr>
      <th>12</th>
      <td>1</td>
    </tr>
    <tr>
      <th>13</th>
      <td>53</td>
    </tr>
    <tr>
      <th>2</th>
      <td>4</td>
    </tr>
    <tr>
      <th>4</th>
      <td>7</td>
    </tr>
    <tr>
      <th>5</th>
      <td>3</td>
    </tr>
    <tr>
      <th>6</th>
      <td>1</td>
    </tr>
    <tr>
      <th>7</th>
      <td>5</td>
    </tr>
    <tr>
      <th>8</th>
      <td>18</td>
    </tr>
    <tr>
      <th>9</th>
      <td>3</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Or as a percent
pd.crosstab(ENIA_1995["REGION"],"percent", normalize="columns")
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
      <th>percent</th>
    </tr>
    <tr>
      <th>REGION</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>0.03</td>
    </tr>
    <tr>
      <th>10</th>
      <td>0.02</td>
    </tr>
    <tr>
      <th>12</th>
      <td>0.01</td>
    </tr>
    <tr>
      <th>13</th>
      <td>0.53</td>
    </tr>
    <tr>
      <th>2</th>
      <td>0.04</td>
    </tr>
    <tr>
      <th>4</th>
      <td>0.07</td>
    </tr>
    <tr>
      <th>5</th>
      <td>0.03</td>
    </tr>
    <tr>
      <th>6</th>
      <td>0.01</td>
    </tr>
    <tr>
      <th>7</th>
      <td>0.05</td>
    </tr>
    <tr>
      <th>8</th>
      <td>0.18</td>
    </tr>
    <tr>
      <th>9</th>
      <td>0.03</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Cumulative sum
pd.crosstab(ENIA_1995["REGION"],"cumulative").cumsum()
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
      <th>cumulative</th>
    </tr>
    <tr>
      <th>REGION</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>3</td>
    </tr>
    <tr>
      <th>10</th>
      <td>5</td>
    </tr>
    <tr>
      <th>12</th>
      <td>6</td>
    </tr>
    <tr>
      <th>13</th>
      <td>59</td>
    </tr>
    <tr>
      <th>2</th>
      <td>63</td>
    </tr>
    <tr>
      <th>4</th>
      <td>70</td>
    </tr>
    <tr>
      <th>5</th>
      <td>73</td>
    </tr>
    <tr>
      <th>6</th>
      <td>74</td>
    </tr>
    <tr>
      <th>7</th>
      <td>79</td>
    </tr>
    <tr>
      <th>8</th>
      <td>97</td>
    </tr>
    <tr>
      <th>9</th>
      <td>100</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Create a new df with all of these
tab = pd.crosstab(ENIA_1995["REGION"],'count')
tab["percent"] = pd.crosstab(ENIA_1995["REGION"],"percent", normalize="columns")
tab["cumulative"] = pd.crosstab(ENIA_1995["REGION"],"cumulative").cumsum()
tab
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
      <th>count</th>
      <th>percent</th>
      <th>cumulative</th>
    </tr>
    <tr>
      <th>REGION</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>3</td>
      <td>0.03</td>
      <td>3</td>
    </tr>
    <tr>
      <th>10</th>
      <td>2</td>
      <td>0.02</td>
      <td>5</td>
    </tr>
    <tr>
      <th>12</th>
      <td>1</td>
      <td>0.01</td>
      <td>6</td>
    </tr>
    <tr>
      <th>13</th>
      <td>53</td>
      <td>0.53</td>
      <td>59</td>
    </tr>
    <tr>
      <th>2</th>
      <td>4</td>
      <td>0.04</td>
      <td>63</td>
    </tr>
    <tr>
      <th>4</th>
      <td>7</td>
      <td>0.07</td>
      <td>70</td>
    </tr>
    <tr>
      <th>5</th>
      <td>3</td>
      <td>0.03</td>
      <td>73</td>
    </tr>
    <tr>
      <th>6</th>
      <td>1</td>
      <td>0.01</td>
      <td>74</td>
    </tr>
    <tr>
      <th>7</th>
      <td>5</td>
      <td>0.05</td>
      <td>79</td>
    </tr>
    <tr>
      <th>8</th>
      <td>18</td>
      <td>0.18</td>
      <td>97</td>
    </tr>
    <tr>
      <th>9</th>
      <td>3</td>
      <td>0.03</td>
      <td>100</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Crosstab multiple variables
pd.crosstab(ENIA_1995["CIIU3"], ENIA_1995["REGION"])
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
      <th>REGION</th>
      <th>1</th>
      <th>10</th>
      <th>12</th>
      <th>13</th>
      <th>2</th>
      <th>4</th>
      <th>5</th>
      <th>6</th>
      <th>7</th>
      <th>8</th>
      <th>9</th>
    </tr>
    <tr>
      <th>CIIU3</th>
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
      <th>1511</th>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
    </tr>
    <tr>
      <th>1512</th>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>3</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>1514</th>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>1531</th>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>1541</th>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>9</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>2</td>
      <td>1</td>
      <td>0</td>
    </tr>
    <tr>
      <th>1552</th>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>1711</th>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>1712</th>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>1721</th>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>1722</th>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>1729</th>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>1810</th>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>5</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>1911</th>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>1920</th>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>3</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>2010</th>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>4</td>
      <td>1</td>
    </tr>
    <tr>
      <th>2021</th>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
    </tr>
    <tr>
      <th>2022</th>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>2101</th>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>2211</th>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>2</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>2219</th>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>2221</th>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
    </tr>
    <tr>
      <th>2424</th>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>2429</th>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>2519</th>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>2520</th>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>6</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>2691</th>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
    </tr>
    <tr>
      <th>2694</th>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>2695</th>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>2</td>
      <td>1</td>
    </tr>
    <tr>
      <th>2710</th>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>2720</th>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
    </tr>
    <tr>
      <th>2811</th>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>2</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
    </tr>
    <tr>
      <th>2899</th>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>4</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>2</td>
      <td>0</td>
    </tr>
    <tr>
      <th>2912</th>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>2</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>2922</th>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
    </tr>
    <tr>
      <th>2924</th>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>3120</th>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>2</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>3312</th>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>3420</th>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>3610</th>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
    </tr>
    <tr>
      <th>3693</th>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
    </tr>
    <tr>
      <th>3699</th>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Normalize by column
pd.crosstab(ENIA_1995["CIIU3"], ENIA_1995["REGION"], normalize="columns")
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
      <th>REGION</th>
      <th>1</th>
      <th>10</th>
      <th>12</th>
      <th>13</th>
      <th>2</th>
      <th>4</th>
      <th>5</th>
      <th>6</th>
      <th>7</th>
      <th>8</th>
      <th>9</th>
    </tr>
    <tr>
      <th>CIIU3</th>
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
      <th>1511</th>
      <td>0.000000</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.000000</td>
      <td>0.00</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.0</td>
      <td>0.2</td>
      <td>0.055556</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>1512</th>
      <td>0.333333</td>
      <td>0.0</td>
      <td>1.0</td>
      <td>0.000000</td>
      <td>0.00</td>
      <td>0.428571</td>
      <td>0.000000</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.000000</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>1514</th>
      <td>0.000000</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.018868</td>
      <td>0.00</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.000000</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>1531</th>
      <td>0.000000</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.000000</td>
      <td>0.25</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.000000</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>1541</th>
      <td>0.000000</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.169811</td>
      <td>0.00</td>
      <td>0.142857</td>
      <td>0.000000</td>
      <td>0.0</td>
      <td>0.4</td>
      <td>0.055556</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>1552</th>
      <td>0.000000</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.018868</td>
      <td>0.00</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.000000</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>1711</th>
      <td>0.000000</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.018868</td>
      <td>0.00</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.000000</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>1712</th>
      <td>0.000000</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.018868</td>
      <td>0.00</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.000000</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>1721</th>
      <td>0.000000</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.018868</td>
      <td>0.00</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.000000</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>1722</th>
      <td>0.000000</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.018868</td>
      <td>0.00</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.000000</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>1729</th>
      <td>0.000000</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.018868</td>
      <td>0.00</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.000000</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>1810</th>
      <td>0.000000</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.094340</td>
      <td>0.00</td>
      <td>0.000000</td>
      <td>0.333333</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.000000</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>1911</th>
      <td>0.000000</td>
      <td>0.5</td>
      <td>0.0</td>
      <td>0.000000</td>
      <td>0.00</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.0</td>
      <td>0.2</td>
      <td>0.000000</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>1920</th>
      <td>0.000000</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.056604</td>
      <td>0.00</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.000000</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>2010</th>
      <td>0.000000</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.000000</td>
      <td>0.00</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.222222</td>
      <td>0.333333</td>
    </tr>
    <tr>
      <th>2021</th>
      <td>0.000000</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.000000</td>
      <td>0.00</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.055556</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>2022</th>
      <td>0.333333</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.018868</td>
      <td>0.00</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.000000</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>2101</th>
      <td>0.000000</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.018868</td>
      <td>0.00</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.000000</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>2211</th>
      <td>0.000000</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.037736</td>
      <td>0.00</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.000000</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>2219</th>
      <td>0.000000</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.018868</td>
      <td>0.00</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.000000</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>2221</th>
      <td>0.000000</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.018868</td>
      <td>0.00</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.055556</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>2424</th>
      <td>0.000000</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.018868</td>
      <td>0.00</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.000000</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>2429</th>
      <td>0.000000</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.018868</td>
      <td>0.00</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.000000</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>2519</th>
      <td>0.000000</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.018868</td>
      <td>0.25</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.000000</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>2520</th>
      <td>0.000000</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.113208</td>
      <td>0.00</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.0</td>
      <td>0.2</td>
      <td>0.000000</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>2691</th>
      <td>0.000000</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.018868</td>
      <td>0.00</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.055556</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>2694</th>
      <td>0.000000</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.000000</td>
      <td>0.00</td>
      <td>0.142857</td>
      <td>0.000000</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.000000</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>2695</th>
      <td>0.000000</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.000000</td>
      <td>0.00</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.111111</td>
      <td>0.333333</td>
    </tr>
    <tr>
      <th>2710</th>
      <td>0.000000</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.018868</td>
      <td>0.00</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.000000</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>2720</th>
      <td>0.000000</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.000000</td>
      <td>0.25</td>
      <td>0.000000</td>
      <td>0.333333</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.055556</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>2811</th>
      <td>0.000000</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.000000</td>
      <td>0.00</td>
      <td>0.285714</td>
      <td>0.000000</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.055556</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>2899</th>
      <td>0.333333</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.075472</td>
      <td>0.00</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.111111</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>2912</th>
      <td>0.000000</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.037736</td>
      <td>0.00</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.000000</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>2922</th>
      <td>0.000000</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.000000</td>
      <td>0.00</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.055556</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>2924</th>
      <td>0.000000</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.018868</td>
      <td>0.00</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>1.0</td>
      <td>0.0</td>
      <td>0.000000</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>3120</th>
      <td>0.000000</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.037736</td>
      <td>0.00</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.000000</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>3312</th>
      <td>0.000000</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.000000</td>
      <td>0.00</td>
      <td>0.000000</td>
      <td>0.333333</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.000000</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>3420</th>
      <td>0.000000</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.018868</td>
      <td>0.00</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.000000</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>3610</th>
      <td>0.000000</td>
      <td>0.5</td>
      <td>0.0</td>
      <td>0.018868</td>
      <td>0.25</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.000000</td>
      <td>0.333333</td>
    </tr>
    <tr>
      <th>3693</th>
      <td>0.000000</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.000000</td>
      <td>0.00</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.055556</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>3699</th>
      <td>0.000000</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.018868</td>
      <td>0.00</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.055556</td>
      <td>0.000000</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Make it percent
round(100*pd.crosstab(ENIA_1995["CIIU3"], ENIA_1995["REGION"], normalize="columns"),2)
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
      <th>REGION</th>
      <th>1</th>
      <th>10</th>
      <th>12</th>
      <th>13</th>
      <th>2</th>
      <th>4</th>
      <th>5</th>
      <th>6</th>
      <th>7</th>
      <th>8</th>
      <th>9</th>
    </tr>
    <tr>
      <th>CIIU3</th>
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
      <th>1511</th>
      <td>0.00</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.00</td>
      <td>0.0</td>
      <td>0.00</td>
      <td>0.00</td>
      <td>0.0</td>
      <td>20.0</td>
      <td>5.56</td>
      <td>0.00</td>
    </tr>
    <tr>
      <th>1512</th>
      <td>33.33</td>
      <td>0.0</td>
      <td>100.0</td>
      <td>0.00</td>
      <td>0.0</td>
      <td>42.86</td>
      <td>0.00</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.00</td>
      <td>0.00</td>
    </tr>
    <tr>
      <th>1514</th>
      <td>0.00</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>1.89</td>
      <td>0.0</td>
      <td>0.00</td>
      <td>0.00</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.00</td>
      <td>0.00</td>
    </tr>
    <tr>
      <th>1531</th>
      <td>0.00</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.00</td>
      <td>25.0</td>
      <td>0.00</td>
      <td>0.00</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.00</td>
      <td>0.00</td>
    </tr>
    <tr>
      <th>1541</th>
      <td>0.00</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>16.98</td>
      <td>0.0</td>
      <td>14.29</td>
      <td>0.00</td>
      <td>0.0</td>
      <td>40.0</td>
      <td>5.56</td>
      <td>0.00</td>
    </tr>
    <tr>
      <th>1552</th>
      <td>0.00</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>1.89</td>
      <td>0.0</td>
      <td>0.00</td>
      <td>0.00</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.00</td>
      <td>0.00</td>
    </tr>
    <tr>
      <th>1711</th>
      <td>0.00</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>1.89</td>
      <td>0.0</td>
      <td>0.00</td>
      <td>0.00</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.00</td>
      <td>0.00</td>
    </tr>
    <tr>
      <th>1712</th>
      <td>0.00</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>1.89</td>
      <td>0.0</td>
      <td>0.00</td>
      <td>0.00</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.00</td>
      <td>0.00</td>
    </tr>
    <tr>
      <th>1721</th>
      <td>0.00</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>1.89</td>
      <td>0.0</td>
      <td>0.00</td>
      <td>0.00</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.00</td>
      <td>0.00</td>
    </tr>
    <tr>
      <th>1722</th>
      <td>0.00</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>1.89</td>
      <td>0.0</td>
      <td>0.00</td>
      <td>0.00</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.00</td>
      <td>0.00</td>
    </tr>
    <tr>
      <th>1729</th>
      <td>0.00</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>1.89</td>
      <td>0.0</td>
      <td>0.00</td>
      <td>0.00</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.00</td>
      <td>0.00</td>
    </tr>
    <tr>
      <th>1810</th>
      <td>0.00</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>9.43</td>
      <td>0.0</td>
      <td>0.00</td>
      <td>33.33</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.00</td>
      <td>0.00</td>
    </tr>
    <tr>
      <th>1911</th>
      <td>0.00</td>
      <td>50.0</td>
      <td>0.0</td>
      <td>0.00</td>
      <td>0.0</td>
      <td>0.00</td>
      <td>0.00</td>
      <td>0.0</td>
      <td>20.0</td>
      <td>0.00</td>
      <td>0.00</td>
    </tr>
    <tr>
      <th>1920</th>
      <td>0.00</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>5.66</td>
      <td>0.0</td>
      <td>0.00</td>
      <td>0.00</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.00</td>
      <td>0.00</td>
    </tr>
    <tr>
      <th>2010</th>
      <td>0.00</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.00</td>
      <td>0.0</td>
      <td>0.00</td>
      <td>0.00</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>22.22</td>
      <td>33.33</td>
    </tr>
    <tr>
      <th>2021</th>
      <td>0.00</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.00</td>
      <td>0.0</td>
      <td>0.00</td>
      <td>0.00</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>5.56</td>
      <td>0.00</td>
    </tr>
    <tr>
      <th>2022</th>
      <td>33.33</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>1.89</td>
      <td>0.0</td>
      <td>0.00</td>
      <td>0.00</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.00</td>
      <td>0.00</td>
    </tr>
    <tr>
      <th>2101</th>
      <td>0.00</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>1.89</td>
      <td>0.0</td>
      <td>0.00</td>
      <td>0.00</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.00</td>
      <td>0.00</td>
    </tr>
    <tr>
      <th>2211</th>
      <td>0.00</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>3.77</td>
      <td>0.0</td>
      <td>0.00</td>
      <td>0.00</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.00</td>
      <td>0.00</td>
    </tr>
    <tr>
      <th>2219</th>
      <td>0.00</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>1.89</td>
      <td>0.0</td>
      <td>0.00</td>
      <td>0.00</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.00</td>
      <td>0.00</td>
    </tr>
    <tr>
      <th>2221</th>
      <td>0.00</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>1.89</td>
      <td>0.0</td>
      <td>0.00</td>
      <td>0.00</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>5.56</td>
      <td>0.00</td>
    </tr>
    <tr>
      <th>2424</th>
      <td>0.00</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>1.89</td>
      <td>0.0</td>
      <td>0.00</td>
      <td>0.00</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.00</td>
      <td>0.00</td>
    </tr>
    <tr>
      <th>2429</th>
      <td>0.00</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>1.89</td>
      <td>0.0</td>
      <td>0.00</td>
      <td>0.00</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.00</td>
      <td>0.00</td>
    </tr>
    <tr>
      <th>2519</th>
      <td>0.00</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>1.89</td>
      <td>25.0</td>
      <td>0.00</td>
      <td>0.00</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.00</td>
      <td>0.00</td>
    </tr>
    <tr>
      <th>2520</th>
      <td>0.00</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>11.32</td>
      <td>0.0</td>
      <td>0.00</td>
      <td>0.00</td>
      <td>0.0</td>
      <td>20.0</td>
      <td>0.00</td>
      <td>0.00</td>
    </tr>
    <tr>
      <th>2691</th>
      <td>0.00</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>1.89</td>
      <td>0.0</td>
      <td>0.00</td>
      <td>0.00</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>5.56</td>
      <td>0.00</td>
    </tr>
    <tr>
      <th>2694</th>
      <td>0.00</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.00</td>
      <td>0.0</td>
      <td>14.29</td>
      <td>0.00</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.00</td>
      <td>0.00</td>
    </tr>
    <tr>
      <th>2695</th>
      <td>0.00</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.00</td>
      <td>0.0</td>
      <td>0.00</td>
      <td>0.00</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>11.11</td>
      <td>33.33</td>
    </tr>
    <tr>
      <th>2710</th>
      <td>0.00</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>1.89</td>
      <td>0.0</td>
      <td>0.00</td>
      <td>0.00</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.00</td>
      <td>0.00</td>
    </tr>
    <tr>
      <th>2720</th>
      <td>0.00</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.00</td>
      <td>25.0</td>
      <td>0.00</td>
      <td>33.33</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>5.56</td>
      <td>0.00</td>
    </tr>
    <tr>
      <th>2811</th>
      <td>0.00</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.00</td>
      <td>0.0</td>
      <td>28.57</td>
      <td>0.00</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>5.56</td>
      <td>0.00</td>
    </tr>
    <tr>
      <th>2899</th>
      <td>33.33</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>7.55</td>
      <td>0.0</td>
      <td>0.00</td>
      <td>0.00</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>11.11</td>
      <td>0.00</td>
    </tr>
    <tr>
      <th>2912</th>
      <td>0.00</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>3.77</td>
      <td>0.0</td>
      <td>0.00</td>
      <td>0.00</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.00</td>
      <td>0.00</td>
    </tr>
    <tr>
      <th>2922</th>
      <td>0.00</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.00</td>
      <td>0.0</td>
      <td>0.00</td>
      <td>0.00</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>5.56</td>
      <td>0.00</td>
    </tr>
    <tr>
      <th>2924</th>
      <td>0.00</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>1.89</td>
      <td>0.0</td>
      <td>0.00</td>
      <td>0.00</td>
      <td>100.0</td>
      <td>0.0</td>
      <td>0.00</td>
      <td>0.00</td>
    </tr>
    <tr>
      <th>3120</th>
      <td>0.00</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>3.77</td>
      <td>0.0</td>
      <td>0.00</td>
      <td>0.00</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.00</td>
      <td>0.00</td>
    </tr>
    <tr>
      <th>3312</th>
      <td>0.00</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.00</td>
      <td>0.0</td>
      <td>0.00</td>
      <td>33.33</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.00</td>
      <td>0.00</td>
    </tr>
    <tr>
      <th>3420</th>
      <td>0.00</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>1.89</td>
      <td>0.0</td>
      <td>0.00</td>
      <td>0.00</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.00</td>
      <td>0.00</td>
    </tr>
    <tr>
      <th>3610</th>
      <td>0.00</td>
      <td>50.0</td>
      <td>0.0</td>
      <td>1.89</td>
      <td>25.0</td>
      <td>0.00</td>
      <td>0.00</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.00</td>
      <td>33.33</td>
    </tr>
    <tr>
      <th>3693</th>
      <td>0.00</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.00</td>
      <td>0.0</td>
      <td>0.00</td>
      <td>0.00</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>5.56</td>
      <td>0.00</td>
    </tr>
    <tr>
      <th>3699</th>
      <td>0.00</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>1.89</td>
      <td>0.0</td>
      <td>0.00</td>
      <td>0.00</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>5.56</td>
      <td>0.00</td>
    </tr>
  </tbody>
</table>
</div>



## Practice - Additional Calculations on DFs
1. What happens if you describe the entire dataframe?
    - What's the maximum contracted men? The maximum total wages?
2. There’s a few more variables that you could be interested in.
    - Make a tabulation looking at `EXPORTADOS` to see how many firms export.
    - Create a variable called `emp_type` that separates firms by < 25 employees, 25-100 employees, 101-499 employees, and 500+ employees. Hint: Check out the function `cut`.
    - Try making your own cross tab of `EXPORTADOS` and `emp_type`.
    - Which one do you want in the columns and which one do you want in the rows?
3. How do you control this with the crosstab method?
    - Do you want counts, percentages that add to one over the entire table, over the row, or over the column — discuss syntax of each.


```python
# Results:
# 1.
#print(ENIA_1995.describe())
#print(ENIA_1995.describe().loc["max","TOTHOM"])
print(ENIA_1995.describe().loc["max","total_wages"])
# 2. 
print(pd.crosstab(ENIA_1995["EXPORTADOS"], "count"))
ENIA_1995["emp_type"] = pd.cut(ENIA_1995["total_emps"],bins = [1,25,100,500,1000])
print(pd.crosstab(ENIA_1995["emp_type"], ENIA_1995["EXPORTADOS"]))
# 3.
print(pd.crosstab(ENIA_1995["emp_type"], ENIA_1995["EXPORTADOS"], normalize="columns"))

```

    3822586.0
    col_0       count
    EXPORTADOS       
    0.0            77
    1.0            23
    EXPORTADOS   0.0  1.0
    emp_type             
    (1, 25]       39    1
    (25, 100]     30    7
    (100, 500]     7   13
    (500, 1000]    1    2
    EXPORTADOS        0.0       1.0
    emp_type                       
    (1, 25]      0.506494  0.043478
    (25, 100]    0.389610  0.304348
    (100, 500]   0.090909  0.565217
    (500, 1000]  0.012987  0.086957
    
