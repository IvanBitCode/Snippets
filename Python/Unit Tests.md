# Unit Tests
To write a unit test for the build-in function `sum()`, you would check the output of `sum()` against a known output. For example, here is how you check that the `sum()` of the numbers (1, 2, 3) equals 6:

```python
>>> assert sum([1, 2, 3]) == 6, "Should be 6"
```

This will not output anything in the REPL because the value are correct.

If the result from `sum()` is incorrect, this will fail with an `AssertionError` and the message `"Should be 6"`:

```python
>>> assert sum([1, 1, 1]) == 6, "Should be 6"

Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
AssertionError: Should be 6
```

## unittest Library
This is a build-in python library.
1. Create a python file to test your code. You can use any name.
2. Import `unittest` from the standard library.
3. Import the function you want to test.
4. Create a testing class that inherits from `unittest.TestCase`.
5. Write a series of methods to test all the cases of your function behaviour. 
    - Remember that every method that starts with `test_` will be run automatically when you run `test_name_function.py`.
6. Run your test file.

Suppose you have this function in a file called `name_utils.py`:

```python
def formatted_name(first_name, last_name):
    full_name = first_name + ' ' + last_name
    return full_name.title()
```

You create your test file `test_names_unittest.py`, as follow:
```python
import unittest
from name_utils import formatted_name

class NamesTestCase(unittest.TestCase):
    def test_formated_name(self):
        result = formatted_name("pete", "seeger")
        self.assertEqual(result, "Pete Seeger")

if __name__ == '__main__':
    unittest.main()
```

Run your test file:

`$ python test_names_unittest.py`
