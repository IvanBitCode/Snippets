# Date And Time
## Example 1: Get Today's Date
```python
from datetime import date
today = date.today()
print("Today's date:", today)
```

## Example 2: Current Date In Different Formats
```python
from datetime import date

today = date.today()
 
# dd/mm/YY
d1 = today.strftime("%d/%m/%Y")
print("d1 =", d1)
# d1 = 16/09/2019
 
# Textual month, day and year 
d2 = today.strftime("%B %d, %Y")
print("d2 =", d2)
# d2 = September 16, 2019
 
# mm/dd/y
d3 = today.strftime("%m/%d/%y")
print("d3 =", d3)
# d3 = 09/16/19
 
# Month abbreviation, day and year 
d4 = today.strftime("%b-%d-%Y")
print("d4 =", d4)
# d4 = Sep-16-2019
```

## Example 3: Get The Current Date And Time
```python
from datetime import datetime
 
# datetime object containing current date and time
now = datetime.now()
 
print("now =", now)
 
# dd/mm/YY H:M:S
dt_string = now.strftime("%d/%m/%Y %H:%M:%S")
print("date and time =", dt_string) 
```

You will gate output like:

```
now = 2021-06-25 07:58:56.550604
date and time = 25/06/2021 07:58:56
```
