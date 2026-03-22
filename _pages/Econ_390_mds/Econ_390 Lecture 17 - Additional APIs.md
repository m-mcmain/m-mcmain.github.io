---
layout: single
sitemap: false
permalink: /pages/Econ_390_SP26_L17_teaching/
title: Econ 390 Lecture 17
---

[Download Jupyter Notebook Empty](https://m-mcmain.github.io/files/Econ390SP26/Lectures/Lecture17_AdditionalAPIs_empty.ipynb)

Download Jupyter Notebook Completed

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
url = "https://sdmx.oecd.org/public/rest/data/OECD.GOV.GIP,DSD_GOV_INT@DF_GOV_TDG_2025,1.1/A.AUS+AUT+BEL+CAN+COL+DNK+EST+FIN+FRA+ISL+IRL+JPN+KOR+LVA+LUX+MEX+NLD+NZL+NOR+PRT+SWE+GBR+OECD_REP.TRUST_NG....HMH.?startPeriod=2021&endPeriod=2021&dimensionAtObservation=AllDimensions&format=csvfilewithlabels"
# Fetch data
response = requests.get(url)
```


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
# Load into pandas DataFrame
df = pd.read_csv(StringIO(response.text))

# Look through the DF
print(df)
```

       STRUCTURE                                   STRUCTURE_ID  \
    0   DATAFLOW  OECD.GOV.GIP:DSD_GOV_INT@DF_GOV_TDG_2025(1.1)   
    1   DATAFLOW  OECD.GOV.GIP:DSD_GOV_INT@DF_GOV_TDG_2025(1.1)   
    2   DATAFLOW  OECD.GOV.GIP:DSD_GOV_INT@DF_GOV_TDG_2025(1.1)   
    3   DATAFLOW  OECD.GOV.GIP:DSD_GOV_INT@DF_GOV_TDG_2025(1.1)   
    4   DATAFLOW  OECD.GOV.GIP:DSD_GOV_INT@DF_GOV_TDG_2025(1.1)   
    5   DATAFLOW  OECD.GOV.GIP:DSD_GOV_INT@DF_GOV_TDG_2025(1.1)   
    6   DATAFLOW  OECD.GOV.GIP:DSD_GOV_INT@DF_GOV_TDG_2025(1.1)   
    7   DATAFLOW  OECD.GOV.GIP:DSD_GOV_INT@DF_GOV_TDG_2025(1.1)   
    8   DATAFLOW  OECD.GOV.GIP:DSD_GOV_INT@DF_GOV_TDG_2025(1.1)   
    9   DATAFLOW  OECD.GOV.GIP:DSD_GOV_INT@DF_GOV_TDG_2025(1.1)   
    10  DATAFLOW  OECD.GOV.GIP:DSD_GOV_INT@DF_GOV_TDG_2025(1.1)   
    11  DATAFLOW  OECD.GOV.GIP:DSD_GOV_INT@DF_GOV_TDG_2025(1.1)   
    12  DATAFLOW  OECD.GOV.GIP:DSD_GOV_INT@DF_GOV_TDG_2025(1.1)   
    13  DATAFLOW  OECD.GOV.GIP:DSD_GOV_INT@DF_GOV_TDG_2025(1.1)   
    14  DATAFLOW  OECD.GOV.GIP:DSD_GOV_INT@DF_GOV_TDG_2025(1.1)   
    15  DATAFLOW  OECD.GOV.GIP:DSD_GOV_INT@DF_GOV_TDG_2025(1.1)   
    16  DATAFLOW  OECD.GOV.GIP:DSD_GOV_INT@DF_GOV_TDG_2025(1.1)   
    17  DATAFLOW  OECD.GOV.GIP:DSD_GOV_INT@DF_GOV_TDG_2025(1.1)   
    18  DATAFLOW  OECD.GOV.GIP:DSD_GOV_INT@DF_GOV_TDG_2025(1.1)   
    19  DATAFLOW  OECD.GOV.GIP:DSD_GOV_INT@DF_GOV_TDG_2025(1.1)   
    20  DATAFLOW  OECD.GOV.GIP:DSD_GOV_INT@DF_GOV_TDG_2025(1.1)   
    
                                           STRUCTURE_NAME ACTION FREQ  \
    0   Trust, security and dignity - government at a ...      I    A   
    1   Trust, security and dignity - government at a ...      I    A   
    2   Trust, security and dignity - government at a ...      I    A   
    3   Trust, security and dignity - government at a ...      I    A   
    4   Trust, security and dignity - government at a ...      I    A   
    5   Trust, security and dignity - government at a ...      I    A   
    6   Trust, security and dignity - government at a ...      I    A   
    7   Trust, security and dignity - government at a ...      I    A   
    8   Trust, security and dignity - government at a ...      I    A   
    9   Trust, security and dignity - government at a ...      I    A   
    10  Trust, security and dignity - government at a ...      I    A   
    11  Trust, security and dignity - government at a ...      I    A   
    12  Trust, security and dignity - government at a ...      I    A   
    13  Trust, security and dignity - government at a ...      I    A   
    14  Trust, security and dignity - government at a ...      I    A   
    15  Trust, security and dignity - government at a ...      I    A   
    16  Trust, security and dignity - government at a ...      I    A   
    17  Trust, security and dignity - government at a ...      I    A   
    18  Trust, security and dignity - government at a ...      I    A   
    19  Trust, security and dignity - government at a ...      I    A   
    20  Trust, security and dignity - government at a ...      I    A   
    
       Frequency of observation  REF_AREA        Reference area   MEASURE  \
    0                    Annual       ISL               Iceland  TRUST_NG   
    1                    Annual       KOR                 Korea  TRUST_NG   
    2                    Annual       COL              Colombia  TRUST_NG   
    3                    Annual       DNK               Denmark  TRUST_NG   
    4                    Annual       EST               Estonia  TRUST_NG   
    5                    Annual       JPN                 Japan  TRUST_NG   
    6                    Annual       FIN               Finland  TRUST_NG   
    7                    Annual       LVA                Latvia  TRUST_NG   
    8                    Annual       LUX            Luxembourg  TRUST_NG   
    9                    Annual       NLD           Netherlands  TRUST_NG   
    10                   Annual       NOR                Norway  TRUST_NG   
    11                   Annual       PRT              Portugal  TRUST_NG   
    12                   Annual       SWE                Sweden  TRUST_NG   
    13                   Annual       GBR        United Kingdom  TRUST_NG   
    14                   Annual  OECD_REP  OECD average country  TRUST_NG   
    15                   Annual       AUS             Australia  TRUST_NG   
    16                   Annual       AUT               Austria  TRUST_NG   
    17                   Annual       BEL               Belgium  TRUST_NG   
    18                   Annual       CAN                Canada  TRUST_NG   
    19                   Annual       IRL               Ireland  TRUST_NG   
    20                   Annual       FRA                France  TRUST_NG   
    
                             Measure  ... OBS_VALUE Observation value OBS_STATUS  \
    0   Trust in national government  ...      50.4               NaN          A   
    1   Trust in national government  ...      48.8               NaN          A   
    2   Trust in national government  ...      20.5               NaN          A   
    3   Trust in national government  ...      48.8               NaN          A   
    4   Trust in national government  ...      46.5               NaN          A   
    5   Trust in national government  ...      24.0               NaN          A   
    6   Trust in national government  ...      61.5               NaN          A   
    7   Trust in national government  ...      24.5               NaN          A   
    8   Trust in national government  ...      55.9               NaN          A   
    9   Trust in national government  ...      49.1               NaN          A   
    10  Trust in national government  ...      63.8               NaN          A   
    11  Trust in national government  ...      40.7               NaN          A   
    12  Trust in national government  ...      39.0               NaN          A   
    13  Trust in national government  ...      34.8               NaN          A   
    14  Trust in national government  ...      41.4               NaN          A   
    15  Trust in national government  ...      38.0               NaN          A   
    16  Trust in national government  ...      25.8               NaN          A   
    17  Trust in national government  ...      31.8               NaN          A   
    18  Trust in national government  ...      44.7               NaN          A   
    19  Trust in national government  ...      50.6               NaN          A   
    20  Trust in national government  ...      28.1               NaN          A   
    
       Observation status  UNIT_MULT  Unit multiplier PRICE_BASE      Price base  \
    0        Normal value          0            Units         _Z  Not applicable   
    1        Normal value          0            Units         _Z  Not applicable   
    2        Normal value          0            Units         _Z  Not applicable   
    3        Normal value          0            Units         _Z  Not applicable   
    4        Normal value          0            Units         _Z  Not applicable   
    5        Normal value          0            Units         _Z  Not applicable   
    6        Normal value          0            Units         _Z  Not applicable   
    7        Normal value          0            Units         _Z  Not applicable   
    8        Normal value          0            Units         _Z  Not applicable   
    9        Normal value          0            Units         _Z  Not applicable   
    10       Normal value          0            Units         _Z  Not applicable   
    11       Normal value          0            Units         _Z  Not applicable   
    12       Normal value          0            Units         _Z  Not applicable   
    13       Normal value          0            Units         _Z  Not applicable   
    14       Normal value          0            Units         _Z  Not applicable   
    15       Normal value          0            Units         _Z  Not applicable   
    16       Normal value          0            Units         _Z  Not applicable   
    17       Normal value          0            Units         _Z  Not applicable   
    18       Normal value          0            Units         _Z  Not applicable   
    19       Normal value          0            Units         _Z  Not applicable   
    20       Normal value          0            Units         _Z  Not applicable   
    
       BASE_PER Base period  
    0       NaN         NaN  
    1       NaN         NaN  
    2       NaN         NaN  
    3       NaN         NaN  
    4       NaN         NaN  
    5       NaN         NaN  
    6       NaN         NaN  
    7       NaN         NaN  
    8       NaN         NaN  
    9       NaN         NaN  
    10      NaN         NaN  
    11      NaN         NaN  
    12      NaN         NaN  
    13      NaN         NaN  
    14      NaN         NaN  
    15      NaN         NaN  
    16      NaN         NaN  
    17      NaN         NaN  
    18      NaN         NaN  
    19      NaN         NaN  
    20      NaN         NaN  
    
    [21 rows x 32 columns]
    


```python
# Subset just what we need
df = df[["OBS_VALUE","REF_AREA"]]
df.index = df["REF_AREA"]
df = df.drop(index = "OECD_REP")
avg_trust = df["OBS_VALUE"].mean()
```


```python
# Create Histogram
fig, ax = plt.subplots()
ax.hist(df["OBS_VALUE"])
ax.set(xlabel="% High and Moderately High",
       title="Distribution of Trust in National Government OECD")
plt.axvline(x=avg_trust, color="red")

plt.show()
```


    
![png](output_10_0.png)
    


## Practice: OECD API
1. Use the [OECD Data Explorer](https://data-explorer.oecd.org/) to find a dataset you'd be interested in downloading.
2. Get the API URL.
3. Display the first five rows. Does this immediately work if you just copy the URL from the API? *Hint: Make sure that you specify the format*


```python
url_practice = ""
response_practice = 
# Load into pandas DataFrame
df_practice = 
# Display first few rows
print(df_practice.head())
```


```python
# Results:
url_practice = "https://sdmx.oecd.org/public/rest/data/OECD.ECO.MAD,DSD_EO_114@DF_EO_114,1.0/AUS+AUT+BEL.BSII+NTR+GDPV_ANNPCT.?startPeriod=2016&endPeriod=2025&dimensionAtObservation=AllDimensions&format=csvfilewithlabels"
response_practice = requests.get(url_practice)
# Load into pandas DataFrame
df_practice = pd.read_csv(StringIO(response_practice.text))
# Display first few rows
print(df_practice.head())
```

      STRUCTURE                            STRUCTURE_ID        STRUCTURE_NAME  \
    0  DATAFLOW  OECD.ECO.MAD:DSD_EO_114@DF_EO_114(1.0)  Economic Outlook 114   
    1  DATAFLOW  OECD.ECO.MAD:DSD_EO_114@DF_EO_114(1.0)  Economic Outlook 114   
    2  DATAFLOW  OECD.ECO.MAD:DSD_EO_114@DF_EO_114(1.0)  Economic Outlook 114   
    3  DATAFLOW  OECD.ECO.MAD:DSD_EO_114@DF_EO_114(1.0)  Economic Outlook 114   
    4  DATAFLOW  OECD.ECO.MAD:DSD_EO_114@DF_EO_114(1.0)  Economic Outlook 114   
    
      ACTION REF_AREA Reference area      MEASURE  \
    0      I      AUS      Australia  GDPV_ANNPCT   
    1      I      AUS      Australia  GDPV_ANNPCT   
    2      I      AUS      Australia  GDPV_ANNPCT   
    3      I      AUS      Australia  GDPV_ANNPCT   
    4      I      AUS      Australia  GDPV_ANNPCT   
    
                                      Measure FREQ Frequency of observation  ...  \
    0  Gross domestic product, volume, growth    Q                Quarterly  ...   
    1  Gross domestic product, volume, growth    Q                Quarterly  ...   
    2  Gross domestic product, volume, growth    Q                Quarterly  ...   
    3  Gross domestic product, volume, growth    Q                Quarterly  ...   
    4  Gross domestic product, volume, growth    Q                Quarterly  ...   
    
        BASE_PER  Base period  METHODOLOGY  Methodology  DECIMALS  Decimals  \
    0  2020-2021          NaN          NaN          NaN         2       Two   
    1  2020-2021          NaN          NaN          NaN         2       Two   
    2  2020-2021          NaN          NaN          NaN         2       Two   
    3  2020-2021          NaN          NaN          NaN         2       Two   
    4  2020-2021          NaN          NaN          NaN         2       Two   
    
      PRICE_BASE Price base  ADJUSTMENT Adjustment  
    0        NaN        NaN         NaN        NaN  
    1        NaN        NaN         NaN        NaN  
    2        NaN        NaN         NaN        NaN  
    3        NaN        NaN         NaN        NaN  
    4        NaN        NaN         NaN        NaN  
    
    [5 rows x 32 columns]
    

## Census API



```python
base_url = 'https://api.census.gov/data/timeseries/intltrade/exports/hs'
```


```python
variables = 'ALL_VAL_MO'  # get the variables: total value
level = 'HS10'            # 10-digit harmonized system
commodity = '2710121510'  # Data for Gasoline
country = '1220'          # Data from Canada
dates = 'from+2016-01'    # Data from Jan 2010 to present
```


```python
# Formulate full URL
full_url = (base_url
            + '?get=' + variables 
            + '&COMM_LVL=' + level 
            + '&E_COMMODITY=' + commodity 
            + '&CTY_CODE=' + country
            + '&time=' + dates)
```


```python
# Set query parameters
base_url = 'https://api.census.gov/data/timeseries/intltrade/exports/hs'
variables = 'ALL_VAL_MO'   # get the variables: total value
level = 'HS10'             # 10-digit harmonized system
commodity = '2710121510'   # Data for Gasoline
country = '1220'           # Data from Canada
dates = 'from+2016-01'     # Data from Jan 2010 to present

# Formulate full URL
full_url = (base_url
            + '?get=' + variables 
            + '&COMM_LVL=' + level 
            + '&E_COMMODITY=' + commodity 
            + '&CTY_CODE=' + country
            + '&time=' + dates)

# Submit query
response = requests.get(full_url)

response
```




    <Response [200]>




```python
# Content of the request
response.content
```




    b'[["ALL_VAL_MO","COMM_LVL","E_COMMODITY","CTY_CODE","time"],\n["155905","HS10","2710121510","1220","2016-01"],\n["260801","HS10","2710121510","1220","2016-02"],\n["241362","HS10","2710121510","1220","2016-03"],\n["461102","HS10","2710121510","1220","2016-04"],\n["442085","HS10","2710121510","1220","2016-05"],\n["449950","HS10","2710121510","1220","2016-06"],\n["398612","HS10","2710121510","1220","2016-07"],\n["214201","HS10","2710121510","1220","2016-08"],\n["260553","HS10","2710121510","1220","2016-09"],\n["94817","HS10","2710121510","1220","2016-10"],\n["93819","HS10","2710121510","1220","2016-11"],\n["119305","HS10","2710121510","1220","2016-12"],\n["118137","HS10","2710121510","1220","2017-01"],\n["54086","HS10","2710121510","1220","2017-02"],\n["116552","HS10","2710121510","1220","2017-03"],\n["318672","HS10","2710121510","1220","2017-04"],\n["444123","HS10","2710121510","1220","2017-05"],\n["389088","HS10","2710121510","1220","2017-06"],\n["272465","HS10","2710121510","1220","2017-07"],\n["511173","HS10","2710121510","1220","2017-08"],\n["130557","HS10","2710121510","1220","2017-09"],\n["201213","HS10","2710121510","1220","2017-10"],\n["40139","HS10","2710121510","1220","2017-11"],\n["103272","HS10","2710121510","1220","2017-12"],\n["137066","HS10","2710121510","1220","2018-01"],\n["361690","HS10","2710121510","1220","2018-02"],\n["1320733","HS10","2710121510","1220","2018-03"],\n["1007941","HS10","2710121510","1220","2018-04"],\n["1073177","HS10","2710121510","1220","2018-05"],\n["928253","HS10","2710121510","1220","2018-06"],\n["1375339","HS10","2710121510","1220","2018-07"],\n["558228","HS10","2710121510","1220","2018-08"],\n["217529","HS10","2710121510","1220","2018-09"],\n["187087","HS10","2710121510","1220","2018-10"],\n["142569","HS10","2710121510","1220","2018-11"],\n["83674","HS10","2710121510","1220","2018-12"],\n["87341","HS10","2710121510","1220","2019-01"],\n["99474","HS10","2710121510","1220","2019-02"],\n["218571","HS10","2710121510","1220","2019-03"],\n["348237","HS10","2710121510","1220","2019-04"],\n["505889","HS10","2710121510","1220","2019-05"],\n["360161","HS10","2710121510","1220","2019-06"],\n["353637","HS10","2710121510","1220","2019-07"],\n["446640","HS10","2710121510","1220","2019-08"],\n["151817","HS10","2710121510","1220","2019-09"],\n["69939","HS10","2710121510","1220","2019-10"],\n["181568","HS10","2710121510","1220","2019-11"],\n["107361","HS10","2710121510","1220","2019-12"],\n["90049","HS10","2710121510","1220","2020-01"],\n["190188","HS10","2710121510","1220","2020-02"],\n["134073","HS10","2710121510","1220","2020-03"],\n["54731","HS10","2710121510","1220","2020-04"],\n["196432","HS10","2710121510","1220","2020-05"],\n["211094","HS10","2710121510","1220","2020-06"],\n["303470","HS10","2710121510","1220","2020-07"],\n["550620","HS10","2710121510","1220","2020-08"],\n["646304","HS10","2710121510","1220","2020-09"],\n["146364","HS10","2710121510","1220","2020-10"],\n["388121","HS10","2710121510","1220","2020-11"],\n["150890","HS10","2710121510","1220","2020-12"],\n["119277","HS10","2710121510","1220","2021-01"],\n["112245","HS10","2710121510","1220","2021-02"],\n["237974","HS10","2710121510","1220","2021-03"],\n["1008608","HS10","2710121510","1220","2021-04"],\n["878643","HS10","2710121510","1220","2021-05"],\n["1143896","HS10","2710121510","1220","2021-06"],\n["1475335","HS10","2710121510","1220","2021-07"],\n["1196134","HS10","2710121510","1220","2021-08"],\n["1297127","HS10","2710121510","1220","2021-09"],\n["841871","HS10","2710121510","1220","2021-10"],\n["283675","HS10","2710121510","1220","2021-11"],\n["372945","HS10","2710121510","1220","2021-12"],\n["401325","HS10","2710121510","1220","2022-01"],\n["462537","HS10","2710121510","1220","2022-02"],\n["1176989","HS10","2710121510","1220","2022-03"],\n["1453827","HS10","2710121510","1220","2022-04"],\n["1616200","HS10","2710121510","1220","2022-05"],\n["2941925","HS10","2710121510","1220","2022-06"],\n["2346022","HS10","2710121510","1220","2022-07"],\n["1445319","HS10","2710121510","1220","2022-08"],\n["1870331","HS10","2710121510","1220","2022-09"],\n["1721816","HS10","2710121510","1220","2022-10"],\n["934718","HS10","2710121510","1220","2022-11"],\n["457709","HS10","2710121510","1220","2022-12"],\n["641850","HS10","2710121510","1220","2023-01"],\n["405674","HS10","2710121510","1220","2023-02"],\n["1298177","HS10","2710121510","1220","2023-03"],\n["1166846","HS10","2710121510","1220","2023-04"],\n["2050420","HS10","2710121510","1220","2023-05"],\n["3351775","HS10","2710121510","1220","2023-06"],\n["1390009","HS10","2710121510","1220","2023-07"],\n["1482895","HS10","2710121510","1220","2023-08"],\n["1675802","HS10","2710121510","1220","2023-09"],\n["1036568","HS10","2710121510","1220","2023-10"],\n["416533","HS10","2710121510","1220","2023-11"],\n["930226","HS10","2710121510","1220","2023-12"],\n["123306","HS10","2710121510","1220","2024-01"],\n["447629","HS10","2710121510","1220","2024-02"],\n["1139964","HS10","2710121510","1220","2024-03"],\n["1238111","HS10","2710121510","1220","2024-04"],\n["2299392","HS10","2710121510","1220","2024-05"],\n["2101577","HS10","2710121510","1220","2024-06"],\n["4132615","HS10","2710121510","1220","2024-07"],\n["4511732","HS10","2710121510","1220","2024-08"],\n["1567507","HS10","2710121510","1220","2024-09"],\n["1702503","HS10","2710121510","1220","2024-10"],\n["992138","HS10","2710121510","1220","2024-11"],\n["685974","HS10","2710121510","1220","2024-12"],\n["619902","HS10","2710121510","1220","2025-01"],\n["704793","HS10","2710121510","1220","2025-02"],\n["949205","HS10","2710121510","1220","2025-03"],\n["1851571","HS10","2710121510","1220","2025-04"],\n["1758005","HS10","2710121510","1220","2025-05"],\n["1491454","HS10","2710121510","1220","2025-06"],\n["2195739","HS10","2710121510","1220","2025-07"],\n["2817558","HS10","2710121510","1220","2025-08"],\n["1768317","HS10","2710121510","1220","2025-09"]]'




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
     ['1768317', 'HS10', '2710121510', '1220', '2025-09']]




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
exports = pd.DataFrame(response.json()[1:], columns=response.json()[0])
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
      <th>112</th>
      <td>1758005</td>
      <td>HS10</td>
      <td>2710121510</td>
      <td>1220</td>
      <td>2025-05</td>
    </tr>
    <tr>
      <th>113</th>
      <td>1491454</td>
      <td>HS10</td>
      <td>2710121510</td>
      <td>1220</td>
      <td>2025-06</td>
    </tr>
    <tr>
      <th>114</th>
      <td>2195739</td>
      <td>HS10</td>
      <td>2710121510</td>
      <td>1220</td>
      <td>2025-07</td>
    </tr>
    <tr>
      <th>115</th>
      <td>2817558</td>
      <td>HS10</td>
      <td>2710121510</td>
      <td>1220</td>
      <td>2025-08</td>
    </tr>
    <tr>
      <th>116</th>
      <td>1768317</td>
      <td>HS10</td>
      <td>2710121510</td>
      <td>1220</td>
      <td>2025-09</td>
    </tr>
  </tbody>
</table>
<p>117 rows × 5 columns</p>
</div>




```python
if response.ok:
    # If server responds, store data in frame
    exports = pd.DataFrame(response.json()[1:], columns=response.json()[0])

    # Convert time to datetime and ALL_VAL_MO to float (in billions of USD)
    exports['time']=pd.to_datetime(exports['time'])
    exports['ALL_VAL_MO']=exports['ALL_VAL_MO'].astype(float) / 1000000

    # Plot the data
    with plt.style.context('paper.mplstyle'):
        fig, ax = plt.subplots(figsize=(10,5))
        ax.plot(exports['time'], exports['ALL_VAL_MO'])
        ax.set(ylabel='Billions of US $',
               title='Gasoline Exports to Canada')    
    plt.show()

else:
    # Otherwise finish by displaying status code
    print ('Server error ', response.status_code)
```


    
![png](output_24_0.png)
    


## Practice - Census API
1. Instead of US Oil Exports to Canada, find US Oil Imports from Russia
2. Start from January 2016 to now
3. Create a line plot of imports over time. Does anything stand out?


```python
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
imports = pd.DataFrame(response.json()[1:], columns=response.json()[0])
imports['time'] = pd.to_datetime(imports['time'])
imports['GEN_VAL_MO'] = imports['GEN_VAL_MO'].astype(int)/1000000

with plt.style.context('paper.mplstyle'):
    fig, ax = plt.subplots()
    ax.plot(imports['time'], imports['GEN_VAL_MO'])
    ax.set(ylabel="Billions of US $",
           title="Gasoline Imports from Russia")
plt.show()
```


    
![png](output_26_0.png)
    

