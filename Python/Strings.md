# Strings
## Substrings
```python
course = "Python programming"
course[0:3] # prints: Pyt
course[:3]  # prints: Pyt
```
Note: the character at the end index is not included.

```python
course[7:]  # prints: programming
course[-1]  # prints: g
```

## Length of a String
```python
course = "Python programming"
len(course)
```

## Concatenate Strings
```python
first = "Ivan"
last = "Bahamaca"
full_name = first + " " + last
```

## String Interpolation
```python
full = f"{first} {last}"
print(full) # prints: Ivan Bahamaca
```

We can use any expression inside { }:
```python
full = f"{len(first)} {2 + 2}"
print(full) # pritns: 4 4 
```

## Formatted Strings
```python
print("| {:<10} | {:<15} | {:>5} |".format(name, last, age))

# Prints:
# | Ivan       | Bahamaca        |    37 |

# :< means aligned to the left 
# :> means aligned to the right 
```

To format float numbers:
```python
pi = 3.1416
print(f"Pi = {pi:.2f}")  # Prints Pi = 3.14
```

## String Methods
```python
course = "python programming"
print(course.upper()) # prints: PYTHON PROGRAMMING
print(course.title()) # prints: Python Programming
print(course.replace("python", "c#")) # prints: c# programming
```

## Trim String
```python
name = "python  "
name.strip() # remove spaces at the begining and end.
```

## Find the index of a character or string
```python
course = "python programming"
print(course.find("pro")) # prints 7
```

Note: If character is not found, find method returns -1.

## Find if a string is in another string
```python
course = "python programming"
print("pro" in course) # prints True
```

## Find if a String is Not in Another String
```python
print("c#" not in course) # prints True
```

## Type Conversion
```python
x = "1";
int(x)   # convert string to int
float(x) # convert string to float
bool(x)  # convert string to bool

y = 5
str(y) # convert int to string
```

## Values Considered False
* Empty strings
* 0
* None

Everything else is considered True.

