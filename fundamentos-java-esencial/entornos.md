
# 📌 Configuración del entorno

<br>

- [📌 Configuración del entorno](#-configuración-del-entorno)
  - [📂 Arquitectura del ecosistema Java](#-arquitectura-del-ecosistema-java)
  - [📂 Ciclo de Vida: compilación vs. ejecución](#-ciclo-de-vida-compilación-vs-ejecución)
    - [🔅 bytecode](#-bytecode)
  - [📂 ❌ Instalación y verificación del JDK](#--instalación-y-verificación-del-jdk)
  - [📂 ❌ Configuración del IDE \[IntelliJ IDEA\]](#--configuración-del-ide-intellij-idea)
    - [▫️ Atajos del teclado](#️-atajos-del-teclado)
  - [📂 Inspección de código: Debugging básico](#-inspección-de-código-debugging-básico)
    - [▫️ Comandos principales](#️-comandos-principales)
    - [▫️ Inspección de Memoria y Pila de Llamadas](#️-inspección-de-memoria-y-pila-de-llamadas)

<br>

## 📂 Arquitectura del ecosistema Java

Para entender Java, hay que diferenciar los tres componentes principales que permiten compilar, ejecutar y desarrollar aplicaciones.  

- ### JVM

  La **Java Virtual Machine** es el componente central y clave de la **portabilidad** de Java.

  Su propósito es ser un programa que **ejecuta el bytecode** generado por el compilador de Java. En lugar de compilar el código fuente directamente al lenguaje nativo de la máquina, el compilador Java (`javac`) lo traduce a este bytecode genérico.

  Su función principal es actuar como un **intérprete** y una capa de abstracción. Cuando un programa Java es ejecutado, la JVM toma las instrucciones del bytecode y las traduce al **lenguaje nativo** del sistema operativo en tiempo real. Esto significa que mientras el bytecode sea el mismo, el programa funcionará en cualquier plataforma que tenga una implementación de la JVM.  

- ### JRE (Java Runtime Environment)

  El **Entorno de Ejecución de Java** es la infraestructura mínima requerida para **correr o ejecutar** cualquier programa Java ya compilado. Está diseñado exclusivamente para la fase de consumo o uso de la aplicación por parte de un usuario final.

  El JRE se compone de dos partes esenciales. La primera es la **JVM**, y la segunda son las **Librerías de Clases Centrales** de Java (los archivos `.jar` y la API central), que contienen todo el código preescrito que su programa utiliza, como las clases para manipular texto, colecciones, y otros elementos básicos.

- ### JDK

  El **Java Development Kit** representa la **suite completa de software** ofrecida por Oracle y está diseñado específicamente para el **desarrollo** de software Java. El JDK proporciona todas las herramientas y utilidades que un ingeniero de sistemas o desarrollador necesita para escribir, compilar, depurar y ejecutar su propio código.

  El JDK es la colección de todo lo necesario para la plataforma Java. Incluye el **JRE** completo (JVM + librerías centrales) y añade herramientas de desarrollo cruciales. Entre estas herramientas clave se encuentra **`javac`**, el compilador de Java que transforma el código fuente (`.java`) en *bytecode* ejecutable (`.class`).  

  Además, el JDK contiene herramientas esenciales para la productividad, como herramientas de depuración y monitoreo, que son fundamentales durante la fase de desarrollo para identificar y corregir errores.

  <br>

## 📂 Ciclo de Vida: compilación vs. ejecución

Java utiliza un proceso de dos pasos: **compilación** y **ejecución**. Cuando se escribe código en Java, se hace en un archivo `.java`. En la compilación del código este archivo se convierte en un archivo `.class` que la JVM puede entender.

- ### Fase de Compilación (`javac`)

  La compilación es el proceso de convertir el código fuente escrito por el programador en un formato INTERMEDIO que la JVM pueda entender.

  El proceso comienza con el `javac` (compilador), que toma como entrada el archivo de texto con la extensión `.java`.  
  Su trabajo no es ejecutar el programa, sino traducir y verificar el código (tipo, sintaxis, referencias) y generar bytecode (`.class`). Si se detecta algún error de sintaxis o de lógica de tipos, el compilador se detiene y no produce ningún archivo de salida.

  Si la compilación es exitosa, `javac` traduce el código fuente a bytecode. El resultado de esta fase es uno o más archivos con la extensión `.class`. Este bytecode no está optimizado para ninguna máquina física específica, sino que está diseñado para la JVM.

- ### Fase de Ejecución (`java`)

  La ejecución comienza cuando el desarrollador o usuario final utiliza el lanzador java (parte del JRE) para invocar la JVM y pasarle el archivo `.class`.

  Aquí es donde ocurre la magia de la portabilidad. La JVM toma el archivo de bytecode y lo carga en la memoria. Como el bytecode sigue siendo un formato de alto nivel, la JVM debe traducirlo al lenguaje nativo del sistema operativo anfitrión. Esta traducción final ocurre en tiempo real (runtime).

  La JVM utiliza el Compilador Just-In-Time (JIT) para optimizar la ejecución. El JIT identifica las partes del código que se ejecutan con mayor frecuencia y las compila a código de máquina nativo de forma permanente. Esto mejora drásticamente el rendimiento, haciendo que Java sea rápido a pesar del paso intermedio del bytecode.

  <br>

  ### 🔅 bytecode

  El **bytecode** es una colección de instrucciones de bajo nivel diseñadas para una máquina virtual. No está pensado para ser legible por humanos, pero sí para que la JVM lo analice, verifique y ejecute.

  Gracias al bytecode, Java consigue portabilidad: compilas una vez y ejecutas en cualquier sistema con JVM.  

  <br>

  > [!IMPORTANT]  
  > La sintaxis es esencial porque el compilador necesita reglas claras para comprender el código.  
  > Sin sintaxis correcta, el compilador no puede traducir la intención a bytecode.

  <br>

## 📂 ❌ Instalación y verificación del JDK

... 

  <br>

## 📂 ❌ Configuración del IDE [IntelliJ IDEA]

### ▫️ Atajos del teclado

<br>

- MOVER una LINEA DE CODIGO

  > **Shift + Alt + ↑ ↓**  
  > Posicionarse sobre la linea que se quiera mover, presionar `Shift` + `Alt` y mover con las flechas del teclado la posicion deseada

<br>

- CAMBIAR nombre de Variable en TODO el archivo

  > **Shift + F6**  
  > Posicionarse sobre la variable a cambiar, presionar `Shift`+ `F6`y elegir el nombre que se desee. Al cambiar la varible lo hara en todo el documento donde esta se encuentre

<br>

—------ **PROBAR !!!!!!!!!!!!** --------------------------------------------------------------------

- Escribir *`sysout`* y presionar *`Crtl + Space`*

  ````java
  System.out.println();
  ````

<br>

| | | |
|---:|:---:|:---|
| *Ctrl + Shift + F* | - | Formatea el código (tabulaciones, saltos de líneas …) |  
| *Ctrl + Shift + C* | - | Comentar-Descomentar con // las líneas seleccionadas |
| *Alt + Shift + S* | - | Generar Getters and Setters AUTOMATICOS |
| *Ctrl + Alt + ↑* | - | Duplica la línea actual en la línea línea superior |
| *Ctrl + Alt + ↓* | - | Duplica la línea actual en la línea línea inferior |
| *Alt + ↑* | - | Intercambia la línea actual con la línea superior |
| *Alt + ↓* | - | Intercambia la línea actual con la línea inferior |
| *Ctrl + D* | - | Elimina la línea actual (en la que se encuentra el cursor) |
| *Ctrl + Z* | - | Deshacer edición |
| *Ctrl + Y* | - | Rehacer edición |
| *Ctrl + L* | - | Ir a la línea número («introducir número») |
| *Ctrl + M* | - | Maximizar-Minimizar el panel activo |
| *Ctrl + S* | - | Guarda cambios del fichero |
| *Ctrl + Shift + P* | - | Con el cursor en un comienzo o fin de llave o paréntesis, lleva al otro extremo |
| *Ctrl + Shift + L* | - | Muestra todos los atajos del teclado |
| *Ctrl + Shift + X* | - | Convierte las letras a mayúsculas (del texto seleccionado) |
| *Ctrl + Shift + Y* | - | Convierte las letras a minúsculas (del texto seleccionado) |
|  |  |  |

<br>

## 📂 Inspección de código: Debugging básico

El **debugger** o depurador es una herramienta integrada en el IDE que permite congelar la ejecución de la JVM y observar exactamente qué hay dentro de las variables en cada instante, sin modificar el código fuente. 

Este actúa como una "lupa de alta precisión". Permite **pausar la ejecución del programa en tiempo real** y examinar la memoria sin alterar el código fuente

<br>

> [!NOTE]  
> #### **breakpoint**  
> Es una marca que se coloca en una línea de código específica. Cuando la JVM ejecuta el programa en **Modo Debug**, la ejecución se detiene justo **antes** de procesar esa línea. Esto permite pausar la aplicación e inspeccionar el estado exacto de las variables en ese instante.

<br>

### ▫️ Comandos principales

Una vez que el programa se detiene en un *breakpoint*, se puede controlar el flujo de ejecución línea por línea utilizando cuatro comandos universales:

| Comando | Tecla habitual (IntelliJ) | Descripción | ¿Cuándo usarlo? |
|:-------:|:-------------------------:|-------------|-------------------|
| **Step Over** | `F8` | Ejecuta la línea actual y avanza a la siguiente línea del mismo método sin entrar en llamadas a otras funciones | Para avanzar secuencialmente observando cómo cambian las variables |
| **Step Into** | `F7` | Ingresa al interior del método que se está invocando en la línea actual | Cuando se sospecha que el error está dentro de una función propia |
| **Step Out** | `Shift+F8` | Ejecuta el resto del método actual y regresa al método llamador | Cuando se termino de revisar un método y se quiere volver arriba |
| **Resume** | `F9` | Reanuda la ejecución normal del programa hasta encontrar el siguiente *breakpoint* o finalizar | Para saltar iteraciones de bucles o avanzar a la siguiente sección crítica |

<br>

### ▫️ Inspección de Memoria y Pila de Llamadas

Cuando la ejecución está pausada, el IDE habilita dos paneles principales:

  1. **Panel de Variables (Scope)**: Muestra el nombre, tipo y valor actual de todas las variables en el ámbito local y de clase.

  2. **Pila de Llamadas (Call Stack)**: Muestra el historial ordenado de métodos que se fueron invocando hasta llegar a la línea actual. Esto te permite rastrear "el camino" exacto que siguió el programa.