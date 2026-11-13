# 📌 Herencia

<br>

- [Herencia](#-herencia)
- [``super``](#-herencia-super)
- [Sobreescritura & Sobrecarga](#-sobrecarga--sobreescritura-de-métodos)
- [Buenas practicas en Herencia](#-sobrecarga--sobreescritura-de-métodos)

<br>

## 📂 Herencia

La herencia es un mecanismo que permite definir **nuevas clases basadas en una clase existente**, es una **relación entre clases**.  
Esta permite definir una jerarquía de las mismas.

<br>

### ✧ Superclase y Subclase

La herencia permite que una clase **herede propiedades y métodos de una clase padre/madre**. Esta **permite reutilizar clases**.  
Generalmente al utilizar herencia se crea una nueva clase que «hereda» o «extiende» métodos y atributos de una clase ya existente sin tener que reescribir el código asociado a esta última.

Esta NUEVA CLASE es denominada generalmente como ``subclase`` **(clase hija) puede poseer atributos y métodos que no existen en la clase original**.  
Por otro lado, la clase original es conocida como ``superclase`` **(clase padre/madre)**.  

Al igual que la «herencia genética» en la vida real, donde los hijos heredan ciertas características y comportamientos de los padres, en la «herencia de programación» se cumple exactamente el mismo concepto.

```java
modificadorAcceso class nombreSubClase extends nombreSuperClase {
    // ... codigo de la subclase
}
    
// ejemplo
public class Empleado extends Persona {
    ...
}
```

<br>

> [!NOTE]  
> La herencia **permite reutilizar código**, ya que deja **compartir** automáticamente **«métodos»** y datos entre clase, subclases y objetos.

<br>

### ✧ `extends`

La herencia a través de la palabra clave reservada ``extends`` sigue una regla de **herencia simple**, lo que significa que una clase hija solo puede tener un único padre directo.  
Esta estructura crea una relación lógica de tipo **«ES-UN»**.

Además de heredar, la subclase tiene la potestad de realizar una sobreescritura de métodos, lo que le permite modificar la implementación de una función del padre para adaptarla a sus necesidades específicas, manteniendo siempre la compatibilidad con el tipo original.

<br>

## 📂 Herencia: ``super``

### ✧ ``super``

Palabra clave reservada que permite acceder a métodos y atributos de la clase padre desde la subclase.  
Solo tiene sentido cuando **HAY HERENCIA**.

En tiempo de ejecución, el objeto es el mismo, pero ``super`` cambia el punto de vista para que actúe sobre el comportamiento heredado, incluso si está sobrescrito.

````java
public class Animal {
    public void hacer_sonido() {
        System.out.println("Sonido genérico");
    }
}

public class Perro extends Animal {
    @Override
    public void hacer_sonido() {
        System.out.println("Primero:");
        super.hacer_sonido();  // Llamar al método del padre
        System.out.println("Luego: ¡Guau!");
    }
}

// Uso:
Perro p = new Perro();
p.hacer_sonido();
````

<br>

## 📂 Sobrecarga & Sobreescritura de métodos

### ✧ Sobreescritura (Override)  

Ocurre cuando una **subclase define un método con el MISMO nombre, parámetros y tipo de retorno que un método de su clase padre**. 

La clase hija **usa el método de la clase padre a su manera**.

````java
public class Animal {
    protected String nombre;
    
    public Animal(String nombre) {
        this.nombre = nombre;
    }
    
    public void hacer_sonido() {
        System.out.println(nombre + " hace un sonido genérico");
    }
}


// clases hijas

public class Perro extends Animal {
    public Perro(String nombre) {
        super(nombre);
    }
    
    // SOBRESCRIBIR el método hacer_sonido()
    @Override
    public void hacer_sonido() {
        System.out.println(nombre + " ladra: ¡Guau!");
    }
}


public class Gato extends Animal {
    public Gato(String nombre) {
        super(nombre);
    }
    
    // SOBRESCRIBIR el método hacer_sonido()
    @Override
    public void hacer_sonido() {
        System.out.println(nombre + " maúlla: ¡Miau!");
    }
}
````

Ahora:

````java
Animal a1 = new Perro("Rex");
Animal a2 = new Gato("Misa");

a1.hacer_sonido(); // Rex ladra: ¡Guau!
a2.hacer_sonido(); // Misa maúlla: ¡Miau!
````

<br>

- ### ``@override``
  
  La anotación ``@Override`` es opcional pero recomendada.  
  Le dice al compilador que estás sobrescribiendo un método.  
  Si se comete un error (por ejemplo, mal nombre), el compilador te lo advierte.  
  Por eso se debe usar ``@Override`` **SIEMPRE** que se sobrescriba un método. Evita errores sutiles.
  
  <br>
  
  La anotación ``@Override`` cumple dos funciones principales que garantizan la solidez del código:

  1. **Detección de Errores en Tiempo de Compilación**  
    El propósito principal es la **validación de la firma**. Cuando se coloca ``@override`` encima de un método, se le está indicando al compilador: ***"Este método debe sobreescribir un método existente en la superclase o en una interfaz implementada."***
    
      - **Seguridad**: Si, por error, se cambia el nombre del método, o sus parámetros (la firma del método), el compilador detectará inmediatamente que no se está sobreescribiendo nada y generará un error de compilación.
      - **Prevención de Bugs**: Esto evita errores sutiles. Sin ``@override``, un método con una firma ligeramente incorrecta se interpretaría como un método nuevo (sobrecarga), no como una sobreescritura, y el código se ejecutaría, pero llamando al método equivocado en la superclase.  
  
  2. **Claridad y Legibilidad**.  
    Sirve como una documentación visual para cualquier desarrollador que lea el código, indicando claramente la intención de que ese método altera un comportamiento heredado.

<br>

### ✧ Sobrecarga (Overload)  

Ocurre cuando una clase tiene **varios métodos con el mismo nombre**, pero con **diferentes parámetros e implementaciones**.  
En la sobrecarga los métodos tienen diferentes tipos o cantidad de parámetros. El sistema sabe cual es el correcto por los parámetros que se le pasan.

````java
class Calculadora {

   public int sumar(int a, int b) {
       return a + b;
   }

   public double sumar(double a, double b) {
       return a + b;
   }

   public int sumar(int a, int b, int c) {
       return a + b + c;
   }
}
````

<br>

## 📂 Buenas practicas en herencia

1. Usa herencia para relaciones **ES-UN**, no para compartir código.
2. La clase padre debe ser **más general** que la hija.
3. Evita cadenas de herencia muy profundas (más de 3 niveles es sospechoso).
4. Sobrescribe métodos **deliberadamente**, no por accidente.
5. Usa protected para atributos que las subclases necesitan.
6. Documenta qué métodos están diseñados para ser sobrescritos.
7. Prefiere **composición** sobre herencia cuando sea posible.