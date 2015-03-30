Common Errors and Solutions
===================

As you all probably know by now, errors are what happen when you run a code that is "incorrect" in some way. While certain strategies can help you avoid errors (like coding in modules!), we all run into them.
However, errors are often simple to fix, because python will always tell you which line the error was on, and what the type of the error was. 
Here are a few types of errors with solution strategies:

## Syntax Errors

These will occur when the **syntax** (the format of the code or the order in which words are written) is incorrect and Python can't parse it.
```
if a == "hi"
	print (a)
```
Our if statement is missing a colon (:) so the syntax is invalid.  With these errors, look for missing colons, missing parentheses, or other similar typos.  Be careful in errors with missing parentheses, because often Python will direct you to the next line when telling you where the error is:
```
lista = ["a","b","c"]
print(len(lista[1])
print(lista)

  File "C:/Users/aloverso/Documents/Python Scripts/errors.py", line 16
    print(lista)
        ^
SyntaxError: invalid syntax
```
Here, Python flags the `print(lista)` line as containing the syntax error, but if you look closely, it's really because we forgot a parentheses on the line before it, `print(len(lista[1])`.

## Type Errors

A type error occurs when the **type** of a variable doesn't match the operation you're trying to do. Types of variables might include a list, string, integer, float, etc.
```
a = "hello"
print(a - 1)

TypeError: unsupported operand type(s) for -: 'str' and 'int'
```
To fix this error, check which variable type your functions/operations are expecting.  Then check what the type your variables are. Use the `print(type(var))` command to check types (in this case `var` would be `a`).

Another example:
```
number = 300
print("Insper is at Rua Quatá " + number)

TypeError: Can't convert 'int' object to str implicitly
```
Python expected to combine two strings within `print` , but instead got a string and an `int`.


## Indentation Errors
Python knows where your code should be executed based on its indentation, so make sure all code is aligned at the right indentation level. Remember, any time you enter a loop or conditional statement, you indent. 
```
if a=="hi":
print (a)

IndentationError: expected an indented block
```
Here, it found an error because the `print(a)` line should be indented so that it executes within the if statement.  In this error, Python expected an indented block and did not find one.  You can also get indentation errors when Python found an indentation block without expecting one:
```
if x == 2:
	print("hello")
		x = 3 

IndentationError: unexpected indent
```

### Infinite Loops

Another common error is an infinite loop. This is when a loop keeps going forever because the condition to stop the loop is never met. Your computer won't give you an error for this, but it might crash.
Sometimes, this is due to an indentation error. Don't forget that the only things included inside of a loop are the things at the appropriate indentation level. For example:
```
n = 0
while n < 5:
	print(n)
n += 1
```
Here, the only thing inside the while loop is `print(n)`. Only after the code stops running the while loop, `n+=1` will be executed. However, the while loop will never stop, because n is not changing inside of it. The code above will print `0` FOR-EV-ER.


## Name Errors
Name errors will occur when you reference the name of a function or variable without defining it correctly beforehand.
```
import random

f = open("entrada.txt")
lines = f.readlines()
random_word = choice(lines)

NameError: name 'choice' is not defined
```
Here, we try to use the `choice` function in the `random` package, but by importing random, we have to use `random.choice` to reference the choice function.

```
if guess == "a":
	print ("You're right")
guess = input("what is your guess")

NameError: name 'guess' is not defined
```
This doesn't work because we try to use the value of guess before assigning it.
```
def my_function():
	x = 1

my_function()
print (x)

NameError: name 'x' is not defined
```
NameErrors can occur when we define a local variable in a function, but then try to access it outside of the scope of the function.

## Attribute Errors
Attribute errors occur when you try to use a function or keyword for a certain variable, but it doesn't have that particular function.  For example:
```
i = 10
i.strip()

AttributeError: 'int' object has no attribute 'strip'
```
The `strip()` function is a string function, so trying to use it on an integer will return an attribute error.

## Index Errors
Index errors occur when you try to access an element of a list or a string, but there exists no element at that index.
```
lista = [1,2]
print(lista[5])

IndexError: list index out of range
```
The lista only has two elements, so there is no element at index 5.

## More Notes

### "Catching" Values
```
name = "Insper"
name.lower()
print(name)
```
This prints "Insper" (still with the capital I!) because the `name.lower()` **returns** the lowercase string, but it does not automatically change the value of `name` itself.  You need to **asssign** the return value to a variable.  Either of these two solutions will work:
```
name = "Insper"
name = name.lower()
print(name)
```
```
name = "Insper"
lowercase_name = name.lower()
print(lowercase_name)
```

Also, be careful about what keywords are functions and require parentheses.  For example:
```
name = "Insper"
print(name.lower)
```
The above is incorrect because it should be `name.lower()`

### Types of `if` statements

Say that we take an input from the user like:
```
x = input("Your favorite number: ")
```

A single if statement:
```
if x == 1:
    print("You like the number one")
```
The above code only cares about the case where x = 1, and does not do anything if the user enters a different number.
```
if x == 1:
    print("You like the number one")
else:
	print("You did not input the number one")
```
The above code adds an else statement, and now, no matter what is entered, the program will print one of the two statements.
```
if x == 1:
    print("You like the number one")
elif x==2:
	print("You like the number two")
```
The command "elif" is Python's way of saying "else if".
An elif statement means that the program will *first* check if x is 1, and then check if x is 2.  Python executes an elif when **both** its conditional statement (x==2) is True **and** the if statement above did not execute.

```
if x == 1:
    print("You like the number one")
    x = 2
elif x==2:
	print("You like the number two")
```
```
if x == 1:
    print("You like the number one")
    x = 2
if x==2:
	print("You like the number two")
```
In these above two examples, we reset the value of x within the if statement.  In the first example, it will **not** print the phrase "You like the number two", even though x gets set to 2, and the conditional x==2 is True.  This is because the elif will only execute when the "if" before it did not.

In the second example, it *will* print the phrase "You like the number two", because we changed the elif to an if.  The second if does not care whether the if statement above it executed, and after x is changed to 2, it will also execute its code.

```
if x == 1:
	if y == 1:
		print("x is 1 and y is 1")
```
*Nested* if statements will check that both conditions are true.  This code above could be replaced by the logically equivalent: 
```
if x == 1 and y == 1:
		print("x is 1 and y is 1")
```
However, if we want to check more things about the y variable, we need the nested statements.  For example:
```
if x == 1:
	if y == 1:
		print("x is 1 and y is 1")
	else:
		print("x is 1 and y is not 1")
```
could not be replaced by merging the if statements in any way.