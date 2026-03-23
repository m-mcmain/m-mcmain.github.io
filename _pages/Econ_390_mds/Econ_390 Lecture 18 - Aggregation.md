---
layout: single
sitemap: false
permalink: /pages/Econ_390_SP26_L18_teaching/
title: Econ 390 Lecture 18
---

[Download Jupyter Notebook Empty](https://m-mcmain.github.io/files/Econ390SP26/Lectures/Lecture18_Aggregation_empty.ipynb)

Download Jupyter Notebook Completed

# Econ 390 - Lecture 18: Groupby and Aggregation
Today we will be going over how to aggregate data and apply the Split-Apply-Combine method using Python. All of [Chapter 10 of McKinney](https://wesmckinney.com/book/data-aggregation) and much of [Data Transformation of Turrell](https://aeturrell.github.io/coding-for-economists/data-transformation.html) are applicable here, though we will not be going over all of what they cover.


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
variables = {"R0000100":"ID", "R0536300":"Sex", 
             "U4950200":"Educational Attainment", "U5753500":"Income", "Z9061912":"Weeks Worked"}
# "R0536402":"Birth Year", "U4943000":"Age", "R0536401":"Birth Month", "R1482600":"Race", "R1235800":"Sample Type",
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
      <th>Educational Attainment</th>
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
     #   Column                  Non-Null Count  Dtype  
    ---  ------                  --------------  -----  
     0   ID                      8984 non-null   int64  
     1   Sex                     8984 non-null   int64  
     2   Educational Attainment  6713 non-null   float64
     3   Income                  6713 non-null   float64
     4   Weeks Worked            8984 non-null   int64  
    dtypes: float64(2), int64(3)
    memory usage: 351.1 KB
    


```python
# Counts of different groups
print(nlsy["Sex"].value_counts())
print(nlsy["Educational Attainment"].value_counts())
```

    Sex
    1    4599
    2    4385
    Name: count, dtype: int64
    Educational Attainment
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
educ_codes = {0:"None", 1:"GED", 2:"High School", 3:"Associate's", 4:"Bachelor's", 5:"Master's", 6:"PhD", 7:"Professional"}
nlsy["Educational Attainment"] = nlsy["Educational Attainment"].replace(educ_codes)

sex_codes = {1:"Male", 2:"Female", 0:"No Info"}
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
      <th>Educational Attainment</th>
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
      <th>Educational Attainment</th>
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
nlsy_meanSex = nlsy_grouped.mean(numeric_only=True)
nlsy_meanSex
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
nlsy_meanSex_working = nlsy.loc[nlsy["Weeks Worked"] > 0].groupby("Sex").mean(numeric_only=True)
nlsy_meanSex_working
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
# Not grouped
nlsy_working = nlsy.loc[nlsy["Weeks Worked"] > 0]
```


```python
# Cleaning and new Value
nlsy_working.loc[(nlsy_working["Educational Attainment"] == "High School") | (nlsy_working["Educational Attainment"] == "GED") | 
                 (nlsy_working["Educational Attainment"] == "None") | (nlsy_working["Educational Attainment"] == "Associate's"), 
                 "Educational Attainment"] = "Associate's or Below"
nlsy_working.loc[(nlsy_working["Educational Attainment"] == "Master's") | (nlsy_working["Educational Attainment"] == "PhD") |
                 (nlsy_working["Educational Attainment"] == "Professional"), "Educational Attainment"] = "Master's or More"
nlsy_working = nlsy_working.loc[nlsy_working["Educational Attainment"] != -3.0]
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
      <th>Educational Attainment</th>
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
      <td>Associate's or Below</td>
      <td>115000.0</td>
      <td>46</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Female</td>
      <td>Associate's or Below</td>
      <td>45000.0</td>
      <td>51</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Male</td>
      <td>Associate's or Below</td>
      <td>150000.0</td>
      <td>43</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Female</td>
      <td>Associate's or Below</td>
      <td>25000.0</td>
      <td>40</td>
    </tr>
    <tr>
      <th>8</th>
      <td>Female</td>
      <td>Master's or More</td>
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
      <td>Associate's or Below</td>
      <td>90000.0</td>
      <td>52</td>
    </tr>
    <tr>
      <th>9019</th>
      <td>Male</td>
      <td>Associate's or Below</td>
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
      <td>Master's or More</td>
      <td>60000.0</td>
      <td>46</td>
    </tr>
  </tbody>
</table>
<p>5526 rows × 4 columns</p>
</div>




```python
# Medians
nlsy_EducMedian_working = nlsy_working.groupby("Educational Attainment").median(numeric_only = True)
nlsy_EducMedian_working
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
      <th>Educational Attainment</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Associate's or Below</th>
      <td>36000.0</td>
      <td>44.0</td>
    </tr>
    <tr>
      <th>Bachelor's</th>
      <td>60000.0</td>
      <td>44.0</td>
    </tr>
    <tr>
      <th>Master's or More</th>
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
nlsy_working_educ = nlsy_working.groupby("Educational Attainment")
q75 = nlsy_working_educ["Income"].quantile(0.75)
q25 = nlsy_working_educ["Income"].quantile(0.25)
print(q75 - q25)
# Associate's or Below has the least amount of variation!
```

    Educational Attainment
    Associate's or Below    45000.0
    Bachelor's              56847.0
    Master's or More        62000.0
    Name: Income, dtype: float64
    


```python
# Alternatively:
nlsy_working_educ["Income"].describe()
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
      <th>Educational Attainment</th>
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
      <th>Associate's or Below</th>
      <td>3583.0</td>
      <td>42892.265420</td>
      <td>44196.696126</td>
      <td>-4.0</td>
      <td>15000.0</td>
      <td>36000.0</td>
      <td>60000.0</td>
      <td>380288.0</td>
    </tr>
    <tr>
      <th>Bachelor's</th>
      <td>1208.0</td>
      <td>75564.911424</td>
      <td>68404.744365</td>
      <td>-4.0</td>
      <td>38153.0</td>
      <td>60000.0</td>
      <td>95000.0</td>
      <td>380288.0</td>
    </tr>
    <tr>
      <th>Master's or More</th>
      <td>735.0</td>
      <td>97691.197279</td>
      <td>83286.984185</td>
      <td>-4.0</td>
      <td>53000.0</td>
      <td>78000.0</td>
      <td>115000.0</td>
      <td>380288.0</td>
    </tr>
  </tbody>
</table>
</div>



## Multiple Groups


```python
# List in groupby
income_medians_educ_sex = nlsy_working.groupby(["Educational Attainment", "Sex"]).median(numeric_only=True)
income_medians_educ_sex
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
      <th>Educational Attainment</th>
      <th>Sex</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th rowspan="2" valign="top">Associate's or Below</th>
      <th>Female</th>
      <td>30000.0</td>
      <td>43.0</td>
    </tr>
    <tr>
      <th>Male</th>
      <td>45000.0</td>
      <td>45.0</td>
    </tr>
    <tr>
      <th rowspan="2" valign="top">Bachelor's</th>
      <th>Female</th>
      <td>54000.0</td>
      <td>44.0</td>
    </tr>
    <tr>
      <th>Male</th>
      <td>75500.0</td>
      <td>44.0</td>
    </tr>
    <tr>
      <th rowspan="2" valign="top">Master's or More</th>
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
income_medians_educ_sex.xs("Female", level="Sex")
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
      <th>Educational Attainment</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Associate's or Below</th>
      <td>30000.0</td>
      <td>43.0</td>
    </tr>
    <tr>
      <th>Bachelor's</th>
      <td>54000.0</td>
      <td>44.0</td>
    </tr>
    <tr>
      <th>Master's or More</th>
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
nlsy_working[["Income", "Sex"]].groupby("Sex").agg(["count", "mean", "median"])
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
nlsy_working[["Income", "Weeks Worked","Sex"]].groupby("Sex").agg(["count", "mean", "median"])
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
      <th colspan="3" halign="left">Weeks Worked</th>
    </tr>
    <tr>
      <th></th>
      <th>count</th>
      <th>mean</th>
      <th>median</th>
      <th>count</th>
      <th>mean</th>
      <th>median</th>
    </tr>
    <tr>
      <th>Sex</th>
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
      <th>Female</th>
      <td>2729</td>
      <td>48550.306706</td>
      <td>40000.0</td>
      <td>2729</td>
      <td>42.765848</td>
      <td>44.0</td>
    </tr>
    <tr>
      <th>Male</th>
      <td>2797</td>
      <td>65882.961387</td>
      <td>53000.0</td>
      <td>2797</td>
      <td>43.727565</td>
      <td>45.0</td>
    </tr>
  </tbody>
</table>
</div>


