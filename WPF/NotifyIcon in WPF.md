# NotifyIcon in WPF

1 Agregar las referencias 

```cs
using System.Windows.Forms
using System.Drawing
```

2 Declarar el campo:

```cs
private System.Windows.Forms.NotifyIcon _notifyIcon;
```

3 Definir el campo en el constructor de la clase:

```cs
_notifyIcon = new System.Windows.Forms.NotifyIcon()
{
    BalloonTipIcon = System.Windows.Forms.ToolTipIcon.Info,
    BalloonTipTitle = "monitor",
    Text = "Monitor",
    Visible = true
};
_notifyIcon.Click += _notifyIcon_Click;
```

4 Dentro del método Window_Loaded:

```cs
var assembly = Assembly.GetExecutingAssembly();
// Note: ico32.ico was set as Embbeded Result in its properties.
var resourceName = "PrjName.Icons.ico32.ico";
Stream iconStream = assembly.GetManifestResourceStream(resourceName);
_notifyIcon.Icon = new System.Drawing.Icon(iconStream);
```

5 Definimos el evento _notifyIcon_Click:

```cs
private void _notifyIcon_Click(object sender, EventArgs e)
{
    WindowState = WindowState.Normal;
}
```

6 Definimos eventos de la ventana:

```cs
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
    if(notifyIcon != null) {
        _notifyIcon.Visible = false;
        _notifyIcon.Dispose();
    }
}
```