# Type Hints
## For Lists
```python
from typing import List

my_list: List[MyClass] = []
get_my_class(my_list)

def get_my_class(list: List[MyClass]):
    pass
```

## For IO Objects
```python
from typing import TextIO

with open("file.txt") as file_obj:
    extract_text(file_obj)

def extract_obj(file: TextIO):
    pass
```
