# Drag and Drop files into TextBox and ListBox

Set this property for both TextBox and ListBox:

```cs
AllowDrop="True"
```

An this event for both TextBox and ListBox:

```cs
PreviewDragOver="Operators_PreviewDragOver"
```

For a TextBox, set this events:

```cs
PreviewDrop="TxtSelectedOperators_PreviewDrop"
```

For a ListBox set this events:

```cs
Drop="LstOperators_Drop"
```

We need two event handlers. The code is compatible for both TextBox and ListBox. The second one will the Drop event in the ListBox:

```cs
private void TxtSelectedOperators_PreviewDragOver(object sender, DragEventArgs e)
{
    e.Effects = DragDropEffects.Copy;
    e.Handled = true;
}
 
private void TxtSelectedOperators_PreviewDrop(object sender, DragEventArgs e)
{
    if (e.Data.GetDataPresent(DataFormats.FileDrop))
    {
        string[] files = (string[])e.Data.GetData(DataFormats.FileDrop);
        try
        {
            foreach (var item in files)
            {
                TxtSelectedOperators.AppendText(item + Strings.NL);
            }
        }
        catch (Exception ex)
        {
            MessageBox.Show(ex.Message, "Error", MessageBoxButton.OK, MessageBoxImage.Error);
        }
    }
}
```

For a ListBox we need an ObservableCollection<T> which will be the ItemSoruce of the ListBox:

```cs
LstOperators.ItemsSource = _OperatorsList;
```

The elements of the list can be deleted when pressing the delete key:

```cs
private void ListBox_KeyUp(object sender, KeyEventArgs e)
{
    if (e.Key == Key.Delete && LstOperators.SelectedIndex != -1) {
        int index = LstOperators.SelectedIndex;
        _OperatorsList.RemoveAt(index);
        if (index >= _OperatorsList.Count) {
            index = _OperatorsList.Count - 1;
        }
        LstOperators.SelectedIndex = index;
    }
}
```
