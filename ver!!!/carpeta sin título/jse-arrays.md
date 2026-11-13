# 📌 Estructuras de Datos Estáticas: Arrays

<br>

- [Arreglos Unidimensionales](#-arreglos-unidimensionales)
- [Arreglos Multidimensionales](#-arreglos-multidimensionales)
- [Propiedad ``length``](#-propiedad-length)
- [Recorrido: ``for`` tradicional vs ``for-each``](#-recorrido)
- [Utilidades del Sistema: Clase `java.util.Arrays`](#-clase-javautilarrays)
  - [Método `sort()`](#-metodo-sort)
  - [Método `fill()`](#-metodo-fill)
  - [Método `equals()`](#-metodo-equals)
  - [Método `toString()`](#-metodo-tostring)

<br>

Los arrays son una **estructura que guarda múltiples valores del mismo tipo en una sola variable**, organizados en posiciones numeradas. Es como una lista de casillas numeradas donde cada casilla puede almacenar un dato. Funciona igual que una lista de compras.

Estas son **ESTRUCTURAS FIJAS** que se declaran y que mantienen su tamaño durante toda la ejecución del programa. Si se declara un arreglo de 5 posiciones, mantendrá esas 5 posiciones siempre.

Por ejemplo en lugar de tener 5 variables separadas (``producto1, producto2, producto3``...), tienes UN array llamado '``listaCompra``' que contiene los 5 productos.

<br>

## 📂 Arreglos Unidimensionales

Antiguamente llamados «vectores», son arreglos unidimensionales que poseen únicamente filas o columnas.

- ### Declaración y Asignación

  En Java se declaran especificando el **tipo de dato** que almacenará, el **nombre** y la **identificación []** la cual determina que se trata de un vector. Al mismo tiempo, para **inicializar** las posiciones de un vector, es necesario asignar al vector declarado la **palabra** ``new`` más el **tipo de dato** y **nuevamente []**, donde esta vez se especifica la **longitud** que tendrá el arreglo.

  ````java
  tipoDato nombreVector[] = new tipoDato[tamañoVector]

  // ejemplo
  int vector[] = new int[5]
  ````

  Una vez declarado e inicializado un vector, es posible **asignarle diferentes valores** en cada una de sus posiciones a partir de dar a conocer el índice donde estos datos deberán ir. A nivel código, si suponemos un vector de 5 posiciones, esta asignación de valores se puede realizar, por ejemplo, mediante las siguientes líneas de código:

  ````java
  nombreVector[posición] = valorAsignado
  
  // asignación manual
  vector [0] = 15;
  vector [1] = 23;
  vector [2] = 32;
  vector [3] = 99;
  vector [4] = 35;
  ````

  Un detalle muy importante a tener en cuenta es que, por convención mundial, los vectores **comienzan su índice en el valor 0**. ¿Qué quiere decir esto? Que si tenemos un vector de 5 posiciones, sus índices irán del 0 al 4, por lo que si hacemos referencia al índice 5, no estaríamos posicionados en la 5ta posición, sino en la sexta; esto, al tratarse de un vector de únicamente 5 posiciones provocaría un **error por desbordamiento**.

- ### Carga

  Suponiendo que el vector se encuentra vacío y lo que se desea realizar es permitirle al usuario la posibilidad de cargar los vectores por teclado. Para ello, será necesario utilizar una clase especial llamada ``Scanner``.

  Esta clase permite el ingreso de información o datos mediante algún periférico de entrada. Para hacer uso de él y poder cargar el vector, es necesario recorrerlo e ir **“Scanneando”** los valores para cada posición.

  ````java
  // se crea el Scanner
  Scanner teclado = new Scanner (System.in);  
  
  // recorremos el array
  for (int i=0; i<vector.lenght; i++) {
  
    System.out.println("Ingrese el número para la posicion " + i);  // se solicita al usuario el ingreso del valor a almacenar
    int tecla = teclado.nextInt();  // se lee por teclado el valor
    vector[i] = tecla;  // se asigna al vector el valor leido 
  }
  ````

- ### Recorrido

  Un vector que ya se con valores asignados, puede ser recorrido. Este se lleva a cabo, tanto para mostrar los valores que contiene el vector como para utilizarlos en caso de que sean necesarios. Para realizar este recorrido la mejor opción es utilizar la estructura repetitiva ``for``.

  Los vectores se recorren **SIEMPRE de manera secuencial**, es decir, posición a posición según un determinado orden que se establezca, por ejemplo:

  ````java
  for (int i=0; i<vector.lenght; i++) {
    System.out.println("Estoy en la posicion " + i);  // muestra por pantalla la posicion 
    System.out.println("Contiene el número " + vector[i]);  // muestra por pantalla el valor que contiene
  }
  ````

  El ciclo ``for`` siempre tendrá **tres parámetros**:

  - El primero corresponde a la **inicialización** de una variable ``i`` que representará, en este caso, el índice del vector.
  - Como segundo parámetro, tenemos la **condición de parada** en la cual, mediante la función ``length`` se puede obtener la longitud exacta del vector, para asegurarse que no haya un error por desbordamiento y el recorrido pare cuando llegue a la última posición.
  - Por último, la **modificación** (incremento o decremento), es decir, la expresión que va a indicar de cuanto en cuanto crece o disminuye el índice y así poder hacer el recorrido secuencial.

<br>

## 📂 Arreglos Multidimensionales

Tambien llamados «Matrices», son arreglos multidireccionales que comprenden tablas de valores, donde cada elemento está **simultáneamente** en una fila y una columna a la vez.

- ### Declaración y Asignación

  Se declara y asigna de la misma manera que los arrays a diferencia que en la matriz van **DOS PARES de corchetes**. 

  > [!NOTE]  
  > El primer par de corchetes corresponde para las filas y el siguiente par para las columnas.

  ````java
  int [][] nombreMatriz = new int [3][3]

  // asignación manual
  matriz [0][0] = 5;
  matriz [0][1] = 57;
  matriz [0][2] = 26;
  matriz [1][0] = 95;
  matriz [1][1] = 78;
  matriz [1][2] = 2;
  matriz [2][0] = 49;
  matriz [2][1] = 811;
  matriz [2][2] = 9;
  ````

- ### Recorrido

  Las matrices al contar con filas y columnas es un poco más complicado a la hora de cargar sus datos y luego recorrerlos para poder visualizarlos. Al igual que los vectores se recorren con la estructura ``for``, pero en este caso van a ser necesarios **DOS estructuras**, uno para las filas y otro para las columnas.

  Como las matrices son estructuras estáticas y se declaran la cantidad de filas y columnas que tendrá, al momento de utilizar los ``for`` hay que poner en la **condición hasta donde se quiere llegar en la matriz** y no se utiliza el lenght.

  ````java
  // ejemplo RECORRIDO
  for (int fila=0; fila<3; fila++) {
  
    for (int columna=0; columna<3; columna++) {
        System.out.println("el valor de la posición f: " + fila + " c: " + columna);
        System.out.println("es de " + matriz[fila][columna]);
    }
  }
  ````

- ### Carga

  Para la carga se utiliza la misma estructura del ``for`` más la declaración del ``Scanner`` para cargar los valores.

  ````java
  // ejemplo ASIGNACIÓN por teclado 
  Scanner teclado = new Scanner (System.in);
  for (int fila=0; fila<3; fila++) {
  
      for (int columna=0; columna<3; columna++) {
          System.out.println("ingrese el valor de la posición f: " + fila + " c: " + columna);
          matriz[fila][columna] = teclado.nextInt());
      }
  }
  ````

<br>

## 📂 Propiedad ``length``

Todos los arrays en Java tienen una propiedad especial llamada ``length`` que te dice cuántos elementos contiene el array. Es como contar cuántos productos hay en la lista.

````java
// ejemplo Lista del Supermercado
String[] productos = {"Leche", "Pan", "Huevos", "Queso", "Manzanas"};
int numeroDeProductos = productos.length;
System.out.println("Tengo " + numeroDeProductos + " productos");  // 5
````

> [!IMPORTANT]  
> Es ``length`` (sin paréntesis), NO ``length()``. A diferencia de los métodos, ``length`` es una propiedad, no una función.

### ⇝ ¿Para qué sirve?

La propiedad ``length`` es fundamental para:

- Saber cuántos elementos hay sin tener que contarlos manualmente
- Acceder al último elemento usando ``array[array.length - 1]``
- Recorrer todos los elementos con bucles
- Evitar errores de índice fuera de rango
- Hacer validaciones como verificar si el array está vacío

<br>

````java
// ejemplo
String[] frutas = {"Manzana", "Banana", "Naranja", "Uva"};

// Obtener el último elemento sin saber el tamaño exacto
String ultimaFruta = frutas[frutas.length - 1];  // "Uva"
System.out.println("La última fruta es: " + ultimaFruta);

// Verificar si el array está vacío
if (frutas.length == 0) {
    System.out.println("El array está vacío");
} else {
    System.out.println("El array tiene " + frutas.length + " elementos");
}

// Verificar si un índice es válido antes de acceder
int indice = 10;
if (indice >= 0 && indice < frutas.length) {
    System.out.println(frutas[indice]);
} else {
    System.out.println("Índice fuera de rango");
}
````

> [!TIP]  
> El último elemento SIEMPRE está en la posición (length - 1), porque los índices empiezan en 0. Si un array tiene 5 elementos (length = 5), el último está en la posición 4 (5 - 1 = 4).

<br>

## 📂 Recorrido

Una de las cosas más útiles de los arrays es poder recorrer todos sus elementos automáticamente. En lugar de escribir array[0], array[1], array[2]... uno por uno, se usan los **bucles** para hacerlo de forma automática y elegante.

<br>

### ✧ ``for`` Tradicional

  Como vimos en los ejemplos anteriores, el bucle ``for`` es perfecto para recorrer arrays porque se puede usar un contador que va desde ``0`` hasta ``length - 1``:

  ````java
  // ejemplo Lista del Supermercado
  String[] productos = {"Leche", "Pan", "Huevos", "Queso", "Manzanas"};

  // Recorrer e imprimir todos los productos
  for (int i = 0; i < productos.length; i++) {
    System.out.println((i + 1) + ". " + productos[i]);
  }

  /* Salida:
  1. Leche
  2. Pan
  3. Huevos
  4. Queso
  5. Manzanas
  */
  ````

<br>

### ✧ ``for-each``  (Mejorado)

Java tiene una versión simplificada del bucle ``for`` especialmente diseñada para recorrer arrays. Se llama ``for-each`` y es más limpio cuando solo se quieren leer los elementos:

````java
// ejemplo Lista del Supermercado
String[] frutas = {"Manzana", "Banana", "Naranja", "Uva"};

// Sintaxis for-each
for (String fruta : frutas) {
    System.out.println("Me gusta la " + fruta);
}

/* Salida:
Me gusta la Manzana
Me gusta la Banana
Me gusta la Naranja
Me gusta la Uva
*/
````

  - ### Explicación del for-each  
    - ``for (String fruta : frutas)`` → se lee como: "Para cada fruta en frutas..."
    - ``String`` → Tipo de dato de cada elemento
    - ``fruta`` → Variable temporal que representa el elemento actual
    - ``:`` → Se lee como "en"
    - ``frutas`` → El array que queremos recorrer

<br>

### ⇒ Comparación ``for`` tradicional vs. ``for-each``

 | ``for`` tradicional | ``for-each`` |
  | :--- | :--- |
  | Tienes acceso al índice (posición) | No tienes acceso al índice |
  | Puedes modificar elementos | Solo lectura (no puedes modificar) |
  | Más complejo de escribir | Más simple y limpio |
  | Útil para operaciones complejas | Perfecto para solo leer valores |

<br>

> ✨ **Cuándo usar cada uno**
> - Usar ``for-each`` cuando solo se necesite leer y mostrar valores
> - Usar ``for`` tradicional cuando se necesite el índice o modificar elementos

<br>

## 📂 Clase java.util.Arrays

La clase ``java.util.Arrays`` pertenece al paquete `java.util` y contiene métodos estáticos que la vida al manipular arreglos (ordenar, buscar, llenar, comparar, etc.).

<br>

### ✧ Metodo `sort()`

Este método ordena los elementos de un arreglo de forma ascendente (de menor a mayor).

````java
import java.util.Arrays;

public class EjemploSort {
    public static void main(String[] args) {
        int[] numeros = {5, 1, 8, 3, 2};
        
        // Ordenamos el arreglo
        Arrays.sort(numeros);
        
        // Resultado esperado: [1, 2, 3, 5, 8]
        System.out.println(Arrays.toString(numeros));
    }
}
````

<br>

### ✧ Metodo `fill()`

Se utiliza para asignar un valor específico a todos los elementos de un arreglo (o a un rango determinado). Es ideal para "limpiar" un arreglo o inicializarlo con un valor por defecto que no sea el cero.

````java
int[] puntuaciones = new int[5];

// Llenamos todo el arreglo con el número 10
Arrays.fill(puntuaciones, 10);

// Resultado: [10, 10, 10, 10, 10]
````

<br>

### ✧ Metodo `equals()`

En Java, al usar `==` para comparar dos arreglos, se está preguntando si son el mismo objeto en la memoria (la misma dirección), no si tienen el mismo contenido. Para comparar el contenido real, se usa `Arrays.equals()`.

Este método devuelve `true` solo si:

- Ambos arreglos tienen la misma longitud.
- Todos los elementos en las mismas posiciones son iguales.

````java
int[] bandoA = {1, 2, 3};
int[] bandoB = {1, 2, 3};
int[] bandoC = {3, 2, 1};

// Comparación de contenido
System.out.println(Arrays.equals(bandoA, bandoB)); // true
System.out.println(Arrays.equals(bandoA, bandoC)); // false (mismo contenido, distinto orden)
````

<br>

### ✧ Metodo `toString(()`

Este método convierte el contenido de un arreglo en una cadena de texto (String) con un formato legible: `[elemento1, elemento2, ...]`.

````java
int[] datos = {1, 2, 3};

// Sin Arrays.toString(): [I@15db9742]
// Con Arrays.toString(): [1, 2, 3]
System.out.println(Arrays.toString(datos));
````

<br>

--- 

### **PUNTOS CLAVE A RECORDAR:**

- **In-place:**  
Métodos como `sort()` y `fill()` modifican el arreglo original directamente, no crean uno nuevo.

- **Contenido vs. Referencia:**  
Siempre usar `Arrays.toString()` para ver los datos y `Arrays.equals()` para compararlos.  
Usar `==` o el `println` directo solo dará problemas de direcciones de memoria.