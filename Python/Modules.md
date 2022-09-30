# Modules 
A module is a file that contains python code. It can contain related functions, clases, variables, etc.

Only import the things that you need:

```python
# Importing especific objects:
from sales import calc_shipping, calc_tax

calc_shipping()
calc_tax()

# Importing the whole module as an object:
import sales

sales.calc_shipping()
```

When python look we are importing the sales module, it will find a file name `sales.py` in the current directory where we are working. If it does not find it, python will look in the predefined directory that comes in the python installation.

We can have the following list of python files:
```
app.py    # Main python file
sales.py  # Module to importe inside app.py as import sales.
```

This build in var will return the list of directories that python will look at to find a module:

```python
import sys
sys.path 
```

## Packages
- In file system terms a package is mapped to directory and a module is mapped to a file.
- A package represents a folder that contains several python files.

For instance, suppose you have an application called `app.py` in:
```
C:\PythonExamples    # root folder
    app.py           # main python file
    ecommerce        # package
        __init__.py  # See note below
        sales.py     # module
```

Note: With `__init__.py` file, python will treat the ecommerce folder as a package.

To use our package in a python program:
```python
import ecommerce.sales
ecommerce.sales.calc_tax()
```

However, this sintax is very long. A better approach would be:

```python
from ecommerce.sales import calc_tax
calc_tax()
```

If we can inport several functions, the previous from statement will be very long, so:

```python
from ecommerce import sales
sales.calc_shipping()
```

## Intra-Package References
For instance, suppose you have the following folder structure:

```
C:\PythonExamples  # root folder
    app.py         # main python file
    ecommerce      # package
        __init__.py    
        customer   # subpackage
            __init__.py
            contact.py
        shopping   # subpackage
            __init__.py
            sales.py   # module
```

We want to import the `contact.py` module in the `sales.py` module:

```python
from ecommerce.customer import contact  # Using absolute import
from ..customer import contact  # Using relative import
contact.contact_customer()
```

**Note**: Pep8 recommed using absolute importing, but if this belog too verbose, use relative import.

## Getting Info From A File And Its Package
```python
from ecommerce.customer import contact
print(sales.__name__)
print(sales.__package__)
print(sales.__file__)
```
