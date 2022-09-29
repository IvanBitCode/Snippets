# Read embbeded file

From Visual Studio, select desired file, go to its properties and change **Build Action** to **Embbeded Resource**. Then use this code:

```cs
var assembly = Assembly.GetExecutingAssembly();
var resourceName = "ProjectName.file.txt";
string fileContent;
 
try {
    using (Stream stream = assembly.GetManifestResourceStream(resourceName))
    using (StreamReader reader = new StreamReader(stream)) {
        fileContent = reader.ReadToEnd();
    }
} catch (Except) {
    MessageBox.Show($"file.txt file not found", "Change log",
         MessageBoxButton.OK, MessageBoxImage.Error);
    return;
}
```
