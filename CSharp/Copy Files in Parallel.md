# Copy Files in Parallel

```cs
foreach (string directory in directories)
{
    System.Threading.Tasks.Parallel.ForEach(Directory.GetFiles(directory), (file) =>
    {
        File.Copy(file, file.Replace(directory, targetPath), true);
    });
}
```