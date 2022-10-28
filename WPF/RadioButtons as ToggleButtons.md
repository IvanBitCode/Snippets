# RadioButtons as ToggleButtons

```xml
<StackPanel Orientation="Horizontal" VerticalAlignment="Top" HorizontalAlignment="Center">
    <RadioButton x:Name="RbPacientes" Width="90" Margin="5,0" Background="White" IsChecked="True"
                 Style="{StaticResource {x:Type ToggleButton}}" Click="RbPacientes_Click">
        <StackPanel>
            <Image Source="Icons/pacientes32.png" Width="32"/>
            <TextBlock Text="Pacientes"/>
        </StackPanel>
    </RadioButton>
    <RadioButton x:Name="RbTratamientos" Width="90" Margin="5,0" Background="White"
                 Style="{StaticResource {x:Type ToggleButton}}" Click="RbTratamientos_Click">
        <StackPanel>
            <Image Source="Icons/tratamientos32.png" Width="32"/>
            <TextBlock Text="Tratamientos"/>
        </StackPanel>
    </RadioButton>
</StackPanel>
```