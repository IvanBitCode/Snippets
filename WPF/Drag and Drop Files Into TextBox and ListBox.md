# Drag and Drop Files Into TextBox and ListBox

Set this property for both TextBox and ListBox:

```cs
AllowDrop="True"
```

An this event for both TextBox and ListBox:

```cs
PreviewDragOver="Op_PreviewDragOver"
```

For a TextBox, set this events:

```cs
PreviewDrop="TxtSelectedOp_PreviewDrop"
```

For a ListBox set this events:

```cs
Drop="LstOp_Drop"
```

We need two event handlers. The code is compatible for both TextBox and ListBox. The second one will the Drop event in the ListBox:

```cs
private void TxtSelectedOp_PreviewDragOver(object sender, DragEventArgs e)
{
    e.Effects = DragDropEffects.Copy;
    e.Handled = true;
}
 
private void TxtSelectedOp_PreviewDrop(object sender, DragEventArgs e)
{
    if (e.Data.GetDataPresent(DataFormats.FileDrop))
    {
        string[] files = (string[])e.Data.GetData(DataFormats.FileDrop);
        try
        {
            foreach (var item in files)
            {
                TxtSelectedOp.AppendText(item + Strings.NL);
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
LstOp.ItemsSource = _OperatorsList;
```

The elements of the list can be deleted when pressing the delete key:

```cs
private void ListBox_KeyUp(object sender, KeyEventArgs e)
{
    if (e.Key == Key.Delete && LstOp.SelectedIndex != -1) {
        int index = LstOp.SelectedIndex;
        _OpList.RemoveAt(index);
        if (index >= _OpList.Count) {
            index = _OpList.Count - 1;
        }
        LstOp.SelectedIndex = index;
    }
}
```
