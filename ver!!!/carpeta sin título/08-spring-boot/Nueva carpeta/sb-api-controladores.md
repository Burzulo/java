#  📌 Capa de Controladores (REST)

<br>

- [Introducción a las APIS REST](#-api-rest)
- [Concepto de JSON](#-formato-json)
- [indice ❌](#-...)
- [Mapeo de Rutas: *`@RequestMapping`*](#-mapeo-de-rutas)
- [Anotaciones HTTP: *`@GetMapping`*, *`@PostMapping`* ... ](#-anotaciones-http)

<br>

## 📂 API REST

### ▪︎ ¿Qué son las APIS?
Una **API (Application Programming Interface)** es un conjunto de funciones y procedimientos que permiten que dos aplicaciones se comuniquen entre sí, incluso si están desarrolladas en diferentes lenguajes de programación.

Actúan como una **INTERMEDIARIA** que facilita el intercambio de datos y funcionalidades. Por ejemplo, una API meteorológica puede recibir un código postal desde un cliente y devolver información sobre la temperatura máxima y mínima del día.

### ▪︎ ¿Qué significa REST?

La forma mas comun de implementacion de una API es mediante **REST (Representational State Transfer)**. Este es un tipo de servicio que se caracteriza por **no tener estado alguno** y por lograr interconexiones mediante el protocolo HTTP con mensajes de tipo **XML** o **JSON**.

Una API basada en REST se conoce como **API REST** o **RESTful API**.

> Las APIs REST son ampliamente utilizadas por su simplicidad, escalabilidad y compatibilidad con distintos lenguajes y plataformas.

  ````java
     🖥️    -- GET/POST/PUT/DELETE -->      ☁️    ---->      🗄️
   Client  <-------- JSON -----------   Rest Api  <----   Database
  ````

<br>

### 🔹 Principios de las API REST

1. **Arquitectura Cliente-Servidor:**  
   El cliente maneja la interfaz de usuario y el servidor gestiona la lógica y los datos. Esto permite que ambos evolucionen de manera independiente.

2. **Sin Estado (Stateless):**  
   Cada petición HTTP debe contener toda la información necesaria para ser procesada. El servidor no guarda el estado de la sesión.

3. **Cacheabilidad:**  
   Las respuestas deben indicar si pueden almacenarse en caché para mejorar el rendimiento.

4. **Interfaz Uniforme:**  
   La comunicación entre cliente y servidor debe seguir un formato estandarizado.

5. **Sistema en Capas:**  
   La arquitectura puede dividirse en capas (servidor de API, lógica, base de datos), sin que el cliente las perciba directamente.

6. **Código bajo demanda (opcional):**  
   El servidor puede enviar código al cliente para ser ejecutado dinámicamente, aunque no es un requisito obligatorio.

<br>

### 🔹 Componentes Clave de una API REST

- #### Recursos
  Todo lo que la API gestiona (usuarios, publicaciones, productos, etc.) se denomina **recurso**.  
  Cada recurso se identifica con una **URI** (por ejemplo, `/posteos` o `/usuarios/5`).

- #### Métodos HTTP
  Las operaciones sobre los recursos se realizan mediante los métodos del protocolo HTTP:

   | Método | Acción | Descripción |
   |--------|--------|-------------|
   | **GET** | Leer | Obtiene datos del servidor |
   | **POST** | Crear | Envía datos para crear un nuevo recurso |
   | **PUT** | Actualizar | Modifica un recurso existente |
   | **DELETE** | Eliminar | Borra un recurso |

- #### Representaciones
   Las respuestas de la API se envían en un formato estándar, normalmente **JSON**, por ejemplo:

   ```json
   [
      {
        "id": 1,
        "titulo": "¿Cómo formatear una PC?",
        "autor": "Gonzalo"
      },
      {
        "id": 2,
        "titulo": "¿Cómo mantener la seguridad?",
        "autor": "Pedro"
      }
   ]
   ```

<br>

### 🔹 Buenas Prácticas en el Diseño de APIs REST

- Define claramente tus **recursos** y sus rutas (URIs).  
- Usa los **métodos HTTP adecuados** según la acción.  
- Devuelve los **códigos de estado HTTP** correctos (200 OK, 201 Created, 404 Not Found, etc.).  
- Mantén las peticiones **independientes y sin estado**.  
- Implementa **versionado** si tu API evolucionará con el tiempo.  
- Usa **autenticación basada en tokens (JWT)** en lugar de sesiones.  
- Documenta tu API con herramientas como **Swagger** o **Postman**.

### 🔹 Beneficios de las API REST

- **Ligereza y velocidad** ⇒ al ser sin estado y basarse en HTTP.  
- **Independencia del lenguaje** ⇒ el cliente puede estar en Java, Python, JavaScript, etc.  
- **Escalabilidad** ⇒ fácil de distribuir en varios servidores.  
- **Reutilización** ⇒ una misma API puede ser consumida por distintas aplicaciones.

<br>

## 📂 Formato JSON

JSON (*Javascript Object Notation*), es un formato de texto que es utilizado principalmente para el intercambio de datos mediante el **protocolo HTTP** entre diferentes sistemas o **APIS** interconectados entre sí.

Sirve como un lenguaje «intermedio», dado que independientemente del lenguaje de programación, es posible traducir los datos que se requieren transferir entre sistemas a JSON. No depende de un lenguaje en particular: aunque su sintaxis proviene de JavaScript, se usa en casi todos los lenguajes (Java, Python, PHP, C#, etc.)

JSON se vale del concepto **«clave-valor»**, donde para cada clave existe un valor asociado. Un **conjunto de claves y valores conforman un objeto**, que en JSON se representa mediante la apertura y cierre de llaves `{}`.

Un ejemplo sencillo de la sintaxis de un mensaje JSON:

```json
{
    "nombre" : "Lionel"
    "apellido" : "Messi"
    "edad" : 38  // los valores numericos no llevan " "
}

// Las claves van del lado izquierdo y los valores del lado derecho.
```

Si se quiere incorporar al JSON del ejemplo, los equipos donde jugó, se puede hacer mediante la incorporación de `[]` donde la clave «equipos» no contendrá solo un valor, sino un conjunto de valores.

```json
{
    "nombre" : "Lionel"
    "apellido" : "Messi"
    "edad" : 38
    "equipos" : ["Barcelona",
                 "PSG",
                 "Inter Miami"]
}
```

De igual manera, así como en el JSON anterior hay solo un objeto, es posible incorporar varios objetos, donde cada uno de ellos estará separado por `,` (coma) y un nuevo par de llaves `{}`.

```json
[
    {
        "nombre" : "Lionel"
        "apellido" : "Messi"
        "edad" : 38
        "equipos" : ["Barcelona",
                     "PSG",
                     "Inter Miami"]
    },
    {
        "nombre" : "Cristiano"
        "apellido" : "Ronaldo"
        "edad" : 40
        "equipos" : ["Sporting Club",
                     "Manchester United",
                     "Real Madrid",
                     "Juventus"]
    },
]
```

> ⚠️ **IMPORTANTE**  
> JSON representa datos mediante dos construcciones principales:
  > - Objeto: Una colección desordenada de pares clave : valor, encerrados entre llaves `{}`.
  > - Arreglo (array): Una lista ordenada de valores, encerrada entre corchetes `[]`.

<br>

### ▫️ En el contexto de Spring Boot

Spring Boot (o sus librerías como Jackson) convierte automáticamente objetos de Java a JSON (serialización) y de JSON a objetos Java (deserialización) cuando usas anotaciones como `@RequestBody` y `@ResponseBody`.

Cuando defines un endpoint que devuelve datos, esos datos suelen representarse como JSON para que el cliente (por ejemplo, una aplicación frontend o móvil) los pueda consumir.

<br>

> **¿Por qué es importante manejar y conocer JSON?**  
> Porque la mayor parte de las API REST que se encuentran productivas en la actualidad, utilizan a JSON como formato de mensaje para comunicarse mediante el protocolo HTTP.

<br>

## 📂 ...

<br>

## 📂 Mapeo de Rutas

``@RequestMapping`` es la anotación más antigua y general para **mapear peticiones HTTP** a métodos y clases en Spring MVC / Spring Boot.

Sirve para decirle a Spring:

> « Cuando llegue una solicitud a esta URL y con este método HTTP, ejecutá este método ».

Debido a que el uso de ``@RequestMapping`` es tan común para mapear los métodos HTTP estándar, Spring introdujo anotaciones de **"atajo" (shortcuts)** que son más claras y concisas.  
Existen las anotaciones especializadas (``@GetMapping``, ``@PostMapping``, etc.), pero todas ellas internamente se basan en ``@RequestMapping``.

<br>

### 🔹 ¿Dónde se puede usar?

Se puede aplicar tanto en:

- ### Controladores completos (Nivel Clase)

    Define un prefijo de ruta común para todos los endpoints dentro del controlador.

   ````Java
   @RestController
   @RequestMapping("/api/clientes")
   public class ClienteController {
     
   }
   ````

   Eso significa que cualquier método dentro de este controlador tendrá su ruta empezando por:

   ````bash
   /api/clientes
   ````

- ### Métodos (Nivel Función)

   Define rutas específicas para solicitudes HTTP.

   ````Java
   @RequestMapping("/listar")
   public String listarClientes() {
      return "listado";
   }
   ````

   Esto respondería a la URL:

   ````bash
   /api/clientes/listar
   ````

   (si el controlador tuviera el prefijo anterior).

<br>

### 🔹 ¿Por qué existen ``@GetMapping``, ``@PostMapping``, etc. entonces?

Porque ``@RequestMapping`` es demasiado genérico. Entonces para evitar tener que escribir:

````java
@RequestMapping(value="/clientes", method=RequestMethod.GET)
````

Se usa:

````java
@GetMapping("/clientes")
````

<br>

### 🔹 Entonces… ¿Cuándo se sigue usando ``@RequestMapping``?

Aunque los ``@*Mapping`` modernos son más comunes, ``@RequestMapping`` sigue siendo útil cuando:

- ### Se quiere mapear un controlador entero a un path común

   ````java
   @RestController
   @RequestMapping("/api/empleados")
   public class EmpleadoController { ... }
   ````

- ### Se necesitan aceptar varios métodos HTTP en un solo endpoint

   ````java
   @RequestMapping(value="/ping", method={RequestMethod.GET, RequestMethod.POST})
   public String ping() {
      return "OK";
   }
   ````

- ### Es necesario configurar parámetros más avanzados

   Como headers requeridos o formatos específicos:

   ````java
   @RequestMapping(
      value = "/upload",
      headers = "content-type=multipart/form-data"
   )
   ````

<br>

## 📂 Anotaciones HTTP

En Spring Boot, las anotaciones de métodos HTTP permiten definir de forma declarativa qué tipo de operación maneja un método dentro de un controlador. Cada anotación **indica el verbo HTTP correspondiente** y establece cómo se accede al recurso desde el cliente. Esto facilita la creación de endpoints claros y organizados, alineados con las buenas prácticas de las API REST.

- `@GetMapping` ⇒ leer datos
- `@PostMapping` ⇒ crear datos
- `@PutMapping` ⇒ actualizar datos
- `@DeleteMapping` ⇒ eliminar datos

<br>

### 🔖 @GetMapping – para leer datos

`@GetMapping` es una annotation de Spring Boot para **identificar a los métodos** que pueden **actuar dentro de una API** cuando la misma reciba una **solicitud GET** mediante el protocolo HTTP.

Si se mappea un método con `@GetMapping` de forma genérica, sin especificar una URL en particular, se ejecutará el primer método que se encuentre asignado, dado que como response se enviará lo que se encuentre en el directorio raíz de la aplicación; sin embargo, es posible especificar una URL en particular a cada *método / end-point* que tengamos, de forma tal que dependiendo de la solicitud que recibamos, sea diferente la respuesta.

#### ▫️ EJEMPLO

Probemos modificar la app Hello World. En lugar de dejar el `@GetMapping` genérico, vamos a agregarle un path a la url, por ejemplo `/hello` y vamos a agregar otro método mediante `@GetMapping` que tenga el path `/bye`. Uno de ellos va a saludar y otro a despedir.

```java
@RestController
public class pruebaController {
    
  @GetMapping ("/hello") // ← Path «/hello» agregado 
  public String sayHello() {
      return "Hola Olivia";
  }
    
  @GetMapping ("/bye") // ← Path «/bye» agregado
  public String sayBye() {
      return "Chau Olivia";
  }
}
```

Una vez hecho esto, al ejecutar la aplicación, si se envía una solicitud al directorio raíz (es decir, sin especificar ninguna «/» en la URL) obtendremos un mensaje de error de que el recurso no existe; sin embargo, si colocamos `/hello` o `/bye` obtendremos el mensaje de respuesta que corresponda según la url que hayamos ingresado:

<br>

- localhost:8080 ⇒ Sin path  
  Mensaje → Whitelabel Error Page

- localhost:8080/hello ⇒ Path `/hello`  
  Mensaje → Hola Olivia

- localhost:8080/bye ⇒ Path `/bye`  
  Mensaje → Chau Olivia

<br>

### 🔖 @PostMapping – para crear datos
La annotation `@PostMapping` se emplea para manejar solicitudes HTTP POST, utilizadas principalmente para crear nuevos recursos en el servidor. El cliente suele enviar la información en el cuerpo de la petición, normalmente en formato JSON. El servidor procesa esos datos, crea el recurso y devuelve una respuesta.

La annotation se coloca para mapear el método que se ejecutará al recibir la petición POST en la determinada URL que se especifique.

```java
// Ejemplo

@RestController
public class holaController {
    
  @PostMapping ("/cliente")
  public void nuevoCliente() {

  ....  // lo que hará el método
  }
}
```

> **NOTA**  
> ``@PostMapping`` tiene un fiel aliado a la hora de recibir valores en una solicitud o request, la annotation ``@RequestBody``.
Ésta permite recibir objetos de dominio completos en cualquier endpoint de la API dentro del cuerpo (body) de la request.
Estos datos que se reciben en el body serán transformados luego en objetos de Java dentro de la aplicación.

<br>

### 🔖 @PutMapping – para actualizar datos

`@PutMapping` se utiliza para manejar solicitudes HTTP PUT. Este método se usa para **actualizar completamente un recurso existente**.

Por convención, la URL suele incluir el **id del recurso a actualizar**. El cliente envía la información completa del objeto actualizado.  
Requiere enviar el objeto completo en el cuerpo de la petición.

```java
// Ejemplo

@RestController
public class ClienteController {

  @PutMapping ("/cliente/{id}")
  public String actualizarCliente(@PathVariable Long id, @RequestBody Cliente datosActualizados) {
      // lógica para actualizar al cliente con ese id

  return "Cliente actualizado correctamente";

  }
}
```

<br>

### 🔖 @DeleteMapping – para eliminar datos

`@DeleteMapping` maneja solicitudes HTTP DELETE, utilizadas para **eliminar recursos del servidor**.

Este método generalmente recibe un **id** por la URL para identificar qué recurso debe eliminarse.  
Una vez procesada la petición, el servidor responde normalmente con un código HTTP 200 OK o 204 No Content si la eliminación se realiza con éxito.

```java
// Ejemplo

@RestController
public class ClienteController {


   @DeleteMapping ("/cliente/{id}")
   public String eliminarCliente(@PathVariable Long id) {
       // lógica para eliminar el cliente

  return "Cliente eliminado correctamente";
  
  }
}
```

<br>

### ✔️ Resumen Final

<br>

| Método HTTP | Anotación Spring | Acción | Uso típico |
|-------------|------------------|--------|------------|
| GET | `@GetMapping` | Leer | Obtener datos de la API |
| POST | `@PostMapping` | Crear | Registrar un recurso nuevo |
| PUT | `@PutMapping` | Actualizar | Reemplazar un recurso existente |
| DELETE | `@DeleteMapping` | Eliminar | Borrar un recurso |
