# 📌 Manejo de Excepciones

<br>

- [Jerarquía de errores: `Throwable`, `Error` vs `Exception`](#-jerarquia-de-errores)
- [Bloques de control: `try`, `catch`, `finally`](#-bloques-de-control)
- [Flujo de Excepciones: `throw` vs `throws`](#-flujo-de-excepciones)
- [❌ Creación de Excepciones Personalizadas](#-)

<br>

Una excepción es un evento o condición inusual que ocurre durante la ejecución de un programa y que interrumpe el flujo normal de la ejecución.  
Las **excepciones** se utilizan para manejar y señalar errores y situaciones excepcionales.

Muchas cosas pueden causar excepciones, como errores de hardware, operaciones matemáticas no posibles (dividir por cero), errores de programa (error de desbordamiento de un array), apertura de un archivo inexistente, etc ...

<br>

## 📂 Jerarquia de errores

### ✧ La Clase ``Throwable``

En el ecosistema Java, todo lo que puede ser "lanzado" (usando la palabra clave `throw`) y posteriormente "capturado" (en un bloque `catch`) debe descender de la clase `java.lang.Throwable`.

Esta es la superclase de todos los errores y excepciones en el lenguaje.  
Si una clase no hereda de `Throwable`, la JVM no la reconocerá como un objeto que pueda interrumpir el flujo normal del programa.

<br>

La jerarquía se divide inmediatamente en dos grandes ramas que tienen propósitos semánticos y prácticos completamente distintos: `Error` y `Exception`.

- ### `java.lang.Error`

  La clase `Error` indica problemas razonablemente graves que una aplicación normal **no debería intentar capturar**.  
  Estos representan condiciones anormales que suelen originarse en la propia JVM o en el entorno de ejecución, más que en la lógica del código.
  
  Un `Error` suele ser terminal. Ejemplo: si nos quedamos sin memoria física (`OutOfMemoryError`) o si hay un desbordamiento en la pila de llamadas por una recursión infinita (`StackOverflowError`), el programa generalmente no puede hacer nada para sanear la situación y continuar funcionando de forma segura.
  
  En el mundo profesional, ver un `Error` suele significar que hay un problema de configuración de hardware, de la JVM o un fallo de diseño estructural masivo.
  
  <br>
  
- ### `java.lang.Exception`
  
  Por otro lado, la clase `Exception` representa condiciones que una aplicación **sí debería querer capturar**.  
  Aquí es donde vive la lógica de recuperación de fallos.
  
  Si un archivo no existe o un servidor de base de datos no responde, Java lanza una excepción para que el desarrollador decida qué hacer: ¿reintentar la conexión?, ¿pedir al usuario otra ruta de archivo?, ¿cerrar los recursos de forma elegante?.
  
  Dentro de esta rama, existe una subdivisión crítica que separa las excepciones que el compilador obliga a gestionar (**Checked**) de aquellas que ocurren por errores de programación (**Unchecked** o `RuntimeException`).
  
<br>

## 📂 Bloques de control

En Java el uso de bloques de control, permiten gestionar los errores y las situaciones anormales que ocurren durante la ejecución de un programa, permitiendo que la aplicación continúe su funcionamiento o termine de forma controlada.

Los **Bloques de Control** fundamentales para este manejo son:

- ``try`` bloque donde puede ocurrir la excepción.
- ``catch`` es como el «else» del try, se ejecuta al disparar una excepción en el bloque ``try``.
- ``finally`` bloque de código que se ejecuta SIEMPRE, sin importar si hubieron errores o no.

<br>

### ✧ ``try`` / ``catch``

Para atrapar las excepciones se encierra en un bloque ``try`` las **instrucciones que generan excepciones**. Y todo bloque ``try`` requiere que sea seguido por un bloque ``catch``

````java
try {
    // instrucciones 
}
catch (Exception nombreParámetro) {
    // instrucciones a seguir si ocurre una excepción
}
````

Luego de la palabra clave ``catch`` se indica entre paréntesis el nombre de un ``parámetro`` cualquiera y el nombre de la ``excepción`` a capturar.

El bloque ``catch`` normalmente no se ejecuta salvo en los casos excepcionales que dentro del bloque ``try`` informa que se disparó dicha ``excepción``.

<br>

### ✧ ``finally``

El objetivo de este bloque es **liberar recursos** que se solicitan en el bloque ``try``. El bloque ``finally`` se **ejecuta siempre**, inclusive si se genera la captura de una excepción.  
Los recursos más comunes que se deben liberar son las conexiones a bases de datos, uso de archivos y conexiones de red.  
Un recurso que no se libera impide que otro programa lo pueda utilizar.

Al disponer la liberación de recursos en el bloque ``finally`` nos aseguramos que todo recurso se liberará, inclusive aunque se dispare una excepción. Si NO se disparan ninguna excepción en un bloque ``try`` luego de esto se ejecuta el bloque ``finally``.

El bloque ``finally`` es opcional y en el caso de estar presente se coloca después del último bloque ``catch``.

````java
try {
    // instrucciones 
}
catch (Exception nombreParámetro) {
    // instrucciones a seguir si ocurre una excepción
}
finally (Exception nombreParámetro) {
    // instrucciones que siempre se ejecutan
}
````

<br>

## 📂 Flujo de Excepciones

Para gestionar el flujo de transferencia de control ante una condición anómala, Java implementa un mecanismo de propagación basado en dos palabras claves que suenan parecido pero cumplen funciones totalmente distintas: `throw` y `throws`.

### ✧ `throws`

La cláusula *`throws`* se utiliza exclusivamente en la firma o cabecera de un método para indicar la lista de excepciones que este podría emitir durante su ejecución sin capturarlas internamente.

Funciona como un contrato de interfaz que advierte a los consumidores del método sobre los posibles riesgos, delegando la responsabilidad de la gestión del error al bloque de código que invoca dicha función.

En el caso de las excepciones verificadas (**Checked Exceptions**), el uso de `throws` es obligatorio por diseño del lenguaje si el desarrollador decide no implementar un bloque `try-catch` local.

### ✧ `throw`

Por el contrario, la instrucción `throw` es una **sentencia de acción** que se coloca dentro del cuerpo de un método para instanciar y disparar una excepción de forma inmediata.

Al ejecutarse un `throw`, el flujo normal del programa se interrumpe y la JVM comienza un proceso de búsqueda hacia atrás en la pila de llamadas para localizar un manejador compatible.

Esta palabra clave se emplea comúnmente para validar reglas de negocio o precondiciones, forzando una salida controlada cuando el estado del sistema no es el esperado.

<br>

### ⇒ Ejemplo

Escenario de una lógica de transferencia bancaria donde se coordinan ambas palabras claves

```java
public class SistemaBancario {

    // 'throws' declara que este método puede fallar por causas externas (Checked Exception)
    public void procesarTransferencia(double monto) throws Exception {
        
        double saldoDisponible = 100.0;

        if (monto > saldoDisponible) {
            // 'throw' dispara la excepción físicamente si no hay fondos
            throw new Exception("Fondos insuficientes: el monto excede el saldo.");
        }

        System.out.println("Transferencia procesada con éxito.");
    }

    public static void main(String[] args) {
        SistemaBancario banco = new SistemaBancario();
        
        try {
            // El programador que usa el método debe gestionar la excepción declarada
            banco.procesarTransferencia(250.0);
        } catch (Exception e) {
            System.err.println("Error en la operación: " + e.getMessage());
        }
    }
}

```

<br>

> [!NOTE]  
>Un error no gestionado sube por la jerarquía de llamadas hasta encontrar un responsable.