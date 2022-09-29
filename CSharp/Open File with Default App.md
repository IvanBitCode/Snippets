# Open File with Default Application

```cs
FileInfo fi = new FileInfo(@"D:\Users\file.xlsx");

if (fi.Exists()) {
    // Open file using Excel and wait until it is closed.
    System.Diagnostics.Process.Start(@"D:\Users\file.xlsx").WaitForExit();
}
```
