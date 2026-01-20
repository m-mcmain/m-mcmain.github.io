---
layout: single
title: "Econ 390 Lecture 1"
sitemap: false
permalink: /pages/Econ_390_SP26_L1/
---

[Download Jupyter Notebook](https://m-mcmain.github.io/files/Econ390SP26/Lecture1_Introduction.ipynb)

# Welcome to Econ 390 - Introduction Programming: Economic Data
This class will introduce you to programming, specifically through the lens of working with economic data. We will be using Python as our language of choice, though once you learn one language it's very easy to learn more!

That being said, there is *another* course in the Economics Department that teaches you how to code using Python, and that is **Econ 570**. Econ 570 will (generally) *assume* you have experience with Python and know (or can learn quickly) Pandas and Matplotlib.

Perhaps unsurprisingly, the intention of this course is to prepare students who have no (or very little) prior coding experience for Econ 570. This course is **not** meant for students who are *already comfortable with Python*. If you are the latter student, you will be very bored throughout the semester in this course and are potentially taking space from students who could genuinely use an introduction to Python through the Economics Department.

## Waitlist Policy
Students will be admitted from the waitlist very simply based on their spot in line. I cannot guarantee that those spots will open up, but I would highly recommend attending lectures in the meantime so you are not behind.

## Class Meetings
- Attendance will be very important in this class
- The Jupyter Notebooks that I fill out in class will be uploaded on the [course website](https://m-mcmain.github.io/teaching/econ-370)
    - I'll upload the blank version before class so you can download it before lecture begins
    - I'll also upload the filled in version after class is over
    - If you are unable to come to class, I would still recommend taking the time to download the blank version of the lecture and manually type it out while you are going through *as if you were in lecture* as a way to simulate the experience
        - I'm very happy to help fill in any gaps during Office Hours as well!
- I am relatively easy to distract, so please don't have any side conversations while the lecture is going on
- But if you are confused or have any questions while we're going, please **don't be afraid to interrupt with questions**. I am willing to bet someone else is wondering the same thing and will appreciate you speaking up!
- You will absolutely need access to a laptop and a secure internet connection throughout this semester. If you do not have a laptop already, the University has both a [short term](https://it.wisc.edu/services/equipment-checkout/) and a [long term](https://it.wisc.edu/services/computer-lending-program/) process for borrowing laptops (I would recommend the long term for the sake of consistency).

## Textbook
The textbook for this course will be primarily [Python for Data Analysis 3E](https://wesmckinney.com/book/) and secondarily [Coding for Economists](https://aeturrell.github.io/coding-for-economists/) which are fully available for free! I will try to make it clear which material come from where at the top of the Notebooks.

## Course Calendar
You can find a course calendar on the [course website](https://m-mcmain.github.io/teaching/econ-370). Since it's my first time teaching this course, some things may be faster or slower than expeted but I will guarantee that **Problem Sets** and **Exams** will not change due dates at all.

## Grading
I will take the better of the following two grading schemes:

**Raw Grade** \
[92, 100] = A \
[88, 92) = AB \
[82, 88) = B \
[78, 82) = BC \
[70, 78) = C \
[60, 70) = D

**Percentile in Class** \
[75, 100] = A \
[50, 75) = AB \
[30, 50) = B \
[10, 30) = BC \
[0, 10) = C, D, F

I.e. the "curve" will never hurt you, it can only help. I will happily give you all A's if you earn it!

### Grading Scheme
The final grade for student $i$ is calculated using the following equation:

$$
G_{i}^{final} = 40 \times \frac{Points_{i}^{PS}}{Points^{PS}} + 20 \times \frac{Points_{i}^{Midterm}}{Points^{Midterm}} + 20 \times \frac{Points_{i}^{Final}}{Points^{Final}} + 20 \times \frac{Points_{i}^{Attendance}}{Points^{Attendance}}
$$

Problem Sets ($PS$) will be worth 40% of your final grade
- There will be **twelve** Probem Sets throughout the semester
- They will be due **Monday's at 5 PM** the week after the course material is covered.
- The first Problem Set will be due on **Monday January 26th at 5 PM**
- Late problem sets will have their grade reduced by 20% for every day they are late
- You are absolutely welcome to work with other classmates and consult the internet when working with the Problem Sets, however what you turn in must be *your own*
    - Students whose code is *identical* to another student's will receive a 0 (this is very easy to avoid and incredibly unlikey to occur randomly)
    - If you use any LLMs/Generative AI please include copies of the queries you used and responses you got
    - While they are a helpful tool, don't let them replace actually learning the course material! The exams will be much harder for you if you are unable to engage with the course material without Generative AI.

The Midterm Exam will be worth 20% of your final grade
- It will be held **in person** during our normal class session on **Thursday March 5th, 2026**
- If you know you cannot make this date for some reason, let me know ASAP so we can figure out how to resolve this
- It will be 100% handwritten and modelled similarly to Econ 570 exams.

The Final Exam will be worth 20% of your final grade
- The Final Exam will be held **in person** on **Friday May 8th, 2026 from 2:45-4:45 PM**
- If you have another exam at the exact same time let me know and we will figure something out

Attendance will be worth 20% off your final grade
- Attendance will be taken using Tophat at the end of class, which can be accessed from Canvas.
- If you do not want to take attendance using Tophat you're welcome to come up and "sign in" on a piece of paper at the end of class.

# Introduction
Thanks in large part to the internet, the world is a very data driven place. Economists *especially* work with data to understand and analyze the world around us. As a result, we need to decide *how* we are going to work with the data. Options include:
- General purpose programming languages like Julia or Python
- Languages specifically taylored for statistics such as R or Stata
- Languages optimized for working with large matrices like Matlab or Gauss
- Spreadsheets such as Excel or Google Sheets
Generally, many of these options will work for any given task! Preference will be up to you. However, there is nuance for when some might be better suited for what you're specifically hoping to do.

# When to Use Python
Python, with the help of some of the packages we will be using during the course, is a very good middle ground between what I consider a "Computer Programming" language (Java, C++) and a "Data Analysis" language (R or Stata). This allows for versatility, especially when working with APIs to scrape data online, while still allowing for robust data cleaning and visualization.

# Examples


```python
# Import packages
import pandas as pd
import pandas_datareader.data as web
import matplotlib.pyplot as plt
# Get monthly Yuan-per-dollar exchange rate
# fred tells DataReader to use the FRED repository
# EXCHUS tells DataReader which data series to get
# start tells DataReader we want data from 1990 onward
exchus = web.DataReader('EXCHUS',
'fred',
start='1990-01-01')
# Plot the exchange rate over time (labeling the axes)
plt.plot(exchus.index, exchus['EXCHUS'], 'b' )
plt.xlabel('Date')
plt.ylabel('Yuan per Dollar')
plt.show()
```


    
![png](images/L1_output_2_0.png)
    



```python
# Import packages
import pandas as pd
import pandas_datareader.data as web
import matplotlib.pyplot as plt
# List the data series we would like to plot
series_list = ['EXCHUS', 'EXJPUS', 'EXCAUS', 'EXUSEU']
# List the units for each y axis
units = ['Chinese Yuan per USD',
'Japanese Yen per USD',
'Canadian Dollar per USD',
'USD per Euro']
# Read the data (passing list of codes rather a single code)
ex_many = web.DataReader(series_list, 'fred', start='1990-01-01')
# Plot the exchange rate over time (labeling the axes)
fig, ax = plt.subplots(2, 2, figsize=(15,6))
for series, unit, axi in zip(series_list, units, fig.axes) :
    axi.plot(ex_many.index, ex_many[series], 'r')
    axi.set_ylabel(unit)
```


    
![png](images/L1_output_3_0.png)
    


# Setting up Python & Jupyter

## Python
We'll need to start by [installing Python](https://www.python.org/downloads/). Follow the link and click on the download for the appropriate operating system. It's best to install the newest version, but versions 3.11 and newer should do. If you already have Python installed - great! You don't need to reinstall.

## Jupyter
Now that Python is installed, your computer will be able to interface with it. There are many different compilers for Python that exist, but for this class I am going to be using Jupyter. For one, notebooks will make it very easy for you to follow along in class as I can prepare them ahead of time. It will also provide a uniform method of turning in homework. That being said, if you prefer to use a different IDE you're welcome to, I just won't be able to provide any tech support if things go wrong.

First you will need to install [Anaconda](https://www.anaconda.com/download). Unfortunately, you will need to create an account for free using your wisc email. I have not had any annoyances from creating an account.

Once you do that you can select the appropriate "Distribution Installers" for your operating system.
- For Mac you'll need to know what type of CPU chip you have
- If you're unsure, you can go to "About This Mac" in the Apple Menu

Then you can open up the Anaconda Navigator by searching for it in the taskbar (Windows) or Application folder (Mac)! Once the Anaconda Navigator is open you'll be able to open Jupyter Notebooks and interact with them as needed.
