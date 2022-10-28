# Application-Level Styles

In App.xml file, add this:

```xml
<Application.Resources>
    <!--This will apply to all TextBoxes(no x:Key)-->
    <Style TargetType="{x:Type TextBox}">
        <Setter Property="VerticalContentAlignment" Value="Center"/>
        <Setter Property="Height" Value="23"/>
        <Setter Property="TextWrapping" Value="NoWrap"/>
    </Style>

    <!--This will apply to all Buttons(no x:Key)-->
    <Style TargetType="{x:Type Button}">
        <Setter Property="Height" Value="23"/>
        <Setter Property="Width" Value="75"/>
    </Style>

    <!--This will apply to all Label(no x:Key)-->
    <Style TargetType="{x:Type Label}">
        <Setter Property="Height" Value="23"/>
        <Setter Property="Padding" Value="0"/>
        <Setter Property="VerticalContentAlignment" Value="Center"/>
    </Style>
</Application.Resources>
```