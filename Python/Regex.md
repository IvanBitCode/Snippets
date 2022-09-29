# Regex
```python
import re

# Source file ends with a backslash character followed by a newline:
backslash_pattern = r"\\(\r\n?|\r)$"
match = re.search(backslash_pattern, file_content, re.IGNORECASE)

if match:
    print("message")

# Catch one group
match.group(1)

# Catch several groups
(g1, g3, g5) = match.group(1, 3, 5)

# Note: If group 5 is not found, g5 will be None.
```
