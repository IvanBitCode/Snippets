# JSON Settings

Install:
`PM> Install-Package nucs.JsonSettings`

Define this two fields
```cs
public const string jsonSettingsFile = @"D:\Documentos Ivan\myAppSettings.json";
dynamic _settings = JsonSettings.Load<SettingsBag>(jsonSettingsFile).EnableAutosave().AsDynamic();
```

Notes: 
* Dynamic settings will automatically create new keys.
* Settings are serialized and saved into a readable-editable json file due to calling 'EnableAutosave'.

Create/use a setting
```cs
_settings.StartWithWin = true;

// Can also use:
_sttings["StartWithWin"] = true;
```

Notes:
* A null is returned if a key does not exist.
* It is possible that a setting saved as int must be casted to int after loaded because it's loaded as long.
