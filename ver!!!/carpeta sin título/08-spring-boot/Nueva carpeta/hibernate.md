#  📌 Hibernate

Hibernate es un servicio **ORM de persistencia y consultas a bases de datos implementado para Java**.  
No se trata de una herramienta o servicio aparte, sino de una implementación o **proveedor de JPA**, trabajando de forma conjunta y complementaria con esta API.

El principal objetivo de Hibernate es **mapear las clases del modelo de datos** de una aplicación y asociarlas con las tablas de una base de datos, utilizando **annotations** para definir las reglas de mapeo.

&nbsp;

## Anotaciones más comunes en Hibernate

A continuación se presentan las anotaciones más utilizadas, junto con su función y uso habitual.

### 🏷️ `@Entity`
Mapea todas las clases que se convertirán en entidades en la futura base de datos. <br>
Por lo tanto `@Entity` indica que una clase Java representa una **entidad persistente**, es decir, una *tabla en la base de datos*.

### 🏷️ `@Table`
Se utiliza junto con `@Entity`.  
Permite **asociar la entidad con una tabla específica** en la base de datos o definir el nombre de la tabla.  
Si no se usa, JPA toma el **nombre de la clase** como nombre de la tabla.

```java
@Entity
@Table(name = "clientes")
public class Cliente { ... }
```

### 🏷️ `@Id`
Define el campo que actuará como **clave primaria (Primary Key)** en la base de datos.

### 🏷️ `@GeneratedValue`

Se usa junto a `@Id` para definir cómo se generará el valor de la clave primaria.  
Principales estrategias de generación automática de secuencias:

- **`AUTO`** → Estrategia por defecto. Hibernate decide la mejor forma según la base de datos.  
 Pensada principalmente para ids numéricas.

- **`IDENTITY`** → Generalmente autoincremental. Usada para claves primarias ya existentes en una base de datos por las cuales Hibernate debe guiarse para continuar la secuencia.

- **`SEQUENCE`** → Genera secuencias numéricas personalizables.  
  De forma automática hace el incremento de 1 en 1, pero puede ser personalizada según sea necesario.

- **`TABLE`** → Usa una tabla auxiliar para manejar la generación de IDs.

  ```java
  // ejemplo 

  @Id
  @GeneratedValue(strategy = GenerationType.IDENTITY)
  private Long id;
  ```

### 🏷️ `@Column`
Mapea un atributo de la clase con una **columna** de la tabla.  
Es opcional: si no se especifica, JPA usa el nombre del atributo como nombre de la columna.  
Es una annotation principalmente pensada para el mapeo de atributos sobre columnas de tablas en bases de datos ya existentes.

```java
@Column(name = "nombre_cliente", nullable = false)
private String nombre;
```

### 🔗 Relaciones entre entidades
Hibernate permite mapear distintos tipos de **relaciones** entre clases (tablas relacionales), los cuales se traducirán a nivel de base de datos como relaciones entre tablas:

- `@OneToOne` → Relación uno a uno.  
- `@OneToMany` → Relación uno a muchos.  
- `@ManyToOne` → Relación muchos a uno.  
- `@ManyToMany` → Relación muchos a muchos.  

  ```java
  // Ejemplo

  @OneToMany(mappedBy = "cliente")
  private List<Pedido> pedidos;
  ```

### 🏷️ `@JoinColumn`
Define la **columna que actuará como clave foránea (foreign key)** para realizar uniones (*joins*) entre tablas.

```java
@ManyToOne
@JoinColumn(name = "cliente_id")
private Cliente cliente;
```

&nbsp;

### ▫️Conclusiones

Hibernate es un **proveedor de JPA potente y flexible**, ampliamente utilizado en el ecosistema Java.  
No es necesario memorizar todas sus anotaciones, pero sí comprender su función y saber cómo consultarlas en la documentación oficial.

> 📚 **Documentación oficial:**  
> 🔗 [https://hibernate.org/orm/documentation/6.0/](https://hibernate.org/orm/documentation/6.0/)

💡 *Hibernate también incluye su propio lenguaje de consultas llamado **HQL (Hibernate Query Language)**, diseñado para trabajar con entidades en lugar de tablas SQL.*