# Tuples
A tuple is a read-only list. Tuples use parentheses, whereas lists use square brackets.
```python
tup1 = ('physics', 'chemistry', 1997, 2000)
tup2 = (1, 2, 3, 4, 5 )
tup3 = "a", "b", "c", "d"
 
# Define empty tuple:
tup1 = ();
 
# To write a tuple containing a single value you have to include a comma, even though there is only one value:
tup1 = (50,)

# Create a tuple from a list
point = tuple([1, 2])

# Create a tuple from a string
letters = tuple("Hello World")

# Unpack a tupple
point = (1, 2, 3)
x, y, z = point
```

## Accessing Values in Tuples
To access values in tuple, use the square brackets for slicing along with the index or indices to obtain the value available at that index. For example:

```python
tup1 = ('physics', 'chemistry', 1997, 2000)
tup2 = (1, 2, 3, 4, 5, 6, 7 )
 
print ("tup1[0]: ", tup1[0])
print ("tup2[1:5]: ", tup2[1:5])
 
# When the above code is executed, it produces the following result:
tup1[0]:  physics
tup2[1:5]:  (2, 3, 4, 5)
```
