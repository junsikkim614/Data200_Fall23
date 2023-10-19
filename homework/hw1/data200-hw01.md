# Data 200: Data Systems for Data Analytics


# Homework 1: File Processing in Python


<font color='red'>**Due Date**: Sep 14 beginning of class </font>
---
Enter your name in the markdown cell below.

# Name:


```python
import numpy as np
import os
```

# Tasks

- Read pages 17-48 in the textbook, Bressoud and White.
- Push your completed Jupyter notebook + its exported Markdown file.

# Exercises

The file `quotes.txt` in the `data` folder contains five famous quotes. The file is organized so that the quote is on one line and then the name of the person to whom the quote is attributed on the next line.  This is repeated for 5 different quotes. Open up the file with your text editor to inspect it. 

<div class="exercise"><b>Exercise 1</b></div> 

Write Python statements to <br>

- Open the `quotes.txt` file
- Read and print the first line of the file (using the `readline()` method)
- Close the file

The output from my solution is:<br>

<code>
When you reach the end of your rope, tie a knot in it and hang on.</code>


```python
file = open(r"/Users/junsik/Documents/GitHub/Data200_Fall23/homework/hw1/data/quotes.txt", 'r')
firstline = file.readline()
print(firstline)
```

    When you reach the end of your rope, tie a knot in it and hang on.
    


<div class="exercise"><b>Exercise 2</b></div> 

Write Python statements to <br>

- Open the `quotes.txt` file
- Read all of the lines of the file using the `readlines(.)` method
- Print all the lines using a for-loop
- Close the file

The output from my solution is:<br>

<code>
When you reach the end of your rope, tie a knot in it and hang on.
Franklin D. Roosevelt
Always remember that you are absolutely unique. Just like everyone else.
Margaret Mead
The best and most beautiful things in the world cannot be seen or even touched — they must be felt with the heart.
Helen Keller
Success depends upon previous preparation, and without such preparation, there is sure to be failure.
Confucius
The journey of a thousand miles begins with one step.
Lao Tzu</code>


```python
file = open(r"/Users/junsik/Documents/GitHub/Data200_Fall23/homework/hw1/data/quotes.txt", 'r')
lines = file.readlines()
for i in range(len(lines)): 
    print(lines[i])
    
```

    When you reach the end of your rope, tie a knot in it and hang on.
    
    Franklin D. Roosevelt
    
    Always remember that you are absolutely unique. Just like everyone else.
    
    Margaret Mead
    
    The best and most beautiful things in the world cannot be seen or even touched — they must be felt with the heart.
    
    Helen Keller
    
    Success depends upon previous preparation, and without such preparation, there is sure to be failure.
    
    Confucius
    
    The journey of a thousand miles begins with one step.
    
    Lao Tzu


Run the cell below that defines a few `string` variables.


```python
s1 = "Yeah, we fancy like Applebee's on a date night"
s2 = "Got that Bourbon Street steak with the Oreo shake"
s3 = "Get some whipped cream on the top too"
s4 = "Two straws, one check, girl, I got you"
```

<div class="exercise"><b>Exercise 3</b></div> 

Write Python statements that use the `split(.)` method (remember that the default separator is any whitespace) to print out:<br>

a) The 5th word (index 4) of `s1`<br>
b) The last word of `s2`<br>

The output from my solution is:<br>

<code>
Applebee's
shake</code>


```python
split1 = s1.split()
split2 = s2.split()
print(split1[4])
print(split2[-1])
```

    Applebee's
    shake


<div class="exercise"><b>Exercise 4</b></div> 

Write Python statements that determines the number of words in the `quotes.txt` file. Specifically,
- Open the file `quotes.txt`
- Read the entire file using the `read(.)` method and assign it to a string
- Use the `split(.)` method to split the string using the default separator (whitespace)
- Use the `len(.)` method to determine the number of words
- Print the number of words.
The output from my solution is:<br>
<code>
The number of words is 85</code>


```python
file = open(r"/Users/junsik/Documents/GitHub/Data200_Fall23/homework/hw1/data/quotes.txt", 'r')
content = file.read()
content = content.split() 
length = len(content)
print("The number of words is" , length)

```

    The number of words is 85


<div class="exercise"><b>Exercise 5</b></div> 

Write Python code that processes the file `quotes.txt`, line by line, and accumulates and returns a list of tuples, one per line. Each tuple consists of the two values of the line number and the number of words on the line (line numbers in a file start at 1). Finally, print the list of tuples.  It might be helpful to review the `readNames(.)` method.

The output from my solution is:<br>
<code>
[[1, 16], [2, 3], [3, 11], [4, 2], [5, 23], [6, 2], [7, 15], [8, 1], [9, 10], [10, 2]]</code>


```python
file = open(r"/Users/junsik/Documents/GitHub/Data200_Fall23/homework/hw1/data/quotes.txt", 'r')
tuples = [] 
lines = file.readlines() 
for i in range(len(lines)): 
    line = lines[i]
    split = line.split() 
    length = len(split) 
    tuple = (i+1, length)
    tuples.append(tuple)
print(tuples)


```

    [(1, 16), (2, 3), (3, 11), (4, 2), (5, 23), (6, 2), (7, 15), (8, 1), (9, 10), (10, 2)]


<div class="exercise"><b>Exercise 6</b></div> 

Write a function `numWordsPerLine(filepath)` that processes the file as in **Exercise 5** and returns the tuple produced (this is just to give you practice writing code as functions)--we will use the function shortly. Note that `filepath` should be the path to the input file.


```python
def numWordsPerLine(filepath): 
    file = open(filepath, 'r')
    tuples = [] 
    lines = file.readlines() 
    for i in range(len(lines)): 
        line = lines[i]
        split = line.split() 
        length = len(split) 
        tuple = (i+1, length)
        tuples.append(tuple)
    print(tuples)

numWordsPerLine("/Users/junsik/Documents/GitHub/Data200_Fall23/homework/hw1/data/quotes.txt")
```

    [(1, 16), (2, 3), (3, 11), (4, 2), (5, 23), (6, 2), (7, 15), (8, 1), (9, 10), (10, 2)]


Let's now get some practice using the `os.path.join(.)` method.  Run the following code cell


```python
import os

datadir = "data"
```

# <div class="exercise"><b>Exercise 7</b></div> 

There is text file called `summerDay.txt` in the `data` folder.  Create a file path called `filepath` by using the `os.path.join(.)` method to join together `datadir` and the name of the file `summerDay.txt`.  Then call the function `numWordsPerLine(filepath)` you wrote in **Exercise 6** and pass in `filepath`.

The output from my solution is:<br>
<code>
[[1, 8], [2, 7], [3, 9], [4, 9], [5, 8], [6, 7], [7, 7], [8, 7], [9, 7], [10, 8], [11, 9], [12, 8], [13, 10], [14, 10]]</code>


```python
filepath = os.path.join(datadir,'summerDay.txt')
numWordsPerLine(filepath)
```

    [(1, 8), (2, 7), (3, 9), (4, 9), (5, 8), (6, 7), (7, 7), (8, 7), (9, 7), (10, 8), (11, 9), (12, 8), (13, 10), (14, 10)]


<div class="exercise"><b>Exercise 8</b></div> 

There is text file called `babyNames.txt` in the `data` folder as depicted below:

    22127,      Jacob
    18002,      Ethan
    17350,    Michael
    17179,     Jayden
    17051,    William
    16756,  Alexander
    
Each line of the file captures one data case/observation. The values are separated by commas, with the count occurring first and the name second, and *spaces* (not tabs)  are used to align the columns of data to make it easier for a human reader.

In the cell below, **complete the function**

    `readNamesCounts(filepath)`

that processes the filepath file and returns two lists: `namelist` = list of names and `countlist` = integer counts. To accomplish this, modify the `readNamesCounts(.)` function (be sure to use the `with open()` approach). You may need to call `strip()` twice, once to remove the newline `\n` characters and again later to remove the spaces.

The output from my solution is:<br>
<code>
['Jacob', 'Ethan', 'Michael', 'Jayden', 'William', 'Alexander']
[22127, 18002, 17350, 17179, 17051, 16756]</code>


```python
def readNamesCounts(filepath):
    namelist = []
    countlist = []
    ## FINISH THE FUNCTION HERE
    with open(filepath, 'r') as file: 
        for line in file: 
            line = line.strip() 
            count, name = line.split(',')
            name = name.strip()
            count = int(count) 
            namelist.append(name)
            countlist.append(count)
    return namelist, countlist


filepath = os.path.join(datadir, "babyNames.txt")
namelist, countlist = readNamesCounts(filepath)
print(namelist)
print(countlist)
```

    ['Jacob', 'Ethan', 'Michael', 'Jayden', 'William', 'Alexander']
    [22127, 18002, 17350, 17179, 17051, 16756]

