---
layout: single
sitemap: false
permalink: /pages/Econ_390_SP26_L7_empty/
---

[Download Jupyter Notebook Empty](https://m-mcmain.github.io/files/Econ390SP26/Lectures/Lecture7_Loops_empty.ipynb)

Download Jupyter Notebook Completed

# Econ 390 - Lecture 7: Loops

Today we will go through Loops and List Comprehension. These are powerful tools that allow you to do the same task over and over again until certain conditions are met. You can find relevant reading for [McKinney](https://wesmckinney.com/book/python-basics#control_for) and [Turrell](https://aeturrell.github.io/coding-for-economists/code-basics.html#loops-and-list-comprehensions).

## Loops


```python
# For loops just go through each entry after "for"
```


```python
# Here is how range works
```


```python
# You can print through lists by indexing
```


```python
# Or by directly referencing the list
```


```python
# You can utilize enumerate for lists as well
```


```python
# If you don't like indexing with 0 you can start at 1 instead
```


```python
# You can add elif statements if you want it to match
```


```python
# You can force out of a loop by using break
```


```python
# You can reference multiple lists using indexing
```


```python
# Or taking advantage of zip
```


```python
# This is what zip does
```


```python
# While loops exist, but are generally less common
```


```python
# Input is a thing, though not very helpful for economics
```

## Practice - Loops
1. Write a for loop that calculates and saves the previous 1, 2, and 3 years in a list
   - Then, unpack the list and save them as years_ago_1, years_ago_2, and years_ago_3 appropriately
2. Write a for loop that goes through the most recent inflation in each country, using the format method to print out "X recently experienced low/high/hyper inflation of Y%" where X is the country and Y is their inflation. Define low as less than or equal to 2%, high as between 2% and 50%, and hyper as above 50%.


```python
year = 2026
inflation_dict = {'United States':2.9, 'United Arab Emirates':1.7, 'Angola':4.0, 'Venezuela':219.9}
```

## String Comprehension


```python
# Lists can internally do it
```


```python
# Same with strings
```


```python
# And ifs
```


```python
# Even if elses
```

## Practice - List Comprehension
1. Use list comprehension to convert this list of dollars into a list of M-Bills, where one M-Bill is 1.5 dollars.
`[1, 5, 20, 100]`
2. Use list comprehension to convert this integer into a list of singular numbers. (Hint: What have we seen before that separates singular characters in lists?)
`a = 32651`
3. Using list comprehension, create two lists, one of the even numbers and one of the odd numbers of the following list. (Hint: % is "modular", which will return the leftover from division. E.g. 4%3 = 1)
`[1, 2, 3, 4, 5, 6]`


```python

```
