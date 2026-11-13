# 📌 Encapsulamiento

<br>

- [Modificadores de Acceso](#-encapsulamiento--acceso)
- [Getters & Setters](#-patrón-getters--setters)

<br>

## 📂 Encapsulamiento & Acceso

Es una propiedad que permite **ocultar los detalles internos de una clase** y **proporcionar acceso controlado** a sus atributos y métodos, mediante palabras reservadas llamadas «modificadores de acceso».  
Esto permite ocultar la complejidad interna de una clase y mejora la seguridad e integridad de los datos.

### ✧ Modificadores de Acceso

- `public`  
Es el modificador de acceso más abierto y utilizado. Los miembros (atributos, métodos, constructores) declarados como públicos son **accesibles desde cualquier clase y paquete**.  
Pueden ser utilizados por cualquier objeto que tenga acceso a la clase.

- `private`  
Es el modificador de acceso más restrictivo. Los miembros declarados como privados son **accesibles SÓLO dentro de la misma clase**.  
No pueden ser accedidos ni siquiera por clases derivadas de la misma.

- `protected`  
Los miembros declarados como protected son **accesibles SÓLO dentro de la misma clase, en clases hijas (subclases) y dentro del mismo paquete**.

- `default` (sin modificador)  
Si no se especifica ningún modificador de acceso, se considera el acceso por defecto. Los miembros con acceso por defecto son **accesibles SÓLO dentro del mismo paquete**.  
No pueden ser accedidos desde clases en paquetes diferentes.

<br>

Con el encapsulamiento se puede lograr la inmutabilidad de ciertos atributos de una clase. Al marcar un atributo como `private` y proporcionar sólo un método de lectura (`getter`), se evita que dicho atributo sea modificado accidentalmente o intencionalmente desde fuera de la clase.

Por convención **TODOS los atributos de una clase** deben ser `private` para proteger que ningúna otra `clase` tenga acceso a ellos y obligue a usar los `getters` y `setters` para introducir los valores

````java
// atributos
private int id;
private String nombre;
private String apellido;
````

<br>

## 📂 Patrón `Getters` & `Setters`

Los métodos de acceso en Java son métodos públicos que se utilizan para CONTROLAR el acceso a los **atributos privados** de una clase.  
Son la herramienta fundamental para implementar el principio de Encapsulamiento en la Programación Orientada a Objetos (POO).

Se dividen en dos tipos principales, que siguen una convención de nombres estándar en Java.

### ✧ Getter & Setter
Un `getter` es un método que se utiliza para **obtener el valor de una variable privada**, mientras que un `setter` es un método que se utiliza para **modificar el valor de una variable privada**.

- `getter` - «traer » «obtener» los datos.  
- `setter` - «colocar» «asignar» valores a los atributos.

<br>

Los `getters` y `setters` permiten que los atributos de una clase se **mantengan privados y no se puedan acceder directamente desde fuera de la clase**.  
Es importante tener en cuenta que, aunque permitir el acceso directo a variables privadas puede ser útil en algunas situaciones, también puede ser riesgoso. Por ejemplo, si alguna otra clase altera accidentalmente la variable privada, podría causar errores difíciles de encontrar.

Aquí es donde entran en juego los `getters` y `setters`. Al definirlos, puedes **controlar quién puede acceder y modificar las variables privadas en la clase**. Además, también puedes aplicar validaciones para los datos que se ingresen.

Es importante **nombrarlos correctamente**.  
El nombre debe **reflejar claramente la propiedad que MANIPULA** y debe seguir las convenciones de nomenclatura de Java. Ejemplo, si hay una propiedad llamada «edad», el `getter` debería llamarse `getEdad()` y el `setter` debería llamarse `setEdad(int edad)`.

<br>

- ### Sintaxis

  Ambos se declaran en la clase y permiten desde el `Main` leer y escribir los valores de las variables privadas (desde afuera de la clase donde fueron creadas). Por convención (y buenas prácticas) siempre van antes de los métodos por defectos «personalizados».

  El `getter` tiene la estructura de una función, ya que devuelve un valor.

  ````java
  modificadorAcceso tipoDato_a_devolver getNombreMétodo() {
      return nombre_atributo;
  }
   
  // ejemplo
  public int getId() {
      return id;
  }
  ````
  
  <br>

  El `setter` tiene la estructura de una función, ya que devuelve un valor.

  ````java
  modificadorAcceso void setNombreMétodo(tipoDato nombreAtributo) {
      this.nombreAtributo = nombreAtributo;
  }
  
  // ejemplo
  public void setId(int id) {
      this.id = id;
  }
  ````