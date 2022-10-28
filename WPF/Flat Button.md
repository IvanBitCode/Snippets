# Flat Button

To make a button flat, just set its Style property:

```cs
<Button Style="{StaticResource {x:Static ToolBar.ButtonStyleKey}}" 
        Height="24">
    <StackPanel Orientation="Horizontal" HorizontalAlignment="Left">
        <Image Source="/Icons/help24.png"/>
        <TextBlock Text="Help" Margin="5,0,0,0"/>
    </StackPanel>
</Button>
```