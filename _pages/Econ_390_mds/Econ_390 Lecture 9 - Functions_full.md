---
layout: single
sitemap: false
permalink: /pages/Econ_390_SP26_L9/
---

[Download Jupyter Notebook Empty](https://m-mcmain.github.io/files/Econ390SP26/Lectures/Lecture9_Functions_empty.ipynb)

[Download Jupyter Notebook Completed](https://m-mcmain.github.io/files/Econ390SP26/Lectures/Lecture9_Functions_full.ipynb)

# Econ 390 - Lecture 9: Functions and Packages

Today we will go over how to create and utilize your own functions and then how to install and use pre-written functions from packages. You can find relevant readings in [Turrell](https://aeturrell.github.io/coding-for-economists/code-basics.html#writing-functions) and [McKinney](https://wesmckinney.com/book/python-builtin#functions).


```python
# You can create your own functions!
def km_to_miles(km):
    '''
    Convert kilometers to miles
    Input: 
        km (float): Distance in Kilometers
    Output:
        miles (float): Distance in Miles
    '''

    # 1 km = 0.621371 miles
    miles = km*0.621371

    # Use return to tell the function what to send back after being called
    return miles

race_km = 5
```


```python
# Test it out
print(km_to_miles(race_km))
```

    3.106855
    


```python
# See everything defined in your kernal
%whos
```

    Variable          Type             Data/Info
    --------------------------------------------
    NamespaceMagics   MetaHasTraits    <class 'IPython.core.magi<...>mespace.NamespaceMagics'>
    collections       module           <module 'collections' fro<...>ollections\\__init__.py'>
    get_ipython       function         <function get_ipython at 0x0000023383EE0EA0>
    islice            type             <class 'itertools.islice'>
    json              module           <module 'json' from 'C:\\<...>\Lib\\json\\__init__.py'>
    km_to_miles       function         <function km_to_miles at 0x00000233871C32E0>
    race_km           int              5
    sys               module           <module 'sys' (built-in)>
    


```python
# Introspection on user generated functions?
km_to_miles?
```


    [1;31mSignature:[0m [0mkm_to_miles[0m[1;33m([0m[0mkm[0m[1;33m)[0m[1;33m[0m[1;33m[0m[0m
    [1;31mDocstring:[0m
    Convert kilometers to miles
    Input: 
        km (float): Distance in Kilometers
    Output:
        miles (float): Distance in Miles
    [1;31mFile:[0m      c:\users\micha\appdata\local\temp\ipykernel_4416\354150623.py
    [1;31mType:[0m      function



```python
# Help?
help(km_to_miles)
```

    Help on function km_to_miles in module __main__:
    
    km_to_miles(km)
        Convert kilometers to miles
        Input:
            km (float): Distance in Kilometers
        Output:
            miles (float): Distance in Miles
    
    


```python
# Make use of it
race_miles = km_to_miles(race_km)
print("The race will be {:.2f} miles.".format(race_miles))
```

    The race will be 3.11 miles.
    


```python
# Testing no return
def test():
    a = 1
    b = 2
    a+b
    print(a)
```


```python
# What is it?
print(test())
type(test)
```

    None
    




    function




```python
# Scope?
test()
km_to_miles(5)
```

    1
    




    3.106855




```python
# Does it exist?
print(miles)
```


    ---------------------------------------------------------------------------

    NameError                                 Traceback (most recent call last)

    Cell In[27], line 2
          1 # Does it exist?
    ----> 2 print(miles)
    

    NameError: name 'miles' is not defined



```python
# Is it saved?
%whos
```

    Variable          Type             Data/Info
    --------------------------------------------
    NamespaceMagics   MetaHasTraits    <class 'IPython.core.magi<...>mespace.NamespaceMagics'>
    collections       module           <module 'collections' fro<...>ollections\\__init__.py'>
    get_ipython       function         <function get_ipython at 0x0000023383EE0EA0>
    islice            type             <class 'itertools.islice'>
    json              module           <module 'json' from 'C:\\<...>\Lib\\json\\__init__.py'>
    km_to_miles       function         <function km_to_miles at 0x00000233871C32E0>
    race_km           int              5
    race_miles        float            3.106855
    sys               module           <module 'sys' (built-in)>
    test              function         <function test at 0x0000023387F58F40>
    


```python
# Define another function
def city_state_fixer(city, state):
    '''
    Fix capitalization problems with cities and states, returning one string with the first letter of each word capitalized
    Input:
        city (str): String of city name
        state (str): String of state name
    Output:
        String with proper capitalization for city and state in "City, State"
    '''

    # The method "title" capitalizes the first letter but makes the rest lowercase
    return city.title() + ", " + state.title()
```


```python
# Test it out!
city_state_fixer("MADison", "wISCONSIN")
```




    'Madison, Wisconsin'




```python
# Name of inputs?
city_state_fixer(state = "WISCONSIN", city = "MADISON")
```




    'Madison, Wisconsin'




```python
# Do you HAVE to use both?
city_state_fixer()
```


    ---------------------------------------------------------------------------

    TypeError                                 Traceback (most recent call last)

    Cell In[34], line 2
          1 # Do you HAVE to use both?
    ----> 2 city_state_fixer()
    

    TypeError: city_state_fixer() missing 2 required positional arguments: 'city' and 'state'



```python
# Initializing variables
def city_state_fixer_v2(city="", state=""):
    '''
    Fix capitalization problems with cities and states, returning one string with the first letter of each word capitalized
    Input:
        city (str): String of city name
        state (str): String of state name
    Output:
        String with proper capitalization for city and state in "City, State"
    '''

    if city == "" or state == "":
        return city.title() + state.title()
    else:
        # The method "title" capitalizes the first letter but makes the rest lowercase
        return city.title() + ", " + state.title()
```


```python
# Testing it out again
city_state_fixer_v2(city="MADison")
```




    'Madison'




```python
# Still work?
city_state_fixer_v2(city="MADison", state="wISCONSIN")
```




    'Madison, Wisconsin'




```python
# Checking with state
city_state_fixer_v2(state="wISCONSIN")
```




    'Wisconsin'




```python
# Changing return type
def city_state_fixer_v3(city="", state=""):
    '''
    Fix capitalization problems with cities and states, returning one string with the first letter of each word capitalized
    Input:
        city (str): String of city name
        state (str): String of state name
    Output:
        City and State
    '''

    if city == "" or state == "":
        return city.title(), state.title()
    else:
        # The method "title" capitalizes the first letter but makes the rest lowercase
        return city.title(), state.title()
```


```python
# What does it look like now?
city_state_fixer_v3(city="MADison", state="wISCONSIN")
```




    ('Madison', 'Wisconsin')




```python
# Unpacking it
city1, state1 = city_state_fixer_v3(city="MADison", state="wISCONSIN")
print(city1, state1)
```

    Madison Wisconsin
    


```python
# What happens with incorrect types?
race_km = "5"
race_miles = km_to_miles(race_km)
```


    ---------------------------------------------------------------------------

    TypeError                                 Traceback (most recent call last)

    Cell In[51], line 3
          1 # What happens with incorrect types?
          2 race_km = "5"
    ----> 3 race_miles = km_to_miles(race_km)
    

    Cell In[6], line 12, in km_to_miles(km)
          3 '''
          4 Convert kilometers to miles
          5 Input: 
       (...)
          8     miles (float): Distance in Miles
          9 '''
         11 # 1 km = 0.621371 miles
    ---> 12 miles = km*0.621371
         14 # Use return to tell the function what to send back after being called
         15 return miles
    

    TypeError: can't multiply sequence by non-int of type 'float'



```python
# Manual warning
def km_to_miles_v2(km):
    '''
    Convert kilometers to miles, give a warning if they don't input a float/int
    Input: 
        km (float): Distance in Kilometers
    Output:
        miles (float): Distance in Miles
        or
        Print a warning if the input is of the wrong type
    '''

    if type(km) == float or type(km) == int:
        
        # 1 km = 0.621371 miles
        miles = km*0.621371

        # Use return to tell the function what to send back after being called
        return miles
    else:
        print('Warning: km_to_miles_v2 only takes ints or floats.')
        return -99
```


```python
# What happens with incorrect types?
race_miles = km_to_miles_v2(race_km)
print(race_miles)
```

    Warning: km_to_miles_v2 only takes ints or floats.
    -99
    


```python
# Try & Except
a = 10
b = 0
try:
    print(a/b)
except:
    print('WARNING: unable to divid {num} by {den}.'.format(num=a, den=b))

a/b
```

    WARNING: unable to divid 10 by 0.
    


    ---------------------------------------------------------------------------

    ZeroDivisionError                         Traceback (most recent call last)

    Cell In[57], line 9
          6 except:
          7     print('WARNING: unable to divid {num} by {den}.'.format(num=a, den=b))
    ----> 9 a/b
    

    ZeroDivisionError: division by zero



```python
# Making use in a function
def divide(a,b):
    '''

    '''
    try:
        print(a/b, end="")
    except TypeError:
        print('TypeError: unable to divide {num} by {den} due to type.'.format(num=a, den=b))
    except ZeroDivisionError:
        print('ZeroDivisionError: you cannot divide {num} by {den}.'.format(num=a, den=b))
    else:
        print(' --> Calculation succeeded')
```


```python
# Test it out!
divide(10,"0")
```

    TypeError: unable to divide10 by 0 due to type.
    

## Practice - Functions
1. Write a function called change_counting. Pass the function the number of pennies, nickels, dimes, and quarters and output the value of the coins in dollars.
2. Modify city_state_fixer_v3 to also return the length of the string of the city + state. Test it with "DETROIT" and "michigan", printing the city, state, and length of the sum.


```python
# Results
# 1.
def change_counting(pennies=0, nickels=0, dimes=0, quarters=0):
    '''
    Gives you the value of coins.
    '''
    return (pennies*1+nickels*5+dimes*10+quarters*25)/100
print(change_counting(pennies = 3, dimes = 2, quarters = 1))
# 2.
def city_state_fixer_v3(city="", state=""):
    '''
    Fix capitalization problems with cities and states, returning one string with the first letter of each word capitalized
    Input:
        city (str): String of city name
        state (str): String of state name
    Output:
        City and State
    '''

    if city == "" or state == "":
        return city.title(), state.title(), len(city+state)
    else:
        # The method "title" capitalizes the first letter but makes the rest lowercase
        return city.title(), state.title(), len(city+state)
print(city_state_fixer_v3("DETROIT"))
```

    0.48
    ('Detroit', '', 7)
    

## Packages


```python
# Functions we might expect
log(10)
```


    ---------------------------------------------------------------------------

    NameError                                 Traceback (most recent call last)

    Cell In[69], line 2
          1 # Functions we might expect
    ----> 2 log(10)
    

    NameError: name 'log' is not defined



```python
# Importing packages
import numpy as np
```


```python
# How does it show up?
%whos
```

    Variable              Type             Data/Info
    ------------------------------------------------
    NamespaceMagics       MetaHasTraits    <class 'IPython.core.magi<...>mespace.NamespaceMagics'>
    a                     int              10
    b                     int              0
    change_counting       function         <function change_counting at 0x0000023387296AC0>
    city1                 str              Madison
    city_state_fixer      function         <function city_state_fixer at 0x0000023387F593A0>
    city_state_fixer_v2   function         <function city_state_fixe<...>v2 at 0x0000023387FC5260>
    city_state_fixer_v3   function         <function city_state_fixe<...>v3 at 0x0000023384C0CA40>
    collections           module           <module 'collections' fro<...>ollections\\__init__.py'>
    divide                function         <function divide at 0x0000023387294E00>
    get_ipython           function         <function get_ipython at 0x0000023383EE0EA0>
    islice                type             <class 'itertools.islice'>
    json                  module           <module 'json' from 'C:\\<...>\Lib\\json\\__init__.py'>
    km_to_miles           function         <function km_to_miles at 0x00000233871C32E0>
    km_to_miles_v2        function         <function km_to_miles_v2 at 0x0000023387F5A020>
    np                    module           <module 'numpy' from 'C:\<...>ges\\numpy\\__init__.py'>
    race_km               str              5
    race_miles            int              -99
    state1                str              Wisconsin
    sys                   module           <module 'sys' (built-in)>
    test                  function         <function test at 0x0000023387F58F40>
    


```python
# Importing more and renaming
import os
```


```python
# Making use of it
print(np.log(10))
print(np.exp(10))
```

    2.302585092994046
    22026.465794806718
    


```python
# Importing specific functions
from numpy import pi, log as ln, exp
```


```python
# Now?
print(ln(10))
print(pi)
```

    2.302585092994046
    3.141592653589793
    


```python
# Tiny Dip into Regular Expression
import re

def city_state_fixer_v4(city= "", state = ""):
    city_no_symb = re.sub("[!#? ]", "", city)
    state_no_symb = re.sub("[!#? ]", "", state)

    return city_no_symb.title(), state_no_symb.title()        
```


```python
# Test it out
city_state_fixer_v4("MADison!", "?wiSCONSIN")
```




    ('Madison', 'Wisconsin')




```python
# Pandas!
import pandas as pd
```


```python
# Getting more and more stuff
%whos
```

    Variable              Type             Data/Info
    ------------------------------------------------
    NamespaceMagics       MetaHasTraits    <class 'IPython.core.magi<...>mespace.NamespaceMagics'>
    a                     int              10
    b                     int              0
    change_counting       function         <function change_counting at 0x0000023387296AC0>
    city1                 str              Madison
    city_state_fixer      function         <function city_state_fixer at 0x0000023387F593A0>
    city_state_fixer_v2   function         <function city_state_fixe<...>v2 at 0x0000023387FC5260>
    city_state_fixer_v3   function         <function city_state_fixe<...>v3 at 0x0000023384C0CA40>
    city_state_fixer_v4   function         <function city_state_fixe<...>v4 at 0x0000023387FC6980>
    collections           module           <module 'collections' fro<...>ollections\\__init__.py'>
    divide                function         <function divide at 0x0000023387294E00>
    exp                   ufunc            <ufunc 'exp'>
    get_ipython           function         <function get_ipython at 0x0000023383EE0EA0>
    islice                type             <class 'itertools.islice'>
    json                  module           <module 'json' from 'C:\\<...>\Lib\\json\\__init__.py'>
    km_to_miles           function         <function km_to_miles at 0x00000233871C32E0>
    km_to_miles_v2        function         <function km_to_miles_v2 at 0x0000023387F5A020>
    ln                    ufunc            <ufunc 'log'>
    np                    module           <module 'numpy' from 'C:\<...>ges\\numpy\\__init__.py'>
    os                    module           <module 'os' from 'C:\\Us<...>\\anaconda3\\Lib\\os.py'>
    pd                    module           <module 'pandas' from 'C:<...>es\\pandas\\__init__.py'>
    pi                    float            3.141592653589793
    race_km               str              5
    race_miles            int              -99
    re                    module           <module 're' from 'C:\\Us<...>3\\Lib\\re\\__init__.py'>
    state1                str              Wisconsin
    sys                   module           <module 'sys' (built-in)>
    test                  function         <function test at 0x0000023387F58F40>
    


```python
# Import everything from numpy
from numpy import *
```


```python
# Wow!
%whos
```

    Variable                  Type                          Data/Info
    -----------------------------------------------------------------
    False_                    bool                          False
    NamespaceMagics           MetaHasTraits                 <class 'IPython.core.magi<...>mespace.NamespaceMagics'>
    ScalarType                tuple                         n=31
    True_                     bool                          True
    a                         int                           10
    abs                       ufunc                         <ufunc 'absolute'>
    absolute                  ufunc                         <ufunc 'absolute'>
    acos                      ufunc                         <ufunc 'arccos'>
    acosh                     ufunc                         <ufunc 'arccosh'>
    add                       ufunc                         <ufunc 'add'>
    all                       _ArrayFunctionDispatcher      <function all at 0x00000233881D5EE0>
    allclose                  _ArrayFunctionDispatcher      <function allclose at 0x00000233881E5BC0>
    amax                      _ArrayFunctionDispatcher      <function amax at 0x00000233881D65C0>
    amin                      _ArrayFunctionDispatcher      <function amin at 0x00000233881D6840>
    angle                     _ArrayFunctionDispatcher      <function angle at 0x00000233883CEB60>
    any                       _ArrayFunctionDispatcher      <function any at 0x00000233881D5DA0>
    append                    _ArrayFunctionDispatcher      <function append at 0x00000233883D9940>
    apply_along_axis          _ArrayFunctionDispatcher      <function apply_along_axis at 0x00000233883E0A40>
    apply_over_axes           _ArrayFunctionDispatcher      <function apply_over_axes at 0x00000233883E0B80>
    arange                    builtin_function_or_method    <built-in function arange>
    arccos                    ufunc                         <ufunc 'arccos'>
    arccosh                   ufunc                         <ufunc 'arccosh'>
    arcsin                    ufunc                         <ufunc 'arcsin'>
    arcsinh                   ufunc                         <ufunc 'arcsinh'>
    arctan                    ufunc                         <ufunc 'arctan'>
    arctan2                   ufunc                         <ufunc 'arctan2'>
    arctanh                   ufunc                         <ufunc 'arctanh'>
    argmax                    _ArrayFunctionDispatcher      <function argmax at 0x00000233881D4D60>
    argmin                    _ArrayFunctionDispatcher      <function argmin at 0x00000233881D4EA0>
    argpartition              _ArrayFunctionDispatcher      <function argpartition at 0x00000233881D49A0>
    argsort                   _ArrayFunctionDispatcher      <function argsort at 0x00000233881D4C20>
    argwhere                  _ArrayFunctionDispatcher      <function argwhere at 0x00000233881E49A0>
    around                    _ArrayFunctionDispatcher      <function around at 0x00000233881D6F20>
    array                     builtin_function_or_method    <built-in function array>
    array2string              _ArrayFunctionDispatcher      <function array2string at 0x00000233881E71A0>
    array_equal               _ArrayFunctionDispatcher      <function array_equal at 0x00000233881E5EE0>
    array_equiv               _ArrayFunctionDispatcher      <function array_equiv at 0x00000233881E6020>
    array_repr                _ArrayFunctionDispatcher      <function array_repr at 0x00000233882047C0>
    array_split               _ArrayFunctionDispatcher      <function array_split at 0x00000233883E11C0>
    array_str                 _ArrayFunctionDispatcher      <function array_str at 0x0000023388204AE0>
    asanyarray                builtin_function_or_method    <built-in function asanyarray>
    asarray                   builtin_function_or_method    <built-in function asarray>
    asarray_chkfinite         function                      <function asarray_chkfini<...>te at 0x00000233883CE2A0>
    ascontiguousarray         builtin_function_or_method    <built-in function ascontiguousarray>
    asfortranarray            builtin_function_or_method    <built-in function asfortranarray>
    asin                      ufunc                         <ufunc 'arcsin'>
    asinh                     ufunc                         <ufunc 'arcsinh'>
    asmatrix                  function                      <function asmatrix at 0x00000233883523E0>
    astype                    _ArrayFunctionDispatcher      <function astype at 0x00000233881E6160>
    atan                      ufunc                         <ufunc 'arctan'>
    atan2                     ufunc                         <ufunc 'arctan2'>
    atanh                     ufunc                         <ufunc 'arctanh'>
    atleast_1d                _ArrayFunctionDispatcher      <function atleast_1d at 0x00000233881D7240>
    atleast_2d                _ArrayFunctionDispatcher      <function atleast_2d at 0x00000233881D7420>
    atleast_3d                _ArrayFunctionDispatcher      <function atleast_3d at 0x00000233881D7560>
    average                   _ArrayFunctionDispatcher      <function average at 0x00000233883CE200>
    b                         int                           0
    bartlett                  function                      <function bartlett at 0x00000233883CFEC0>
    base_repr                 function                      <function base_repr at 0x00000233881E5940>
    binary_repr               function                      <function binary_repr at 0x00000233881E58A0>
    bincount                  _ArrayFunctionDispatcher      <built-in function bincount>
    bitwise_and               ufunc                         <ufunc 'bitwise_and'>
    bitwise_count             ufunc                         <ufunc 'bitwise_count'>
    bitwise_invert            ufunc                         <ufunc 'invert'>
    bitwise_left_shift        ufunc                         <ufunc 'left_shift'>
    bitwise_not               ufunc                         <ufunc 'invert'>
    bitwise_or                ufunc                         <ufunc 'bitwise_or'>
    bitwise_right_shift       ufunc                         <ufunc 'right_shift'>
    bitwise_xor               ufunc                         <ufunc 'bitwise_xor'>
    blackman                  function                      <function blackman at 0x00000233883CFE20>
    block                     _ArrayFunctionDispatcher      <function block at 0x00000233881E4040>
    bmat                      function                      <function bmat at 0x00000233883B7D80>
    bool                      type                          <class 'numpy.bool'>
    bool_                     type                          <class 'numpy.bool'>
    broadcast                 type                          <class 'numpy.broadcast'>
    broadcast_arrays          _ArrayFunctionDispatcher      <function broadcast_arrays at 0x0000023388352160>
    broadcast_shapes          function                      <function broadcast_shapes at 0x0000023388352020>
    broadcast_to              _ArrayFunctionDispatcher      <function broadcast_to at 0x0000023388351EE0>
    busday_count              _ArrayFunctionDispatcher      <built-in function busday_count>
    busday_offset             _ArrayFunctionDispatcher      <built-in function busday_offset>
    busdaycalendar            type                          <class 'numpy.busdaycalendar'>
    byte                      type                          <class 'numpy.int8'>
    bytes_                    type                          <class 'numpy.bytes_'>
    c_                        CClass                        <numpy.lib._index_tricks_<...>ct at 0x00000233883D5F80>
    can_cast                  _ArrayFunctionDispatcher      <built-in function can_cast>
    cbrt                      ufunc                         <ufunc 'cbrt'>
    cdouble                   type                          <class 'numpy.complex128'>
    ceil                      ufunc                         <ufunc 'ceil'>
    change_counting           function                      <function change_counting at 0x0000023387296AC0>
    char                      module                        <module 'numpy.char' from<...>umpy\\char\\__init__.py'>
    character                 type                          <class 'numpy.character'>
    choose                    _ArrayFunctionDispatcher      <function choose at 0x00000233881D40E0>
    city1                     str                           Madison
    city_state_fixer          function                      <function city_state_fixer at 0x0000023387F593A0>
    city_state_fixer_v2       function                      <function city_state_fixe<...>v2 at 0x0000023387FC5260>
    city_state_fixer_v3       function                      <function city_state_fixe<...>v3 at 0x0000023384C0CA40>
    city_state_fixer_v4       function                      <function city_state_fixe<...>v4 at 0x0000023387FC6980>
    clip                      _ArrayFunctionDispatcher      <function clip at 0x00000233881D5B20>
    clongdouble               type                          <class 'numpy.clongdouble'>
    collections               module                        <module 'collections' fro<...>ollections\\__init__.py'>
    column_stack              _ArrayFunctionDispatcher      <function column_stack at 0x00000233883E0EA0>
    common_type               _ArrayFunctionDispatcher      <function common_type at 0x0000023388350F40>
    complex128                type                          <class 'numpy.complex128'>
    complex64                 type                          <class 'numpy.complex64'>
    complexfloating           type                          <class 'numpy.complexfloating'>
    compress                  _ArrayFunctionDispatcher      <function compress at 0x00000233881D59E0>
    concat                    _ArrayFunctionDispatcher      <built-in function concatenate>
    concatenate               _ArrayFunctionDispatcher      <built-in function concatenate>
    conj                      ufunc                         <ufunc 'conjugate'>
    conjugate                 ufunc                         <ufunc 'conjugate'>
    convolve                  _ArrayFunctionDispatcher      <function convolve at 0x00000233881E4D60>
    copy                      _ArrayFunctionDispatcher      <function copy at 0x00000233883CE660>
    copysign                  ufunc                         <ufunc 'copysign'>
    copyto                    _ArrayFunctionDispatcher      <built-in function copyto>
    core                      module                        <module 'numpy.core' from<...>umpy\\core\\__init__.py'>
    corrcoef                  _ArrayFunctionDispatcher      <function corrcoef at 0x00000233883CFD80>
    correlate                 _ArrayFunctionDispatcher      <function correlate at 0x00000233881E4C20>
    cos                       ufunc                         <ufunc 'cos'>
    cosh                      ufunc                         <ufunc 'cosh'>
    count_nonzero             _ArrayFunctionDispatcher      <function count_nonzero at 0x00000233881E47C0>
    cov                       _ArrayFunctionDispatcher      <function cov at 0x00000233883CFC40>
    cross                     _ArrayFunctionDispatcher      <function cross at 0x00000233881E5580>
    csingle                   type                          <class 'numpy.complex64'>
    ctypeslib                 module                        <module 'numpy.ctypeslib'<...>es\\numpy\\ctypeslib.py'>
    cumprod                   _ArrayFunctionDispatcher      <function cumprod at 0x00000233881D6AC0>
    cumsum                    _ArrayFunctionDispatcher      <function cumsum at 0x00000233881D6340>
    cumulative_prod           _ArrayFunctionDispatcher      <function cumulative_prod at 0x00000233881D60C0>
    cumulative_sum            _ArrayFunctionDispatcher      <function cumulative_sum at 0x00000233881D6200>
    datetime64                type                          <class 'numpy.datetime64'>
    datetime_as_string        _ArrayFunctionDispatcher      <built-in function datetime_as_string>
    datetime_data             builtin_function_or_method    <built-in function datetime_data>
    deg2rad                   ufunc                         <ufunc 'deg2rad'>
    degrees                   ufunc                         <ufunc 'degrees'>
    delete                    _ArrayFunctionDispatcher      <function delete at 0x00000233883D96C0>
    diag                      _ArrayFunctionDispatcher      <function diag at 0x0000023388353240>
    diag_indices              function                      <function diag_indices at 0x00000233883DA8E0>
    diag_indices_from         _ArrayFunctionDispatcher      <function diag_indices_fr<...>om at 0x00000233883DAA20>
    diagflat                  _ArrayFunctionDispatcher      <function diagflat at 0x00000233883532E0>
    diagonal                  _ArrayFunctionDispatcher      <function diagonal at 0x00000233881D53A0>
    diff                      _ArrayFunctionDispatcher      <function diff at 0x00000233883CE8E0>
    digitize                  _ArrayFunctionDispatcher      <function digitize at 0x00000233883D9A80>
    divide                    ufunc                         <ufunc 'divide'>
    divmod                    ufunc                         <ufunc 'divmod'>
    dot                       _ArrayFunctionDispatcher      <built-in function dot>
    double                    type                          <class 'numpy.float64'>
    dsplit                    _ArrayFunctionDispatcher      <function dsplit at 0x00000233883E1620>
    dstack                    _ArrayFunctionDispatcher      <function dstack at 0x00000233883E0FE0>
    dtype                     _DTypeMeta                    <class 'numpy.dtype'>
    dtypes                    module                        <module 'numpy.dtypes' fr<...>kages\\numpy\\dtypes.py'>
    e                         float                         2.718281828459045
    ediff1d                   _ArrayFunctionDispatcher      <function ediff1d at 0x00000233883E1BC0>
    einsum                    _ArrayFunctionDispatcher      <function einsum at 0x00000233882E04A0>
    einsum_path               _ArrayFunctionDispatcher      <function einsum_path at 0x00000233882E0360>
    emath                     module                        <module 'numpy.lib.scimat<...>\numpy\\lib\\scimath.py'>
    empty                     builtin_function_or_method    <built-in function empty>
    empty_like                _ArrayFunctionDispatcher      <built-in function empty_like>
    equal                     ufunc                         <ufunc 'equal'>
    errstate                  type                          <class 'numpy.errstate'>
    euler_gamma               float                         0.5772156649015329
    exceptions                module                        <module 'numpy.exceptions<...>s\\numpy\\exceptions.py'>
    exp                       ufunc                         <ufunc 'exp'>
    exp2                      ufunc                         <ufunc 'exp2'>
    expand_dims               _ArrayFunctionDispatcher      <function expand_dims at 0x00000233883E0CC0>
    expm1                     ufunc                         <ufunc 'expm1'>
    extract                   _ArrayFunctionDispatcher      <function extract at 0x00000233883CF060>
    eye                       function                      <function eye at 0x0000023388353100>
    f2py                      module                        <module 'numpy.f2py' from<...>umpy\\f2py\\__init__.py'>
    fabs                      ufunc                         <ufunc 'fabs'>
    fft                       module                        <module 'numpy.fft' from <...>numpy\\fft\\__init__.py'>
    fill_diagonal             _ArrayFunctionDispatcher      <function fill_diagonal at 0x00000233883DA840>
    finfo                     type                          <class 'numpy.finfo'>
    fix                       _ArrayFunctionDispatcher      <function fix at 0x0000023388350400>
    flatiter                  type                          <class 'numpy.flatiter'>
    flatnonzero               _ArrayFunctionDispatcher      <function flatnonzero at 0x00000233881E4AE0>
    flexible                  type                          <class 'numpy.flexible'>
    flip                      _ArrayFunctionDispatcher      <function flip at 0x00000233883CDF80>
    fliplr                    _ArrayFunctionDispatcher      <function fliplr at 0x0000023388352FC0>
    flipud                    _ArrayFunctionDispatcher      <function flipud at 0x0000023388353060>
    float16                   type                          <class 'numpy.float16'>
    float32                   type                          <class 'numpy.float32'>
    float64                   type                          <class 'numpy.float64'>
    float_power               ufunc                         <ufunc 'float_power'>
    floating                  type                          <class 'numpy.floating'>
    floor                     ufunc                         <ufunc 'floor'>
    floor_divide              ufunc                         <ufunc 'floor_divide'>
    fmax                      ufunc                         <ufunc 'fmax'>
    fmin                      ufunc                         <ufunc 'fmin'>
    fmod                      ufunc                         <ufunc 'fmod'>
    format_float_positional   function                      <function format_float_po<...>al at 0x00000233881E7740>
    format_float_scientific   function                      <function format_float_sc<...>ic at 0x00000233881E76A0>
    frexp                     ufunc                         <ufunc 'frexp'>
    from_dlpack               builtin_function_or_method    <built-in function from_dlpack>
    frombuffer                builtin_function_or_method    <built-in function frombuffer>
    fromfile                  builtin_function_or_method    <built-in function fromfile>
    fromfunction              function                      <function fromfunction at 0x00000233881E56C0>
    fromiter                  builtin_function_or_method    <built-in function fromiter>
    frompyfunc                builtin_function_or_method    <built-in function frompyfunc>
    fromregex                 function                      <function fromregex at 0x0000023388333BA0>
    fromstring                builtin_function_or_method    <built-in function fromstring>
    full                      function                      <function full at 0x00000233881E4540>
    full_like                 _ArrayFunctionDispatcher      <function full_like at 0x00000233881E4680>
    gcd                       ufunc                         <ufunc 'gcd'>
    generic                   type                          <class 'numpy.generic'>
    genfromtxt                function                      <function genfromtxt at 0x0000023388333C40>
    geomspace                 _ArrayFunctionDispatcher      <function geomspace at 0x0000023388206480>
    get_include               function                      <function get_include at 0x000002338831EC00>
    get_ipython               function                      <function get_ipython at 0x0000023383EE0EA0>
    get_printoptions          function                      <function get_printoptions at 0x00000233881E68E0>
    getbufsize                function                      <function getbufsize at 0x00000233881B2DE0>
    geterr                    function                      <function geterr at 0x00000233881B2CA0>
    geterrcall                function                      <function geterrcall at 0x00000233881B2F20>
    gradient                  _ArrayFunctionDispatcher      <function gradient at 0x00000233883CE7A0>
    greater                   ufunc                         <ufunc 'greater'>
    greater_equal             ufunc                         <ufunc 'greater_equal'>
    half                      type                          <class 'numpy.float16'>
    hamming                   function                      <function hamming at 0x00000233883D8040>
    hanning                   function                      <function hanning at 0x00000233883CFF60>
    heaviside                 ufunc                         <ufunc 'heaviside'>
    histogram                 _ArrayFunctionDispatcher      <function histogram at 0x00000233883CCFE0>
    histogram2d               _ArrayFunctionDispatcher      <function histogram2d at 0x00000233883537E0>
    histogram_bin_edges       _ArrayFunctionDispatcher      <function histogram_bin_e<...>es at 0x00000233883CCEA0>
    histogramdd               _ArrayFunctionDispatcher      <function histogramdd at 0x00000233883CD120>
    hsplit                    _ArrayFunctionDispatcher      <function hsplit at 0x00000233883E14E0>
    hstack                    _ArrayFunctionDispatcher      <function hstack at 0x00000233881D77E0>
    hypot                     ufunc                         <ufunc 'hypot'>
    i0                        _ArrayFunctionDispatcher      <function i0 at 0x00000233883D8360>
    identity                  function                      <function identity at 0x00000233881E5A80>
    iinfo                     type                          <class 'numpy.iinfo'>
    imag                      _ArrayFunctionDispatcher      <function imag at 0x0000023388350720>
    in1d                      _ArrayFunctionDispatcher      <function in1d at 0x00000233883E3240>
    index_exp                 IndexExpression               <numpy.lib._index_tricks_<...>ct at 0x00000233883C70A0>
    indices                   function                      <function indices at 0x00000233881E5620>
    inexact                   type                          <class 'numpy.inexact'>
    inf                       float                         inf
    info                      function                      <function info at 0x000002338831F1A0>
    inner                     _ArrayFunctionDispatcher      <built-in function inner>
    insert                    _ArrayFunctionDispatcher      <function insert at 0x00000233883D9800>
    int16                     type                          <class 'numpy.int16'>
    int32                     type                          <class 'numpy.int32'>
    int64                     type                          <class 'numpy.int64'>
    int8                      type                          <class 'numpy.int8'>
    int_                      type                          <class 'numpy.int64'>
    intc                      type                          <class 'numpy.intc'>
    integer                   type                          <class 'numpy.integer'>
    interp                    _ArrayFunctionDispatcher      <function interp at 0x00000233883CEA20>
    intersect1d               _ArrayFunctionDispatcher      <function intersect1d at 0x00000233883E2FC0>
    intp                      type                          <class 'numpy.int64'>
    invert                    ufunc                         <ufunc 'invert'>
    is_busday                 _ArrayFunctionDispatcher      <built-in function is_busday>
    isclose                   _ArrayFunctionDispatcher      <function isclose at 0x00000233881E5D00>
    iscomplex                 _ArrayFunctionDispatcher      <function iscomplex at 0x0000023388350860>
    iscomplexobj              _ArrayFunctionDispatcher      <function iscomplexobj at 0x00000233883509A0>
    isdtype                   function                      <function isdtype at 0x00000233881B1E40>
    isfinite                  ufunc                         <ufunc 'isfinite'>
    isfortran                 function                      <function isfortran at 0x00000233881E4860>
    isin                      _ArrayFunctionDispatcher      <function isin at 0x00000233883E3420>
    isinf                     ufunc                         <ufunc 'isinf'>
    islice                    type                          <class 'itertools.islice'>
    isnan                     ufunc                         <ufunc 'isnan'>
    isnat                     ufunc                         <ufunc 'isnat'>
    isneginf                  _ArrayFunctionDispatcher      <function isneginf at 0x0000023388350540>
    isposinf                  _ArrayFunctionDispatcher      <function isposinf at 0x00000233883504A0>
    isreal                    _ArrayFunctionDispatcher      <function isreal at 0x0000023388350900>
    isrealobj                 _ArrayFunctionDispatcher      <function isrealobj at 0x0000023388350A40>
    isscalar                  function                      <function isscalar at 0x00000233881E5800>
    issubdtype                function                      <function issubdtype at 0x00000233881B1EE0>
    iterable                  function                      <function iterable at 0x00000233883CE020>
    ix_                       _ArrayFunctionDispatcher      <function ix_ at 0x00000233883D99E0>
    json                      module                        <module 'json' from 'C:\\<...>\Lib\\json\\__init__.py'>
    kaiser                    function                      <function kaiser at 0x00000233883D8400>
    km_to_miles               function                      <function km_to_miles at 0x00000233871C32E0>
    km_to_miles_v2            function                      <function km_to_miles_v2 at 0x0000023387F5A020>
    kron                      _ArrayFunctionDispatcher      <function kron at 0x00000233883E1800>
    lcm                       ufunc                         <ufunc 'lcm'>
    ldexp                     ufunc                         <ufunc 'ldexp'>
    left_shift                ufunc                         <ufunc 'left_shift'>
    less                      ufunc                         <ufunc 'less'>
    less_equal                ufunc                         <ufunc 'less_equal'>
    lexsort                   _ArrayFunctionDispatcher      <built-in function lexsort>
    lib                       module                        <module 'numpy.lib' from <...>numpy\\lib\\__init__.py'>
    linalg                    module                        <module 'numpy.linalg' fr<...>py\\linalg\\__init__.py'>
    linspace                  _ArrayFunctionDispatcher      <function linspace at 0x0000023388206200>
    little_endian             bool                          True
    ln                        ufunc                         <ufunc 'log'>
    load                      function                      <function load at 0x00000233883328E0>
    loadtxt                   function                      <function loadtxt at 0x00000233883339C0>
    log                       ufunc                         <ufunc 'log'>
    log10                     ufunc                         <ufunc 'log10'>
    log1p                     ufunc                         <ufunc 'log1p'>
    log2                      ufunc                         <ufunc 'log2'>
    logaddexp                 ufunc                         <ufunc 'logaddexp'>
    logaddexp2                ufunc                         <ufunc 'logaddexp2'>
    logical_and               ufunc                         <ufunc 'logical_and'>
    logical_not               ufunc                         <ufunc 'logical_not'>
    logical_or                ufunc                         <ufunc 'logical_or'>
    logical_xor               ufunc                         <ufunc 'logical_xor'>
    logspace                  _ArrayFunctionDispatcher      <function logspace at 0x0000023388206340>
    long                      type                          <class 'numpy.int32'>
    longdouble                type                          <class 'numpy.longdouble'>
    longlong                  type                          <class 'numpy.int64'>
    ma                        module                        <module 'numpy.ma' from '<...>\numpy\\ma\\__init__.py'>
    mask_indices              function                      <function mask_indices at 0x0000023388353880>
    matmul                    ufunc                         <ufunc 'matmul'>
    matrix                    type                          <class 'numpy.matrix'>
    matrix_transpose          _ArrayFunctionDispatcher      <function matrix_transpose at 0x00000233881D4720>
    max                       _ArrayFunctionDispatcher      <function max at 0x00000233881D6660>
    maximum                   ufunc                         <ufunc 'maximum'>
    may_share_memory          _ArrayFunctionDispatcher      <built-in function may_share_memory>
    mean                      _ArrayFunctionDispatcher      <function mean at 0x00000233881D7060>
    median                    _ArrayFunctionDispatcher      <function median at 0x00000233883D8720>
    memmap                    type                          <class 'numpy.memmap'>
    meshgrid                  _ArrayFunctionDispatcher      <function meshgrid at 0x00000233883D9580>
    mgrid                     MGridClass                    <numpy.lib._index_tricks_<...>ct at 0x00000233883C6F80>
    min                       _ArrayFunctionDispatcher      <function min at 0x00000233881D67A0>
    min_scalar_type           _ArrayFunctionDispatcher      <built-in function min_scalar_type>
    minimum                   ufunc                         <ufunc 'minimum'>
    mintypecode               function                      <function mintypecode at 0x0000023388350220>
    mod                       ufunc                         <ufunc 'remainder'>
    modf                      ufunc                         <ufunc 'modf'>
    moveaxis                  _ArrayFunctionDispatcher      <function moveaxis at 0x00000233881E5440>
    multiply                  ufunc                         <ufunc 'multiply'>
    nan                       float                         nan
    nan_to_num                _ArrayFunctionDispatcher      <function nan_to_num at 0x0000023388350C20>
    nanargmax                 _ArrayFunctionDispatcher      <function nanargmax at 0x00000233883DB420>
    nanargmin                 _ArrayFunctionDispatcher      <function nanargmin at 0x00000233883DB2E0>
    nancumprod                _ArrayFunctionDispatcher      <function nancumprod at 0x00000233883DB920>
    nancumsum                 _ArrayFunctionDispatcher      <function nancumsum at 0x00000233883DB7E0>
    nanmax                    _ArrayFunctionDispatcher      <function nanmax at 0x00000233883DB1A0>
    nanmean                   _ArrayFunctionDispatcher      <function nanmean at 0x00000233883DBA60>
    nanmedian                 _ArrayFunctionDispatcher      <function nanmedian at 0x00000233883DBD80>
    nanmin                    _ArrayFunctionDispatcher      <function nanmin at 0x00000233883DB060>
    nanpercentile             _ArrayFunctionDispatcher      <function nanpercentile at 0x00000233883DBEC0>
    nanprod                   _ArrayFunctionDispatcher      <function nanprod at 0x00000233883DB6A0>
    nanquantile               _ArrayFunctionDispatcher      <function nanquantile at 0x00000233883E0040>
    nanstd                    _ArrayFunctionDispatcher      <function nanstd at 0x00000233883E04A0>
    nansum                    _ArrayFunctionDispatcher      <function nansum at 0x00000233883DB560>
    nanvar                    _ArrayFunctionDispatcher      <function nanvar at 0x00000233883E0360>
    ndarray                   type                          <class 'numpy.ndarray'>
    ndenumerate               type                          <class 'numpy.ndenumerate'>
    ndim                      _ArrayFunctionDispatcher      <function ndim at 0x00000233881D6C00>
    ndindex                   type                          <class 'numpy.ndindex'>
    nditer                    type                          <class 'numpy.nditer'>
    negative                  ufunc                         <ufunc 'negative'>
    nested_iters              builtin_function_or_method    <built-in function nested_iters>
    newaxis                   NoneType                      None
    nextafter                 ufunc                         <ufunc 'nextafter'>
    nonzero                   _ArrayFunctionDispatcher      <function nonzero at 0x00000233881D5760>
    not_equal                 ufunc                         <ufunc 'not_equal'>
    np                        module                        <module 'numpy' from 'C:\<...>ges\\numpy\\__init__.py'>
    number                    type                          <class 'numpy.number'>
    object_                   type                          <class 'numpy.object_'>
    ogrid                     OGridClass                    <numpy.lib._index_tricks_<...>ct at 0x00000233883C6EF0>
    ones                      function                      <function ones at 0x00000233881E42C0>
    ones_like                 _ArrayFunctionDispatcher      <function ones_like at 0x00000233881E4400>
    os                        module                        <module 'os' from 'C:\\Us<...>\\anaconda3\\Lib\\os.py'>
    outer                     _ArrayFunctionDispatcher      <function outer at 0x00000233881E4EA0>
    packbits                  _ArrayFunctionDispatcher      <built-in function packbits>
    pad                       _ArrayFunctionDispatcher      <function pad at 0x0000023388406700>
    partition                 _ArrayFunctionDispatcher      <function partition at 0x00000233881D4860>
    pd                        module                        <module 'pandas' from 'C:<...>es\\pandas\\__init__.py'>
    percentile                _ArrayFunctionDispatcher      <function percentile at 0x00000233883D8900>
    permute_dims              _ArrayFunctionDispatcher      <function transpose at 0x00000233881D45E0>
    pi                        float                         3.141592653589793
    piecewise                 _ArrayFunctionDispatcher      <function piecewise at 0x00000233883CE3E0>
    place                     _ArrayFunctionDispatcher      <function place at 0x00000233883CF1A0>
    poly                      _ArrayFunctionDispatcher      <function poly at 0x00000233883E3920>
    poly1d                    type                          <class 'numpy.poly1d'>
    polyadd                   _ArrayFunctionDispatcher      <function polyadd at 0x00000233884040E0>
    polyder                   _ArrayFunctionDispatcher      <function polyder at 0x00000233883E3CE0>
    polydiv                   _ArrayFunctionDispatcher      <function polydiv at 0x0000023388404360>
    polyfit                   _ArrayFunctionDispatcher      <function polyfit at 0x00000233883E3E20>
    polyint                   _ArrayFunctionDispatcher      <function polyint at 0x00000233883E3BA0>
    polymul                   _ArrayFunctionDispatcher      <function polymul at 0x0000023388404220>
    polynomial                module                        <module 'numpy.polynomial<...>polynomial\\__init__.py'>
    polysub                   _ArrayFunctionDispatcher      <function polysub at 0x0000023388404180>
    polyval                   _ArrayFunctionDispatcher      <function polyval at 0x00000233883E3F60>
    positive                  ufunc                         <ufunc 'positive'>
    pow                       ufunc                         <ufunc 'power'>
    power                     ufunc                         <ufunc 'power'>
    printoptions              function                      <function printoptions at 0x00000233881E6AC0>
    prod                      _ArrayFunctionDispatcher      <function prod at 0x00000233881D6980>
    promote_types             builtin_function_or_method    <built-in function promote_types>
    ptp                       _ArrayFunctionDispatcher      <function ptp at 0x00000233881D6480>
    put                       _ArrayFunctionDispatcher      <function put at 0x00000233881D4360>
    put_along_axis            _ArrayFunctionDispatcher      <function put_along_axis at 0x00000233883E0900>
    putmask                   _ArrayFunctionDispatcher      <built-in function putmask>
    quantile                  _ArrayFunctionDispatcher      <function quantile at 0x00000233883D8A40>
    r_                        RClass                        <numpy.lib._index_tricks_<...>ct at 0x00000233883D5F40>
    race_km                   str                           5
    race_miles                int                           -99
    rad2deg                   ufunc                         <ufunc 'rad2deg'>
    radians                   ufunc                         <ufunc 'radians'>
    random                    module                        <module 'numpy.random' fr<...>py\\random\\__init__.py'>
    ravel                     _ArrayFunctionDispatcher      <function ravel at 0x00000233881D5620>
    ravel_multi_index         _ArrayFunctionDispatcher      <built-in function ravel_multi_index>
    re                        module                        <module 're' from 'C:\\Us<...>3\\Lib\\re\\__init__.py'>
    real                      _ArrayFunctionDispatcher      <function real at 0x00000233883505E0>
    real_if_close             _ArrayFunctionDispatcher      <function real_if_close at 0x0000023388350D60>
    rec                       module                        <module 'numpy.rec' from <...>numpy\\rec\\__init__.py'>
    recarray                  type                          <class 'numpy.rec.recarray'>
    reciprocal                ufunc                         <ufunc 'reciprocal'>
    record                    type                          <class 'numpy.record'>
    remainder                 ufunc                         <ufunc 'remainder'>
    repeat                    _ArrayFunctionDispatcher      <function repeat at 0x00000233881D4220>
    require                   function                      <function require at 0x0000023388204C20>
    reshape                   _ArrayFunctionDispatcher      <function reshape at 0x00000233881B3F60>
    resize                    _ArrayFunctionDispatcher      <function resize at 0x00000233881D5120>
    result_type               _ArrayFunctionDispatcher      <built-in function result_type>
    right_shift               ufunc                         <ufunc 'right_shift'>
    rint                      ufunc                         <ufunc 'rint'>
    roll                      _ArrayFunctionDispatcher      <function roll at 0x00000233881E5120>
    rollaxis                  _ArrayFunctionDispatcher      <function rollaxis at 0x00000233881E5260>
    roots                     _ArrayFunctionDispatcher      <function roots at 0x00000233883E3A60>
    rot90                     _ArrayFunctionDispatcher      <function rot90 at 0x00000233883CDE40>
    round                     _ArrayFunctionDispatcher      <function round at 0x00000233881D6E80>
    row_stack                 function                      <function row_stack at 0x00000233883E0D60>
    s_                        IndexExpression               <numpy.lib._index_tricks_<...>ct at 0x00000233883C7100>
    save                      _ArrayFunctionDispatcher      <function save at 0x00000233883332E0>
    savetxt                   _ArrayFunctionDispatcher      <function savetxt at 0x0000023388333B00>
    savez                     _ArrayFunctionDispatcher      <function savez at 0x0000023388333420>
    savez_compressed          _ArrayFunctionDispatcher      <function savez_compressed at 0x0000023388333560>
    sctypeDict                dict                          n=50
    searchsorted              _ArrayFunctionDispatcher      <function searchsorted at 0x00000233881D4FE0>
    select                    _ArrayFunctionDispatcher      <function select at 0x00000233883CE520>
    set_printoptions          function                      <function set_printoptions at 0x00000233881E67A0>
    setbufsize                function                      <function setbufsize at 0x00000233881B2D40>
    setdiff1d                 _ArrayFunctionDispatcher      <function setdiff1d at 0x00000233883E36A0>
    seterr                    function                      <function seterr at 0x00000233881B2C00>
    seterrcall                function                      <function seterrcall at 0x00000233881B2E80>
    setxor1d                  _ArrayFunctionDispatcher      <function setxor1d at 0x00000233883E3100>
    shape                     _ArrayFunctionDispatcher      <function shape at 0x00000233881D58A0>
    shares_memory             _ArrayFunctionDispatcher      <built-in function shares_memory>
    short                     type                          <class 'numpy.int16'>
    show_config               function                      <function show at 0x00000233880AC9A0>
    show_runtime              function                      <function show_runtime at 0x000002338831EB60>
    sign                      ufunc                         <ufunc 'sign'>
    signbit                   ufunc                         <ufunc 'signbit'>
    signedinteger             type                          <class 'numpy.signedinteger'>
    sin                       ufunc                         <ufunc 'sin'>
    sinc                      _ArrayFunctionDispatcher      <function sinc at 0x00000233883D8540>
    single                    type                          <class 'numpy.float32'>
    sinh                      ufunc                         <ufunc 'sinh'>
    size                      _ArrayFunctionDispatcher      <function size at 0x00000233881D6D40>
    sort                      _ArrayFunctionDispatcher      <function sort at 0x00000233881D4AE0>
    sort_complex              _ArrayFunctionDispatcher      <function sort_complex at 0x00000233883CEDE0>
    spacing                   ufunc                         <ufunc 'spacing'>
    split                     _ArrayFunctionDispatcher      <function split at 0x00000233883E13A0>
    sqrt                      ufunc                         <ufunc 'sqrt'>
    square                    ufunc                         <ufunc 'square'>
    squeeze                   _ArrayFunctionDispatcher      <function squeeze at 0x00000233881D5260>
    stack                     _ArrayFunctionDispatcher      <function stack at 0x00000233881D7920>
    state1                    str                           Wisconsin
    std                       _ArrayFunctionDispatcher      <function std at 0x00000233881D71A0>
    str_                      type                          <class 'numpy.str_'>
    strings                   module                        <module 'numpy.strings' f<...>y\\strings\\__init__.py'>
    subtract                  ufunc                         <ufunc 'subtract'>
    sum                       _ArrayFunctionDispatcher      <function sum at 0x00000233881D5C60>
    swapaxes                  _ArrayFunctionDispatcher      <function swapaxes at 0x00000233881D44A0>
    sys                       module                        <module 'sys' (built-in)>
    take                      _ArrayFunctionDispatcher      <function take at 0x00000233881B3E20>
    take_along_axis           _ArrayFunctionDispatcher      <function take_along_axis at 0x00000233883E07C0>
    tan                       ufunc                         <ufunc 'tan'>
    tanh                      ufunc                         <ufunc 'tanh'>
    tensordot                 _ArrayFunctionDispatcher      <function tensordot at 0x00000233881E4FE0>
    test                      PytestTester                  <numpy._pytesttester.Pyte<...>ct at 0x00000233880AAEA0>
    testing                   module                        <module 'numpy.testing' f<...>y\\testing\\__init__.py'>
    tile                      _ArrayFunctionDispatcher      <function tile at 0x00000233883E1940>
    timedelta64               type                          <class 'numpy.timedelta64'>
    trace                     _ArrayFunctionDispatcher      <function trace at 0x00000233881D54E0>
    transpose                 _ArrayFunctionDispatcher      <function transpose at 0x00000233881D45E0>
    trapezoid                 _ArrayFunctionDispatcher      <function trapezoid at 0x00000233883D93A0>
    trapz                     function                      <function trapz at 0x00000233883D9440>
    tri                       function                      <function tri at 0x0000023388353380>
    tril                      _ArrayFunctionDispatcher      <function tril at 0x00000233883534C0>
    tril_indices              function                      <function tril_indices at 0x0000023388353920>
    tril_indices_from         _ArrayFunctionDispatcher      <function tril_indices_fr<...>om at 0x0000023388353A60>
    trim_zeros                _ArrayFunctionDispatcher      <function trim_zeros at 0x00000233883CEF20>
    triu                      _ArrayFunctionDispatcher      <function triu at 0x0000023388353560>
    triu_indices              function                      <function triu_indices at 0x0000023388353B00>
    triu_indices_from         _ArrayFunctionDispatcher      <function triu_indices_fr<...>om at 0x0000023388353BA0>
    true_divide               ufunc                         <ufunc 'divide'>
    trunc                     ufunc                         <ufunc 'trunc'>
    typecodes                 dict                          n=9
    typename                  function                      <function typename at 0x0000023388350E00>
    typing                    module                        <module 'numpy.typing' fr<...>py\\typing\\__init__.py'>
    ubyte                     type                          <class 'numpy.uint8'>
    ufunc                     type                          <class 'numpy.ufunc'>
    uint                      type                          <class 'numpy.uint64'>
    uint16                    type                          <class 'numpy.uint16'>
    uint32                    type                          <class 'numpy.uint32'>
    uint64                    type                          <class 'numpy.uint64'>
    uint8                     type                          <class 'numpy.uint8'>
    uintc                     type                          <class 'numpy.uintc'>
    uintp                     type                          <class 'numpy.uint64'>
    ulong                     type                          <class 'numpy.uint32'>
    ulonglong                 type                          <class 'numpy.uint64'>
    union1d                   _ArrayFunctionDispatcher      <function union1d at 0x00000233883E3560>
    unique                    _ArrayFunctionDispatcher      <function unique at 0x00000233883E1DA0>
    unique_all                _ArrayFunctionDispatcher      <function unique_all at 0x00000233883E2AC0>
    unique_counts             _ArrayFunctionDispatcher      <function unique_counts at 0x00000233883E2C00>
    unique_inverse            _ArrayFunctionDispatcher      <function unique_inverse at 0x00000233883E2D40>
    unique_values             _ArrayFunctionDispatcher      <function unique_values at 0x00000233883E2E80>
    unpackbits                _ArrayFunctionDispatcher      <built-in function unpackbits>
    unravel_index             _ArrayFunctionDispatcher      <built-in function unravel_index>
    unsignedinteger           type                          <class 'numpy.unsignedinteger'>
    unstack                   _ArrayFunctionDispatcher      <function unstack at 0x00000233881D7A60>
    unwrap                    _ArrayFunctionDispatcher      <function unwrap at 0x00000233883CECA0>
    ushort                    type                          <class 'numpy.uint16'>
    vander                    _ArrayFunctionDispatcher      <function vander at 0x00000233883536A0>
    var                       _ArrayFunctionDispatcher      <function var at 0x00000233881D72E0>
    vdot                      _ArrayFunctionDispatcher      <built-in function vdot>
    vecdot                    ufunc                         <ufunc 'vecdot'>
    vectorize                 type                          <class 'numpy.vectorize'>
    void                      type                          <class 'numpy.void'>
    vsplit                    _ArrayFunctionDispatcher      <function vsplit at 0x00000233883E1580>
    vstack                    _ArrayFunctionDispatcher      <function vstack at 0x00000233881D7740>
    where                     _ArrayFunctionDispatcher      <built-in function where>
    zeros                     builtin_function_or_method    <built-in function zeros>
    zeros_like                _ArrayFunctionDispatcher      <function zeros_like at 0x00000233881E4220>
    
