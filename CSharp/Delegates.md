# Delegates

Un delegado es un **tipo de dato** que representa referencias a métodos con una lista de parámetros determinada y un tipo de valor devuelto. Cuando se crea una instancia de un delegado, se puede asociar su instancia a cualquier método mediante una firma y un tipo de valor devuelto compatibles. Puede invocar (o llamar) al método a través de la instancia del delegado. 

Cualquier método de cualquier clase o struct accesible que coincida con el tipo de delegado se puede asignar al delegado. El método puede ser estático o de instancia.

Los delegados tienen las propiedades siguientes:
- Los delegados son como los punteros de función de C++, pero tienen seguridad de tipos.
- Los delegados permiten pasar los métodos como parámetros.
- Los delegados pueden usarse para definir métodos de devolución de llamada. 

```cs
namespace DelegadosPrj {
    delegate void MetodoDelegado(string mensaje)

    public class ClaseDelegado {
        public MetodoDelegado DireccionDelMetodo;

        if (MetodoDelegado != null) {
            // Si es diferente de null significa que ya nos pasaron la dirección de memoria
            MetodoDelegado("Mensaje proporcionado");
        }
    }
}
```

Notas:
* Línea 2: Para declarar un delegado escribimos la palabra `delegate` y luego ponemos la firma del método cuya dirección queremos que este delegado apunte. En el ejemplo anterior, el delegado va almacenar direcciones de memoria de métodos cuya firma regrese `void` y pida un `string` como parámetro. El nombre `MetodoDelegado` es el tipo de dato que estamos creando. El delegado puede declararse a nivel de namespace o a nivel de clase.
* Línea 4: Declaramos una variable de tipo `MetodoDelegado`.

Clase que usa el delegado:
```cs
namespace DelegadosPrj {
    class Ejemplo {
        ClaseDelegado c = new ClaseDelegado();
        // Pasamos el nombre del método. 
        // C# sabe que estamos pasando la dirección del mismo.
        c.DireccionDelMetodo = Escribe;
 
        void Escribe(string mensaje) {
            Console.WriteLine(mensaje);
        }
    }
}
```

## Delegados anonimos

Si el método cuya dirección de memoria se asigna al delegado solo se usa en una parte del código y no en otras, entonces
conviene crear un delegado anónimo.

```cs
UnaClase.DireccionDelMetodo = delegate(string mensaje) {
    Console.WriteLine("Delegado anónimo");
}
```

Los delegados se utilizan para pasar métodos como argumentos a otros métodos. Esta capacidad de hacer referencia a un método como parámetro hace que los delegados sean idóneos para definir métodos de devolución de llamada. Por ejemplo, una referencia a un método que compara dos objetos podría pasarse como argumento a un algoritmo de ordenación. Dado que el código de comparación está en un procedimiento independiente, el algoritmo de ordenación se puede escribir de manera más general. 

## Expresiones Lambda

El compilador sabe que la variable mensaje es string debido a la definición del delegado:

```cs
UnaClase.DireccionDelMetodo = (mensaje) => {
    Console.WriteLine("Operador lambda");
}
```

El código anterior se puede simplificar mediante:

```cs
UnaClase.DireccionDelMetodo = mensaje => Console.WriteLine("Operador lambda");
```

Esto es válido cuando la expresión lambda es una sola expresión.

## Delegados Predefinidos

El delegado `Action` representa un delegado que devuelve `void` y recibe un solo parámetro. Si queremos que el parámetro sea de tipo string, entonces: 
```cs
Action<string>
```

El delegado `Func` representa un delegado que devuelve un tipo de dato y recibe un tipo de dato. Si queremos que el parámetro sea string y que devuelva un boolean, entonces: 
```cs
Func<string, bool>.
```