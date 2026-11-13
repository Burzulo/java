# 📌 Introducción al Ecosistema Java

<br>

- [📌 Introducción al Ecosistema Java](#-introducción-al-ecosistema-java)
  - [📂 Estructura Básica de un Programa Java](#-estructura-básica-de-un-programa-java)
    - [⇒ Análisis de la Firma](#-análisis-de-la-firma)

<br>

## 📂 Estructura Básica de un Programa Java

Para que cualquier código Java sea funcional, debe estar organizado dentro de una estructura jerárquica que define el punto de inicio del programa y el alcance de sus instrucciones.
  
- ### Definición de la Clase (`class`)
  
  El primer y más fundamental requisito en Java es que todo el código ejecutable debe residir dentro de una clase. La clase actúa como el contenedor lógico del programa, encapsulando tanto los datos (atributos) como el comportamiento (métodos).

  ````java
  public class NombreDeLaClase {
      // Todo el código va aquí dentro
  }
  ````

- ### El Bloque Principal (`main`)

  El método `main` es el **punto de entrada** oficial del programa. Una vez que la estructura de la clase está definida, necesitamos un punto de inicio para la ejecución. Este rol lo cumple el método ``main``, el cual es buscado y llamado directamente por la JVM cuando se lanza el programa.

  La firma de este método es estricta y mandatoria para que la JVM pueda reconocerlo y utilizarlo:

  ```java
  public static void main(String[] args) {
      // Las instrucciones del programa comienzan aquí
  }
  ```

  > 💡 **NOTA**  
  > Dentro de ``main`` se coloca el código que se ejecuta al arrancar la aplicación: crear objetos, llamar métodos, inicializar recursos o simplemente ejecutar instrucciones simples para empezar.

  ### ⇒ Análisis de la Firma

  - ``public`` indica visibilidad. Significa que la JVM (u otros componentes externos) pueden ver y llamar a este método..  

  - ``static`` significa que el método pertenece a la clase, no a una instancia. La JVM no necesita crear un objeto de la clase para llamar a ``main``; lo invoca directamente sobre la clase.

  - ``void`` es el tipo de retorno del método. Indica que main **no devuelve ningún valor** a quien lo llama.

  - ``main`` es simplemente el nombre del método. Es la convención que la JVM reconoce como arranque.

  - ``String[] args`` es la lista de parámetros que recibe ``main``. Es un arreglo (lista) de cadenas de texto. Permite recibir argumentos desde la línea de comandos cuando se ejecuta la aplicación.

- ### Bloques de Código y Llaves (`{}`)
  
  En Java, las llaves (``{}``) son fundamentales, ya que definen los **bloques de código** y establecen el **alcance** (scope) de las variables y las instrucciones.  

  Todo cuerpo de clase, método, o estructura de control de flujo (como ``if``, ``for``, ``while``) debe estar delimitado por estas llaves. Las instrucciones dentro de un bloque se ejecutan secuencialmente, y las variables declaradas dentro de ese bloque solo existen hasta que el programa sale de él. Esto ayuda a mantener el código organizado y evita conflictos de nombres.