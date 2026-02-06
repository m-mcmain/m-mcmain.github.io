---
layout: single
sitemap: false
permalink: /pages/Econ_390_SP26_L8_teaching/
---

# Econ 390 - Lecture 8: Slicing and String Manipulation
You can find Turrell's [Slicing](https://aeturrell.github.io/coding-for-economists/code-basics.html#lists-and-slicing) and [String Manipulation](https://aeturrell.github.io/coding-for-economists/code-basics.html#strings) and McKinney's [Slicing](https://wesmckinney.com/book/python-builtin#list_slicing) and [String Manipulation](https://wesmckinney.com/book/data-cleaning#text_string_manip) (though McKinney's String Manipulation is more in depth than what we'll be doing today!).


```python
# Create a list of monthly inflation
monthly_inflation = [3, 2.81, 2.41, 2.33, 2.38, 2.67, 2.73, 2.94]

some_months = monthly_inflation[0] + monthly_inflation[2] + monthly_inflation[7]
some_months
```




    8.35




```python
# Need to define it as a list
some_months = [monthly_inflation[0], monthly_inflation[1], monthly_inflation[7]]
some_months
```




    [3, 2.81, 2.94]




```python
# But you can be more efficient
some_months = [monthly_inflation[i] for i in [0, 1, 7]]
some_months
```




    [3, 2.81, 2.94]




```python
# You can choose a sequential subset
monthly_inflation[2:5]
```




    [2.41, 2.33, 2.38]




```python
# Or start somewhere and go to the end
print(monthly_inflation[5:])
# Or start from the beginning and end somewhere
print(monthly_inflation[:5])
```

    [2.67, 2.73, 2.94]
    [3, 2.81, 2.41, 2.33, 2.38]
    


```python
# You can also choose the "step"
print(monthly_inflation[2:7:2])
print(monthly_inflation[2:7:3])
print(monthly_inflation[::2])
```

    [2.41, 2.38, 2.73]
    [2.41, 2.67]
    [3, 2.41, 2.38, 2.73]
    


```python
# You can also go backwards
print(monthly_inflation[-4])
print(monthly_inflation[-4:-2])
```

    2.38
    [2.38, 2.67]
    


```python
# You can do negative "steps" to reverse the whole thing
print(monthly_inflation[::-1])
```

    [2.94, 2.73, 2.67, 2.38, 2.33, 2.41, 2.81, 3]
    

## Practice: Slicing
1. Slice out the fourth, fifth, and sixth entries of the list `primes`.
   - What range do you give? How many numbers does it span (e.g. 1-4 spans 4 numbers)? Is that intuitive?
   - Now do it backwards. How many numbers does that span?
2. Slice out every other element of `primes` but ignore the first and last.
   - Do it again but now such that it will work even if we add more numbers to `primes`.
4. Using list commprehension create a list starting from 1990 and ending with 2026. Then create a new variable (named appropriately) that slices the list of years to just be census years (always the first year of the decade). (Note: This is not the only, or even most efficient, way to do this)


```python
primes = [1, 2, 3, 5, 7, 11, 13, 17]
# Results
# 1. 
print(primes[3:6])
print(primes[-5:-2])
# 2.
print(primes[1:7:2])
print(primes[1:len(primes)-1:2])
# 3.
election_years = [x for x in range(1990,2026)][0::10]
election_years
```

    [5, 7, 11]
    [5, 7, 11]
    [2, 5, 11]
    [2, 5, 11]
    




    [1990, 2000, 2010, 2020]



## String Manipulation


```python
# If you're worried about the consistency of variables, you can force a string to be all lowercase
state = "Wisconsin"
state_lower = state.lower()
print(state, state_lower)
```

    Wisconsin wisconsin
    


```python
# But you can also do it in the middle of the code
print("wisconsin" == state.lower())
```

    True
    


```python
# If you're worried about spaces before or after, you can get rid of those
state = "Wisconsin "
state_stripped = state.strip()
print(state_stripped)
print(state_stripped == "Wisconsin")
```

    Wisconsin
    True
    


```python
print(" Wiscon sin ".strip())
print(" Wisconsin ".strip())
```

    Wiscon sin
    Wisconsin
    


```python
print(" Wisconsin ".strip().lower() == "wisconsin")
```

    True
    


```python
# If there is a consistent issue, like a slash showing up, you can replace it
print("Wisc/onsin".replace("/",""))
print("Wisc/onsin    ".replace("/","").strip().lower() == "wisconsin")
```

    Wisconsin
    True
    


```python
# You can insert variables into strings as well
year = '2024'
gdp = 27720.7093
print('The GDP in', year, 'is', gdp, 'billions of dollars')
print('The GDP in ' + year + ' is ' + str(gdp) + ' billions of dollars')
```

    The GDP in 2024 is 27720.7093 billions of dollars
    The GDP in 2024 is 27720.7093 billions of dollars
    


```python
# You can use format to insert in a way that is a bit more simple
print('The GDP in {} is {} billions of dollars'.format(year,gdp))
print('The GDP in {Y} is {G} billions of dollars'.format(G=gdp, Y=year))
```

    The GDP in 2024 is 27720.7093 billions of dollars
    The GDP in 2024 is 27720.7093 billions of dollars
    


```python
# If you're concerned with the exact way it is being displayed you can select the variable type of what you list
print('The GDP in {Y} is {G:.1f} billions of dollars'.format(G=gdp,Y=year))
```

    The GDP in 2024 is 27720.7 billions of dollars
    

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
class_rank_lower = [rank.lower() for rank in class_rank]
print(class_rank_lower)

income = "25,800.50"
income = float(income.replace(",",""))
print("Their income was {d:.1f} thousand dollars last year.".format(d=income/1000))
```

    ['senior', 'junior', 'sophomore', 'freshman']
    Their income was 25.8 thousand dollars last year.
    
