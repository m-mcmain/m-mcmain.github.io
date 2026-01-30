---
layout: single
sitemap: false
permalink: /pages/Econ_390_SP26_L4/
---
[Download Jupyter Notebook Empty](https://m-mcmain.github.io/files/Econ390SP26/Lectures/Lecture4_VariablesandTypes_empty.ipynb)

[Download Jupyter Notebook Completed](https://m-mcmain.github.io/files/Econ390SP26/Lectures/Lecture4_VariablesandTypes_full.ipynb)

# Econ 390 - Lecture 4: Variables and Types

The goal for this lecture is to learn how to create variables (focusing on Int, Float, and String) and applying various operators to them (addition, multiplication, etc...). You can find further reading in [McKinney](https://wesmckinney.com/book/python-basics#scalar_types) and Turrell for [variables](https://aeturrell.github.io/coding-for-economists/code-basics.html#values-variables-and-types) and [operators](https://aeturrell.github.io/coding-for-economists/code-basics.html#operators).

## Int & Float


```python
# Let's just try the most basic type
a = 0.05
a;
print(type(a))
```

    <class 'float'>
    


```python
# How does printing Ints vs. Floats differ? How similar can variable names be?
age_pres = 35
age_retire = 65

# Federal Funds Rate
interest_rate_FFR = 0.035
# Bank's Interest Rate
interest_rate_Bank = 0.03

print(age_pres, age_retire, sep=", ")
print(interest_rate_FFR, interest_rate_Bank)
```

    35, 65
    0.035 0.03
    


```python
# Variable name with a number in it?
#2_years_ago = 2024

# Type it out
two_years_ago = 2024

# Just don't have it first
years_ago_2 = 2024
print(two_years_ago, years_ago_2)
```

    2024 2024
    


```python
# Variables equal to each other
# Define a
a = 5

# Define b as equal to a
b = a

# Re-Define a
a = a*5

# What happens?
print(a, b)
```

    25 5
    


```python
# How do spaces after equal signs work?
z = 2*2
zz = 2 * 2
zzz = 2               *                        2

print(z, zz, zzz)
```

    4 4 4
    


```python
# Printing more than just variables
print('This is', z, zz, zzz, sep=", ", end=".\n")
print("Hi there.")
```

    This is, 4, 4, 4.
    Hi there.
    


```python
# Order of operations and Python
x1 = 4 / 2 * 3

# Clarify the denominator
x2 = 4 / (2 * 3)

# Specify the numerator
x3 = (4 / 2) * 3

print(x1, x2, x3)
```

    6.0 0.6666666666666666 6.0
    


```python
# Style after the equals sign
# Squish it all together
x_1 = 3+4*2
# Separate by prio
x_2 = 3 + 4*2
# Parentheses also emphasized
x_3 = 3 + (4 * 2)
# A lot of them suck
x_4 = ( (3) + (4 * 2) )

print(x_1, x_2, x_3, x_4)
```

    11 11 11 11
    


```python
# Division is possible
d = 10/2
d2 = 365/12
d3 = 16.25/3.2

print(d, d2, d3)
```

    5.0 30.416666666666668 5.078125
    


```python
# Test the types
print(type(d), type(d2))
```

    <class 'float'> <class 'float'>
    


```python
# Explore float precision
start = 2
root = 2**(0.5)
back_to_start = root**2
print(start, root, back_to_start)
```

    2 1.4142135623730951 2.0000000000000004
    


```python
# Assignment and updating with ease
n_firm = 1000

# Update when something happens
additional_firms = 100
n_firm += additional_firms
n_firm
```




    1100



## Practice - Int and Float
1. Create a variable `years_ago_3` and set it equal to `years_ago_2` minus 1.
2. Create a variable `years_ago_4` by referencing `years_ago_3`.
3. Print all of the `years_ago_x` variables.
4. Create a variable called `age` and set it equal to your own age.
5. Create a variable called `years_until_pres` and set it equal to how many years it will be before you can be president (don't worry about citizenship concerns). Be sure to only reference variables to create this one.
6. Create a variable called `pres_year` and set it equal to the year you will be able to become president (don't worry about actual election years). Only reference variables again (which means you'll need to create a new variable - name it whatever you'd like).


```python
# Results:
# 1.
years_ago_3 = years_ago_2 - 1
# 2.
years_ago_4 = years_ago_3 - 1
# 3. 
print(years_ago_2, years_ago_3, years_ago_4)
# 4.
age = 27
# 5.
years_until_pres = age_pres - age
# 6. 
year = 2026
pres_year = year + years_until_pres
pres_year
```

    2024 2023 2022
    




    2034




```python
years_ago_3
```




    2023



## String


```python
# Define some strings
string_1 = 'String One'
string_2 = "String Two"
print(string_1, type(string_2))
```

    String One <class 'str'>
    


```python
# Problematic Strings
print("I'm cold, the weatherman said \"it's gonna be real cold tomorrow\"")
print('I\'m cold')
```

    I'm cold, the weatherman said "it's gonna be real cold tomorrow"
    I'm cold
    


```python
# Let's fix that
string_1 = "I'm cold, the weatherman said"
string_2 = '"it\'s gonna be real cold tomorrow"'
string_3 = "I'm still cold"
print(string_1, string_2, string_3)
```

    I'm cold, the weatherman said "it's gonna be real cold tomorrow" I'm still cold
    


```python
# We can do new lines as well
strong_lines = "This is the first line\nThis is the second line\nThis is the third"
print(strong_lines)
```

    This is the first line
    This is the second line
    This is the third
    


```python
# Adding Strings?
first = "Bucky"
last = "Badger"
print(first+last)
```

    BuckyBadger
    


```python
# Multiplying Strings??
print(first*5)
print(10*first)
```

    BuckyBuckyBuckyBuckyBucky
    BuckyBuckyBuckyBuckyBuckyBuckyBuckyBuckyBuckyBucky
    


```python
# Division in Text
print(first/5)
```


    ---------------------------------------------------------------------------

    TypeError                                 Traceback (most recent call last)

    Cell In[67], line 2
          1 # Division in Text
    ----> 2 print(first/5)
    

    TypeError: unsupported operand type(s) for /: 'str' and 'int'


## Practice - Strings:
1. Without running any code, which of these are strings?
    - [ ] x = "10"
    - [ ] x = 10
    - [ ] x = '10'
    - [ ] x = "My Name"
    - [ ] x = 3.5
2. Make a code cell below and put in `color = 'Our's is Blue'` and fix it so that it works.
3. In that same cell, update the BuckyBadger series of code such that it reads "Bucky Badger" when it gets printed.


```python
print("Our's is Blue")
print('Our\'s is Blue')

print(first + " " + last)
```

    Our's is Blue
    Our's is Blue
    Bucky Badger
    


```python
# Big Strings and Adding
hitchhikers_guide = """
For a moment, nothing happened.
Then, after a second or so, nothing continued to happen.
"""
print(hitchhikers_guide)
```

    
    For a moment, nothing happened.
    Then, after a second or so, nothing continued to happen.
    
    


```python
# Strings as headers
"""
This program does stuff
[your name]
[date you wrote it]
"""

a = 88
b = 22

print(a+b)
type(type(string_2))
```

    110
    




    type


