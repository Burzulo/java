# 📌 Interfaces

<br>

- [Interfaces](#-interfaces)
- [Metodos: `default`, `static` y `private`](#-evolucion-de-los-metodos)
- [Clases Abstractas vs Interfaces](#-clases-abstractas-vs-interfaces)

<br>

## 📂 Interfaces

Una interfaz es un tipo de referencia, similar a una clase, que puede contener solo CONSTANTES, firmas de métodos, métodos predeterminados, métodos estáticos y tipos anidados.  
Por lo tanto, su función principal es **«definir un conjunto de comportamientos que deben ser implementados por cualquier clase que firme ese contrato»**.

Las clases que implementan una interfaz deben ser las encargadas de proporcionar la implementación de todos los métodos declarados en la misma.

<br>

> [!NOTE]  
> "La interfaz define un ROL (lo que el objeto HACE), mientras que la clase define una IDENTIDAD (lo que el objeto ES)."

<br>

### ✧ ``implements``

Cuando una clase emplea la palabra reservada ``implements``, está «firmando» un compromiso legal ante el compilador: **"Yo prometo que voy a proporcionar una implementación para todos los métodos declarados en esta interfaz"**.

Si la clase no cumple su promesa (no implementa los métodos), el código simplemente no compilará, a menos que la clase sea declarada como ``abstract``.

- ### Sintaxis

    ```Java
    // 1. Declaración de la Interfaz
    public interface Volador {
        void volar(); // Implícitamente public abstract
    }

    // 2. Clase que IMPLEMENTA la Interfaz
    public class Pato implements Volador { 

        @Override
        public void volar() {
            // Lógica de implementación de Pato
        }
    }
    ```

    Si una clase debe cumplir varios «contratos», donde se deben implementar múltiples interfaces, estas se enumeran separadas por comas.

    ```Java
    public class Pato implements Volador, Nadador, Comunicador {
        // ... deben implementarse todos los métodos de las tres interfaces.
    }
    ```

    <br> 

    > [!NOTE]  
    > **¿Por qué es útil esto?**  
    Imagina que estás construyendo un sistema de pagos. Puedes tener una interfaz ``MetodoPago``. No importa si es ``TarjetaCredito`` o ``PayPal``; mientras ambas «firmen el contrato» de tener un método ``procesarPago()``, el resto del sistema puede tratarlas por igual. Esto se conoce como **desacoplamiento**.

<br>

## 📂 Evolucion de los Metodos

Históricamente, las interfaces solo podían tener métodos abstractos (sin cuerpo).  
Pero hoy esto cambió para dar más flexibilidad sin romper el código existente.

- ``default``  
  Permiten añadir nuevas funcionalidades a las interfaces existentes sin obligar a todas las clases que ya la implementaban a cambiar su código.  
  Tienen cuerpo y se heredan.  

- ``static``  
  Son métodos de utilidad que pertenecen a la interfaz, no a los objetos.  
  No se heredan y se invocan usando el nombre de la interfaz (ej. ``MiInterfaz.miMetodoEstatico()``).  

- ``private``  
  Se usan para evitar la duplicación de código dentro de la interfaz, permitiendo que varios métodos ``default`` compartan una lógica común sin exponerla al exterior.

### ⇒ Ejemplo Integrador

  Una interfaz que define el comportamiento de un vehículo, y cómo cada método cumple un rol distinto:

```Java
public interface Vehiculo {
    
    // 1. Método Abstracto (El contrato clásico)
    void acelerar();

    // 2. Método default (Funcionalidad compartida heredable)
    default void encender() {
        registrarLog("Iniciando sistema..."); // Uso del método privado
        System.out.println("Vehículo encendido.");
    }

    // 3. Método static (Utilidad global de la interfaz)
    static boolean esCombustibleValido(String tipo) {
        return tipo.equalsIgnoreCase("Gasolina") || tipo.equalsIgnoreCase("Electrico");
    }

    // 4. Método private (Encapsulamiento de lógica interna)
    private void registrarLog(String mensaje) {
        System.out.println("[LOG INTERNO]: " + mensaje);
    }
}
```

- #### Análisis del código

  - `acelerar()`: Obliga a cualquier clase (ej. `Auto`, `Moto`) a escribir su propia lógica. Si no lo hacen, el código **no compila**.  

  - `encender()`: Si se crea un `Auto`, ya tiene este método "gratis". No es necesario programarlo de nuevo, pero se puede *sobrescribirlo* en caso necesario.  

  - `esCombustibleValido()`: Se usa así: `Vehiculo.esCombustibleValido("Diesel")`. No se necesita crear un objeto para usarlo.  

  - `registrarLog()`: Solo existe dentro de la interfaz. Si se intenta llamarlo desde fuera (como desde la clase `Main`), Java dará un error. Sirve para que `encender()` no tenga tanto código repetido si tuvieras otros métodos `default`.

<br>

> [!TIP]  
> No hay que abusar de los métodos `default`. Si una interfaz empieza a tener demasiada lógica (mucho cuerpo de código), quizás debería ser una **Clase Abstracta**. La interfaz debe mantenerse lo más "limpia" posible.

<br>

## 📂 Clases abstractas vs Interfaces

<br>

### ▫️ Comparativa de Componentes y Propósito

La tabla se centra en la estructura interna y el objetivo principal de cada mecanismo.

| Característica | Clases Abstractas | Interfaces |
| :--- | :--- | :--- |
| Filosofía de Diseño | Define una identidad base: **"ES / SER"** | Define una capacidad: **"PUEDE HACER"** |
| Estado (Variables) | Puede tener **estado** (variables de instancia que cambian) | **No tiene estado**. Solo constantes (``public static final``) |
| Métodos Abstractos | Pueden ser ``public`` o ``protected`` | Son implícitamente ``public abstract`` |
| Métodos con Cuerpo | Sí, métodos concretos (lógica de negocio) | Sí: ``default`` (heredables), ``static`` y ``private`` |
| Modificadores de Acceso | Libertad total (``private``, ``protected``, ``public``) | Mayormente ``public``. Los ``private`` solo para uso interno |
| Instanciación | No se pueden instanciar (``new``) | No se pueden instanciar (``new``) |

<br>

### ▫️ Comparativa de Herencia y Uso

Esta tabla se enfoca en cómo se relacionan con otras clases o interfaces en la jerarquía.

| Característica | Clases Abstractas | Interfaces |
| :--- | :--- | :--- |
| Herencia de Clases | Solo pueden **extender una única clase** (herencia simple) | **No pueden extender clases** |
| Herencia Múltiple | **No permite** herencia múltiple de clases | **Sí permite** herencia múltiple entre interfaces |
| Implementación | Una clase solo extiende una clase abstracta | Una clase puede implementar múltiples interfaces |
| Palabra Clave | Se utiliza ``extends`` | Se utiliza ``implements`` (clases) o ``extends`` (entre interfaces) |
| Conflicto de Nombres | No existe (solo hay un padre) | Si hay colisión de métodos ``default``, la clase debe resolverlo |