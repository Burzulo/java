#  📌 Creando un CRUD con JPA + Hibernate

<br>

### ▫️Configuración JPA + Hibernate
  > A partir de las configuraciones realizadas en la clase pasada: [Configurando un proyecto con JPA + Hibernate](proyecto-jpa-&-hibernate.md), en donde se establecio nuestro modelo `Persona`, nuestro `@Repository PersonaRepository`, nuestro `@Service PersonaService` (sin métodos implementados) y nuestra interfaz de métodos CRUD `IPersonaService`, podemos proceder a realizar la implementación de cada método CRUD.

<br>

## 🏷️ @Métodos CRUD en la Capa Service

<br>

- **PASO 1️⃣**  

  A partir de la correcta creación de la clase de secuencias de Hibernate y de la clase `Persona` de la clase anterior, es posible llevar a cabo los métodos correspondientes para lograr un CRUD.

  Para ello, es necesario configurar los servicios que tendrá disponible la aplicación, para lo cual se deberá crear una interface `IPersonaService` la cual contendrá los métodos necesarios para el ABML SIN IMPLEMENTARLOS (dado que es una interfaz).

  ```java
  public interface IPersonaService {

    // método para traer todas las personas
    public list<Persona> getPersonas();

    // método para dar de alta una persona
    public void savePersona (Persona perso);

    // método para borrar una persona
    public void deletePersona (Long id);

    // método para encontrar una persona
    public Persona findPersona (Long id);

  }
  ```
<br>

- **PASO 2️⃣**  

  Se debe implementar la interfaz `IPersonaService` desde la clase `PersonaService` para poder empezar con la implementación de cada método:

  ```java
  // Implementación de IPersonaService desde PersonaService

  @Service
  public class PersonaService implements IpersonaService {

  }
  ```

  ```java
  // Métodos que se sobrescriben a partir de la implementación de IPersonaService

  @Service
  public class PersonaService implements IpersonaService {

    @Override
    public List<Persona> getPersonas() {

    }

    @Override
    public void savePersona(Persona perso) {
      
    }

    @Override
    public void deletePersona(Long id) {
      
    }
    
    @Override
    public Persona findPersona(Long id) {
      
    }
    
  }
  ```

  <br>

  > 💡 **NOTA**  
  > En Java, una **interfaz** como `IPersonaService` define un conjunto de métodos que deben existir, pero sin código. `PersonaService` usa `implements` para cumplir ese contrato y escribir cómo funciona cada método. Por lo tanto Implementar la interfaz es el paso necesario para poder empezar a desarrollar la lógica real del servicio.

<br>

- **PASO 3️⃣**  
  
  Hecho el paso 2, y antes de implementar cada uno de los métodos a nivel lógico, es importante generar la inyección de dependencias entre `PersonaService` y `PersonaRepository`, dado que `PersonaRepository` será la clase encargada de proporcionarnos los datos.  
  
  Para ello, se crea un objeto de tipo `PersonaRepository` y se inyecta la dependencia mediante `@Autowired`

  ```java
  @Service
  public class PersonaService implements IpersonaService {

    @Autowired
    private PersonaRepository persoRepository;
  ```

<br>

- **PASO 4️⃣ – READ/CONSULTA**  
  
  En este paso se va a codificar el método `getPersonas`, el cual va a permitir la lectura (read) de todas las personas que tengamos desde nuestro repositorio de datos.
  
  Para ello, utilizaremos nuestro objeto repository y el método JPA findAll() de la siguiente manera:

  ```java
  // Implementación del método getPersonas en PersonaService

  @Override
  public List<Persona> getPersonas() {

    List<Persona> listaPersonas = persoRepository.findAll();
    return listaPersonas;

  }
  ```

<br>

- **PASO 5️⃣ – CREATE/ALTA**  
  
  En este paso se va a codificar el método `savePersona`, el cual va a permitir el alta (create) de cada persona que queramos agregar a nuestro repositorio de datos.  
  
  Para ello, utilizar el objeto `repository` y el método JPA `save()`, en donde se recibiren como parámetro un objeto `persona` (que a futuro provendrá del controller) de la siguiente manera:

  ```java
  // Implementación del método savePersona en PersonaService

  @Override
  public void savePersona(Persona perso) {
        persoRepository.save(perso);
  }
  ```

<br>

- **PASO 6️⃣ – DELETE/BAJA**  
  
  En este se va a codificar el método `deletePersona`, el cual va a permitir la baja (delete) de cada persona que se quiera eliminar completamente de nuestro repositorio de datos.

  Para ello, se utiliza el objeto `repository` y el método JPA `deleteById()`, en donde se recibe como parámetro la `id` de la persona a borrar de la siguiente manera:
  
  > Tener en cuenta que existen también otros métodos de eliminado en Hibernate pero vamos a elegir el más común y utilizado para este ejemplo

  ```java
  // Implementación del método deletePersona en PersonaService

  @Override
  public void deletePersona(Long id) {
        persoRepository.deleteById(id);
  }
  ```

<br>

- **PASO 7️⃣ – BÚSQUEDA**  
  
  En este paso se va a codificar el método `findPersona`, el cual va a poder buscar de manera individual una persona u objeto en nuestro repositorio de datos.

  Para ello, se utiliza el objeto `repository` y el método JPA `findById()`, en donde se reciben como parámetro la `id` de la persona a buscar/traer de la siguiente manera:

  ```java
  // Implementación de método findPersona en PersonaService

  @Override
  public Persona findPersona(Long id) {
        // aca si no se encuentra la persona, devuelve null por eso va "orElse"
        Persona perso = persoRepository.findById(id).orElse(null);
        return perso;
  }
  ```

<br>

- **PASO 8️⃣ – UPDATE/MODIFICACIÓN**  
  
  Para este paso primero se debe comprender cómo funciona la modificación con JPA + Hibernate.

  En otras implementaciones de JPA (como ser Eclipselink) existe un método dedicado a la edición llamado «edit»; sin embargo, en Hibernate no es así sino que se REUTILIZA el método JPA `save`.

  ¿Cómo funciona entonces la modificación? Para realizar la modificación se debe recibir desde el controller los nuevos datos del objeto que queremos modificar y su `id` original.  
  A partir de esto, se busca el objeto en cuestión mediante `find`, se modifican sus atributos por los nuevos (a nivel lógico mediante métodos sets) y luego se vuelven a guardar mediante `save`.

  Para ello, se puede crear en nuestra clase `IPersonaService` un método «`editPersona()`» que reciba los parámetros mencionados anteriormente y luego implementarlo en la clase `PersonaService` de la siguiente manera:

  ```java
  // Agregado de método editPersona en IPersonaService

  public interface IPersonaService {

        // método para traer todas las personas
          public List<Persona> getPersonas ();

        // método para dar de alta una persona
          public void savePersona (Persona perso);

        // método para borrar una persona
          public void deletePersona (Long id)

        // método para encontrar una persona
          public Persona findPersona (Long id)

        // método para editar una persona
          public void editPersona (Long idOriginal, Long idNueva,
                                   String nuevoNombre, String nuevoApellido,
                                   int nuevaEdad);

  }
  ```

  ```java
  // Método editPersona en PersonaService

  @Override
  public void editPersona (Long id_original, Long nuevaId, String nuevoNombre, String nuevoApellido, int nuevaEdad) {

    // ocupo this porque llamo al mismo método "findPersona" de esta clase
    Persona perso = this.findPersona(id_original);
    perso.setId(nuevaId);
    perso.setApellido(nuevoApellido);
    perso.setNombre(nuevoNombre);
    perso.setEdad(nuevaEdad);

    // ocupo this porque llamo al mismo método "savePersona" de esta clase
    this.savePersona(perso);
    
  }
  ```
  
  <br>
  
  Con la implementación de cada uno de los métodos en nuestra clase `PersonaService`, se tiene la lógica de negocio lista para llevar a cabo un CRUD completo.

  Ahora, es necesario configurar el `Controller` para poder recibir las solicitudes y llevar a cabo cada una de estas operaciones CRUD.

<br>

## 🏷️ Endpoints para operaciones CRUD en el Controller

Una vez lista toda la lógica de negocio, será necesario inyectar la dependencia de la clase controladora con la capa de servicio.

Para ello, se crea un objeto de `IPersonaService` y lo inyectaremos mediante `@Autowired`.

  ```java
  @RestController
  public class PersonaController {

      @Autowired
      private IPersonaService interPersona;
  ```

<br>

### ▫️¿Por qué inyectamos sobre la interfaz y no sobre la clase servicio en concreto?  
  
Esto se debe a que, en `IPersonaService` haremos cualquier agregado o modificación ante la aparición de nuevos métodos. Esto permite que, por más que aún no se hayan realizado modificaciones en la clase concreta de `Service`, se pueda tener acceso de igual manera a los métodos declarados en la interfaz en caso de ser necesario, entre muchas otras ventajas.

Una vez inyectada la dependencia, armaremos cada uno de los endpoints con los que vamos a recibir las solicitudes para luego llamar a cada servicio.  

Algunos ejemplos de cómo codificarlos se especifican a continuación:

```java  
# Endpoints creados en la clase controladora

// Endpoint para obtener todas las personas
@GetMapping("/personas/traer")
public List<Persona> getPersonas() {

    return interPersona.getPersonas();
}

// Endpoint para crear una nueva persona
@PostMapping("/personas/crear")
public String createStudent(@RequestBody Persona perso) {

    interPersona.savePersona(perso);
    // devuelve un string avisando si creó correctamente
    return "La persona fue creada correctamente";
}

// Endpoint para dar de baja una nueva persona
@DeleteMapping("/personas/borrar/{id}")
public String deletePersona(@PathVariable Long id) {

    interPersona.deletePersona(id);
    // devuelve un string avisando si eliminó correctamente
    return "La persona fue eliminada correctamente";
}

// Endpoint para modificar una persona
@PutMapping("/personas/editar/{id_modificar}")
public Persona editPersona(@PathVariable Long id_original,
          @RequestParam(required = false, name = "id") Long nuevaId,
          @RequestParam(required = false, name = "nombre") String nuevoNombre,
          @RequestParam(required = false, name = "apellido") String nuevoApellido,
          @RequestParam(required = false, name = "edad") int nuevaEdad) {

      // Envío id original (para buscar)
      // Envío nuevos datos para modificar
      interPersona.editPersona(id_original, nuevaId, nuevoNombre, nuevoApellido, nuevaEdad);

      // Busco la persona editada para mostrarla en la "Response"                
      Persona perso = interPersona.findPersona(id_origina);

      // Retorna la nueva persona
      return perso;
}
```

<br>

### ▫️¿Qué significan los required utilizados con `@RequestParam`?  

`RequestParam` tiene la posibilidad de incluir algunas indicaciones para los parámetros que se reciben en las solicitudes. `Required` nos permite identificar si un parámetro que recibimos es obligatorio (true) o no (false). En este caso, como no siempre vamos a editar todos los parámetros, ponemos todos como no requeridos. Por otro lado, mediante `name`, identificamos a cada uno de los parámetros para poder especificar su obligatoriedad o no.

### ▫️¿Qué son las nuevas anotaciones que aparecen?  
¿`@PutMapping`? ¿`@DeleteMapping`? Así como para las solicitudes GET y POST utilizamos `@GetMapping` y `@SetMapping`, para poder implementar los métodos DELETE y PUT (para bajas y modificaciones) tenemos las annotations `@DeleteMapping` y `@PutMapping`. Ambas pueden ser utilizadas en conjunto con `@PathVariable` o `@RequestParam`.

<br>

## 🏷️ Pruebas con POSTMAN

Finalmente, terminamos todas las configuraciones en nuestro proyecto para poder realizar solicitudes mediante Postman y ver qué obtenemos como respuesta.  

A continuación, vamos a entrar en detalle de cómo realizar cada una de las solicitudes utilizando cata método HTTP en particular.  

<br>

### 🔖 Prueba de ALTA
Daremos de alta una nueva persona, para ello en Postman seleccionaremos el método **POST**, incluiremos los datos de la nueva persona en el **body** mediante formato JSON y lo enviamos a nuestra aplicación. Si todo sale bien, la aplicación nos responderá el mensaje que parametrizamos y, al mismo tiempo, en nuestra base de datos tendremos un nuevo registro.

```json
# POSTMAN

POST  localhost:8080/personas/crear

// body
{
  "nombre" : "Yugi",
  "apellido" : "Moto",
  "edad" : "15"
}

"La persona fue creada correctamente"
```

```
# BASE DE DATOS
    
| id  | apellido | edad | nombre |
| --- | -------- | ---- | ------ |
|  1  |   Moto   |  15  |  Yugi  | 
```

Probemos ahora agregar más personas para poder contar con mayor cantidad de datos para probar las siguientes consultas. Para ello nos valdremos de dos personajes más.

```json
{
  "nombre" : "Seto",
  "apellido" : "Kaiba",
  "edad" : "17"
}
```
```json
{
  "nombre" : "Joey",
  "apellido" : "Wheeler",
  "edad" : "1"
}
```

<br>

### 🔖 Prueba de LECTURA de todas las personas

Para probar el endpoint que nos permite obtener la lista completa de personas, utilizaremos Postman y simularemos una solicitud **GET**. Si todo sale bien, obtendremos como resultado un JSON con todas las personas cargadas en la base de datos.

```json
[
  {
    "nombre" : "Yugi",
    "apellido" : "Moto",
    "edad" : "15"
  },
  {
    "nombre" : "Seto",
    "apellido" : "Kaiba",
    "edad" : "17"
  },
  {
    "nombre" : "Joey",
    "apellido" : "Wheeler",
    "edad" : "1"
  }
]
```

<br>

### 🔖 Prueba de BAJA de una persona

Para llevar a cabo la eliminación de una persona, realizaremos una request mediante postman y el método **HTTP DELETE**. Además de esto, indicaremos en la URL la `id` de la persona que queramos borrar. En este caso elegiremos la id 3.

```json
# POSTMAN

DELETE  localhost:8080/personas/borrar/3


La persona fue eliminada correctamente
```

Si volvemos a realizar una consulta **GET** para traer todas las personas, observaremos que la persona con id 3 ya no existe en la base de datos.

<br>

### 🔖 Prueba de MODIFICACIÓN de una persona

Supongamos que una de las personas tiene sus datos ingresados incorrectamente y queremos corregirlos. Para ello, simularemos una solicitud **UPDATE** mediante **POSTMAN**. Para solicitar la modificación a nuestra aplicación, debemos proporcionar la ``id``; este caso de ejemplo, modificaremos los datos de la persona 1.

Al utilizar Postman, es necesario especificar los nuevos parámetros en la pestaña «params», esto agregará los mismos de forma automática a la URL sin que tengamos que hacerlo manualmente. En la imagen a continuación, se ve como el resultado de la ``request`` es el objeto creado (tal cual como fue parametrizado en el endpoint).

```json
# POSTMAN

PUT  localhost:8080/personas/editar/1?nombre=Yami&apellido=Faraon&edad=16


// Pretty
{
    "id" : 1,
    "nombre" : "Yami",
    "apellido" : "Faraon",
    "edad" : "16"
}
```

<br>

Con todos estos pasos tendremos como resultado un ABML (CRUD) completo implementando Spring Boot + JPA +  Hibernate.

<br>

> ⚠️ **IMPORTANTE**  
> Si bien pudiste seguramente seguir todos los pasos para implementar un CRUD completo, existen muchas complicaciones y detalles a tener en cuenta a la hora de ir codificando. Es por ello que en el siguiente video, la profe replica el paso a paso para que puedas seguirla y verificar si todo quedó perfecto, para poder tener tu primer CRUD oficialmente realizado con Java + SpringBoot + JPA + Hibernate.