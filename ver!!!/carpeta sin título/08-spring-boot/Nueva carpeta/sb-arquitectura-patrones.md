# 📌 Arquitectura y Patrones

<br>

- [Patrón MVC](#-patron-mvc)
- [Arquitectura Multicapas](#-arquitectura-multicapas)

<br>

## 📂 Patron MVC

El **Model-View-Controller (MVC)** es un **patrón de diseño de software** que permite separar la **lógica de negocio**, la **interfaz de usuario** y el **control del flujo de datos** dentro de una aplicación. Esta separación mejora la organización, el mantenimiento y la escalabilidad del código.

En este patrón, el **usuario realiza una petición**, un **controlador** la recibe y decide qué acciones ejecutar, interactuando con el modelo y la vista según sea necesario.

<br>

El Modelo-Vista-Controlador organiza la aplicación en tres componentes:  

- El **Modelo** gestiona los datos y la lógica de negocio.  
- La **Vista** muestra la interfaz al usuario.  
- El **Controlador** maneja las peticiones del usuario.

  > En **Spring Boot**, los controladores (`@Controller` o `@RestController`) gestionan las rutas y devuelven vistas o respuestas JSON.

<br>

### ▫️ Componentes del patrón MVC

Cada una de las partes del patrón cumple con una funcionalidad en particular:

### 🔖 Controller

- Actúa como **intermediario** entre la vista y el modelo.  
- Recibe las órdenes del usuario, solicita los datos al modelo y los envía a la vista.  
- Funciona como un **pivote** que distribuye las tareas.  
- En **Spring Boot**, los controladores se definen mediante la Annotation `@RestController`.

### 🔖 Model

- Se encarga del **modelado de los datos** y de la **lógica de negocio**.  
- Generalmente incluye la conexión con bases de datos o fuentes de información externas.  
- Representa el núcleo funcional de la aplicación.

### 🔖 View

- Es la **interfaz gráfica** o el medio de presentación de los datos al usuario.  
- Recibe información del modelo a través del controlador y la muestra visualmente.

<br>

![mvc](https://github.com/Burzulo/MisNotas/blob/main/MisNotas/roadmap-java/imagenes/patron-mvc.png?raw=true)

<br>

El desarrollo **Backend** se centra principalmente en dos partes del patrón: el **Controlador** y el **Modelo**.

A nivel de código, el MVC se implementa en Java mediante una **división en capas** y una **distribución de responsabilidades**, lo que se conoce como **Arquitectura Multicapas**.

<br>

> ⚠️ **IMPORTANTE**  
> Este modelo es fundamental para el mantenimiento del sistema, ya que al estar separados los componentes, se puede identificar fácilmente dónde realizar modificaciones o correcciones sin afectar otras partes del proyecto.

<br>

## 📂 Arquitectura Multicapas

Toda aplicación que sigue **buenas prácticas de desarrollo de software**, cumple con algún tipo de modelo o **arquitectura de capas**, es decir, una **separación entre cada una de las partes con la que interactúa la misma y una forma de comunicación entre ellas**.

Existen diversos modelos o arquitecturas multicapa que pueden ser implementados según el proyecto sobre el cual se esté trabajando, sin embargo, hay algunas estandarizaciones a seguir que se adaptan a la mayoría de los desarrollos realizados en Java.

&nbsp;

A continuación, se especifica en mayor detalle cada una de las capas de una de las **arquitecturas multicapas estándar más utilizada** para el desarrollo de aplicaciones con Spring Boot.

- *Controller*: capa encargada de atender las solicitudes `http` entrantes, derivarlas a la capa que corresponda, esperar por una respuesta, generarla y transmitirla nuevamente al cliente. Generalmente la capa `Controller` trabaja estrechamente con la capa de `Service`, donde a partir de una `request` llama a las funciones que necesite de la capa service para generar una `response`.

- *Repository o DAO (Data Access Object)*: capa encargada de la **persistencia de los datos**, es decir, del resultado de la **interacción de modelado entre las clases desarrolladas y las tablas de una base de datos**. Permite el acceso a los datos mediante diferentes tecnologías como por ejemplo JDBC o algún ORM como JPA con Hibernate. Cada una de las clases que se encuentren dentro de esta capa deben estar mapeadas/etiquetadas mediante la annotation `@Repository`.

- *Model (o Entity)*: La capa «`model`» trabaja estrechamente en conjunto con la clase `Repository`. Cada una de las clases modela un objeto de la vida real y es marcado con la annotation `@Entity` en caso de que se transforme en una entidad (tabla) en la base de datos. **Cada instancia que se haga a una clase entity, en caso que sea persistida, representará una fila en una tabla de la base de datos**. Resumiendo acá van todas las clases estándares creadas que representen una entidad.

- *DTO (Data Transfer Object)*: capa que se encarga de contener todas las clases `DTO` que hayan sido especificadas en un proyecto. Los DTO buscan desacoplar la forma de presentación de los datos (a futuro en el frontend) con respecto a los objetos propiamente dichos de la capa `Model`.

- *Service*: La capa de `Service`, mejor conocida como lógica de negocio, es la capa donde **se especifican todas las funciones u operaciones de los métodos que sean necesarias** y que puedan ofrecer, como dice su nombre, un servicio a la capa `controller`. La capa `service`, por ejemplo, puede encargarse de las autenticaciones o de las políticas de autorización que puede tener la aplicación con respecto al acceso a determinadas funciones. 

  &nbsp;
  
  > ⚠️ **IMPORTANTE:**  
  > La separación en paquetes es solo EL PRIMER PASO para poder aplicar una buena práctica de desarrollo.

&nbsp;

```java
// Vista del proyecto (ejemplo) de ARQUITECTURA MULTICAPAS
     
▼ Source Packages
  ▶︎ com.miaplicacion.primerproyecto
  ▶︎ com.miaplicacion.primerproyecto.controller
  ▶︎ com.miaplicacion.primerproyecto.dto
  ▶︎ com.miaplicacion.primerproyecto.model
  ▶︎ com.miaplicacion.primerproyecto.repository
  ▶︎ com.miaplicacion.primerproyecto.service
```