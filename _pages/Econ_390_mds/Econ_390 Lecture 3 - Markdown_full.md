---
layout: single
sitemap: false
permalink: /pages/Econ_390_SP26_L3_full/
---
[Download Jupyter Notebook Empty](https://m-mcmain.github.io/files/Econ390SP26/Lectures/Lecture3_Markdown_empty.ipynb)

[Download Jupyter Notebook Completed](https://m-mcmain.github.io/files/Econ390SP26/Lectures/Lecture3_Markdown_full.ipynb)

# Econ 390 - Lecture 3: Markdown
Today we will be learning how to use Markdown. It is useful both in Jupyter Notebook but it also shows up in many other places! E.g. Github websites, notion.io, Discord

## Headings: Make this match up with [McKinney](https://wesmckinney.com/book/preliminaries)!

# 1  Preliminaries

> This Open Access web version of Python for Data Analysis 3rd Edition is now available as a companion to the print and digital editions.

## 1.1 What Is This Book About?

This book is concerned with the nuts and bolts of manipulating, processing, cleaning, and crunching data in Python.

>[!NOTE]
> Some might characterize much of the content of the book as "data manipulation" as opposed to "data analysis." We also use the terms wrangling or munging to refer to data manipulation.

### What Kinds of Data?

When I say “data,” what am I referring to exactly?

## In-Line: Only slightly more work than Microsoft Word
*Italics* are used emphasis, but also for titles of books, plays, newspapers, and movies. The highest grossing film 
(in real terms) is *Gone with the Wind*.

**Bold** is used for even more emphasis. **Never count your chickens before they hatch!**

~~Strikethrough~~ useful if you want to make it clear there was a mistake that's updated. ~~*Avatar*~~ *Gone with the Wind* is the highest grossing film in real terms.

`Monospace` is used for file paths, file names, and computer code. Anaconda installed itself into the `/anaconda3/` folder.

How do we underline? __test__

### HTML Use:
<center>Center this text</center>
<font color="Green">I don't any Lorax quotes.</font>

## Text Block:
### You can make block quotes:
> > "You miss 100% of the shots you don't take" -Michael Jordan
> 
> -Michael Scott

### Lists can be useful
- First item
- Second
- Third

### They can even be numbered
1. Begin with the first
2. Then the second
3. And the third
5. Test

### Sub-Items are possible
- Breakfast
    - Eggs
        - Only half a dozen
    - Waffles
- Dinner
    - Tofu

### Lists that can be checked off
- [x] Econ 390 Homework
- [ ] Econ 461 Homework
- [ ] Philos 560 Essay

### Tables can be made
| Team | Wins | Losses |
| - | - | - |
| Milwaukee Brewers | 97 | 65 |
| Philedelphia Phillies | 96 | 66 |
| Toronto Blue Jays | 94 | 68 |

You can use `df.to_markdown()` or the website [this website](https://tablesgenerator.com/markdown_tables).

### You can actually the code to look right
``` Python
import pandas as pd
df = pd.DataFrame([[1,2,3],[4,5,6],[7,8,9]]), columns=["a","b","c"])
```

### Support for math:
Dollar signs allow for "math mode" where it allows for equations and symbols using LaTeX notation in line $ f(L,K) = A L^\alpha K^{1-\alpha} $

To give an equation it's own line and center it, use double dollar signs. $$\frac{d}{dL} f(L,K) = \alpha A (\frac{K}{L})^{1-\alpha} $$

### Links
You can hyperlink [your favorite websites](https://my.wisc.edu). You can also include images from online: 

![jpowe](https://upload.wikimedia.org/wikipedia/commons/thumb/f/f0/Jerome_H._Powell%2C_Federal_Reserve_Chair_%28cropped%29.jpg/500px-Jerome_H._Powell%2C_Federal_Reserve_Chair_%28cropped%29.jpg)

You can link to other sections of the [notebook](#1--Preliminaries)

## Practice Markdown:
1. Make a new notebook titled "Lecture3_Practice"
    - Make the first cell say "Econ 390 - Lecture 3 Practice" as a Header
    - Under the header, make a numbered list of your classes this semester. Order them in chronological order of their first day of class.
    - Bold the course you are most excited for. Italicize the course furthest from where you live. Strikethrough the course you are most likely to fall asleep during.
    - Below that, type the equation E = mc^2 using LaTeX typeset.
2. Make a second cell that is a code cell containing `hw = "Hello World!"`, a new line, and `print(hw)`
3. Make a third cell that is a markdown cell containing the code you just ran formatted as a code block with correct syntax highlighting
4. Run all of the cells and make sure they work as expected!

# Other Markdown Resources:

- [Github Markdown Guide](https://docs.github.com/en/github/writing-on-github/getting-started-with-writing-and-formatting-on-github/basic-writing-and-formatting-syntax)
- [Markdown Cheat Sheet](https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet)
