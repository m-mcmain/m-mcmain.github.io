---
layout: single
sitemap: false
permalink: /pages/Econ_390_SP26_L19_teaching/
title: Econ 390 Lecture 19
---

[Download Jupyter Notebook Empty](https://m-mcmain.github.io/files/Econ390SP26/Lectures/Lecture19_Merging_empty.ipynb)

Download Jupyter Notebook Completed

# Econ 390 - Lecture 19: Merging
Today we will go over how to merge datasets. We will be covering much of [8.1 and 8.2 from McKinney](https://wesmckinney.com/book/data-wrangling) and [Joins in Turrell](https://aeturrell.github.io/coding-for-economists/data-joining-data.html#joins).


```python
import pandas as pd

econ390path = "https://m-mcmain.github.io/files/Econ390SP26/"
```

## Concatenate


```python
# Read in the data
telework2023 = pd.read_csv(econ390path + "state-telework-2023.csv", index_col = 0)
telework2024 = pd.read_csv(econ390path + "state-telework-2024.csv", index_col = 0)

telework2023.head()
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
      <th>Teleworked_Some</th>
      <th>Teleworked_All</th>
      <th>Year</th>
    </tr>
    <tr>
      <th>State</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Alabama</th>
      <td>3.0</td>
      <td>4.6</td>
      <td>2023</td>
    </tr>
    <tr>
      <th>Alaska</th>
      <td>7.8</td>
      <td>6.1</td>
      <td>2023</td>
    </tr>
    <tr>
      <th>Arizona</th>
      <td>10.0</td>
      <td>13.9</td>
      <td>2023</td>
    </tr>
    <tr>
      <th>Arkansas</th>
      <td>3.9</td>
      <td>5.1</td>
      <td>2023</td>
    </tr>
    <tr>
      <th>California</th>
      <td>11.5</td>
      <td>11.1</td>
      <td>2023</td>
    </tr>
  </tbody>
</table>
</div>




```python
# concat method
pd.concat([telework2023, telework2024], axis = 1)
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
      <th>Teleworked_Some</th>
      <th>Teleworked_All</th>
      <th>Year</th>
      <th>Teleworked_Some</th>
      <th>Teleworked_All</th>
      <th>Year</th>
    </tr>
    <tr>
      <th>State</th>
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
      <th>Alabama</th>
      <td>3.0</td>
      <td>4.6</td>
      <td>2023.0</td>
      <td>4.4</td>
      <td>6.3</td>
      <td>2024</td>
    </tr>
    <tr>
      <th>Alaska</th>
      <td>7.8</td>
      <td>6.1</td>
      <td>2023.0</td>
      <td>9.5</td>
      <td>7.2</td>
      <td>2024</td>
    </tr>
    <tr>
      <th>Arizona</th>
      <td>10.0</td>
      <td>13.9</td>
      <td>2023.0</td>
      <td>12.6</td>
      <td>14.9</td>
      <td>2024</td>
    </tr>
    <tr>
      <th>Arkansas</th>
      <td>3.9</td>
      <td>5.1</td>
      <td>2023.0</td>
      <td>6.0</td>
      <td>5.6</td>
      <td>2024</td>
    </tr>
    <tr>
      <th>California</th>
      <td>11.5</td>
      <td>11.1</td>
      <td>2023.0</td>
      <td>14.1</td>
      <td>11.4</td>
      <td>2024</td>
    </tr>
    <tr>
      <th>Colorado</th>
      <td>16.0</td>
      <td>15.8</td>
      <td>2023.0</td>
      <td>16.6</td>
      <td>15.7</td>
      <td>2024</td>
    </tr>
    <tr>
      <th>Connecticut</th>
      <td>14.4</td>
      <td>10.7</td>
      <td>2023.0</td>
      <td>16.2</td>
      <td>9.0</td>
      <td>2024</td>
    </tr>
    <tr>
      <th>Delaware</th>
      <td>10.5</td>
      <td>10.0</td>
      <td>2023.0</td>
      <td>11.6</td>
      <td>10.7</td>
      <td>2024</td>
    </tr>
    <tr>
      <th>District of Columbia</th>
      <td>33.1</td>
      <td>23.4</td>
      <td>2023.0</td>
      <td>36.0</td>
      <td>20.8</td>
      <td>2024</td>
    </tr>
    <tr>
      <th>Florida</th>
      <td>5.3</td>
      <td>10.0</td>
      <td>2023.0</td>
      <td>7.7</td>
      <td>11.3</td>
      <td>2024</td>
    </tr>
    <tr>
      <th>Georgia</th>
      <td>6.9</td>
      <td>10.9</td>
      <td>2023.0</td>
      <td>10.6</td>
      <td>11.6</td>
      <td>2024</td>
    </tr>
    <tr>
      <th>Hawaii</th>
      <td>6.5</td>
      <td>6.4</td>
      <td>2023.0</td>
      <td>8.9</td>
      <td>6.8</td>
      <td>2024</td>
    </tr>
    <tr>
      <th>Idaho</th>
      <td>7.2</td>
      <td>8.0</td>
      <td>2023.0</td>
      <td>9.1</td>
      <td>10.6</td>
      <td>2024</td>
    </tr>
    <tr>
      <th>Illinois</th>
      <td>11.2</td>
      <td>9.7</td>
      <td>2023.0</td>
      <td>14.5</td>
      <td>11.8</td>
      <td>2024</td>
    </tr>
    <tr>
      <th>Indiana</th>
      <td>7.4</td>
      <td>7.4</td>
      <td>2023.0</td>
      <td>10.3</td>
      <td>7.9</td>
      <td>2024</td>
    </tr>
    <tr>
      <th>Iowa</th>
      <td>5.6</td>
      <td>6.6</td>
      <td>2023.0</td>
      <td>8.9</td>
      <td>6.8</td>
      <td>2024</td>
    </tr>
    <tr>
      <th>Kansas</th>
      <td>8.0</td>
      <td>8.5</td>
      <td>2023.0</td>
      <td>11.3</td>
      <td>9.0</td>
      <td>2024</td>
    </tr>
    <tr>
      <th>Kentucky</th>
      <td>6.6</td>
      <td>6.6</td>
      <td>2023.0</td>
      <td>8.1</td>
      <td>7.5</td>
      <td>2024</td>
    </tr>
    <tr>
      <th>Louisiana</th>
      <td>4.0</td>
      <td>5.5</td>
      <td>2023.0</td>
      <td>6.5</td>
      <td>6.3</td>
      <td>2024</td>
    </tr>
    <tr>
      <th>Maine</th>
      <td>10.1</td>
      <td>11.6</td>
      <td>2023.0</td>
      <td>11.9</td>
      <td>11.6</td>
      <td>2024</td>
    </tr>
    <tr>
      <th>Maryland</th>
      <td>13.0</td>
      <td>14.6</td>
      <td>2023.0</td>
      <td>16.3</td>
      <td>14.1</td>
      <td>2024</td>
    </tr>
    <tr>
      <th>Massachusetts</th>
      <td>16.1</td>
      <td>13.3</td>
      <td>2023.0</td>
      <td>18.9</td>
      <td>12.6</td>
      <td>2024</td>
    </tr>
    <tr>
      <th>Michigan</th>
      <td>10.2</td>
      <td>10.3</td>
      <td>2023.0</td>
      <td>11.9</td>
      <td>9.3</td>
      <td>2024</td>
    </tr>
    <tr>
      <th>Minnesota</th>
      <td>12.7</td>
      <td>12.4</td>
      <td>2023.0</td>
      <td>14.5</td>
      <td>11.4</td>
      <td>2024</td>
    </tr>
    <tr>
      <th>Mississippi</th>
      <td>1.6</td>
      <td>3.1</td>
      <td>2023.0</td>
      <td>2.9</td>
      <td>4.4</td>
      <td>2024</td>
    </tr>
    <tr>
      <th>Missouri</th>
      <td>7.6</td>
      <td>9.3</td>
      <td>2023.0</td>
      <td>11.7</td>
      <td>10.0</td>
      <td>2024</td>
    </tr>
    <tr>
      <th>Montana</th>
      <td>7.2</td>
      <td>8.8</td>
      <td>2023.0</td>
      <td>10.6</td>
      <td>10.0</td>
      <td>2024</td>
    </tr>
    <tr>
      <th>Nebraska</th>
      <td>8.5</td>
      <td>8.7</td>
      <td>2023.0</td>
      <td>9.6</td>
      <td>8.7</td>
      <td>2024</td>
    </tr>
    <tr>
      <th>Nevada</th>
      <td>5.1</td>
      <td>7.9</td>
      <td>2023.0</td>
      <td>6.5</td>
      <td>9.7</td>
      <td>2024</td>
    </tr>
    <tr>
      <th>New Hampshire</th>
      <td>10.4</td>
      <td>12.0</td>
      <td>2023.0</td>
      <td>12.8</td>
      <td>13.2</td>
      <td>2024</td>
    </tr>
    <tr>
      <th>New Jersey</th>
      <td>13.1</td>
      <td>11.2</td>
      <td>2023.0</td>
      <td>15.9</td>
      <td>11.2</td>
      <td>2024</td>
    </tr>
    <tr>
      <th>New Mexico</th>
      <td>5.8</td>
      <td>7.2</td>
      <td>2023.0</td>
      <td>8.5</td>
      <td>8.9</td>
      <td>2024</td>
    </tr>
    <tr>
      <th>New York</th>
      <td>10.7</td>
      <td>8.6</td>
      <td>2023.0</td>
      <td>12.8</td>
      <td>8.4</td>
      <td>2024</td>
    </tr>
    <tr>
      <th>North Carolina</th>
      <td>8.2</td>
      <td>10.4</td>
      <td>2023.0</td>
      <td>10.7</td>
      <td>11.3</td>
      <td>2024</td>
    </tr>
    <tr>
      <th>North Dakota</th>
      <td>5.3</td>
      <td>6.0</td>
      <td>2023.0</td>
      <td>7.9</td>
      <td>6.5</td>
      <td>2024</td>
    </tr>
    <tr>
      <th>Ohio</th>
      <td>9.4</td>
      <td>9.3</td>
      <td>2023.0</td>
      <td>11.4</td>
      <td>9.9</td>
      <td>2024</td>
    </tr>
    <tr>
      <th>Oklahoma</th>
      <td>5.7</td>
      <td>5.3</td>
      <td>2023.0</td>
      <td>7.6</td>
      <td>7.1</td>
      <td>2024</td>
    </tr>
    <tr>
      <th>Oregon</th>
      <td>12.1</td>
      <td>14.1</td>
      <td>2023.0</td>
      <td>14.1</td>
      <td>15.3</td>
      <td>2024</td>
    </tr>
    <tr>
      <th>Pennsylvania</th>
      <td>10.2</td>
      <td>11.0</td>
      <td>2023.0</td>
      <td>12.3</td>
      <td>11.5</td>
      <td>2024</td>
    </tr>
    <tr>
      <th>Rhode Island</th>
      <td>9.4</td>
      <td>9.9</td>
      <td>2023.0</td>
      <td>14.1</td>
      <td>9.2</td>
      <td>2024</td>
    </tr>
    <tr>
      <th>South Carolina</th>
      <td>5.8</td>
      <td>8.3</td>
      <td>2023.0</td>
      <td>8.7</td>
      <td>9.6</td>
      <td>2024</td>
    </tr>
    <tr>
      <th>South Dakota</th>
      <td>4.0</td>
      <td>5.5</td>
      <td>2023.0</td>
      <td>7.7</td>
      <td>6.8</td>
      <td>2024</td>
    </tr>
    <tr>
      <th>Tennessee</th>
      <td>6.8</td>
      <td>8.5</td>
      <td>2023.0</td>
      <td>9.0</td>
      <td>10.5</td>
      <td>2024</td>
    </tr>
    <tr>
      <th>Texas</th>
      <td>7.7</td>
      <td>10.7</td>
      <td>2023.0</td>
      <td>10.8</td>
      <td>11.7</td>
      <td>2024</td>
    </tr>
    <tr>
      <th>Utah</th>
      <td>9.8</td>
      <td>12.0</td>
      <td>2023.0</td>
      <td>13.2</td>
      <td>13.6</td>
      <td>2024</td>
    </tr>
    <tr>
      <th>Vermont</th>
      <td>10.8</td>
      <td>11.8</td>
      <td>2023.0</td>
      <td>14.0</td>
      <td>12.3</td>
      <td>2024</td>
    </tr>
    <tr>
      <th>Virginia</th>
      <td>13.3</td>
      <td>13.9</td>
      <td>2023.0</td>
      <td>15.1</td>
      <td>13.5</td>
      <td>2024</td>
    </tr>
    <tr>
      <th>Washington</th>
      <td>14.0</td>
      <td>14.5</td>
      <td>2023.0</td>
      <td>16.3</td>
      <td>14.5</td>
      <td>2024</td>
    </tr>
    <tr>
      <th>West Virginia</th>
      <td>4.2</td>
      <td>5.2</td>
      <td>2023.0</td>
      <td>5.9</td>
      <td>6.5</td>
      <td>2024</td>
    </tr>
    <tr>
      <th>Wisconsin</th>
      <td>8.0</td>
      <td>8.4</td>
      <td>2023.0</td>
      <td>11.8</td>
      <td>10.1</td>
      <td>2024</td>
    </tr>
    <tr>
      <th>Wyoming</th>
      <td>5.1</td>
      <td>5.1</td>
      <td>2023.0</td>
      <td>6.4</td>
      <td>7.1</td>
      <td>2024</td>
    </tr>
    <tr>
      <th>All States</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>11.9</td>
      <td>10.9</td>
      <td>2024</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Now specify the type for Year in the telework 2023 data
telework2023 = pd.read_csv(econ390path + "state-telework-2023.csv", dtype = {"Year":"Int64"}, index_col = 0)
telework2024 = pd.read_csv(econ390path + "state-telework-2024.csv", index_col = 0)

telework2023.head()
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
      <th>Teleworked_Some</th>
      <th>Teleworked_All</th>
      <th>Year</th>
    </tr>
    <tr>
      <th>State</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Alabama</th>
      <td>3.0</td>
      <td>4.6</td>
      <td>2023</td>
    </tr>
    <tr>
      <th>Alaska</th>
      <td>7.8</td>
      <td>6.1</td>
      <td>2023</td>
    </tr>
    <tr>
      <th>Arizona</th>
      <td>10.0</td>
      <td>13.9</td>
      <td>2023</td>
    </tr>
    <tr>
      <th>Arkansas</th>
      <td>3.9</td>
      <td>5.1</td>
      <td>2023</td>
    </tr>
    <tr>
      <th>California</th>
      <td>11.5</td>
      <td>11.1</td>
      <td>2023</td>
    </tr>
  </tbody>
</table>
</div>




```python
# This is still Bad
pd.concat([telework2023, telework2024], axis = 0)
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
      <th>Teleworked_Some</th>
      <th>Teleworked_All</th>
      <th>Year</th>
    </tr>
    <tr>
      <th>State</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Alabama</th>
      <td>3.0</td>
      <td>4.6</td>
      <td>2023</td>
    </tr>
    <tr>
      <th>Alaska</th>
      <td>7.8</td>
      <td>6.1</td>
      <td>2023</td>
    </tr>
    <tr>
      <th>Arizona</th>
      <td>10.0</td>
      <td>13.9</td>
      <td>2023</td>
    </tr>
    <tr>
      <th>Arkansas</th>
      <td>3.9</td>
      <td>5.1</td>
      <td>2023</td>
    </tr>
    <tr>
      <th>California</th>
      <td>11.5</td>
      <td>11.1</td>
      <td>2023</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>Virginia</th>
      <td>15.1</td>
      <td>13.5</td>
      <td>2024</td>
    </tr>
    <tr>
      <th>Washington</th>
      <td>16.3</td>
      <td>14.5</td>
      <td>2024</td>
    </tr>
    <tr>
      <th>West Virginia</th>
      <td>5.9</td>
      <td>6.5</td>
      <td>2024</td>
    </tr>
    <tr>
      <th>Wisconsin</th>
      <td>11.8</td>
      <td>10.1</td>
      <td>2024</td>
    </tr>
    <tr>
      <th>Wyoming</th>
      <td>6.4</td>
      <td>7.1</td>
      <td>2024</td>
    </tr>
  </tbody>
</table>
<p>103 rows × 3 columns</p>
</div>




```python
# Now we can have concat do even more work for us
Years = [2023, 2024]
pd.concat([telework2023, telework2024], keys = Years, axis = 0)
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
      <th>Teleworked_Some</th>
      <th>Teleworked_All</th>
      <th>Year</th>
    </tr>
    <tr>
      <th></th>
      <th>State</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th rowspan="5" valign="top">2023</th>
      <th>Alabama</th>
      <td>3.0</td>
      <td>4.6</td>
      <td>2023</td>
    </tr>
    <tr>
      <th>Alaska</th>
      <td>7.8</td>
      <td>6.1</td>
      <td>2023</td>
    </tr>
    <tr>
      <th>Arizona</th>
      <td>10.0</td>
      <td>13.9</td>
      <td>2023</td>
    </tr>
    <tr>
      <th>Arkansas</th>
      <td>3.9</td>
      <td>5.1</td>
      <td>2023</td>
    </tr>
    <tr>
      <th>California</th>
      <td>11.5</td>
      <td>11.1</td>
      <td>2023</td>
    </tr>
    <tr>
      <th>...</th>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th rowspan="5" valign="top">2024</th>
      <th>Virginia</th>
      <td>15.1</td>
      <td>13.5</td>
      <td>2024</td>
    </tr>
    <tr>
      <th>Washington</th>
      <td>16.3</td>
      <td>14.5</td>
      <td>2024</td>
    </tr>
    <tr>
      <th>West Virginia</th>
      <td>5.9</td>
      <td>6.5</td>
      <td>2024</td>
    </tr>
    <tr>
      <th>Wisconsin</th>
      <td>11.8</td>
      <td>10.1</td>
      <td>2024</td>
    </tr>
    <tr>
      <th>Wyoming</th>
      <td>6.4</td>
      <td>7.1</td>
      <td>2024</td>
    </tr>
  </tbody>
</table>
<p>103 rows × 3 columns</p>
</div>



## Hierarchical Indexing


```python
# Reset to just State as index
telework_stacked = pd.concat([telework2023, telework2024], axis = 0)
telework_stacked
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
      <th>Teleworked_Some</th>
      <th>Teleworked_All</th>
      <th>Year</th>
    </tr>
    <tr>
      <th>State</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Alabama</th>
      <td>3.0</td>
      <td>4.6</td>
      <td>2023</td>
    </tr>
    <tr>
      <th>Alaska</th>
      <td>7.8</td>
      <td>6.1</td>
      <td>2023</td>
    </tr>
    <tr>
      <th>Arizona</th>
      <td>10.0</td>
      <td>13.9</td>
      <td>2023</td>
    </tr>
    <tr>
      <th>Arkansas</th>
      <td>3.9</td>
      <td>5.1</td>
      <td>2023</td>
    </tr>
    <tr>
      <th>California</th>
      <td>11.5</td>
      <td>11.1</td>
      <td>2023</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>Virginia</th>
      <td>15.1</td>
      <td>13.5</td>
      <td>2024</td>
    </tr>
    <tr>
      <th>Washington</th>
      <td>16.3</td>
      <td>14.5</td>
      <td>2024</td>
    </tr>
    <tr>
      <th>West Virginia</th>
      <td>5.9</td>
      <td>6.5</td>
      <td>2024</td>
    </tr>
    <tr>
      <th>Wisconsin</th>
      <td>11.8</td>
      <td>10.1</td>
      <td>2024</td>
    </tr>
    <tr>
      <th>Wyoming</th>
      <td>6.4</td>
      <td>7.1</td>
      <td>2024</td>
    </tr>
  </tbody>
</table>
<p>103 rows × 3 columns</p>
</div>




```python
# Set two indices?
telework_stacked.reset_index().set_index(["State", "Year"]) 
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
      <th>Teleworked_Some</th>
      <th>Teleworked_All</th>
    </tr>
    <tr>
      <th>State</th>
      <th>Year</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Alabama</th>
      <th>2023</th>
      <td>3.0</td>
      <td>4.6</td>
    </tr>
    <tr>
      <th>Alaska</th>
      <th>2023</th>
      <td>7.8</td>
      <td>6.1</td>
    </tr>
    <tr>
      <th>Arizona</th>
      <th>2023</th>
      <td>10.0</td>
      <td>13.9</td>
    </tr>
    <tr>
      <th>Arkansas</th>
      <th>2023</th>
      <td>3.9</td>
      <td>5.1</td>
    </tr>
    <tr>
      <th>California</th>
      <th>2023</th>
      <td>11.5</td>
      <td>11.1</td>
    </tr>
    <tr>
      <th>...</th>
      <th>...</th>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>Virginia</th>
      <th>2024</th>
      <td>15.1</td>
      <td>13.5</td>
    </tr>
    <tr>
      <th>Washington</th>
      <th>2024</th>
      <td>16.3</td>
      <td>14.5</td>
    </tr>
    <tr>
      <th>West Virginia</th>
      <th>2024</th>
      <td>5.9</td>
      <td>6.5</td>
    </tr>
    <tr>
      <th>Wisconsin</th>
      <th>2024</th>
      <td>11.8</td>
      <td>10.1</td>
    </tr>
    <tr>
      <th>Wyoming</th>
      <th>2024</th>
      <td>6.4</td>
      <td>7.1</td>
    </tr>
  </tbody>
</table>
<p>103 rows × 2 columns</p>
</div>




```python
# Change the order?
telework_stacked.reset_index().set_index(["Year","State"])
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
      <th>Teleworked_Some</th>
      <th>Teleworked_All</th>
    </tr>
    <tr>
      <th>Year</th>
      <th>State</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th rowspan="5" valign="top">2023</th>
      <th>Alabama</th>
      <td>3.0</td>
      <td>4.6</td>
    </tr>
    <tr>
      <th>Alaska</th>
      <td>7.8</td>
      <td>6.1</td>
    </tr>
    <tr>
      <th>Arizona</th>
      <td>10.0</td>
      <td>13.9</td>
    </tr>
    <tr>
      <th>Arkansas</th>
      <td>3.9</td>
      <td>5.1</td>
    </tr>
    <tr>
      <th>California</th>
      <td>11.5</td>
      <td>11.1</td>
    </tr>
    <tr>
      <th>...</th>
      <th>...</th>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th rowspan="5" valign="top">2024</th>
      <th>Virginia</th>
      <td>15.1</td>
      <td>13.5</td>
    </tr>
    <tr>
      <th>Washington</th>
      <td>16.3</td>
      <td>14.5</td>
    </tr>
    <tr>
      <th>West Virginia</th>
      <td>5.9</td>
      <td>6.5</td>
    </tr>
    <tr>
      <th>Wisconsin</th>
      <td>11.8</td>
      <td>10.1</td>
    </tr>
    <tr>
      <th>Wyoming</th>
      <td>6.4</td>
      <td>7.1</td>
    </tr>
  </tbody>
</table>
<p>103 rows × 2 columns</p>
</div>




```python
# Setting the index with options
telework_stacked.set_index("Year", append=True, inplace = True)
telework_stacked
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
      <th>Teleworked_Some</th>
      <th>Teleworked_All</th>
    </tr>
    <tr>
      <th>State</th>
      <th>Year</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Alabama</th>
      <th>2023</th>
      <td>3.0</td>
      <td>4.6</td>
    </tr>
    <tr>
      <th>Alaska</th>
      <th>2023</th>
      <td>7.8</td>
      <td>6.1</td>
    </tr>
    <tr>
      <th>Arizona</th>
      <th>2023</th>
      <td>10.0</td>
      <td>13.9</td>
    </tr>
    <tr>
      <th>Arkansas</th>
      <th>2023</th>
      <td>3.9</td>
      <td>5.1</td>
    </tr>
    <tr>
      <th>California</th>
      <th>2023</th>
      <td>11.5</td>
      <td>11.1</td>
    </tr>
    <tr>
      <th>...</th>
      <th>...</th>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>Virginia</th>
      <th>2024</th>
      <td>15.1</td>
      <td>13.5</td>
    </tr>
    <tr>
      <th>Washington</th>
      <th>2024</th>
      <td>16.3</td>
      <td>14.5</td>
    </tr>
    <tr>
      <th>West Virginia</th>
      <th>2024</th>
      <td>5.9</td>
      <td>6.5</td>
    </tr>
    <tr>
      <th>Wisconsin</th>
      <th>2024</th>
      <td>11.8</td>
      <td>10.1</td>
    </tr>
    <tr>
      <th>Wyoming</th>
      <th>2024</th>
      <td>6.4</td>
      <td>7.1</td>
    </tr>
  </tbody>
</table>
<p>103 rows × 2 columns</p>
</div>




```python
# What *is* the index?
telework_stacked.index
```




    MultiIndex([(             'Alabama', 2023),
                (              'Alaska', 2023),
                (             'Arizona', 2023),
                (            'Arkansas', 2023),
                (          'California', 2023),
                (            'Colorado', 2023),
                (         'Connecticut', 2023),
                (            'Delaware', 2023),
                ('District of Columbia', 2023),
                (             'Florida', 2023),
                ...
                (        'South Dakota', 2024),
                (           'Tennessee', 2024),
                (               'Texas', 2024),
                (                'Utah', 2024),
                (             'Vermont', 2024),
                (            'Virginia', 2024),
                (          'Washington', 2024),
                (       'West Virginia', 2024),
                (           'Wisconsin', 2024),
                (             'Wyoming', 2024)],
               names=['State', 'Year'], length=103)




```python
# How does sort work
telework_stacked.sort_values('Teleworked_All')
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
      <th>Teleworked_Some</th>
      <th>Teleworked_All</th>
    </tr>
    <tr>
      <th>State</th>
      <th>Year</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th rowspan="2" valign="top">Mississippi</th>
      <th>2023</th>
      <td>1.6</td>
      <td>3.1</td>
    </tr>
    <tr>
      <th>2024</th>
      <td>2.9</td>
      <td>4.4</td>
    </tr>
    <tr>
      <th>Alabama</th>
      <th>2023</th>
      <td>3.0</td>
      <td>4.6</td>
    </tr>
    <tr>
      <th>Arkansas</th>
      <th>2023</th>
      <td>3.9</td>
      <td>5.1</td>
    </tr>
    <tr>
      <th>Wyoming</th>
      <th>2023</th>
      <td>5.1</td>
      <td>5.1</td>
    </tr>
    <tr>
      <th>...</th>
      <th>...</th>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>Oregon</th>
      <th>2024</th>
      <td>14.1</td>
      <td>15.3</td>
    </tr>
    <tr>
      <th rowspan="2" valign="top">Colorado</th>
      <th>2024</th>
      <td>16.6</td>
      <td>15.7</td>
    </tr>
    <tr>
      <th>2023</th>
      <td>16.0</td>
      <td>15.8</td>
    </tr>
    <tr>
      <th rowspan="2" valign="top">District of Columbia</th>
      <th>2024</th>
      <td>36.0</td>
      <td>20.8</td>
    </tr>
    <tr>
      <th>2023</th>
      <td>33.1</td>
      <td>23.4</td>
    </tr>
  </tbody>
</table>
<p>103 rows × 2 columns</p>
</div>




```python
# Sort in descending order
telework_stacked.sort_values('Teleworked_All', ascending=False)
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
      <th>Teleworked_Some</th>
      <th>Teleworked_All</th>
    </tr>
    <tr>
      <th>State</th>
      <th>Year</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th rowspan="2" valign="top">District of Columbia</th>
      <th>2023</th>
      <td>33.1</td>
      <td>23.4</td>
    </tr>
    <tr>
      <th>2024</th>
      <td>36.0</td>
      <td>20.8</td>
    </tr>
    <tr>
      <th rowspan="2" valign="top">Colorado</th>
      <th>2023</th>
      <td>16.0</td>
      <td>15.8</td>
    </tr>
    <tr>
      <th>2024</th>
      <td>16.6</td>
      <td>15.7</td>
    </tr>
    <tr>
      <th>Oregon</th>
      <th>2024</th>
      <td>14.1</td>
      <td>15.3</td>
    </tr>
    <tr>
      <th>...</th>
      <th>...</th>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>Arkansas</th>
      <th>2023</th>
      <td>3.9</td>
      <td>5.1</td>
    </tr>
    <tr>
      <th>Wyoming</th>
      <th>2023</th>
      <td>5.1</td>
      <td>5.1</td>
    </tr>
    <tr>
      <th>Alabama</th>
      <th>2023</th>
      <td>3.0</td>
      <td>4.6</td>
    </tr>
    <tr>
      <th rowspan="2" valign="top">Mississippi</th>
      <th>2024</th>
      <td>2.9</td>
      <td>4.4</td>
    </tr>
    <tr>
      <th>2023</th>
      <td>1.6</td>
      <td>3.1</td>
    </tr>
  </tbody>
</table>
<p>103 rows × 2 columns</p>
</div>




```python
# Sorting on index?
telework_stacked.sort_index
```




    <bound method DataFrame.sort_index of                     Teleworked_Some  Teleworked_All
    State         Year                                 
    Alabama       2023              3.0             4.6
    Alaska        2023              7.8             6.1
    Arizona       2023             10.0            13.9
    Arkansas      2023              3.9             5.1
    California    2023             11.5            11.1
    ...                             ...             ...
    Virginia      2024             15.1            13.5
    Washington    2024             16.3            14.5
    West Virginia 2024              5.9             6.5
    Wisconsin     2024             11.8            10.1
    Wyoming       2024              6.4             7.1
    
    [103 rows x 2 columns]>




```python
# Specify different levels and ascending
telework_stacked.sort_index(level=['Year','State'], ascending=[True,False])
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
      <th>Teleworked_Some</th>
      <th>Teleworked_All</th>
    </tr>
    <tr>
      <th>State</th>
      <th>Year</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Wyoming</th>
      <th>2023</th>
      <td>5.1</td>
      <td>5.1</td>
    </tr>
    <tr>
      <th>Wisconsin</th>
      <th>2023</th>
      <td>8.0</td>
      <td>8.4</td>
    </tr>
    <tr>
      <th>West Virginia</th>
      <th>2023</th>
      <td>4.2</td>
      <td>5.2</td>
    </tr>
    <tr>
      <th>Washington</th>
      <th>2023</th>
      <td>14.0</td>
      <td>14.5</td>
    </tr>
    <tr>
      <th>Virginia</th>
      <th>2023</th>
      <td>13.3</td>
      <td>13.9</td>
    </tr>
    <tr>
      <th>...</th>
      <th>...</th>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>Arkansas</th>
      <th>2024</th>
      <td>6.0</td>
      <td>5.6</td>
    </tr>
    <tr>
      <th>Arizona</th>
      <th>2024</th>
      <td>12.6</td>
      <td>14.9</td>
    </tr>
    <tr>
      <th>All States</th>
      <th>2024</th>
      <td>11.9</td>
      <td>10.9</td>
    </tr>
    <tr>
      <th>Alaska</th>
      <th>2024</th>
      <td>9.5</td>
      <td>7.2</td>
    </tr>
    <tr>
      <th>Alabama</th>
      <th>2024</th>
      <td>4.4</td>
      <td>6.3</td>
    </tr>
  </tbody>
</table>
<p>103 rows × 2 columns</p>
</div>




```python
# Alternative options for sort_index
telework_stacked.sort_index(level=[0,1], ascending=[True,False])
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
      <th>Teleworked_Some</th>
      <th>Teleworked_All</th>
    </tr>
    <tr>
      <th>State</th>
      <th>Year</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th rowspan="2" valign="top">Alabama</th>
      <th>2024</th>
      <td>4.4</td>
      <td>6.3</td>
    </tr>
    <tr>
      <th>2023</th>
      <td>3.0</td>
      <td>4.6</td>
    </tr>
    <tr>
      <th rowspan="2" valign="top">Alaska</th>
      <th>2024</th>
      <td>9.5</td>
      <td>7.2</td>
    </tr>
    <tr>
      <th>2023</th>
      <td>7.8</td>
      <td>6.1</td>
    </tr>
    <tr>
      <th>All States</th>
      <th>2024</th>
      <td>11.9</td>
      <td>10.9</td>
    </tr>
    <tr>
      <th>...</th>
      <th>...</th>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>West Virginia</th>
      <th>2023</th>
      <td>4.2</td>
      <td>5.2</td>
    </tr>
    <tr>
      <th rowspan="2" valign="top">Wisconsin</th>
      <th>2024</th>
      <td>11.8</td>
      <td>10.1</td>
    </tr>
    <tr>
      <th>2023</th>
      <td>8.0</td>
      <td>8.4</td>
    </tr>
    <tr>
      <th rowspan="2" valign="top">Wyoming</th>
      <th>2024</th>
      <td>6.4</td>
      <td>7.1</td>
    </tr>
    <tr>
      <th>2023</th>
      <td>5.1</td>
      <td>5.1</td>
    </tr>
  </tbody>
</table>
<p>103 rows × 2 columns</p>
</div>




```python
# Basic
telework_stacked.sort_index(inplace=True)
telework_stacked
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
      <th>Teleworked_Some</th>
      <th>Teleworked_All</th>
    </tr>
    <tr>
      <th>State</th>
      <th>Year</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th rowspan="2" valign="top">Alabama</th>
      <th>2023</th>
      <td>3.0</td>
      <td>4.6</td>
    </tr>
    <tr>
      <th>2024</th>
      <td>4.4</td>
      <td>6.3</td>
    </tr>
    <tr>
      <th rowspan="2" valign="top">Alaska</th>
      <th>2023</th>
      <td>7.8</td>
      <td>6.1</td>
    </tr>
    <tr>
      <th>2024</th>
      <td>9.5</td>
      <td>7.2</td>
    </tr>
    <tr>
      <th>All States</th>
      <th>2024</th>
      <td>11.9</td>
      <td>10.9</td>
    </tr>
    <tr>
      <th>...</th>
      <th>...</th>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>West Virginia</th>
      <th>2024</th>
      <td>5.9</td>
      <td>6.5</td>
    </tr>
    <tr>
      <th rowspan="2" valign="top">Wisconsin</th>
      <th>2023</th>
      <td>8.0</td>
      <td>8.4</td>
    </tr>
    <tr>
      <th>2024</th>
      <td>11.8</td>
      <td>10.1</td>
    </tr>
    <tr>
      <th rowspan="2" valign="top">Wyoming</th>
      <th>2023</th>
      <td>5.1</td>
      <td>5.1</td>
    </tr>
    <tr>
      <th>2024</th>
      <td>6.4</td>
      <td>7.1</td>
    </tr>
  </tbody>
</table>
<p>103 rows × 2 columns</p>
</div>




```python
# Finding specific entries for one index
telework_stacked.loc["Wisconsin",:]
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
      <th>Teleworked_Some</th>
      <th>Teleworked_All</th>
    </tr>
    <tr>
      <th>Year</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2023</th>
      <td>8.0</td>
      <td>8.4</td>
    </tr>
    <tr>
      <th>2024</th>
      <td>11.8</td>
      <td>10.1</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Finding specific entries for two indices
telework_stacked.loc[("Wisconsin", 2023),:]
```




    Teleworked_Some    8.0
    Teleworked_All     8.4
    Name: (Wisconsin, 2023), dtype: float64




```python
# Comparison
telework_stacked.loc["Wisconsin"]
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
      <th>Teleworked_Some</th>
      <th>Teleworked_All</th>
    </tr>
    <tr>
      <th>Year</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2023</th>
      <td>8.0</td>
      <td>8.4</td>
    </tr>
    <tr>
      <th>2024</th>
      <td>11.8</td>
      <td>10.1</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Stacked Loc
telework_stacked.loc[("Wisconsin", 2023)]
```




    Teleworked_Some    8.0
    Teleworked_All     8.4
    Name: (Wisconsin, 2023), dtype: float64




```python
# xs turns the dataframe into a cross section for the specified index
telework_stacked.xs(2023, level="Year")
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
      <th>Teleworked_Some</th>
      <th>Teleworked_All</th>
    </tr>
    <tr>
      <th>State</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Alabama</th>
      <td>3.0</td>
      <td>4.6</td>
    </tr>
    <tr>
      <th>Alaska</th>
      <td>7.8</td>
      <td>6.1</td>
    </tr>
    <tr>
      <th>Arizona</th>
      <td>10.0</td>
      <td>13.9</td>
    </tr>
    <tr>
      <th>Arkansas</th>
      <td>3.9</td>
      <td>5.1</td>
    </tr>
    <tr>
      <th>California</th>
      <td>11.5</td>
      <td>11.1</td>
    </tr>
    <tr>
      <th>Colorado</th>
      <td>16.0</td>
      <td>15.8</td>
    </tr>
    <tr>
      <th>Connecticut</th>
      <td>14.4</td>
      <td>10.7</td>
    </tr>
    <tr>
      <th>Delaware</th>
      <td>10.5</td>
      <td>10.0</td>
    </tr>
    <tr>
      <th>District of Columbia</th>
      <td>33.1</td>
      <td>23.4</td>
    </tr>
    <tr>
      <th>Florida</th>
      <td>5.3</td>
      <td>10.0</td>
    </tr>
    <tr>
      <th>Georgia</th>
      <td>6.9</td>
      <td>10.9</td>
    </tr>
    <tr>
      <th>Hawaii</th>
      <td>6.5</td>
      <td>6.4</td>
    </tr>
    <tr>
      <th>Idaho</th>
      <td>7.2</td>
      <td>8.0</td>
    </tr>
    <tr>
      <th>Illinois</th>
      <td>11.2</td>
      <td>9.7</td>
    </tr>
    <tr>
      <th>Indiana</th>
      <td>7.4</td>
      <td>7.4</td>
    </tr>
    <tr>
      <th>Iowa</th>
      <td>5.6</td>
      <td>6.6</td>
    </tr>
    <tr>
      <th>Kansas</th>
      <td>8.0</td>
      <td>8.5</td>
    </tr>
    <tr>
      <th>Kentucky</th>
      <td>6.6</td>
      <td>6.6</td>
    </tr>
    <tr>
      <th>Louisiana</th>
      <td>4.0</td>
      <td>5.5</td>
    </tr>
    <tr>
      <th>Maine</th>
      <td>10.1</td>
      <td>11.6</td>
    </tr>
    <tr>
      <th>Maryland</th>
      <td>13.0</td>
      <td>14.6</td>
    </tr>
    <tr>
      <th>Massachusetts</th>
      <td>16.1</td>
      <td>13.3</td>
    </tr>
    <tr>
      <th>Michigan</th>
      <td>10.2</td>
      <td>10.3</td>
    </tr>
    <tr>
      <th>Minnesota</th>
      <td>12.7</td>
      <td>12.4</td>
    </tr>
    <tr>
      <th>Mississippi</th>
      <td>1.6</td>
      <td>3.1</td>
    </tr>
    <tr>
      <th>Missouri</th>
      <td>7.6</td>
      <td>9.3</td>
    </tr>
    <tr>
      <th>Montana</th>
      <td>7.2</td>
      <td>8.8</td>
    </tr>
    <tr>
      <th>Nebraska</th>
      <td>8.5</td>
      <td>8.7</td>
    </tr>
    <tr>
      <th>Nevada</th>
      <td>5.1</td>
      <td>7.9</td>
    </tr>
    <tr>
      <th>New Hampshire</th>
      <td>10.4</td>
      <td>12.0</td>
    </tr>
    <tr>
      <th>New Jersey</th>
      <td>13.1</td>
      <td>11.2</td>
    </tr>
    <tr>
      <th>New Mexico</th>
      <td>5.8</td>
      <td>7.2</td>
    </tr>
    <tr>
      <th>New York</th>
      <td>10.7</td>
      <td>8.6</td>
    </tr>
    <tr>
      <th>North Carolina</th>
      <td>8.2</td>
      <td>10.4</td>
    </tr>
    <tr>
      <th>North Dakota</th>
      <td>5.3</td>
      <td>6.0</td>
    </tr>
    <tr>
      <th>Ohio</th>
      <td>9.4</td>
      <td>9.3</td>
    </tr>
    <tr>
      <th>Oklahoma</th>
      <td>5.7</td>
      <td>5.3</td>
    </tr>
    <tr>
      <th>Oregon</th>
      <td>12.1</td>
      <td>14.1</td>
    </tr>
    <tr>
      <th>Pennsylvania</th>
      <td>10.2</td>
      <td>11.0</td>
    </tr>
    <tr>
      <th>Rhode Island</th>
      <td>9.4</td>
      <td>9.9</td>
    </tr>
    <tr>
      <th>South Carolina</th>
      <td>5.8</td>
      <td>8.3</td>
    </tr>
    <tr>
      <th>South Dakota</th>
      <td>4.0</td>
      <td>5.5</td>
    </tr>
    <tr>
      <th>Tennessee</th>
      <td>6.8</td>
      <td>8.5</td>
    </tr>
    <tr>
      <th>Texas</th>
      <td>7.7</td>
      <td>10.7</td>
    </tr>
    <tr>
      <th>Utah</th>
      <td>9.8</td>
      <td>12.0</td>
    </tr>
    <tr>
      <th>Vermont</th>
      <td>10.8</td>
      <td>11.8</td>
    </tr>
    <tr>
      <th>Virginia</th>
      <td>13.3</td>
      <td>13.9</td>
    </tr>
    <tr>
      <th>Washington</th>
      <td>14.0</td>
      <td>14.5</td>
    </tr>
    <tr>
      <th>West Virginia</th>
      <td>4.2</td>
      <td>5.2</td>
    </tr>
    <tr>
      <th>Wisconsin</th>
      <td>8.0</td>
      <td>8.4</td>
    </tr>
    <tr>
      <th>Wyoming</th>
      <td>5.1</td>
      <td>5.1</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Different process, same result
telework_stacked.xs("Wisconsin", level="State")
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
      <th>Teleworked_Some</th>
      <th>Teleworked_All</th>
    </tr>
    <tr>
      <th>Year</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2023</th>
      <td>8.0</td>
      <td>8.4</td>
    </tr>
    <tr>
      <th>2024</th>
      <td>11.8</td>
      <td>10.1</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Keep the level
telework_stacked.xs("Wisconsin", level="State", drop_level=False)
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
      <th>Teleworked_Some</th>
      <th>Teleworked_All</th>
    </tr>
    <tr>
      <th>State</th>
      <th>Year</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th rowspan="2" valign="top">Wisconsin</th>
      <th>2023</th>
      <td>8.0</td>
      <td>8.4</td>
    </tr>
    <tr>
      <th>2024</th>
      <td>11.8</td>
      <td>10.1</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Multiple states?
telework_stacked.xs(["Wisconsin","Michigan"], level="State", drop_level=False)
```


    ---------------------------------------------------------------------------

    TypeError                                 Traceback (most recent call last)

    ~\AppData\Local\Temp\ipykernel_11912\2178257805.py in ?()
          1 # Multiple states?
    ----> 2 telework_stacked.xs(["Wisconsin","Michigan"], level="State", drop_level=False)
    

    ~\anaconda3\Lib\site-packages\pandas\core\generic.py in ?(self, key, axis, level, drop_level)
       4265         axis = self._get_axis_number(axis)
       4266         labels = self._get_axis(axis)
       4267 
       4268         if isinstance(key, list):
    -> 4269             raise TypeError("list keys are not supported in xs, pass a tuple instead")
       4270 
       4271         if level is not None:
       4272             if not isinstance(labels, MultiIndex):
    

    TypeError: list keys are not supported in xs, pass a tuple instead



```python
# Work around with concat
telework_WI = telework_stacked.xs("Wisconsin", level="State", drop_level=False)
telework_MI = telework_stacked.xs("Michigan", level="State", drop_level=False)
pd.concat([telework_WI, telework_MI])
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
      <th>Teleworked_Some</th>
      <th>Teleworked_All</th>
    </tr>
    <tr>
      <th>State</th>
      <th>Year</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th rowspan="2" valign="top">Wisconsin</th>
      <th>2023</th>
      <td>8.0</td>
      <td>8.4</td>
    </tr>
    <tr>
      <th>2024</th>
      <td>11.8</td>
      <td>10.1</td>
    </tr>
    <tr>
      <th rowspan="2" valign="top">Michigan</th>
      <th>2023</th>
      <td>10.2</td>
      <td>10.3</td>
    </tr>
    <tr>
      <th>2024</th>
      <td>11.9</td>
      <td>9.3</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Loc works fine
telework_stacked.loc[["Wisconsin", "Michigan"]]
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
      <th>Teleworked_Some</th>
      <th>Teleworked_All</th>
    </tr>
    <tr>
      <th>State</th>
      <th>Year</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th rowspan="2" valign="top">Wisconsin</th>
      <th>2023</th>
      <td>8.0</td>
      <td>8.4</td>
    </tr>
    <tr>
      <th>2024</th>
      <td>11.8</td>
      <td>10.1</td>
    </tr>
    <tr>
      <th rowspan="2" valign="top">Michigan</th>
      <th>2023</th>
      <td>10.2</td>
      <td>10.3</td>
    </tr>
    <tr>
      <th>2024</th>
      <td>11.9</td>
      <td>9.3</td>
    </tr>
  </tbody>
</table>
</div>




```python
# send to csv
telework_stacked.to_csv("telework_stacked.csv")
```


```python
# read in with multiple indices
pd.read_csv("telework_stacked.csv", index_col = ["State", "Year"])
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
      <th>Teleworked_Some</th>
      <th>Teleworked_All</th>
    </tr>
    <tr>
      <th>State</th>
      <th>Year</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th rowspan="2" valign="top">Alabama</th>
      <th>2023</th>
      <td>3.0</td>
      <td>4.6</td>
    </tr>
    <tr>
      <th>2024</th>
      <td>4.4</td>
      <td>6.3</td>
    </tr>
    <tr>
      <th rowspan="2" valign="top">Alaska</th>
      <th>2023</th>
      <td>7.8</td>
      <td>6.1</td>
    </tr>
    <tr>
      <th>2024</th>
      <td>9.5</td>
      <td>7.2</td>
    </tr>
    <tr>
      <th>All States</th>
      <th>2024</th>
      <td>11.9</td>
      <td>10.9</td>
    </tr>
    <tr>
      <th>...</th>
      <th>...</th>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>West Virginia</th>
      <th>2024</th>
      <td>5.9</td>
      <td>6.5</td>
    </tr>
    <tr>
      <th rowspan="2" valign="top">Wisconsin</th>
      <th>2023</th>
      <td>8.0</td>
      <td>8.4</td>
    </tr>
    <tr>
      <th>2024</th>
      <td>11.8</td>
      <td>10.1</td>
    </tr>
    <tr>
      <th rowspan="2" valign="top">Wyoming</th>
      <th>2023</th>
      <td>5.1</td>
      <td>5.1</td>
    </tr>
    <tr>
      <th>2024</th>
      <td>6.4</td>
      <td>7.1</td>
    </tr>
  </tbody>
</table>
<p>103 rows × 2 columns</p>
</div>



## Practice - Hierarchical Indexing
1. Find the telework data for D.C.
2. Find the telework data for D.C. in 2023
3. Find the percent of workers who entirely teleworked in D.C. in 2023
4. Get all of the data for teleworking in 2023


```python
# Results
print(telework_stacked.loc["District of Columbia"])
print(telework_stacked.loc["District of Columbia", 2023])
print(telework_stacked.loc["District of Columbia", 2023].loc["Teleworked_All"])
telework_stacked.xs(2023, level="Year")
```

          Teleworked_Some  Teleworked_All
    Year                                 
    2023             33.1            23.4
    2024             36.0            20.8
    Teleworked_Some    33.1
    Teleworked_All     23.4
    Name: (District of Columbia, 2023), dtype: float64
    23.4
    




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
      <th>Teleworked_Some</th>
      <th>Teleworked_All</th>
    </tr>
    <tr>
      <th>State</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Alabama</th>
      <td>3.0</td>
      <td>4.6</td>
    </tr>
    <tr>
      <th>Alaska</th>
      <td>7.8</td>
      <td>6.1</td>
    </tr>
    <tr>
      <th>Arizona</th>
      <td>10.0</td>
      <td>13.9</td>
    </tr>
    <tr>
      <th>Arkansas</th>
      <td>3.9</td>
      <td>5.1</td>
    </tr>
    <tr>
      <th>California</th>
      <td>11.5</td>
      <td>11.1</td>
    </tr>
    <tr>
      <th>Colorado</th>
      <td>16.0</td>
      <td>15.8</td>
    </tr>
    <tr>
      <th>Connecticut</th>
      <td>14.4</td>
      <td>10.7</td>
    </tr>
    <tr>
      <th>Delaware</th>
      <td>10.5</td>
      <td>10.0</td>
    </tr>
    <tr>
      <th>District of Columbia</th>
      <td>33.1</td>
      <td>23.4</td>
    </tr>
    <tr>
      <th>Florida</th>
      <td>5.3</td>
      <td>10.0</td>
    </tr>
    <tr>
      <th>Georgia</th>
      <td>6.9</td>
      <td>10.9</td>
    </tr>
    <tr>
      <th>Hawaii</th>
      <td>6.5</td>
      <td>6.4</td>
    </tr>
    <tr>
      <th>Idaho</th>
      <td>7.2</td>
      <td>8.0</td>
    </tr>
    <tr>
      <th>Illinois</th>
      <td>11.2</td>
      <td>9.7</td>
    </tr>
    <tr>
      <th>Indiana</th>
      <td>7.4</td>
      <td>7.4</td>
    </tr>
    <tr>
      <th>Iowa</th>
      <td>5.6</td>
      <td>6.6</td>
    </tr>
    <tr>
      <th>Kansas</th>
      <td>8.0</td>
      <td>8.5</td>
    </tr>
    <tr>
      <th>Kentucky</th>
      <td>6.6</td>
      <td>6.6</td>
    </tr>
    <tr>
      <th>Louisiana</th>
      <td>4.0</td>
      <td>5.5</td>
    </tr>
    <tr>
      <th>Maine</th>
      <td>10.1</td>
      <td>11.6</td>
    </tr>
    <tr>
      <th>Maryland</th>
      <td>13.0</td>
      <td>14.6</td>
    </tr>
    <tr>
      <th>Massachusetts</th>
      <td>16.1</td>
      <td>13.3</td>
    </tr>
    <tr>
      <th>Michigan</th>
      <td>10.2</td>
      <td>10.3</td>
    </tr>
    <tr>
      <th>Minnesota</th>
      <td>12.7</td>
      <td>12.4</td>
    </tr>
    <tr>
      <th>Mississippi</th>
      <td>1.6</td>
      <td>3.1</td>
    </tr>
    <tr>
      <th>Missouri</th>
      <td>7.6</td>
      <td>9.3</td>
    </tr>
    <tr>
      <th>Montana</th>
      <td>7.2</td>
      <td>8.8</td>
    </tr>
    <tr>
      <th>Nebraska</th>
      <td>8.5</td>
      <td>8.7</td>
    </tr>
    <tr>
      <th>Nevada</th>
      <td>5.1</td>
      <td>7.9</td>
    </tr>
    <tr>
      <th>New Hampshire</th>
      <td>10.4</td>
      <td>12.0</td>
    </tr>
    <tr>
      <th>New Jersey</th>
      <td>13.1</td>
      <td>11.2</td>
    </tr>
    <tr>
      <th>New Mexico</th>
      <td>5.8</td>
      <td>7.2</td>
    </tr>
    <tr>
      <th>New York</th>
      <td>10.7</td>
      <td>8.6</td>
    </tr>
    <tr>
      <th>North Carolina</th>
      <td>8.2</td>
      <td>10.4</td>
    </tr>
    <tr>
      <th>North Dakota</th>
      <td>5.3</td>
      <td>6.0</td>
    </tr>
    <tr>
      <th>Ohio</th>
      <td>9.4</td>
      <td>9.3</td>
    </tr>
    <tr>
      <th>Oklahoma</th>
      <td>5.7</td>
      <td>5.3</td>
    </tr>
    <tr>
      <th>Oregon</th>
      <td>12.1</td>
      <td>14.1</td>
    </tr>
    <tr>
      <th>Pennsylvania</th>
      <td>10.2</td>
      <td>11.0</td>
    </tr>
    <tr>
      <th>Rhode Island</th>
      <td>9.4</td>
      <td>9.9</td>
    </tr>
    <tr>
      <th>South Carolina</th>
      <td>5.8</td>
      <td>8.3</td>
    </tr>
    <tr>
      <th>South Dakota</th>
      <td>4.0</td>
      <td>5.5</td>
    </tr>
    <tr>
      <th>Tennessee</th>
      <td>6.8</td>
      <td>8.5</td>
    </tr>
    <tr>
      <th>Texas</th>
      <td>7.7</td>
      <td>10.7</td>
    </tr>
    <tr>
      <th>Utah</th>
      <td>9.8</td>
      <td>12.0</td>
    </tr>
    <tr>
      <th>Vermont</th>
      <td>10.8</td>
      <td>11.8</td>
    </tr>
    <tr>
      <th>Virginia</th>
      <td>13.3</td>
      <td>13.9</td>
    </tr>
    <tr>
      <th>Washington</th>
      <td>14.0</td>
      <td>14.5</td>
    </tr>
    <tr>
      <th>West Virginia</th>
      <td>4.2</td>
      <td>5.2</td>
    </tr>
    <tr>
      <th>Wisconsin</th>
      <td>8.0</td>
      <td>8.4</td>
    </tr>
    <tr>
      <th>Wyoming</th>
      <td>5.1</td>
      <td>5.1</td>
    </tr>
  </tbody>
</table>
</div>



## Merging


```python
pd.merge(telework2023, telework2024)
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
      <th>Teleworked_Some</th>
      <th>Teleworked_All</th>
      <th>Year</th>
    </tr>
  </thead>
  <tbody>
  </tbody>
</table>
</div>




```python
pd.merge(telework2023, telework2024, on = "State")
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
      <th>Teleworked_Some_x</th>
      <th>Teleworked_All_x</th>
      <th>Year_x</th>
      <th>Teleworked_Some_y</th>
      <th>Teleworked_All_y</th>
      <th>Year_y</th>
    </tr>
    <tr>
      <th>State</th>
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
      <th>Alabama</th>
      <td>3.0</td>
      <td>4.6</td>
      <td>2023</td>
      <td>4.4</td>
      <td>6.3</td>
      <td>2024</td>
    </tr>
    <tr>
      <th>Alaska</th>
      <td>7.8</td>
      <td>6.1</td>
      <td>2023</td>
      <td>9.5</td>
      <td>7.2</td>
      <td>2024</td>
    </tr>
    <tr>
      <th>Arizona</th>
      <td>10.0</td>
      <td>13.9</td>
      <td>2023</td>
      <td>12.6</td>
      <td>14.9</td>
      <td>2024</td>
    </tr>
    <tr>
      <th>Arkansas</th>
      <td>3.9</td>
      <td>5.1</td>
      <td>2023</td>
      <td>6.0</td>
      <td>5.6</td>
      <td>2024</td>
    </tr>
    <tr>
      <th>California</th>
      <td>11.5</td>
      <td>11.1</td>
      <td>2023</td>
      <td>14.1</td>
      <td>11.4</td>
      <td>2024</td>
    </tr>
    <tr>
      <th>Colorado</th>
      <td>16.0</td>
      <td>15.8</td>
      <td>2023</td>
      <td>16.6</td>
      <td>15.7</td>
      <td>2024</td>
    </tr>
    <tr>
      <th>Connecticut</th>
      <td>14.4</td>
      <td>10.7</td>
      <td>2023</td>
      <td>16.2</td>
      <td>9.0</td>
      <td>2024</td>
    </tr>
    <tr>
      <th>Delaware</th>
      <td>10.5</td>
      <td>10.0</td>
      <td>2023</td>
      <td>11.6</td>
      <td>10.7</td>
      <td>2024</td>
    </tr>
    <tr>
      <th>District of Columbia</th>
      <td>33.1</td>
      <td>23.4</td>
      <td>2023</td>
      <td>36.0</td>
      <td>20.8</td>
      <td>2024</td>
    </tr>
    <tr>
      <th>Florida</th>
      <td>5.3</td>
      <td>10.0</td>
      <td>2023</td>
      <td>7.7</td>
      <td>11.3</td>
      <td>2024</td>
    </tr>
    <tr>
      <th>Georgia</th>
      <td>6.9</td>
      <td>10.9</td>
      <td>2023</td>
      <td>10.6</td>
      <td>11.6</td>
      <td>2024</td>
    </tr>
    <tr>
      <th>Hawaii</th>
      <td>6.5</td>
      <td>6.4</td>
      <td>2023</td>
      <td>8.9</td>
      <td>6.8</td>
      <td>2024</td>
    </tr>
    <tr>
      <th>Idaho</th>
      <td>7.2</td>
      <td>8.0</td>
      <td>2023</td>
      <td>9.1</td>
      <td>10.6</td>
      <td>2024</td>
    </tr>
    <tr>
      <th>Illinois</th>
      <td>11.2</td>
      <td>9.7</td>
      <td>2023</td>
      <td>14.5</td>
      <td>11.8</td>
      <td>2024</td>
    </tr>
    <tr>
      <th>Indiana</th>
      <td>7.4</td>
      <td>7.4</td>
      <td>2023</td>
      <td>10.3</td>
      <td>7.9</td>
      <td>2024</td>
    </tr>
    <tr>
      <th>Iowa</th>
      <td>5.6</td>
      <td>6.6</td>
      <td>2023</td>
      <td>8.9</td>
      <td>6.8</td>
      <td>2024</td>
    </tr>
    <tr>
      <th>Kansas</th>
      <td>8.0</td>
      <td>8.5</td>
      <td>2023</td>
      <td>11.3</td>
      <td>9.0</td>
      <td>2024</td>
    </tr>
    <tr>
      <th>Kentucky</th>
      <td>6.6</td>
      <td>6.6</td>
      <td>2023</td>
      <td>8.1</td>
      <td>7.5</td>
      <td>2024</td>
    </tr>
    <tr>
      <th>Louisiana</th>
      <td>4.0</td>
      <td>5.5</td>
      <td>2023</td>
      <td>6.5</td>
      <td>6.3</td>
      <td>2024</td>
    </tr>
    <tr>
      <th>Maine</th>
      <td>10.1</td>
      <td>11.6</td>
      <td>2023</td>
      <td>11.9</td>
      <td>11.6</td>
      <td>2024</td>
    </tr>
    <tr>
      <th>Maryland</th>
      <td>13.0</td>
      <td>14.6</td>
      <td>2023</td>
      <td>16.3</td>
      <td>14.1</td>
      <td>2024</td>
    </tr>
    <tr>
      <th>Massachusetts</th>
      <td>16.1</td>
      <td>13.3</td>
      <td>2023</td>
      <td>18.9</td>
      <td>12.6</td>
      <td>2024</td>
    </tr>
    <tr>
      <th>Michigan</th>
      <td>10.2</td>
      <td>10.3</td>
      <td>2023</td>
      <td>11.9</td>
      <td>9.3</td>
      <td>2024</td>
    </tr>
    <tr>
      <th>Minnesota</th>
      <td>12.7</td>
      <td>12.4</td>
      <td>2023</td>
      <td>14.5</td>
      <td>11.4</td>
      <td>2024</td>
    </tr>
    <tr>
      <th>Mississippi</th>
      <td>1.6</td>
      <td>3.1</td>
      <td>2023</td>
      <td>2.9</td>
      <td>4.4</td>
      <td>2024</td>
    </tr>
    <tr>
      <th>Missouri</th>
      <td>7.6</td>
      <td>9.3</td>
      <td>2023</td>
      <td>11.7</td>
      <td>10.0</td>
      <td>2024</td>
    </tr>
    <tr>
      <th>Montana</th>
      <td>7.2</td>
      <td>8.8</td>
      <td>2023</td>
      <td>10.6</td>
      <td>10.0</td>
      <td>2024</td>
    </tr>
    <tr>
      <th>Nebraska</th>
      <td>8.5</td>
      <td>8.7</td>
      <td>2023</td>
      <td>9.6</td>
      <td>8.7</td>
      <td>2024</td>
    </tr>
    <tr>
      <th>Nevada</th>
      <td>5.1</td>
      <td>7.9</td>
      <td>2023</td>
      <td>6.5</td>
      <td>9.7</td>
      <td>2024</td>
    </tr>
    <tr>
      <th>New Hampshire</th>
      <td>10.4</td>
      <td>12.0</td>
      <td>2023</td>
      <td>12.8</td>
      <td>13.2</td>
      <td>2024</td>
    </tr>
    <tr>
      <th>New Jersey</th>
      <td>13.1</td>
      <td>11.2</td>
      <td>2023</td>
      <td>15.9</td>
      <td>11.2</td>
      <td>2024</td>
    </tr>
    <tr>
      <th>New Mexico</th>
      <td>5.8</td>
      <td>7.2</td>
      <td>2023</td>
      <td>8.5</td>
      <td>8.9</td>
      <td>2024</td>
    </tr>
    <tr>
      <th>New York</th>
      <td>10.7</td>
      <td>8.6</td>
      <td>2023</td>
      <td>12.8</td>
      <td>8.4</td>
      <td>2024</td>
    </tr>
    <tr>
      <th>North Carolina</th>
      <td>8.2</td>
      <td>10.4</td>
      <td>2023</td>
      <td>10.7</td>
      <td>11.3</td>
      <td>2024</td>
    </tr>
    <tr>
      <th>North Dakota</th>
      <td>5.3</td>
      <td>6.0</td>
      <td>2023</td>
      <td>7.9</td>
      <td>6.5</td>
      <td>2024</td>
    </tr>
    <tr>
      <th>Ohio</th>
      <td>9.4</td>
      <td>9.3</td>
      <td>2023</td>
      <td>11.4</td>
      <td>9.9</td>
      <td>2024</td>
    </tr>
    <tr>
      <th>Oklahoma</th>
      <td>5.7</td>
      <td>5.3</td>
      <td>2023</td>
      <td>7.6</td>
      <td>7.1</td>
      <td>2024</td>
    </tr>
    <tr>
      <th>Oregon</th>
      <td>12.1</td>
      <td>14.1</td>
      <td>2023</td>
      <td>14.1</td>
      <td>15.3</td>
      <td>2024</td>
    </tr>
    <tr>
      <th>Pennsylvania</th>
      <td>10.2</td>
      <td>11.0</td>
      <td>2023</td>
      <td>12.3</td>
      <td>11.5</td>
      <td>2024</td>
    </tr>
    <tr>
      <th>Rhode Island</th>
      <td>9.4</td>
      <td>9.9</td>
      <td>2023</td>
      <td>14.1</td>
      <td>9.2</td>
      <td>2024</td>
    </tr>
    <tr>
      <th>South Carolina</th>
      <td>5.8</td>
      <td>8.3</td>
      <td>2023</td>
      <td>8.7</td>
      <td>9.6</td>
      <td>2024</td>
    </tr>
    <tr>
      <th>South Dakota</th>
      <td>4.0</td>
      <td>5.5</td>
      <td>2023</td>
      <td>7.7</td>
      <td>6.8</td>
      <td>2024</td>
    </tr>
    <tr>
      <th>Tennessee</th>
      <td>6.8</td>
      <td>8.5</td>
      <td>2023</td>
      <td>9.0</td>
      <td>10.5</td>
      <td>2024</td>
    </tr>
    <tr>
      <th>Texas</th>
      <td>7.7</td>
      <td>10.7</td>
      <td>2023</td>
      <td>10.8</td>
      <td>11.7</td>
      <td>2024</td>
    </tr>
    <tr>
      <th>Utah</th>
      <td>9.8</td>
      <td>12.0</td>
      <td>2023</td>
      <td>13.2</td>
      <td>13.6</td>
      <td>2024</td>
    </tr>
    <tr>
      <th>Vermont</th>
      <td>10.8</td>
      <td>11.8</td>
      <td>2023</td>
      <td>14.0</td>
      <td>12.3</td>
      <td>2024</td>
    </tr>
    <tr>
      <th>Virginia</th>
      <td>13.3</td>
      <td>13.9</td>
      <td>2023</td>
      <td>15.1</td>
      <td>13.5</td>
      <td>2024</td>
    </tr>
    <tr>
      <th>Washington</th>
      <td>14.0</td>
      <td>14.5</td>
      <td>2023</td>
      <td>16.3</td>
      <td>14.5</td>
      <td>2024</td>
    </tr>
    <tr>
      <th>West Virginia</th>
      <td>4.2</td>
      <td>5.2</td>
      <td>2023</td>
      <td>5.9</td>
      <td>6.5</td>
      <td>2024</td>
    </tr>
    <tr>
      <th>Wisconsin</th>
      <td>8.0</td>
      <td>8.4</td>
      <td>2023</td>
      <td>11.8</td>
      <td>10.1</td>
      <td>2024</td>
    </tr>
    <tr>
      <th>Wyoming</th>
      <td>5.1</td>
      <td>5.1</td>
      <td>2023</td>
      <td>6.4</td>
      <td>7.1</td>
      <td>2024</td>
    </tr>
  </tbody>
</table>
</div>




```python
pd.merge(telework2023, telework2024, on = "State", suffixes = ("_23","_24")).drop(["Year_23", "Year_24"],axis=1)
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
      <th>Teleworked_Some_23</th>
      <th>Teleworked_All_23</th>
      <th>Teleworked_Some_24</th>
      <th>Teleworked_All_24</th>
    </tr>
    <tr>
      <th>State</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Alabama</th>
      <td>3.0</td>
      <td>4.6</td>
      <td>4.4</td>
      <td>6.3</td>
    </tr>
    <tr>
      <th>Alaska</th>
      <td>7.8</td>
      <td>6.1</td>
      <td>9.5</td>
      <td>7.2</td>
    </tr>
    <tr>
      <th>Arizona</th>
      <td>10.0</td>
      <td>13.9</td>
      <td>12.6</td>
      <td>14.9</td>
    </tr>
    <tr>
      <th>Arkansas</th>
      <td>3.9</td>
      <td>5.1</td>
      <td>6.0</td>
      <td>5.6</td>
    </tr>
    <tr>
      <th>California</th>
      <td>11.5</td>
      <td>11.1</td>
      <td>14.1</td>
      <td>11.4</td>
    </tr>
    <tr>
      <th>Colorado</th>
      <td>16.0</td>
      <td>15.8</td>
      <td>16.6</td>
      <td>15.7</td>
    </tr>
    <tr>
      <th>Connecticut</th>
      <td>14.4</td>
      <td>10.7</td>
      <td>16.2</td>
      <td>9.0</td>
    </tr>
    <tr>
      <th>Delaware</th>
      <td>10.5</td>
      <td>10.0</td>
      <td>11.6</td>
      <td>10.7</td>
    </tr>
    <tr>
      <th>District of Columbia</th>
      <td>33.1</td>
      <td>23.4</td>
      <td>36.0</td>
      <td>20.8</td>
    </tr>
    <tr>
      <th>Florida</th>
      <td>5.3</td>
      <td>10.0</td>
      <td>7.7</td>
      <td>11.3</td>
    </tr>
    <tr>
      <th>Georgia</th>
      <td>6.9</td>
      <td>10.9</td>
      <td>10.6</td>
      <td>11.6</td>
    </tr>
    <tr>
      <th>Hawaii</th>
      <td>6.5</td>
      <td>6.4</td>
      <td>8.9</td>
      <td>6.8</td>
    </tr>
    <tr>
      <th>Idaho</th>
      <td>7.2</td>
      <td>8.0</td>
      <td>9.1</td>
      <td>10.6</td>
    </tr>
    <tr>
      <th>Illinois</th>
      <td>11.2</td>
      <td>9.7</td>
      <td>14.5</td>
      <td>11.8</td>
    </tr>
    <tr>
      <th>Indiana</th>
      <td>7.4</td>
      <td>7.4</td>
      <td>10.3</td>
      <td>7.9</td>
    </tr>
    <tr>
      <th>Iowa</th>
      <td>5.6</td>
      <td>6.6</td>
      <td>8.9</td>
      <td>6.8</td>
    </tr>
    <tr>
      <th>Kansas</th>
      <td>8.0</td>
      <td>8.5</td>
      <td>11.3</td>
      <td>9.0</td>
    </tr>
    <tr>
      <th>Kentucky</th>
      <td>6.6</td>
      <td>6.6</td>
      <td>8.1</td>
      <td>7.5</td>
    </tr>
    <tr>
      <th>Louisiana</th>
      <td>4.0</td>
      <td>5.5</td>
      <td>6.5</td>
      <td>6.3</td>
    </tr>
    <tr>
      <th>Maine</th>
      <td>10.1</td>
      <td>11.6</td>
      <td>11.9</td>
      <td>11.6</td>
    </tr>
    <tr>
      <th>Maryland</th>
      <td>13.0</td>
      <td>14.6</td>
      <td>16.3</td>
      <td>14.1</td>
    </tr>
    <tr>
      <th>Massachusetts</th>
      <td>16.1</td>
      <td>13.3</td>
      <td>18.9</td>
      <td>12.6</td>
    </tr>
    <tr>
      <th>Michigan</th>
      <td>10.2</td>
      <td>10.3</td>
      <td>11.9</td>
      <td>9.3</td>
    </tr>
    <tr>
      <th>Minnesota</th>
      <td>12.7</td>
      <td>12.4</td>
      <td>14.5</td>
      <td>11.4</td>
    </tr>
    <tr>
      <th>Mississippi</th>
      <td>1.6</td>
      <td>3.1</td>
      <td>2.9</td>
      <td>4.4</td>
    </tr>
    <tr>
      <th>Missouri</th>
      <td>7.6</td>
      <td>9.3</td>
      <td>11.7</td>
      <td>10.0</td>
    </tr>
    <tr>
      <th>Montana</th>
      <td>7.2</td>
      <td>8.8</td>
      <td>10.6</td>
      <td>10.0</td>
    </tr>
    <tr>
      <th>Nebraska</th>
      <td>8.5</td>
      <td>8.7</td>
      <td>9.6</td>
      <td>8.7</td>
    </tr>
    <tr>
      <th>Nevada</th>
      <td>5.1</td>
      <td>7.9</td>
      <td>6.5</td>
      <td>9.7</td>
    </tr>
    <tr>
      <th>New Hampshire</th>
      <td>10.4</td>
      <td>12.0</td>
      <td>12.8</td>
      <td>13.2</td>
    </tr>
    <tr>
      <th>New Jersey</th>
      <td>13.1</td>
      <td>11.2</td>
      <td>15.9</td>
      <td>11.2</td>
    </tr>
    <tr>
      <th>New Mexico</th>
      <td>5.8</td>
      <td>7.2</td>
      <td>8.5</td>
      <td>8.9</td>
    </tr>
    <tr>
      <th>New York</th>
      <td>10.7</td>
      <td>8.6</td>
      <td>12.8</td>
      <td>8.4</td>
    </tr>
    <tr>
      <th>North Carolina</th>
      <td>8.2</td>
      <td>10.4</td>
      <td>10.7</td>
      <td>11.3</td>
    </tr>
    <tr>
      <th>North Dakota</th>
      <td>5.3</td>
      <td>6.0</td>
      <td>7.9</td>
      <td>6.5</td>
    </tr>
    <tr>
      <th>Ohio</th>
      <td>9.4</td>
      <td>9.3</td>
      <td>11.4</td>
      <td>9.9</td>
    </tr>
    <tr>
      <th>Oklahoma</th>
      <td>5.7</td>
      <td>5.3</td>
      <td>7.6</td>
      <td>7.1</td>
    </tr>
    <tr>
      <th>Oregon</th>
      <td>12.1</td>
      <td>14.1</td>
      <td>14.1</td>
      <td>15.3</td>
    </tr>
    <tr>
      <th>Pennsylvania</th>
      <td>10.2</td>
      <td>11.0</td>
      <td>12.3</td>
      <td>11.5</td>
    </tr>
    <tr>
      <th>Rhode Island</th>
      <td>9.4</td>
      <td>9.9</td>
      <td>14.1</td>
      <td>9.2</td>
    </tr>
    <tr>
      <th>South Carolina</th>
      <td>5.8</td>
      <td>8.3</td>
      <td>8.7</td>
      <td>9.6</td>
    </tr>
    <tr>
      <th>South Dakota</th>
      <td>4.0</td>
      <td>5.5</td>
      <td>7.7</td>
      <td>6.8</td>
    </tr>
    <tr>
      <th>Tennessee</th>
      <td>6.8</td>
      <td>8.5</td>
      <td>9.0</td>
      <td>10.5</td>
    </tr>
    <tr>
      <th>Texas</th>
      <td>7.7</td>
      <td>10.7</td>
      <td>10.8</td>
      <td>11.7</td>
    </tr>
    <tr>
      <th>Utah</th>
      <td>9.8</td>
      <td>12.0</td>
      <td>13.2</td>
      <td>13.6</td>
    </tr>
    <tr>
      <th>Vermont</th>
      <td>10.8</td>
      <td>11.8</td>
      <td>14.0</td>
      <td>12.3</td>
    </tr>
    <tr>
      <th>Virginia</th>
      <td>13.3</td>
      <td>13.9</td>
      <td>15.1</td>
      <td>13.5</td>
    </tr>
    <tr>
      <th>Washington</th>
      <td>14.0</td>
      <td>14.5</td>
      <td>16.3</td>
      <td>14.5</td>
    </tr>
    <tr>
      <th>West Virginia</th>
      <td>4.2</td>
      <td>5.2</td>
      <td>5.9</td>
      <td>6.5</td>
    </tr>
    <tr>
      <th>Wisconsin</th>
      <td>8.0</td>
      <td>8.4</td>
      <td>11.8</td>
      <td>10.1</td>
    </tr>
    <tr>
      <th>Wyoming</th>
      <td>5.1</td>
      <td>5.1</td>
      <td>6.4</td>
      <td>7.1</td>
    </tr>
  </tbody>
</table>
</div>


