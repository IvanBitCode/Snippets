# Input Box Dialog

## Xaml code:

```xml
<Window ...>
    <Grid Margin="10">
        <Grid.RowDefinitions>
            <RowDefinition Height="Auto" />
            <RowDefinition Height="Auto"/>
            <RowDefinition Height="Auto"/>
        </Grid.RowDefinitions>
 
        <TextBlock x:Name="LblMsg" Grid.Row="0" TextWrapping="Wrap" Margin="0,0,0,5"
                   Text="Type your input" />
        
        <TextBox x:Name="TxtInput" Grid.Row="1" Height="23" Margin="0,0,0,15" TabIndex="1" 
                 TextWrapping="NoWrap" HorizontalAlignment="Stretch" VerticalAlignment="Top"
                 Text=""/>
        
        <Button x:Name="BtnCancel" Grid.Row="2" Content="Cancel" HorizontalAlignment="Right" 
                VerticalAlignment="Top" Width="75" IsCancel="True" Click="BtnCancel_Click" TabIndex="3"/>
        <Button x:Name="BtnOK" Grid.Row="2" Content="OK" Margin="0,0,80,0"  VerticalAlignment="Top" 
                HorizontalAlignment="Right" Width="75" Click="BtnOK_Click" TabIndex="2" IsDefault="True"/>
    </Grid>
</Window>
```

## C# Code:
```cs
public partial class WinInputBox : Window {
    private static WinInputBox mThisDialog;
    private static string mInput;
    
    private WinInputBox(string message, string title, string input) {
        InitializeComponent();
            
        txtInput.Focus();
        lblMsg.Text = message;
        Title = title;
        txtInput.Text = input;
    }
    
    public static string Show(string message, string title, string input = "") {
        mThisDialog = new WinInputBox(message, title, input);
        mThisDialog.ShowDialog();
        return mInput;
    }
    
    private void btnCancel_Click(object sender, RoutedEventArgs e) {
        Close();
    }
    
    private void btnOK_Click(object sender, RoutedEventArgs e) {
        if (txtInput.Text == "")
            return;

        mInput = txtInput.Text;
        DialogResult = true;
        Close();
    }
    
    private void Window_Closed(object sender, System.EventArgs e) {
        mThisDialog = null;
    }
}
```

## Usage:
```cs
string result = WinInputBox.Show("Enter Title:", "New Title");

if (!string.IsNullOrEmpty(result)) {
    //...
}
```
