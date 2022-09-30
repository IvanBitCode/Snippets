# Python Basics
## Executing Python 3 Scripts
Add this in the first line of your python script:

`#!python3`

Run your script as follow:

`py scriptName.py`

## Naming convention
Here are naming conventions for Python identifiers:
* **Class** names start with an uppercase letter. All other identifiers start with a lowercase letter.
* Starting an identifier with a single leading underscore indicates that the identifier is **private**.
* Starting an identifier with two leading underscores indicates a **strong private** identifier.
* If the identifier also ends with two trailing underscores, the identifier is a **language-defined special name**.

## Indentation
Python does not use braces({}) to indicate blocks of code for class and function definitions or flow control. Blocks of code are denoted by line indentation, which is rigidly enforced.

## Multi-Line Statements
Statements in Python typically end with a new line. Python, however, allows the use of the line continuation character (\) to denote that the line should continue. For example:
```python
total = item_one + \
    item_two + \
    item_three
```

Comments
```python
# This is a comment.
# This is a comment, too.
```

## Waiting for the User
The following line of the program displays the prompt and, the statement saying "Press the enter key to exit", and then waits for the user to take action:

```python
input("\n\nPress the enter key to exit.") 
```

Here, `"\n\n"` is used to create two new lines before displaying the actual line.

## Suites
Groups of individual statements, which make a single code block are called suites in Python:

```python
if expression:
    suite
elif expression:
    suite
else:
    suite
```

## Data Type Conversion
Sometimes, you may need to perform conversions between the built-in types. To convert between types, you simply use the type-names as a function.
There are several built-in functions to perform conversion from one data type to another. These functions return a new object representing the converted value.

```python
int(x [,base]) # Converts x to an integer. The base specifies the base if x is a string.
float(x)       # Converts x to a floating-point number.
str(x)         # Converts object x to a string representation.
eval(str)      # Evaluates a string and returns an object.
tuple(s)       # Converts s to a tuple.
list(s)        # Converts s to a list.
dict(d)        # Creates a dictionary. d must be a sequence of (key,value) tuples.
chr(x)         # Converts an integer to a character.
unichr(x)      # Converts an integer to a Unicode character.
ord(x)         # Converts a single character to its integer value.
hex(x)         # Converts an integer to a hexadecimal string.
```

## Python Membership Operators
Python's membership operators test for membership in a sequence, such as strings, lists, or tuples. There are two membership operators as explained below.

* `in`: Evaluates to true if it finds a variable in the specified sequence and false otherwise.
* `not in`: Evaluates to true if it does not finds a variable in the specified sequence and false otherwise.

## Single Statement Suites
If the suite of an if clause consists only of a single line, it may go on the same line as the header statement:
```python
var = 100
if ( var  == 100 ) : print ("Value of expression is 100")
```


