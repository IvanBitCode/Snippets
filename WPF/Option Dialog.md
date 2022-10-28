# Option Dialog

## XAML
```xml
<Window ...>
    
    <StackPanel Margin="10">
        <TextBlock x:Name="TxtMessage" Text="Message" Margin="0,0,0,10" TextWrapping="Wrap"/>
        <ListBox x:Name="OptionsList" SelectionMode="Single" MinHeight="50" MaxHeight="140">
            <ListBox.ItemTemplate>
                <DataTemplate>
                    <Label Content="{Binding}" VerticalContentAlignment="Center"/>
                </DataTemplate>
            </ListBox.ItemTemplate>
        </ListBox>
 
        <StackPanel Margin="0,10,0,0" Orientation="Horizontal" HorizontalAlignment="Right">
            <Button x:Name="BtnOK" Content="OK" Margin="0,0,10,0" Click="BtnOK_Click"/>
            <Button x:Name="BtnCancel" Content="Cancel" IsCancel="True" Click="BtnCancel_Click"/>
        </StackPanel>
    </StackPanel>
<Window>
```

## Code

```cs
public partial class WinOptionDialog
{
    public int SelectedIndex { get; set; }
    public string SelectedValue { get; set; }
 
    public WinOptionDialog(string title, string message, string[] options)
    {
        InitializeComponent();
        Title = title;
        TxtMessage.Text = message;
        OptionsList.ItemsSource = options;
    }
 
    private void BtnOK_Click(object sender, RoutedEventArgs e)
    {
        SelectedIndex = OptionsList.SelectedIndex;
        SelectedValue = OptionsList.SelectedValue.ToString();
 
        DialogResult = true;
        Close();
    }
 
    private void BtnCancel_Click(object sender, RoutedEventArgs e)
    {
        Close();
    }
}
```

## Usage
```cs
WinOptionDialog opDlg = new WinOptionDialog(
    "Option Dialog", 
    "Select only one option:", 
    new string[] { "Option 1", "Option 2", "Option 3", "Option 4", "Option 5" });
    
if (opDlg.ShowDialog() == true) {
    MessageBox.Show($"Index = {opDlg.SelectedIndex}, Value = {opDlg.SelectedValue}.");
}
```