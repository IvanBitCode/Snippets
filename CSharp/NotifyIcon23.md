Open file with default application

```cs
FileInfo fi = new FileInfo(@"D:\Users\UnitsToReview.xlsx");

if (fi.Exists()) {
    // Open file using Excel and wait until it is closed.
    System.Diagnostics.Process.Start(@"D:\Users\UnitsToReview.xlsx").WaitForExit();
}
```
