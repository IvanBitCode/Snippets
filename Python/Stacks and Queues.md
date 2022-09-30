# Stacks and Queues
## Stacks
```python
browsing_session = []

# Adding a element to the list:
browsing_session.append(1)

# Removing element from the Stack (last in - first out)
browsing_session.pop()

# Accesing to the last item (the newest one in the stack)
browsing_session[-1]
```

## Queues
```python
from collections import deque

# Creating a queue
queue = deque([])

# Add items to the queue
queue.append(1)
queue.append(2)

# Remove items in the queue (first in - first out)
queue.popleft();
```
