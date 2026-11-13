# 📌 Patrón DTO (Data Transfer Object)

Una de las problemáticas más comunes a la hora de desarrollar aplicaciones (sobre todo web) es la necesidad de **interconexión e intercambio de mensajes** entre capas u otras aplicaciones. Esto hace que sea realmente importante, el hecho de encontrar una forma de diseñar cómo o mediante qué formato debe transmitirse la información.

Es común en estos casos que se utilicen las mismas clases / entidades que hay creadas en el modelo de la aplicación; sin embargo, existe una forma más óptima para llevar a cabo esta tarea: implementando el patrón DTO.

**DTO** es un **patrón de diseño** que tiene como finalidad **crear un objeto plano (POJO)** con una serie de atributos que puedan ser enviados o recuperados del servidor en una sola invocación. Un DTO puede **contener datos de múltiples clases, fuentes o tablas de una base de datos y agruparlos en una única clase simple**.

<br>

En base a esto se puede decir que DTO permite:

- Crear estructuras de datos totalmente independientes al modelo de datos (o clases entidades).
- Incorporar en una misma clase elementos o datos de clases distintas según la necesidad que tengamos.

<br>

Como ventaja principal de implementar DTO, un caso común que suele darse día a día en un ambiente de desarrollo, donde el modelo de datos deba cambiar por algún motivo en particular. Si esto sucede, no afectará a la forma en la que DTO devuelve los datos, ya que su estructura seguiría siendo la misma.

**Spring** permite manejar **objetos DTO** dentro del **controller** para luego transformarlos en formato **JSON** y retornarlos al cliente que haya realizado una determinada solicitud.

<br>

### ▪︎ ¿Cómo implementar DTO?
Supongamos un caso de una inmobiliaria, que contiene una clase `Propiedad` (muestra los datos de una determinada propiedad en alquiler) y una clase `Inquilino` (muestra los datos de un potencial inquilino).

En el modelo de datos, ambas clases estarán por separado, pero si aplicamos el **patrón DTO**, podemos crear una clase que incorpore los datos que necesitamos de cada una de ellas para devolverlo en una response. 

<br>

Ejemplo paso a paso:

- **PASO 1️⃣**<br>
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

- **PASO 2️⃣**<br>
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

- **PASO 3️⃣** <br>
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

- **PASO 4️⃣** <br>
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

> 💡 **NOTA**  
> ¿Por qué es importante utilizar DTO? Porque disminuye la carga de datos que son devueltos desde el servidor hacia el cliente (bajando de esa manera también el tiempo de respuesta) y facilita ampliamente, al cliente que esté consultando, la posibilidad de obtener únicamente los datos que está necesitando, sin tener que hacer luego un «refiltrado» entre todos los datos que pueda recibir.

<br>

### ▪︎ Relación entre LOMBOK y los DTO
- Un **DTO** es simplemente una clase Java (POJO) que se usa para transportar datos entre capas o a través de la red.  
- **Lombok** es una librería que reduce el código repetitivo que no aporta lógica (boilerplate code) en POJOs, incluyendo DTOs. 

Esta relación genera un código mucho más limpio, y sigue funcionando igual.
