# 📌 Clases & Objetos

<br>

- [Conceptos: Clase y Objeto](#-clases-y-objetos)
- [Miembros: Atributos y Métodos](#-miembros-atributos-y-métodos)
- [Constructores: por defecto, parametrizado y uso de `this`](#-constructores)

<br>

## 📂 Conceptos: Clase y Objeto

### ✧ Clases

Las clases son **plantillas** que permiten **construir objetos**.  
Es una de las principales formas de **«abstraer» objetos de la vida real**.

Todas las clases tienen las siguientes características o particularidades:

- Representan «entidades» del mundo real.
- Poseen atributos y métodos.
- Para poder hacer uso de ellas, se deben crear «instancias» u «objetos».

````java
modificadorAcceso class nombreClase {
    // ... atributos y métodos
}

// ejemplo 
private class Persona {
    // ... atributos y métodos
}
````

Al momento de crear una clase y ponerle un **«nombre»** hay que tener en cuenta que generalmente están asociadas a **SUSTANTIVOS** en **SINGULAR**.  
Todas las clases deben comenzar con letra **MAYÚSCULA** en cada una de sus palabras. Ej: ``Alumno``, ``AlumnoEgresado`` …

<br>

### ✧ Objetos

Los objetos son **instancias de clases** y se crean mediante la invocación de un **método** llamado **constructor**.  
Un OBJETO en programación es la representación lógica de un objeto en la vida real.

Para entenderlo profundamente, debemos desglosar sus tres pilares esenciales:

   1. **Los Tres Componentes de un Objeto**  

      Para que un objeto exista como tal debe cumplir con tres características:

        - ***Estado***  
        Representado por sus **atributos**.  
        Es el conjunto de valores que tiene el objeto en un momento dado (por ejemplo, un objeto ``Auto`` cuyo atributo ``velocidad`` es ``80 km/h``).

        - ***Comportamiento***  
        Representado por sus **métodos**.  
        Define qué puede hacer el objeto o qué servicios ofrece (el método ``acelerar()`` o ``frenar()``).

        - ***Identidad***  
        Es lo que diferencia a un objeto de otro, incluso si tienen el mismo estado.  
        Dos objetos ``Persona`` pueden tener el mismo nombre y edad, pero son instancias distintas en la memoria.

   2. **El Ciclo de Vida: Instanciación y Memoria**  

      El proceso de crear un objeto se llama ***instanciación***. En Java, esto ocurre principalmente mediante la palabra reservada ``new``.

      ````java
      // ejemplo
      Persona p1 = new Persona();
      ````

      Ocurren dos cosas críticas:

        - **Invocación del Constructor**: Se ejecuta un bloque de código especial para inicializar los atributos.
        - **Reserva de Memoria Heap**: El objeto se aloja en un área de la memoria llamada **Heap**, mientras que la variable ``p1`` es solo una **referencia** que nos permite manipular dicho objeto.

   3. **Abstracción y Modelado**  

      Modelar un objeto no significa copiar la realidad tal cual, sino abstraer solo lo necesario para el sistema.  
      Si modelamos una ``Persona`` para un sistema de nómina, nos interesa su ``sueldo``; si la modelamos para un hospital, nos interesa su ``tipoDeSangre``.  
      Un objeto es, por tanto, una simplificación útil de una entidad de la vida real.

<br>

## 📂 Miembros: ``Atributos`` y ``Métodos``

El término «Miembros» refiere a los componentes estructurales que definen qué es y qué puede hacer una clase en Java, según la Especificación del Lenguaje Java.  
En el contexto de la POO, los miembros son como los ***bloques de construcción de un objeto***.

<br>

### ✧ Atributos

Los atributos son **características que posee una clase**.  
Son variables contenidas y establecidas por los objetos y normalmente cuentan con un tipo de dato asociado.

Todos los **atributos** deben **comenzar con MINÚSCULA**, y si tienen más de una palabra comenzar con mayúscula. **No pueden haber espacios**. Ej: ``nombreMascota``, ``apellidoAlumno`` ...

```java
modificadorAcceso class Alumno {
    int id;
    String nombre;
    String apellido;
}
```

<br>

### ✧ Métodos

Un MÉTODO es una FUNCIÓN, el nombre diferente depende del contexto.  
Los métodos son **acciones contenidas en una clase** y ayudan a **definir el comportamiento de la misma**, diciendo cuáles son las acciones que ésta puede hacer.

Suelen estar representados como **verbos en infinitivo** (ar, er, ir) y puede tener opcionalmente valores de entrada (Parámetros) y valores de salida (Retorno).

```java
modificadorAcceso tipoDato_a_devolver nombreMétodo() {
    // ... acción a realizar según el método
}

//ejemplo
private String Rendir() {
    // ... acción a realizar según el método

}
```

<br>

Existen métodos que pueden ser:

- **PROCEDIMIENTOS** ⟹ no retornan un valor.
- **FUNCIONES** ⟹ retornan un valor de un tipo de dato en particular.

<br>

### ✔ Parámetros - valores de entrada

Los parámetros son **valores** que pueden ser **enviados** en un método.  
Los métodos toman los parámetros como valores de entrada, y así puede realizar las acciones necesarias a partir de los mismos.  
Todos los parámetros deben **tener un tipo de dato asociado** (como así también pueden haber parámetros vacíos).

Por ejemplo, en una clase ``auto`` tenemos los métodos ``encender()`` sin parámetros, ``acelerar(int)`` recibe como parámetro la cantidad de «km» a acelerar y ``frenar(int)`` recibe como parámetro la cantidad de «km» que debe bajar de velocidad.

### ✔ Retorno - valores de salida

La **salida** de un método es un **valor** en particular que el mismo **retorna luego de haber realizado una serie de acciones o procesos**.  
Los valores de entrada son datos, y los valores de salida son considerados generalmente como información.  
Todos los valores de salida deben tener un tipo de dato asociado.

En los métodos, es posible retornar un único valor de salida y ésta acción se lleva a cabo mediante la palabra reservada ``return``.

<br>

> [!NOTE]  
> Un *atributo* es un **estado** interno del objeto.  
> Un *método* es un **comportamiento** del objeto. 

<br>

## 📂 Constructores

Técnicamente, un constructor es un bloque de código encargado de inicializar la memoria reservada para un nuevo objeto.  
Aunque se asemeja a un método, carece de un tipo de retorno (ni siquiera `void`) porque su función no es devolver un valor, sino configurar la instancia.

Un constructor se llama automáticamente cuando se **crea un objeto de una clase**. Estos se utilizan para inicializar los atributos del objeto cuando se crea.  
 En Java, si un desarrollador no define ningún constructor, el compilador inserta automáticamente un **Constructor por Defecto** (invisible, sin parámetros y vacío).

Cada clase puede tener uno o más constructores y **cada constructor se llama SIEMPRE igual a la clase**

<br>

> [!IMPORTANT]  
> Los constructores NO retornan ningún valor (ni siquiera ``void``).

<br>

### ✧ Tipos de Constructores y Sobrecarga

En el diseño de software profesional, se suele utilizar la **Sobrecarga de Constructores** para ofrecer flexibilidad al instanciar clases.

- El **Constructor Parametrizado** es aquel que recibe datos externos para asignar valores a los atributos inmediatamente, permitiendo que el objeto sea funcional desde su primer microsegundo de existencia.  

- El **Constructor Sin Argumentos** (vacío) se utiliza a menudo para inicializar atributos con valores por defecto predefinidos o cuando se trabaja con frameworks como Hibernate o Spring, que requieren esta estructura para instanciar objetos mediante reflexión.  
Esta variedad permite que una misma clase responda a diferentes necesidades de negocio, ya sea creando un "``Usuario``" con datos mínimos o uno con el perfil completo.

  <br>

  > [!NOTE]  
  > ***Reflexión*** se refiere a la capacidad de un programa para inspeccionar, analizar y modificar su propia estructura y comportamiento en tiempo de ejecución

<br>

### ✧ `this`

La palabra clave `this` en Java representa una **referencia al objeto actual dentro de una clase**.  
Su uso principal en los constructores es la **desambiguación**: cuando un parámetro del constructor tiene el mismo nombre que un atributo de la clase `this` le indica al compilador que nos referimos a la variable de instancia y no a la variable local. Sin el uso de `this`, el compilador priorizaría el parámetro, dejando el atributo de la clase sin cambios.

````java
public class Vehiculo {
   String marca;

   public Vehiculo(String marca) {
       this.marca = marca; // 'this' se refiere al atributo de la clase
   }

   public void mostrar() {
       System.out.println("La marca del vehiculo es " + this.marca);
   }
}
````

<br>

### ✧ Uso Avanzado: Constructor Chaining

Más allá de la asignación de variables, `this` permite el **encadenamiento de constructores** mediante la sintaxis `this()`.  
Esta técnica permite que un constructor invoque a otro dentro de la misma clase, evitando la duplicación de lógica de inicialización.

Por ejemplo, un constructor vacío podría llamar a un constructor parametrizado con valores por defecto utilizando `this("Desconocido", 0)`.  
Es imperativo recordar que, cuando se usa de esta forma, la llamada a `this()` debe ser obligatoriamente la **primera línea de código** dentro del constructor, asegurando así una jerarquía de inicialización ordenada y segura.

<br>

### ▫️ EJEMPLO de Implementación

```java
public class Vehiculo {
    private String marca;
    private int modelo;

    // Constructor Parametrizado
    public Vehiculo(String marca, int modelo) {
        this.marca = marca; // Desambiguación
        this.modelo = modelo;
    }

    // Constructor Sin Argumentos que encadena (Chaining) al anterior
    public Vehiculo() {
        this("Genérico", 2024); // Invoca al constructor de arriba
    }
}
```