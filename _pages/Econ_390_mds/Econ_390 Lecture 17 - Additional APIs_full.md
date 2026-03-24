---
layout: single
sitemap: false
permalink: /pages/Econ_390_SP26_L17/
title: Econ 390 Lecture 17
---

[Download Jupyter Notebook Empty](https://m-mcmain.github.io/files/Econ390SP26/Lectures/Lecture17_AdditionalAPIs_empty.ipynb)

[Download Jupyter Notebook Completed](https://m-mcmain.github.io/files/Econ390SP26/Lectures/Lecture17_AdditionalAPIs_full.ipynb)

# Econ 390 - Lecture 17: APIs using Requests Package
Today we will be looking at a more "manual" method of using APIs in Python using the `requests` package. This package is mentioned in [6.3 of McKinney](https://wesmckinney.com/book/accessing-data#io_web_apis) and in [Turrell](https://aeturrell.github.io/coding-for-economists/data-extraction.html#obtaining-data-using-apis).


```python
import requests
import pandas as pd
import matplotlib.pyplot as plt
from io import StringIO
import io
```

## OECD API

The [OECD website](https://www.oecd.org/en/data/insights/data-explainers/2024/09/api.html) goes through their API! You'll also find a link to a PDF with more details on how to use the API.


```python
# Define API query URL (CSV with labels format)
url = "https://sdmx.oecd.org/public/rest/data/OECD.GOV.GIP,DSD_GOV_INT@DF_GOV_TDG_2025,1.1/A..TRUST_NG....HMH.?startPeriod=2021&endPeriod=2021&dimensionAtObservation=AllDimensions&format=csvfilewithlabels"
# Fetch data
response = requests.get(url)

# Load into pandas DataFrame
df = pd.read_csv(StringIO(response.text))

# Display first few rows
print(df.head())
```

      STRUCTURE                                   STRUCTURE_ID  \
    0  DATAFLOW  OECD.GOV.GIP:DSD_GOV_INT@DF_GOV_TDG_2025(1.1)   
    1  DATAFLOW  OECD.GOV.GIP:DSD_GOV_INT@DF_GOV_TDG_2025(1.1)   
    2  DATAFLOW  OECD.GOV.GIP:DSD_GOV_INT@DF_GOV_TDG_2025(1.1)   
    3  DATAFLOW  OECD.GOV.GIP:DSD_GOV_INT@DF_GOV_TDG_2025(1.1)   
    4  DATAFLOW  OECD.GOV.GIP:DSD_GOV_INT@DF_GOV_TDG_2025(1.1)   
    
                                          STRUCTURE_NAME ACTION FREQ  \
    0  Trust, security and dignity - government at a ...      I    A   
    1  Trust, security and dignity - government at a ...      I    A   
    2  Trust, security and dignity - government at a ...      I    A   
    3  Trust, security and dignity - government at a ...      I    A   
    4  Trust, security and dignity - government at a ...      I    A   
    
      Frequency of observation REF_AREA Reference area   MEASURE  \
    0                   Annual      ISL        Iceland  TRUST_NG   
    1                   Annual      KOR          Korea  TRUST_NG   
    2                   Annual      COL       Colombia  TRUST_NG   
    3                   Annual      DNK        Denmark  TRUST_NG   
    4                   Annual      EST        Estonia  TRUST_NG   
    
                            Measure  ... OBS_VALUE Observation value OBS_STATUS  \
    0  Trust in national government  ...      50.4               NaN          A   
    1  Trust in national government  ...      48.8               NaN          A   
    2  Trust in national government  ...      20.5               NaN          A   
    3  Trust in national government  ...      48.8               NaN          A   
    4  Trust in national government  ...      46.5               NaN          A   
    
      Observation status  UNIT_MULT  Unit multiplier PRICE_BASE      Price base  \
    0       Normal value          0            Units         _Z  Not applicable   
    1       Normal value          0            Units         _Z  Not applicable   
    2       Normal value          0            Units         _Z  Not applicable   
    3       Normal value          0            Units         _Z  Not applicable   
    4       Normal value          0            Units         _Z  Not applicable   
    
      BASE_PER Base period  
    0      NaN         NaN  
    1      NaN         NaN  
    2      NaN         NaN  
    3      NaN         NaN  
    4      NaN         NaN  
    
    [5 rows x 32 columns]
    


```python
# Type?
type(response)
```




    requests.models.Response




```python
# Status Code
response.status_code
```




    200




```python
# What does it look like?
print(type(response.text))
response.text
```

    <class 'str'>
    




    'STRUCTURE,STRUCTURE_ID,STRUCTURE_NAME,ACTION,FREQ,Frequency of observation,REF_AREA,Reference area,MEASURE,Measure,UNIT_MEASURE,Unit of measure,SECTOR,Institutional sector,EDITION,Edition,SCALE,Scale,CATEGORY,Category,TIME_PERIOD,Time period,OBS_VALUE,Observation value,OBS_STATUS,Observation status,UNIT_MULT,Unit multiplier,PRICE_BASE,Price base,BASE_PER,Base period\r\nDATAFLOW,OECD.GOV.GIP:DSD_GOV_INT@DF_GOV_TDG_2025(1.1),"Trust, security and dignity - government at a glance indicators, 2025 edition",I,A,Annual,ISL,Iceland,TRUST_NG,Trust in national government,PT_RESP,Percentage of respondents,_Z,Not applicable,2025,2025,HMH,High and moderately high,TDG,"Trust, security and dignity",2021,,50.4,,A,Normal value,0,Units,_Z,Not applicable,,\r\nDATAFLOW,OECD.GOV.GIP:DSD_GOV_INT@DF_GOV_TDG_2025(1.1),"Trust, security and dignity - government at a glance indicators, 2025 edition",I,A,Annual,KOR,Korea,TRUST_NG,Trust in national government,PT_RESP,Percentage of respondents,_Z,Not applicable,2025,2025,HMH,High and moderately high,TDG,"Trust, security and dignity",2021,,48.8,,A,Normal value,0,Units,_Z,Not applicable,,\r\nDATAFLOW,OECD.GOV.GIP:DSD_GOV_INT@DF_GOV_TDG_2025(1.1),"Trust, security and dignity - government at a glance indicators, 2025 edition",I,A,Annual,COL,Colombia,TRUST_NG,Trust in national government,PT_RESP,Percentage of respondents,_Z,Not applicable,2025,2025,HMH,High and moderately high,TDG,"Trust, security and dignity",2021,,20.5,,A,Normal value,0,Units,_Z,Not applicable,,\r\nDATAFLOW,OECD.GOV.GIP:DSD_GOV_INT@DF_GOV_TDG_2025(1.1),"Trust, security and dignity - government at a glance indicators, 2025 edition",I,A,Annual,DNK,Denmark,TRUST_NG,Trust in national government,PT_RESP,Percentage of respondents,_Z,Not applicable,2025,2025,HMH,High and moderately high,TDG,"Trust, security and dignity",2021,,48.8,,A,Normal value,0,Units,_Z,Not applicable,,\r\nDATAFLOW,OECD.GOV.GIP:DSD_GOV_INT@DF_GOV_TDG_2025(1.1),"Trust, security and dignity - government at a glance indicators, 2025 edition",I,A,Annual,EST,Estonia,TRUST_NG,Trust in national government,PT_RESP,Percentage of respondents,_Z,Not applicable,2025,2025,HMH,High and moderately high,TDG,"Trust, security and dignity",2021,,46.5,,A,Normal value,0,Units,_Z,Not applicable,,\r\nDATAFLOW,OECD.GOV.GIP:DSD_GOV_INT@DF_GOV_TDG_2025(1.1),"Trust, security and dignity - government at a glance indicators, 2025 edition",I,A,Annual,JPN,Japan,TRUST_NG,Trust in national government,PT_RESP,Percentage of respondents,_Z,Not applicable,2025,2025,HMH,High and moderately high,TDG,"Trust, security and dignity",2021,,24,,A,Normal value,0,Units,_Z,Not applicable,,\r\nDATAFLOW,OECD.GOV.GIP:DSD_GOV_INT@DF_GOV_TDG_2025(1.1),"Trust, security and dignity - government at a glance indicators, 2025 edition",I,A,Annual,FIN,Finland,TRUST_NG,Trust in national government,PT_RESP,Percentage of respondents,_Z,Not applicable,2025,2025,HMH,High and moderately high,TDG,"Trust, security and dignity",2021,,61.5,,A,Normal value,0,Units,_Z,Not applicable,,\r\nDATAFLOW,OECD.GOV.GIP:DSD_GOV_INT@DF_GOV_TDG_2025(1.1),"Trust, security and dignity - government at a glance indicators, 2025 edition",I,A,Annual,LVA,Latvia,TRUST_NG,Trust in national government,PT_RESP,Percentage of respondents,_Z,Not applicable,2025,2025,HMH,High and moderately high,TDG,"Trust, security and dignity",2021,,24.5,,A,Normal value,0,Units,_Z,Not applicable,,\r\nDATAFLOW,OECD.GOV.GIP:DSD_GOV_INT@DF_GOV_TDG_2025(1.1),"Trust, security and dignity - government at a glance indicators, 2025 edition",I,A,Annual,LUX,Luxembourg,TRUST_NG,Trust in national government,PT_RESP,Percentage of respondents,_Z,Not applicable,2025,2025,HMH,High and moderately high,TDG,"Trust, security and dignity",2021,,55.9,,A,Normal value,0,Units,_Z,Not applicable,,\r\nDATAFLOW,OECD.GOV.GIP:DSD_GOV_INT@DF_GOV_TDG_2025(1.1),"Trust, security and dignity - government at a glance indicators, 2025 edition",I,A,Annual,NLD,Netherlands,TRUST_NG,Trust in national government,PT_RESP,Percentage of respondents,_Z,Not applicable,2025,2025,HMH,High and moderately high,TDG,"Trust, security and dignity",2021,,49.1,,A,Normal value,0,Units,_Z,Not applicable,,\r\nDATAFLOW,OECD.GOV.GIP:DSD_GOV_INT@DF_GOV_TDG_2025(1.1),"Trust, security and dignity - government at a glance indicators, 2025 edition",I,A,Annual,NOR,Norway,TRUST_NG,Trust in national government,PT_RESP,Percentage of respondents,_Z,Not applicable,2025,2025,HMH,High and moderately high,TDG,"Trust, security and dignity",2021,,63.8,,A,Normal value,0,Units,_Z,Not applicable,,\r\nDATAFLOW,OECD.GOV.GIP:DSD_GOV_INT@DF_GOV_TDG_2025(1.1),"Trust, security and dignity - government at a glance indicators, 2025 edition",I,A,Annual,PRT,Portugal,TRUST_NG,Trust in national government,PT_RESP,Percentage of respondents,_Z,Not applicable,2025,2025,HMH,High and moderately high,TDG,"Trust, security and dignity",2021,,40.7,,A,Normal value,0,Units,_Z,Not applicable,,\r\nDATAFLOW,OECD.GOV.GIP:DSD_GOV_INT@DF_GOV_TDG_2025(1.1),"Trust, security and dignity - government at a glance indicators, 2025 edition",I,A,Annual,SWE,Sweden,TRUST_NG,Trust in national government,PT_RESP,Percentage of respondents,_Z,Not applicable,2025,2025,HMH,High and moderately high,TDG,"Trust, security and dignity",2021,,39,,A,Normal value,0,Units,_Z,Not applicable,,\r\nDATAFLOW,OECD.GOV.GIP:DSD_GOV_INT@DF_GOV_TDG_2025(1.1),"Trust, security and dignity - government at a glance indicators, 2025 edition",I,A,Annual,GBR,United Kingdom,TRUST_NG,Trust in national government,PT_RESP,Percentage of respondents,_Z,Not applicable,2025,2025,HMH,High and moderately high,TDG,"Trust, security and dignity",2021,,34.8,,A,Normal value,0,Units,_Z,Not applicable,,\r\nDATAFLOW,OECD.GOV.GIP:DSD_GOV_INT@DF_GOV_TDG_2025(1.1),"Trust, security and dignity - government at a glance indicators, 2025 edition",I,A,Annual,OECD_REP,OECD average country,TRUST_NG,Trust in national government,PT_RESP,Percentage of respondents,_Z,Not applicable,2025,2025,HMH,High and moderately high,TDG,"Trust, security and dignity",2021,,41.4,,A,Normal value,0,Units,_Z,Not applicable,,\r\nDATAFLOW,OECD.GOV.GIP:DSD_GOV_INT@DF_GOV_TDG_2025(1.1),"Trust, security and dignity - government at a glance indicators, 2025 edition",I,A,Annual,AUS,Australia,TRUST_NG,Trust in national government,PT_RESP,Percentage of respondents,_Z,Not applicable,2025,2025,HMH,High and moderately high,TDG,"Trust, security and dignity",2021,,38,,A,Normal value,0,Units,_Z,Not applicable,,\r\nDATAFLOW,OECD.GOV.GIP:DSD_GOV_INT@DF_GOV_TDG_2025(1.1),"Trust, security and dignity - government at a glance indicators, 2025 edition",I,A,Annual,AUT,Austria,TRUST_NG,Trust in national government,PT_RESP,Percentage of respondents,_Z,Not applicable,2025,2025,HMH,High and moderately high,TDG,"Trust, security and dignity",2021,,25.8,,A,Normal value,0,Units,_Z,Not applicable,,\r\nDATAFLOW,OECD.GOV.GIP:DSD_GOV_INT@DF_GOV_TDG_2025(1.1),"Trust, security and dignity - government at a glance indicators, 2025 edition",I,A,Annual,BEL,Belgium,TRUST_NG,Trust in national government,PT_RESP,Percentage of respondents,_Z,Not applicable,2025,2025,HMH,High and moderately high,TDG,"Trust, security and dignity",2021,,31.8,,A,Normal value,0,Units,_Z,Not applicable,,\r\nDATAFLOW,OECD.GOV.GIP:DSD_GOV_INT@DF_GOV_TDG_2025(1.1),"Trust, security and dignity - government at a glance indicators, 2025 edition",I,A,Annual,CAN,Canada,TRUST_NG,Trust in national government,PT_RESP,Percentage of respondents,_Z,Not applicable,2025,2025,HMH,High and moderately high,TDG,"Trust, security and dignity",2021,,44.7,,A,Normal value,0,Units,_Z,Not applicable,,\r\nDATAFLOW,OECD.GOV.GIP:DSD_GOV_INT@DF_GOV_TDG_2025(1.1),"Trust, security and dignity - government at a glance indicators, 2025 edition",I,A,Annual,IRL,Ireland,TRUST_NG,Trust in national government,PT_RESP,Percentage of respondents,_Z,Not applicable,2025,2025,HMH,High and moderately high,TDG,"Trust, security and dignity",2021,,50.6,,A,Normal value,0,Units,_Z,Not applicable,,\r\nDATAFLOW,OECD.GOV.GIP:DSD_GOV_INT@DF_GOV_TDG_2025(1.1),"Trust, security and dignity - government at a glance indicators, 2025 edition",I,A,Annual,FRA,France,TRUST_NG,Trust in national government,PT_RESP,Percentage of respondents,_Z,Not applicable,2025,2025,HMH,High and moderately high,TDG,"Trust, security and dignity",2021,,28.1,,A,Normal value,0,Units,_Z,Not applicable,,\r\n'




```python
# Look through the DF
df.head()
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
      <th>STRUCTURE</th>
      <th>STRUCTURE_ID</th>
      <th>STRUCTURE_NAME</th>
      <th>ACTION</th>
      <th>FREQ</th>
      <th>Frequency of observation</th>
      <th>REF_AREA</th>
      <th>Reference area</th>
      <th>MEASURE</th>
      <th>Measure</th>
      <th>...</th>
      <th>OBS_VALUE</th>
      <th>Observation value</th>
      <th>OBS_STATUS</th>
      <th>Observation status</th>
      <th>UNIT_MULT</th>
      <th>Unit multiplier</th>
      <th>PRICE_BASE</th>
      <th>Price base</th>
      <th>BASE_PER</th>
      <th>Base period</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>DATAFLOW</td>
      <td>OECD.GOV.GIP:DSD_GOV_INT@DF_GOV_TDG_2025(1.1)</td>
      <td>Trust, security and dignity - government at a ...</td>
      <td>I</td>
      <td>A</td>
      <td>Annual</td>
      <td>ISL</td>
      <td>Iceland</td>
      <td>TRUST_NG</td>
      <td>Trust in national government</td>
      <td>...</td>
      <td>50.4</td>
      <td>NaN</td>
      <td>A</td>
      <td>Normal value</td>
      <td>0</td>
      <td>Units</td>
      <td>_Z</td>
      <td>Not applicable</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1</th>
      <td>DATAFLOW</td>
      <td>OECD.GOV.GIP:DSD_GOV_INT@DF_GOV_TDG_2025(1.1)</td>
      <td>Trust, security and dignity - government at a ...</td>
      <td>I</td>
      <td>A</td>
      <td>Annual</td>
      <td>KOR</td>
      <td>Korea</td>
      <td>TRUST_NG</td>
      <td>Trust in national government</td>
      <td>...</td>
      <td>48.8</td>
      <td>NaN</td>
      <td>A</td>
      <td>Normal value</td>
      <td>0</td>
      <td>Units</td>
      <td>_Z</td>
      <td>Not applicable</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2</th>
      <td>DATAFLOW</td>
      <td>OECD.GOV.GIP:DSD_GOV_INT@DF_GOV_TDG_2025(1.1)</td>
      <td>Trust, security and dignity - government at a ...</td>
      <td>I</td>
      <td>A</td>
      <td>Annual</td>
      <td>COL</td>
      <td>Colombia</td>
      <td>TRUST_NG</td>
      <td>Trust in national government</td>
      <td>...</td>
      <td>20.5</td>
      <td>NaN</td>
      <td>A</td>
      <td>Normal value</td>
      <td>0</td>
      <td>Units</td>
      <td>_Z</td>
      <td>Not applicable</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>3</th>
      <td>DATAFLOW</td>
      <td>OECD.GOV.GIP:DSD_GOV_INT@DF_GOV_TDG_2025(1.1)</td>
      <td>Trust, security and dignity - government at a ...</td>
      <td>I</td>
      <td>A</td>
      <td>Annual</td>
      <td>DNK</td>
      <td>Denmark</td>
      <td>TRUST_NG</td>
      <td>Trust in national government</td>
      <td>...</td>
      <td>48.8</td>
      <td>NaN</td>
      <td>A</td>
      <td>Normal value</td>
      <td>0</td>
      <td>Units</td>
      <td>_Z</td>
      <td>Not applicable</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>4</th>
      <td>DATAFLOW</td>
      <td>OECD.GOV.GIP:DSD_GOV_INT@DF_GOV_TDG_2025(1.1)</td>
      <td>Trust, security and dignity - government at a ...</td>
      <td>I</td>
      <td>A</td>
      <td>Annual</td>
      <td>EST</td>
      <td>Estonia</td>
      <td>TRUST_NG</td>
      <td>Trust in national government</td>
      <td>...</td>
      <td>46.5</td>
      <td>NaN</td>
      <td>A</td>
      <td>Normal value</td>
      <td>0</td>
      <td>Units</td>
      <td>_Z</td>
      <td>Not applicable</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
<p>5 rows × 32 columns</p>
</div>




```python
# Subset just what we need
df = df[["OBS_VALUE","REF_AREA"]]
df.index = df["REF_AREA"]
df = df.drop(index="OECD_REP")
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
      <th>OBS_VALUE</th>
      <th>REF_AREA</th>
    </tr>
    <tr>
      <th>REF_AREA</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>ISL</th>
      <td>50.4</td>
      <td>ISL</td>
    </tr>
    <tr>
      <th>KOR</th>
      <td>48.8</td>
      <td>KOR</td>
    </tr>
    <tr>
      <th>COL</th>
      <td>20.5</td>
      <td>COL</td>
    </tr>
    <tr>
      <th>DNK</th>
      <td>48.8</td>
      <td>DNK</td>
    </tr>
    <tr>
      <th>EST</th>
      <td>46.5</td>
      <td>EST</td>
    </tr>
    <tr>
      <th>JPN</th>
      <td>24.0</td>
      <td>JPN</td>
    </tr>
    <tr>
      <th>FIN</th>
      <td>61.5</td>
      <td>FIN</td>
    </tr>
    <tr>
      <th>LVA</th>
      <td>24.5</td>
      <td>LVA</td>
    </tr>
    <tr>
      <th>LUX</th>
      <td>55.9</td>
      <td>LUX</td>
    </tr>
    <tr>
      <th>NLD</th>
      <td>49.1</td>
      <td>NLD</td>
    </tr>
    <tr>
      <th>NOR</th>
      <td>63.8</td>
      <td>NOR</td>
    </tr>
    <tr>
      <th>PRT</th>
      <td>40.7</td>
      <td>PRT</td>
    </tr>
    <tr>
      <th>SWE</th>
      <td>39.0</td>
      <td>SWE</td>
    </tr>
    <tr>
      <th>GBR</th>
      <td>34.8</td>
      <td>GBR</td>
    </tr>
    <tr>
      <th>AUS</th>
      <td>38.0</td>
      <td>AUS</td>
    </tr>
    <tr>
      <th>AUT</th>
      <td>25.8</td>
      <td>AUT</td>
    </tr>
    <tr>
      <th>BEL</th>
      <td>31.8</td>
      <td>BEL</td>
    </tr>
    <tr>
      <th>CAN</th>
      <td>44.7</td>
      <td>CAN</td>
    </tr>
    <tr>
      <th>IRL</th>
      <td>50.6</td>
      <td>IRL</td>
    </tr>
    <tr>
      <th>FRA</th>
      <td>28.1</td>
      <td>FRA</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Create Histogram
avg_trust = df["OBS_VALUE"].mean()
fig, ax = plt.subplots()
ax.hist(df["OBS_VALUE"])
ax.set(xlabel="% High and Moderately High",
       title="Distribution of Trust in National Government OECD")
ax.axvline(x=avg_trust,color="red")
plt.show()
```


    
![png](output_10_0.png)
    


## Practice: OECD API
1. Use the [OECD Data Explorer](https://data-explorer.oecd.org/) to find a dataset you'd be interested in downloading.
2. Get the API URL.
3. Display the first five rows. Does this immediately work if you just copy the URL from the API? *Hint: Make sure that you specify the format*


```python
url_practice = "https://sdmx.oecd.org/public/rest/data/OECD.EDU.IMEP,DSD_EAG_LSO_EA@DF_LSO_NEAC_DISTR_EA,1.0/AUS+AUT+BEL+CAN+CHL+COL+CRI+CZE+DNK+EST+FIN+FRA+DEU+GRC+HUN+ISL+IRL+ISR+ITA+JPN+KOR+LVA+LTU+LUX+MEX+NLD+NZL+NOR+POL+PRT+SVK+SVN+ESP+SWE+CHE+TUR+GBR+USA+OECD+ARG+BRA+BGR+HRV+IND+IDN+PER+ROU+ZAF._T.Y25T64.ISCED11A_0T2+ISCED11A_3_4+ISCED11A_5T8..........OBS...A?startPeriod=2020&endPeriod=2024&lastNObservations=1&dimensionAtObservation=AllDimensions&format=csvfilewithlabels"
response_practice = requests.get(url_practice)
# Load into pandas DataFrame
df_practice = pd.read_csv(StringIO(response_practice.text))
# Display first few rows
print(df_practice.head())
```

      STRUCTURE                                       STRUCTURE_ID  \
    0  DATAFLOW  OECD.EDU.IMEP:DSD_EAG_LSO_EA@DF_LSO_NEAC_DISTR...   
    1  DATAFLOW  OECD.EDU.IMEP:DSD_EAG_LSO_EA@DF_LSO_NEAC_DISTR...   
    2  DATAFLOW  OECD.EDU.IMEP:DSD_EAG_LSO_EA@DF_LSO_NEAC_DISTR...   
    3  DATAFLOW  OECD.EDU.IMEP:DSD_EAG_LSO_EA@DF_LSO_NEAC_DISTR...   
    4  DATAFLOW  OECD.EDU.IMEP:DSD_EAG_LSO_EA@DF_LSO_NEAC_DISTR...   
    
                                          STRUCTURE_NAME ACTION REF_AREA  \
    0  Adults' educational attainment distribution, b...      I      PER   
    1  Adults' educational attainment distribution, b...      I      LUX   
    2  Adults' educational attainment distribution, b...      I      SVN   
    3  Adults' educational attainment distribution, b...      I      TUR   
    4  Adults' educational attainment distribution, b...      I      LVA   
    
      Reference area SEX    Sex     AGE                  Age  ...  OBS_VALUE  \
    0           Peru  _T  Total  Y25T64  From 25 to 64 years  ...  39.276722   
    1     Luxembourg  _T  Total  Y25T64  From 25 to 64 years  ...  28.003969   
    2       Slovenia  _T  Total  Y25T64  From 25 to 64 years  ...  54.374645   
    3        Türkiye  _T  Total  Y25T64  From 25 to 64 years  ...  49.924622   
    4         Latvia  _T  Total  Y25T64  From 25 to 64 years  ...  40.456608   
    
      Observation value OBS_STATUS Observation status CONF_STATUS  \
    0               NaN          A       Normal value         NaN   
    1               NaN          A       Normal value         NaN   
    2               NaN          A       Normal value         NaN   
    3               NaN          A       Normal value         NaN   
    4               NaN          A       Normal value         NaN   
    
      Confidentiality status UNIT_MULT Unit multiplier DECIMALS Decimals  
    0                    NaN         0           Units        1      One  
    1                    NaN         0           Units        1      One  
    2                    NaN         0           Units        1      One  
    3                    NaN         0           Units        1      One  
    4                    NaN         0           Units        1      One  
    
    [5 rows x 50 columns]
    

## Census API
We'll be focusing on the [International Trade API](https://www.census.gov/data/developers/data-sets/international-trade.html) which has a pdf guide [here](https://www.census.gov/foreign-trade/reference/guides/Guide_to_International_Trade_Datasets.pdf).


```python
# Base URL
base_url = "https://api.census.gov/data/timeseries/intltrade/exports/hs"
```


```python
# Systematic components
variables = "ALL_VAL_MO" # get the variables of interes: total value
level = "HS10"           # 10-digit HS level
commodity = "2710121510" # Gasoline
country = "1220"         # Canada
dates = "from+2016-01"   # Data from 2016 through now
```


```python
# Formulate full URL
full_url = (base_url
            + "?get=" + variables
            + "&COMM_LVL=" + level
            + "&E_COMMODITY=" + commodity
            + "&CTY_CODE=" + country
            + "&time=" + dates)
```


```python
# Submit Query
response = requests.get(full_url)
response
full_url
```




    'https://api.census.gov/data/timeseries/intltrade/exports/hs?get=ALL_VAL_MO&COMM_LVL=HS10&E_COMMODITY=2710121510&CTY_CODE=1220&time=from+2016-01'




```python
# Content of the request
response.content
```




    b'[["ALL_VAL_MO","COMM_LVL","E_COMMODITY","CTY_CODE","time"],\n["155905","HS10","2710121510","1220","2016-01"],\n["260801","HS10","2710121510","1220","2016-02"],\n["241362","HS10","2710121510","1220","2016-03"],\n["461102","HS10","2710121510","1220","2016-04"],\n["442085","HS10","2710121510","1220","2016-05"],\n["449950","HS10","2710121510","1220","2016-06"],\n["398612","HS10","2710121510","1220","2016-07"],\n["214201","HS10","2710121510","1220","2016-08"],\n["260553","HS10","2710121510","1220","2016-09"],\n["94817","HS10","2710121510","1220","2016-10"],\n["93819","HS10","2710121510","1220","2016-11"],\n["119305","HS10","2710121510","1220","2016-12"],\n["118137","HS10","2710121510","1220","2017-01"],\n["54086","HS10","2710121510","1220","2017-02"],\n["116552","HS10","2710121510","1220","2017-03"],\n["318672","HS10","2710121510","1220","2017-04"],\n["444123","HS10","2710121510","1220","2017-05"],\n["389088","HS10","2710121510","1220","2017-06"],\n["272465","HS10","2710121510","1220","2017-07"],\n["511173","HS10","2710121510","1220","2017-08"],\n["130557","HS10","2710121510","1220","2017-09"],\n["201213","HS10","2710121510","1220","2017-10"],\n["40139","HS10","2710121510","1220","2017-11"],\n["103272","HS10","2710121510","1220","2017-12"],\n["137066","HS10","2710121510","1220","2018-01"],\n["361690","HS10","2710121510","1220","2018-02"],\n["1320733","HS10","2710121510","1220","2018-03"],\n["1007941","HS10","2710121510","1220","2018-04"],\n["1073177","HS10","2710121510","1220","2018-05"],\n["928253","HS10","2710121510","1220","2018-06"],\n["1375339","HS10","2710121510","1220","2018-07"],\n["558228","HS10","2710121510","1220","2018-08"],\n["217529","HS10","2710121510","1220","2018-09"],\n["187087","HS10","2710121510","1220","2018-10"],\n["142569","HS10","2710121510","1220","2018-11"],\n["83674","HS10","2710121510","1220","2018-12"],\n["87341","HS10","2710121510","1220","2019-01"],\n["99474","HS10","2710121510","1220","2019-02"],\n["218571","HS10","2710121510","1220","2019-03"],\n["348237","HS10","2710121510","1220","2019-04"],\n["505889","HS10","2710121510","1220","2019-05"],\n["360161","HS10","2710121510","1220","2019-06"],\n["353637","HS10","2710121510","1220","2019-07"],\n["446640","HS10","2710121510","1220","2019-08"],\n["151817","HS10","2710121510","1220","2019-09"],\n["69939","HS10","2710121510","1220","2019-10"],\n["181568","HS10","2710121510","1220","2019-11"],\n["107361","HS10","2710121510","1220","2019-12"],\n["90049","HS10","2710121510","1220","2020-01"],\n["190188","HS10","2710121510","1220","2020-02"],\n["134073","HS10","2710121510","1220","2020-03"],\n["54731","HS10","2710121510","1220","2020-04"],\n["196432","HS10","2710121510","1220","2020-05"],\n["211094","HS10","2710121510","1220","2020-06"],\n["303470","HS10","2710121510","1220","2020-07"],\n["550620","HS10","2710121510","1220","2020-08"],\n["646304","HS10","2710121510","1220","2020-09"],\n["146364","HS10","2710121510","1220","2020-10"],\n["388121","HS10","2710121510","1220","2020-11"],\n["150890","HS10","2710121510","1220","2020-12"],\n["119277","HS10","2710121510","1220","2021-01"],\n["112245","HS10","2710121510","1220","2021-02"],\n["237974","HS10","2710121510","1220","2021-03"],\n["1008608","HS10","2710121510","1220","2021-04"],\n["878643","HS10","2710121510","1220","2021-05"],\n["1143896","HS10","2710121510","1220","2021-06"],\n["1475335","HS10","2710121510","1220","2021-07"],\n["1196134","HS10","2710121510","1220","2021-08"],\n["1297127","HS10","2710121510","1220","2021-09"],\n["841871","HS10","2710121510","1220","2021-10"],\n["283675","HS10","2710121510","1220","2021-11"],\n["372945","HS10","2710121510","1220","2021-12"],\n["401325","HS10","2710121510","1220","2022-01"],\n["462537","HS10","2710121510","1220","2022-02"],\n["1176989","HS10","2710121510","1220","2022-03"],\n["1453827","HS10","2710121510","1220","2022-04"],\n["1616200","HS10","2710121510","1220","2022-05"],\n["2941925","HS10","2710121510","1220","2022-06"],\n["2346022","HS10","2710121510","1220","2022-07"],\n["1445319","HS10","2710121510","1220","2022-08"],\n["1870331","HS10","2710121510","1220","2022-09"],\n["1721816","HS10","2710121510","1220","2022-10"],\n["934718","HS10","2710121510","1220","2022-11"],\n["457709","HS10","2710121510","1220","2022-12"],\n["641850","HS10","2710121510","1220","2023-01"],\n["405674","HS10","2710121510","1220","2023-02"],\n["1298177","HS10","2710121510","1220","2023-03"],\n["1166846","HS10","2710121510","1220","2023-04"],\n["2050420","HS10","2710121510","1220","2023-05"],\n["3351775","HS10","2710121510","1220","2023-06"],\n["1390009","HS10","2710121510","1220","2023-07"],\n["1482895","HS10","2710121510","1220","2023-08"],\n["1675802","HS10","2710121510","1220","2023-09"],\n["1036568","HS10","2710121510","1220","2023-10"],\n["416533","HS10","2710121510","1220","2023-11"],\n["930226","HS10","2710121510","1220","2023-12"],\n["123306","HS10","2710121510","1220","2024-01"],\n["447629","HS10","2710121510","1220","2024-02"],\n["1139964","HS10","2710121510","1220","2024-03"],\n["1238111","HS10","2710121510","1220","2024-04"],\n["2299392","HS10","2710121510","1220","2024-05"],\n["2101577","HS10","2710121510","1220","2024-06"],\n["4132615","HS10","2710121510","1220","2024-07"],\n["4511732","HS10","2710121510","1220","2024-08"],\n["1567507","HS10","2710121510","1220","2024-09"],\n["1702503","HS10","2710121510","1220","2024-10"],\n["992138","HS10","2710121510","1220","2024-11"],\n["685974","HS10","2710121510","1220","2024-12"],\n["619902","HS10","2710121510","1220","2025-01"],\n["704793","HS10","2710121510","1220","2025-02"],\n["949205","HS10","2710121510","1220","2025-03"],\n["1851571","HS10","2710121510","1220","2025-04"],\n["1758005","HS10","2710121510","1220","2025-05"],\n["1491454","HS10","2710121510","1220","2025-06"],\n["2195739","HS10","2710121510","1220","2025-07"],\n["2817558","HS10","2710121510","1220","2025-08"],\n["1768317","HS10","2710121510","1220","2025-09"],\n["1246003","HS10","2710121510","1220","2025-10"],\n["657671","HS10","2710121510","1220","2025-11"],\n["108068","HS10","2710121510","1220","2025-12"],\n["372361","HS10","2710121510","1220","2026-01"]]'




```python
# Using json method
response.json()
```




    [['ALL_VAL_MO', 'COMM_LVL', 'E_COMMODITY', 'CTY_CODE', 'time'],
     ['155905', 'HS10', '2710121510', '1220', '2016-01'],
     ['260801', 'HS10', '2710121510', '1220', '2016-02'],
     ['241362', 'HS10', '2710121510', '1220', '2016-03'],
     ['461102', 'HS10', '2710121510', '1220', '2016-04'],
     ['442085', 'HS10', '2710121510', '1220', '2016-05'],
     ['449950', 'HS10', '2710121510', '1220', '2016-06'],
     ['398612', 'HS10', '2710121510', '1220', '2016-07'],
     ['214201', 'HS10', '2710121510', '1220', '2016-08'],
     ['260553', 'HS10', '2710121510', '1220', '2016-09'],
     ['94817', 'HS10', '2710121510', '1220', '2016-10'],
     ['93819', 'HS10', '2710121510', '1220', '2016-11'],
     ['119305', 'HS10', '2710121510', '1220', '2016-12'],
     ['118137', 'HS10', '2710121510', '1220', '2017-01'],
     ['54086', 'HS10', '2710121510', '1220', '2017-02'],
     ['116552', 'HS10', '2710121510', '1220', '2017-03'],
     ['318672', 'HS10', '2710121510', '1220', '2017-04'],
     ['444123', 'HS10', '2710121510', '1220', '2017-05'],
     ['389088', 'HS10', '2710121510', '1220', '2017-06'],
     ['272465', 'HS10', '2710121510', '1220', '2017-07'],
     ['511173', 'HS10', '2710121510', '1220', '2017-08'],
     ['130557', 'HS10', '2710121510', '1220', '2017-09'],
     ['201213', 'HS10', '2710121510', '1220', '2017-10'],
     ['40139', 'HS10', '2710121510', '1220', '2017-11'],
     ['103272', 'HS10', '2710121510', '1220', '2017-12'],
     ['137066', 'HS10', '2710121510', '1220', '2018-01'],
     ['361690', 'HS10', '2710121510', '1220', '2018-02'],
     ['1320733', 'HS10', '2710121510', '1220', '2018-03'],
     ['1007941', 'HS10', '2710121510', '1220', '2018-04'],
     ['1073177', 'HS10', '2710121510', '1220', '2018-05'],
     ['928253', 'HS10', '2710121510', '1220', '2018-06'],
     ['1375339', 'HS10', '2710121510', '1220', '2018-07'],
     ['558228', 'HS10', '2710121510', '1220', '2018-08'],
     ['217529', 'HS10', '2710121510', '1220', '2018-09'],
     ['187087', 'HS10', '2710121510', '1220', '2018-10'],
     ['142569', 'HS10', '2710121510', '1220', '2018-11'],
     ['83674', 'HS10', '2710121510', '1220', '2018-12'],
     ['87341', 'HS10', '2710121510', '1220', '2019-01'],
     ['99474', 'HS10', '2710121510', '1220', '2019-02'],
     ['218571', 'HS10', '2710121510', '1220', '2019-03'],
     ['348237', 'HS10', '2710121510', '1220', '2019-04'],
     ['505889', 'HS10', '2710121510', '1220', '2019-05'],
     ['360161', 'HS10', '2710121510', '1220', '2019-06'],
     ['353637', 'HS10', '2710121510', '1220', '2019-07'],
     ['446640', 'HS10', '2710121510', '1220', '2019-08'],
     ['151817', 'HS10', '2710121510', '1220', '2019-09'],
     ['69939', 'HS10', '2710121510', '1220', '2019-10'],
     ['181568', 'HS10', '2710121510', '1220', '2019-11'],
     ['107361', 'HS10', '2710121510', '1220', '2019-12'],
     ['90049', 'HS10', '2710121510', '1220', '2020-01'],
     ['190188', 'HS10', '2710121510', '1220', '2020-02'],
     ['134073', 'HS10', '2710121510', '1220', '2020-03'],
     ['54731', 'HS10', '2710121510', '1220', '2020-04'],
     ['196432', 'HS10', '2710121510', '1220', '2020-05'],
     ['211094', 'HS10', '2710121510', '1220', '2020-06'],
     ['303470', 'HS10', '2710121510', '1220', '2020-07'],
     ['550620', 'HS10', '2710121510', '1220', '2020-08'],
     ['646304', 'HS10', '2710121510', '1220', '2020-09'],
     ['146364', 'HS10', '2710121510', '1220', '2020-10'],
     ['388121', 'HS10', '2710121510', '1220', '2020-11'],
     ['150890', 'HS10', '2710121510', '1220', '2020-12'],
     ['119277', 'HS10', '2710121510', '1220', '2021-01'],
     ['112245', 'HS10', '2710121510', '1220', '2021-02'],
     ['237974', 'HS10', '2710121510', '1220', '2021-03'],
     ['1008608', 'HS10', '2710121510', '1220', '2021-04'],
     ['878643', 'HS10', '2710121510', '1220', '2021-05'],
     ['1143896', 'HS10', '2710121510', '1220', '2021-06'],
     ['1475335', 'HS10', '2710121510', '1220', '2021-07'],
     ['1196134', 'HS10', '2710121510', '1220', '2021-08'],
     ['1297127', 'HS10', '2710121510', '1220', '2021-09'],
     ['841871', 'HS10', '2710121510', '1220', '2021-10'],
     ['283675', 'HS10', '2710121510', '1220', '2021-11'],
     ['372945', 'HS10', '2710121510', '1220', '2021-12'],
     ['401325', 'HS10', '2710121510', '1220', '2022-01'],
     ['462537', 'HS10', '2710121510', '1220', '2022-02'],
     ['1176989', 'HS10', '2710121510', '1220', '2022-03'],
     ['1453827', 'HS10', '2710121510', '1220', '2022-04'],
     ['1616200', 'HS10', '2710121510', '1220', '2022-05'],
     ['2941925', 'HS10', '2710121510', '1220', '2022-06'],
     ['2346022', 'HS10', '2710121510', '1220', '2022-07'],
     ['1445319', 'HS10', '2710121510', '1220', '2022-08'],
     ['1870331', 'HS10', '2710121510', '1220', '2022-09'],
     ['1721816', 'HS10', '2710121510', '1220', '2022-10'],
     ['934718', 'HS10', '2710121510', '1220', '2022-11'],
     ['457709', 'HS10', '2710121510', '1220', '2022-12'],
     ['641850', 'HS10', '2710121510', '1220', '2023-01'],
     ['405674', 'HS10', '2710121510', '1220', '2023-02'],
     ['1298177', 'HS10', '2710121510', '1220', '2023-03'],
     ['1166846', 'HS10', '2710121510', '1220', '2023-04'],
     ['2050420', 'HS10', '2710121510', '1220', '2023-05'],
     ['3351775', 'HS10', '2710121510', '1220', '2023-06'],
     ['1390009', 'HS10', '2710121510', '1220', '2023-07'],
     ['1482895', 'HS10', '2710121510', '1220', '2023-08'],
     ['1675802', 'HS10', '2710121510', '1220', '2023-09'],
     ['1036568', 'HS10', '2710121510', '1220', '2023-10'],
     ['416533', 'HS10', '2710121510', '1220', '2023-11'],
     ['930226', 'HS10', '2710121510', '1220', '2023-12'],
     ['123306', 'HS10', '2710121510', '1220', '2024-01'],
     ['447629', 'HS10', '2710121510', '1220', '2024-02'],
     ['1139964', 'HS10', '2710121510', '1220', '2024-03'],
     ['1238111', 'HS10', '2710121510', '1220', '2024-04'],
     ['2299392', 'HS10', '2710121510', '1220', '2024-05'],
     ['2101577', 'HS10', '2710121510', '1220', '2024-06'],
     ['4132615', 'HS10', '2710121510', '1220', '2024-07'],
     ['4511732', 'HS10', '2710121510', '1220', '2024-08'],
     ['1567507', 'HS10', '2710121510', '1220', '2024-09'],
     ['1702503', 'HS10', '2710121510', '1220', '2024-10'],
     ['992138', 'HS10', '2710121510', '1220', '2024-11'],
     ['685974', 'HS10', '2710121510', '1220', '2024-12'],
     ['619902', 'HS10', '2710121510', '1220', '2025-01'],
     ['704793', 'HS10', '2710121510', '1220', '2025-02'],
     ['949205', 'HS10', '2710121510', '1220', '2025-03'],
     ['1851571', 'HS10', '2710121510', '1220', '2025-04'],
     ['1758005', 'HS10', '2710121510', '1220', '2025-05'],
     ['1491454', 'HS10', '2710121510', '1220', '2025-06'],
     ['2195739', 'HS10', '2710121510', '1220', '2025-07'],
     ['2817558', 'HS10', '2710121510', '1220', '2025-08'],
     ['1768317', 'HS10', '2710121510', '1220', '2025-09'],
     ['1246003', 'HS10', '2710121510', '1220', '2025-10'],
     ['657671', 'HS10', '2710121510', '1220', '2025-11'],
     ['108068', 'HS10', '2710121510', '1220', '2025-12'],
     ['372361', 'HS10', '2710121510', '1220', '2026-01']]




```python
# First entry
response.json()[0]
```




    ['ALL_VAL_MO', 'COMM_LVL', 'E_COMMODITY', 'CTY_CODE', 'time']




```python
# First row?
response.json()[1]
```




    ['155905', 'HS10', '2710121510', '1220', '2016-01']




```python
# Turn into DF
exports = pd.DataFrame(response.json()[1:],columns=response.json()[0])
exports
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
      <th>ALL_VAL_MO</th>
      <th>COMM_LVL</th>
      <th>E_COMMODITY</th>
      <th>CTY_CODE</th>
      <th>time</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>155905</td>
      <td>HS10</td>
      <td>2710121510</td>
      <td>1220</td>
      <td>2016-01</td>
    </tr>
    <tr>
      <th>1</th>
      <td>260801</td>
      <td>HS10</td>
      <td>2710121510</td>
      <td>1220</td>
      <td>2016-02</td>
    </tr>
    <tr>
      <th>2</th>
      <td>241362</td>
      <td>HS10</td>
      <td>2710121510</td>
      <td>1220</td>
      <td>2016-03</td>
    </tr>
    <tr>
      <th>3</th>
      <td>461102</td>
      <td>HS10</td>
      <td>2710121510</td>
      <td>1220</td>
      <td>2016-04</td>
    </tr>
    <tr>
      <th>4</th>
      <td>442085</td>
      <td>HS10</td>
      <td>2710121510</td>
      <td>1220</td>
      <td>2016-05</td>
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
      <th>116</th>
      <td>1768317</td>
      <td>HS10</td>
      <td>2710121510</td>
      <td>1220</td>
      <td>2025-09</td>
    </tr>
    <tr>
      <th>117</th>
      <td>1246003</td>
      <td>HS10</td>
      <td>2710121510</td>
      <td>1220</td>
      <td>2025-10</td>
    </tr>
    <tr>
      <th>118</th>
      <td>657671</td>
      <td>HS10</td>
      <td>2710121510</td>
      <td>1220</td>
      <td>2025-11</td>
    </tr>
    <tr>
      <th>119</th>
      <td>108068</td>
      <td>HS10</td>
      <td>2710121510</td>
      <td>1220</td>
      <td>2025-12</td>
    </tr>
    <tr>
      <th>120</th>
      <td>372361</td>
      <td>HS10</td>
      <td>2710121510</td>
      <td>1220</td>
      <td>2026-01</td>
    </tr>
  </tbody>
</table>
<p>121 rows × 5 columns</p>
</div>




```python
# If/else
if response.ok:
    # If server responds run this code:
    exports = pd.DataFrame(response.json()[1:],columns=response.json()[0])
    print(type(exports["ALL_VAL_MO"][2]))
    
    # Convert time to datetime
    exports['time'] = pd.to_datetime(exports['time'])
    exports["ALL_VAL_MO"] = exports["ALL_VAL_MO"].astype(float)/100000

    # Plot the data over time
    fig, ax = plt.subplots()
    ax.plot(exports["time"], exports["ALL_VAL_MO"])
    ax.set(ylabel="Billions of US$",
           title="US Gasoline Exports to Canada")

    plt.show()
    
else:
    # otherwise display the status code:
    print("Error ",response.status_code)
```

    <class 'str'>
    


    
![png](output_23_1.png)
    


## Practice - Census API
1. Instead of US Oil Exports to Canada, find US Imports from Russia
2. Start from January 2016 to now
3. Create a line plot of imports over time. Does anything stand out?


```python
# Results:
# Set query parameters
base_url = 'https://api.census.gov/data/timeseries/intltrade/imports/hs'
variables = 'GEN_VAL_MO,CTY_NAME'
country = '4621'
dates = 'from+2016-01'

# Formula full URL
full_url = (base_url
            + '?get=' + variables 
            + '&CTY_CODE=' + country
            + '&time=' + dates)

# Submit query
response = requests.get(full_url)

# Clean up resulting data frame 
imports = pd.DataFrame(response.json()[1:],columns=response.json()[0])

# Convert time to datetime
imports['time'] = pd.to_datetime(imports['time'])
imports["GEN_VAL_MO"] = imports["GEN_VAL_MO"].astype(float)/100000

# Plot the data over time
fig, ax = plt.subplots()
ax.plot(imports["time"], imports["GEN_VAL_MO"])
ax.set(ylabel="Billions of US$",
       title="US Gasoline Imports from Russia")

plt.show()
```

    <class 'str'>
    


    
![png](output_25_1.png)
    

