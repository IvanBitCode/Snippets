# Exceptions
## Handling A Exception
```python
try:
    # statement
except Type_of_except:
    print("An exception ocurred.")
except another_type_of_except as error:
    print(f"Another exception ocurred: error")
else:
    print("No exceptions were thrown.")
```

## Handling Multiple Exceptions
```python
try:
    file = open("app.py")
    # statement
except (type_of_except1, type_of_except2):
    print("Another exception ocurred.")
else:
    print("No exceptions were thrown.")
finally:
    file.close()
```

## With Statement
We use `with` to release resources automatically

```python
try:
    with open("app.py") as file:
        print("File opened.")
    # More statement…
except (type_of_except1, type_of_except2):
    print("Another exception ocurred.")
```

File object will be closed automatically when the flow of the logic goes out of the with block.

We can use `with` statement to release multiple resources:

```python
with open("app.py") as file, open("another.txt") as target:
    # more statements
```

## Raising Exceptions
```python
def calculate_xfactor(age):
    if age <= 0:
        raise ValueError("Age cannot be 0 or less.")
    return 10 / age
```

Note: raising exception is costly, so try not to raise exceptions.

## Cost Of Raising Exceptions
The `timeit` function allow us to calculate the execution time of a python code.

```python
from timeit import timeit

code = """
def calculate_xfactor(age):
    if age <= 0:
        raise ValueError("Age cannot be 0 or less.")
    return 10 / age

try:
    calculate_xfactor(-1)
except:
    pass # just pass to the next line (we cannot have empty after except).
"""

timeit(code, number=1000) # Repeat the code 1000 times
```
