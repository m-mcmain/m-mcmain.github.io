---
layout: single
sitemap: false
permalink: /pages/Econ_390_SP26_L25/
title: Econ 390 Lecture 25
---

[Download Jupyter Notebook Empty](https://m-mcmain.github.io/files/Econ390SP26/Lectures/Lecture25_Lasso_empty.ipynb)

Download Jupyter Notebook Completed

# Econ 390 - Lecture 25: Least Absolute Shrinkage and Selection Operator (Lasso)
Today we'll be talking about Machine Learning, specifically the Lasso regression. You can find a chapter in [Turrell](https://aeturrell.github.io/coding-for-economists/ml-sup.html) that covers Lasso and other similar regression methods. I also used [this](https://geostatsguy.github.io/MachineLearningDemos_Book/MachineLearning_LASSO_regression.html) resource when creating this lecture. Machine Learning is a complicated topic, you can spend much much more time on Lasso alone. Regardless, I am hoping after this class you can have at least a basic understanding of how Lasso works and how it can be useful.

## The Lasso


```python
import matplotlib.pyplot as plt
import numpy as np
import pandas as pd

# Reproducability
seed = 42
prng = np.random.default_rng(seed)
```


```python
# New library!
from sklearn.datasets import make_regression

# Creates a dataset based on a randomized regression

```


```python
# What is X?

```


```python
# Convert to DataFrame

```


```python
# x0 on y

```


```python
# Supervised means training set and test set
from sklearn.model_selection import train_test_split

```


```python
# Let's run Lasso!
from sklearn import linear_model


```


```python
# Results:

```


```python
# Predictions:

```


```python
# Mean Square Error (MSE):
from sklearn.metrics import mean_squared_error

```


```python
# Compare MSE in and out of sample

```


```python
# Prediction vs. Truth

```


```python
# Plot the errors

```


```python
# Different values of alpha

```

## UCI Machine Learning Repository
UC Irvine has a [website](https://archive.ics.uci.edu/) full of datasets that are useful for Machine Learning! Today we will be using the [Default of Credit Cards](https://archive.ics.uci.edu/dataset/350/default+of+credit+card+clients) dataset.


```python
econ390path = "https://m-mcmain.github.io/files/Econ390SP26/"
```


```python
# Read in the data
default = pd.read_csv(econ390path + "default_of_credit_card_clients_cut.csv")
log_columns = ["LIMIT_BAL", "BILL_AMT1", "BILL_AMT2", "BILL_AMT3", "BILL_AMT4", "BILL_AMT5", "BILL_AMT6", 
               "PAY_AMT1", "PAY_AMT2", "PAY_AMT3", "PAY_AMT4", "PAY_AMT5", "PAY_AMT6"]

```


```python
# Create the training and testing set

```


```python
# Standard OLS
import statsmodels.formula.api as smf

```


```python
# Collect the results for many different alpha

```


```python
# Plot the MSE over alpha

```


```python
# Plot the coefficients for different values of alpha, natural Feature Selection

```

## Optional Extra Credit Posted
You've likely noticed the new "assignment" on Canvas. It is a completely optional extra credit that will cover the Lasso and is worth 5 Assignment points. These points will be added on *after* the curve is applied. So, importantly, not doing this extra credit will have **no negative impact** on your grade. This is just a way to give people who are right on the edge of a grade cutoff to get that little boost necessary to get "bumped" up. 

Here's the calculation:
1. I will do the standard curve, splitting up the class into bins based on percentiles.
   - This will set the grade cutoffs for each letter
2. I will then add any extra credit after the cutoffs are set
   - If the extra credit pushes you above the cutoff, your letter grade will go up
3. I will then compare that grade to the grade your numerical score would earn and choose the higher of the two

## End of Content
We made it! Before we leave, I'd appreciate if you could take 5-10 minutes here completing the [course evaluation](https://heliocampusac.wisc.edu/) if you haven't already. You should be able to click on the link, login, and look for the "Available Forms" tile and click on this course. 

Since this is my first time as an instructor and first time teaching this course, you can have a very big impact on what this course looks like if I teach it again. So I would appreciate any honest, constructive feedback you have for me!

Thanks for spending part of your semester with me in Econ 390 and on Thursday we will review for the Final Exam.
