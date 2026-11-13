# 📌 Infraestructura y Conceptos

<br>

- [Spring Framework](#-spring-framework)
- [Gestión de Dependencias](#-gestión-de-dependencias)

<br>

## 📂 Spring Framework

Spring Framework es un conjunto de proyectos de código abierto desarrollados en Java con el objetivo de agilizar el desarrollo de aplicaciones en este lenguaje. Todo su pack de aplicaciones es conocido como **Spring platform** e incluye herramientas para el desarrollo web, microservicios, manejo de base de datos, seguridad, entre otros.

Entre los principales proyectos se encuentran:

- **Spring Boot** → Facilita la creación y configuración inicial de proyectos de Spring para generar aplicaciones de fácil y rápida puesta en marcha.  
- **Spring Data** → Utilizado para la administración, manejo y comunicación con bases de datos, tanto relacionales como no-relacionales.  
- **Spring Security** → Utilizado para las cuestiones de seguridad que puede necesitar todo proyecto.  
- **Spring Web Services** → Utilizado para facilitar el desarrollo de Web Services SOAP.

<br>

La lista completa de todos los proyectos de Spring está disponible en el siguiente enlace:
  >📚 **Documentación oficial:**  
  > 🔗 [https://spring.io/projects](https://spring.io/projects)

<br>

### 🔖 Spring Framework vs Spring Boot

**Spring Boot** es una **extensión de Spring Framework** y se encuentra dentro de su lista de proyectos. Este fue creado con la *finalidad de facilitar la creación de aplicaciones web* listas para salir a producción, es decir, bajo el concepto *«Just Run»* (solo ejecutar).

Anteriormente, realizar las configuraciones iniciales para llevar a cabo una aplicación en Spring llevaba mucho tiempo a los desarrolladores. Esto, se realizaba mediante una configuración manual de un ``archivo xml`` y de un **servidor de aplicaciones web**, consumiendo gran parte del tiempo de desarrollo del proyecto en realizar configuraciones.

Dada esta problemática y con la finalidad de resolverla, fue desarrollado Spring Boot, que requiere una configuración mínima y que puede ser integrado con otros proyectos de Spring o librerías externas.

<br>

## 📂 Gestión de Dependencias

En el desarrollo profesional, rara vez se escribe todo el código desde cero; los desarrolladores se suelen apoyar en librerías externas (como Hibernate o Spring).

<br>

### 🔖 Maven

Maven es una herramienta que se creó para simplificar los procesos de **build** (compilar y generar ejecutables a partir del código fuente), librando de todas las dificultades que hay por detrás.

> Antes que Maven proporcionara una interfaz común para hacer builds del software, los desarrolladores tenían que perder tiempo en aprender las peculiaridades de cada nuevo proyecto en el que participaban. Si querían compilar y generar ejecutables de un proyecto, tenían que analizar qué partes de código se debían compilar, qué librerías utilizaba el código, dónde incluirlas, qué dependencias de compilación había en el proyecto …

Maven es capaz de gestionar un proyecto software completo, desde la etapa en la que se comprueba que el código es correcto, hasta que se despliega la aplicación, pasando por la ejecución de pruebas y generación de informes y documentación.

#### ▫️ ¿Cómo funciona Maven?

La unidad básica de trabajo en Maven es el llamado **Modelo de Objetos de Proyecto** conocido simplemente como ``POM`` (en inglés: Project Object Model).

Se trata de un archivo XML llamado ``pom.xml`` que se encuentra por defecto en la raíz de los proyectos y que contiene toda la información del proyecto. Este archivo describe las dependencias del proyecto, el proceso de compilación y otra información importante. Cuando se ejecuta una compilación de Maven, Maven lee el archivo ``pom.xml`` y lo utiliza para determinar qué se debe hacer.

<br>

### 🔹 Dependencias

Una de las características claves es su sistema de *gestión de dependencias*. Cuando se especifica una dependencia en el archivo ``pom.xml`` Maven la descargará automáticamente de un repositorio central de Maven o uno local y la añadirá al classpath del proyecto, de esta forma gestiona las librerias externas.

Esto permite ahorrar mucho tiempo y esfuerzo en comparación con descargar e instalar manualmente las dependencias.

````java
// ejemplo archivo .xml

<project>
  <modelVersion>4.0.0</modelVersion>
  <groupId>es.campus</groupId>d>
  <artifactId>demo</artifactId>
  <version>1.0</version>
  <!-- Dependencias -->
     ....

</project>
````

Los 4 primeros nodos son los **únicos** obligatorios y definen respectivamente el modelo de objetos que utilizará Maven, esto es lo mínimo que debe incluir el archivo.

Cada librería en el mundo Maven se identifica por tres coordenadas: ``groupId`` (quién la hizo), ``artifactId`` (nombre del proyecto) y ``version``.

<br>

### 🔹 Empaquetado

El empaquetado es el proceso de transformar el código fuente (``.java``) en un archivo distributivo que otros puedan usar o ejecutar.

<br>

> 💡 **NOTA**  
> Maven se usa principalmente en proyectos Java, donde es muy común ya que está escrita en este lenguaje. De hecho, frameworks Java como *Spring* y *Spring Boot* la utilizan por defecto.


--- 
!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!

hay una separación clara entre el código (archivos .java) y los recursos (archivos .fxml, imágenes, estilos .css).

La regla de oro en Maven es:

````src/main/java: Solo archivos .java (Controladores, Modelos, Lógica).  ````

````src/main/resources: Solo archivos no-java (Vistas FXML, Imágenes, CSS, Configuración).````