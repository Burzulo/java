# 📌 Variables y Memoria

<br>

- [Variables y Tipos Primitivos](#-variables-y-tipos-primitivos)
- [Casting: Conversiones de Datos](#-casting-conversiones-de-datos)
- [Wrappers](#-wrappers)

<br>

## 📂 Variables y Tipos Primitivos

### ✧ Variables

Una variable es donde se **almacenan y se recuperan los datos** de un programa. En programación, se utilizan para guardar datos y estados, asignar ciertos valores de variables a otras, representar valores de expresiones matemáticas y mostrar valores por pantallas.

Las variables se expresan:

- Como un **número**
- Como un **texto**
- Como un **dato abstracto**
- Como un **objeto**

  ### ⇒ Declaración

  La declaración de las variables cuenta con dos partes fundamentales: el *tipo de dato*, *nombre* de la variable y *punto y coma* al finalizar. Una vez declaradas, a las variables se le pueden asignar diferentes valores teniendo en cuenta el tipo de dato.

  ````java
  // sintaxis
  tipoDato nombre;

  // ejemplo
  int numero = 56;
  ````

<br>

### ✧ Tipos De Datos

En Java, los **tipos de datos primitivos** son los más básicos y eficientes para almacenar información simple. **No son objetos**, y se almacenan directamente en memoria, lo que los hace más rápidos que los objetos. Los tipos de datos definen qué puede ser almacenado dentro de una variable.

Algunos de los tipos de datos más usados son:

- **Entero** ⇒ `int`  
Para representar valores enteros. Es adecuado para la mayoría de las operaciones numéricas. Ej: 0. 51, 654, etc.

- **Entero largo** ⇒ `long`  
Para representar valores enteros con signo. Debido a su mayor rango, es útil para manejar valores más grandes, como marcas de tiempo en milisegundos, valores monetarios más precisos o identificadores únicos extensos.

- **Decimales** ⇒ `float`  
Para representar valores en cálculos científicos y de ingeniería, donde la precisión no necesita ser extremadamente alta.

- **Decimales** ⇒ `double`  
Similar al float, pero es más preciso. Se utiliza en cálculos que requieren mayor precisión. Ej: 1.5, 3.14.

- **Booleanos** ⇒ `boolean`  
Para representar valores de verdad (verdadero o falso). Se utiliza para tomar decisiones en el código basadas en condiciones lógicas. Ej: true o false.

- **Caracteres** ⇒ `char`  
Para representar un único carácter. Puede contener letras, números, símbolos o caracteres especiales. Ej: ’a’, ’b’, ’r’, ’p’, etc.

- **Cadena de caracteres / texto** ⇒ `String`  
Ej: “Hola mundo”, “probando 1, 2, 3”.

<br>

> ⚠️ **IMPORTANTE**  
> ¿Por qué el tipo va antes? Porque Java necesita saber cuánta memoria reservar y qué operaciones son válidas sobre esa variable. Esto ayuda a evitar errores y a que el compilador detecte problemas antes de ejecutar el programa.

<br>

## 📂 Casting: Conversiones de Datos

El **Casting** es un mecanismo que permite convertir un tipo de dato primitivo en otro. Es fundamental para gestionar cómo se almacena y procesa la información cuando se trabaja con diferentes precisiones numéricas.

Este proceso de transformar una variable de un tipo de dato a otro, cambia la forma en que el programa interpreta ese valor en memoria.

- ### Casting Implícito (Widening)

  Se produce de forma AUTOMÁTICA cuando se mueve un valor de un tipo con menor capacidad a uno con mayor capacidad.  
  **No hay pérdida de datos**.

  ````java
  int edad = 25;
  double edadPrecisa = edad; // El int "cabe" perfectamente en el double
  // Resultado: 25.0
  ````

  > **Ruta de seguridad**: byte → short → int → long → float → double.

- ### Casting Explícito (Narrowing)

  Se debe realizar MANUALMENTE cuando se mueve un valor de un tipo con mayor capacidad a uno con menor capacidad.  
  **Existe riesgo de pérdida de precisión o información**.

  ````java
  double precioOriginal = 19.99;

  // Casting Explícito: Forzamos la conversión a entero
  int precioRedondeado = (int) precioOriginal; 
  
  System.out.println("Precio original: " + precioOriginal); // 19.99
  System.out.println("Precio en int: " + precioRedondeado);   // 19
  ````

  <br>

## 📂 Wrappers

Los `Wrappers` (envoltorios) son "clases especiales" que permite a los tipos primitivos (`int, double, boolean`, etc.) para que puedan comportarse como objetos.

En Java, los tipos primitivos son rápidos y eficientes, pero tienen una limitación: no son objetos. Esto significa que no tienen métodos y no pueden usarse en ciertas estructuras avanzadas de Java.

Esta distinción es crucial porque muchas herramientas avanzadas de Java, especialmente el marco de colecciones (Collections Framework), **requieren objetos para funcionar**, impidiendo el uso directo de datos puros.

Entender la diferencia técnica entre los primitivos y los Wrappers es fundamental para dominar Java.  
Cada primitivo tiene su "pareja" Wrapper.

| Tipo Primitivo | Clase Wrapper  |
| :------------: | :------------: |
| `int`          | `Integer`      |
| `double`       | `Double`       |
| `char`         | `Character`    |
| `boolean`      | `Boolean`      |
| `byte`         | `Byte`         |

<br>

La razón técnica número uno por la que se usan los Wrappers es que las estructuras de datos modernas de Java (como el `ArrayList`) solo aceptan objetos. No pueden guardar primitivos directamente.

````java
// Si se intenta hacer esto:
ArrayList<int> lista = new ArrayList<>();  // Error de compilación

// Se debe usar el Wrapper:
ArrayList<Integer> lista = new ArrayList<>();  // Correcto
````

Java introdujo el **Autoboxing** para no tener que convertir manualmente cada número. El compilador hace el trabajo sucio:

````java
ArrayList<Integer> numeros = new ArrayList<>();
numeros.add(5); // El compilador transforma el int 5 en un objeto Integer automáticamente.
````

<br>

### ⇒ Diferencias Técnicas Clave

| | Primitivos | Wrappers |
| :------------ | :------------ | :------------ |
| **Naturaleza** | Son valores básicos | Son Objetos (Clases) |
| **Almacenamiento** | Memoria **Stack** (Rápida y ligera) | Memoria **Heap** (Más lenta) |
| **Valor por defecto** | Siempre tiene uno (ej. `0`, `false`) | Pueden ser `null` |
| **Funcionalidad** | Solo guardan el valor | Tienen métodos (ej. `parseInt()`) |
| **Uso en Colecciones** | No permitido ❌ | Requerido (ej. `List<Intenger>`) |

<br>

> [!IMPORTANT]  
> El uso de Wrappers introduce la capacidad de manejar valores nulos (``null``), algo imposible con los primitivos. Esta característica es fundamental en aplicaciones reales, como cuando trabajamos con bases de datos donde un campo numérico puede estar ausente. Sin embargo, como desarrolladores se debe ser consciente de que el uso excesivo de Wrappers conlleva una ligera carga adicional en el consumo de memoria y procesamiento, por lo que la regla general es priorizar los primitivos para cálculos intensivos y reservar los Wrappers para estructuras de datos y lógica de objetos.