---
layout: single
sitemap: false
permalink: /pages/Econ_390_SP26_L9_teaching/
---

[Download Jupyter Notebook Empty](https://m-mcmain.github.io/files/Econ390SP26/Lectures/Lecture9_Functions_empty.ipynb)

Download Jupyter Notebook Completed

# Econ 390 - Lecture 9: Functions and Packages

Today we will go over how to create and utilize your own functions and then how to install and use pre-written functions from packages. You can find relevant readings in [Turrell](https://aeturrell.github.io/coding-for-economists/code-basics.html#writing-functions) and [McKinney](https://wesmckinney.com/book/python-builtin#functions).


```python
# You can create your own functions!
def km_to_miles(km):
    '''
    Converts kilometers to miles
    '''
    
    # 1 km = 0.621371 miles
    miles = km*0.621371

    # Use return to tell the function what to send back after being called
    return miles

race_km = 5
```


```python
# Test it out
km_to_miles(race_km)
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
    get_ipython       function         <function get_ipython at 0x000001F351130E00>
    islice            type             <class 'itertools.islice'>
    json              module           <module 'json' from 'C:\\<...>\Lib\\json\\__init__.py'>
    km_to_miles       function         <function km_to_miles at 0x000001F353C20C20>
    race_km           int              5
    sys               module           <module 'sys' (built-in)>
    


```python
# Introspection on user generated functions?
km_to_miles?
```


    [1;31mSignature:[0m [0mkm_to_miles[0m[1;33m([0m[0mkm[0m[1;33m)[0m[1;33m[0m[1;33m[0m[0m
    [1;31mDocstring:[0m Converts kilometers to miles
    [1;31mFile:[0m      c:\users\micha\appdata\local\temp\ipykernel_24900\3993506249.py
    [1;31mType:[0m      function



```python
# Help?
help(km_to_miles)
```

    Help on function km_to_miles in module __main__:
    
    km_to_miles(km)
        Converts kilometers to miles
    
    


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
    #print(a)
```


```python
# What is it?
test
type(test())
```




    NoneType




```python
# Scope?
km_to_miles(5)
```




    3.106855




```python
# Does it exist?
print(miles)
```


    ---------------------------------------------------------------------------

    NameError                                 Traceback (most recent call last)

    Cell In[10], line 2
          1 # Does it exist?
    ----> 2 print(miles)
    

    NameError: name 'miles' is not defined



```python
# Is it saved?
km_to_miles(3)
%whos
```

    Variable          Type             Data/Info
    --------------------------------------------
    NamespaceMagics   MetaHasTraits    <class 'IPython.core.magi<...>mespace.NamespaceMagics'>
    collections       module           <module 'collections' fro<...>ollections\\__init__.py'>
    get_ipython       function         <function get_ipython at 0x000001F351130E00>
    islice            type             <class 'itertools.islice'>
    json              module           <module 'json' from 'C:\\<...>\Lib\\json\\__init__.py'>
    km_to_miles       function         <function km_to_miles at 0x000001F353C20C20>
    race_km           int              5
    race_miles        float            3.106855
    sys               module           <module 'sys' (built-in)>
    test              function         <function test at 0x000001F353C22F20>
    


```python
# Define another function
def city_state_fixer(city, state):
    '''
    Fixes capitalization problems with cities and states, returning one string with first letter of each word capitalized
    '''

    # The function "title" capitalizes the first letter and makes the rest lower case 
    return city.title() + ", " + state.title()    
```


```python
# Test it out!
city_state_fixer("MADison", "wISCONSIN")
```




    'Madison, Wisconsin'




```python
# Name of inputs?
city_state_fixer(city = "MADison", state = "wISCONSIN")
```




    'Madison, Wisconsin'




```python
# Do you HAVE to use both?
city_state_fixer(city = "MADison")
```


    ---------------------------------------------------------------------------

    TypeError                                 Traceback (most recent call last)

    Cell In[15], line 2
          1 # Do you HAVE to use both?
    ----> 2 city_state_fixer(city = "MADison")
    

    TypeError: city_state_fixer() missing 1 required positional argument: 'state'



```python
# Initializing variables
def city_state_fixer_v2(city = "", state = ""):
    '''
    Fixes capitalization problems with cities and states, allowing for one or the other
    '''

    if city == "" or state == "":
        return city.title() + state.title()
    else:
        return city.title() + ", " + state.title()
```


```python
# Testing it out again
city_state_fixer_v2("MADison")
```




    'Madison'




```python
# Still work?
city_state_fixer_v2("MADison", "wISCONSIN")
```




    'Madison, Wisconsin'




```python
# Checking with state
city_state_fixer_v2("wISCONSIN")
```




    'Wisconsin'




```python
# Changing return type
def city_state_fixer_v3(city = "", state = ""):
    '''
    Fixes capitalization problems with cities and states, allowing for one or the other
    '''

    if city == "" or state == "":
        return city.title(), state.title()
    else:
        return city.title(), state.title()
```


```python
# What does it look like now?
city_state_fixer_v3("Madison", "Wisconsin")
```




    ('Madison', 'Wisconsin')




```python
# Unpacking it
city1, state1 = city_state_fixer_v3("MADison","wISCONSIN")
print(city1)
print(state1)
```

    Madison
    Wisconsin
    


```python
# What happens with incorrect types?
race_km = "5"
race_miles = km_to_miles(race_km)
```


    ---------------------------------------------------------------------------

    TypeError                                 Traceback (most recent call last)

    Cell In[23], line 3
          1 # What happens with incorrect types?
          2 race_km = "5"
    ----> 3 race_miles = km_to_miles(race_km)
    

    Cell In[1], line 8, in km_to_miles(km)
          3 '''
          4 Converts kilometers to miles
          5 '''
          7 # 1 km = 0.621371 miles
    ----> 8 miles = km*0.621371
         10 # Use return to tell the function what to send back after being called
         11 return miles
    

    TypeError: can't multiply sequence by non-int of type 'float'



```python
# Manual warning
def km_to_miles_v2(km):
    """
    Input a distance in km. Return the distance in miles.
    """

    if type(km)==float or type(km)== int:
        miles = km * 0.621371
        return km
    else:
        print('WARNING: km_to_miles_v2 only takes ints or floats.')
        return -99
```


```python
# What happens with incorrect types?
race_km = "5"
race_miles = km_to_miles_v2(race_km)
```

    WARNING: km_to_miles_v2 only takes ints or floats.
    


```python
# Try & Except
a=10
b=0
try:
    print(a/b)
except:
    print('WARNING: unable to divide {num} by {den}'.format(num=a,den=b))
```

    WARNING: unable to divide 10 by 0
    


```python
# Making use in a function
def divide(a, b):
    try:
        print(a/b,end='')
    except TypeError:
        print('TypeError: unable to divide {num} by {den}'.format(num=a,den=b))
    except ZeroDivisionError:
        print('ZeroDivisionError: unable to divide {num} by {den}'.format(num=a,den=b))
    else:
        print(' --> Calculation succeeded')
```


```python
# Test it out!
divide(1,'Rabbits')
divide(1,0)
divide(1,2)
```

    TypeError: unable to divide 1 by Rabbits
    ZeroDivisionError: unable to divide 1 by 0
    0.5 --> Calculation succeeded
    

## Practice - Functions
1. Write a function called change_counting. Pass the function the number of pennies, nickels, dimes, and quarters and output the value of the coins.
2. Modify city_state_fixer_v3 to also return the length of the string of the city + state. Test it with "DETROIT" and "michigan", printing the city, state, and length of the sum.


```python
# Results
# 1.
def change_counting(pennies=0, nickels=0, dimes=0, quarters=0):
    return (pennies*1+nickels*5+dimes*10+quarters*25)/100
print(change_counting(quarters=4, nickels=2))
# 2. 
# Changing return type
def city_state_fixer_v3(city = "", state = ""):
    '''
    Fixes capitalization problems with cities and states, allowing for one or the other
    '''

    if city == "" or state == "":
        return city.title(), state.title(), len(city+state)
    else:
        return city.title(), state.title(), len(city+state)
print(city_state_fixer_v3("DETROIT", "michigan"))
```

    1.1
    ('Detroit', 'Michigan', 15)
    

## Packages


```python
# Functions we might expect
log(10)
```


    ---------------------------------------------------------------------------

    NameError                                 Traceback (most recent call last)

    Cell In[29], line 2
          1 # Functions we might expect
    ----> 2 log(10)
    

    NameError: name 'log' is not defined



```python
# Importing packages
import os
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
    city1                 str              Madison
    city_state_fixer      function         <function city_state_fixer at 0x000001F354A9FD80>
    city_state_fixer_v2   function         <function city_state_fixe<...>v2 at 0x000001F354A9D440>
    city_state_fixer_v3   function         <function city_state_fixe<...>v3 at 0x000001F354A9CE00>
    collections           module           <module 'collections' fro<...>ollections\\__init__.py'>
    divide                function         <function divide at 0x000001F354A9D6C0>
    get_ipython           function         <function get_ipython at 0x000001F351130E00>
    islice                type             <class 'itertools.islice'>
    json                  module           <module 'json' from 'C:\\<...>\Lib\\json\\__init__.py'>
    km_to_miles           function         <function km_to_miles at 0x000001F353C20C20>
    km_to_miles_v2        function         <function km_to_miles_v2 at 0x000001F354A9DEE0>
    os                    module           <module 'os' from 'C:\\Us<...>\\anaconda3\\Lib\\os.py'>
    race_km               str              5
    race_miles            int              -99
    state1                str              Wisconsin
    sys                   module           <module 'sys' (built-in)>
    test                  function         <function test at 0x000001F353C22F20>
    


```python
# Importing more and renaming
import numpy as np
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
print(ln(10))
print(exp(10))
print(pi)
```

    2.302585092994046
    22026.465794806718
    3.141592653589793
    


```python
# Tiny Dip into Regular Expression
import re

def city_state_fixer_v4(city = "", state = ""):
    city_no_symb = re.sub("[!#? ]", "", city)
    state_no_symb = re.sub("[!#? ]", "", state)

    if city == "" or state == "":
        return city_no_symb.title(), state_no_symb.title()
    else:
        return city_no_symb.title(), state_no_symb.title()
```


```python
# Test it out
city_state_fixer_v4(city = "MADison!", state = "wISCONSIN ")
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
    city1                 str              Madison
    city_state_fixer      function         <function city_state_fixer at 0x000001F354A9FD80>
    city_state_fixer_v2   function         <function city_state_fixe<...>v2 at 0x000001F354A9D440>
    city_state_fixer_v3   function         <function city_state_fixe<...>v3 at 0x000001F354A9CE00>
    city_state_fixer_v4   function         <function city_state_fixe<...>v4 at 0x000001F354A9CEA0>
    collections           module           <module 'collections' fro<...>ollections\\__init__.py'>
    divide                function         <function divide at 0x000001F354A9D6C0>
    exp                   ufunc            <ufunc 'exp'>
    get_ipython           function         <function get_ipython at 0x000001F351130E00>
    islice                type             <class 'itertools.islice'>
    json                  module           <module 'json' from 'C:\\<...>\Lib\\json\\__init__.py'>
    km_to_miles           function         <function km_to_miles at 0x000001F353C20C20>
    km_to_miles_v2        function         <function km_to_miles_v2 at 0x000001F354A9DEE0>
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
    test                  function         <function test at 0x000001F353C22F20>
    


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
    all                       _ArrayFunctionDispatcher      <function all at 0x000001F354C6E480>
    allclose                  _ArrayFunctionDispatcher      <function allclose at 0x000001F354C9A160>
    amax                      _ArrayFunctionDispatcher      <function amax at 0x000001F354C6EB60>
    amin                      _ArrayFunctionDispatcher      <function amin at 0x000001F354C6EDE0>
    angle                     _ArrayFunctionDispatcher      <function angle at 0x000001F354DBB880>
    any                       _ArrayFunctionDispatcher      <function any at 0x000001F354C6E340>
    append                    _ArrayFunctionDispatcher      <function append at 0x000001F354DD2660>
    apply_along_axis          _ArrayFunctionDispatcher      <function apply_along_axis at 0x000001F354DE9760>
    apply_over_axes           _ArrayFunctionDispatcher      <function apply_over_axes at 0x000001F354DE98A0>
    arange                    builtin_function_or_method    <built-in function arange>
    arccos                    ufunc                         <ufunc 'arccos'>
    arccosh                   ufunc                         <ufunc 'arccosh'>
    arcsin                    ufunc                         <ufunc 'arcsin'>
    arcsinh                   ufunc                         <ufunc 'arcsinh'>
    arctan                    ufunc                         <ufunc 'arctan'>
    arctan2                   ufunc                         <ufunc 'arctan2'>
    arctanh                   ufunc                         <ufunc 'arctanh'>
    argmax                    _ArrayFunctionDispatcher      <function argmax at 0x000001F354C6D300>
    argmin                    _ArrayFunctionDispatcher      <function argmin at 0x000001F354C6D440>
    argpartition              _ArrayFunctionDispatcher      <function argpartition at 0x000001F354C6CF40>
    argsort                   _ArrayFunctionDispatcher      <function argsort at 0x000001F354C6D1C0>
    argwhere                  _ArrayFunctionDispatcher      <function argwhere at 0x000001F354C98F40>
    around                    _ArrayFunctionDispatcher      <function around at 0x000001F354C6F4C0>
    array                     builtin_function_or_method    <built-in function array>
    array2string              _ArrayFunctionDispatcher      <function array2string at 0x000001F354C9B740>
    array_equal               _ArrayFunctionDispatcher      <function array_equal at 0x000001F354C9A480>
    array_equiv               _ArrayFunctionDispatcher      <function array_equiv at 0x000001F354C9A5C0>
    array_repr                _ArrayFunctionDispatcher      <function array_repr at 0x000001F354CBCD60>
    array_split               _ArrayFunctionDispatcher      <function array_split at 0x000001F354DE9EE0>
    array_str                 _ArrayFunctionDispatcher      <function array_str at 0x000001F354CBD080>
    asanyarray                builtin_function_or_method    <built-in function asanyarray>
    asarray                   builtin_function_or_method    <built-in function asarray>
    asarray_chkfinite         function                      <function asarray_chkfini<...>te at 0x000001F354DBAFC0>
    ascontiguousarray         builtin_function_or_method    <built-in function ascontiguousarray>
    asfortranarray            builtin_function_or_method    <built-in function asfortranarray>
    asin                      ufunc                         <ufunc 'arcsin'>
    asinh                     ufunc                         <ufunc 'arcsinh'>
    asmatrix                  function                      <function asmatrix at 0x000001F354D2EFC0>
    astype                    _ArrayFunctionDispatcher      <function astype at 0x000001F354C9A700>
    atan                      ufunc                         <ufunc 'arctan'>
    atan2                     ufunc                         <ufunc 'arctan2'>
    atanh                     ufunc                         <ufunc 'arctanh'>
    atleast_1d                _ArrayFunctionDispatcher      <function atleast_1d at 0x000001F354C6F7E0>
    atleast_2d                _ArrayFunctionDispatcher      <function atleast_2d at 0x000001F354C6F9C0>
    atleast_3d                _ArrayFunctionDispatcher      <function atleast_3d at 0x000001F354C6FB00>
    average                   _ArrayFunctionDispatcher      <function average at 0x000001F354DBAF20>
    b                         int                           0
    bartlett                  function                      <function bartlett at 0x000001F354DD0C20>
    base_repr                 function                      <function base_repr at 0x000001F354C99EE0>
    binary_repr               function                      <function binary_repr at 0x000001F354C99E40>
    bincount                  _ArrayFunctionDispatcher      <built-in function bincount>
    bitwise_and               ufunc                         <ufunc 'bitwise_and'>
    bitwise_count             ufunc                         <ufunc 'bitwise_count'>
    bitwise_invert            ufunc                         <ufunc 'invert'>
    bitwise_left_shift        ufunc                         <ufunc 'left_shift'>
    bitwise_not               ufunc                         <ufunc 'invert'>
    bitwise_or                ufunc                         <ufunc 'bitwise_or'>
    bitwise_right_shift       ufunc                         <ufunc 'right_shift'>
    bitwise_xor               ufunc                         <ufunc 'bitwise_xor'>
    blackman                  function                      <function blackman at 0x000001F354DD0B80>
    block                     _ArrayFunctionDispatcher      <function block at 0x000001F354C985E0>
    bmat                      function                      <function bmat at 0x000001F354DB8AE0>
    bool                      type                          <class 'numpy.bool'>
    bool_                     type                          <class 'numpy.bool'>
    broadcast                 type                          <class 'numpy.broadcast'>
    broadcast_arrays          _ArrayFunctionDispatcher      <function broadcast_arrays at 0x000001F354D2ECA0>
    broadcast_shapes          function                      <function broadcast_shapes at 0x000001F354D2EB60>
    broadcast_to              _ArrayFunctionDispatcher      <function broadcast_to at 0x000001F354D2EA20>
    busday_count              _ArrayFunctionDispatcher      <built-in function busday_count>
    busday_offset             _ArrayFunctionDispatcher      <built-in function busday_offset>
    busdaycalendar            type                          <class 'numpy.busdaycalendar'>
    byte                      type                          <class 'numpy.int8'>
    bytes_                    type                          <class 'numpy.bytes_'>
    c_                        CClass                        <numpy.lib._index_tricks_<...>ct at 0x000001F354DE0680>
    can_cast                  _ArrayFunctionDispatcher      <built-in function can_cast>
    cbrt                      ufunc                         <ufunc 'cbrt'>
    cdouble                   type                          <class 'numpy.complex128'>
    ceil                      ufunc                         <ufunc 'ceil'>
    char                      module                        <module 'numpy.char' from<...>umpy\\char\\__init__.py'>
    character                 type                          <class 'numpy.character'>
    choose                    _ArrayFunctionDispatcher      <function choose at 0x000001F354C6C680>
    city1                     str                           Madison
    city_state_fixer          function                      <function city_state_fixer at 0x000001F354A9FD80>
    city_state_fixer_v2       function                      <function city_state_fixe<...>v2 at 0x000001F354A9D440>
    city_state_fixer_v3       function                      <function city_state_fixe<...>v3 at 0x000001F354A9CE00>
    city_state_fixer_v4       function                      <function city_state_fixe<...>v4 at 0x000001F354A9CEA0>
    clip                      _ArrayFunctionDispatcher      <function clip at 0x000001F354C6E0C0>
    clongdouble               type                          <class 'numpy.clongdouble'>
    collections               module                        <module 'collections' fro<...>ollections\\__init__.py'>
    column_stack              _ArrayFunctionDispatcher      <function column_stack at 0x000001F354DE9BC0>
    common_type               _ArrayFunctionDispatcher      <function common_type at 0x000001F354D2DA80>
    complex128                type                          <class 'numpy.complex128'>
    complex64                 type                          <class 'numpy.complex64'>
    complexfloating           type                          <class 'numpy.complexfloating'>
    compress                  _ArrayFunctionDispatcher      <function compress at 0x000001F354C6DF80>
    concat                    _ArrayFunctionDispatcher      <built-in function concatenate>
    concatenate               _ArrayFunctionDispatcher      <built-in function concatenate>
    conj                      ufunc                         <ufunc 'conjugate'>
    conjugate                 ufunc                         <ufunc 'conjugate'>
    convolve                  _ArrayFunctionDispatcher      <function convolve at 0x000001F354C99300>
    copy                      _ArrayFunctionDispatcher      <function copy at 0x000001F354DBB380>
    copysign                  ufunc                         <ufunc 'copysign'>
    copyto                    _ArrayFunctionDispatcher      <built-in function copyto>
    core                      module                        <module 'numpy.core' from<...>umpy\\core\\__init__.py'>
    corrcoef                  _ArrayFunctionDispatcher      <function corrcoef at 0x000001F354DD0AE0>
    correlate                 _ArrayFunctionDispatcher      <function correlate at 0x000001F354C991C0>
    cos                       ufunc                         <ufunc 'cos'>
    cosh                      ufunc                         <ufunc 'cosh'>
    count_nonzero             _ArrayFunctionDispatcher      <function count_nonzero at 0x000001F354C98D60>
    cov                       _ArrayFunctionDispatcher      <function cov at 0x000001F354DD09A0>
    cross                     _ArrayFunctionDispatcher      <function cross at 0x000001F354C99B20>
    csingle                   type                          <class 'numpy.complex64'>
    ctypeslib                 module                        <module 'numpy.ctypeslib'<...>es\\numpy\\ctypeslib.py'>
    cumprod                   _ArrayFunctionDispatcher      <function cumprod at 0x000001F354C6F060>
    cumsum                    _ArrayFunctionDispatcher      <function cumsum at 0x000001F354C6E8E0>
    cumulative_prod           _ArrayFunctionDispatcher      <function cumulative_prod at 0x000001F354C6E660>
    cumulative_sum            _ArrayFunctionDispatcher      <function cumulative_sum at 0x000001F354C6E7A0>
    datetime64                type                          <class 'numpy.datetime64'>
    datetime_as_string        _ArrayFunctionDispatcher      <built-in function datetime_as_string>
    datetime_data             builtin_function_or_method    <built-in function datetime_data>
    deg2rad                   ufunc                         <ufunc 'deg2rad'>
    degrees                   ufunc                         <ufunc 'degrees'>
    delete                    _ArrayFunctionDispatcher      <function delete at 0x000001F354DD23E0>
    diag                      _ArrayFunctionDispatcher      <function diag at 0x000001F354D2FF60>
    diag_indices              function                      <function diag_indices at 0x000001F354DD3600>
    diag_indices_from         _ArrayFunctionDispatcher      <function diag_indices_fr<...>om at 0x000001F354DD3740>
    diagflat                  _ArrayFunctionDispatcher      <function diagflat at 0x000001F354D70040>
    diagonal                  _ArrayFunctionDispatcher      <function diagonal at 0x000001F354C6D940>
    diff                      _ArrayFunctionDispatcher      <function diff at 0x000001F354DBB600>
    digitize                  _ArrayFunctionDispatcher      <function digitize at 0x000001F354DD27A0>
    divide                    ufunc                         <ufunc 'divide'>
    divmod                    ufunc                         <ufunc 'divmod'>
    dot                       _ArrayFunctionDispatcher      <built-in function dot>
    double                    type                          <class 'numpy.float64'>
    dsplit                    _ArrayFunctionDispatcher      <function dsplit at 0x000001F354DEA340>
    dstack                    _ArrayFunctionDispatcher      <function dstack at 0x000001F354DE9D00>
    dtype                     _DTypeMeta                    <class 'numpy.dtype'>
    dtypes                    module                        <module 'numpy.dtypes' fr<...>kages\\numpy\\dtypes.py'>
    e                         float                         2.718281828459045
    ediff1d                   _ArrayFunctionDispatcher      <function ediff1d at 0x000001F354DEA8E0>
    einsum                    _ArrayFunctionDispatcher      <function einsum at 0x000001F354CCCCC0>
    einsum_path               _ArrayFunctionDispatcher      <function einsum_path at 0x000001F354CCCB80>
    emath                     module                        <module 'numpy.lib.scimat<...>\numpy\\lib\\scimath.py'>
    empty                     builtin_function_or_method    <built-in function empty>
    empty_like                _ArrayFunctionDispatcher      <built-in function empty_like>
    equal                     ufunc                         <ufunc 'equal'>
    errstate                  type                          <class 'numpy.errstate'>
    euler_gamma               float                         0.5772156649015329
    exceptions                module                        <module 'numpy.exceptions<...>s\\numpy\\exceptions.py'>
    exp                       ufunc                         <ufunc 'exp'>
    exp2                      ufunc                         <ufunc 'exp2'>
    expand_dims               _ArrayFunctionDispatcher      <function expand_dims at 0x000001F354DE99E0>
    expm1                     ufunc                         <ufunc 'expm1'>
    extract                   _ArrayFunctionDispatcher      <function extract at 0x000001F354DBBD80>
    eye                       function                      <function eye at 0x000001F354D2FE20>
    f2py                      module                        <module 'numpy.f2py' from<...>umpy\\f2py\\__init__.py'>
    fabs                      ufunc                         <ufunc 'fabs'>
    fft                       module                        <module 'numpy.fft' from <...>numpy\\fft\\__init__.py'>
    fill_diagonal             _ArrayFunctionDispatcher      <function fill_diagonal at 0x000001F354DD3560>
    finfo                     type                          <class 'numpy.finfo'>
    fix                       _ArrayFunctionDispatcher      <function fix at 0x000001F354D2CF40>
    flatiter                  type                          <class 'numpy.flatiter'>
    flatnonzero               _ArrayFunctionDispatcher      <function flatnonzero at 0x000001F354C99080>
    flexible                  type                          <class 'numpy.flexible'>
    flip                      _ArrayFunctionDispatcher      <function flip at 0x000001F354DBACA0>
    fliplr                    _ArrayFunctionDispatcher      <function fliplr at 0x000001F354D2FCE0>
    flipud                    _ArrayFunctionDispatcher      <function flipud at 0x000001F354D2FD80>
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
    format_float_positional   function                      <function format_float_po<...>al at 0x000001F354C9BCE0>
    format_float_scientific   function                      <function format_float_sc<...>ic at 0x000001F354C9BC40>
    frexp                     ufunc                         <ufunc 'frexp'>
    from_dlpack               builtin_function_or_method    <built-in function from_dlpack>
    frombuffer                builtin_function_or_method    <built-in function frombuffer>
    fromfile                  builtin_function_or_method    <built-in function fromfile>
    fromfunction              function                      <function fromfunction at 0x000001F354C99C60>
    fromiter                  builtin_function_or_method    <built-in function fromiter>
    frompyfunc                builtin_function_or_method    <built-in function frompyfunc>
    fromregex                 function                      <function fromregex at 0x000001F354D2C680>
    fromstring                builtin_function_or_method    <built-in function fromstring>
    full                      function                      <function full at 0x000001F354C98AE0>
    full_like                 _ArrayFunctionDispatcher      <function full_like at 0x000001F354C98C20>
    gcd                       ufunc                         <ufunc 'gcd'>
    generic                   type                          <class 'numpy.generic'>
    genfromtxt                function                      <function genfromtxt at 0x000001F354D2C720>
    geomspace                 _ArrayFunctionDispatcher      <function geomspace at 0x000001F354CBEAC0>
    get_include               function                      <function get_include at 0x000001F354D03600>
    get_ipython               function                      <function get_ipython at 0x000001F351130E00>
    get_printoptions          function                      <function get_printoptions at 0x000001F354C9AE80>
    getbufsize                function                      <function getbufsize at 0x000001F354C3F380>
    geterr                    function                      <function geterr at 0x000001F354C3F240>
    geterrcall                function                      <function geterrcall at 0x000001F354C3F4C0>
    gradient                  _ArrayFunctionDispatcher      <function gradient at 0x000001F354DBB4C0>
    greater                   ufunc                         <ufunc 'greater'>
    greater_equal             ufunc                         <ufunc 'greater_equal'>
    half                      type                          <class 'numpy.float16'>
    hamming                   function                      <function hamming at 0x000001F354DD0D60>
    hanning                   function                      <function hanning at 0x000001F354DD0CC0>
    heaviside                 ufunc                         <ufunc 'heaviside'>
    histogram                 _ArrayFunctionDispatcher      <function histogram at 0x000001F354DB9D00>
    histogram2d               _ArrayFunctionDispatcher      <function histogram2d at 0x000001F354D70540>
    histogram_bin_edges       _ArrayFunctionDispatcher      <function histogram_bin_e<...>es at 0x000001F354DB9BC0>
    histogramdd               _ArrayFunctionDispatcher      <function histogramdd at 0x000001F354DB9E40>
    hsplit                    _ArrayFunctionDispatcher      <function hsplit at 0x000001F354DEA200>
    hstack                    _ArrayFunctionDispatcher      <function hstack at 0x000001F354C6FD80>
    hypot                     ufunc                         <ufunc 'hypot'>
    i0                        _ArrayFunctionDispatcher      <function i0 at 0x000001F354DD1080>
    identity                  function                      <function identity at 0x000001F354C9A020>
    iinfo                     type                          <class 'numpy.iinfo'>
    imag                      _ArrayFunctionDispatcher      <function imag at 0x000001F354D2D260>
    in1d                      _ArrayFunctionDispatcher      <function in1d at 0x000001F354DEBF60>
    index_exp                 IndexExpression               <numpy.lib._index_tricks_<...>ct at 0x000001F354DC30D0>
    indices                   function                      <function indices at 0x000001F354C99BC0>
    inexact                   type                          <class 'numpy.inexact'>
    inf                       float                         inf
    info                      function                      <function info at 0x000001F354D03BA0>
    inner                     _ArrayFunctionDispatcher      <built-in function inner>
    insert                    _ArrayFunctionDispatcher      <function insert at 0x000001F354DD2520>
    int16                     type                          <class 'numpy.int16'>
    int32                     type                          <class 'numpy.int32'>
    int64                     type                          <class 'numpy.int64'>
    int8                      type                          <class 'numpy.int8'>
    int_                      type                          <class 'numpy.int64'>
    intc                      type                          <class 'numpy.intc'>
    integer                   type                          <class 'numpy.integer'>
    interp                    _ArrayFunctionDispatcher      <function interp at 0x000001F354DBB740>
    intersect1d               _ArrayFunctionDispatcher      <function intersect1d at 0x000001F354DEBCE0>
    intp                      type                          <class 'numpy.int64'>
    invert                    ufunc                         <ufunc 'invert'>
    is_busday                 _ArrayFunctionDispatcher      <built-in function is_busday>
    isclose                   _ArrayFunctionDispatcher      <function isclose at 0x000001F354C9A2A0>
    iscomplex                 _ArrayFunctionDispatcher      <function iscomplex at 0x000001F354D2D3A0>
    iscomplexobj              _ArrayFunctionDispatcher      <function iscomplexobj at 0x000001F354D2D4E0>
    isdtype                   function                      <function isdtype at 0x000001F354C3E3E0>
    isfinite                  ufunc                         <ufunc 'isfinite'>
    isfortran                 function                      <function isfortran at 0x000001F354C98E00>
    isin                      _ArrayFunctionDispatcher      <function isin at 0x000001F354DF8180>
    isinf                     ufunc                         <ufunc 'isinf'>
    islice                    type                          <class 'itertools.islice'>
    isnan                     ufunc                         <ufunc 'isnan'>
    isnat                     ufunc                         <ufunc 'isnat'>
    isneginf                  _ArrayFunctionDispatcher      <function isneginf at 0x000001F354D2D080>
    isposinf                  _ArrayFunctionDispatcher      <function isposinf at 0x000001F354D2CFE0>
    isreal                    _ArrayFunctionDispatcher      <function isreal at 0x000001F354D2D440>
    isrealobj                 _ArrayFunctionDispatcher      <function isrealobj at 0x000001F354D2D580>
    isscalar                  function                      <function isscalar at 0x000001F354C99DA0>
    issubdtype                function                      <function issubdtype at 0x000001F354C3E480>
    iterable                  function                      <function iterable at 0x000001F354DBAD40>
    ix_                       _ArrayFunctionDispatcher      <function ix_ at 0x000001F354DD2700>
    json                      module                        <module 'json' from 'C:\\<...>\Lib\\json\\__init__.py'>
    kaiser                    function                      <function kaiser at 0x000001F354DD1120>
    km_to_miles               function                      <function km_to_miles at 0x000001F353C20C20>
    km_to_miles_v2            function                      <function km_to_miles_v2 at 0x000001F354A9DEE0>
    kron                      _ArrayFunctionDispatcher      <function kron at 0x000001F354DEA520>
    lcm                       ufunc                         <ufunc 'lcm'>
    ldexp                     ufunc                         <ufunc 'ldexp'>
    left_shift                ufunc                         <ufunc 'left_shift'>
    less                      ufunc                         <ufunc 'less'>
    less_equal                ufunc                         <ufunc 'less_equal'>
    lexsort                   _ArrayFunctionDispatcher      <built-in function lexsort>
    lib                       module                        <module 'numpy.lib' from <...>numpy\\lib\\__init__.py'>
    linalg                    module                        <module 'numpy.linalg' fr<...>py\\linalg\\__init__.py'>
    linspace                  _ArrayFunctionDispatcher      <function linspace at 0x000001F354CBE840>
    little_endian             bool                          True
    ln                        ufunc                         <ufunc 'log'>
    load                      function                      <function load at 0x000001F354D1F380>
    loadtxt                   function                      <function loadtxt at 0x000001F354D2C4A0>
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
    logspace                  _ArrayFunctionDispatcher      <function logspace at 0x000001F354CBE980>
    long                      type                          <class 'numpy.int32'>
    longdouble                type                          <class 'numpy.longdouble'>
    longlong                  type                          <class 'numpy.int64'>
    ma                        module                        <module 'numpy.ma' from '<...>\numpy\\ma\\__init__.py'>
    mask_indices              function                      <function mask_indices at 0x000001F354D705E0>
    matmul                    ufunc                         <ufunc 'matmul'>
    matrix                    type                          <class 'numpy.matrix'>
    matrix_transpose          _ArrayFunctionDispatcher      <function matrix_transpose at 0x000001F354C6CCC0>
    max                       _ArrayFunctionDispatcher      <function max at 0x000001F354C6EC00>
    maximum                   ufunc                         <ufunc 'maximum'>
    may_share_memory          _ArrayFunctionDispatcher      <built-in function may_share_memory>
    mean                      _ArrayFunctionDispatcher      <function mean at 0x000001F354C6F600>
    median                    _ArrayFunctionDispatcher      <function median at 0x000001F354DD1440>
    memmap                    type                          <class 'numpy.memmap'>
    meshgrid                  _ArrayFunctionDispatcher      <function meshgrid at 0x000001F354DD22A0>
    mgrid                     MGridClass                    <numpy.lib._index_tricks_<...>ct at 0x000001F354DC2EF0>
    min                       _ArrayFunctionDispatcher      <function min at 0x000001F354C6ED40>
    min_scalar_type           _ArrayFunctionDispatcher      <built-in function min_scalar_type>
    minimum                   ufunc                         <ufunc 'minimum'>
    mintypecode               function                      <function mintypecode at 0x000001F354D2CD60>
    mod                       ufunc                         <ufunc 'remainder'>
    modf                      ufunc                         <ufunc 'modf'>
    moveaxis                  _ArrayFunctionDispatcher      <function moveaxis at 0x000001F354C999E0>
     <ufunc 'multiply'>       ufunc                        
    nan                       float                         nan
    nan_to_num                _ArrayFunctionDispatcher      <function nan_to_num at 0x000001F354D2D760>
    nanargmax                 _ArrayFunctionDispatcher      <function nanargmax at 0x000001F354DE8180>
    nanargmin                 _ArrayFunctionDispatcher      <function nanargmin at 0x000001F354DE8040>
    nancumprod                _ArrayFunctionDispatcher      <function nancumprod at 0x000001F354DE8680>
    nancumsum                 _ArrayFunctionDispatcher      <function nancumsum at 0x000001F354DE8540>
    nanmax                    _ArrayFunctionDispatcher      <function nanmax at 0x000001F354DD3EC0>
    nanmean                   _ArrayFunctionDispatcher      <function nanmean at 0x000001F354DE87C0>
    nanmedian                 _ArrayFunctionDispatcher      <function nanmedian at 0x000001F354DE8AE0>
    nanmin                    _ArrayFunctionDispatcher      <function nanmin at 0x000001F354DD3D80>
    nanpercentile             _ArrayFunctionDispatcher      <function nanpercentile at 0x000001F354DE8C20>
    nanprod                   _ArrayFunctionDispatcher      <function nanprod at 0x000001F354DE8400>
    nanquantile               _ArrayFunctionDispatcher      <function nanquantile at 0x000001F354DE8D60>
    nanstd                    _ArrayFunctionDispatcher      <function nanstd at 0x000001F354DE91C0>
    nansum                    _ArrayFunctionDispatcher      <function nansum at 0x000001F354DE82C0>
    nanvar                    _ArrayFunctionDispatcher      <function nanvar at 0x000001F354DE9080>
    ndarray                   type                          <class 'numpy.ndarray'>
    ndenumerate               type                          <class 'numpy.ndenumerate'>
    ndim                      _ArrayFunctionDispatcher      <function ndim at 0x000001F354C6F1A0>
    ndindex                   type                          <class 'numpy.ndindex'>
    nditer                    type                          <class 'numpy.nditer'>
    negative                  ufunc                         <ufunc 'negative'>
    nested_iters              builtin_function_or_method    <built-in function nested_iters>
    newaxis                   NoneType                      None
    nextafter                 ufunc                         <ufunc 'nextafter'>
    nonzero                   _ArrayFunctionDispatcher      <function nonzero at 0x000001F354C6DD00>
    not_equal                 ufunc                         <ufunc 'not_equal'>
    np                        module                        <module 'numpy' from 'C:\<...>ges\\numpy\\__init__.py'>
    number                    type                          <class 'numpy.number'>
    object_                   type                          <class 'numpy.object_'>
    ogrid                     OGridClass                    <numpy.lib._index_tricks_<...>ct at 0x000001F354DC2F50>
    ones                      function                      <function ones at 0x000001F354C98860>
    ones_like                 _ArrayFunctionDispatcher      <function ones_like at 0x000001F354C989A0>
    os                        module                        <module 'os' from 'C:\\Us<...>\\anaconda3\\Lib\\os.py'>
    outer                     _ArrayFunctionDispatcher      <function outer at 0x000001F354C99440>
    packbits                  _ArrayFunctionDispatcher      <built-in function packbits>
    pad                       _ArrayFunctionDispatcher      <function pad at 0x000001F354DFB420>
    partition                 _ArrayFunctionDispatcher      <function partition at 0x000001F354C6CE00>
    pd                        module                        <module 'pandas' from 'C:<...>es\\pandas\\__init__.py'>
    percentile                _ArrayFunctionDispatcher      <function percentile at 0x000001F354DD1620>
    permute_dims              _ArrayFunctionDispatcher      <function transpose at 0x000001F354C6CB80>
    pi                        float                         3.141592653589793
    piecewise                 _ArrayFunctionDispatcher      <function piecewise at 0x000001F354DBB100>
    place                     _ArrayFunctionDispatcher      <function place at 0x000001F354DBBEC0>
    poly                      _ArrayFunctionDispatcher      <function poly at 0x000001F354DF8680>
    poly1d                    type                          <class 'numpy.poly1d'>
    polyadd                   _ArrayFunctionDispatcher      <function polyadd at 0x000001F354DF8E00>
    polyder                   _ArrayFunctionDispatcher      <function polyder at 0x000001F354DF8A40>
    polydiv                   _ArrayFunctionDispatcher      <function polydiv at 0x000001F354DF9080>
    polyfit                   _ArrayFunctionDispatcher      <function polyfit at 0x000001F354DF8B80>
    polyint                   _ArrayFunctionDispatcher      <function polyint at 0x000001F354DF8900>
    polymul                   _ArrayFunctionDispatcher      <function polymul at 0x000001F354DF8F40>
    polynomial                module                        <module 'numpy.polynomial<...>polynomial\\__init__.py'>
    polysub                   _ArrayFunctionDispatcher      <function polysub at 0x000001F354DF8EA0>
    polyval                   _ArrayFunctionDispatcher      <function polyval at 0x000001F354DF8CC0>
    positive                  ufunc                         <ufunc 'positive'>
    pow                       ufunc                         <ufunc 'power'>
    power                     ufunc                         <ufunc 'power'>
    printoptions              function                      <function printoptions at 0x000001F354C9B060>
    prod                      _ArrayFunctionDispatcher      <function prod at 0x000001F354C6EF20>
    promote_types             builtin_function_or_method    <built-in function promote_types>
    ptp                       _ArrayFunctionDispatcher      <function ptp at 0x000001F354C6EA20>
    put                       _ArrayFunctionDispatcher      <function put at 0x000001F354C6C900>
    put_along_axis            _ArrayFunctionDispatcher      <function put_along_axis at 0x000001F354DE9620>
    putmask                   _ArrayFunctionDispatcher      <built-in function putmask>
    quantile                  _ArrayFunctionDispatcher      <function quantile at 0x000001F354DD1760>
    r_                        RClass                        <numpy.lib._index_tricks_<...>ct at 0x000001F354DE0600>
    race_km                   str                           5
    race_miles                int                           -99
    rad2deg                   ufunc                         <ufunc 'rad2deg'>
    radians                   ufunc                         <ufunc 'radians'>
    random                    module                        <module 'numpy.random' fr<...>py\\random\\__init__.py'>
    ravel                     _ArrayFunctionDispatcher      <function ravel at 0x000001F354C6DBC0>
    ravel_multi_index         _ArrayFunctionDispatcher      <built-in function ravel_multi_index>
    re                        module                        <module 're' from 'C:\\Us<...>3\\Lib\\re\\__init__.py'>
    real                      _ArrayFunctionDispatcher      <function real at 0x000001F354D2D120>
    real_if_close             _ArrayFunctionDispatcher      <function real_if_close at 0x000001F354D2D8A0>
    rec                       module                        <module 'numpy.rec' from <...>numpy\\rec\\__init__.py'>
    recarray                  type                          <class 'numpy.rec.recarray'>
    reciprocal                ufunc                         <ufunc 'reciprocal'>
    record                    type                          <class 'numpy.record'>
    remainder                 ufunc                         <ufunc 'remainder'>
    repeat                    _ArrayFunctionDispatcher      <function repeat at 0x000001F354C6C7C0>
    require                   function                      <function require at 0x000001F354CBD1C0>
    reshape                   _ArrayFunctionDispatcher      <function reshape at 0x000001F354C6C540>
    resize                    _ArrayFunctionDispatcher      <function resize at 0x000001F354C6D6C0>
    result_type               _ArrayFunctionDispatcher      <built-in function result_type>
    right_shift               ufunc                         <ufunc 'right_shift'>
    rint                      ufunc                         <ufunc 'rint'>
    roll                      _ArrayFunctionDispatcher      <function roll at 0x000001F354C996C0>
    rollaxis                  _ArrayFunctionDispatcher      <function rollaxis at 0x000001F354C99800>
    roots                     _ArrayFunctionDispatcher      <function roots at 0x000001F354DF87C0>
    rot90                     _ArrayFunctionDispatcher      <function rot90 at 0x000001F354DBAB60>
    round                     _ArrayFunctionDispatcher      <function round at 0x000001F354C6F420>
    row_stack                 function                      <function row_stack at 0x000001F354DE9A80>
    s_                        IndexExpression               <numpy.lib._index_tricks_<...>ct at 0x000001F354DC3130>
    save                      _ArrayFunctionDispatcher      <function save at 0x000001F354D1FD80>
    savetxt                   _ArrayFunctionDispatcher      <function savetxt at 0x000001F354D2C5E0>
    savez                     _ArrayFunctionDispatcher      <function savez at 0x000001F354D1FEC0>
    savez_compressed          _ArrayFunctionDispatcher      <function savez_compressed at 0x000001F354D2C040>
    sctypeDict                dict                          n=50
    searchsorted              _ArrayFunctionDispatcher      <function searchsorted at 0x000001F354C6D580>
    select                    _ArrayFunctionDispatcher      <function select at 0x000001F354DBB240>
    set_printoptions          function                      <function set_printoptions at 0x000001F354C9AD40>
    setbufsize                function                      <function setbufsize at 0x000001F354C3F2E0>
    setdiff1d                 _ArrayFunctionDispatcher      <function setdiff1d at 0x000001F354DF8400>
    seterr                    function                      <function seterr at 0x000001F354C3F1A0>
    seterrcall                function                      <function seterrcall at 0x000001F354C3F420>
    setxor1d                  _ArrayFunctionDispatcher      <function setxor1d at 0x000001F354DEBE20>
    shape                     _ArrayFunctionDispatcher      <function shape at 0x000001F354C6DE40>
    shares_memory             _ArrayFunctionDispatcher      <built-in function shares_memory>
    short                     type                          <class 'numpy.int16'>
    show_config               function                      <function show at 0x000001F353C23380>
    show_runtime              function                      <function show_runtime at 0x000001F354D03560>
    sign                      ufunc                         <ufunc 'sign'>
    signbit                   ufunc                         <ufunc 'signbit'>
    signedinteger             type                          <class 'numpy.signedinteger'>
    sin                       ufunc                         <ufunc 'sin'>
    sinc                      _ArrayFunctionDispatcher      <function sinc at 0x000001F354DD1260>
    single                    type                          <class 'numpy.float32'>
    sinh                      ufunc                         <ufunc 'sinh'>
    size                      _ArrayFunctionDispatcher      <function size at 0x000001F354C6F2E0>
    sort                      _ArrayFunctionDispatcher      <function sort at 0x000001F354C6D080>
    sort_complex              _ArrayFunctionDispatcher      <function sort_complex at 0x000001F354DBBB00>
    spacing                   ufunc                         <ufunc 'spacing'>
    split                     _ArrayFunctionDispatcher      <function split at 0x000001F354DEA0C0>
    sqrt                      ufunc                         <ufunc 'sqrt'>
    square                    ufunc                         <ufunc 'square'>
    squeeze                   _ArrayFunctionDispatcher      <function squeeze at 0x000001F354C6D800>
    stack                     _ArrayFunctionDispatcher      <function stack at 0x000001F354C6FEC0>
    state1                    str                           Wisconsin
    std                       _ArrayFunctionDispatcher      <function std at 0x000001F354C6F740>
    str_                      type                          <class 'numpy.str_'>
    strings                   module                        <module 'numpy.strings' f<...>y\\strings\\__init__.py'>
    subtract                  ufunc                         <ufunc 'subtract'>
    sum                       _ArrayFunctionDispatcher      <function sum at 0x000001F354C6E200>
    swapaxes                  _ArrayFunctionDispatcher      <function swapaxes at 0x000001F354C6CA40>
    sys                       module                        <module 'sys' (built-in)>
    take                      _ArrayFunctionDispatcher      <function take at 0x000001F354C6C400>
    take_along_axis           _ArrayFunctionDispatcher      <function take_along_axis at 0x000001F354DE94E0>
    tan                       ufunc                         <ufunc 'tan'>
    tanh                      ufunc                         <ufunc 'tanh'>
    tensordot                 _ArrayFunctionDispatcher      <function tensordot at 0x000001F354C99580>
    test                      PytestTester                  <numpy._pytesttester.Pyte<...>ct at 0x000001F354C42B10>
    testing                   module                        <module 'numpy.testing' f<...>y\\testing\\__init__.py'>
    tile                      _ArrayFunctionDispatcher      <function tile at 0x000001F354DEA660>
    timedelta64               type                          <class 'numpy.timedelta64'>
    trace                     _ArrayFunctionDispatcher      <function trace at 0x000001F354C6DA80>
    transpose                 _ArrayFunctionDispatcher      <function transpose at 0x000001F354C6CB80>
    trapezoid                 _ArrayFunctionDispatcher      <function trapezoid at 0x000001F354DD20C0>
    trapz                     function                      <function trapz at 0x000001F354DD2160>
    tri                       function                      <function tri at 0x000001F354D700E0>
    tril                      _ArrayFunctionDispatcher      <function tril at 0x000001F354D70220>
    tril_indices              function                      <function tril_indices at 0x000001F354D70680>
    tril_indices_from         _ArrayFunctionDispatcher      <function tril_indices_fr<...>om at 0x000001F354D707C0>
    trim_zeros                _ArrayFunctionDispatcher      <function trim_zeros at 0x000001F354DBBC40>
    triu                      _ArrayFunctionDispatcher      <function triu at 0x000001F354D702C0>
    triu_indices              function                      <function triu_indices at 0x000001F354D70860>
    triu_indices_from         _ArrayFunctionDispatcher      <function triu_indices_fr<...>om at 0x000001F354D70900>
    true_divide               ufunc                         <ufunc 'divide'>
    trunc                     ufunc                         <ufunc 'trunc'>
    typecodes                 dict                          n=9
    typename                  function                      <function typename at 0x000001F354D2D940>
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
    union1d                   _ArrayFunctionDispatcher      <function union1d at 0x000001F354DF82C0>
    unique                    _ArrayFunctionDispatcher      <function unique at 0x000001F354DEAAC0>
    unique_all                _ArrayFunctionDispatcher      <function unique_all at 0x000001F354DEB7E0>
    unique_counts             _ArrayFunctionDispatcher      <function unique_counts at 0x000001F354DEB920>
    unique_inverse            _ArrayFunctionDispatcher      <function unique_inverse at 0x000001F354DEBA60>
    unique_values             _ArrayFunctionDispatcher      <function unique_values at 0x000001F354DEBBA0>
    unpackbits                _ArrayFunctionDispatcher      <built-in function unpackbits>
    unravel_index             _ArrayFunctionDispatcher      <built-in function unravel_index>
    unsignedinteger           type                          <class 'numpy.unsignedinteger'>
    unstack                   _ArrayFunctionDispatcher      <function unstack at 0x000001F354C98040>
    unwrap                    _ArrayFunctionDispatcher      <function unwrap at 0x000001F354DBB9C0>
    ushort                    type                          <class 'numpy.uint16'>
    vander                    _ArrayFunctionDispatcher      <function vander at 0x000001F354D70400>
    var                       _ArrayFunctionDispatcher      <function var at 0x000001F354C6F880>
    vdot                      _ArrayFunctionDispatcher      <built-in function vdot>
    vecdot                    ufunc                         <ufunc 'vecdot'>
    vectorize                 type                          <class 'numpy.vectorize'>
    void                      type                          <class 'numpy.void'>
    vsplit                    _ArrayFunctionDispatcher      <function vsplit at 0x000001F354DEA2A0>
    vstack                    _ArrayFunctionDispatcher      <function vstack at 0x000001F354C6FCE0>
    where                     _ArrayFunctionDispatcher      <built-in function where>
    zeros                     builtin_function_or_method    <built-in function zeros>
    zeros_like                _ArrayFunctionDispatcher      <function zeros_like at 0x000001F354C987C0>
    
