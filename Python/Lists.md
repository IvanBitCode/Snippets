# Lists
## Basic List Operations
Lists respond to the + and * operators much like strings; they mean concatenation and repetition here too, except that the result is a new list, not a string.

```python
Python Expression               Results                         Description
--------------------------------------------------------------------------------
len([1, 2, 3])                  3                               Length
[1, 2, 3] + [4, 5, 6]           [1, 2, 3, 4, 5, 6]              Concatenation
['Hi!'] * 4                     ['Hi!', 'Hi!', 'Hi!', 'Hi!']    Repetition
3 in [1, 2, 3]                  True                            Membership
for x in [1,2,3]: print(x)      1 2 3                           Iteration
numbers = list(range(5))        [0, 1, 2, 3, 4]                 List from range
Chars = list("Hello")           ['H','e','l','l','0',]          List from string
```

## Accessing Items
```python
letters = ["a", "b", "c", "d", "e"]

# Get the first item
letters[0]

# Get the last item
letters[-1]

# Get a range in the list (first two elements)
letters[0:2] # Get ['a','b']

# Get every second element
letters[::2] # Get ['a','c','e']

# Get list in reverse order
letters[::-1]
```

## Unpacking List
```python
numbers = [1, 2, 3]
first, second, third = numbers

# This is the same as:
first = numbers[0]
second = numbers[1]
third = numbers[2]
```

Note: The number of variables at the left of '=' must be equal than the number of elements in the list.

```python
# Unpacking first and last item
Numbers = [1, 2, 3, 4, 4, 4, 9]
first, *other, last = numbers
print(fist, last)
print(other)

# We get:
1 9 
[2, 3, 4, 4, 4]
```

## Looping over Lists
```python
letters = ["a", "b", "c"]
for letter in letters:
    print (letter)

# To get the index of a list in the same loop:
for letter in enumerate(letters):
    print (letter)

# We get:
(0, 'a')
(1, 'b')
(2, 'c')
```

## Using list unpacking
```python
for index, letter in enumerate(letters):
    print (index, letter)

# We get:
0 a
1 b
2 c
```

## Adding or Removing Items
```python
letters = ["a", "b", "c"]

# Add at the end
letters.append("d")

# Insert at a specific position index 
letters.insert(0, "-")

# Remove the last item
letters.pop()

# Remove at a specific position index
letters.pop(0)

# Remove specific element
letters.pop("b")

# Delete a range of items
del letters[0:3]

# Remove all items
letters.clear()
```

## Finding Items
```python
letters = ["a", "b", "c"]

# Get the index of an element
letters.index("a") # returns 0

# Note: If the element does not exist, an exception will be thorwn.

# Check if an element exists before getting its index
if "d" in letters:
    print(letters.index("d"))

# Get the number of occurrences
letters.count("d") # Gets 0 since there's no d letter in letters.
```

## Sorting Lists
```python
# Ascending order (It modifies the original list)
numbers.sort()

# Descending order
numbers.sort(reverse=True)

# Sort not modifying the original list (it returns a new list sorted)
sorted(number)
sorted()
```

### Sorting complex list
```python
items = [
    ("Product1", 10)
    ("Product2", 9)
    ("Product3", 12)
]

# Define a function that will take the price to order the list by it.
def sort_item(item):
    return item[1]

# Calls the built-in function sort.
items.sort(key=sort_item)
print(items)

# Prints
[('Product2', 9),
('Product1', 10),
('Product3', 12)]
```

### Sorting complex list using lambda expression
```python
items.sort(key=lambda item: item[1])

# Sorting list of objects example:
items.sort(key=lambda item: item.count])
items.sort(key=lambda item: item.product_name])
```

Now we don't need to define the previous function.

### Map Function (getting a list from a list of tuples)
```python
items = [
    ("Product1", 10)
    ("Product2", 9)
    ("Product3", 12)
]

# We want to extract the prices into a list.
prices = list(map(lambda item:item[1], items))
```

### Filter function
We want to filter previous list of products by price >= 10
```python
filtered = list(filter(lambda item:item[1] >= 10, items))
print(filtered)

# We get:
[('Product1', 10),
('Product3', 12)]
```

### List Comprehensions
```python
items = [
    ("Product1", 10)
    ("Product2", 9)
    ("Product3", 12)
]

# The following statement (List Comprehensions):
prices = [item[1] for item in items]
# Is equivalent to using map function:
prices = list(map(lambda item:item[1], items))

# Using a list comprehension to filter:
filtered = [item for item in items if item[1] >= 10]
# Which is equivalent to:
filtered = list(filter(lambda item:item[1] >= 10, items))
```

## Built-in List Functions and Methods
```python
max(list)
# Returns item from the list with max value.

min(list)
# Returns item from the list with min value.

list(seq)
# Converts a tuple into list.

list.append(obj)
# Appends object obj to list
 
list.count(obj)
# Returns count of how many times obj occurs in list
 
list.extend(seq)
# Appends the contents of seq to list
 
list.sort([func])
# Sorts objects of list, use compare func if given
```
