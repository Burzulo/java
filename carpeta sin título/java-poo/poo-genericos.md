# 📌 Genericos

<br>

- [...](#-)
- [...](#-)

<br>

## 📂 Genericos

Los genéricos son una característica de Java que permite definir clases, interfaces y métodos con **tipos de datos parametrizados**.  
Esto permite escribir código más flexible y reutilizable, garantizando la seguridad de tipos (Type Safety) desde el momento de la compilación.

Su principal objetivo es proporcionar una manera de manejar objetos de diferentes tipos sin perder la integridad de los datos.  

La principal ventaja es ELIMINACIÓN del CASTEO EXPLÍCITO.

<br>

### Sintaxis Básica

La sintaxis se basa en el uso de parámetros de tipo (`< >`). La letra `T` actúa como un marcador de posición que será reemplazado por un tipo de dato real cuando se instancie la clase.

```java
// Ejemplo: Una caja multiuso
     
public class Caja<T> {   // IMPORTANTE declarar <T> al lado del nombre de la clase
    private T contenido;

    public void poner(T contenido) {
        this.contenido = contenido;
    }

    public T sacar() {
        return this.contenido;
    }
}
```

  <br>

- #### Uso desde el método `main`

  Gracias al operador diamante `<>`, el compilador ya sabe exactamente qué tipo de dato hay dentro.

  ```java
  public static void main(String[] args) {
  
    // Caja para Cadenas
    Caja<String> cajaDeString = new Caja<>();
    cajaDeString.poner("Hola Generics");
    String texto = cajaDeString.sacar(); // No necesita casteo

    // Caja para Enteros
    Caja<Integer> cajaDeEnteros = new Caja<>();
    cajaDeEnteros.poner(32); // Se pasa el int directamente
    Integer numero = cajaDeEnteros.sacar();
    
    // ERROR DE COMPILACIÓN
    // cajaDeEnteros.poner("32"); // El compilador impide esto porque espera un Integer y se intento  
    // poner un String ("32")

  }
  ```
  
  <br>

- #### El problema que resuelve

  Antes de los genéricos, se usaba la clase `Object` para guardar cualquier cosa, pero esto obligaba a convertir el dato manualmente al sacarlo, lo cual era peligroso.

  ```java
  ArrayList lista = new ArrayList();
  lista.add("Hola");
  String texto = (String) lista.get(0); // Requiere casteo manual y puede fallar en la ejecución
  ```

<br>

### Convenciones de Nomenclatura

  Aunque la `T` es la letra más comúnmente utilizada para representar un tipo genérico, hay varias letras que se utilizan para representar diferentes tipos de parámetros

  | Letra | Significado | Uso común | Ejemplo |
  |:--:|:--|:--|:--|
  | `T` | Type | Representa un tipo genérico | public class Caja<T> {...} |
  | `E` | Element | Representa un elemento, común en colecciones | public interface List<E> {...} |
  | `K` | Key | Representa una clave, común en mapas | public interface Map<K, V> {...} |
  | `V` | Value | Representa una clave, común en mapas | public interface Map<K, V> {...} |
  | `N` | Number | Representa un número | public class NumericContainer<N extends Number< {...} |
  | `S`, `U`, `V` | 2nd, 3rd, 4th types | Representan un segundo, tercer y cuarto tipo genérico | public class Triple<T, U, V> {...} |

<br>

> [!TIP]  
> Los genéricos solo funcionan con Clases Wrapper (`Integer`, `Double`, `Boolean`).  
> No se puede usar tipos primitivos como `int` o `double` dentro de los diamantes `< >`.