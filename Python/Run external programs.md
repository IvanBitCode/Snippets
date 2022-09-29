# Run External Programs
## Run a Command
```python
import subprocess

# Syntax:
# returned = subprocess.run(["command1", "arg1"])

# Example
completed = subprocess.run(["ls", "-l"])
print(completed.args) # prints: ['ls', '-l']
print(completed.returncode) # prints: 0
print(completed.stderr) # prints: None
print(completed.stdout) # prints: None
```

Notes:
* Any non zero value indicates an error. 0 means no errors.
* stderr is None because the command does not throw any error.
* stdout is None because we are not capturing the output, it is printed in the terminal window.

## Save the Output to a String
First, we need to capture the output. Therefore, the output will not be printed on the terminal.
* The output will be capture in the stdout property.
* We will use text argument to capture the output as string.

```python
completed = subprocess.run(["ls", "-l"], 
                           capture_output=True, 
                           text=True)
completed.stdout # output of the command as string
```

## Run Other Python Script as a Separate Process

```python
completed = subprocess.run("python3 other.py", 
                           capture_output=True, 
                           text=True)
```
Note: The other.py script will be executed in another process and will not share variables.

## Check for Errors Before Continue
```python
if completed.returncode != 0:
    print(completed.stderr)
```

If we add the check argument, an exception will be thrown:
```python
try:
    completed = subprocess.run("python3 other.py"], 
                               capture_output=True, 
                               text=True,
                               check=True)
    print(completed.returncode)
except subprocess.CalledProcessError as ex:
    print(ex)
```
