#  📌 ORM - Introducción
Uno de los aspectos más importantes al desarrollar aplicaciones web es **cómo almacenar y manejar los datos** que utiliza la aplicación.

Existen diferentes formas de hacerlo: desde el uso directo de **JDBC**, hasta el empleo de herramientas más avanzadas conocidas como **ORM** (*Object Relational Mapping* o *Mapeo Objeto-Relacional*).<br>
Los ORM facilitan la tarea de **vincular las clases de Java con las tablas de una base de datos**, evitando la necesidad de escribir consultas SQL manualmente en la mayoría de los casos.

Además, un ORM permite trabajar con los datos **como objetos Java**, simplificando la lógica de negocio y haciendo que el código sea **más legible, mantenible y portable** entre distintos motores de base de datos.

<br>

## 🏷️ JPA (Java Persistence API)
JPA, o mejor conocida por sus siglas **«Java Persistence API»**, es una colección de clases y métodos que tienen como objetivo lograr la **persistencia de datos** entre una aplicación desarrollada en Java y una base de datos.<br>

Su objetivo principal es lograr la **persistencia de datos** entre una aplicación desarrollada en Java y una base de datos, **sin depender directamente de SQL** o de un proveedor específico.

> ⚠️ **IMPORTANTE**  
> Cabe destacar, que **JPA no es un framework, sino una API** como tal que brinda sus servicios y herramientas para poder ser implementados.

<br>

### ▫️ ¿Qué busca JPA?
JPA, como todo ORM, busca **traducir el modelo de las clases Java a un modelado relacional** en una base de datos.<br>
Esto permite al programador decidir **qué clases u objetos persistir, cómo hacerlo, y de qué manera serán representados** en la base de datos (nombres, tipos de datos, relaciones, etc.).

Para lograrlo, JPA utiliza **mapeos mediante annotations** (`@Entity`, `@Table`, `@Column`, `@Id`, etc.), aplicadas sobre los elementos de las clases.<br>
De esta forma, **JPA actúa como un traductor** entre el mundo de los objetos (Java) y el mundo relacional (SQL).

Un ejemplo del proceso general seria:

```
Aplicaciones Java ⟹ JPA + Proveedor de JPA ⟹ BD
```

<br>

### ▫️ Proveedores de JPA
JPA no funciona por sí misma, sino que necesita un **«Proveedor de JPA»**, es decir, una implementación concreta que ejecute las operaciones de persistencia. <br>
Estos proveedores ofrecen las herramientas y annotations necesarias para interactuar correctamente entre las aplicaciones y las bases de datos. <br>

Entre los más conocidos se encuentran:

- EclipseLink  
- *Hibernate* (el más popular, flexible y eficiente)

    > Por su alto rendimiento, flexibilidad y compatibilidad con Spring Boot, Hibernate es uno de los favoritos de la comunidad Java.