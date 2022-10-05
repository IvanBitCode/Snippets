# Paths, Directories and Files
## Paths
```python
# We need to import:
from pathlib import Path

# Create a raw path using the r prefix
Path(r"C:\Programs\Microsoft")

# Combine paths using /
Path(r"C:\Programs\Microsoft") / Path("VS Code") / "V17"

# Return the home directory of the current user
Path.home()

# Check if a path exists, is a directory or if it is a file
path = Path(r"C:\Programs\Microsoft")
path.exists()
path.is_file()
path.is_dir()

# Gets the file name of a path, extension or parent
path = Path(r"C:\Programs\Microsoft\Word.exe")
path.parent  # Gets: C:\Programs\Microsoft
path.name    # Gets: Word.exe
path.stem    # Gets: Word
path.suffix  # Gets: .exe (extension)
path.parent.name  # Gets: Microsoft

# Create a new path re using an existing one
path = Path(r"C:\Programs\Microsoft\Word.exe")
path2 = path.with_name("Excel.exe")
print(path2)  # Prints C:\Programs\Microsoft\Excel.exe

path = Path(r"C:\Programs\Microsoft\Word.exe")
path2 = path.with_suffix(".txt")
print(path2)  # Prints C:\Programs\Microsoft\Excel.txt
```

## Directories
```python
# We need to import:
from pathlib import Path

path = Path("ecommers")
path.exists() # Check if dir exists
path.mkdir()  # Create dir
path.rmdir()  # Remove dir
path.rename("ecommers2")

# Get a list of directories and files from a path (not recursively)
path.iterdir()  # Returns a generator object.

# Note: a generator object gets a new value with every iteration. 
#       This is more efficent for directories with thousands of files. 
# Example:
for p in path.iterdir():
    print(p)

# Convert the generator to a list
paths = [p for p in path.iterdir()]

# If we are only interested in files:
paths = [p for p in path.iterdir() if p.is_file]

# Get a list of directories and files from a path RECURSIVELY
# We use the recursive glob function (rglob):
path = Path(r"C:\Programs\Microsoft")
py_files = [p for p in path.rglob("*.py")]

# Get the current user directory:
os.path.expanduer('~')  # Gets C:\Users\ivanb
```

## Files
```python
# We need to import:
from pathlib import Path

path = Path("ecommers/file.py")
path.exists()  # Check if file exists
path.rename("init.py") # Rename file
path.unlink()  # Delete file

# Get the content of a file as a string
path = Path("ecommers/file.py")
path.read_text()

# The read_text() method do the same job as (Therefore it is better to use read_text()):
with open("file.py", "r") as file:
   ...

# Get lines of a file
with open("file.txt") as file:
    lines = [line.strip() for line in file]
    lines.remove('') # Remove empty lines from list.

    # Remove empty lines from list in one line:
    lines = [line.strip() for line in file if line.strip()]

# Create a file set its content
path = Path("ecommers/file.py")
path.write_text("content")

# Writing a list to a file
path.write_text("\n".join(python_list))

# Copying, moving and renaming files
import shutil

source = Path("ecommers/file1.txt")
target = Path("ecommers/prod/file1.txt")
shutil.copy(source, target)
# Note: If target file exist, it will be replaced.

os.rename(source, dest)
```

## Copy files in parallel
The `concurrent.futures` module provides high-level interface for asyncronously executing callables.
* The `ThreadPoolExecutor` is an `Executor` subclass that uses a pool of threads to execute calls asyncronously.
* The function `submit(fn, *args, **kargs)` schedules `fn` to be executed with its `*args` and `**karg`s.
    - The `*args` parameter in a function is used to optionally pass a variable number of positional arguments.
    - The `**kwargs` parameter in a function is used to optionally pass a variable number of named arguments.

```python
import concurrent.futures

with concurrent.futures.ThreadPoolExecutor(max_workers=4) as executor:
    for file in files:
        executor.submit(shutil.copy, file, target_file)
```

To avoid the for loop:

```python
with concurrent.futures.ThreadPoolExecutor(max_workers=4) as executor:
    executor.map(os.remove, files) # files is a list or iterable
```

## Getting file persmissions

```python
import os
import stat

mask = oct(os.stat(file).st_mode)[-3:]
```

`mask` will be:
- 444: Users are only able to read the file. They cannot write ot it or execute it.
- 666: Users can read and write but cannot execute the file.

To change the file permissions:

```python
os.chmod(file, stat.S_IWRITE)
```
