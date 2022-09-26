# TaskbarItem Progressbar
**Add the TaskbarItemInfo to XAML**

```xml
<Window ...>
    <Window.TaskbarItemInfo>
        <TaskbarItemInfo x:Name="taskbarInfo" Description="Master List"/>
    </Window.TaskbarItemInfo>
    ...
</Window>
```

**Set the state**

Set the state before start the background process:

```csharp
TaskbarItemProgressState.Indeterminate;
// or
taskbarInfo.ProgressState = TaskbarItemProgressState.Normal;
```

When the background process ends:

```csharp
taskbarInfo.ProgressState = TaskbarItemProgressState.None;
```

**Change the progress**

It can be set to a double between 0 (0%) and 1 (100%):

```csharp
TaskbarInfo.ProgressValue = 0;
```
