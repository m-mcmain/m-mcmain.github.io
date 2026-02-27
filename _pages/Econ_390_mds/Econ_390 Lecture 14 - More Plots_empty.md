---
layout: single
sitemap: false
permalink: /pages/Econ_390_SP26_L14/
---

[Download Jupyter Notebook Empty](https://m-mcmain.github.io/files/Econ390SP26/Lectures/Lecture14_MorePlots_empty.ipynb)

Download Jupyter Notebook Completed

# Econ 390 - Lecture 14: More Plots
Today we will be going over making plots with Matplotlib that aren't line plots. Appropriate material is [the rest of Chapter 9 that is not about line plots in McKinney](https://wesmckinney.com/book/plotting-and-visualization) and similar for [Turrell](https://aeturrell.github.io/coding-for-economists/vis-matplotlib.html).

## Subplots


```python
# As always
```


```python
# Initialize our figure
```


```python
# Add Subplot method
```


```python
# More?
```


```python
# Fill out one of the subplots
```


```python
# And the others
```


```python
# Reshape to move panels around and access like a list
```


```python
# Side by side subplots
```


```python
# Making it look a bit nicer
```


```python
# Let's utilize a loop to be more efficient

# To do so, we need a subset that only has CHY_USD and USD_Broad
```


```python
# Generate World Plot

# Generate Regional Plots

# Label Regional Graph Axes
```

## Histograms


```python
# Calculating percent growth of variables
```


```python
# Plotting growth rates

# Add a horizontal line at y=0 for reference
```


```python
# Histogram is more suitable
```


```python
# Default methods
```


```python
# Adding our usuals
```

## Practice - Histograms
Try the following changes:
1. Change the year range to 1929–1985. HINT: Take a slice with .loc[ ]
2. Make a plot with two subplots (side-by-side), where the first shows the data from 2006-2012 and the second shows the data 2013–2024
3. Change the figsize, bin, alpha, and color arguments to whatever you like!
4. Add a vertical line at zero. *Hint: Knowing how to do a horizontal line, how would you make it vertical?*
5. Challenging: For each of the two plots, compute the mean annual percent growth rate for that time period and put the vertical line there instead of at zero


```python
# Reference Code
fig, ax1 = plt.subplots(figsize=(16,9))
ax1.hist(USD_ER['USD_Broad_growth'], bins=20, alpha=1, color='navy')
ax1.set(ylabel='Frequency',
        xlabel='Monthly growth rate (%)',
        title='Frequency of Broad USD growth rates (2006-2025)')
ax1.spines[['right','top']].set_visible(False)
plt.show()
```


```python
# Practice
```

## Bar Plots


```python
# Tally the number of times each percent growth rate occurs

# Generate a bar chart
```


```python
# Go back to our manufacturing data
```


```python
# Convert Data
```


```python
# Gen total employment
```


```python
# Calculate number of times each outcome occurs
```


```python
# Generate bar chart
```


```python
# We can use similar options as before
```


```python
# Some changes
```

## Practice - Bar Plots
Try the following changes to the bar chart above:
1. Try displaying percentages instead of counts. *Hint: You only need to change the crosstab statement. Look back to Lecture 12 if you've forgotten.*
2. Can we make this a horizontal bar chart? It’s pretty easy actually. Instead of the bar method, try the barh method. Do we get an error? Why?


```python

```
