---
layout: single
sitemap: false
permalink: /pages/Econ_390_SP26_L6_teaching/
---
[Download Jupyter Notebook Empty](https://m-mcmain.github.io/files/Econ390SP26/Lectures/Lecture6_Conditionals_empty.ipynb)

[Download Jupyter Notebook Completed](https://m-mcmain.github.io/files/Econ390SP26/Lectures/Lecture6_Conditionals_full.ipynb)

# Econ 390 - Lecture 6: Conditionals

This lecture we will discuss the Boolean data type and implementing conditionals in if statements and loops. Conditionals are incredibly useful for limiting what happens in the code and when. At the base of a conditional is a Boolean. This is mostly inspired by [this](https://aeturrell.github.io/coding-for-economists/data-boolean.html) chapter in Turrell.


```python
# You can just call False and True
var_bool = False
print(var_bool)
var_bool2 = True
print(var_bool2)
```

    False
    True
    


```python
# And, or, and not act as expected
print(var_bool or var_bool2)
print(var_bool and var_bool2)
print(not var_bool)
```

    True
    False
    True
    


```python
# You can cast bool into int, and vice verse
print(int(var_bool))
print(int(var_bool2))
print(bool(0))
print(bool(1))
```

    0
    1
    False
    True
    


```python
# There are many operators that act as expected
print(3 < 3)
print(3 >= 3)
print(2 == 3)
print(2 != 3)
```

    False
    True
    False
    True
    


```python
# You can create variables that use those operators, but ultimately are just bools
operator_bool = 3.14 == 3.1415
print(operator_bool)
```

    False
    


```python
# You can also do operators with all variables
inflation_target = 2
inflation = 2.9
above_target = inflation > inflation_target
print(above_target)
```

    True
    

## Practice - Boolean Variables
1. In the code cell below, use boolean operators to see if 1.5^10 is larger or smaller than 2^5
2. Create two variables, `a` that is 6/2 and `b` that is 9/3.
   - Should they be equal to each other?
   - Does Python think they are equal to each other?
   - Test it out the appropriate boolean operator
3. Cast the number 2 to bool.
   - What do you think it should return?
   - Does Python agree?
   - Test it out by printing it out.


```python

```

## If Statements


```python
# If statements can be really helpful
if inflation > inflation_target:
    print("Inflation is above the current target.")
    print("We must lower inflation by", round(inflation - inflation_target, 2), "percentage points before we hit our target.")
print("This will be said no matter what since it's outside of the if statement")
```

    Inflation is above the current target.
    We must lower inflation by 0.9 percentage points before we hit our target.
    This will be said no matter what since it's outside of the if statement
    


```python
# We can add elif and else for flexibility
inflation = 1.9
if inflation > inflation_target:
    print("Inflation is above the current target.")
    print("We must lower inflation by", round(inflation - inflation_target, 2), "percentage points before we hit our target.")
elif inflation < inflation_target:
    print("Inflation is below the current target.")
    print("We must increase inflation by", round(inflation_target - inflation, 2), "percentage points before we hit our target.")
else:
    print("Inflation is currently at the current target.")
```

    Inflation is below the current target.
    We must increase inflation by 0.1 percentage points before we hit our target.
    


```python
# You can use and & or as well
unemployment = 4.3
unemployment_avg = 3.8
if inflation > inflation_target and unemployment > unemployment_avg:
    print("We have high inflation and high unemployment. Yikes.")
          
elif inflation > inflation_target and unemployment < unemployment_avg:
    print("We have high inflation and low unemployment. We need to get inflation under control and labor market looks good. Consider raising rates.")

elif inflation < inflation_target and unemployment > unemployment_avg:
    print("We have low inflation and high unemployment. We need to get more people jobs. Consider lowering rates.")

else:
    print("We have low inflation and low unemployment. Things could be better, consider lowering rates.")
```

    We have low inflation and high unemployment. We need to get more people jobs. Consider lowering rates.
    


```python
# You can use booleans to check lists
name_list = ["Lovelace", "Smith", "Hopper", "Babbage"]

print("Lovelace" in name_list)

print("Bob" in name_list)
```

    True
    False
    


```python
pi = "3.14159"
if str(pi) == str(3.14159):
    pi = float(pi)
    print(pi_num)
```

    3.14159
    


```python
string1 = "Memorial"
string2 = "Union"
if len(string1) > len(string2):
    print(string1, string2)
elif len(string1) == len(string2):
    print("The strings are equal in length.")
else:
    print(string2, string1)
```

    Memorial Union
    

## Practice - If Statements
1. Redo #2 in the previous practice and use what you've learned since then to get Python to recognize that `a` *is* equal to `b`. Use print for proof.
2. Create two variables, `my_age` and `my_name` which is equal to your age and name, and `their_age` and `their_name` which is equal to the age and name of someone sitting near you. Then write and if else statement that prints out a sentence remarking on who is older (referring to names).
3. Create a variable `final_grade_point` and set it equal any GPA you could get in this course. Then, using the `grades` dictionary, write and if else statement going through if you would be happy, fine, or disappointed if you actually got `final_grade_point`.


```python
grades = {'A':4.0, 'AB':3.5, 'B':3, 'BC':2.5, 'C':2.0, 'D':1.0, 'F':0.0}
```
