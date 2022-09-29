# Command line args

Arguments are parsed using `argparse`, which is a python build-in function.

```python
import argparse

ap = argparse.ArgumentParser(description="Info", epilog="Additional info")

# Add arguments to the parser
ap.add_argument("-w", "--path", required=True, help="Path is required.")
ap.add_argument("-t", "--type", required=True, help="Type is required.")

# The action set to 'store_true' will store the argument as True if present.
ap.add_argument("--output", action="store_true") 

# Type determines the type of the argument
ap.add_argument("-n", type=int, help="number of random integers")

# Default option specifies the default value, if the value is not given
ap.add_argument("-e", type=int, default=2, help="exponent")

# The choices option limits the arguments to the given list
ap.add_argument("--date_format", choices=['std', 'iso', 'unix'])
$ mtype.py --date_format iso
$ mtype.py --date_format std

args = vars(ap.parse_args())

# Get arguments
workarea_dir = args['path']
```
