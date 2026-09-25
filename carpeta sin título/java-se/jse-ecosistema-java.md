# 📌 Introducción al Ecosistema Java

<br>

- [Arquitectura](#-arquitectura-del-ecosistema-java)
- [Ciclo de vida: Compilación vs. Ejecución](#-ciclo-de-vida-compilación-vs-ejecución)
- [Estructura básica](#-estructura-básica-de-un-programa-java)

<br>

## 📂 Arquitectura del Ecosistema Java

Para entender Java, hay que diferenciar los tres componentes principales que permiten compilar, ejecutar y desarrollar aplicaciones.  

- ### JVM (Java Virtual Machine)

  La **Máquina Virtual de Java (JVM)** es el componente central y clave de la **portabilidad** de Java.

  Su propósito es ser un programa que **ejecuta el bytecode** generado por el compilador de Java. En lugar de compilar el código fuente directamente al lenguaje nativo de la máquina, el compilador Java (``javac``) lo traduce a este bytecode genérico.

  Su función principal es actuar como un **intérprete** y una capa de abstracción. Cuando un programa Java es ejecutado, la JVM toma las instrucciones del bytecode y las traduce al **lenguaje nativo** del sistema operativo en tiempo real. Esto significa que mientras el bytecode sea el mismo, el programa funcionará en cualquier plataforma que tenga una implementación de la JVM.  

- ### JRE (Java Runtime Environment)

  El **Entorno de Ejecución de Java (JRE)** es la infraestructura mínima requerida para **correr o ejecutar** cualquier programa Java ya compilado. Está diseñado exclusivamente para la fase de consumo o uso de la aplicación por parte de un usuario final.

  El JRE se compone de dos partes esenciales. La primera es la **Máquina Virtual de Java (JVM)**. La segunda son las **Librerías de Clases Centrales** de Java (los archivos `.jar` y la API central), que contienen todo el código preescrito que su programa utiliza, como las clases para manipular texto, colecciones, y otros elementos básicos.

- ### JDK (Java Development Kit)

  El **Kit de Desarrollo de Java (JDK)** representa la **suite completa de software** ofrecida por Oracle y está diseñado específicamente para el **desarrollo** de software Java. El JDK proporciona todas las herramientas y utilidades que un ingeniero de sistemas o desarrollador necesita para escribir, compilar, depurar y ejecutar su propio código.

  El JDK es la colección de todo lo necesario para la plataforma Java. Incluye el **Entorno de Ejecución de Java (JRE)** completo (JVM + librerías centrales) y añade herramientas de desarrollo cruciales. Entre estas herramientas clave se encuentra **`javac`**, el compilador de Java que transforma el código fuente (`.java`) en *bytecode* ejecutable (`.class`).  

  Además, el JDK contiene herramientas esenciales para la productividad, como herramientas de depuración y monitoreo, que son fundamentales durante la fase de desarrollo para identificar y corregir errores.

  <br>

## 📂 Ciclo de Vida: Compilación vs. Ejecución

Java utiliza un proceso de dos pasos: la **compilación** y la **ejecución**.  

Cuando se escribe código en Java, se hace en un archivo ``.java``. En la compilación del código este archivo ``.java`` se convierte en un archivo ``.class`` que la máquina virtual de Java puede entender.

<br>

- ### Fase de Compilación (``javac``)

  La compilación es el proceso de convertir el código fuente escrito por el programador en un formato INTERMEDIO que la JVM pueda entender.

  El proceso comienza con el ``javac`` (compilador), que toma como entrada el archivo de texto con la extensión ``.java``.  
  Su trabajo no es ejecutar el programa, sino traducir y verificar el código (tipo, sintaxis, referencias) y generar bytecode (``.class``). Si se detecta algún error de sintaxis o de lógica de tipos, el compilador se detiene y no produce ningún archivo de salida.

  Si la compilación es exitosa, ``javac`` traduce el código fuente a código de bytes (bytecode). El resultado de esta fase es uno o más archivos con la extensión ``.class``. Este bytecode no está optimizado para ninguna máquina física específica, sino que está diseñado para la JVM.

- ### Fase de Ejecución (``java``)

  La ejecución comienza cuando el desarrollador o usuario final utiliza el lanzador java (parte del JRE) para invocar la JVM y pasarle el archivo ``.class``.

  Aquí es donde ocurre la magia de la portabilidad. La JVM toma el archivo de bytecode y lo carga en la memoria. Como el bytecode sigue siendo un formato de alto nivel, la JVM debe traducirlo al lenguaje nativo del sistema operativo anfitrión. Esta traducción final ocurre en tiempo real (runtime).

  La JVM utiliza el Compilador Just-In-Time (JIT) para optimizar la ejecución. El JIT identifica las partes del código que se ejecutan con mayor frecuencia y las compila a código de máquina nativo de forma permanente. Esto mejora drásticamente el rendimiento, haciendo que Java sea rápido a pesar del paso intermedio del bytecode.

  <br>

  ### ⇒ bytecode

  El **bytecode** es una colección de instrucciones de bajo nivel diseñadas para una máquina virtual. No está pensado para ser legible por humanos, pero sí para que la JVM lo analice, verifique y ejecute.

  El bytecode es una representación intermedia: no es código máquina nativo de un CPU, sino instrucciones pensadas para la JVM. Gracias al bytecode, Java consigue portabilidad: compilas una vez y ejecutas en cualquier sistema con JVM.  

  > ⚠️ **IMPORTANTE**  
  > La sintaxis es esencial porque el compilador necesita reglas claras para comprender el código.  
  Sin sintaxis correcta, el compilador no puede traducir la intención a bytecode.

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