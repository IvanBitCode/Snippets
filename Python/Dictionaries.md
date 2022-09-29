# Dictionaries

## Basic Operations
```python
# Empty Dic:
point = {}
# Defined dic:
point = {"X": 1, "Y": 2}
# Create a dic
point = dict(x=1, y=2) # keyword argument

#Accesing an element of a dic
point[0] # Not allowed
point["x"] = 10

# Add a new entry
point["z"] = 20 # since z does not exist, it is added.

# Check if an item exists
if "a" in point:
    print(point["a"])

# Using the get method
point.get("a") # returns None if element does not exist

# Delete an element
del point["x"]
```

Keys are unique within a dictionary while values may not be. The values of a dictionary can be of any type, but the keys must be of an immutable data type such as strings, numbers, or tuples.

Note: Elements in a dictionary cannot be sorted.

## Loop over a Dic
```python
for key in point:
    print(key) # prints the key, but no the value.
    print(point[key]) # prints the value.
```

## Getting tuples
```python
for key, value in point.items():
    print(key, value)
```

## Dic comprehensions
```python
values = {x: x * 2 for x in range(5)}
print(values)
# We get:
{0:0, 1:2, 2:4, 3:6, 4:8}
```

## Generator Expressions
Generator objects are iterable. In each iteration it generates a new value. They do not store all items in memory, which is appropiate when we have to iterate over a really large number of items.
```python
# Value is not a list, it is a generator object.
value = (x: x * 2 for x in range(5))
```

Note that we replace brackets [] with parenthesis ().

## Unpacking Operator
Este operador nos permite obtener o desempaquetar valores individuales de cualquier objeto que sea iterable.
```python
values = [*range(5), *"Hello"]
print(values)

# We get:
[0, 1, 2, 3, 4, 'H', 'e', 'l', 'l', 'o']
```
 
## Built-in Dictionary Functions and Methods
```python
dict.clear()
# Removes all elements of dictionary dict
 
dict.items()
# Returns a list of dict's (key, value) tuple pairs
 
dict.keys()
# Returns list of dictionary dict's keys
 
dict.values()
# Returns list of dictionary dict's values.
```
