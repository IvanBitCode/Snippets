# Getting progress report

Podemos crear una clase que se encargue de almacenar información del progreso:

```cs
class InfoReported {
    public int ActualProgress { get; set; }
    public string Mensaje { get; set; }
}
```

Cada vez que se realiza un progreso, reportamos ese progreso usando el método **Report**. Dicha info la podremos recuperar mas adelante:

```cs
class AnotherClass {
    public static async Task<DataModel> MethodAsync(IProgress<InfoReported> progreso) {
        foreach(...) {
            // Perform consuming time operations…
            // Note: you must create a InfoReported obj. Before reporting progress.
            InfoReported infoRep = new InfoReported();
            infoRep.Mensaje = "Mensaje del progreso";
            infoRep.ActualProgress = (actual * 100) / total;
            progreso.Report(infoRep);
        }
    }
}
```

Creamos un objeto tipo **Progress** que nos permitirá monitorear el progreso, al cual le definimos un manejador de eventos, **ReportarProgreso**. Este manejador de eventos se llamará automáticamente cuando se reporte un progreso usando el método **Report()**. La variable progreso la pasamos al método **MethodAsync()**:

```cs
class UiWin : Window {
    public async void MyEvent(...) {
        Progress<InfoReported> progreso = new Progress<InfoReported>();
        progreso.ProgressChanged += ReportarProgreso;
        await MethodAsync(progreso);
    }
    
    private void ReportarProgreso(object sender, ActualProgress e) {
        // Actualizar controles en la UI mostrando el progreso.
        // mediante e.Mensaje y e.ActualProgress.
    }
}
```

# Cancelling a progress

Para cancelar un progreso, necesitamos un **CancellationToken**, del cual pasamos la propiedad **Token** al método **MethodAsync()**:

```cs
class UiWin : Window {
    CancellationTokenSource cts; // System.Threading.CancellationTokenSource
    
    public async void MyEvent(...) {
        ...
        try {
            cts = new CancellationTokenSource();
            await MethodAsync(progreso, cts.Token);
        } catch(OperationCanceledException) {
            // Actualizar controles en la UI diciendo que la operación se canceló.
        }
    }
    
    private void Cancel_Click(...) {
        cts.Cancel();
    }
}

class AnotherClass {
    public static async Task<DataModel> MethodAsync(IProgress<InfoReported> progreso, 
                                                    CancellationToken ct) {
        ...
        foreach(...) {
            // Perform consuming time operations…

            ct.ThrowIfCancellationRequested();

            // También podemos usar ct.IsCancellationRequested, 
            // el cual nos permitirá hacer algo de limpieza antes de cancelar.
            // ...
        }
    }
}
```
