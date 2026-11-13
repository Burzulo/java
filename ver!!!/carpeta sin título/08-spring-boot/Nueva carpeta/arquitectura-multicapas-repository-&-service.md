# 📌 Arquitectura Multicapas: @Repository y @Service

### ▪︎ Annotations para Capas <br>
Como ya hemos notado a medida que fuimos aprendiendo Spring Boot, el framework se basa principalmente en el uso de annotations; es por ello que, al aplicar una arquitectura multicapas, más allá de realizar la correspondiente división de paquetes para mantener ordenada nuestra estructura, es necesario marcar de alguna manera cada una de las clases que pertenezcan a estas capas para que el Framework las reconozca.

Para ello se vale de 3 annotations:

	              @Component 
					
		   ↓           ↓           ↓
	  @Controller   @Service   @Repository
	       ↓            
	@RestController

En la imagen podemos ver `@Component`, el cual es una annotation para hacer referencia de forma genérica a cualquier annotation de Spring Boot.

La línea que nos interesa es la que podemos observar en color verde, donde podemos identificar la annotation para la capa `Controller`. Anteriormente se utilizaba `@Controller`, sin embargo, tal como se puede ver en la imagen, con las últimas actualizaciones del Framework, esta annotation se convirtió en `@RestController`.

Por otro lado nos encontramos con `@Repository` (para la capa repository) y `@Service` (para la capa service).

&nbsp;

## 🏷️ @Repository
`@Repository` es una anotación de Spring que indica que la clase anotada con ella es un repositorio de datos. Con esto no nos referimos a un repositorio como GitHub o GitLab, sino a un lugar donde se realiza el almacenamiento, manejo o administración de los datos con los que trabajará la aplicación, sea una base de datos, un archivo, etc.

Todas las clases de manejo de persistencia de datos deberán tener antes de su nombre la annotation `@Repository` y por convención, también el nombre de estas clases suele llevar dicha palabra incorporada.

Por ejemplo:

```java
@Repository
public class PersonaRepository {
    // contenido de la clase
}
```

Una ventaja de usar esta anotación es que tiene habilitada la traducción automática de excepciones de persistencia. Cuando se usa un marco de persistencia, por ejemplo: JPA con Hibernate, las excepciones nativas lanzadas dentro de las clases anotadas con `@Repository` se traducirán automáticamente en subclases de `DataAccessExeption` de Spring.

&nbsp;

## 🏷️ @Service
La capa service se encarga de llevar dentro la capa de la lógica de negocio de nuestra aplicación.

Si bien anteriormente estuvimos trabajando directamente en nuestro controller para lograr la devolución de datos y ejecución de métodos, a partir de ahora lo haremos en clases especiales que se van a encontrar en el paquete service. La pregunta ahora es… ¿Cómo vamos a identificar a estas clases que nos van a proporcionar la lógica de usuario? Y la respuesta es, mediante la annotation `@Service`.

`@Service` se usa de igual manera que `@Repository`. Cada clase dentro de nuestro paquete service debe de tener la annotation antes del nombre de la misma, como así también por convención (y buena práctica) se suele incluir la palabra service en el nombre de la clase.

Por ejemplo:

```java
@Service
public class PersonaService {
    // contenido de la clase
}
```

&nbsp;

### ▪︎ Implementación de capas mediante INTERFACES
Tanto nuestras clases `Service` como `Repository`, tendrán una gran cantidad de métodos que podremos implementar de diferentes maneras dependiendo de las funcionalidades que debamos desarrollar.

Dado esto, como buena práctica de utilización de capas y división de tareas, tanto la lista completa de métodos que tengamos para nuestras clases `Service` como para nuestras clases `Repository`, no estarán en sus clases concretas (por ejemplo `PersonaService` o `PersonaRepository`) sino, que se listarán en una interfaz (asociada a cada clase) que será implementada por cada una de las clases concretas en cuestión.

&nbsp;

Dicho esto… ¿Cómo hacemos esto? De la siguiente manera:

- **PASO 1️⃣**<br>
  Haremos el ejemplo con una clase de nuestra capa service (sin embargo, tener en cuenta que se debe aplicar lo mismo en las clases repository).

  Vamos a crear una clase llamada `PersonaService`, dentro del paquete (capa) service de nuestro proyecto y la vamos a dejar vacía.

  ```java
  @Service
  public class PersonaService {
       
  }
  ```

&nbsp;

- **PASO 2️⃣**<br>
  Crearemos una interfaz llamada `IPersonaService` (la I delante indica que es la interfaz asociada a nuestra clase creada anteriormente `PersonaService`).

  Dentro de esta interfaz vamos a declarar dos métodos: `crearPersona` y `traerPersonas`, pero SIN ESTABLECER SU IMPLEMENTACIÓN (tal y como se lleva a cabo en todas las interfaces):

  ```java
  public interface IPersonaService {
  public void crearPersona(Persona per);
  public List<Persona> traerPersonas ();
  
  }
  ```

&nbsp;

- **PASO 3️⃣**<br>
  Una vez terminada nuestra interfaz, vamos a ir a nuestra clase concreta `PersonaService` y vamos a implementar la interfaz anteriormente creada.

  Una vez implementada, podremos pasar a detallar la lógica en cuestión de cada uno de los métodos.

  ```java
  @Service 
  public class PersonaService implements IPersonaService {
    
      @Override
      public void crearPersona(Persona per) {
            // aquí se crea una persona
      }
    
      @Override
      public List<Persona> traerPersonas () {
            // aquí se buscan todas las personas a devolver
            return null;   // aqui devolverá la lista de personas (no null)
      }
  }
  ```

<br> Y la estructura de clases dentro del proyecto quedaría de esta manera:

    ▼ Source Packages
      ▶︎ com.miaplicacion.cursoSpringBoot
      ▼ com.miaplicacion.cursoSpringBoot.controller
         aplicacionController.java
      ▶︎ com.miaplicacion.cursoSpringBoot.dto
      ▼ com.miaplicacion.cursoSpringBoot.model
         Persona.java  
      ▶︎ com.miaplicacion.cursoSpringBoot.repository
      ▼ com.miaplicacion.cursoSpringBoot.service
         IPersonaService.java
         PersonaService.java