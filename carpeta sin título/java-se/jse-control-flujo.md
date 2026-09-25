# 📌 Control de Flujo

<br>

- [Estructuras Condicionales](#-estructuras-condicionales)
  - [``If``](#-if)
  - [``If + Else``](#-if--else)
  - [``If + Else + If | Else``](#-if--else--if--else)
- [Selección múltiple](#-selección-múltiple)
  - [``switch``](#-switch)
- [Iteraciones](#-iteraciones)
  - [``while``](#-while)
  - [``for``](#-for)
  - [``do-while``](#-do-while)
- [Control de Saltos](#-control-de-saltos)
  - [``break``](#-break)
  - [``continue``](#-continue)
  - [``return``](#-return)

<br>

## 📂 Estructuras Condicionales

Son aquellas que permiten la ejecución de unas u otras acciones dependiendo de que se cumpla o no una condición o dependiendo del valor que tome una determinada variable.

<br>

### ✧ ``If``
  
La estructura ``if`` ejecuta un **bloque de sentencias** solamente cuando se cumple la condición del ``if``.

- Si la condición es verdadera se ejecuta el bloque de sentencias  
- Si la condición es falsa, el flujo del programa continúa en la sentencia inmediatamente posterior al ``if``  

````java
if (condición) {
    // bloque de sentencias
}
````

La ``condición`` es una expresión que evalúa un valor lógico, por lo que el resultado solo puede ser ``true`` o ``false``. La condición siempre se debe escribir entre paréntesis. La selección se produce sobre el bloque de sentencias delimitado por llaves.

<br>

### ✧ ``If + Else``

La estructura ``if-else`` selecciona entre **dos bloques de sentencias** mutuamente excluyentes.

- Si se cumple la condición, se ejecuta el bloque de sentencias asociado al ``if``  
- Si la condición no se cumple, entonces se ejecuta el bloque de sentencias asociado al ``else``  

````java
if (condición) {
    // bloque de sentencias if
} else {
    // bloque de sentencias else
}
````

<br>

### ✧ ``If + Else + If | Else``

Los condicionales múltiples son estructuras ``if`` y ``else`` anidadas entre sí, que permiten tener mayor control del flujo de un programa dependiendo de lo que se quiera hacer (o no) según diferentes condiciones y situaciones.

````java
if (condición-1) {
    // instrucciones si la condición-1 es verdadera
    bloque-de-sentencias
} else if (condición-2) {
    // instrucciones si la condición-2 es verdadera
    bloque-de-sentencias
} else if (condición-3) {
    // instrucciones si la condición-3 es verdadera
    bloque-de-sentencias
} else {
    // instrucciones si ninguna condición anterior es verdadera
    bloque-de-sentencias
}
````

<br>

## 📂 Selección múltiple

### ✧ ``switch``

La estructura ``switch`` permite **seleccionar un bloque de sentencias** entre varios casos. Permite múltiples caminos a partir de la evaluación de una sola expresión/condición. La construcción de esta estructura se ejecuta mediante la evaluación de la condición y un conjunto de casos llamados ``cases``.

Cada ``case`` es una posible respuesta a la evaluación de esa condición, si el valor que se busca coincide con algún ``case``, se ejecuta el mismo hasta la sentencia ``break`` o hasta el final del ``switch``.

````java
switch (expresión) {
case valor1:
    bloque-de-sentencias-1;
    break
case valor2:
    bloque-de-sentencias-2;
    break
case valor3:
    bloque-de-sentencias-3;
    break
case valor4:
    bloque-de-sentencias-4;
    break
default:
    bloque-de-sentencias-default;
}
````

Es importante colocar una **instrucción ``break`` al final** de cada ``case``, de esta forma solo se ejecutará el código del ``case`` correspondiente y no se continuará con los ``case`` siguientes. En default no es necesario poner ``break`` porque suele ser el último caso que se ejecutará cuando no se cumpla ninguna de las condiciones especificadas en los case anteriores, por tanto, llega a su fin y no hay más casos que evaluar.

<br>

## 📂 Iteraciones

Estas estructuras permiten repetir un **número determinado** de instrucciones un **número finito** de veces.  Esta ejecución repetitiva se conoce como **«bucle»** o **iteración**, existiendo dos tipos de ellas:

- Controladas por un centinela
- Controladas por un contador.

<br>

### ✧ ``while``

La estructura de repetición ``while`` repite el bloque de sentencias mientras **la condición del ``while`` es verdadera**. La condición se comprueba justo al principio. Si el resultado es falso, entonces no se ejecuta el bloque de sentencias. Por eso se puede ejecutar el bloque de sentencias de 0 (ninguna) a n (muchas) veces.

````java
while (condición) {
    // bloque de sentencias
}
````

La condición se escribe obligatoriamente entre paréntesis. Cuando el programa ejecuta un ``while``, lo primero que hace es evaluar la condición. Si es verdadera ejecuta el bloque de sentencias, si es falsa finaliza el ``while``.

En cada iteración, cuando finaliza la ejecución del bloque de sentencias, vuelve a evaluar la condición. De nuevo, si es verdadera, ejecuta el bloque de sentencias, si es falsa finaliza el ``while``. Cuando esto último se produce, el flujo del programa continúa en la sentencia inmediatamente posterior al ``while``.

<br>

### ✧ ``for``

La estructura ``for`` repite el bloque de sentencias **mientras la condición del ``for`` es verdadera**. Sólo se debe utilizar cuando se sabe el número de veces que se debe repetir el bloque de sentencias.

El ``for`` también es la estructura que se utiliza por excelencia para recorrer ``arrays`` (vectores y matrices).

Su estructura está compuesta por tres partes:

- *Inicialización de la variable*: Esta se utiliza en la condición (se ejecuta solo una vez al principio del ciclo).
- *Condición de fin del ciclo*: se evalúa esta expresión al comienzo de cada iteración.
- *Modificación de la variable*: incremento o decremento, se ejecuta al final de cada iteración.

````java
for (inicializacion; condicion; actualización) {
    // bloque de sentencias
}
````

<br>

### ✧ ``do-while``

La estructura de repetición ``do-while`` ejecuta el bloque de sentencias **al menos una vez**. Después comprueba la condición y repite el bloque de sentencias mientras la condición es verdadera.

````java
inicialización;
do {
    // bloque de sentencias
    // actualización
} while (condición);
````

Si en la *condicion* se utiliza la funcion ``equals`` lo que estamos diciendo es «mientras la palabra sea igual a … », por ejemplo cuando se busca que una palabra «centinela» nos indique que una vez escrita debemos salir del programa, se utiliza el símbolo ``!`` delante ya que estamos buscando lo contrario.

````java
while (!palabra.equals("salir")) {

}
````

Cuando la palabra sea igual a ``salir``, el ``while`` se detiene y continúa con el código. Mientras se ingresen otras palabras el bucle seguirá girando.

<br>

> [!NOTE]  
> **Bucles Infinitos**  
> Se produce cuando por algún motivo el programa entra en un bucle, pero el mismo no tiene una condición de salida. Esto puede suceder tanto en los bucles controlados por centinelas como por los controlados por contador.
>  
>  Se le llama **bucle infinito** porque al no haber una condición de salida, el bucle **continúa ejecutándose sin fin**.

<br>

## 📂 Control de Saltos

Son instrucciones especiales que alteran el flujo normal de un programa, principalmente dentro de bucles (``for``, ``while``, etc.) o métodos.

<br>

### ✧ ``break``

Esta sentencia **termina** inmediatamente el bucle más cercano en el que se encuentra. Se usa para salir de un bucle cuando se cumple una condición y/o detener un ``switch``.

```java
for (int i = 1; i <= 10; i++) {
    
    if (i == 5) {
        break;   // sale del bucle cuando i es 5
    }
    
    System.out.println(i);
}
```

<br>

### ✧ ``continue``

La sentencia **salta** el resto del código en la iteración actual del bucle y pasa a la siguiente vuelta. Se usa para ignorar ciertos valores o casos dentro de un bucle.

```java
for (int i = 1; i <= 5; i++) {

    if (i == 3) {
        continue;   // se salta el 3
    }
 
    System.out.println(i);
}
```

<br>

### ✧ ``return``

Esta sentencia **finaliza** la ejecución de un método y (opcionalmente) **devuelve** un valor. Se usa en métodos que devuelven resultados o métodos ``void`` para salir antes si no hay nada más que hacer.

````java
// ejemplo 1 con VALOR
public static int suma(int a, int b) {

    return a + b;   // devuelve el resultado

}

// ejemplo 2 en un MÉTODO
public static void saludar(String nombre) {

    if (nombre == null) {

        return;   // sale si no hay nombre
    }
 
    System.out.println("Hola, " + nombre);
}
````