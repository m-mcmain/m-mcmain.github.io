---
layout: single
sitemap: false
permalink: /pages/Econ_390_SP26_L3_teaching/
---
[Download Jupyter Notebook Empty](https://m-mcmain.github.io/files/Econ390SP26/Lecture3_Markdown_empty.ipynb)

Download Jupyter Notebook Completed

# Econ 390 - Lecture 3: Markdown
Today we will be learning how to use Markdown. It is useful both in Jupyter Notebook but it also shows up in many other places! E.g. github websites, notion.io, Discord

## Headings: Make this match up with [McKinney](https://wesmckinney.com/book/preliminaries)!

# 1  Preliminaries

> This Open Access web version of *Python for Data Analysis 3rd Edition* is now available as a companion to the [print and digital editions](https://amzn.to/3DyLaJc).

## 1.1 What Is This Book About?

This book is concerned with the nuts and bolts of manipulating, processing, cleaning, and crunching data in Python. 

>[!NOTE]
>Some might characterize much of the content of the book as "data manipulation" as opposed to "data analysis." We also use the terms wrangling or munging to refer to data manipulation.

### What Kinds of Data?

When I say “data,” what am I referring to exactly?

## In-Line: Only slightly more work than Microsoft Word

*Italics* are used for emphasis, and also for the titles of things like books, plays, newspapers, and movies.  The highest grossing film of all time is *Gone with the Wind*.

**Bold** is used for even greater emphasis.  **Never count your chickens before they hatch!**

~~Strikethrough~~ is used when we wish to make it obvious that a change was made. ~~Madison is in Minnesota.~~  Actually, Madison is in Wisconsin.

`Monospace` is used for file paths, file names, and computer code.  On my laptop, Anaconda installed itself into the `/anaconda3/` folder.

How do we underline?  Is it _this_?  Or __this__?

### HTML Use:

<center> You can force text to be centered! </center>
<font color = "green"> This text is green! </font>

## Text Block:

### You can create block quotes:

> "You miss 100% of the shots you don't take" - Michael Jordan
> 
> -Michael Scott

### Lists can be useful:

- First Item
- Second Item
- Third Item

### They can even be numbered:

1. First things first
2. Second
3. Third

### Sub-Items are possible:

- Breakfast
    - Eggs
        - Only half a dozen
    - Waffles
- Dinner
    - Tofu
 
### You can even make lists with check marks:

- [x] Econ 390 Homework
- [ ] Econ 461 Homework
- [ ] Philos 560 Essay

### You can manually make tables:

| Team | Wins | Losses |
|-|-|-|
| Milwaukee Brewers | 97 | 65 |
| Philadelphia Phillies | 96 | 66 |
| Toronto Blue Jays | 94 | 68 |

But you're likely better off by using `df.to_markdown()` or the website [Markdown Table Generator](https://www.tablesgenerator.com/markdown_tables)

### You can also include code:

By telling it what language you are using, it will know to highlight key words
```python
import pandas as pd
df = pd.DataFrame([[1, 2, 3], [4, 5, 6], [7, 8, 9]]),
                  columns=['a', 'b', 'c'])
```

### Support for math:

Dollar signs will allow for "math mode" where it allows for equations and symbols using LaTeX notation in line $ f(L, K) = A L^\alpha K^{1-\alpha} $

Or you can use double dollar signs to center it on a new line:
$$ \frac{\partial}{\partial L}f(L,K) = \alpha A \left(\frac{K}{L}\right)^{1-\alpha}$$

### Links

You can even [hyperlink your favorite websites](https://fred.stlouisfed.org/) seamlessly in the text or include an image from online: ![JPow](https://upload.wikimedia.org/wikipedia/commons/thumb/f/f0/Jerome_H._Powell%2C_Federal_Reserve_Chair_%28cropped%29.jpg/500px-Jerome_H._Powell%2C_Federal_Reserve_Chair_%28cropped%29.jpg)

Or, you can link to [other sections in the notebook](#Econ-390---Lecture-3:-Markdown)! Or make a nice little Table of Contents:
1. [Title](#Econ-390---Lecture-3:-Markdown)
2. [Headings](#Headings:-Make-this-match-up-with-the-textbook!)
3. [In-Line](#In-Line:-Only-slightly-more-work-than-Microsoft-Word)
4. [Text Block](#Text-Block:)
6. [Other Markdown Resources](#Other-Markdown-Resources:)


## Practice Markdown:
1. Make a new notebook titled "Lecture3_Practice"
    - Make the first cell say "Econ 390 - Lecture 3 Practive" as a Header
    - Under the header, make a numbered list of your classes this semester. Order them in chronological order of their first day of class.
    - Bold the course you are most excited for. Italicize the course furthest from where you live. Strikethrough the course you are most likely to fall asleep during.
    - Below that, type the equation E = mc^2 using LaTeX typeset.
2. Make a second cell that is a code cell containing `hw = "Hello World!"`, a new line, and `print(hw)`
3. Make a third cell that is a markdown cell containing the code you just ran formatted as a code block with correct syntax highlighting
4. Run all of the cells and make sure they work as expected!

# Other Markdown Resources:

- [Github Markdown Guide](https://docs.github.com/en/github/writing-on-github/getting-started-with-writing-and-formatting-on-github/basic-writing-and-formatting-syntax)
- [Markdown Cheat Sheet](https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet)
