# Persistent Settings

## Adding settings strings to the project

1. Abrir las propiedades del proyecto.
2. Ir a la pestaña Settings.
3. Agregar los elementos necesarios. El contenido de cada setting puede ser multilinea.
4. Guardar cambios.
	
## Binding a setting to a textbox:
1 Add the following name space in xaml:

```xml
xmlns:p="clr-namespace:YOUR_APP_NAME.Properties"
```

2 Bind thet attribute of the textbox:

```cs
Text="{Binding Source={x:Static p:Settings.Default}, Path=AppDir, Mode=TwoWay}"
```

Note: The two-way binding automatically updates the AppDir setting, and similarly at startup, the TextBox will be populated with the most recently saved AppDir value.
	
3 Remember that you have to persist saved settings by:

```cs
private void OnExit(object sender, ExitEventArgs e) { 
    Properties.Settings.Default.Save(); 
}
```
