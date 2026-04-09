---
layout: single
sitemap: false
permalink: /pages/Econ_390_SP26_L19/
title: Econ 390 Lecture 19
---

[Download Jupyter Notebook Empty](https://m-mcmain.github.io/files/Econ390SP26/Lectures/Lecture19_Merging_empty.ipynb)

[Download Jupyter Notebook Completed](https://m-mcmain.github.io/files/Econ390SP26/Lectures/Lecture19_Merging_full.ipynb)

# Econ 390 - Lecture 19: Merging
Today we will go over how to merge datasets. We will be covering much of [8.1 and 8.2 from McKinney](https://wesmckinney.com/book/data-wrangling) and [Joins in Turrell](https://aeturrell.github.io/coding-for-economists/data-joining-data.html#joins).


```python
import pandas as pd

econ390path = "https://m-mcmain.github.io/files/Econ390SP26/"
```

## Concatenate


```python
# Read in the data
telework2023 = pd.read_csv(econ390path + "state-telework-2023.csv", index_col =0)
telework2024 = pd.read_csv(econ390path + "state-telework-2024.csv", index_col =0)

telework2024.head()
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
      <th>All States</th>
      <td>11.9</td>
      <td>10.9</td>
      <td>2024</td>
    </tr>
    <tr>
      <th>Alabama</th>
      <td>4.4</td>
      <td>6.3</td>
      <td>2024</td>
    </tr>
    <tr>
      <th>Alaska</th>
      <td>9.5</td>
      <td>7.2</td>
      <td>2024</td>
    </tr>
    <tr>
      <th>Arizona</th>
      <td>12.6</td>
      <td>14.9</td>
      <td>2024</td>
    </tr>
    <tr>
      <th>Arkansas</th>
      <td>6.0</td>
      <td>5.6</td>
      <td>2024</td>
    </tr>
  </tbody>
</table>
</div>




```python
# concat method
pd.concat([telework2023, telework2024], axis=1)
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
telework2023 = pd.read_csv(econ390path + "state-telework-2023.csv", dtype = {"Year":"Int64"}, index_col =0)
telework2024 = pd.read_csv(econ390path + "state-telework-2024.csv", index_col =0)

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
pd.concat([telework2023, telework2024], axis=0)
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
pd.concat([telework2023, telework2024], axis=0, keys = Years)
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
telework_stacked = pd.concat([telework2023, telework2024], axis=0)
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
# Change the order?
telework_stacked.reset_index().set_index(["Year", "State"])
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
telework_stacked.set_index("Year", append=True, inplace=True)
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
telework_stacked.sort_values("Teleworked_All")
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
telework_stacked.sort_values("Teleworked_All", ascending=False)
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
telework_stacked.sort_index(level=["Year","State"], ascending=[True, False])
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
telework_stacked.sort_index(level=[0,1], ascending=[True, False])

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
# Finding specific entries for both index
telework_stacked.loc[("Wisconsin", 2024)]
```




    Teleworked_Some    11.8
    Teleworked_All     10.1
    Name: (Wisconsin, 2024), dtype: float64




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
# xs turns the dataframe into a cross section for the specified index
telework_stacked.xs("Wisconsin",level="State")
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
telework_stacked.xs("Wisconsin",level="State", drop_level = False)
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
telework_stacked.xs(("Wisconsin", "Michigan"), level="State", drop_level = False)
```


    ---------------------------------------------------------------------------

    KeyError                                  Traceback (most recent call last)

    File ~\anaconda3\Lib\site-packages\pandas\core\indexes\base.py:3805, in Index.get_loc(self, key)
       3804 try:
    -> 3805     return self._engine.get_loc(casted_key)
       3806 except KeyError as err:
    

    File index.pyx:167, in pandas._libs.index.IndexEngine.get_loc()
    

    File index.pyx:175, in pandas._libs.index.IndexEngine.get_loc()
    

    File pandas\\_libs\\index_class_helper.pxi:86, in pandas._libs.index.MaskedInt64Engine._check_type()
    

    KeyError: 'Michigan'

    
    The above exception was the direct cause of the following exception:
    

    KeyError                                  Traceback (most recent call last)

    File index.pyx:768, in pandas._libs.index.BaseMultiIndexCodesEngine.get_loc()
    

    File ~\anaconda3\Lib\site-packages\pandas\core\indexes\base.py:3812, in Index.get_loc(self, key)
       3811         raise InvalidIndexError(key)
    -> 3812     raise KeyError(key) from err
       3813 except TypeError:
       3814     # If we have a listlike key, _check_indexing_error will raise
       3815     #  InvalidIndexError. Otherwise we fall through and re-raise
       3816     #  the TypeError.
    

    KeyError: 'Michigan'

    
    During handling of the above exception, another exception occurred:
    

    KeyError                                  Traceback (most recent call last)

    File ~\anaconda3\Lib\site-packages\pandas\core\indexes\multi.py:3220, in MultiIndex._get_loc_level(self, key, level)
       3219 try:
    -> 3220     return (self._engine.get_loc(key), None)
       3221 except KeyError as err:
    

    File index.pyx:771, in pandas._libs.index.BaseMultiIndexCodesEngine.get_loc()
    

    KeyError: ('Wisconsin', 'Michigan')

    
    The above exception was the direct cause of the following exception:
    

    KeyError                                  Traceback (most recent call last)

    Cell In[60], line 2
          1 # Multiple states?
    ----> 2 telework_stacked.xs(("Wisconsin", "Michigan"), level="State", drop_level = False)
    

    File ~\anaconda3\Lib\site-packages\pandas\core\generic.py:4274, in NDFrame.xs(self, key, axis, level, drop_level)
       4272 if not isinstance(labels, MultiIndex):
       4273     raise TypeError("Index must be a MultiIndex")
    -> 4274 loc, new_ax = labels.get_loc_level(key, level=level, drop_level=drop_level)
       4276 # create the tuple of the indexer
       4277 _indexer = [slice(None)] * self.ndim
    

    File ~\anaconda3\Lib\site-packages\pandas\core\indexes\multi.py:3150, in MultiIndex.get_loc_level(self, key, level, drop_level)
       3147 else:
       3148     level = [self._get_level_number(lev) for lev in level]
    -> 3150 loc, mi = self._get_loc_level(key, level=level)
       3151 if not drop_level:
       3152     if lib.is_integer(loc):
       3153         # Slice index must be an integer or None
    

    File ~\anaconda3\Lib\site-packages\pandas\core\indexes\multi.py:3222, in MultiIndex._get_loc_level(self, key, level)
       3220     return (self._engine.get_loc(key), None)
       3221 except KeyError as err:
    -> 3222     raise KeyError(key) from err
       3223 except TypeError:
       3224     # e.g. partial string indexing
       3225     #  test_partial_string_timestamp_multiindex
       3226     pass
    

    KeyError: ('Wisconsin', 'Michigan')



```python
# Work around that with concat
telework_WI = telework_stacked.xs("Wisconsin",level="State",drop_level=False)
telework_MI = telework_stacked.xs("Michigan",level="State",drop_level=False)
pd.concat([telework_WI,telework_MI])
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
# loc still works
telework_stacked.loc[["Wisconsin","Michigan"]]
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
# Send it to a csv
telework_stacked.to_csv("telework_stacked.csv")
```


```python
# Read it in with multiple indices
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
# Results:
# 1.
print(telework_stacked.loc["District of Columbia"])
# 2.
print(telework_stacked.loc[("District of Columbia", 2023)])
# 3.
print(telework_stacked.loc[("District of Columbia", 2023)].iloc[1])
# 4.
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
# Merge Method
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
# Gotta specify "on"
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
# Suffixes and dropping
pd.merge(telework2023, telework2024, how = "outer", indicator = True,on = "State", suffixes=("_23","_24")).drop(["Year_23","Year_24"],axis=1)
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
      <th>_merge</th>
    </tr>
    <tr>
      <th>State</th>
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
      <td>4.4</td>
      <td>6.3</td>
      <td>both</td>
    </tr>
    <tr>
      <th>Alaska</th>
      <td>7.8</td>
      <td>6.1</td>
      <td>9.5</td>
      <td>7.2</td>
      <td>both</td>
    </tr>
    <tr>
      <th>All States</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>11.9</td>
      <td>10.9</td>
      <td>right_only</td>
    </tr>
    <tr>
      <th>Arizona</th>
      <td>10.0</td>
      <td>13.9</td>
      <td>12.6</td>
      <td>14.9</td>
      <td>both</td>
    </tr>
    <tr>
      <th>Arkansas</th>
      <td>3.9</td>
      <td>5.1</td>
      <td>6.0</td>
      <td>5.6</td>
      <td>both</td>
    </tr>
    <tr>
      <th>California</th>
      <td>11.5</td>
      <td>11.1</td>
      <td>14.1</td>
      <td>11.4</td>
      <td>both</td>
    </tr>
    <tr>
      <th>Colorado</th>
      <td>16.0</td>
      <td>15.8</td>
      <td>16.6</td>
      <td>15.7</td>
      <td>both</td>
    </tr>
    <tr>
      <th>Connecticut</th>
      <td>14.4</td>
      <td>10.7</td>
      <td>16.2</td>
      <td>9.0</td>
      <td>both</td>
    </tr>
    <tr>
      <th>Delaware</th>
      <td>10.5</td>
      <td>10.0</td>
      <td>11.6</td>
      <td>10.7</td>
      <td>both</td>
    </tr>
    <tr>
      <th>District of Columbia</th>
      <td>33.1</td>
      <td>23.4</td>
      <td>36.0</td>
      <td>20.8</td>
      <td>both</td>
    </tr>
    <tr>
      <th>Florida</th>
      <td>5.3</td>
      <td>10.0</td>
      <td>7.7</td>
      <td>11.3</td>
      <td>both</td>
    </tr>
    <tr>
      <th>Georgia</th>
      <td>6.9</td>
      <td>10.9</td>
      <td>10.6</td>
      <td>11.6</td>
      <td>both</td>
    </tr>
    <tr>
      <th>Hawaii</th>
      <td>6.5</td>
      <td>6.4</td>
      <td>8.9</td>
      <td>6.8</td>
      <td>both</td>
    </tr>
    <tr>
      <th>Idaho</th>
      <td>7.2</td>
      <td>8.0</td>
      <td>9.1</td>
      <td>10.6</td>
      <td>both</td>
    </tr>
    <tr>
      <th>Illinois</th>
      <td>11.2</td>
      <td>9.7</td>
      <td>14.5</td>
      <td>11.8</td>
      <td>both</td>
    </tr>
    <tr>
      <th>Indiana</th>
      <td>7.4</td>
      <td>7.4</td>
      <td>10.3</td>
      <td>7.9</td>
      <td>both</td>
    </tr>
    <tr>
      <th>Iowa</th>
      <td>5.6</td>
      <td>6.6</td>
      <td>8.9</td>
      <td>6.8</td>
      <td>both</td>
    </tr>
    <tr>
      <th>Kansas</th>
      <td>8.0</td>
      <td>8.5</td>
      <td>11.3</td>
      <td>9.0</td>
      <td>both</td>
    </tr>
    <tr>
      <th>Kentucky</th>
      <td>6.6</td>
      <td>6.6</td>
      <td>8.1</td>
      <td>7.5</td>
      <td>both</td>
    </tr>
    <tr>
      <th>Louisiana</th>
      <td>4.0</td>
      <td>5.5</td>
      <td>6.5</td>
      <td>6.3</td>
      <td>both</td>
    </tr>
    <tr>
      <th>Maine</th>
      <td>10.1</td>
      <td>11.6</td>
      <td>11.9</td>
      <td>11.6</td>
      <td>both</td>
    </tr>
    <tr>
      <th>Maryland</th>
      <td>13.0</td>
      <td>14.6</td>
      <td>16.3</td>
      <td>14.1</td>
      <td>both</td>
    </tr>
    <tr>
      <th>Massachusetts</th>
      <td>16.1</td>
      <td>13.3</td>
      <td>18.9</td>
      <td>12.6</td>
      <td>both</td>
    </tr>
    <tr>
      <th>Michigan</th>
      <td>10.2</td>
      <td>10.3</td>
      <td>11.9</td>
      <td>9.3</td>
      <td>both</td>
    </tr>
    <tr>
      <th>Minnesota</th>
      <td>12.7</td>
      <td>12.4</td>
      <td>14.5</td>
      <td>11.4</td>
      <td>both</td>
    </tr>
    <tr>
      <th>Mississippi</th>
      <td>1.6</td>
      <td>3.1</td>
      <td>2.9</td>
      <td>4.4</td>
      <td>both</td>
    </tr>
    <tr>
      <th>Missouri</th>
      <td>7.6</td>
      <td>9.3</td>
      <td>11.7</td>
      <td>10.0</td>
      <td>both</td>
    </tr>
    <tr>
      <th>Montana</th>
      <td>7.2</td>
      <td>8.8</td>
      <td>10.6</td>
      <td>10.0</td>
      <td>both</td>
    </tr>
    <tr>
      <th>Nebraska</th>
      <td>8.5</td>
      <td>8.7</td>
      <td>9.6</td>
      <td>8.7</td>
      <td>both</td>
    </tr>
    <tr>
      <th>Nevada</th>
      <td>5.1</td>
      <td>7.9</td>
      <td>6.5</td>
      <td>9.7</td>
      <td>both</td>
    </tr>
    <tr>
      <th>New Hampshire</th>
      <td>10.4</td>
      <td>12.0</td>
      <td>12.8</td>
      <td>13.2</td>
      <td>both</td>
    </tr>
    <tr>
      <th>New Jersey</th>
      <td>13.1</td>
      <td>11.2</td>
      <td>15.9</td>
      <td>11.2</td>
      <td>both</td>
    </tr>
    <tr>
      <th>New Mexico</th>
      <td>5.8</td>
      <td>7.2</td>
      <td>8.5</td>
      <td>8.9</td>
      <td>both</td>
    </tr>
    <tr>
      <th>New York</th>
      <td>10.7</td>
      <td>8.6</td>
      <td>12.8</td>
      <td>8.4</td>
      <td>both</td>
    </tr>
    <tr>
      <th>North Carolina</th>
      <td>8.2</td>
      <td>10.4</td>
      <td>10.7</td>
      <td>11.3</td>
      <td>both</td>
    </tr>
    <tr>
      <th>North Dakota</th>
      <td>5.3</td>
      <td>6.0</td>
      <td>7.9</td>
      <td>6.5</td>
      <td>both</td>
    </tr>
    <tr>
      <th>Ohio</th>
      <td>9.4</td>
      <td>9.3</td>
      <td>11.4</td>
      <td>9.9</td>
      <td>both</td>
    </tr>
    <tr>
      <th>Oklahoma</th>
      <td>5.7</td>
      <td>5.3</td>
      <td>7.6</td>
      <td>7.1</td>
      <td>both</td>
    </tr>
    <tr>
      <th>Oregon</th>
      <td>12.1</td>
      <td>14.1</td>
      <td>14.1</td>
      <td>15.3</td>
      <td>both</td>
    </tr>
    <tr>
      <th>Pennsylvania</th>
      <td>10.2</td>
      <td>11.0</td>
      <td>12.3</td>
      <td>11.5</td>
      <td>both</td>
    </tr>
    <tr>
      <th>Rhode Island</th>
      <td>9.4</td>
      <td>9.9</td>
      <td>14.1</td>
      <td>9.2</td>
      <td>both</td>
    </tr>
    <tr>
      <th>South Carolina</th>
      <td>5.8</td>
      <td>8.3</td>
      <td>8.7</td>
      <td>9.6</td>
      <td>both</td>
    </tr>
    <tr>
      <th>South Dakota</th>
      <td>4.0</td>
      <td>5.5</td>
      <td>7.7</td>
      <td>6.8</td>
      <td>both</td>
    </tr>
    <tr>
      <th>Tennessee</th>
      <td>6.8</td>
      <td>8.5</td>
      <td>9.0</td>
      <td>10.5</td>
      <td>both</td>
    </tr>
    <tr>
      <th>Texas</th>
      <td>7.7</td>
      <td>10.7</td>
      <td>10.8</td>
      <td>11.7</td>
      <td>both</td>
    </tr>
    <tr>
      <th>Utah</th>
      <td>9.8</td>
      <td>12.0</td>
      <td>13.2</td>
      <td>13.6</td>
      <td>both</td>
    </tr>
    <tr>
      <th>Vermont</th>
      <td>10.8</td>
      <td>11.8</td>
      <td>14.0</td>
      <td>12.3</td>
      <td>both</td>
    </tr>
    <tr>
      <th>Virginia</th>
      <td>13.3</td>
      <td>13.9</td>
      <td>15.1</td>
      <td>13.5</td>
      <td>both</td>
    </tr>
    <tr>
      <th>Washington</th>
      <td>14.0</td>
      <td>14.5</td>
      <td>16.3</td>
      <td>14.5</td>
      <td>both</td>
    </tr>
    <tr>
      <th>West Virginia</th>
      <td>4.2</td>
      <td>5.2</td>
      <td>5.9</td>
      <td>6.5</td>
      <td>both</td>
    </tr>
    <tr>
      <th>Wisconsin</th>
      <td>8.0</td>
      <td>8.4</td>
      <td>11.8</td>
      <td>10.1</td>
      <td>both</td>
    </tr>
    <tr>
      <th>Wyoming</th>
      <td>5.1</td>
      <td>5.1</td>
      <td>6.4</td>
      <td>7.1</td>
      <td>both</td>
    </tr>
  </tbody>
</table>
</div>


