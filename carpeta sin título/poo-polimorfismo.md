# 📌 Polimorfismo


<br>

- [Casting (Conversión)](#-casting-conversión)
- [``instanceof``](#-operador-instanceof)

<br>

El polimorfismo refiere a la capacidad de un objeto de tomar MUCHAS DIFERENTES FORMAS, significa que **un objeto puede ser tratado como si fuera de varios tipos**.  
En Java, **se logra a través de la herencia y los métodos de sobreescritura**.  

Por ejemplo si hay una clase base llamada `Animal` y clases derivadas como `Perro` y `Gato`. Tanto los perros como los gatos son animales, por lo que pueden heredar de la clase base `Animal`.  
El polimorfismo permite tratar un perro o un gato como un animal genérico.

También permite que dentro del mismo código **dos métodos tengan el mismo nombre** pero ejecutan FUNCIONES DIFERENTES ya que cada una va a recibir diferentes parámetros.

<br>

| Polimorfismo | Herencia |
|:------------:|:------------:|
| La clase anidada (hija) recibe atributos y métodos que la clase padre pero cuenta con **su propia implementación para cada método**. | La clase hija hereda los mismos atributos y métodos de la clase en la que está anidada (padre) **sin modificar** su funcionalidad. |

<br>

- #### Ejemplo

  ```java
  // Clase PADRE
  Animal     
     
  // Clases HIJAS o DERIVADAS
  Gato, Perro, Gallo;   
  
  // DECLARACIÓN de la función
  function hacerSonido(Animal) {
    ...  
  }
  
  // INVOCAR la función
  hacerSonido(Gato);
  hacerSonido(Perro);
  hacerSonido(Gallo);
  ```

<br>

## 📂 Casting (Conversión)

### ✧ ``Upcasting``

El ``Upcasting`` es el proceso de convertir una referencia de una subclase (clase hija) a una referencia de una superclase (clase padre).  
Para que el Upcasting exista, debe haber **herencia**. Y en Java, esto es automático y seguro:

```java
// Upcasting automático (seguro)
Perro perro = new Perro("Rex");
Animal animal = perro;  // Perro ES-UN Animal
 
// Equivalente:
Animal animal = new Perro("Rex");
```

**⇒** ¿Por qué es seguro? Porque un ``Perro`` es siempre un ``Animal``. La relación **"ES-UN"** lo garantiza.  
Cuando se hace Upcasting se está **limitando la visibilidad** del objeto, por lo tanto solo se puede acceder a los métodos que existan en la clase ``Animal``.

- #### Ejemplo

  ¿Para qué sirve en la vida real? Imaginemos que tenemos un método que debe alimentar animales. Sin Upcasting, habria que hacer:
  
  ```java
  public void alimentarLeon(Leon l) { ... }
  public void alimentarPerro(Perro p) { ... }
  ```
  
  En cambio con **Upcasting**, gracias a que todos pueden ser tratados como su padre, solo se hace:
  
  ```Java
  public void alimentarAnimal(Animal a) {
      a.comer(); // No importa si entra un León o un Perro, Java sabe qué comer() usar.
  }
  ```

<br>

### ✧ ``Downcasting``

A la inversa, cuando es necesario convertir una referencia de superclase a subclase, se realiza el ``downcasting``.

Este es peligroso si no es seguro, si se intenta un casting sin la Identificación previa (`instanceof`), y los tipos no son compatibles, el programa arrojará la temida excepción `ClassCastException` en tiempo de ejecución.

```java
Animal a = new Perro("Rex");

// Downcasting seguro (verificamos primero)
if (a instanceof Perro) {
    Perro p = (Perro) a;
    p.ladrar(); // ✓ Seguro
}

// ❌ Downcasting peligroso
Animal a2 = new Gato("Misa");
Perro p = (Perro) a2; // ClassCastException en runtime
p.ladrar();
```

<br>

> [!NOTE]  
> Siempre verificar con ``instanceof`` antes de hacer ``downcasting``.

<br>

## 📂 Operador `instanceof`

### ✧ ``instanceof``
 
`instanceof` es un operador que sirve para **verificar en TIEMPO REAL** si un **objeto** es una instancia de una clase particular, una subclase de esa clase, o si implementa una interfaz específica y poder tomar desiciones antes de hacer un casting y controlar el flujo en estructuras condicionales usando el tipo dinámico del objeto.

> Es como un **"seguro de vida"** antes de hacer un ``downcasting``.

```java
Animal a = new Perro("Rex");

if (a instanceof Perro) {
    System.out.println("Es un Perro");
    Perro p = (Perro) a;  // Casting seguro
    p.ladrar();
} else if (a instanceof Gato) {
    System.out.println("Es un Gato");
    Gato g = (Gato) a;
    g.maullar();
}
```

**⇒** ¿Cuándo usar ``instanceof``? Solo cuando se necesite un comportamiento específico de una subclase.  
Si todas las subclases implementan el método de forma diferente, no es necesario.

<br>

> [!NOTE]  
> Si se escriben muchos ``instanceof``, probablemente se este perdiendo el polimorfismo, por lo tanto es recomedable reevaluar el diseño.