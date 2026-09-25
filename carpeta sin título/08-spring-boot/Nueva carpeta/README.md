# Spring Boot

<br>

## 🌿 Spring Boot Core

- **Infraestructura y Conceptos:** [⇒](infraestructura-conceptos.md)
  - Ecosistema Spring: *Spring Framework* vs. *Spring Boot*
  - ❌ Gestión de Dependencias con *Maven*: El *`pom.xml`*, dependencias y empaquetado (JAR)

- **Principios de Diseño (IoC/DI):**
  - Inversión de Control (IoC)
  - Inyección de Dependencias (DI)
    - Mediante *`Constructor`* y *`Setter`*
    - Mediante *`@Autowired`*
    - Resolución de Ambigüedad: *`@Primary`* y *`@Qualifier`*

- **Arquitectura y Patrones:** [⇒](arquitectura-patrones.md)
  - Patrón MVC
  - Arquitectura Multicapas -- teoría

- [❌] **Configuración del Framework:**
  - Rol de `@SpringBootApplication`, Component `Scanning`
  - Configuración Externa: `application.properties/yml` (perfiles y variables de entorno).

<br>

## 🗄️ Persistencia de Datos con JPA e Hibernate

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

<br>

---

## 🌐 Desarrollo de API REST y Calidad

- **Capa de Controladores (REST):** [⇒](api-controladores.md)
  - API REST – Introducción
  - Concepto de JSON
  - ❌ *`@RestController`*: El controlador MVC adaptado a datos
  - Mapeo de rutas: *`@RequestMapping`*
  - Anotaciones de Métodos HTTP: *`@GetMapping`*, *`@PostMapping`*, *`@PutMapping`*, *`@DeleteMapping`*

- **Comunicación y Flujo de Datos:** [⇒](comunicacion-flujo.md)
  - Manejo de datos en Endpoints: *`@PathVariable`*, *`@RequestParam`*, *`@RequestBody`*, *`❌ @RequestHeader`*
  - Patrón DTO (Data Transfer Object)
  - ❌ Respuestas profesionales: Uso de *`ResponseEntity`* y códigos de estado HTTP

- **Robustez y Calidad:** [⇒](robustez-calidad.md)
  - ❌ Validación de datos: Uso de *`@Valid`* y anotaciones de restricción
  - ❌ Manejo Global de Excepciones: *`@RestControllerAdvice`* y *`@ExceptionHandler`*
  - Pruebas de integración: Uso de **Postman** para testing de endpoints

---

- Primer proyecto en Spring Boot

<br>

<br>

<br>

> ▶️📚 **links**  
> [Pagina oficial de Spring Boot](https://spring.io/)