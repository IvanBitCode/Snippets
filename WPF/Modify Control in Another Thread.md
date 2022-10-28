# Modify Control in Another Thread

```cs
Application.Current.Dispatcher.Invoke(new Action(() => {
    // Code here...
}));
```

Or:

```cs
lblMsj.Dispatcher.Invoke(new Action(delegate () {
    lblMsj.Content = "";
 }));
```

Copy to clipboard
```cs
Clipboard.SetText(txtCmdEnv.Text);
```
