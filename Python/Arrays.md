# Arrays
Arrays are useful when performance matter (list of 10,000 or more). Arrays are like generics in C#. For instance:

```python
numbers = arrays("i", [1, 2, 3])
```

In this case `"i"` means that the array will contains only integers.
Consult the python doc para ver detalles de las letras para los diferentes tipos de datos.

If we try to set an argument to a data type other than integer, we will get an exception. For example:

```python
numbers[0] = 1.0
# We got an exception
```
