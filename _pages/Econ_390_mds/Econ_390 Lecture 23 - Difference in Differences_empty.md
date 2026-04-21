---
layout: single
sitemap: false
permalink: /pages/Econ_390_SP26_L23_empty/
title: Econ 390 Lecture 23
---

[Download Jupyter Notebook Empty](https://m-mcmain.github.io/files/Econ390SP26/Lectures/Lecture23_DifferenceinDifferences_empty.ipynb)

Download Jupyter Notebook Completed

# Econ 390: Lecture 23 - Difference in Differences
Today we will be going over how to visualize and conduct the econometric method called Difference in Differences (DiD). DiD at its core is very simple, there is a point in time where something changes and we want to understand what that change caused. We can't just assume everything after the change is due to the change alone, so we find a comparison group to disentangle the change and time itself. Inspiration for this lecture can be found [here](https://www.pymc.io/projects/examples/en/latest/causal_inference/difference_in_differences.html) and [here](https://aaronmams.github.io/Card-Krueger-Replication/).

![Simple Diff-in-Diff Example](https://www.pymc.io/projects/examples/en/latest/_images/8f0282bc3fafdc3f95d353ed712496d5fab4d0c009f5c0d8ecaf42f7a8626b37.png)

## Parallel Trends
Parallel trends are *paramount* to our assumption of Difference-in-Differences analysis! It must be the case that these two groups are **actually comparable**. This analysis is all about what would have happened if the treatment group was not treated. We must be confident that we can actually extract that using the information on the control group!

## Card and Krueger (1994)
One of the most famous example of DiD is from the 1992 American Economic Review (AER) paper "Minimum Wages and Employment: A Case Study of the Fast-Food Industry in New Jersey and Pennsylvania" by David Card and Alan Krueger (you can find the paper and data on Card's website [here](https://davidcard.berkeley.edu/data_sets)).


```python
import pandas as pd
import matplotlib.pyplot as plt 
import statsmodels.formula.api as smf 

econ390path = "https://m-mcmain.github.io/files/Econ390SP26/"
```


```python
# Data process
names = ["CHAINr", "CO_OWNED", "STATEr", "SOUTHJ", "CENTRALJ", "NORTHJ", "PA1", "PA2", "SHORE", "NCALLS", 
         "EMPFT", "EMPPT", "NMGRS", "WAGE_ST", "INCTIME", "FIRSTINC", "BONUS", "PCTAFF", "MEAL", "OPEN",
         "HRSOPEN", "PSODA", "PFRY", "PENTREE", "NREGS", "NREGS11", "TYPE2", "STATUS2", "DATE2", "NCALLS2",
         "EMPFT2", "EMPPT2", "NMGRS2", "WAGE_ST2", "INCTIME2", "FIRSTIN2", "SPECIAL2", "MEALS2", "OPEN2R",
         "HRSOPEN2", "PSODA2", "PFRY2", "PENTREE2", "NREGS2", "NREGS112"]
```


```python
# Measure of employment

```


```python
# Convert data we need

```

## Wage Visualizations


```python
# Basic Visualization of Wages

```


```python
# Force the Same Bins

```


```python
# Second Period same bins

```


```python
# Good reason to not have the same bins!

```


```python
# Compare within NJ before and after

```


```python
# What happens in PA?

```


```python
# Classic DiD Plot on Wage:

```


```python
# Standard Plot, not necessarily surprising results

```

## Employment Visualization


```python
# Eployment Across Time in NJ

```


```python
# Employment Across States in Post-Period

```


```python
# Employment Across States in Pre-Period

```


```python
# Classic DiD Plot on Employment:

```


```python
# Standard Plot, not necessarily surprising results

```

## DiD Regression


```python
# Basic Regressions

```




```python
# More Elaborate Regressions

```


```python
# This is kind of a non-standard way to do DiD

```


```python
# Now do the regression

```
