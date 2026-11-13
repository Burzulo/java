#  📌 Configurando un proyecto con JPA + Hibernate

<br>

## 🏷️ @Configuración JPA + Hibernate
Conociendo ya los conceptos de JPA y su principal proveedor Hibernate, es posible implementar ahora una aplicación sencilla que represente un ABML (alta, baja, modificación y lectura).

Como resumen en primer lugar se trabaja con las siguientes herramientas:  
- Base de datos MySQL (adminsitrada con PHPMy admin). Se puede utilizar Wamp, Xampp Server o cualquier proveedor de MySQL.  
- IDE que contengan Maven integrado.  
- Spring Boot + Initializr  
- JPA + Hibernate  

<br>

- **PASO 1️⃣**  
  Ir a initializr y crear un nuevo proyecto Spring Boot teniendo en cuenta las siguientes dependencias. 
  
  > - Lombok
  > - Spring Boot DevTools
  > - Spring Web
  > - Spring Data JPA
  > - H2 Database
  > - MySQL Driver

  <br>

  Luego, abrirlo en el IDE con el que estemos trabajando y dejar descargar completamente las correspondientes dependencias mediante Maven.

<br>

- **PASO 2️⃣**  
  Crear una base de datos MySQL llamada `prueba_jpa` y asignar un usuario y contraseña con todos los privilegios, para ello, utilizar el servidor y gestor de preferencia. Asegurarse que la base de datos se encuentre totalmente vacía (sin ninguna tabla creada).  

  En este ejemplo se utiliza:

  > - Xampp Server (video de instalación disponible: https://youtu.be/pwTbAKRiRvA )
  > - Nombre base de datos: prueba_jpa
  > - Usuario: admin
  > - Contraseña: admin

<br>

- **PASO 3️⃣**  
  Debemos ir al archivo `application.properties` que initializr nos crea por defecto en nuestro proyecto.

   ```java
  ▼♨️ jpa Demo  
    ▼📁 Source Packages  
      ▼📁 com.example.jpaDemo
        📑 JpaDemoApplication.java  
       📁 com.example.jpaDemo.Controller
      ▼📁 com.example.jpaDemo.Model
        📑 Student.java  
       📁 com.example.jpaDemo.Repository  
       📁 com.example.jpaDemo.Service  
     🗂️ Test Packages   
    ▼📁 Other Sources  
      ▼📁 src/main/resources
        ▼📁 <default packages>  
          📑 application.properties // ⇐ este
         📁 static  
         📁 templates  
    📁 Dependencies  
   ```

  Y realizar las siguientes configuraciones:
  
  ```
  spring.jpa.hibernate.ddl-auto=update
  spring.datasource.url=jdbc:mysql://localhost:3306/prueba_jpa?useSSL=false&serverTimezone=UTC ⬅️
  spring.datasource.username=admin ⬅️
  spring.datasource.password=admin ⬅️
  spring.jpa.database-platform=org.hibernate.dialect.MySQL8Dialect
  ```
  
  El archivo `application.properties` permite establecer diversas configuraciones sobre una aplicación realizada con Spring Boot, en este caso está siendo utilizado para establecer los parámetros de la base de datos.

  Los parámetros que se configuran en este archivo (tal como se puede ver en la ilustración) son los siguientes:

  - `jpa.hibernate.ddl-auto` ⟹ establece la estrategia que utilizarán JPA y Spring para el manejo de tablas. Al colocar el valor en Update se establece que la estrategia será de actualización de tablas.

  - `datasource.url` ⟹ establece la dirección donde se encuentra alojada la base de datos.  
  Es de vital importancia en este apartado colocar correctamente el nombre de la base de datos (en este ejemplo `prueba_jpa`) y el puerto donde se encuentra levantada la misma (generalmente `3306` en bases de datos mysql). Por otro lado la especificación `?useSSL=false&serverTimezone=UTC` establecen que para la conexión no se utilizará SSL y que se tendrá en cuenta una zona horaria estándar para el servidor (esta configuración es de gran importancia para posibles errores en cuanto a diferencias de fecha y hora entre el servidor de base de datos y la aplicación).
  
  - `datasource.username` ⟹ se utiliza para parametrizar el nombre de usuario de la base de datos (configurado anteriormente en la misma).

  - `datasource.password` ⟹ se utiliza para parametrizar la contraseña asociada al nombre de usuario especificado anteriormente.

  - `spring.jpa.database-platform` ⟹ en este apartado se debe especificar el dialecto que se utilizará para comunicar la aplicación con la base de datos MySQL creada. Es importante tener en cuenta la versión del driver de MySQL que se esté utilizando en este momento, para ello, podemos verificar la misma en el archivo pom.xml tal como se ve en la ilustración:

    <br>
  
   ```xml
   # Dependencia del driver de MySQL

   <dependency>
         <groupId>mysql</groupId>
         <artifactId>mysql-connector-java</artifactId>
         <scope>runtime</scope>
   </dependency>
   ```

  > 💡 **NOTA**  
  > En caso de que en el archivo pom.xml no se especifique ninguna versión en particular, podemos tomar la más reciente. En este ejemplo utilizaremos la versión 8, mediante “org.hibernate.dialect.MySQL8Dialect”.

<br>

- **PASO 4️⃣**  
  - Ejecutar la aplicación.  
    > 💡 **NOTA**  
    > Antes de esto, asegurarse de que el servidor de la base de datos esté activo y ejecutándose.
  - Una vez ejecutada, intentar acceder a la url: http://localhost:8080/h2-console/  
  - Si todo funciona correctamente será posible visualizar una pantalla como la que se puede observar en la ilustración:

  ![h2-console](https://github.com/Burzulo/MisNotas/blob/main/MisNotas/roadmap-java/imagenes/h2-console.png?raw=true)

  H2, es una base de datos «lógica» y «embebida» (de alguna manera) que ofrece Spring para poder trabajar sobre ella sin la necesidad de tener un servidor de base de datos aparte. No será utilizada en este momento porque ya se cuenta con una base de datos MySQL creada, pero se hace referencia por ser una herramienta de gran ayuda.

<br>

- **PASO 5️⃣**  
  Una vez probada la correcta conexión con la base de datos, procederemos a crear una clase `Persona` mediante la cual realizaremos un ABML de prueba en próximas clases. Para ello, vamos a crear las siguientes clases/interfaces y realizaremos los correspondientes mapeos mediante las Annotations que vimos la clase pasada:

  - En la capa model: clase `Persona`.  
  - En la capa repository: interface `PersonaRepository`.  
  - En la capa service: clase `PersonaService`.
  
  <br>
  
  Asi deberían quedar:

  ```java
  // Clase Persona con sus mapeos JPA
  
  @Getter @Setter
  @Entity
  public class Persona {

    @Id
    @GeneratedValue(strategy=GenerationType.SEQUENCE)
    private Long Id;
    private String nombre;
    private String apellido;
    private int edad;
  }
  ```

  ```java
  // Interface PersonaRepository
  
  import com.jpa.pruebahibernate.model.Persona;
  import com.springframework.data.jpa.repository.JpaRepository;
  import com.springframework.stereotype.Repository;
  
  @Repository // mapeamos como repositorio
  // la interface extinede de JpaRepository (que maneja repositorios JPA) 
  // en los parámetros <> deben ir: <clase a persistir, tipo de dato de su ID>
  public interface PersonaRepository extends JpaRepository <Persona, Long> {

  }
  ```

  ```java
  // Clase PersonaService
  
  public class PersonaService {

    @Autowired
    private PersonaRepository persoRepository;

  }
  ```

<br>

- **PASO 6️⃣**  
  A partir de la correcta creación de la clase de secuencias de Hibernate y de la clase `Persona`, es posible llevar a cabo los métodos correspondientes para lograr un CRUD (ABML en español).

  Para ello, es necesario configurar los servicios que tendrá disponible la aplicación, para lo cual se deberá crear una interface `IPersonaService` la cual contendrá los métodos necesarios para el ABML SIN IMPLEMENTARLOS (dado que es una interfaz).

  Como resultado de este paso, es posible ejecutar la aplicación y la misma, mediante JPA, deberá crear dos tablas:

  - La tabla persona
  - La tabla hibernate_sequence (para el manejo de las secuencias de las ids)

  <br>

  Una vez llevados a cabo todos estos pasos ya contamos con la base necesaria para proceder a la implementación de cada uno de los métodos que nos van a permitir realizar los correspondientes ABML (altas, bajas, modificaciones y lecturas).