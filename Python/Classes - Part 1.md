# Classes - Part 1
## Creating Classes
- Class names follows the pascal naming convention. There should not be underscore between words, and every word should be uppercase.
- All functions must have at least one parameter which is called self by convention.

```python
class MyPoint:
    def draw(self):
        print("draw")

point = MyPoint()
point.draw()
```

## Constructors
- The constructor of a class is always __init__, and it's executed when we create a new object.
- As all methods, the constructor should have at least one parameter: self. After this, we can define additional parameters.
- self is a reference to the current object. 
- Once we define atributes in the constructor, we can use them in the definition of other methods.

```python
class MyPoint:
    def __init__(self, x, y):
        self.x = x
        self.y = y
    
    def draw(self):
        print(f"Point ({self.x}, {self.y})")

point = MyPoint(1, 2)
print(point.x) # prints: 1
point.draw()   # prints: Point (1, 2)
```

## Class vs Instance Attributes
- Class attributes are defined without using self and outside of the constructor.
- Class attributes are shared in all instances of a class.

```python
class MyPoint:
    default_color = "red" # class attribute

    def __init__(self, x, y):
        self.x = x  # instance attribute
        self.y = y  # instance attribute
```

We can access to a class attribute through the class name:
```python
print(MyPoint.default_color) # prints: red
```

But we can also access to that class attribute thorugh an object created:
```python
point = MyPoint(1, 2)
print(point.default_color) # prints: red
```

Similarly, we can modify a class attribute by using an object or the class name:
```python
MyPoint.default_color = "blue"
point1.default_color  = "blue"
```

## Class vs Instance Methods
- To define a class method we need to use the decorator `@classmethod`.
- By convention, the first parameter of an class method must be cls.
- Instance methods do not use the decorator `@classmethod`.

```python
class MyPoint:
    @classmethod
    def zero(cls):
        return cls(0, 0) # creates and initialize a new point object.

MyPoint.zero()
```

## Magic Methods
- They have two underscores at the beggining and at the end.
- They were inherited from the base class.
- They are called automatically by the python interpreter.
- The `__str__` method below will be overriden.

```python
class MyPoint:
    def __str__(self): # Similar to toString() method in java.
        return f"({self.x}, {self.y})"

point = MyPoint(1, 2)
print(point) # prints (1, 2)
```

If we print a point object without defining our `__srt__` magic method we will get something like this: 

```python
<__main__.MyPoint object at 0x107658128>
```

## Comparing Objects
By default, when comparing two objects, the == operator compares the references or addresses of two objects in memory. we need to define the `__eq__` method to make the comparison properly.

```python
class MyPoint:
    def __eq__(self, other):
        return (self.x == other.x) and (self.y == other.y)

    def __gt__(self, other):
        return (self.x > other.x) and (self.y > other.y)
```

Now the `__eq__` method has been defined, we can use the == operator.

```python
point = MyPoint(1, 2)
other = MyPoint(1, 2)
point(point == other)

point = MyPoint(10, 20)
other = MyPoint(1, 2)
point(point > other)
```

## Arithmetic Operations With Magic Methods
```python
class Point:
    def __add__(self, other):
        return MyPoint(self.x + other.x, self.y + other.y)

point = Point(1, 2)
other = Point(1, 2)
print(point + other)
```

## Private Members
- To make a member private, just add double underscore (__) at the begining. 
- To make a method private, just add double underscore (__) at the begining. 

The concept of private members is not the same as in Java or C#, we can still access to private members, but it is a little bit more difficult. Using double underscore is just a convention to prevent accidental access of those private members.

```python
class Point:
    def __init__(self, x, y):
        self.x = x
        self.y = y
        self.__z = x + y

# Var z is not accesible from outside
point = MyPoint(1, 2)
point.z   # error
point.__z # error
```

## Properties
```python
class Product:
    def __init__(self, price):
        self.price = price # Use price property.

    @property # Decorator to make this get method not accesible.
    def price(self):
        return self.__price # Price var is private.

    @price.setter # Decorator to make this set method not accesible.
    def price(self, value):
        if value < 0:
            raise ValueError("Price cannot be negative.")
        self.__price = value

product = Product(10)
print(product.price) # Using the price property not the price variable.
```

Notes:
- Please note that the property is used in the constructor to set the private member price. We don't use `self.__price`, but just self.price.

## Read-Only Properties
```python
class A(object):
    def __init__(self, a):
        self.__a = a

    @property
    def a(self):
        return self.__a

a = A('test')
a.a. #prints 'test''
a.a = 'pleh'
```

We will get:
```
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
AttributeError: can't set attribute
```
