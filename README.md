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

## Operations with other types
Filip mentioned that different types behave differently in Python.
When you sum two strings, for example, you'll get different behavior than when you sum two integers or two booleans.
In the script some variables with different types have already been created. It's up to you to use them.

## Instructions
<li>Calculate the product of savings and factor. Store the result in year1.</li>
What do you think the resulting type will be? Find out by printing out the type of year1.</li>
<li>Calculate the sum of desc and desc and store the result in a new variable doubledesc.
<li>Print out doubledesc. Did you expect this?</li>






























