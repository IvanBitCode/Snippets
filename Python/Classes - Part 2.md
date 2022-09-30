# Classes - Part 2
## Inheritance
- Limite inheritance at two levels max. For instance: Employee - Person - LivingCreature.
- Multiple inheritance can be used when two base clases have nothing in common and we cant to re-use the code in those.

In the following example, `Animal` is the base class and `Mammal` is the subclase.

```python
class Animal:
    def __init__(self):
        self.age = 1

    def eat(self):
        print("eat")

class Mammal(Animal): # Between parenthesis we put from which class inheritate.
    def walk(self):
        print("walk")

m = Mammal()
m.eat()  #this method is inheritated from the base class Animal.
```

## Method Overriding
- Method overriding means replace a method defined in the base class.
- If we want to use attributes defined in the base class in a derived class, we need to call the `super().__init__()` method.

```python
class Animal:
    def __init__(self):
        self.age = 1

class Mammal(Animal):
    def __init__(self):
        super().__init__()  # Calls the base class contructor
        self.weight = 2

m = Mammal()
print(m.age)     # Prints 1
print(m.weight)  # Prints 2
```

Note: If we don't call the `super().__init__()` method, we will get an exception when we try to access to `m.age`.

## A Good Example of Inheritance
We want to model the concept of a stream of data. We can read a stream from a file, network or from memory. All these strems have several thing in common: we can open them, close them, read data from them. But how we read data from a stream is dependent upon the type of a stream: reading data from a file is different from reading data from a network.

Create our custom exception (`InvalidOperationError` inherits from `Exception`):

```python
class InvalidOperationError(Exception):
    pass
```

Define our clases to demonstrate a good example of inheritance:

```python
class Stream:
    def __init__(self):
        self.opened = False

    def open(self):
        if self.opened:
            raise InvalidOperationError("The stream is already opened.")
        self.opened = True
    
    def close(self):
        if not self.opened:
            raise InvalidOperationError("The stream is already closed.")
        self.opened = False

class FileStream(Stream):
    def read(self):
        print("Reading data from a file.")

class NetworkStream(Stream):
    def read(self):
        print("Reading data from a network.")
```

This is a good example of inheritance because:
- We do not have multi level inheritance.

## Abstract Base Classes
Continuing with the previous example of inheritance.

From `Stream` class, we can see that the open method is like a asbtract concept, since what means open? Open what, a file a network?

Also, notice that `FileStream` and `NetworkStream` have a method called `read()`. It would be better to have a contract in the base clase to redefine these methods, so that, the `read()` method is allways the same name. We can solve this problems using an abstract base class.

An abstract base class defined as below, cannot be instanciated. 

```python
from abc import ABC, abstractmethod

class Stream(ABC):
    def __init__(self):
        self.opened = False

    def open(self):
        if self.opened:
            raise InvalidOperationError("The stream is already opened.")
        self.opened = True
    
    def close(self):
        if not self.opened:
            raise InvalidOperationError("The stream is already closed.")
        self.opened = False

    @abstractmethod
    def read(self):
        pass # No current implementation


class FileStream(Stream):
    def read(self):
        print("Reading data from a file.")

class NetworkStream(Stream):
    def read(self):
        print("Reading data from a network.")

stream = Stream() # Error: we cannot instantiate an abstract class.
stream.open()
```

Inheritated claseses from stream need to implement read method.

## Polymorphims
To implement polymorphism:
1. Define a base class.
2. Inside this class, define a common behaviour (method) that we need in the derivatives.
3. In another class or file (usually), define a method to achive polimorphic behaviour as shown in `def draw(control)` method below.

Let's consider the following bastract class:

```python
from abc import ABC, abstractmethod

# This class only defines the contract or interface 
# that all derivatives class should follow.
class UIControl(ABC):
    @abstractmethod
    def draw(self):
        pass

class TextBox(UIControl):
    def draw(self):
        print("TextBox")

class DropDownList(UIControl):
    def draw(self):
        print("TextBox")

def draw(control): # This function can be in another class or file.
    control.draw()

ddl = DropDownList()
draw(ddl) # This is possible since DropDownList is an instance of control.
print(isinstance(ddl, UIControl))  # Prints: True
```

If we change the draw method:

```python
def draw(controls):
    for control in controls:
        control.draw()
```

This way, we can, for example, render the UI of an app.

## Extending Built-In Types
Create a class that have all methods that the class `str` has:

```python
class MyText(str):
    # We are extending the funcionality of str class 
    # by adding a new custom method.
    def duplicate(self):
        return self + self

text = MyText()
text.duplicate("Pepe") # will print PepePepe.
```

Create a class that extends the funcionality of lists:
```python
class TrackableList(list):
    # Override append method adding extra functionality.
    def append(self, object):
        print("Append called")
        # Call the original method
        super().append(object)

list = TrackableList()
list.append("1")
```

## Data Clases
Data clases are clases that only contains data, not behaviours (methods).
```python
# Create a data class
from collections import nametuple

Point = nametuple("Point", ["x", "y"])
p1 = Point(x=1, y=2) # We use keyword arguments
p2 = Point(x=1, y=2)
print(p1 == p2) # Prints True 
```

We do not need to implement magic methods to implement the `__eq__` functionality.

In addition, we cannot modify this named tuple after initialization in constructor:
```python
p1.x = 10 # Error
```
