# Start App with Windows

App to automatically start an application on Windows startup.

You must register it in the Windows Registry by adding a new value to the following registry key:
`HKEY_CURRENT_USER\SOFTWARE\Microsoft\Windows\CurrentVersion\Run`

Fields
```cs
private string _path = @"SOFTWARE\Microsoft\Windows\CurrentVersion\Run";
private const string _keyName = "StartWithWindowsApp";
```

Sets the application to start automatically
```cs
RegistryKey key = Registry.CurrentUser.OpenSubKey(_path, true);
key.SetValue(_keyName, Application.ExecutablePath.ToString());
```

Sets the application don't start automatically.
```
RegistryKey key = Registry.CurrentUser.OpenSubKey(_path, true);
key.DeleteValue(_keyName, false);
```

Check if a key exists
```cs
RegistryKey key = Registry.CurrentUser.OpenSubKey(_path);
object keyVal = key.GetValue(_keyName);
if (keyVal == null) { /* Key does not exist */ }
```
