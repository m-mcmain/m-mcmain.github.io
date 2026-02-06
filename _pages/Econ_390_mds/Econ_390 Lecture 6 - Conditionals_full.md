---
layout: single
sitemap: false
permalink: /pages/Econ_390_SP26_L6/
---

[Download Jupyter Notebook Empty](https://m-mcmain.github.io/files/Econ390SP26/Lectures/Lecture6_Conditionals_empty.ipynb)

Download Jupyter Notebook Completed

# Econ 390 - Lecture 6: Conditionals

This lecture we will discuss the Boolean data type and implementing conditionals in if statements and loops. Conditionals are incredibly useful for limiting what happens in the code and when. At the base of a conditional is a Boolean. This is mostly inspired by [this](https://aeturrell.github.io/coding-for-economists/data-boolean.html) chapter in Turrell.


```python
# You can just call False and True
var_bool = False
print(var_bool)
var_bool2 = True
print(type(var_bool2))
```

    False
    <class 'bool'>
    


```python
# And, or, and not act as expected
print(var_bool and var_bool2) 
print(var_bool or var_bool2)

# Is it "exclusive or" i.e. one or the other and NOT both
var_bool3 = True
print(var_bool2 or var_bool3)

# not ?
print(not var_bool)
```

    False
    True
    True
    True
    


```python
# You can cast bool into int, and vice verse
print(int(var_bool))
print(int(var_bool2))

# Int -> Bool
print(bool(1))
print(bool(0))
```

    0
    1
    True
    False
    


```python
# There are many operators that act as expected
print(3 < 4)
print(3 >= 3)
print (2 == 3)
print(2 != 3)
```

    True
    True
    False
    True
    


```python
# You can create variables that are equal to a condition
operator_bool = 3.14 == 3.1415
print(operator_bool)
```

    False
    


```python
# Conditionals work with variables as well!
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
# Results:
# 1. 
print(1.5**10 > 2**5)
# 2. 
a = 6/2
b = 9.0**0.5
print(a == b)
# 3. 
print(bool(2))
```

    True
    True
    True
    

## If Statements


```python
# If statements can be really helpful
inflation = 2.0
if inflation > inflation_target:
    print("Inflation is above the current target.")
    print("We must lower inflation by", round(inflation - inflation_target, 2), "percentage points before we hit our target.")
print("This will print no matter what.")
```

    This will print no matter what.
    


```python
# We can add elif and else for flexibility
inflation = 1.9
if inflation > inflation_target:
    print("Inflation is above the current target.")
    print("We must lower inflation by", round(inflation - inflation_target, 2), "percentage points before we hit our target.")
elif inflation < inflation_target:
    print("Inflation is below the current target.")
    print("We must raise inflation by", round(inflation_target - inflation, 2), "percentage points before we hit our target.")
else:
    print("Inflation is currently at its target.")
```

    Inflation is below the current target.
    We must raise inflation by 0.1 percentage points before we hit our target.
    


```python
# You can use and & or as well
unemployment = 3.8
unemployment_avg = 3.8

inflation = 2.9

if inflation > inflation_target and unemployment > unemployment_avg:
    print("We have high inflation and high unemployment. Yikes.")
elif inflation > inflation_target and unemployment <= unemployment_avg:
    print("We have high inflation but low unemployment. Might want to raise interest rates.")
elif inflation <= inflation_target and unemployment > unemployment_avg:
    print("We have low inflation but high unemployment. Might want to lower interest rates.")
else:
    print("We have low inflation and low unemployment. We're chilling, maybe consider lowering rates.")
```

    We have high inflation but low unemployment. Might want to raise interest rates.
    


```python
# You can use booleans to check lists
name_list = ["Andrew", "Karl", "Dane", "Jack"]

print("Carmen" in name_list)
print("Dane" in name_list)
```

    False
    True
    


```python
# Clever way to get around float precision
pi = 3.14159
print(str(pi) == str(3.14159))
```

    True
    


```python
# Testing strings
string1 = "Memorial"
string2 = "Union"
if len(string1) > len(string2):
    print(string1, string2)
elif len(string1) == len(string2):
    print("The strings have equal length")
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
# Results
# 1. Ensure it works:
print(str(a) == str(b))
# 2. 
my_age = 27
my_name = "M"
their_age = 26
their_name = "Anais"
if my_age > their_age:
    print(my_name, "is older than",their_name)
else:
    print(their_name,"is older than",my_name)
# 3.
final_grade_point = 2
if final_grade_point >= grades["AB"]:
    print("I'd be happy.")
elif final_grade_point >= grades["BC"]:
    print("I'd be fine.")
else:
    print("I'd be disappointed.")
```

    True
    M is older than Anais
    I'd be disappointed.
    
