---
layout: single
sitemap: false
permalink: /pages/Econ_390_SP26_L24/
title: Econ 390 Lecture 24
---

[Download Jupyter Notebook Empty](https://m-mcmain.github.io/files/Econ390SP26/Lectures/Lecture24_RegEx_empty.ipynb)

[Download Jupyter Notebook Completed](https://m-mcmain.github.io/files/Econ390SP26/Lectures/Lecture24_RegEx_full.ipynb)

# Econ 390 - Lecture 24: Regular Expression (RegEx)
Today we'll be talking about Regular Expression (RegEx), which is an incredibly in-depth and widely used (basically every coding language can use RegEx). You can find a nice chapter in [Turrell](https://aeturrell.github.io/coding-for-economists/text-regex.html) and a small section in [McKinney](https://wesmckinney.com/book/data-cleaning#text_string_manip_re) dedicated to regex.


```python
import re
text = "Let's try #21 for $15. Are you listening?"
text1 = "Here is an example string. We can have this be as long as we want!"
text2 = "And really include anything. This is lecture 24 and this will be useful for problem set 12."
text3 = "Coffee is like $3.50 now, gas is above $4, it's getting out of control!"
big_text = text + "\n" + text1 + "\n" + text2 + "\n" + text3
print(big_text)
```

    Let's try #21 for $15. Are you listening?
    Here is an example string. We can have this be as long as we want!
    And really include anything. This is lecture 24 and this will be useful for problem set 12.
    Coffee is like $3.50 now, gas is above $4, it's getting out of control!
    


```python
# r as treating the string as "raw"
print(r"test\nwas")
```

    test\nwas
    


```python
# Regular Expression Basics - match checks the beginning of the string
print(re.match("is", text1))
```

    None
    


```python
# search finds where it is in the string
print(re.search(" is", "here is what this is "))
# methods on match type
print(re.search(" is", text1).start())
print(re.search(" is", text1).end())
print(re.search(" is", text1).group(0))
```

    <re.Match object; span=(4, 7), match=' is'>
    4
    7
     is
    


```python
# findall gives you a list of all of the matches in the string
re.findall(" Is", "here is what this is ")
```




    []




```python
# split does exactly that to the string where the match occurs
re.split(" is ", text1)
```




    ['Here', 'an example string. We can have this be as long as we want!']



## Special Characters


```python
# Digits
print(re.findall("\d", text2))
print(re.findall("\d\d", text2))
# and converse
print(re.findall("\D", text2))
print(re.findall("\D\D", text2))
```

    ['2', '4', '1', '2']
    ['24', '12']
    ['A', 'n', 'd', ' ', 'r', 'e', 'a', 'l', 'l', 'y', ' ', 'i', 'n', 'c', 'l', 'u', 'd', 'e', ' ', 'a', 'n', 'y', 't', 'h', 'i', 'n', 'g', '.', ' ', 'T', 'h', 'i', 's', ' ', 'i', 's', ' ', 'l', 'e', 'c', 't', 'u', 'r', 'e', ' ', ' ', 'a', 'n', 'd', ' ', 't', 'h', 'i', 's', ' ', 'w', 'i', 'l', 'l', ' ', 'b', 'e', ' ', 'u', 's', 'e', 'f', 'u', 'l', ' ', 'f', 'o', 'r', ' ', 'p', 'r', 'o', 'b', 'l', 'e', 'm', ' ', 's', 'e', 't', ' ', '.']
    ['An', 'd ', 're', 'al', 'ly', ' i', 'nc', 'lu', 'de', ' a', 'ny', 'th', 'in', 'g.', ' T', 'hi', 's ', 'is', ' l', 'ec', 'tu', 're', ' a', 'nd', ' t', 'hi', 's ', 'wi', 'll', ' b', 'e ', 'us', 'ef', 'ul', ' f', 'or', ' p', 'ro', 'bl', 'em', ' s', 'et']
    


```python
# "Word" text
print(re.findall("\w", text))
# and converse
print(re.findall("\W", text))
```

    ['L', 'e', 't', 's', 't', 'r', 'y', '2', '1', 'f', 'o', 'r', '1', '5', 'A', 'r', 'e', 'y', 'o', 'u', 'l', 'i', 's', 't', 'e', 'n', 'i', 'n', 'g']
    ["'", ' ', ' ', '#', ' ', ' ', '$', '.', ' ', ' ', ' ', '?']
    


```python
# Whitespace
print(re.findall("\s", text))
# and converse
print(re.findall("\S", text))
```

    [' ', ' ', ' ', ' ', ' ', ' ', ' ']
    ['L', 'e', 't', "'", 's', 't', 'r', 'y', '#', '2', '1', 'f', 'o', 'r', '$', '1', '5', '.', 'A', 'r', 'e', 'y', 'o', 'u', 'l', 'i', 's', 't', 'e', 'n', 'i', 'n', 'g', '?']
    


```python
# End of string
print(re.findall("\d\d.\Z",text2))
```

    ['12.']
    


```python
# Anything
print(re.findall(r"\w\w\s.\d",big_text))
```

    ['ry #2', 'or $1', 're 24', 'et 12', 'ke $3', 've $4']
    

## Quantifiers & Metacharacters


```python
# {m} exactly m occurences of the preceeding character
re.findall("\wl{2}",text2)
```




    ['all', 'ill']




```python
# {n,m} between n and m occurences of the preceeding character
re.findall(".l{1,3}.", "I'll go around and call on leaders lll llll.")
```




    ["'ll ", 'all ', ' le', ' lll ', 'llll.']




```python
# * zero or more
re.findall("\wl*", "I'll go around and call on leaders lll llll.")
```




    ['I',
     'll',
     'g',
     'o',
     'a',
     'r',
     'o',
     'u',
     'n',
     'd',
     'a',
     'n',
     'd',
     'c',
     'all',
     'o',
     'n',
     'l',
     'e',
     'a',
     'd',
     'e',
     'r',
     's',
     'lll',
     'llll']




```python
# + one or more
re.findall("\w+f+\w+", text3)
```




    ['Coffee']




```python
# ? optional!
re.findall(r"\$?\d\d",text)
```




    ['21', '$15']




```python
# ^ start of string/line
re.findall("^\w+",text2)
```




    ['And']




```python
# $ end of string/line
re.findall("\w+.$",big_text)
```




    ['control!']




```python
# \b represents a boundary
re.findall(r"\w?\w?is\b",big_text)
```




    ['is', 'this', 'This', 'is', 'this', 'is', 'is']




```python
# \B converse of boundary
re.findall(r"\Bis\B",big_text)
```




    ['is']



## Ranges


```python
# [character] looks for those characters
print(re.findall(r"[#\$]\d+",big_text))
```

    ['#21', '$15', '$3', '$4']
    ['2', '1', '1', '5', 'A', 'H', 'A', '2', '4', '1', '2', 'C', '3', '5', '0', '4']
    


```python
# [^character] looks for NOT those characters
print(re.findall(r"[^#\$]\d+",big_text))
```

    ['21', '15', ' 24', ' 12', '.50']
    


```python
# [character-character] looks for anything in the range
print(re.findall(r"[A-H0-9]",big_text))
```

    ['2', '1', '1', '5', 'A', 'H', 'A', '2', '4', '1', '2', 'C', '3', '5', '0', '4']
    

## Tying It All Together


```python
# Capitalized words
re.findall("[A-Z]\w*",big_text)
```




    ['Let', 'Are', 'Here', 'We', 'And', 'This', 'Coffee']




```python
# All words or numbers
re.findall("[^\s]+", text)
```




    ["Let's", 'try', '#21', 'for', '$15.', 'Are', 'you', 'listening?']




```python
# Numbers with a character before them
re.findall("[^A-Za-z0-9]\d+", text)
```




    ['#21', '$15']




```python
# E-Mails
emails = """Dave dave@google.com
Steve steve@gmail.com
Rob rob@gmail.com
Ryan ryan@yahoo.com """ + big_text
emails

re.findall(r"[A-Za-z0-9]+@[A-Za-z0-9]+\.[A-Za-z]{2,4}",emails)
```




    ['dave@google.com', 'steve@gmail.com', 'rob@gmail.com', 'ryan@yahoo.com']




```python
# Emails separately using "Capture Groups"
print(re.findall(r"([A-Za-z0-9._%+-]+)(@[A-Za-z0-9.-]+)(\.[A-Za-z]{2,4})",emails))
print(re.findall(r"([A-Za-z0-9._%+-]+)(?:@[A-Za-z0-9.-]+)(?:\.[A-Za-z]{2,4})",emails))
```

    [('dave', '@google', '.com'), ('steve', '@gmail', '.com'), ('rob', '@gmail', '.com'), ('ryan', '@yahoo', '.com')]
    ['dave', 'steve', 'rob', 'ryan']
    


```python
# Getting Crazy
str_ranges = "This job pays gbp 30500.00 to 35000 per year. Apply at number 100 per the below address."
sal_r_sal = r"\b([0-9]{1,7}(:?\.)?(:?[0-9]{1,2})?(\s?-\s?|\s?to\s?)[0-9]{1,6}(:?\.)?([0-9]{1,2})?(\s?per))"
re.findall(sal_r_sal, str_ranges)
```




    [('30500.00 to 35000 per', '.', '00', ' to ', '', '', ' per')]



## Practice - RegEx
When filling out the practice, try as hard as you can to keep the RegEx queries general instead of specific to the string.
1. Use findall to extract all numbers in `salary_string` (not considering periods, so you get 13 results here)
2. Extract all numbers letting periods be optional (you should get 4 results here)
3. Extract all ranges of numbers, i.e. allowing for non-letters between multiple numbers (you should get 2 results here)
4. Extract only ranges of numbers that begin with a dollar sign (you should get 1 result here)


```python
# New strings:
salary_string = "Salary Pay in range $9.00 - $12.02 but you must start at 8.00 - 8.30 every morning 10."
# Results:
# 1.
print(re.findall("\d",salary_string))
# 2.
print(re.findall("\d+\.?\d+",salary_string))
# 3.
print(re.findall("\d+\.?\d+\W+\d+\.?\d+",salary_string))
# 4.
print(re.findall("\$\d+\.?\d+\W+\$\d+\.?\d+",salary_string))
```

    ['9', '0', '0', '1', '2', '0', '2', '8', '0', '0', '8', '3', '0', '1', '0']
    ['9.00', '12.02', '8.00', '8.30', '10']
    ['9.00 - $12.02', '8.00 - 8.30']
    ['$9.00 - $12.02']
    
