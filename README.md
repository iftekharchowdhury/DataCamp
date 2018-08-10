# DataCamp
This repo contains all of my Datacamp source code and projects. Anyone use this code and program
<b>First Course of Data Analyst with Python</b>
<h1>Intro to Python For Data Science</h1>
<p>
<h2>Python Basics</h2>
An introduction to the basic concepts of Python. Learn how to use Python both interactively and through a script. Create your first variables and acquaint yourself with Python's basic data types. 

<b>First Problem Exercise No = 1</b>
<li>The Python Interface</li>
In the Python script on the right, you can type Python code to solve the exercises. If you hit Run Code or Submit Answer, your python script (script.py) is executed and the output is shown in the IPython Shell. Submit Answer checks whether your submission is correct and gives you feedback.
You can hit Run Code and Submit Answer as often as you want. If you're stuck, you can click Get Hint, and ultimately Get Solution.
You can also use the IPython Shell interactively by simply typing commands and hitting Enter. When you work in the shell directly, your code will not be checked for correctness so it is a great way to experiment

<li>Experiment in the IPython Shell; type 5 / 8, for example.</li>
<li>Add another line of code to the Python script: print(7 + 10).</li>
<li>Hit Submit Answer to execute the Python script and receive feedback.</li>

<h2>Any Comments</h2>
Something that Filip didn't mention in his videos is that you can add comments to your Python scripts. Comments are important to make sure that you and others can understand what your code is about.
To add comments to your Python script, you can use the # tag. These comments are not run as Python code, so they will not influence your result. As an example, take the comment on the right, # Division; it is completely ignored during execution.

## Python As A Calculator

Python is perfectly suited to do basic calculations. Apart from addition, subtraction, multiplication and division, there is also support for more advanced operations such as:
<li>Exponentiation: **. This operator raises the number to its left to the power of the number to its right. For example 4**2 will give 16.</li>

<li>Modulo: %. This operator returns the remainder of the division of the number to the left by the number on its right. For example 18 % 7 equals 4.</li>
<li>The code in the script on the right gives some examples.</li>

## Suppose you have $100, which you can invest with a 10% return each year. After one year, 
it's 100×1.1=110
100×1.1=110
dollars, and after two years it's 
100×1.1×1.1=121
100×1.1×1.1=121
Add code on the right to calculate how much money you end up with after 7 years.

## Variable Assignment
 <li>In Python, a variable allows you to refer to a value with a name. To create a variable use =, like this example:</li>
<li>x = 5</li>
<li>You can now use the name of this variable, x, instead of the actual value, 5.</li>
<li>Remember, = in Python means assignment, it doesn't test equality!</li>

## Exercise 5 
#### Calculations with variables

Remember how you calculated the money you ended up with after 7 years of investing $100? You did something like this:
100 * 1.10 ** 7
Instead of calculating with the actual values, you can use variables instead. The savings variable you've created in the previous exercise represents the $100 you started with. It's up to you to create a new variable to represent 1.10 and then redo the calculations!

<li>Create a variable factor, equal to 1.10.</li>
<li>Use savings and factor to calculate the amount of money you end up with after 7 years. Store the result in a new variable, result.</li>
<li>Print out the value of result.</li>
</p>

## Other variable types

In the previous exercise, you worked with two Python data types:
<li>int, or integer: a number without a fractional part. savings, with the value 100, is an example of an integer.</li>
<li>float, or floating point: a number that has both an integer and fractional part, separated by a point. factor, with the value 1.10, is an example of a float.</li>
<li>Next to numerical data types, there are two other very common data types:</li>
<li>str, or string: a type to represent text. You can use single or double quotes to build a string.</li>
<li>bool, or boolean: a type to represent logical values. Can only be True or False (the capitalization is important!).</li>

<li> Create a new string, desc, with the value "compound interest". </li>
<li> Create a new boolean, profitable, with the value True. </li>

```python

# Create a variable desc
desc = "compound interest"
# Create a variable profitable
profitable = True

```

## Guess the type

To find out the type of a value or a variable that refers to that value, you can use the type() function. Suppose you've defined a variable a, but you forgot the type of this variable. To determine the type of a, simply execute:
type(a)
We already went ahead and created three variables: a, b and c. You can use the IPython shell on the right to discover their type. Which of the following options is correct?

# Operations with other types

Filip mentioned that different types behave differently in Python.
When you sum two strings, for example, you'll get different behavior than when you sum two integers or two booleans.
In the script some variables with different types have already been created. It's up to you to use them.

# Instructions

<li>Calculate the product of savings and factor. Store the result in year1.</li>
What do you think the resulting type will be? Find out by printing out the type of year1.</li>
<li>Calculate the sum of desc and desc and store the result in a new variable doubledesc.
<li>Print out doubledesc. Did you expect this?</li>

# Create a list
As opposed to int, bool etc., a list is a compound data type; you can group values together:

```python 

a = "is"
b = "nice"
my_list = ["my", "list", a, b]

```
After measuring the height of your family, you decide to collect some information on the house you're living in. The areas of the different parts of your house are stored in separate variables for now, as shown in the script.

# Instructions

<li>Create a list, areas, that contains the area of the hallway (hall), kitchen (kit), living room (liv), bedroom (bed) and bathroom (bath), in this order. Use the predefined variables.</li>
<li>Print areas with the print() function.</li>

# Create list with different types

A list can contain any Python type. Although it's not really common, a list can also contain a mix of Python types including strings, floats, booleans, etc.
The printout of the previous exercise wasn't really satisfying. It's just a list of numbers representing the areas, but you can't tell which area corresponds to which part of your house.
The code on the right is the start of a solution. For some of the areas, the name of the corresponding room is already placed in front. Pay attention here! "bathroom" is a string, while bath is a variable that represents the float 9.50 you specified earlier.

# Instructions

<li>Finish the line of code that creates the areas list. Build the list so that the list first contains the name of each room as a string and then its area. In other words, add the strings "hallway", "kitchen" and "bedroom" at the appropriate locations.</li>
<li>Print areas again; is the printout more informative this time?</li>

```python 

# area variables (in square meters)
hall = 11.25
kit = 18.0
liv = 20.0
bed = 10.75
bath = 9.50

# Adapt list areas
areas = ["hallway", hall, "kitchen", kit, "living room", liv,"bedroom", bed, "bathroom", bath]

# Print areas
print (areas)

```

# List of lists

As a data scientist, you'll often be dealing with a lot of data, and it will make sense to group some of this data.

Instead of creating a flat list containing strings and floats, representing the names and areas of the rooms in your house, you can create a list of lists. The script on the right can already give you an idea.

Don't get confused here: "hallway" is a string, while hall is a variable that represents the float 11.25 you specified earlier.

# Instructions

* Finish the list of lists so that it also contains the bedroom and bathroom data. Make sure you enter these in order!
* Print out house; does this way of structuring your data make more sense?
* Print out the type of house. Are you still dealing with a list?


```python 

# area variables (in square meters)
hall = 11.25
kit = 18.0
liv = 20.0
bed = 10.75
bath = 9.50

# house information as list of lists
house = [["hallway", hall],
         ["kitchen", kit],
         ["living room", liv],
         ["bedroom", bed],
         ["bathroom", bath]]
# Print out house
print (house)
# Print out the type of house
print (type(house))

```

## Subset and conquer

Subsetting Python lists is a piece of cake. Take the code sample below, which creates a list **x** and then selects "b" from it. Remember that this is the second element, so it has index 1. You can also use negative indexing.
```
x = ["a", "b", "c", "d"]
x[1]
x[-3] # same result!
```
Remember the areas list from before, containing both strings and floats? Its definition is already in the script. Can you add the correct code to do some Python subsetting?

## Instructions
* Print out the second element from the areas list, so 11.25.
* Subset and print out the last element of areas, being 9.50. Using a negative index makes sense here!
* Select the number representing the area of the living room and print it out.

```python 

# Create the areas list
areas = ["hallway", 11.25, "kitchen", 18.0, "living room", 20.0, "bedroom", 10.75, "bathroom", 9.50]

# Print out second element from areas
print (areas[1])

# Print out last element from areas
print (areas[-1])

# Print out the area of the living room
print (areas[5])
```
## Subset and calculate

After you've extracted values from a list, you can use them to perform additional calculations. Take this example, where the second and fourth element of a list x are extracted. The strings that result are pasted together using the + operator:

```
x = ["a", "b", "c", "d"]
print(x[1] + x[3])
```
## Instructions

* Using a combination of list subsetting and variable assignment, create a new variable, eat_sleep_area, that contains the sum of the area of the kitchen and the area of the bedroom.
* Print the new variable eat_sleep_area

```python

# Create the areas list
areas = ["hallway", 11.25, "kitchen", 18.0, "living room", 20.0, "bedroom", 10.75, "bathroom", 9.50]

# Sum of kitchen and bedroom area: eat_sleep_area
eat_sleep_area = areas[3] + areas[7]

# Print the variable eat_sleep_area
print (eat_sleep_area)
```
# Slicing and dicing

Selecting single values from a list is just one part of the story. It's also possible to slice your list, which means selecting multiple elements from your list. Use the following syntax:

``` 
my_list[start:end]
```
The start index will be included, while the end index is not.
The code sample below shows an example. A list with "b" and "c", corresponding to indexes 1 and 2, are selected from a list x:

```
x = ["a", "b", "c", "d"]
x[1:3]
```
The elements with index 1 and 2 are included, while the element with index 3 is not.

## Instructions

* Use slicing to create a list, downstairs, that contains the first 6 elements of areas.
* Do a similar thing to create a new variable, upstairs, that contains the last 4 elements of areas.
* Print both downstairs and upstairs using print().

```python

# Create the areas list
areas = ["hallway", 11.25, "kitchen", 18.0, "living room", 20.0, "bedroom", 10.75, "bathroom", 9.50]

# Use slicing to create downstairs
downstairs = areas[0:6]
# Use slicing to create upstairs
upstairs = areas[6:11]

# Print out downstairs and upstairs
print (downstairs)x[2] results in a list, that you can subset again by adding additional square brackets.
print (upstairs)
```
# Subsetting lists of lists

You saw before that a Python list can contain practically anything; even other lists! To subset lists of lists, you can use the same technique as before: square brackets. Try out the commands in the following code sample in the IPython Shell:

```python

x = [["a", "b", "c"],
     ["d", "e", "f"],
     ["g", "h", "i"]]
x[2][0]
x[2][:2]
```
What will house[-1][1] return? house, the list of lists that you created before, is already defined for you in the workspace. You can experiment with it in the IPython Shell.

# Replace list elements
Replacing list elements is pretty easy. Simply subset the list and assign new values to the subset. You can select single elements or you can change entire list slices at once.
Use the IPython Shell to experiment with the commands below. Can you tell what's happening and why?

```python

x = ["a", "b", "c", "d"]
x[1] = "r"
x[2:] = ["s", "t"]
```
For this and the following exercises, you'll continue working on the areas list that contains the names and areas of different rooms in a house.

* Update the area of the bathroom area to be 10.50 square meters instead of 9.50.
* Make the areas list more trendy! Change "living room" to "chill zone".

```python

# Create the areas list
areas = ["hallway", 11.25, "kitchen", 18.0, "living room", 20.0, "bedroom", 10.75, "bathroom", 9.50]
# Correct the bathroom area
areas[-1] = 10.50
# Change "living room" to "chill zone"
areas[4]="chill zone"
print (areas )
```
# Extend a list
If you can change elements in a list, you sure want to be able to add elements to it, right? You can use the + operator:

```
x = ["a", "b", "c", "d"]
y = x + ["e", "f"]
```
You just won the lottery, awesome! You decide to build a poolhouse and a garage. Can you add the information to the areas list?

## Instruction
* Use the + operator to paste the list ["poolhouse", 24.5] to the end of the areas list. Store the resulting list as areas_1.
* Further extend areas_1 by adding data on your garage. Add the string "garage" and float 15.45. Name the resulting list areas_2.
## Solution

```python

# Create the areas list and make some changes
areas = ["hallway", 11.25, "kitchen", 18.0, "chill zone", 20.0,
         "bedroom", 10.75, "bathroom", 10.50]

# Add poolhouse data to areas, new list is areas_1
areas_1 = areas + ["poolhouse", 24.5]
# Add garage data to areas_1, new list is areas_2

areas_2 = areas_1 + ["garage", 15.45]

print (areas_2)
```
# Inner workings of lists
At the end of the video, Filip explained how Python lists work behind the scenes. In this exercise you'll get some hands-on experience with this.
The Python code in the script already creates a list with the name areas and a copy named areas_copy. Next, the first element in the areas_copy list is changed and the areas list is printed out. If you hit Run Code you'll see that, although you've changed areas_copy, the change also takes effect in the areas list. That's because areas and areas_copy point to the same list.
If you want to prevent changes in areas_copy from also taking effect in areas, you'll have to do a more explicit copy of the areas list. You can do this with list() or by using [:].

## Instructions
Change the second command, that creates the variable areas_copy, such that areas_copy is an explicit copy of areas. After your edit, changes made to areas_copy shouldn't affect areas. Hit Submit Answer to check this.

## Solution

```python
# Create list areas
areas = [11.25, 18.0, 20.0, 10.75, 9.50]

# Create areas_copy
areas_copy = list(areas)

# Change areas_copy
areas_copy[0] = 5.0

# Print areas
print(areas)
print(areas_copy)
```

# Function And Packages

## Familiar functions
Out of the box, Python offers a bunch of built-in functions to make your life as a data scientist easier. You already know two such functions: print() and type(). You've also used the functions str(), int(), bool() and float() to switch between data types. These are built-in functions as well.
Calling a function is easy. To get the type of 3.0 and store the output as a new variable, result, you can use the following

```python

result = type(3.0)
```
The general recipe for calling functions and saving the result to a variable is thus:

```python

output = function_name(input)
```
* Use print() in combination with type() to print out the type of var1.
* Use len() to get the length of the list var1. Wrap it in a print() call to directly print it out.
* Use int() to convert var2 to an integer. Store the output as out2.
## Solution

```python
# Create variables var1 and var2
var1 = [1, 2, 3, 4]
var2 = True

# Print out type of var1
print (type(var1))

# Print out length of var1
print (len(var1))

# Convert var2 to an integer: out2
out2 = int(var2)
```
# Multiple arguments
In the previous exercise, the square brackets around imag in the documentation showed us that the imag argument is optional. But Python also uses a different way to tell users about arguments being optional.
Have a look at the documentation of sorted() by typing help(sorted) in the IPython Shell.
You'll see that sorted() takes three arguments: iterable, key and reverse.
key=None means that if you don't specify the key argument, it will be None. reverse=False means that if you don't specify the reverse argument, it will be False.
In this exercise, you'll only have to specify iterable and reverse, not key. The first input you pass to sorted() will be matched to the iterable argument, but what about the second input? To tell Python you want to specify reverse without changing anything about key, you can use =:

```
sorted(___, reverse = ___)
```
Two lists have been created for you on the right. Can you paste them together and sort them in descending order?
Note: For now, we can understand an iterable as being any collection of objects, e.g. a List.

## Instruction
* Use + to merge the contents of first and second into a new list: full.
* Call sorted() on full and specify the reverse argument to be True. Save the sorted list as full_sorted.
* Finish off by printing out full_sorted.

```python

# Create lists first and second
first = [11.25, 18.0, 20.0]
second = [10.75, 9.50]

# Paste together first and second: full
full = first + second

# Sort full in descending order: full_sorted
full_sorted = sorted(full,reverse=True)

# Print out full_sorted
print (full_sorted)
```
# String Methods

Strings come with a bunch of methods. Follow the instructions closely to discover some of them. If you want to discover them in more detail, you can always type help(str) in the IPython Shell.
A string place has already been created for you to experiment with.

## Instructions

* Use the upper() method on place and store the result in place_up. Use the syntax for calling methods that you learned in the previous video.
* Print out place and place_up. Did both change?
* Print out the number of o's on the variable place by calling count() on place and passing the letter 'o' as an input to the method. * * We're talking about the variable place, not the word "place"!

```python

# string to experiment with: room
room = "poolhouse"

# Use upper() on room: room_up
room_up = room.upper()

# Print out room and room_up
print (room)
print (room_up)
# Print out the number of o's in room
print (room.count("o"))
```
# List Methods
Strings are not the only Python types that have methods associated with them. Lists, floats, integers and booleans are also types that come packaged with a bunch of useful methods. In this exercise, you'll be experimenting with:
* **index()**, to get the index of the first element of a list that matches its input and count(), to get the number of times an element appears in a list.
* You'll be working on the list with the area of different parts of a **house: areas.**

# Instructions
* Use the **index()** method to get the index of the element in areas that is equal to 20.0. Print out this index.
* Call **count()** on areas to find out how many times 9.50 appears in the list. Again, simply print out this number.

```python

# Create list areas
areas = [11.25, 18.0, 20.0, 10.75, 9.50]

# Print out the index of the element 20.0
print (areas.index(20.0))

# Print out how often 14.5 appears in areas

print (areas.count(14.5))
```
# List Methods (2)
Most list methods will change the list they're called on. Examples are:
* **append()**, that adds an element to the list it is called on,
* **remove()**, that removes the first element of a list that matches the input, and **reverse()**, that reverses the order of the elements in the list it is called on.
* You'll be working on the list with the area of different parts of the house: areas.

# Instruction
* Use append() twice to add the size of the poolhouse and the garage again: 24.5 and 15.45, respectively. Make sure to add them in this order.
* Print out areas
* Use the reverse() method to reverse the order of the elements in areas.
* Print out areas once more.

```python

# Create list areas
areas = [11.25, 18.0, 20.0, 10.75, 9.50]

# Use append twice to add poolhouse and garage size
areas.append(24.5)
areas.append(15.45)
# Print out areas
print (areas)
# Reverse the orders of the elements in areas
print (areas.reverse())

# Print out areas
print (areas)
```
# Import package
As a data scientist, some notions of geometry never hurt. Let's refresh some of the basics.
For a fancy clustering algorithm, you want to find the circumference, 
C=2πr
A=πr2
To use the constant pi, you'll need the math package. A variable r is already coded in the script. Fill in the code to calculate C and A and see how the print() functions create some nice printouts.

## Instruction
* Import the math package. Now you can access the constant pi with **math.pi**.
* Calculate the circumference of the circle and store it in C.
* Calculate the area of the circle and store it in A.


```python

# Definition of radius
r = 0.43

# Import the math package
import math

# Calculate C
C = 2 * r * math.pi

# Calculate A
A = math.pi * r ** 2

# Build printout
print("Circumference: " + str(C))
print("Area: " + str(A))
```
# Selective import
General imports, like import math, make all functionality from the math package available to you. However, if you decide to only use a specific part of a package, you can always make your import more selective:
**from math import pi**
Let's say the Moon's orbit around planet Earth is a perfect circle, with a radius r (in km) that is defined in the script.

# Instruction
* Perform a selective import from the math package where you only import the radians function.
* Calculate the distance travelled by the Moon over 12 degrees of its orbit. Assign the result to dist. You can calculate this as r * phi, where r is the radius and phi is the angle in radians. To convert an angle in degrees to an angle in radians, use the radians() function, which you just imported.
* Print out dist.
## Solution
```python

# Definition of radius
r = 192500
# Import radians function of math package
from math import radians
from math import pi
# Travel distance of Moon over 12 degrees. Store in dist.
dist = r *  radians(12)
# Print out dist
print (dist)
```
## Your First NumPy Array
In this chapter, we're going to dive into the world of baseball. Along the way, you'll get comfortable with the basics of numpy, a powerful package to do data science.
A list baseball has already been defined in the Python script, representing the height of some baseball players in centimeters. Can you add some code here and there to create a numpy array from it?

# Instruction
* Import the numpy package as np, so that you can refer to numpy with np.
* Use np.array() to create a numpy array from baseball. Name this array np_baseball.
* Print out the type of np_baseball to check that you got it right.

## Solution

```python
# Create list baseball
baseball = [180, 215, 210, 210, 188, 176, 209, 200]

# Import the numpy package as np
import numpy as np

# Create a numpy array from baseball: np_baseball
np_baseball = np.array(baseball)

# Print out type of np_baseball
print (type(np_baseball))
```






