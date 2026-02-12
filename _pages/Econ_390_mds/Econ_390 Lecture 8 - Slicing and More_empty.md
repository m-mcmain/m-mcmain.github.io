---
layout: single
sitemap: false
permalink: /pages/Econ_390_SP26_L8_empty/
---

[Download Jupyter Notebook Empty](https://m-mcmain.github.io/files/Econ390SP26/Lectures/Lecture8_SlicingandMore_empty.ipynb)

Download Jupyter Notebook Completed

# Econ 390 - Lecture 8: Slicing and String Manipulation
You can find Turrell's [Slicing](https://aeturrell.github.io/coding-for-economists/code-basics.html#lists-and-slicing) and [String Manipulation](https://aeturrell.github.io/coding-for-economists/code-basics.html#strings) and McKinney's [Slicing](https://wesmckinney.com/book/python-builtin#list_slicing) and [String Manipulation](https://wesmckinney.com/book/data-cleaning#text_string_manip) (though McKinney's String Manipulation is more in depth than what we'll be doing today!).


```python
# Create a list of monthly inflation
```


```python
# Need to define it as a list
```


```python
# But you can be more efficient
```


```python
# You can choose a sequential subset
```


```python
# Or start somewhere and go to the end
```


```python
# You can also choose the "step"
```


```python
# You can also go backwards
```


```python
# You can do negative "steps" to reverse the whole thing
```

## Practice: Slicing
1. Slice out the fourth, fifth, and sixth entries of the list `primes`.
   - What range do you give? How many numbers does it span (e.g. 1-4 spans 4 numbers)? Is that intuitive?
   - Now do it backwards. How many numbers does that span?
2. Slice out every other element of `primes` but ignore the first and last.
   - Do it again but now such that it will work even if we add more numbers to `primes`.
4. Using list commprehension create a list starting from 1990 and ending with 2026. Then create a new variable (named appropriately) that slices the list of years to just be census years (always the first year of the decade). (Note: This is not the only, or even most efficient, way to do this)


```python
primes = [1, 2, 3, 5, 7, 11, 13, 17]
```

## String Manipulation


```python
# If you're worried about the consistency of variables, you can force a string to be all lowercase
```


```python
# But you can also do it in the middle of the code
```


```python
# If you're worried about spaces before or after, you can get rid of those
```


```python
# Spaces in the middle?
```


```python
# Multiple Methods!
```


```python
# If there is a consistent issue, like a slash showing up, you can replace it
```


```python
# You can insert variables into strings as well
```


```python
# You can use format to insert in a way that is a bit more simple
```


```python
# If you're concerned with the exact way it is being displayed you can select the variable type of what you list
```

## Practice: String Manipulation
Consider the list `class_rank = ['SENIOR', 'junior', 'Sophomore', 'FRESHMAN']`
1. Use a list comprehension to create a list called class_rank_lower that converts class_rank into all lowercase.
2. Use a list comprehension to create a list called class_rank_upper that just keeps the elements of class_rank that are all uppercase.

Now consider `income = "25,800.50"`

3. Can you cast income as a float? Why might Python be upset?
4. How can you get income into a castable form without changing the definition of the variable?
5. Using the format method, print something like "Their income was 25.8 thousand dollars last year."


```python
class_rank = ['SENIOR', 'junior', 'Sophomore', 'FRESHMAN']
income = "25,800.50"
```
