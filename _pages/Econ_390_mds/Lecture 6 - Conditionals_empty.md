# Econ 390 - Lecture 6: Conditionals

This lecture we will discuss the Boolean data type and implementing conditionals in if statements and loops. Conditionals are incredibly useful for limiting what happens in the code and when. At the base of a conditional is a Boolean. This is mostly inspired by [this](https://aeturrell.github.io/coding-for-economists/data-boolean.html) chapter in Turrell.


```python
# You can just call False and True
```


```python
# And, or, and not act as expected
```


```python
# You can cast bool into int, and vice verse
```


```python
# There are many operators that act as expected
```


```python
# You can create variables that use those operators, but ultimately are just bools
```


```python
# You can also do operators with all variables
```

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
```


```python
# We can add elif and else for flexibility
```


```python
# You can use and & or as well
```


```python
# You can use booleans to check lists
```


```python
# Clever way to get around float precision
```


```python
# Testing strings
```

## Practice - If Statements
1. Redo #2 in the previous practice and use what you've learned since then to get Python to recognize that `a` *is* equal to `b`. Use print for proof.
2. Create two variables, `my_age` and `my_name` which is equal to your age and name, and `their_age` and `their_name` which is equal to the age and name of someone sitting near you. Then write and if else statement that prints out a sentence remarking on who is older (referring to names).
3. Create a variable `final_grade_point` and set it equal any GPA you could get in this course. Then, using the `grades` dictionary, write and if else statement going through if you would be happy, fine, or disappointed if you actually got `final_grade_point`.


```python
grades = {'A':4.0, 'AB':3.5, 'B':3, 'BC':2.5, 'C':2.0, 'D':1.0, 'F':0.0}
```
