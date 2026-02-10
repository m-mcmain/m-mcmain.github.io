# Econ 390 - Lecture 7: Loops

Today we will go through Loops and List Comprehension. These are powerful tools that allow you to do the same task over and over again until certain conditions are met. You can find relevant reading for [McKinney](https://wesmckinney.com/book/python-basics#control_for) and [Turrell](https://aeturrell.github.io/coding-for-economists/code-basics.html#loops-and-list-comprehensions).

## Loops


```python
# For loops just go through each entry after "for"
for i in range(3):
    print(i)
```

    0
    1
    2
    


```python
# Here is how range works
print(list(range(3)))
print(type(range(3)))
```

    [0, 1, 2]
    <class 'range'>
    


```python
# You can print through lists by indexing
var_names = ["GDP", "POP", "INVEST", "EXPORTS"]
for i in range(4):
    print(var_names[i])
```

    GDP
    POP
    INVEST
    EXPORTS
    


```python
# Or by directly referencing the list
for VARIABLE in var_names:
    print(VARIABLE)
```

    GDP
    POP
    INVEST
    EXPORTS
    


```python
# You can utilize enumerate for lists as well
for i, name in enumerate(var_names):
    print(name, "is the", i+1, "entry")
```

    GDP is the 1 entry
    POP is the 2 entry
    INVEST is the 3 entry
    EXPORTS is the 4 entry
    


```python
# If you don't like indexing with 0 you can start at 1 instead
for i, name in enumerate(var_names, start=1):
    print(name, "is the", i, "entry")
```

    GDP is the 1 entry
    POP is the 2 entry
    INVEST is the 3 entry
    EXPORTS is the 4 entry
    


```python
# You can add elif statements if you want it to match
for i, name in enumerate(var_names, start=1):
    if i == 1:
        print(name, " is the ", i, "st entry", sep ="")
    elif i == 2:
        print("{} is the {}nd entry".format(name, i))
    elif i == 3:
        print("The {1}rd entry is {0}".format(name, i))
    else:
        print("{var} is the {num}th entry".format(var=name, num=i))

# Format has other useful functions
a = "{:,}".format(1200340)
print(a)
pi = 3.14159
print("{:.2f}".format(pi))

print(var_names)
```

    GDP is the 1st entry
    POP is the 2nd entry
    The 3rd entry is INVEST
    EXPORTS is the 4th entry
    1,200,340
    3.14
    ['GDP', 'POP', 'INVEST', 'EXPORTS']
    


```python
# You can force out of a loop by using break
for name in var_names:
    print(name)
    if name == "INVEST":
        break
    print("again!")
```

    GDP
    again!
    POP
    again!
    INVEST
    EXPORTS
    again!
    


```python
# You can reference multiple lists using indexing
first_names = ["Adam", "Karl", "Aristotle"]
last_names = ["Smith", "Marx", ""]
for i in range(3):
    print(first_names[i], last_names[i])
```

    Adam Smith
    Karl Marx
    Aristotle 
    


```python
# Or taking advantage of zip
for f, l in zip(first_names, last_names):
    print(f, l)
```

    Adam Smith
    Karl Marx
    Aristotle 
    


```python
# This is what zip does
print(zip(first_names,last_names))
print(list(zip(first_names,last_names)))
```

    <zip object at 0x000001E299660780>
    [('Adam', 'Smith'), ('Karl', 'Marx'), ('Aristotle', '')]
    


```python
# While loops exist, but are generally less common
i = 0
while i < 3:
    print(i)
    i += 1
```

    0
    1
    2
    


```python
# Input is a thing, though not very helpful for economics
x = "go"
print('Type stop to end this loop!')
while x != "stop":
    x = input()
```

    Type stop to end this loop!
    

     go
     keep going
     stop
    

## Practice - Loops
1. Write a for loop that calculates and saves the previous 1, 2, and 3 years in a list
   - Then, unpack the list and save them as years_ago_1, years_ago_2, and years_ago_3 appropriately
2. Write a for loop that goes through the most recent inflation in each country, using the format method to print out "X recently experienced low/high/hyper inflation of Y%" where X is the country and Y is their inflation. Define low as less than or equal to 2%, high as between 2% and 50%, and hyper as above 50%.


```python
year = 2026
inflation_dict = {'United States':2.9, 'United Arab Emirates':1.7, 'Angola':4.0, 'Venezuela':219.9}
# Results:
# 1.
years_ago = []
for i in range(3):
    years_ago.append(year-(i+1))
years_ago_1, years_ago_2, years_ago_3 = years_ago
print(years_ago, years_ago_1, years_ago_2, years_ago_3) 

# 2. 
for country in inflation_dict:
    if inflation_dict[country] <= 2:
        print("{c} recently experienced low inflation of {inflation}%".format(c=country,inflation=inflation_dict[country]))
    elif inflation_dict[country] <= 50:
        print("{c} recently experienced high inflation of {inflation}%".format(c=country,inflation=inflation_dict[country]))
    else:
        print("{c} recently experienced hyper inflation of {inflation}%".format(c=country,inflation=inflation_dict[country]))
```

    [2025, 2024, 2023] 2025 2024 2023
    United States recently experienced high inflation of 2.9%
    United Arab Emirates recently experienced low inflation of 1.7%
    Angola recently experienced high inflation of 4.0%
    Venezuela recently experienced hyper inflation of 219.9%
    

## List Comprehension


```python
# Lists can internally do it
sq = [num**2 for num in range(3)]
print(sq)
```

    [0, 1, 4]
    


```python
# Same with strings
names = ["Sophie", "Andrew", "Jacob", "Jash"]
init = [name[0] + "." for name in names]
print(init)
```

    ['S.', 'A.', 'J.', 'J.']
    


```python
# And ifs
init = [name[0] + "." for name in names if len(name) > 4]
print(init)
```

    ['S.', 'A.', 'J.']
    


```python
# Even if elses
init = [name[0] + "." if len(name) > 4 else name for name in names]
print(init)
```

    ['S.', 'A.', 'J.', 'Jash']
    

## Practice - List Comprehension
1. Use list comprehension to convert this list of dollars into a list of M-Bills, where one M-Bill is 1.5 dollars.
`[1, 5, 20, 100]`
2. Use list comprehension to convert this integer into a list of singular numbers. (Hint: What have we seen before that separates singular characters in lists?)
`a = 32651`
3. Using list comprehension, create two lists, one of the even numbers and one of the odd numbers of the following list. (Hint: % is "modulo", which will return the leftover from division. E.g. 4%3 = 1)
`[1, 2, 3, 4, 5, 6]`


```python
# Results:
# 1.
dollars = [1, 5, 20, 100]
mbills = [1.5*d for d in dollars]
print(mbills)

#2.
a = 32651
a_list = [int(x) for x in str(a)]
print(a_list)

# 3.
nums = [1, 2, 3, 4, 5, 6]
evens = [x for x in nums if x%2 == 0]
odds = [x for x in nums if x%2 == 1]
print(evens, odds)
```

    [1.5, 7.5, 30.0, 150.0]
    [3, 2, 6, 5, 1]
    [2, 4, 6] [1, 3, 5]
    
