# Remove Read-only Attribute from File

```cs
FileAttributes attributes = File.GetAttributes(file);

if ((attributes & FileAttributes.ReadOnly) == FileAttributes.ReadOnly)
{
    attributes = attributes & ~FileAttributes.ReadOnly;
    File.SetAttributes(file, attributes);
}
```