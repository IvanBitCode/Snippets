# Async Tasks

## Method that returns a Task without result
```cs
private Task ListCarsAsync() {
    Task task = Task.Run(() => {
        // Body of task...
    });
    return task;
}
```

Call the async method:
```cs
await ListCarsAsync();
```

## Method that returns an async Task without result
```cs
private async Task StartEvalAsync() {
    Credentials cred = GetCredentials();
    if (cred == null) { return; }
 
    Progress<MyProgress> myProgress = new Progress<MyProgress>();
    myProgress.ProgressChanged += myProgress_ProgressChanged;
 
    try {
        var review = new Utils();
        await review.EvaluateAsync(myProgress);
    } catch (Exception ex) {
        throw ex;
    } finally {
        myProgress.ProgressChanged -= MyProgress_ProgressChanged;
    }
 
    MessageBox.Show("Message");
    # We do not need a return statement here.
}
```

Note that:
* If we need to return early from the StartEvalAsync() method, we only use the return; statement.
* StartEvalAsync() method does not create any task, just wait that the async method to finish.

Calling previous method inside an event handler:
```cs
await StartEvalAsync();
```

## Method that returns an async Task with result
Define a method that returns, for instance, a list of strings:

```cs
public async Task<List<string>> EvalAsync() {
    Task<List<string>> myTask = Task.Run(() => {
        var resultList = new List<string>();
        // Do something with the list...
        return resultList;
    });

    await myTask;
    return myTask.Result;
}
```

Call the async method:
```cs
List<string> resultList = await EvalAsync();
```