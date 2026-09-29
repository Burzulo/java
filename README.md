# Mi Roadmap Java

<br>

- [Fundamentos y Java Esencial](...)  🚧 en CONSTRUCCION !!!!

<br>

## ✧ Fundamentos y Java Esencial

- **Lógica de Programación y Algoritmos** [⇒](./..)
  - ❌ Descomposición de problemas
  - ❌ Ejercicios: promedio, par/impar, ordenación

- **Configuración del Entorno** [⇒](./..)
  - Arquitectura Java: Diferencias y rol de la **JVM**, **JRE** y **JDK**
  - Ciclo de vida del código: Compilación (`javac`) vs. Ejecución (`java`)
  - Instalación y verificación del JDK
  - Configuración del IDE: IntelliJ IDEA y sus atajos
  - Inspección de código: Debugging básico (breakpoints)

- **Sintaxis Básica de Java** [⇒](./..)
  - Estructura mínima: `class`, método `main` (`public static void main(String[] args)`)
  - Convenciones de nomenclatura (`camelCase`, `PascalCase`, `UPPER_SNAKE_CASE`)
  - Comentarios

- **Tipos de Datos y Variables** [⇒](./..)
  - Tipos primitivos (`int`, `double`, `boolean`, `char`) y de referencia (`String`)
  - Declaración, inicialización y ámbito (*scope*)
  - Constantes: Uso de la palabra clave `final`
  - Conversión de tipos (*Casting* implícito y explícito)

- **Entrada/Salida Estándar (I/O)** [⇒](./..)
  - Uso de la clase `Scanner`
  - Salida de datos formateada: `System.out.println` y `System.out.printf`

- **Estructuras de Control** [⇒](./..)
  - Condicionales: `if`, `else if`, `else`, `switch`
  - Bucles: `for`, `while`, `do-while`
  - Transferencia de control: `break`, `continue` y `return`

- **Métodos y Alcance** [⇒](./..)
  - Declaración y firma de métodos (`static`, tipo de retorno y nombre)
  - Paso de parámetros y uso de la sentencia `return`
  - Sobrecarga de métodos (*Overloading*)
  - Ámbito de variables (*Scope*): Variables locales vs. Atributos de clase

- **Arrays** [⇒](./..)
  - Declaración, creación con `new` e inicialización de índices
  - Recorrido: Bucle `for` tradicional y bucle `for-each`
  - Algoritmos clásicos: Búsqueda lineal y ordenación manual
  - Inspección de datos: Uso de `Arrays.toString()` para *debugging*

- **Strings y StringBuilder** [⇒](./..)
  - Métodos indispensables de `String` (`length()`, `charAt()`, `substring()`, `toLowerCase()`, etc.)
  - Comparación de texto: Diferencia entre `==` y `.equals()` / `.equalsIgnoreCase()`
  - Concepto de inmutabilidad en cadenas de texto
  - Construcción eficiente de texto mediante `StringBuilder`

- **Excepciones** [⇒](./..)
  - Jerarquía de errores: `Throwable`, `Error`, `Exception`
  - Tipos de Excepciones: Checked vs Unchecked
  - Bloques de control: `try`, `catch`, `finally`
  - Flujo y propagación: `throw` vs `throws`
  - Creación de Excepciones Personalizadas

- ❌ **Herramientas Esenciales

Terminal: cd, ls, mkdir
Git: init, add, commit, push, pull, branch, merge
GitHub: creación de repositorios, pull requests, clonación







--- 

## ✧ Entornos de Desarrollo

- **IntelliJ IDEA** [⇒](./entorno-desarrollo/id-intellij.md)
  - Atajos de teclado

- **Eclipse** [⇒](./entorno-desarrollo/id-eclipse.md)
  - Atajos de teclado

<br>

## ✧ Java Standard Edition

- **Variables y Memoria** [⇒](./java-se/jse-variable-memoria.md)
  - Variables y Tipos Primitivos: `int`, `double`, `boolean`, `char`, ...
  - Casting: Conversiones implícitas y explícitas
  - Wrappers: Autoboxing y Unboxing
  - ❌ Constantes: Uso de la palabra clave `final`
  - ❌ El String Pool: Inmutabilidad de la clase `String`

- **Operadores** [⇒](./java-se/jse-operadores.md)
  - Aritméticos, Unarios, Relacionales y Lógicos
  - Ternario

- **Estructuras de Datos Estáticas (Arrays)** [⇒](./java-se/jse-arrays.md)
  - Arrays Unidimensionales y Multidimensionales
  - Propiedad ``lenght``
  - Recorrido: Uso de ``for`` tradicional vs. ``for-each``
  - Utilidades del Sistema: Clase ``java.util.Arrays`` (métodos `sort`, `fill`, `equals`, `toString`)

<br>

## ✧ Programacion Orientada a Objetos

- **Fundamentos de Clases y Objetos** [⇒](./java-poo/poo-clases-objetos.md)
  - Conceptos: Clase y Objeto (ciclo de vida e instanciación `new`)
  - Miembros de una clase: Atributos y Métodos
  - Constructores: Por defecto, parametrizados y el rol de `this`
  - ❌ Modificador `static`: Atributos y métodos de clase

- **Gestión de Memoria** [⇒](./java-poo/poo-gestion-memoria.md)
  - El modelo *Stack* vs. *Heap*
  - El rol del *Garbage Collector*

- **Encapsulamiento** [⇒](./java-poo/poo-encapsulamiento.md)
  - Modificadores de acceso: `public`, `private`, `protected`, `default`
  - Uso de *getters / setters*

- **Abstracción** [⇒](./java-poo/poo-abstraccion.md)
  - Clases abstractas
  - Métodos Abstractos

- **Herencia** [⇒](./java-poo/poo-herencia.md)
  - Jerarquías (`extends`)
  - `super`
  - Sobreescritura (`@Override`) y Sobrecarga de métodos

- **Polimorfisimo** [⇒](./java-poo/poo-polimorfismo.md)
  - Casting de objetos: `upcasting` \ `downcasting`
  - Operador `instanceof`  

- **Relaciones entre Clases** [⇒](./java-poo/poo-relaciones-entre-clases.md)
  - Asociación
  - Agregación
  - Composición

- **Interfaces** [⇒](./java-poo/poo-interfaces.md)
  - Declaración de Contratos (`implements`)
  - Métodos `default`, `static` y `private`
  - Comparativa: Clases abstractas vs. Interfaces

- **Genéricos** [⇒](./java-poo/poo-genericos.md)
  - El concepto de tipo parametrizado `<T>`

- **Java Collections Framework**
  - Jerarquía de la API: Interface `Collection` vs. `Map`
  - Listas: `ArrayList` vs. `LinkedList`
  - Conjuntos: `HashSet`, `LinkedHashSet` y `TreeSet` para evitar duplicados
  - Mapas: `HashMap` y `TreeMap` (almacenamiento clave-valor)
  - ❌ Ordenación: Interfaces `Comparable` y `Comparator`

- **Manejo de Excepciones** [⇒](./java-poo/poo-excepciones.md)
  - Jerarquía de errores: `Throwable`, `Error` vs `Exception`
  - Bloques de control: `try`, `catch`, `finally`
  - Flujo de Excepciones: `throw` vs `throws`
  - ❌ Creación de Excepciones Personalizadas

<br>

## ✧ Java Web

- [Índice ⇒](...)  🚧 en CONSTRUCCION !!!!

<br>

## ✧ Programación Funcional

- [Índice ⇒](...)  🚧 en CONSTRUCCION !!!!

<br>

## ✧ Spring Boot

### Fundamentos y Contenedor de Spring (Core)

- **Ecosistema e Infraestructura:** [⇒](./08-spring-boot/sb-infraestructura-conceptos.md)
  - Ecosistema Spring: *Spring Framework* vs. *Spring Boot*
  - ❌ Gestión de Dependencias (Maven): Análisis del `pom.xml` y empaquetado `JAR`.

- **El Contenedor de Inversión de Control (IoC):** [⇒](./08-spring-boot/sb-inversion-de-control.md)
  - ❌ Concepto de Beans y Application Context.
  - Inyección de Dependencias (DI): mediante `Constructor`, `Setter` y `@Autowired`
  - Resolución de Ambigüedad: `@Primary` y `@Qualifier`

- **Configuración del Proyecto:**
  - ❌ `@SpringBootApplication` y el proceso de *Component Scanning*.
  - ❌ Externalización: `application.properties` / `yml`, perfiles y variables de entorno.

### Arquitectura y Lógica de Negocio

- **Patrones de Diseño de Software:**
  - ❌ Patrón **MVC** (Model-View-Controller) en profundidad.
  - ❌ Arquitectura **Multicapas** (Theory): Controller -\> Service -\> Repository.

- **Capa de Servicio (Business Logic):**
  - ❌ Implementación con `@Service`.
  - ❌ Manejo de la lógica de negocio y transaccionalidad básica.

- **Productividad:**
  - ❌ **Lombok**: Limpieza de código en Entidades y DTOs (`@Data`, `@Builder`, etc.).

### Acceso a Datos (Persistencia con JPA/Hibernate)

- **Mapeo Objeto-Relacional (ORM):**
  - ❌ JPA vs. Hibernate: Estándar vs. Implementación.
  - ❌ Definición de Entidades: `@Entity`, `@Id`, `@GeneratedValue`.
  - ❌ Mapeo de Relaciones: `@OneToOne`, `@OneToMany`, `@ManyToMany`.

- **Spring Data JPA:**
  - ❌ Jerarquía de Repositorios: `CrudRepository` y `JpaRepository`.
  - ❌ *Query Methods*: Creación de consultas mediante nombres de métodos.
  - ❌ Ciclo de vida de una Entidad (Persistence Context).

### Desarrollo de APIs REST

- **Endpoints y Protocolo HTTP:**
  - ❌ Principios REST y formato JSON.
  - ❌ `@RestController` y el uso de `@ResponseBody`.
  - ❌ Mapeo de Rutas y Verbos: `@GetMapping`, `@PostMapping`, `@PutMapping`, `@DeleteMapping`.

- **Captura y Transformación de Datos:**
  - ❌ Parámetros: `@PathVariable`, `@RequestParam`, `@RequestBody`, `@RequestHeader`.
  - ❌ **Patrón DTO (Data Transfer Object)**: Separación de la entidad del modelo de entrada/salida.

- **Respuestas y Protocolo:**
  - ❌ Uso de `ResponseEntity` para el control de Status Codes (200, 201, 404, 500).

### Calidad, Validación y Robustez

- **Validación de Datos:**
  - ❌ Bean Validation: `@Valid` y anotaciones `@NotNull`, `@Size`, `@Email`.

- **Tratamiento de Errores:**
  - ❌ Manejo Global de Excepciones: `@RestControllerAdvice` y `@ExceptionHandler`.

- **Testing y Herramientas:**
  - ❌ Pruebas manuales de Endpoints con **Postman**.
  - ❌ Introducción a la documentación con **Swagger / OpenAPI**.

-----
EL INDICE DE ARRIBA VA
¿

### 🏷️ Spring Boot Core



- **Arquitectura y Patrones:** [⇒](sb-arquitectura-patrones.md)
  - Patrón MVC
  - Arquitectura Multicapas -- teoría

- [❌] **Configuración del Framework:**
  - Rol de `@SpringBootApplication`, Component `Scanning`
  - Configuración Externa: `application.properties/yml` (perfiles y variables de entorno).

<br>

### 🏷️ Persistencia de Datos con JPA e Hibernate

- **Capa de Datos y Negocio (Implementación):** ⇒
  - Implementación de @Service (Lógica) y @Repository (Acceso a datos)
  - Uso de Lombok: Productividad en Entidades y DTOs (@Data, @Builder)

- **ORM y Mapeo de Entidades:** ⇒
  - Concepto de ORM y JPA (Java Persistence API)
  - Hibernate: Mapeo de Entidades (@Entity, @Id, @GeneratedValue)
  - Estado de los objetos: Domain Object vs Entity
  - Relaciones: @OneToOne, @OneToMany, @ManyToOne, @ManyToMany

- Spring Data JPA: ⇒
  - Jerarquía: CrudRepository vs JpaRepository
  - Métodos automáticos del repositorio (CRUD)
  - Configuración y creación de un proyecto con persistencia real

---

- **Arquitectura Multicapas:** -- implementacion practica *`@Repository`* y *`@Service`* – 
- **Lombok**  
  - [❌] Uso en entidades (para getters, setters, constructores)
  - [❌] Uso en DTOs (*`@Data`*, *`@Builder`*)
- **Introducción a ORM + JPA **
- [❌] Objeto Modelo (Entity) y su Estado (Domain Object).
- Motor JPA: Hibernate – Annotations (``@Entity``, ``@Id``, ``@GeneratedValue`` ... )
- [❌] Spring Data JPA: Jerarquía de Repositorios:
  - [❌] CrudRepository (La interfaz base y sus métodos).
  - [❌] JpaRepository (Extensión y métodos avanzados para simplificación del CRUD).
- Relaciones con JPA + Hibernate: *`@OneToOne`*, *`@OneToMany`*, *`@ManyToMany`*
- Configurando un proyecto con JPA + Hibernate
- Creando un CRUD con JPA + Hibernate

---

### 🏷️ Desarrollo de API REST y Calidad

- **Capa de Controladores (REST):** [⇒](sb-api-controladores.md)
  - API REST – Introducción
  - Concepto de JSON
  - ❌ *`@RestController`*: El controlador MVC adaptado a datos
  - Mapeo de rutas: *`@RequestMapping`*
  - Anotaciones de Métodos HTTP: *`@GetMapping`*, *`@PostMapping`*, *`@PutMapping`*, *`@DeleteMapping`*

- **Comunicación y Flujo de Datos:** [⇒](sb-comunicacion-flujo.md)
  - Manejo de datos en Endpoints: *`@PathVariable`*, *`@RequestParam`*, *`@RequestBody`*, *`❌ @RequestHeader`*
  - Patrón DTO (Data Transfer Object)
  - ❌ Respuestas profesionales: Uso de *`ResponseEntity`* y códigos de estado HTTP

- **Robustez y Calidad:** [⇒](sb-robustez-calidad.md)
  - ❌ Validación de datos: Uso de *`@Valid`* y anotaciones de restricción
  - ❌ Manejo Global de Excepciones: *`@RestControllerAdvice`* y *`@ExceptionHandler`*
  - Pruebas de integración: Uso de **Postman** para testing de endpoints


## ✧ Microservicios

- [Índice ⇒](...)  🚧 en CONSTRUCCION !!!!

## ✧ Seguridad

- [Índice ⇒](...)  🚧 en CONSTRUCCION !!!!

## ✧ Testing

- [Índice ⇒](...)  🚧 en CONSTRUCCION !!!!

## ✧ Deploy

- [Índice ⇒](...)  🚧 en CONSTRUCCION !!!!

## ✧ Patrones de Diseño

- [Índice ⇒](...)  🚧 en CONSTRUCCION !!!!

## ✧ Spring IA

- [Índice ⇒](...)  🚧 en CONSTRUCCION !!!!

## ✧ Herramientas Complementarias

- [Índice ⇒](...)  🚧 en CONSTRUCCION !!!!