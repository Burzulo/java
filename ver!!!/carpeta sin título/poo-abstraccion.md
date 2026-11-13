# 📌 Abstracción

<br>

- [Clases Abstractas](#-abstraccion)
- [Metodos Abstractos](#-metodos-abstractos)

<br>

## 📂 Abstraccion

La abstracción en POO es el proceso de **identificar y separar las características esenciales de un objeto** de la vida real para representarlas de forma abstracta o lógica en un programa.  
En Java, se logra mediante la creación de clases y la definición de sus atributos y métodos.

### ✧ Clases Abstractas

Es una clase que **NO PUEDE SER INSTANCIADA** directamente, es decir, no se pueden (o deben) crear objetos de esa clase específica.  
Se UTILIZA COMO una **clase base o plantilla** para otras clases relacionadas.

La principal característica de una clase abstracta es que puede tener métodos abstractos.  
Un método abstracto **es abstracto cuando está declarado pero sin su implementación**, es decir, no contiene entre sus «llaves» nada de código.  
En un MÉTODO ABSTRACTO, **sólo se declara su firma, incluyendo el nombre del método y los parámetros que acepta**, nada más que eso, convirtiéndola así en una **clase padre**.

Las clases que heredan de una clase abstracta, llamadas «subclases o clases hijas», deben proporcionar una implementación para todos los métodos abstractos heredados.  
Esto significa que **las subclases deben completar / implementar los métodos abstractos declarados en la clase abstracta**.

<br>

> [!IMPORTANT]  
> Cuando se usan clases abstractas, **una clase no puede heredar de varias clases abstractas a la vez** (como en las interfaces), **solo UNA**.

<br>

Una clase abstracta se utiliza como una abstracción general de la cual se derivan clases más específicas. Proporciona una estructura común y define los métodos abstractos que deben implementarse en las subclases. Esto promueve la reutilización del código y la creación de jerarquías de clases.

Generalmente las clases abstractas indican **«ES/SER»** de un objeto.

<br>

- ### Cuando se usan las Clases Abstractas ?

  Cuando se desea definir una abstracción que englobe objetos de distintos tipos y se quiere hacer uso del **polimorfismo**.

  Por ejemplo, un ``círculo`` y un ``cuadrado`` son figuras geométricas, en este caso ``Figura`` es una **clase abstracta** porque no tiene sentido calcular su área, pero sí la de sus hijos (``cuadrado`` y ``círculo``) …
  
  Cuando una clase declara al menos un método abstracto, se debe marcar como abstracta utilizando la palabra clave `abstract`.  
  Una clase abstracta puede tener tanto métodos abstractos como métodos concretos (implementados), pero **si o si debe implementar al menos un método abstracto para considerarse como clase abstracta como tal**.
  
  ````java
  modificadorAcceso abstract class nombreClase {
      ... 
      modificadorAcceso abstract tipoDato nombreMétodo();   // método abstracto
  }
  
  // ejemplo de CLASE ABSTRACTA
  public abstract class Figura {
     ... 
     public abstract double calculaArea();
  }
  ````
  
<br>

> [!IMPORTANT]  
> Sus niveles de visualización deben ser *public o protected* pero **NUNCA _private_**.

<br>

## 📂 Metodos Abstractos

En POO, un **método abstracto** es una declaración de intención pero sin su implementación.  
Es la herramienta principal para definir **qué** debe hacer una clase, pero dejando que las subclases decidan **cómo** hacerlo.

Un método abstracto **no tiene cuerpo** (sin llaves `{ }`).  
Solo contiene la **firma** (nombre, parámetros y tipo de retorno) y termina en punto y coma `;`.

<br>

> [!IMPORTANT]  
> Si una clase contiene al menos un método abstracto, la **clase también debe ser declarada como abstracta**.

<br>

- ### Características claves:
  
  * **Obligatoriedad:** Cualquier clase "hija" que herede de una clase abstracta **debe** implementar de todos los métodos abstractos del padre.
  * **Sin instancia:** No se puede crear un objeto de una clase que tenga métodos abstractos (estarían incompletos).
  * **Firma:** Define el "Contrato" que las subclases deben respetar.

<br>

- ### Implementación y Sintaxis

  Por ejemplo, todos los animales hacen un sonido pero un `Perro` no suena igual que un `Gato`.
  
    ```java
    // La clase DEBE ser abstracta para tener métodos abstractos
    public abstract class Animal {
        private String nombre;

        // Método con implementación
        public void dormir() {
            System.out.println("Zzz...");
        }

        // MÉTODO ABSTRACTO
        public abstract void hacerSonido();
    }


    // La clase hija se ve OBLIGADA a implementar el método
    public class Perro extends Animal {
        @Override
        public void hacerSonido() {
            System.out.println("¡Guau! ¡Guau!");
        }
    }
    ```

<br>

- ### ¿Cuándo se usan?

  Se utilizan en dos situaciones principales:

  - **Cuando la acción es común pero la forma es única:**  
    Como en el ejemplo anterior, todos los `Animales` hacen sonidos pero cada uno lo hace de manera diferente.
  
  - **Para forzar estándares:**  
    Si se trabaja en equipo, el arquitecto de software crea métodos abstractos para que los demás programadores no olviden implementar funciones críticas (como `validarUsuario()` o `procesarPago()`).

<br>

- ### Compilacion

  Si hay una clase abstracta `FiguraGeometrica` con un método abstracto `calcularArea()`, y luego se crea una clase hija `Circulo` pero NO se escribe el método `calcularArea()`... Al momento de compilar el código Java lanzara un error de compilación y no te dejara continuar.
  
  ```java
  // ❌ ERROR DE COMPILACIÓN
  public class Circulo extends FiguraGeometrica {
      private double radio;
  }
  
  
  // Solucion correcta
  public class Circulo extends FiguraGeometrica {
      private double radio;
  
      @Override
      public void calcularArea() {
          double area = Math.PI * Math.pow(radio, 2);
          System.out.println("El área es: " + area);
      }
  }
  ```

<br>

### ⇒ Diferencias rápidas entre métodos
  
| Característica | Método Concreto | Método Abstracto |
| --- | --- | --- |
| **Cuerpo `{ }`** | Sí tiene | No tiene, termina en `;` |
| **Palabra clave** | No requiere | Requiere `abstract` |
| **Implementación** | Ya está definida | Se delega a la subclase |
| **Uso** | Acciones compartidas | Acciones obligatorias pero variables |