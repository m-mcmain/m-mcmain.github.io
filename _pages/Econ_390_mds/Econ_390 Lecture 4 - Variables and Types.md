# Econ 390 - Lecture 4: Variables and Types

The goal for this lecture is to learn how to create variables (focusing on Int, Float, and String) and applying various operators to them (addition, multiplication, etc...). You can find further reading in [McKinney](https://wesmckinney.com/book/python-basics#scalar_types) and Turrell for [variables](https://aeturrell.github.io/coding-for-economists/code-basics.html#values-variables-and-types) and [operators](https://aeturrell.github.io/coding-for-economists/code-basics.html#operators).

## Int & Float


```python
# Let's just try the most basic type
a = 0.05
print(type(a))
```

    <class 'float'>
    


```python
# How does printing Ints vs. Floats differ? How similar can variable names be?
age_pres = 35
age_retirement = 65

# Federal Funds Rate:
interest_rate = 0.05
# Bank Interest Rate:
Interest_rate = 0.03

print(age_pres, age_retirement)
print(interest_rate, Interest_rate)
```

    35 65
    0.05 0.03
    


```python
# Variable name with a number in it?
#2_years_ago = 2023

# Need to type it out
two_years_ago = 2023

# Unless it's not first
years_ago_2 = 2023 
```


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
zzz = 2        *        2

print(z, zz, zzz)
```

    4 4 4
    


```python
# Printing more than just variables
#print(This is z, zz, zzz)

print("This is", z, zz, zzz)
```

    This is 4 4 4
    


```python
# Order of operations and Python
x1 = 4 / 2 * 3

# Clarify the denominator
x2 = 4 / (2 * 3)

# Or the numerator
x3 = (4 / 2) * 3

# What does Python do?
print(x1, x2, x3)
```

    6.0 0.6666666666666666 6.0
    


```python
# Style after the equals sign
# Squish it all together
x_1 = 3+4*2
# Or separate based on priority
x_2 = 3 + 4*2
# Parentheses can help
x_3 = 3 + (4 * 2)
# But they can also hurt
x_4 = ( (3) + ( (4)*(2) ) )

print(x_1, x_2, x_3, x_4)
```

    11 11 11 11
    


```python
# Division is possible
d = 10/2
# But also more complicated
d2 = 365/12
# And even MORE complicated
d3 = 16.25/3.2

print(d, d2, d3)
```

    5.0 30.416666666666668 5.078125
    


```python
# Test the types
print(type(d), type(d3))
```

    <class 'float'> <class 'float'>
    


```python
# Explore float precision
start = 2
root = 2**(0.5)
back_to_start = root**2
print(back_to_start)
```

    2.0000000000000004
    


```python
# Assignment and updating with ease
n_firm = 1000

# Update when something happens
additional_firms = 100
n_firm += additional_firms

print(n_firm)
```

    1100
    

## Practice - Int and Float
1. Create a variable `years_ago_3` and set it equal to `years_ago_2` minus 1.
2. Create a variable `years_ago_4` by referencing `years_ago_3`.
3. Print all of the `years_ago_x` variables.
4. Create a variable called `age` and set it equal to your own age.
5. Create a variable called `years_until_pres` and set it equal to how many years it will be before you can be president (don't worry about citizenship concerns). Be sure to only reference variables to create this one.
6. Create a variable called `pres_year` and set it equal to the year you will be able to become president (don't worry about actual election years). Only reference variables again (which means you'll need to create a new variable - name it whatever you'd like).
7. Print variables from #4 - 6 to make sure they're correct. Adjust if they are not.


```python
# Results
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
# 7. 
print(age, years_until_pres, pres_year)
```

    2023 2022 2021
    27 8 2034
    

## String


```python
# Define some strings
string_1 = 'First String'
string_2 = "Second String"
print(string_1, type(string_2))
print('I\'m happy here')
```

    First String <class 'str'>
    I'm happy here
    


```python
# Problematic Strings
#string_problem = "They said "Things are OK" even though they were not"
#string_problem2 = 'What's the deal with airplane food?'
```


```python
# Let's fix that
string_1 = 'They said "Things are OK" even though they were not.'
string_2 = "I'll repeat."
string_3 = 'They said "Things are OK" even though they weren\'t.'
print(string_1, string_2, string_3)
```

    They said "Things are OK" even though they were not. I'll repeat. They said "Things are OK" even though they weren't.
    


```python
# We can do new lines as well
string_lines = "This is the first line \n This is the second \nThis is the third"
print(string_lines)
```

    This is the first line 
     This is the second 
    This is the third
    


```python
# Adding Strings?
first = "Bucky"
last = "Badger"
name = first+last
print(name)
```

    BuckyBadger
    


```python
# Multiplying Strings ??
print(first*5)
print(10*first)
```

    BuckyBuckyBuckyBuckyBucky
    BuckyBuckyBuckyBuckyBuckyBuckyBuckyBuckyBuckyBucky
    


```python
# Division, Multiplication, Text
dm = 20.4/5.1
print(dm,type(dm))
# Multiplication
dm = 4*2
print(dm,type(dm))
# Text
dm = "direct message"
print(dm,type(dm))
```

    4.0 <class 'float'>
    8 <class 'int'>
    direct message <class 'str'>
    

add

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
# Results
# 1. First, third, and fourth 
# 2.
color = "Our's is Blue"
color = 'Our\'s is Blue'
# 3.
first = "Bucky "
last = "Badger"
print(first+last)
```

    Bucky Badger
    


```python
# Big Strings and Adding
hitchikers_guide = """
For a moment, nothing happened.
Then, after a second or so, nothing continued to happen.
"""

r_j = '''
Two households, both alike in dignity,
In fair Verona, where we lay our scene,
From ancient grudge break to new mutiny,
Where civil blood makes civil hands unclean.
'''

chaos = hitchikers_guide + r_j
print(chaos)
```

    
    For a moment, nothing happened.
    Then, after a second or so, nothing continued to happen.
    
    Two households, both alike in dignity,
    In fair Verona, where we lay our scene,
    From ancient grudge break to new mutiny,
    Where civil blood makes civil hands unclean.
    
    


```python
# Strings as headers
"""
This program [description of program here]
[your name here]
[date the program was written here]
"""

a = 88
b = 22

print(a+b)
```

    110
    
