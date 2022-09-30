# Sets
Sets are a collection with no duplicates.

```python
numbers = [1, 1, 2, 3, 4]
uniques = set(numbers)
print(uniques)

# We get (duplicates removed):
{1, 2, 3, 4}
```

Sets are defined using braces.

```python
first = {1, 2, 3, 4}
second = {1, 4}

# Common Operations
second.add(5)
second.remove(5)
len(second)
```

## Sets Operations
### Union
```python
first | second
```

The new set will contain the elements of the first and second sets but with duplicates removed.

### Intersection
```python
first & secod
```

The new set will contain only the items common to both sets.

### Difference
```python
first - second
```

The new set will contain only the elements that we have in the first set and not in the second.

### Symmetric Difference
```python
first ^ second
```

The new set will contain only the elements present in the first or second set but not both.

**Note**: It is not possible to access the elements of a set using indices.

Find out if an element is in a set
```python
if 1 in first:
    print("yes")
```
