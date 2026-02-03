---
layout: single
sitemap: false
permalink: /pages/Econ_390_SP26_L5/
---
[Download Jupyter Notebook Empty](https://m-mcmain.github.io/files/Econ390SP26/Lectures/Lecture5_DataStructures_empty.ipynb)

[Download Jupyter Notebook Completed](https://m-mcmain.github.io/files/Econ390SP26/Lectures/Lecture5_DataStructures_full.ipynb)

# Econ 390: Lecture 5 - Tuples, Lists, and Dictionaries

This lecture we will go through a few more variable types. You can find the relevant reading for [McKinney](https://wesmckinney.com/book/python-builtin#tut_data_structures) and the appropriate subsections in Turrell ([Lists and Slicing](https://aeturrell.github.io/coding-for-economists/code-basics.html#lists-and-slicing) & [Dictionaries](https://aeturrell.github.io/coding-for-economists/code-basics.html#dictionaries)).

## Tuples

A tuple is a type of variable that has a fixed length and cannot be changed once it is initialized.


```python
# Tuples use parentheses
tup = (1, 2, 3)

print(tup)
print(type(tup))
print(len(tup))
```

    (1, 2, 3)
    <class 'tuple'>
    3
    


```python
# Or nothing at all
tup = 1, 2, 3
print(tup)
```

    (1, 2, 3)
    


```python
# Convert things by using tuple
tuple([1, 2, 3])
```




    (1, 2, 3)




```python
# Strings included!
tup_string = tuple("snow")
print(tup_string)

# Accessing the elements, index starting with 0
print(tup_string[1])
print(tup_string[-4])
```

    ('s', 'n', 'o', 'w')
    n
    s
    


```python
# You can assign other variables to be elements if you don't want to use index
a, b, c = tup
d = tup[0]
print(d)
```

    1
    


```python
# You can have a tuple of tuples
tup_of_tup = ((1, 2, 3), (4, 5))
tup_of_tup
```




    ((1, 2, 3), (4, 5))




```python
# And access them as you might expect
tup_of_tup[0][1]
```




    2




```python
# Tuples of different types are possible
tup_types = ("snow", [1,2], True)
tup_types
#tup_types[2] = False
```




    ('snow', [1, 2], True)




```python
# But if one of the types are mutable, you can modify it
tup_types[1].append(3)
tup_types[1][1] = 4
print(tup_types)
```

    ('snow', [1, 4, 3], True)
    


```python
# You can also concatinate by "addition"
tup + (4, 5)
```




    (1, 2, 3, 4, 5)




```python
# Multiplication works as expected
print(("On", "Wisconsin!")*2)
```

    ('On', 'Wisconsin!', 'On', 'Wisconsin!')
    


```python
# Count is handy for learning how many times something shows up in a Tuple
a = 9, 9, 10, 8, 9
a.count(9)
```




    3



## Lists

Lists are similar to Tuples in some ways (e.g. nesting, different variable types), however they are very different in the sense that they can be easily changed.


```python
# Lists use brackets instead of parentheses
my_list = [1,2,3]
print(my_list)
print(type(my_list))

# Cast stuff into lists
list_tup = list(tup_types)
print(list_tup)

# Cast string into list
list_string = list("it's snowing!\n")
print(list_string)
```

    [1, 2, 3]
    <class 'list'>
    ['snow', [1, 4, 3], True]
    ['i', 't', "'", 's', ' ', 's', 'n', 'o', 'w', 'i', 'n', 'g', '!', '\n']
    


```python
# And now you can change stuff that previously couldn't be!
list_string[0] = "I"
print(list_string)
```

    ['I', 't', "'", 's', ' ', 's', 'n', 'o', 'w', 'i', 'n', 'g', '!', '\n']
    


```python
# You can append and delete from lists
my_list.append(4)
print(my_list)
del my_list[0]
print(my_list)
```

    [3, 4, 4, 4]
    [4, 4, 4]
    


```python
# If you want to print and remove an element you can use pop
print(my_list)
a = my_list.pop(0)
print(a, my_list)
```

    [2, 3, 4]
    2 [3, 4]
    


```python
# You can also remove by name
my_list = [4, 1, 2, 4, 3, 4]
my_list.remove(4)
print(my_list)
```

    [1, 2, 4, 3, 4]
    


```python
# You can see if your list contains an element
print("Wisconsin" in my_list)
print(3 in my_list)
print("3" in my_list)
print(3.0 in my_list)
```

    False
    True
    False
    True
    


```python
# You can concatinate by addition or using extend if it's already defined
print(["On", "Wisconsin!"] + [1, 2, 3])
my_list.extend(["On", "Wisconsin!"])
print(my_list)
```

    ['On', 'Wisconsin!', 1, 2, 3]
    [1, 2, 4, 3, 4, 'On', 'Wisconsin!']
    


```python
# You can similarly create variables to be elements
a, b, c, *_ = my_list
print(a,b,c,_)
```

    1 2 4 [3, 4, 'On', 'Wisconsin!']
    


```python
# Lists as pointers and not "variables"
a = 3
b = a
a += 1
new_list = my_list
new_list.append("Coffee")
print(a,b, my_list)
```

    4 3 [1, 2, 4, 3, 4, 'On', 'Wisconsin!', 'Coffee']
    

## Dictionaries

Dictionaries create a conversion mechanism for one variable to another (e.g. Grades!)


```python
# You create dictionaries like this:
grades = {'A':4.0, 'AB':3.5, 'B':3.0, 'BC':2.5, 'C':2.0, 'D':1.0, 'F':0.0}
print(grades)
print(type(grades))
```

    {'A': 4.0, 'AB': 3.5, 'B': 3.0, 'BC': 2.5, 'C': 2.0, 'D': 1.0, 'F': 0.0}
    <class 'dict'>
    


```python
# Here the letters are being converted to numbers
print(grades['BC'])
```

    2.5
    


```python
# Is it the other way around?
print(grades[2.5])
```


    ---------------------------------------------------------------------------

    KeyError                                  Traceback (most recent call last)

    Cell In[107], line 2
          1 # Is it the other way around?
    ----> 2 print(grades[2.5])
    

    KeyError: 2.5



```python
# We can add to the dictionary
grades['W'] = None
print(grades['W'])
print(grades)
```

    None
    {'A': 4.0, 'AB': 3.5, 'B': 3.0, 'BC': 2.5, 'C': 2.0, 'D': 1.0, 'F': 0.0, 'W': None}
    


```python
# We can also delete
del grades['W']
print(grades)
print(len(grades))
```

    {'A': 4.0, 'AB': 3.5, 'B': 3.0, 'BC': 2.5, 'C': 2.0, 'D': 1.0, 'F': 0.0}
    7
    

## Casting

You can convert variables to many different types (extending beyond what you've seen so far), usually in a way that's expected.


```python
# String
pi = "3.54156"
print(pi)
```

    3.54156
    


```python
# Into float
pi_float = float(pi)
print(type(pi_float))
```

    <class 'float'>
    


```python
# And Int?
pi_int = int(pi)
```


    ---------------------------------------------------------------------------

    ValueError                                Traceback (most recent call last)

    Cell In[121], line 2
          1 # And Int?
    ----> 2 pi_int = int(pi)
    

    ValueError: invalid literal for int() with base 10: '3.54156'



```python
# Float to Int
pi_int = int(pi_float)
print(pi_int)
```

    3
    
