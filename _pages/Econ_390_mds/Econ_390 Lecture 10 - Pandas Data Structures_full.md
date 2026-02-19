---
layout: single
sitemap: false
permalink: /pages/Econ_390_SP26_L10/
---

[Download Jupyter Notebook Empty](https://m-mcmain.github.io/files/Econ390SP26/Lectures/Lecture10_PandasDataStructures_empty.ipynb)

[Download Jupyter Notebook Completed](https://m-mcmain.github.io/files/Econ390SP26/Lectures/Lecture10_PandasDataStructures_full.ipynb)

# Econ 390 - Lecture 10: Pandas Series and Data Frames

Today we will be going over the incredibly popular package Pandas and how to utilize the data structures that they bring to Python. You can find good chapters in both [McKinney](https://wesmckinney.com/book/pandas-basics#pandas_construction) and [Turrell](https://aeturrell.github.io/coding-for-economists/data-intro.html#working-with-data) dedicated to this.

## Series


```python
# First you always need to import Pandas
import pandas as pd
```


```python
# Creating a series
wisc_cfb_wins = pd.Series([4, 5, 7, 7, 9, 4])
wisc_cfb_wins
```




    0    4
    1    5
    2    7
    3    7
    4    9
    5    4
    dtype: int64




```python
# What does it look like?
print(list(wisc_cfb_wins))
print(wisc_cfb_wins.to_dict())
print(wisc_cfb_wins.index)
```

    [4, 5, 7, 7, 9, 4]
    {0: 4, 1: 5, 2: 7, 3: 7, 4: 9, 5: 4}
    RangeIndex(start=0, stop=6, step=1)
    


```python
# Mutable?
wisc_cfb_wins[0] = 5
print(wisc_cfb_wins)
```

    0    5
    1    5
    2    7
    3    7
    4    9
    5    4
    dtype: int64
    


```python
# You can change the index after the fact
wisc_cfb_wins.index = range(2025, 2019,-1)
print(wisc_cfb_wins)

# just define the index to begin with
wisc_cfb_wins = pd.Series(list(wisc_cfb_wins), index = range(2025, 2019, -1))
print(wisc_cfb_wins)
```

    2025    5
    2024    5
    2023    7
    2022    7
    2021    9
    2020    4
    dtype: int64
    2025    5
    2024    5
    2023    7
    2022    7
    2021    9
    2020    4
    dtype: int64
    


```python
# Accessing with new index?
wisc_cfb_wins[2025] = 4
print(wisc_cfb_wins)
```

    2025    4
    2024    5
    2023    7
    2022    7
    2021    9
    2020    4
    dtype: int64
    


```python
# Locate by raw index or by label
print(wisc_cfb_wins.iloc[0])
print(wisc_cfb_wins.loc[2025])
```

    4
    4
    


```python
# Slicing series
print(wisc_cfb_wins.iloc[0:3])
print(wisc_cfb_wins.loc[2025:2023])
```

    2025    4
    2024    5
    2023    7
    dtype: int64
    2025    4
    2024    5
    2023    7
    dtype: int64
    


```python
# Conditionals?
bowls = wisc_cfb_wins >= 6
print(bowls)
print(wisc_cfb_wins[bowls])
```

    2025    False
    2024    False
    2023     True
    2022     True
    2021     True
    2020    False
    dtype: bool
    2023    7
    2022    7
    2021    9
    dtype: int64
    

## Practice - Series
1. Create a series of inflation where the index is country.
2. Print out entries that only have inflation above 3%
3. Create another series where the index is country but the values are "Low Inflation" if inflation is <= 2, "High Inflation" if inflation is between 2 and 50, and "Hyper Inflation" if inflation is above 50.


```python
inflation_dict = {'United States':2.9, 'United Arab Emirates':1.7, 'Angola':4.0, 'Venezuela':219.9}
# Results
# 1.
inflation_series = pd.Series(inflation_dict)
print(inflation_series)
# 2.
print(inflation_series[inflation_series > 3])
# 3.
inflation_type = []
for country in inflation_series.index:
    if inflation_series[country] <= 2:
        inflation_type.append("Low Inflation")
    elif inflation_series[country] <= 50:
        inflation_type.append("High Inflation")
    else:
        inflation_type.append("Hyper Inflation")

inflation_type_series = pd.Series(dict(zip(inflation_series.index, inflation_type)))
print(inflation_type_series)
```

    United States             2.9
    United Arab Emirates      1.7
    Angola                    4.0
    Venezuela               219.9
    dtype: float64
    Angola         4.0
    Venezuela    219.9
    dtype: float64
    United States            High Inflation
    United Arab Emirates      Low Inflation
    Angola                   High Inflation
    Venezuela               Hyper Inflation
    dtype: object
    

## Dataframes
Real data from [FRED](https://fred.stlouisfed.org/series/PAPOP)


```python
# Create your first dataframe!
data = {"state": ["Ohio", "Ohio", "Ohio", "Pennsylvania", "Pennsylvania", "Pennsylvania"],
        "year": [2000, 2001, 2002, 2001, 2002, 2003],
        "pop_growth": [0.95, 0.21, 0.18, 0.12, 0.26, 0.35]}

frame = pd.DataFrame(data)
print(frame)
```

              state  year  pop_growth
    0          Ohio  2000        0.95
    1          Ohio  2001        0.21
    2          Ohio  2002        0.18
    3  Pennsylvania  2001        0.12
    4  Pennsylvania  2002        0.26
    5  Pennsylvania  2003        0.35
    


```python
# Just look at the first five
frame.head()
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
      <th>state</th>
      <th>year</th>
      <th>pop_growth</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Ohio</td>
      <td>2000</td>
      <td>0.95</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Ohio</td>
      <td>2001</td>
      <td>0.21</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Ohio</td>
      <td>2002</td>
      <td>0.18</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Pennsylvania</td>
      <td>2001</td>
      <td>0.12</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Pennsylvania</td>
      <td>2002</td>
      <td>0.26</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Or the last five
frame.tail()
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
      <th>state</th>
      <th>year</th>
      <th>pop_growth</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>Ohio</td>
      <td>2001</td>
      <td>0.21</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Ohio</td>
      <td>2002</td>
      <td>0.18</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Pennsylvania</td>
      <td>2001</td>
      <td>0.12</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Pennsylvania</td>
      <td>2002</td>
      <td>0.26</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Pennsylvania</td>
      <td>2003</td>
      <td>0.35</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Selecting columns by name
frame["pop_growth"]
```




    0    0.95
    1    0.21
    2    0.18
    3    0.12
    4    0.26
    5    0.35
    Name: pop_growth, dtype: float64




```python
# Subsetting
frame[["state", "pop_growth"]]
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
      <th>state</th>
      <th>pop_growth</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Ohio</td>
      <td>0.95</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Ohio</td>
      <td>0.21</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Ohio</td>
      <td>0.18</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Pennsylvania</td>
      <td>0.12</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Pennsylvania</td>
      <td>0.26</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Pennsylvania</td>
      <td>0.35</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Changing column order
pd.DataFrame(data, columns=["year","state","pop_growth"])
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
      <th>state</th>
      <th>pop_growth</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2000</td>
      <td>Ohio</td>
      <td>0.95</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2001</td>
      <td>Ohio</td>
      <td>0.21</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2002</td>
      <td>Ohio</td>
      <td>0.18</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2001</td>
      <td>Pennsylvania</td>
      <td>0.12</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2002</td>
      <td>Pennsylvania</td>
      <td>0.26</td>
    </tr>
    <tr>
      <th>5</th>
      <td>2003</td>
      <td>Pennsylvania</td>
      <td>0.35</td>
    </tr>
  </tbody>
</table>
</div>




```python
# You can create new variables
frame["high_pop_growth"] = frame["pop_growth"] > 0.25
frame
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
      <th>state</th>
      <th>year</th>
      <th>pop_growth</th>
      <th>high_pop_growth</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Ohio</td>
      <td>2000</td>
      <td>0.95</td>
      <td>True</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Ohio</td>
      <td>2001</td>
      <td>0.21</td>
      <td>False</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Ohio</td>
      <td>2002</td>
      <td>0.18</td>
      <td>False</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Pennsylvania</td>
      <td>2001</td>
      <td>0.12</td>
      <td>False</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Pennsylvania</td>
      <td>2002</td>
      <td>0.26</td>
      <td>True</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Pennsylvania</td>
      <td>2003</td>
      <td>0.35</td>
      <td>True</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Rename columns
frame = frame.rename(columns={"pop_growth":"Population Growth", "high_pop_growth":"High Population Growth"})
frame
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
      <th>state</th>
      <th>year</th>
      <th>Population Growth</th>
      <th>High Population Growth</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Ohio</td>
      <td>2000</td>
      <td>0.95</td>
      <td>True</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Ohio</td>
      <td>2001</td>
      <td>0.21</td>
      <td>False</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Ohio</td>
      <td>2002</td>
      <td>0.18</td>
      <td>False</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Pennsylvania</td>
      <td>2001</td>
      <td>0.12</td>
      <td>False</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Pennsylvania</td>
      <td>2002</td>
      <td>0.26</td>
      <td>True</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Pennsylvania</td>
      <td>2003</td>
      <td>0.35</td>
      <td>True</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Locating Rows
print(frame.iloc[1,:])
print(frame.loc[1,:])
```

    state                      Ohio
    year                       2001
    Population Growth          0.21
    High Population Growth    False
    Name: 1, dtype: object
    state                      Ohio
    year                       2001
    Population Growth          0.21
    High Population Growth    False
    Name: 1, dtype: object
    


```python
# Columns
print(frame.iloc[:,1])
print(frame.loc[:,"year"])
```

    0    2000
    1    2001
    2    2002
    3    2001
    4    2002
    5    2003
    Name: year, dtype: int64
    0    2000
    1    2001
    2    2002
    3    2001
    4    2002
    5    2003
    Name: year, dtype: int64
    


```python
# Subsetting based on a condition
frame_PA = frame[frame["state"] == "Pennsylvania"]
print(frame_PA.iloc[0,:])
print(frame_PA.loc[3,:])
```

    state                     Pennsylvania
    year                              2001
    Population Growth                 0.12
    High Population Growth           False
    Name: 3, dtype: object
    state                     Pennsylvania
    year                              2001
    Population Growth                 0.12
    High Population Growth           False
    Name: 3, dtype: object
    


```python
# Reset index after subsetting
frame_PA = frame[frame["state"] == "Pennsylvania"].reset_index()
print(frame_PA)
```

       index         state  year  Population Growth  High Population Growth
    0      3  Pennsylvania  2001               0.12                   False
    1      4  Pennsylvania  2002               0.26                    True
    2      5  Pennsylvania  2003               0.35                    True
    


```python
# Drop old index
print(frame_PA.drop("index", axis = 1))
print(frame_PA)
frame_PA = frame_PA.drop("index", axis = 1)
print(frame_PA)
```

              state  year  Population Growth  High Population Growth
    0  Pennsylvania  2001               0.12                   False
    1  Pennsylvania  2002               0.26                    True
    2  Pennsylvania  2003               0.35                    True
       index         state  year  Population Growth  High Population Growth
    0      3  Pennsylvania  2001               0.12                   False
    1      4  Pennsylvania  2002               0.26                    True
    2      5  Pennsylvania  2003               0.35                    True
              state  year  Population Growth  High Population Growth
    0  Pennsylvania  2001               0.12                   False
    1  Pennsylvania  2002               0.26                    True
    2  Pennsylvania  2003               0.35                    True
    


```python
# Setting index to something that makes sense
frame_PA = frame_PA.set_index(frame_PA["year"])
frame_PA
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
      <th>state</th>
      <th>year</th>
      <th>Population Growth</th>
      <th>High Population Growth</th>
    </tr>
    <tr>
      <th>year</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2001</th>
      <td>Pennsylvania</td>
      <td>2001</td>
      <td>0.12</td>
      <td>False</td>
    </tr>
    <tr>
      <th>2002</th>
      <td>Pennsylvania</td>
      <td>2002</td>
      <td>0.26</td>
      <td>True</td>
    </tr>
    <tr>
      <th>2003</th>
      <td>Pennsylvania</td>
      <td>2003</td>
      <td>0.35</td>
      <td>True</td>
    </tr>
  </tbody>
</table>
</div>




```python
# loc works as expected
print(frame_PA.loc[2001,:])
print(frame_PA.iloc[0,:])
```

    state                     Pennsylvania
    year                              2001
    Population Growth                 0.12
    High Population Growth           False
    Name: 2001, dtype: object
    state                     Pennsylvania
    year                              2001
    Population Growth                 0.12
    High Population Growth           False
    Name: 2001, dtype: object
    

## Practice - Dataframes
1. Create a Dataframe of inflation and inflation type with index country.
   - Hint: What happens if you call DataFrame on a series?
   - Hint: How might you create a new variable that is a different series?
3. In `frame`, replace Pennsylvania with PA.


```python
#Results:
# 1.
inflation_df = pd.DataFrame(inflation_series).rename(columns={0:"Inflation"})
inflation_df["Inflation Type"] = inflation_type_series
print(inflation_df)
# 2. 
frame["state"] = frame["state"].replace("Pennsylvania", "PA")
print(frame)
```

                          Inflation   Inflation Type
    United States               2.9   High Inflation
    United Arab Emirates        1.7    Low Inflation
    Angola                      4.0   High Inflation
    Venezuela                 219.9  Hyper Inflation
      state  year  Population Growth  High Population Growth
    0  Ohio  2000               0.95                    True
    1  Ohio  2001               0.21                   False
    2  Ohio  2002               0.18                   False
    3    PA  2001               0.12                   False
    4    PA  2002               0.26                    True
    5    PA  2003               0.35                    True
    
