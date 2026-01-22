# Econ 390 - Lecture 2: Jupyter Notebook

At the end of last lecture, we downloaded Anaconda Navigator, which includes Jupyter Notebook. Open up the Anaconda Navigator and begin a Jupyter Notebook.

You'll notice it brings you to a screen that looks like a file directory. I would recommend you make a folder dedicated to *just this class* as a way to keep everything together. Perhaps even having different folders for lectures and Problem Sets. You'll also notice, you can access these files through your own file explorer! So you don't need Jupyter open to copy/paste these files.

When you open a Jupyter Notebook, it should start with a cell at the top. It defaults to code, but you can change it to "Markdown" (which is what I'm using for this block) or "Raw" (which we won't really use). Code cells are going to be our bread and butter for actually writing and running code.

## Compiled vs. Interpreted Languages
Compiled Languages (e.g. C++) are coding languages where you write your code, then you "compile" the code, then you run the compiled code as a program.

Interpreted languages (e.g. Python) are coding languages where you write your code, then run the code using an interpreter.

Interpreted Languages are good because they're generally very quick to get off the ground and run, plus they're easy to transfer from one platform to another. The downside is, the entire code needs to be run everytime, an interpreter needs to be installed anywhere you want to run the code, and they can be a bit slow.

But, for the purposes of working with economic data, they work great! We don't *really* ask it to do anything crazy and we often have many different machines we work on.

## Three Ways to Run Python Code
1. Launch Python on Command Line
2. Write your code in an Integrated Development Environment (IDE) and run it like a script
3. Use Jupyter Notebook to write the code interactively

## Anaconda Navigator
To open the Anaconda Navigator, you can either search for it in the taskbar on Windows or find it in your Application folder on Mac.

It might take a while for it to load in as it sets everything up (and for Mac users it will pull up a terminal, this is normal!). Then you can click on Notebook to launch it (or use JupyterLab, either one will work, but I have a slight preference for Notebook). From there you should see a file directory where I would recommend navigating to a folder you like to keep course work in and add a folder for this class. In there you can create a new notebook with a Python 3 kernel and code along with me! Alternatively, you can navigate to where you downloaded this file and click on it to open it up.

Some useful things to note:
1. To run cells, you can either click on the "Play" button in the header or  `Control + Enter` to just run the cell or `Shift + Enter` to run the cell and advance or `Shift + Alt` to run the cell and insert a cell below no matter what
2. You can change cells to Markdown by pressing `M` while the cell is highlight (but while you're not in it!) or to Code by pressing `Y`
3. There is a bunch of options you can see by hovering to the top right of the cell you're in
   - You can duplicate the cell
   - Push it up or down in the order
   - Add a cell above or below
   - Delete the cell
4. The `Run` tab at the top will give you a ton of options for running one (or many) cells.
5. The `Kernel` tab is useful if something gets messed up in your code and you need to start over
6. You can rename the file just by clicking on the name in the top right


```python

```


```python

```


```python

```


```python

```


```python

```


```python

```

## Closing Out
To close out of a Jupyter Notebook it's good to make sure you've saved first! Then you can go to `File > Close and Shut Down Notebook` and it should automatically close the tab (and *should* warn you if you haven't saved). You can just exit out of the tab but the kernel will technically still be running and taking up resources from your laptop.

Then, to close out of Notebook entirely go to `File > Shut Down > Confirm` and you should be notified that it has shut down and you can close the tab (this will also automatically end all of the other kernels you are running). You can close out of Anaconda Navigator like normal programs.

## Practice - Jupyter
1. Open Jupyter Notebook again and create a new Notebook called "Econ390_lec2_practice". Make the first cell a Markdown Cell and write your name in it.
2. Run the cell, save the notebook, then close and shut it down.
3. Use the file browser to open up Econ390_lec2_practice and then use the file menu to make a copy of it and name the copy "Econ390_lec2_practice_v2"
4. In Econ390_lec2_practice, write down three of your favorite classes you've taken so far at UW Madison. Save the notebook and shut it down.
5. Can you see both files in the Jupyter Home?
6. Can you find the files on your laptop? Whether this is by knowing the file location or searching for it by name. (This will be important for turning in homeworks)
