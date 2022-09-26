# DataGrid selected row background color

```xml
<DataGrid x:Name="DgPaths" ItemsSource="{Binding}" ...> 
    <DataGrid.Resources> 
        <!--Selected row background color--> 
        <SolidColorBrush x:Key="{x:Static SystemColors.HighlightBrushKey}" 
                         Color="#0080FF"/> 
        <!--Selected inactive row background color--> 
        <SolidColorBrush x:Key="{x:Static SystemColors.InactiveSelectionHighlightBrushKey}" 
                         Color="#99CCFF"/> 
    </DataGrid.Resources> 
</DataGrid> 
```
