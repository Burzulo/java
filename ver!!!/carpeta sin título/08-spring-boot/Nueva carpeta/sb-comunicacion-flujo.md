# 📌 Comunicación y Flujo de Datos

<br>

- [Manejo de datos en Endpoints: *`@PathVariable`*, *`@RequestParam`*, *`@RequestBody`*, *`@RequestHeader`*](#-manejo-de-datos-en-endpoints)
- [Patrón DTO](#-patron-dto)
- [❌ Respuestas ...](#-...)

<br>

## 📂 Manejo de datos en Endpoints

Los parámetros en endpoints son los datos que un método del controlador recibe desde el cliente para procesar una petición. Estos pueden llegar de distintas formas:

- `@PathVariable`
- `@RequestParam`
- `@RequestBody`
- `@RequestHeader`

Cada tipo de parámetro se maneja con su propia anotación, lo que permite capturar y utilizar la información de manera precisa y eficiente.

<br>

### 🔖 `@PathVariable` – en la ruta de la URL

Así como en un `@GetMapping` puede establecerse un determinado *path*, también es posible recibir, tal como el **método HTTP GET** lo indica, valores o parámetros **mediante la URL**. Éstos, pueden asignarse a las diferentes funciones que tengamos en el controller a partir de la annotation `@PathVariable`.

```java
// ejemplo

public class pruebaController {

  @GetMapping ("/hello/{nombre}")  // nombre del parámetro en la URL
  public String sayHello(@PathVariable String nombre) {  // mismo "nombre" que el @PathVariable  
    return "Hola " + nombre;
  }
}
```

Aqui se recibe mediante el método GET y por la URL un «nombre» como parámetro. Con `@PathVariable` se asigna este valor a una variable (que debe tener el mismo nombre) para luego utilizarla en la función en cuestión, en este caso, para agregar el «nombre» al saludo «Hola».

> Si realizamos pruebas enviando diferentes parámetros «nombre», vamos a recibir diferentes respuestas.

Se pueden agregar nuevos parámetros e ir recibiéndolos por la URL de la misma manera sea tanto en el mismo end-point, como creando un endpoint distinto. De esta manera, si enviamos solo el parámetro «nombre» nos va a responder el primer endpoint, mientras que si también enviamos «edad» y «profesión», nos va a responder el segundo.

```java
@GetMapping ("/bye/{nombre}/{edad}/{profesion}") 
public String sayBye(@PathVariable String nombre,
                     @PathVariable int edad,
                     @PathVariable String profesion) {
    return "Chau ! " + "Nombre: " + nombre + " Edad: " + edad + " Profesión: " + profesion;
}
```

**Ejemplo:**  
 `http://localhost:8080/bye/Pedro/48/Contratista` dará como salida:
 > *«Chau ! Nombre: Pedro Edad: 48 Profesión: Contratista»*

<br>

### 🔖 `@RequestParam` – como parte de la cadena de consulta

Otra forma de recibir múltiples parámetros en un endpoint dentro de un controller, es mediante el uso de la annotation `@RequestParam`. Ésta **permite recibir parámetros** mediante el método GET.

La especificación de los parámetros no se realiza mediante la separación con «paths», sino que se manifiesta mediante un signo `?` luego del path en cuestión y a partir de él, cada uno de los parámetros se indica mediante su nombre, un símbolo igual y su valor.  
En caso de que haya más de un parámetro, se unen entre sí mediante el símbolo `&`.

Para hacer uso de cada uno de estos parámetros dentro del endpoint, se debe especificar la anotación `@RequestParam` por cada uno de los parámetros que recibiremos, con su respectiva variable asociada.  

```java
// ejemplo

@RestController
public class pruebaController {
 
    @GetMapping ("/hola") // en el path no se especifican los parámetros
    public String sayHola(@RequestParam String nombre,  // se especifica el RequestParam
                          @RequestParam int edad,
                          @RequestParam String profesion) {
            
        return "Hola " + "Tu nombre es " + nombre + ". Tienes " + edad + " años. De profesión " + profesion;
    }
}
```

Ésto, dará como resultado en el navegador lo mismo que utilizando `@PathVariable`. Sin embargo la forma en la que viajan los datos en la solicitud, como así también la forma de trabajarlos internamente, es totalmente distinta.

**Ejemplo:**  
 `http://localhost:8080/hola?nombre=Pedro&edad=48&profesion=Contratista` dará como salida:
 > *«Hola Tu nombre es Pedro. Tienes 48 años. De profesión Contratista»*

<br>

> 💡 **NOTA**  
> `@PathVariable` y `@RequestParam` cumplen funciones muy similares, sin embargo, sus implementaciones son diferentes. En `@PathVariable`, los parámetros se brindan mediante diferentes apartados path (`/`) de la dirección, mientras que en `@RequestParam`, los datos se especifican dentro de un mismo path mediante el símbolo `?` y separando a cada uno de ellos mediante el símbolo `&`.

<br>

### 🔖 `@RequestBody` – en el cuerpo de la solicitud
`@PostMapping` tiene un fiel aliado a la hora de recibir valores en una solicitud o *request*, la annotation `@RequestBody`.  
Ésta permite recibir objetos de dominio completos en cualquier endpoint de nuestra API dentro del cuerpo (*body*) de la request.  
Estos datos que se reciben en el body serán transformados luego en objetos de Java dentro de nuestra aplicación.

Supongamos que tenemos una clase llamada `Cliente` con los atributos `id`, `nombre`, `apellido` y sus respectivos getters y setters, simplificados mediante Lombok:

```java
@Getter @Setter
public class Cliente {

    private Long id;
    private String nombre;
    private String apellido;
}
```

A partir de esta clase, suponiendo que en el controller está el método `nuevoCliente`, mapeado con `@PostMapping ("/cliente")`:

Con esto armado, mediante `@RequestBody` se podrían recibir los datos correspondientes a un cliente y transformarlos en un objeto de la clase `Cliente` en Java. Pero… ¿Cómo podríamos hacer esto? A continuación un ejemplo del código:

```java
@RestController
public class aplicacionController {

    @PostMapping ("/cliente")
    public void nuevoCliente(@RequestBody Cliente cli) {

        // probamos que nos devuelva por consola del servidor los datos que recibimos
        // desde el cliente mediante el body de la solicitud
        System.out.println("Datos del cliente. Nombre: " + cli.getNombre() + " Apellido: " + cli.getApellido());
    }
}
```

<br>

Como se mencionó, el método **POST no envía valores mediante la URL**, sino mediante el *body* o la cabecera de las solicitudes HTTP.  
Para probar estos endpoints, se necesita simular solicitudes POST, ya que **los navegadores solo utilizan GET por defecto**.  
Por ello que se necesita, para simular solicitudes POST un software adicional. Uno de los más utilizados para realizar este tipo de pruebas, es **Postman**.

<br>

### 🔖 @RequestHeader – en las cabeceras HTTP
🚧 *Falta completar esta sección. !!!!!!!!!!!!!!!!!!!!!!*

<br>

## 📂 Patron DTO

Una de las problemáticas más comunes a la hora de desarrollar aplicaciones (sobre todo web) es la necesidad de **interconexión e intercambio de mensajes** entre capas u otras aplicaciones. Esto hace que sea realmente importante, el hecho de encontrar una forma de diseñar cómo o mediante qué formato debe transmitirse la información.

Es común en estos casos que se utilicen las mismas clases / entidades que hay creadas en el modelo de la aplicación; sin embargo, existe una forma más óptima para llevar a cabo esta tarea: implementando el patrón DTO.

**DTO** (Data Transfer Object) es un **patrón de diseño** que tiene como finalidad **crear un objeto plano (POJO)** con una serie de atributos que puedan ser enviados o recuperados del servidor en una sola invocación. Un DTO puede **contener datos de múltiples clases, fuentes o tablas de una base de datos y agruparlos en una única clase simple**.

<br>

En base a esto se puede decir que DTO permite:

- Crear estructuras de datos totalmente independientes al modelo de datos (o clases entidades).

- Incorporar en una misma clase elementos o datos de clases distintas según la necesidad que tengamos.

<br>

**Spring** permite manejar **objetos DTO** dentro del **controller** para luego transformarlos en formato **JSON** y retornarlos al cliente que haya realizado una determinada solicitud.

<br>

### ▪︎ ¿Cómo implementarlo?

Supongamos un caso de una inmobiliaria, que contiene una clase `Propiedad` (muestra los datos de una determinada propiedad en alquiler) y una clase `Inquilino` (muestra los datos de un potencial inquilino).

En el modelo de datos, ambas clases estarán por separado, pero si aplicamos el **patrón DTO**, podemos crear una clase que incorpore los datos que necesitamos de cada una de ellas para devolverlo en una response. 

Ejemplo paso a paso:

- **PASO 1️⃣**

  Crear un proyecto SpringBoot con Initializr. Luego dentro de él, crear las clases `Propiedad` e `Inquilino`.

  ```java
  public class Propiedad {
    private Long id_propiedad;
    private String tipo_propiedad;
    private String direccion;
    private Double metros_cuadrados;
    private Double valor_alquiler;
  }
     
  public class Inquilino {
    private Long id_inquilino;
    private String dni;
    private String nombre;
    private String apellido;
    private String profesion;
  }
  ```

<br>

- **PASO 2️⃣**

  Crear una clase llamada `PropiedadDTO`, donde se incorporan datos combinados de las propiedades y de los inquilinos (suponiendo que solo esos datos le sirven/interesan al cliente que recibirá la respuesta de nuestra API).

  ```java
  public class PropiedadDTO implements Serializable {
    private Long id_propiedad;
    private String tipo_propiedad;
    private String direccion;
    private Double valor_alquiler;
    private String nombre_inquilino;
    private String apellido_inquilino;
  }
  ```

<br>  

- **PASO 3️⃣**

  Crear el paquete controller y dentro armar la clase controladora. Luego crear un nuevo endpoint, donde abra un objeto `propiedad` y otro `inquilino` que unificamos en un objeto de tipo `PropiedadDTO` para devolverlo mediante `@ResponseBody`.

  ```java
  @RestController
  public class AlquileresController {
     
    @GetMapping ("/propiedad/{id}")
    @ResponseBody
    public PropiedadDTO devolverPropiedad(@PathVariable Long id) {
     
      // suponiendo que se obtiene una propiedad por su id y su inquilino desde una BD
      Inquilino inqui = new Inquilino (1L, "295687366", "Gonza", "Alba", "Sommelier");
      Propiedad prop = new Propiedad (563L, "Casa", "308 Calle Lane", 200.0, 400000.0);
     
      PropiedadDTO propiDTO = new PropiedadDTO();
     
      // Se unifican los datos del inquilino y la propiedad en un solo objeto
      propiDTO.setId_propiedad(prop.getId_propiedad());
      propiDTO.setTipo(prop.getTipo_propiedad());
      propiDTO.setDireccion(prop.getDireccion());
      propiDTO.setValor_alquiler(prop.getValor_alquiler());
      propiDTO.setNombre_inquilino(inqui.getNombre());
      propiDTO.setApellido_inquilino(inqui.getApellido());
     
      return propiDTO;
    }
  }
  ```

<br>

- **PASO 4️⃣**

  Se ejecuta la API desarrollada y probamos realizar con Postman una solicitud y ver si obtenemos como respuesta el objeto DTO que se acaba de crear. Si todo fue realizado correctamente, se obtiene como respuesta nuestro objeto DTO.

  En Postman debe aparecer:

  ```json
  GET localhost:8080/propiedad/563
  
  {
    "id_propiedad": 56321,
    "tipo": "Casa",
    "direccion": "308 Calle Lane",
    "valor_alquiler": 400000.0,
    "nombre_inquilino": "Gonza",
    "apellido_inquilino": "Alba"
  }
  ```

<br>

> 💡 **¿Por qué es importante utilizar DTO?**  
> Porque disminuye la carga de datos que son devueltos desde el servidor hacia el cliente (bajando de esa manera también el tiempo de respuesta) y facilita ampliamente, al cliente que esté consultando, la posibilidad de obtener únicamente los datos que está necesitando, sin tener que hacer luego un «refiltrado» entre todos los datos que pueda recibir.

<br>

### 🔹 Relación entre LOMBOK y los DTO

- Un **DTO** es simplemente una clase Java (POJO) que se usa para transportar datos entre capas o a través de la red.

- **Lombok** es una librería que reduce el código repetitivo que no aporta lógica (boilerplate code) en POJOs, incluyendo DTOs. 

Esta relación genera un código mucho más limpio, y sigue funcionando igual.