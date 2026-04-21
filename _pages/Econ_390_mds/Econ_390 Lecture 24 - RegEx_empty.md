---
layout: single
sitemap: false
permalink: /pages/Econ_390_SP26_L24/
title: Econ 390 Lecture 24
---

[Download Jupyter Notebook Empty](https://m-mcmain.github.io/files/Econ390SP26/Lectures/Lecture24_RegEx_empty.ipynb)

Download Jupyter Notebook Completed

# Econ 390 - Lecture 24: Regular Expression (RegEx)
Today we'll be talking about Regular Expression (RegEx), which is an incredibly in-depth and widely used (basically every coding language can use RegEx). You can find a nice chapter in [Turrell](https://aeturrell.github.io/coding-for-economists/text-regex.html) and a small section in [McKinney](https://wesmckinney.com/book/data-cleaning#text_string_manip_re) dedicated to regex.


```python
import re
text = "Let's try #21 for $15. Are you listening?"
text1 = "Here is an example string. We can have this be as long as we want!"
text2 = "And really include anything. This is lecture 23 and this will be useful for problem set 11."
text3 = "Coffee is like $3.50 now, gas is above $4, it's getting out of control!"
big_text = text + "\n" + text1 + "\n" + text2 + "\n" + text3
print(big_text)
```


```python
# r as treating the string as "raw"

```


```python
# Regular Expression Basics - match checks the beginning of the string

```


```python
# search finds where it is in the string

# methods on match type


```


```python
# findall gives you a list of all of the matches in the string

```


```python
# split does exactly that to the string where the match occurs

```

## Special Characters


```python
# Digits

# and converse

```


```python
# "Word" text

# and converse

```


```python
# Whitespace

# and converse

```


```python
# End of string

```


```python
# Anything

```

## Quantifiers & Metacharacters


```python
# {m} exactly m occurences of the preceeding character

```


```python
# {n,m} between n and m occurences of the preceeding character

```


```python
# * zero or more

```


```python
# + one or more

```


```python
# ? optional!

```


```python
# ^ start of string/line

```


```python
# $ end of string/line

```


```python
# \b represents a boundary

```


```python
# \B converse of boundary

```

## Ranges


```python
# [character] looks for those characters

```


```python
# [^character] looks for NOT those characters

```


```python
# [character-character] looks for anything in the range

```

## Tying It All Together


```python
# Capitalized words

```


```python
# All words or numbers with no decimals

```


```python
# Numbers with a character before them

```


```python
# E-Mails
emails = """Dave dave@google.com
Steve steve@gmail.com
Rob rob@gmail.com
Ryan ryan@yahoo.com"""

```


```python
# Emails separately using "Capture Groups"

```


```python
# Getting Crazy
str_ranges = "This job pays gbp 30500.00 to 35000 per year. Apply at number 100 per the below address."
```

## Practice - RegEx
When filling out the practice, try as hard as you can to keep the RegEx queries general instead of specific to the string.
1. Use findall to extract all numbers in `salary_string` (not considering periods, so you get 13 results here)
2. Extract all numbers letting periods be optional (you should get 4 results here)
3. Extract all ranges of numbers, i.e. allowing for non-letters between multiple numbers (you should get 2 results here)
4. Extract only ranges of numbers that begin with a dollar sign (you should get 1 result here)


```python
# New strings:
salary_string = "Salary Pay in range $9.00 - $12.02 but you must start at 8.00 - 8.30 every morning."
```
