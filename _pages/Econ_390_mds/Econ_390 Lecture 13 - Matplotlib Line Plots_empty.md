---
layout: single
sitemap: false
permalink: /pages/Econ_390_SP26_L13/
---

[Download Jupyter Notebook Empty](https://m-mcmain.github.io/files/Econ390SP26/Lectures/Lecture13_MatplotlibLinePlots_empty.ipynb)

Download Jupyter Notebook Completed

# Econ 390 - Lecture 13: Matplotlib Line Plots
Today we will begin learning how to create plots in Python using Matplotlib. You can find the relevant textbook chapters for [McKinney](https://wesmckinney.com/book/plotting-and-visualization) and [Turrell](https://aeturrell.github.io/coding-for-economists/vis-matplotlib.html#understanding-matplotlib).

## Essay Competition
There is an [Undergraduate Essay Competition](https://csld.wisc.edu/2026/02/27/announcing-the-2026-undergraduate-essay-competition/) being run by the Center for the Study of Liberal Democracy here at UW Madison. ~1000 word essays due on March 30th.

## Data


```python

# Load Exchange Rate Data into a DataFrame
```

## Intro to Matplotlib


```python
# New imports
```


```python
# Defining your first plot
```


```python
# What types are these new objects?
```


```python
# Using plot to make lines
```


```python
# Plotting from our DataFrame
```


```python
# ANOTHER new package

# New option to read_csv
```


```python
# Try it now
```


```python
# Set limits on the axes
```


```python
# Just do it all in one line
```


```python
# When that one line gets really long you can make it more readable
```


```python
# Options
```

## Practice - Line Plots
1. Is there a better way to deal with the axes? What is a way to do it to not manually change xlim and ylim?
2. Copy and paste the previous plot below and add the line for the Chinese Yuan RMB to USD. If you did the previous part right, you still shouldn't need to manually update xlim and ylim!
3. Modify the code to change the color of the Chinese Yuan RMB to USD line.
4. Modify your code and add the argument alpha=0.3 as a line style option for the Chinese Yuan RMB to USD line. What does this change?
5. Modify the code to make one of the lines dashed. Or try out `linestyle = '--'` `linestyle = '-.'` `linestyle = ':'`
6. With all of these changes, how do you feel about the plot? Any concerns?


```python

```

## Line Plots with Multiple Lines


```python
# Multiple lines?
```


```python
# Let's make it look nicer and add another line
```


```python
# Let's fix one of these
```


```python
# Manually include text
```


```python
# Plot alone works, but it makes assumptions about what you want!
```


```python
# Let's drop the USD to EU ER and go again
```


```python
# If you want to have similar styles for many different lines, you can loop through them
```
