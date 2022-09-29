# DataGrid with Filter TextBox

## Quick Example

Xaml

```xml
<DataGrid x:Name="DgPaths" ItemsSource="{Binding}" AutoGenerateColumns="True">
    <DataGrid.Resources>
        <!--Selected row background color-->
        <SolidColorBrush x:Key="{x:Static SystemColors.HighlightBrushKey}" Color="#0080FF"/>
        <!--Selected row background color-->
        <SolidColorBrush x:Key="{x:Static SystemColors.InactiveSelectionHighlightBrushKey}" Color="#99CCFF"/>
    </DataGrid.Resources>
</DataGrid>
```

The code

```cs
ObservableCollection<Path3_Work> _ObsWorkPaths = new ObservableCollection<Path3_Work>();
DgPaths.ItemsSource = _ObsWorkPaths;
```

## Detailed Example

```xml
<DataGrid x:Name="dgEnvVars" ItemsSource="{Binding}" AutoGenerateColumns="False" AlternatingRowBackground="#EEE" 
          AlternationCount="2" SelectionMode="Single" SelectionUnit="FullRow" RowHeight="25" IsReadOnly="True"
          Margin="0,75,0,117" CanUserAddRows="False" CanUserDeleteRows="False" CanUserResizeRows="False" 
          HeadersVisibility="Column" SelectionChanged="DgEnvVars_SelectionChanged">
    <DataGrid.Columns>
        <DataGridTextColumn Header="Type" Binding="{Binding Type}" Width="70" />
        <DataGridTextColumn Header="Name" Binding="{Binding Name}" />
        <DataGridTextColumn Header="Value" Binding="{Binding Value}" Width="400" />
    </DataGrid.Columns>
</DataGrid>
```

### Filter rows in DataGrid

```cs
ObservableCollection<EnvVar> obsEnvVars = new ObservableCollection<EnvVar>();
private ICollectionView _itemList;

foreach (DictionaryEntry variable in Environment.GetEnvironmentVariables(EnvironmentVariableTarget.User))
{
    obsEnvVars.Add(new EnvVar() {
        Type = "User",
        Name = variable.Key.ToString(),
        Value = variable.Value.ToString()
    });
}

foreach (DictionaryEntry variable in Environment.GetEnvironmentVariables(EnvironmentVariableTarget.Machine))
{
    obsEnvVars.Add(new EnvVar()
    {
        Type = "System",
        Name = variable.Key.ToString(),
        Value = variable.Value.ToString()
    });
}

// To filter the DataGrid
CollectionViewSource itemSourceList = new CollectionViewSource() { Source = obsEnvVars };
_itemList = itemSourceList.View;
dgEnvVars.ItemsSource = _itemList;
```

### EnvVar Class for the ObservableCollection
The class implements the INotifyPropertyChanged interface to check for changes in the items of the collection.

```cs
public class EnvVar : INotifyPropertyChanged
{
    public event PropertyChangedEventHandler PropertyChanged;
 
    private string type;
    private string name;
    //...
 
    public string Type {
        get { return type; }
        set {
            if (value != type)
            {
                type = value;
                NotifyPropertyChanged("Type");
            }
        }
    }
 
    public string Name {
        get { return name; }
        set {
            if (value != name)
            {
                name = value;
                NotifyPropertyChanged("Name");
            }
        }
    }
 
    private void NotifyPropertyChanged(string info)
    {
        if (PropertyChanged != null)
        {
            PropertyChanged(this, new PropertyChangedEventArgs(info));
        }
    }
}
```

### Filter when text in TextBox changes

```cs
private void TxtFind_TextChanged(object sender, TextChangedEventArgs e)
{
    _itemList.Filter = new Predicate<object>(item => ((EnvVar)item).Name.ToLower().Contains(txtFind.Text.ToLower()));
}

private void DgEnvVars_SelectionChanged(object sender, SelectionChangedEventArgs e)
{
    EnvVar varEnv = ((EnvVar)dgEnvVars.SelectedItem);
    if (varEnv == null)
    {
        txtDetails.Text = "";
    }
    else
    {
        txtDetails.Text = $"{varEnv.Name}:{Environment.NewLine}{varEnv.Value}";
    }
}
```

