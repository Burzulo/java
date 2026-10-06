# 📌 Entrada / Salida Estándar

<br>

- [Entrada / Salida (I/O): `Scanner`, `System.out`](#-entrada-salida)
- [Manejo de rutas: `java.nio.file`](#-)

<br>

## 📂 Entrada / Salida

La **Entrada/Salida (I/O)** se refiere a la comunicación entre el programa Java (la JVM) y el mundo exterior (el entorno, el usuario, o archivos). Esta comunicación se gestiona mediante **Flujos** o **Corrientes (Streams)**, que son secuencias de datos que fluyen del origen al destino.

Java proporciona tres flujos estándar de forma predeterminada, definidos como campos **estáticos y públicos** dentro de la clase `System` (`java.lang.System`):

1. **`System.in` (Entrada Estándar):**
    * **Propósito:** Leer datos
    * **Origen:** Típicamente el teclado
    * **Tipo:** Es un objeto de la clase `InputStream`

2. **`System.out` (Salida Estándar):**
    * **Propósito:** Mostrar resultados o mensajes informativos
    * **Destino:** Típicamente la pantalla (consola)
    * **Tipo:** Es un objeto de la clase `PrintStream`

<br>

### 🔖 Gestión de la Entrada: La Clase `Scanner`

**`System.in`** es una corriente **cruda** de bytes que vienen del teclado. Para que sea fácil de usar y permita leer tipos de datos (`int`, `double`, `String`, ...), necesitamos una clase utilitaria que envuelva ese flujo.

### ▫️ Rol de `Scanner`

La clase `Scanner` es una utilidad diseñada para **tokenizar** (dividir en piezas) el flujo de entrada basándose en un delimitador (por defecto, el espacio en blanco).

1. **Instanciación:**

    * La sintaxis para crear un objeto `Scanner` requiere que le especifiquemos qué flujo debe "escanear":
        
      ```java
      Scanner lector = new Scanner(System.in);
      ```

    * `System.in` actúa aquí como el **argumento** que le indica a `Scanner` que lea desde el teclado.

2. **Métodos de Lectura (Parsing):**

    * El `Scanner` tiene métodos específicos para **analizar** y **convertir** el texto de entrada en el tipo de dato deseado:

        * `lector.nextInt()`: Lee el siguiente token como un `int`.
        * `lector.nextDouble()`: Lee el siguiente token como un `double`.
        * `lector.nextLine()`: Lee toda la línea restante hasta el salto de línea.

          > 💡 **NOTA**  
          > ``lector`` hace referencia al nombre que el programador le ha asignado a una instancia (un objeto) de la clase Scanner, creado previamente.

<br>

### 🔖 Gestión de la Salida: `System.out`

El objeto **`System.out`** es el mecanismo fundamental en Java para mostrar información del programa al entorno, típicamente la consola. Su Función es mostrar mensajes informativos, resultados de cálculos y cualquier salida normal del programa al usuario.

### ▫️ Métodos Principales de `System.out`

Los métodos clave de la clase `PrintStream` son esenciales para controlar cómo y qué se muestra en la consola:

<br>

| Método | Argumentos | Efecto en la Salida | Uso Típico |
| :--- | :--- | :--- | :--- |
| **`print()`** | Cualquier tipo primitivo, `String`, u `Object`. | Imprime el dato y **mantiene el cursor en la misma línea**. | Construir una frase usando múltiples llamadas. |
| **`println()`** | Cualquier tipo primitivo, `String`, u `Object`. | Imprime el dato y automáticamente añade un carácter de **salto de línea** (`\n`). | Imprimir líneas de código secuenciales. |
| **`printf()`** | `String` de formato + argumentos variables. | Permite la **salida formateada** (ej. justificación, número de decimales), utilizando códigos como `%d` (entero) o `%.2f` (dos decimales). | Mostrar datos de ingeniería o tablas con precisión. |

<br>

> 💡 **Impresión de Objetos**  
> Cuando llamas a cualquiera de estos métodos con un objeto como argumento (ej., `System.out.println(miObjeto)`), Java automáticamente invoca el método **`toString()`** del objeto. Si el alumno no sobreescribe este método, se imprimirá la representación por defecto de la clase (que incluye la dirección de memoria).

<br>

<br>

> ▶️📚 **links**  
> [Entrada y Salida de Datos | Omega Knowledge](https://www.omega-knowledge.dev/curso/java/entrada-y-salida-de-datos-en-java)