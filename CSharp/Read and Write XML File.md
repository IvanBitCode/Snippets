# Read and Write XML File

## XML File Example
```xml
<?xml version="1.0" encoding="UTF-8"?>
<root>
  <work>
    <description>Project Name 1</description>
    <path>C:\User\Docs\Prj1</path>
  </work>
  <work>
    <description>Project Name 2</description>
    <path>C:\User\Docs\Prj2</path>
  </work>
</root>
```

## Write
```cs
XmlDocument doc = new XmlDocument();
XmlNode docNode = doc.CreateXmlDeclaration("1.0", "UTF-8", null);
doc.AppendChild(docNode);
 
XmlNode rootNode = doc.CreateElement("root");
doc.AppendChild(rootNode);
 
foreach (PathPrj item in ListPaths) {
    XmlNode workNode = doc.CreateElement("work");
    rootNode.AppendChild(workNode);
 
    XmlNode descriptionNode = doc.CreateElement("description");
    descriptionNode.InnerText = item.Description;
    workNode.AppendChild(descriptionNode);
 
    XmlNode pathNode = doc.CreateElement("path");
    pathNode.InnerText = item.Path;
    workNode.AppendChild(pathNode);
 
    rootNode.AppendChild(workNode);
}
 
doc.Save("filePath");
```

## Read
```cs
XmlDocument doc = new XmlDocument();
doc.Load(filePath);

foreach (XmlNode rootNode in doc.DocumentElement.ChildNodes)
{
    var work = new Work();
    foreach (XmlNode node in rootNode)
    {
        switch (node.Name)
        {
            case "description":
                work.Description = node.InnerText;
                break;
            case "path":
                work.Path = node.InnerText;
                break;
        }
    }
    workList.Add(work);
}
```