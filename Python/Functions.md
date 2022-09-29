# Functions
## Defining a Function
Simple rules to define a function in Python:
* Function blocks begin with the keyword def followed by the function name and parentheses.
* Any input parameters or arguments should be placed within these parentheses.
* The first statement of a function can be an optional statement - the documentation string of the function or docstring.
* The code block within every function starts with a colon (:) and is indented.
* The statement 'return [expression]' exits a function, optionally passing back an expression to the caller. A return statement with no arguments is the same as return None.
 
Syntax example:

```python
def printme( str ):
    "This prints a passed string into this function"
    print (str)
    return
```
    
## Calling a Function

```python
# Now you can call printme function
printme("This is first call to the user defined function!")
```
 
## Pass by Reference vs Value
All parameters (arguments) in the Python language are passed by reference. It means if you change what a parameter refers to within a function, the change also reflects back in the calling function:

```python
def changeme( mylist ):
    "This changes a passed list into this function"
    print ("Values inside the function before change: ", mylist)
    
    mylist[2]=50
    print ("Values inside the function after change: ", mylist)
    return

# Call changeme function
mylist = [10,20,30]
changeme( mylist )
print ("Values outside the function: ", mylist)
```
 
This would produce the following result:

```
Values inside the function before change:  [10, 20, 30]
Values inside the function after change:  [10, 20, 50]
Values outside the function:  [10, 20, 50]
```
 
Example 2:

```python
# Function definition is here
def changeme( mylist ):
    "This changes a passed list into this function"
    mylist = [1,2,3,4] # This would assign new reference in mylist
    print ("Values inside the function: ", mylist)
    return
 
# Call changeme function
mylist = [10,20,30]
changeme( mylist )
print ("Values outside the function: ", mylist)
```
 
The parameter mylist is local to the function changeme. Changing mylist within the function does not affect mylist. The function accomplishes nothing and finally this would produce the following result:
```
Values inside the function:  [1, 2, 3, 4]
Values outside the function:  [10, 20, 30]
```
 
## Required Arguments
Required arguments are the arguments passed to a function in correct positional order. Here, the number of arguments in the function call should match exactly with the function definition.
 
## Keyword Arguments
When you use keyword arguments in a function call, the caller identifies the arguments by the parameter name.
This allows you to skip arguments or place them out of order because the Python interpreter is able to use the keywords provided to match the values with parameters.

```python
# Function definition is here
def printinfo( name, age ):
   "This prints a passed info into this function"
   print ("Name: ", name)
   print ("Age ", age)
   return
 
# Call printinfo function
printinfo( age = 50, name = "miki" )
```
 
## Default Arguments
A default argument is an argument that assumes a default value if a value is not provided in the function call for that argument.

```python
# Function definition is here
def printinfo( name, age = 35 ):
    "This prints a passed info into this function"
    print ("Name: ", name)
    print ("Age ", age)
    return
 
# Now you can call printinfo function
printinfo( age = 50, name = "miki" )
printinfo( name = "miki" )
```

When the above code is executed, it produces the following result:

```
Name:  miki
Age  50
Name:  miki
Age  35
```
 
## Variable-length Arguments
Syntax:

```python
def functionname([formal_args,] *var_args_tuple ):
    "function_docstring"
    function_suite
    return [expression]
```

An asterisk (*) is placed before the variable name that holds the values of all nonkeyword variable arguments. This tuple remains empty if no additional arguments are specified during the function call.
Example:

```python
# Function definition is here
def printinfo( arg1, *vartuple ):
    "This prints a variable passed arguments"
    print ("Output is: ")
    print (arg1)
    
    for var in vartuple:
       print (var)
    return
 
# Call printinfo function
printinfo( 10 )
printinfo( 70, 60, 50 )
```

## Anonymous Functions
They are not declared in the standard manner by using the def keyword. You can use the lambda keyword to create small anonymous functions.
* Lambda forms can take any number of arguments but return just one value in the form of an expression. They cannot contain commands or multiple expressions.
* An anonymous function cannot be a direct call to print because lambda requires an expression.
* Lambda functions have their own local namespace and cannot access variables other than those in their parameter list and those in the global namespace.
 
Example:
```python
# Function definition is here
sum = lambda arg1, arg2: arg1 + arg2
 
# Now you can call sum as a function
print ("Value of total : ", sum( 10, 20 ))
print ("Value of total : ", sum( 20, 20 ))
```

When the above code is executed, it produces the following result:
```
Value of total :  30
Value of total :  40
```
 
## Scope of Variables
There are two basic scopes of variables in Python:
* **Local variables**. Variables that are defined inside a function body have a local scope.
* **Global variables**. Variables that are defined outside have a global scope.
 