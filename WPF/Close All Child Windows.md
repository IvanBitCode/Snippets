# Close All Child Windows

```cs
private void CloseAllWindows() { 
    for (int intCounter = App.Current.Windows.Count; intCounter > 0; intCounter--) {
        App.Current.Windows[intCounter].Close();
    } 
}
```

Applications stop running only when the Shutdown method of the Application is called. Shut down can occur implicitly or explicitly, as specified by the value of the ShutdownMode property.

If you set ShutdownMode to OnLastWindowClose, WPF implicitly calls Shutdown when the last window in an application closes, even if any currently instantiated windows are set as the main window (see MainWindow).

A ShutdownMode of OnMainWindowClose causes WPF to implicitly call Shutdown when the MainWindow closes, even if other windows are currently open.

In App.xml:

```cs
<Application x:Class="ProjectName.App"
             ...
             StartupUri="MainWindow.xaml">
             ShutdownMode="OnMainWindowClose"
</Application>
```