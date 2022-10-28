# Only One Instance of No-Modal Window

```cs
if (com == null) {
    com = new Commands();
    com.Show();
} else if (com.IsLoaded) {
    com.Activate();
} else { // Is disposed, create a new instance
    com = new Commands();
    com.Show();
}
```