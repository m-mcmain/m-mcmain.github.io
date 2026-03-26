---
layout: single
sitemap: false
permalink: /pages/Econ_390_SP26_L18/
title: Econ 390 Lecture 18
---

[Download Jupyter Notebook Empty](https://m-mcmain.github.io/files/Econ390SP26/Lectures/Lecture18_Aggregation_empty.ipynb)

[Download Jupyter Notebook Completed](https://m-mcmain.github.io/files/Econ390SP26/Lectures/Lecture18_Aggregation_full.ipynb)

# Econ 390 - Lecture 18: Groupby and Aggregation
Today we will be going over how to aggregate data and apply the Split-Apply-Combine method using Python. All of [Chapter 10 of McKinney](wesmckinney.com/book/data-aggregation) and much of [Data Transformation of Turrell](https://aeturrell.github.io/coding-for-economists/data-transformation.html) are applicable here, though we will not be going over all of what they cover.


```python
import pandas as pd

url = "https://m-mcmain.github.io/files/Econ390SP26/"
```

## Split-Apply-Combine
The Split-Apply-Combine method is so common there are different images describing how to use it in both of the textbooks:

![McKinney SAC](https://wesmckinney.com/book/images/pda3_1001.png)
![Turrell SAC](https://jakevdp.github.io/PythonDataScienceHandbook/figures/03.08-split-apply-combine.png)


```python
# NLSY variables
variables = {"R0000100":"ID", "R0536300":"Sex", "U4950200":"Education", 
             "U5753500":"Income", "Z9061912":"Weeks Worked"}
# "R0536401":"Birth Month", "R0536402":"Birth Year", "R1482600":"Race", "U4943000":"Age"
```


```python
# Read in data
nlsy = pd.read_csv(url + "nlsy_wage_educSex.csv", na_values=-5, usecols=variables.keys()).rename(columns=variables)
nlsy
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
      <th>ID</th>
      <th>Sex</th>
      <th>Education</th>
      <th>Income</th>
      <th>Weeks Worked</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>2</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>-4</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>1</td>
      <td>2.0</td>
      <td>115000.0</td>
      <td>46</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>2</td>
      <td>4.0</td>
      <td>-4.0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>2</td>
      <td>2.0</td>
      <td>45000.0</td>
      <td>51</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5</td>
      <td>1</td>
      <td>2.0</td>
      <td>150000.0</td>
      <td>43</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>8979</th>
      <td>9018</td>
      <td>2</td>
      <td>1.0</td>
      <td>90000.0</td>
      <td>52</td>
    </tr>
    <tr>
      <th>8980</th>
      <td>9019</td>
      <td>1</td>
      <td>3.0</td>
      <td>43000.0</td>
      <td>43</td>
    </tr>
    <tr>
      <th>8981</th>
      <td>9020</td>
      <td>1</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>-4</td>
    </tr>
    <tr>
      <th>8982</th>
      <td>9021</td>
      <td>1</td>
      <td>4.0</td>
      <td>47000.0</td>
      <td>52</td>
    </tr>
    <tr>
      <th>8983</th>
      <td>9022</td>
      <td>2</td>
      <td>5.0</td>
      <td>60000.0</td>
      <td>46</td>
    </tr>
  </tbody>
</table>
<p>8984 rows × 5 columns</p>
</div>




```python
# Info
nlsy.info()
```

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 8984 entries, 0 to 8983
    Data columns (total 5 columns):
     #   Column        Non-Null Count  Dtype  
    ---  ------        --------------  -----  
     0   ID            8984 non-null   int64  
     1   Sex           8984 non-null   int64  
     2   Education     6713 non-null   float64
     3   Income        6713 non-null   float64
     4   Weeks Worked  8984 non-null   int64  
    dtypes: float64(2), int64(3)
    memory usage: 351.1 KB
    


```python
# Counts of different groups
print(nlsy["Sex"].value_counts())
print(nlsy["Education"].value_counts())
```

    Sex
    1    4599
    2    4385
    Name: count, dtype: int64
    Education
     2.0    2563
     4.0    1351
     1.0     871
     3.0     621
     5.0     614
     0.0     502
     7.0     106
     6.0      59
    -3.0      26
    Name: count, dtype: int64
    


```python
# Translating codes to what they mean
educ_codes = {0:"None", 1:"GED", 2:"High School", 3:"Associate's", 4:"Bachelor's", 5:"Master's",
              6:"PhD", 7:"Professional"}
sex_codes = {1:"Male", 2:"Female", 0:"No Information"}

nlsy["Education"] = nlsy["Education"].replace(educ_codes)
nlsy["Sex"] = nlsy["Sex"].replace(sex_codes)

nlsy
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
      <th>ID</th>
      <th>Sex</th>
      <th>Education</th>
      <th>Income</th>
      <th>Weeks Worked</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>Female</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>-4</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>Male</td>
      <td>High School</td>
      <td>115000.0</td>
      <td>46</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>Female</td>
      <td>Bachelor's</td>
      <td>-4.0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>Female</td>
      <td>High School</td>
      <td>45000.0</td>
      <td>51</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5</td>
      <td>Male</td>
      <td>High School</td>
      <td>150000.0</td>
      <td>43</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>8979</th>
      <td>9018</td>
      <td>Female</td>
      <td>GED</td>
      <td>90000.0</td>
      <td>52</td>
    </tr>
    <tr>
      <th>8980</th>
      <td>9019</td>
      <td>Male</td>
      <td>Associate's</td>
      <td>43000.0</td>
      <td>43</td>
    </tr>
    <tr>
      <th>8981</th>
      <td>9020</td>
      <td>Male</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>-4</td>
    </tr>
    <tr>
      <th>8982</th>
      <td>9021</td>
      <td>Male</td>
      <td>Bachelor's</td>
      <td>47000.0</td>
      <td>52</td>
    </tr>
    <tr>
      <th>8983</th>
      <td>9022</td>
      <td>Female</td>
      <td>Master's</td>
      <td>60000.0</td>
      <td>46</td>
    </tr>
  </tbody>
</table>
<p>8984 rows × 5 columns</p>
</div>




```python
# Set the index and groupby
nlsy.set_index("ID", inplace=True)
nlsy_grouped = nlsy.groupby("Sex")
```




    <pandas.core.groupby.generic.DataFrameGroupBy object at 0x00000238AFC12660>




```python
# Get Group method
nlsy_grouped.get_group("Female")
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
      <th>Sex</th>
      <th>Education</th>
      <th>Income</th>
      <th>Weeks Worked</th>
    </tr>
    <tr>
      <th>ID</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>Female</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>-4</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Female</td>
      <td>Bachelor's</td>
      <td>-4.0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Female</td>
      <td>High School</td>
      <td>45000.0</td>
      <td>51</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Female</td>
      <td>High School</td>
      <td>25000.0</td>
      <td>40</td>
    </tr>
    <tr>
      <th>8</th>
      <td>Female</td>
      <td>Master's</td>
      <td>70000.0</td>
      <td>52</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>9014</th>
      <td>Female</td>
      <td>None</td>
      <td>-4.0</td>
      <td>22</td>
    </tr>
    <tr>
      <th>9015</th>
      <td>Female</td>
      <td>Master's</td>
      <td>96000.0</td>
      <td>34</td>
    </tr>
    <tr>
      <th>9016</th>
      <td>Female</td>
      <td>Bachelor's</td>
      <td>60000.0</td>
      <td>48</td>
    </tr>
    <tr>
      <th>9018</th>
      <td>Female</td>
      <td>GED</td>
      <td>90000.0</td>
      <td>52</td>
    </tr>
    <tr>
      <th>9022</th>
      <td>Female</td>
      <td>Master's</td>
      <td>60000.0</td>
      <td>46</td>
    </tr>
  </tbody>
</table>
<p>4385 rows × 4 columns</p>
</div>




```python
# Mean
nlsy.mean(numeric_only=True)
```




    Income          48722.649784
    Weeks Worked       25.640583
    dtype: float64




```python
# Mean of grouped
nlsy_grouped.mean(numeric_only=True)
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
      <th>Income</th>
      <th>Weeks Worked</th>
    </tr>
    <tr>
      <th>Sex</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Female</th>
      <td>39800.302482</td>
      <td>25.797719</td>
    </tr>
    <tr>
      <th>Male</th>
      <td>58016.761557</td>
      <td>25.490759</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Limit to just people working
nlsy_working = nlsy.loc[nlsy["Weeks Worked"] > 0]
nlsy_working
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
      <th>Sex</th>
      <th>Education</th>
      <th>Income</th>
      <th>Weeks Worked</th>
    </tr>
    <tr>
      <th>ID</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2</th>
      <td>Male</td>
      <td>High School</td>
      <td>115000.0</td>
      <td>46</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Female</td>
      <td>High School</td>
      <td>45000.0</td>
      <td>51</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Male</td>
      <td>High School</td>
      <td>150000.0</td>
      <td>43</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Female</td>
      <td>High School</td>
      <td>25000.0</td>
      <td>40</td>
    </tr>
    <tr>
      <th>8</th>
      <td>Female</td>
      <td>Master's</td>
      <td>70000.0</td>
      <td>52</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>9016</th>
      <td>Female</td>
      <td>Bachelor's</td>
      <td>60000.0</td>
      <td>48</td>
    </tr>
    <tr>
      <th>9018</th>
      <td>Female</td>
      <td>GED</td>
      <td>90000.0</td>
      <td>52</td>
    </tr>
    <tr>
      <th>9019</th>
      <td>Male</td>
      <td>Associate's</td>
      <td>43000.0</td>
      <td>43</td>
    </tr>
    <tr>
      <th>9021</th>
      <td>Male</td>
      <td>Bachelor's</td>
      <td>47000.0</td>
      <td>52</td>
    </tr>
    <tr>
      <th>9022</th>
      <td>Female</td>
      <td>Master's</td>
      <td>60000.0</td>
      <td>46</td>
    </tr>
  </tbody>
</table>
<p>5542 rows × 4 columns</p>
</div>




```python
# Let's make it grouped!
nlsy_meanSex_grouped = nlsy.loc[nlsy["Weeks Worked"] > 0].groupby("Sex").mean(numeric_only = True)
nlsy_meanSex_grouped
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
      <th>Income</th>
      <th>Weeks Worked</th>
    </tr>
    <tr>
      <th>Sex</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Female</th>
      <td>48450.467860</td>
      <td>42.751278</td>
    </tr>
    <tr>
      <th>Male</th>
      <td>65821.912625</td>
      <td>43.738944</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Cleaning and new Value
nlsy_working = nlsy_working.loc[nlsy_working["Education"] != -3.0]
nlsy_working.loc[(nlsy_working["Education"] == "High School") | (nlsy_working["Education"] == "None") | (nlsy_working["Education"] == "GED"),"Education"] = "High School and Below"
nlsy_working.loc[(nlsy_working["Education"] == "Bachelor's") | (nlsy_working["Education"] == "Associate's"), "Education"] = "Bachelor's and Associate's"
nlsy_working.loc[(nlsy_working["Education"] != "High School and Below") & (nlsy_working["Education"] != "Bachelor's and Associate's"),"Education"] = "Master's and Up"
nlsy_working
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
      <th>Sex</th>
      <th>Education</th>
      <th>Income</th>
      <th>Weeks Worked</th>
    </tr>
    <tr>
      <th>ID</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2</th>
      <td>Male</td>
      <td>High School and Below</td>
      <td>115000.0</td>
      <td>46</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Female</td>
      <td>High School and Below</td>
      <td>45000.0</td>
      <td>51</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Male</td>
      <td>High School and Below</td>
      <td>150000.0</td>
      <td>43</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Female</td>
      <td>High School and Below</td>
      <td>25000.0</td>
      <td>40</td>
    </tr>
    <tr>
      <th>8</th>
      <td>Female</td>
      <td>Master's and Up</td>
      <td>70000.0</td>
      <td>52</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>9016</th>
      <td>Female</td>
      <td>Bachelor's and Associate's</td>
      <td>60000.0</td>
      <td>48</td>
    </tr>
    <tr>
      <th>9018</th>
      <td>Female</td>
      <td>High School and Below</td>
      <td>90000.0</td>
      <td>52</td>
    </tr>
    <tr>
      <th>9019</th>
      <td>Male</td>
      <td>Bachelor's and Associate's</td>
      <td>43000.0</td>
      <td>43</td>
    </tr>
    <tr>
      <th>9021</th>
      <td>Male</td>
      <td>Bachelor's and Associate's</td>
      <td>47000.0</td>
      <td>52</td>
    </tr>
    <tr>
      <th>9022</th>
      <td>Female</td>
      <td>Master's and Up</td>
      <td>60000.0</td>
      <td>46</td>
    </tr>
  </tbody>
</table>
<p>5526 rows × 4 columns</p>
</div>




```python
print(nlsy_working["Education"].value_counts())
```

    Education
    High School and Below         3047
    Bachelor's and Associate's    1744
    Master's and Up                735
    Name: count, dtype: int64
    


```python
# Medians
nlsy_working.groupby("Education").median(numeric_only=True)
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
      <th>Income</th>
      <th>Weeks Worked</th>
    </tr>
    <tr>
      <th>Education</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Bachelor's and Associate's</th>
      <td>55000.0</td>
      <td>44.0</td>
    </tr>
    <tr>
      <th>High School and Below</th>
      <td>35000.0</td>
      <td>44.0</td>
    </tr>
    <tr>
      <th>Master's and Up</th>
      <td>78000.0</td>
      <td>45.0</td>
    </tr>
  </tbody>
</table>
</div>



Common aggregation methods are:
- `.mean()`
- `.sum()`
- `.std()`
- `.describe()`
- `.min()`
- `.max()`

## Practice: Split-Apply-Combine
Let's figure out how to get some measure of how variable annual income of workers are by education attainment.
1. Calculate the 75th percentile of Income for each new education type, storing the result in a DataFrame called q75 (So we split on what? And then apply what method?) *Hint: The .quantile() method computes percentiles.*
3. Calculate the 25th percentile for each type and store it in q25
4. Take the difference between these q75 and q25
5. Based on the IQR, which education type has the least amount of variation?


```python
# Results:
nlsy_working_grouped = nlsy_working.groupby("Education")
q75 = nlsy_working_grouped["Income"].quantile(0.75)
q25 = nlsy_working_grouped["Income"].quantile(0.25)
q75 - q25
```




    Education
    Bachelor's and Associate's    54000.0
    High School and Below         44000.0
    Master's and Up               62000.0
    Name: Income, dtype: float64




```python
nlsy_working_grouped.describe()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead tr th {
        text-align: left;
    }

    .dataframe thead tr:last-of-type th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr>
      <th></th>
      <th colspan="8" halign="left">Income</th>
      <th colspan="8" halign="left">Weeks Worked</th>
    </tr>
    <tr>
      <th></th>
      <th>count</th>
      <th>mean</th>
      <th>std</th>
      <th>min</th>
      <th>25%</th>
      <th>50%</th>
      <th>75%</th>
      <th>max</th>
      <th>count</th>
      <th>mean</th>
      <th>std</th>
      <th>min</th>
      <th>25%</th>
      <th>50%</th>
      <th>75%</th>
      <th>max</th>
    </tr>
    <tr>
      <th>Education</th>
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
      <th>Bachelor's and Associate's</th>
      <td>1744.0</td>
      <td>68138.235092</td>
      <td>64234.270551</td>
      <td>-4.0</td>
      <td>32000.0</td>
      <td>55000.0</td>
      <td>86000.0</td>
      <td>380288.0</td>
      <td>1744.0</td>
      <td>43.588876</td>
      <td>8.528788</td>
      <td>1.0</td>
      <td>41.0</td>
      <td>44.0</td>
      <td>51.0</td>
      <td>52.0</td>
    </tr>
    <tr>
      <th>High School and Below</th>
      <td>3047.0</td>
      <td>41395.575320</td>
      <td>42969.892392</td>
      <td>-4.0</td>
      <td>13000.0</td>
      <td>35000.0</td>
      <td>57000.0</td>
      <td>380288.0</td>
      <td>3047.0</td>
      <td>42.623564</td>
      <td>11.068005</td>
      <td>1.0</td>
      <td>40.0</td>
      <td>44.0</td>
      <td>52.0</td>
      <td>52.0</td>
    </tr>
    <tr>
      <th>Master's and Up</th>
      <td>735.0</td>
      <td>97691.197279</td>
      <td>83286.984185</td>
      <td>-4.0</td>
      <td>53000.0</td>
      <td>78000.0</td>
      <td>115000.0</td>
      <td>380288.0</td>
      <td>735.0</td>
      <td>45.062585</td>
      <td>6.936764</td>
      <td>4.0</td>
      <td>41.0</td>
      <td>45.0</td>
      <td>52.0</td>
      <td>52.0</td>
    </tr>
  </tbody>
</table>
</div>



## Multiple Groups


```python
# List in groupby
nlsy_median_educSex = nlsy_working.groupby(["Education", "Sex"]).median()
nlsy_median_educSex
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
      <th></th>
      <th>Income</th>
      <th>Weeks Worked</th>
    </tr>
    <tr>
      <th>Education</th>
      <th>Sex</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th rowspan="2" valign="top">Bachelor's and Associate's</th>
      <th>Female</th>
      <td>47592.0</td>
      <td>44.0</td>
    </tr>
    <tr>
      <th>Male</th>
      <td>70000.0</td>
      <td>44.0</td>
    </tr>
    <tr>
      <th rowspan="2" valign="top">High School and Below</th>
      <th>Female</th>
      <td>28000.0</td>
      <td>43.0</td>
    </tr>
    <tr>
      <th>Male</th>
      <td>42500.0</td>
      <td>45.0</td>
    </tr>
    <tr>
      <th rowspan="2" valign="top">Master's and Up</th>
      <th>Female</th>
      <td>69000.0</td>
      <td>45.0</td>
    </tr>
    <tr>
      <th>Male</th>
      <td>99000.0</td>
      <td>45.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
# xs method
nlsy_median_educSex.xs("Female", level="Sex")
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
      <th>Income</th>
      <th>Weeks Worked</th>
    </tr>
    <tr>
      <th>Education</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Bachelor's and Associate's</th>
      <td>47592.0</td>
      <td>44.0</td>
    </tr>
    <tr>
      <th>High School and Below</th>
      <td>28000.0</td>
      <td>43.0</td>
    </tr>
    <tr>
      <th>Master's and Up</th>
      <td>69000.0</td>
      <td>45.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Count
nlsy_working[["Income","Sex"]].groupby("Sex").count()
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
      <th>Income</th>
    </tr>
    <tr>
      <th>Sex</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Female</th>
      <td>2729</td>
    </tr>
    <tr>
      <th>Male</th>
      <td>2797</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Agg
nlsy_working[["Income","Sex"]].groupby("Sex").agg("count")
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
      <th>Income</th>
    </tr>
    <tr>
      <th>Sex</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Female</th>
      <td>2729</td>
    </tr>
    <tr>
      <th>Male</th>
      <td>2797</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Multiple agg
nlsy_working[["Income","Sex"]].groupby("Sex").agg(["count", "mean", "median"])
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead tr th {
        text-align: left;
    }

    .dataframe thead tr:last-of-type th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr>
      <th></th>
      <th colspan="3" halign="left">Income</th>
    </tr>
    <tr>
      <th></th>
      <th>count</th>
      <th>mean</th>
      <th>median</th>
    </tr>
    <tr>
      <th>Sex</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Female</th>
      <td>2729</td>
      <td>48550.306706</td>
      <td>40000.0</td>
    </tr>
    <tr>
      <th>Male</th>
      <td>2797</td>
      <td>65882.961387</td>
      <td>53000.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Multiple variables
nlsy_working[["Income", "Weeks Worked", "Sex"]].groupby("Sex").agg(["count", "mean", "median"]).loc[:,("Weeks Worked", "mean")]
```




    Sex
    Female    42.765848
    Male      43.727565
    Name: (Weeks Worked, mean), dtype: float64


