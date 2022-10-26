# Disparar un Evento

**1 Definir un delegado**

```cs
public delegate void VideoEncodedEventHandler(object source, EventArgs args);
```

**2 Definir un evento basado en ese delegado**

```cs
public event VideoEncodedEventHandler VideoEncoded;
```

Ver nota al final.

**3 Disparar el evento**

We need to create a method that is responsible for rasing the event. Net framework suggest this method should be protected and virtual:

```cs
protected virtual void OnVideoEncoded() { // Debe notificar a todos los suscriptores
    if(VideoEncoded != null) { // Si hay suscriptores
        VideoEncoded(this, EventArgs.Empty);
    }
    // Note 1: this refers to the class what is publishing the event, it means, this class.
    // Note 2: We are not sending event args, so we use EventArgs.Empty
}
```

**4 Llamar al método anterior cuando algún procesamiento termine**

```cs
public void Encode(Video video) {
    WriteLine("Encoding video");
    Thread.Sleep(3000);

    OnVideoEncoded(); // Lanzar el evento
}
```

**Nota**: Los pasos anteriores se hacen en la misma clase.

**5 Crear suscriptores**

Definimos el método que va realizar una acción cuando el evento suceda:

```cs
public class MailService {
    public void OnVideoEncoded(object source, EventArgs e) {
        // Hacer algo cuando el evento suceda…
    }
}
```

**6 Definir al publicador, el suscriptor y la suscripción**

Por ejemplo, lo siguiente iria en la clase main:

```cs
var video = new Video();
var videoEncoder = new VideoEncoder(); // Publicador
var mailService = new MailService(); // Suscriptor

videoEncoder.VideoEncoded += mailService.OnVideoEncoded; // Suscripción

videoEncoder.Encode(video);
```

## Como enviar datos a través de EventArgs
**1 Creamos una clase que herede de `EventArgs` y que contenga las propiedades que queremos pasar como argumentos al suscriptor:**

```cs
public class VideoEventArgs : EventArgs {
    public Video Video { get; set; }
}
```

**2 Modificamos la declaración del delegado:**

```cs
public delegate void VideoEncodedEventHandler(source object, VideoEventArgs args);
```

**3 Modificamos el método que dispara el evento:**

```cs
protected virtual void OnVideoEncoded(Video video) {
    if(VideoEncoded != null) {
        VideoEncoded(this, new VideoEventArgs(){ Video = video });
    }
}
```

**4 Modificamos la llamada al método anterior:**

```cs
public void Encode(Video video) {
    WriteLine("Encoding video");
    Thread.Sleep(3000);

    OnVideoEncoded(video); // Lanzar el evento
}
```

**5 Cambiamos el método suscriptor:**
```cs
public class MailService {
    public void OnVideoEncoded(object source, VideoEventArgs e) {
        Console.WriteLine("Sending email: " + e.Video.Title);
    }
}
```

Nota: No necesitamos crear un delegado cada vez que queremos crear un evento. Para ello podemos usar los EventHandler, los cuales son un tipo de delegado. Así, podemos eliminar la línea que declara el delegado y modificar la declaración del evento para que quede así:

```cs
public event EventHandler<VideoEventArgs> VideoEncoded;
```
