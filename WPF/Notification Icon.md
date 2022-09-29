# Notification Icon

Agregar las referencias `System.Windows.Forms` y `System.Drawing`.

Declarar el campo:

```csharp
private System.Windows.Forms.NotifyIcon _notifyIcon;
```

Definir el campo en el constructor de la clase:

```csharp
_notifyIcon = new System.Windows.Forms.NotifyIcon()
{
	BalloonTipIcon = System.Windows.Forms.ToolTipIcon.Info,
	BalloonTipTitle = "App monitor",
	Text = "App Monitor",
	Visible = true
};
_notifyIcon.Click += _notifyIcon_Click;
```

Dentro del método Window_Loaded:

```csharp
var assembly = Assembly.GetExecutingAssembly();
// Note: doors32.ico was set as Embbeded Result in its properties.
var resourceName = "ProjectName.Icons.icon32.ico";
Stream iconStream = assembly.GetManifestResourceStream(resourceName);
_notifyIcon.Icon = new System.Drawing.Icon(iconStream);
```

Definimos el evento _notifyIcon_Click:

```csharp
private void _notifyIcon_Click(object sender, EventArgs e)
{
    WindowState = WindowState.Normal;
}
```

Definimos eventos de la ventana:

```csharp
private void Window_StateChanged(object sender, EventArgs e)
{
    if (WindowState == WindowState.Minimized)
    {
        ShowInTaskbar = false;
        _notifyIcon.Visible = true;
    }
    else if (WindowState == WindowState.Normal)
    {
        _notifyIcon.Visible = false;
        ShowInTaskbar = true;
    }
}

private void Window_Closed(object sender, EventArgs e)
{
    if (notifyIcon != null) {
        _notifyIcon.Visible = false;
        _notifyIcon.Dispose();
    }
}
```
