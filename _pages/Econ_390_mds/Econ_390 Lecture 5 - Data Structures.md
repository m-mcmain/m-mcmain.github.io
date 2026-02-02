---
layout: single
sitemap: false
permalink: /pages/Econ_390_SP26_L5_teaching/
---
[Download Jupyter Notebook Empty](https://m-mcmain.github.io/files/Econ390SP26/Lectures/Lecture5_DataStructures_empty.ipynb)

Download Jupyter Notebook Completed

# Econ 390: Lecture 5 - Tuples, Lists, and Dictionaries

This lecture we will go through a few more variable types. You can find the relevant reading for [McKinney](https://wesmckinney.com/book/python-builtin#tut_data_structures) and the appropriate subsections in [Turrell](aeturrell.github.io/coding-for-economists/code-basics.html) (Lists and Slicing & Dictionaries).

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
tup_string = tuple("string")
print(tup_string)

# Tuples are indexed starting at 0 and can be accessed in reverse
print(tup_string[0])
print(tup_string[-1])
```

    ('s', 't', 'r', 'i', 'n', 'g')
    s
    g
    


```python
# You can assign other variables to be elements if you don't want to use index
a, b, c = tup
print(a, b, c)
```

    1 2 3
    


```python
# You can have a tuple of tuples
tup_of_tup = (1, 2, 3), (4, 5)
tup_of_tup
```




    ((1, 2, 3), (4, 5))




```python
# And access them as you might expect
print(tup_of_tup[1])
print(tup_of_tup[1][0])
```

    (4, 5)
    4
    


```python
# Tuples of different types are possible
tup_types = tuple(["string", [1, 2], True])
#tup_types[2] = False
```


```python
# But if one of the types are mutable, you can modify it
tup_types[1].append(3)
tup_types[1][1] = 4
tup_types
```




    ('string', [1, 4, 3], True)




```python
# You can also concatinate by "addition"
(1, 2, 3) + (True, 1) + (4, 'and',)
```




    (1, 2, 3, True, 1, 4, 'and')




```python
# Multiplication works as expected
("On", "Wisconsin!") * 2
```




    ('On', 'Wisconsin!', 'On', 'Wisconsin!')




```python
# Count is handy for learning how many times something shows up in a Tuple
a = 1, 2, 3, 3, 3, 4, 4, 1, 5, 2, 3
a.count(2)
```




    2



## Lists

Lists are similar to Tuples in some ways (e.g. nesting, different variable types), however they are very different in the sense that they can be easily changed.


```python
# Lists use brackets instead of parentheses
my_list = [1, 2, 3]
print("Here is my list: ", my_list)
print("The type of my list: ", type(my_list))

# The list function can convert something into a list
list_tup = list(tup_types)
print(list_tup)
```

    Here is my list:  [1, 2, 3]
    The type of my list:  <class 'list'>
    ['string', [1, 4, 3], True]
    


```python
# And now you can change stuff that previously couldn't be!
list_tup[2] = False
print(list_tup)
print(len(list_tup))
```

    ['string', [1, 4, 3], False]
    3
    


```python
# You can append and delete from lists
my_list.append(4)
print(my_list)
del my_list[0]
print(my_list)
```

    [1, 2, 3, 4]
    [2, 3, 4]
    


```python
# If you want to print and remove an element you can use pop
print(my_list.pop(0))
print(my_list)
```

    2
    [3, 4]
    


```python
# You can also remove by name
my_list.remove(4)
print(my_list)
```

    [3]
    


```python
# You can see if your list contains an element
print("Wisconsin" in my_list)
print(3 in my_list)
```

    False
    True
    


```python
# You can concatinate by addition or using extend if it's already defined
print(["On", "Wisconsin!", 390, None] + [None, True])
my_list.extend(["Join", "In", 3, None])
print(my_list)
```

    ['On', 'Wisconsin!', 390, None, None, True]
    [3, 'Join', 'In', 3, None]
    


```python
# You can similarly create variables to be elements
a, b, c, *_ = my_list
print(a, b, c, _)
```

    3 Join In [3, None]
    


```python
# Lists as pointers and not "variables"
new_list = my_list
a = 12
b = a
b += 1
new_list.append("Coffee")
print(my_list, new_list, a, b)
```

    [3, 'Join', 'In', 3, None, 'Coffee'] [3, 'Join', 'In', 3, None, 'Coffee'] 12 13
    

## Dictionaries

Dictionaries create a conversion mechanism for one variable to another (e.g. Grades!)


```python
# You create dictionaries like this:
grades = {'A':4.0, 'AB':3.5, 'B':3, 'BC':2.5, 'C':2.0, 'D':1.0, 'F':0.0}
print(grades)
print(type(grades))
```

    {'A': 4.0, 'AB': 3.5, 'B': 3, 'BC': 2.5, 'C': 2.0, 'D': 1.0, 'F': 0.0}
    <class 'dict'>
    


```python
# Here the letters are being converted to numbers
print(grades['BC'])
```

    2.5
    


```python
# Is it the other way around?
#print(grades[1.0])
```


```python
# We can add to the dictionary
grades['W'] = None
print(grades['W'])
print(grades)
```

    None
    {'A': 4.0, 'AB': 3.5, 'B': 3, 'BC': 2.5, 'C': 2.0, 'D': 1.0, 'F': 0.0, 'W': None}
    


```python
# We can also delete
del grades['W']
print(grades)
print(len(grades))
```

    {'A': 4.0, 'AB': 3.5, 'B': 3, 'BC': 2.5, 'C': 2.0, 'D': 1.0, 'F': 0.0}
    7
    

## Casting

You can convert variables to many different types (extending beyond what you've seen so far), usually in a way that's expected.


```python
pi = "3.1415"
print("Pi is", pi)
```

    Pi is 3.1415
    


```python
pi_float = float(pi)
print("Pi is", pi_float)
```

    Pi is 3.1415
    


```python
#pi_int = int(pi)
```


```python
pi_int = int(pi_float)
print("Pi is", pi_int)
```

    Pi is 3
    
