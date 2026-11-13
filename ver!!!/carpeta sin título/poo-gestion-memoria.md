
# 📌 Gestión de Memoria

<br>

- [Stack vs. Heap](#-stack-vs-heap)
- [Garbage Collector](#-garbage-collector)

<br>

## 📂 Stack vs Heap

El concepto de **Stack** y **Heap** no es exclusivo de Java; es una arquitectura de gestión de memoria fundamental que utilizan muchísimos lenguajes (como C, C++, C#, Python o Swift) y los sistemas operativos.  
Sin embargo, cómo se gestionan esas áreas varía drásticamente entre lenguajes.

En el ecosistema Java, la JVM administra la memoria RAM dividiéndola en DOS estructuras principales con comportamientos opuestos pero complementarios.

<br>

### ✧ Stack (Pila)

El **Stack** funciona como el espacio de trabajo inmediato y ordenado de la JVM.

Opera bajo el esquema «LIFO» (Last In, First Out), lo que significa que cada vez que se invoca un método, se apila un nuevo bloque de memoria (frame) que contiene sus variables locales y parámetros.

Aquí se almacenan directamente los tipos primitivos y, fundamentalmente, las referencias (direcciones de memoria) a los objetos.

Al ser una estructura de gestión automática, en cuanto el método termina su ejecución, su bloque se elimina de forma instantánea, liberando el espacio sin intervención externa.

<br>

### ✧ Heap (Montón)

Por otro lado, el **Heap** es un área de memoria mucho más extensa y dinámica, diseñada para albergar todos los objetos creados con la palabra clave ``new``.

A diferencia del Stack, el Heap es compartido por toda la aplicación y es donde reside la "sustancia" de los datos, como los atributos de una instancia o los elementos de un array. Aquí es donde vive la "verdadera" información de las clases.

Debido a su naturaleza desordenada y persistente, la limpieza no es inmediata; aquí entra en juego el Garbage Collector, que monitorea el Heap para identificar y eliminar aquellos objetos que ya no tienen ninguna referencia activa apuntándoles desde el Stack, optimizando así el uso de los recursos del sistema.

Por lo tanto los objetos permanecen aquí mientras tengan al menos una referencia activa en el Stack.

````java
// ejemplo
Libro miLibro = new Libro();
````

- ``:miLibro`` es una variable de referencia que reside en el Stack.  
- ``new Libro()`` crea el objeto real en el Heap
- La variable en el Stack guarda la "dirección" de dónde está el objeto en el Heap.

<br>

### ⇒ Fallos comúnes

- #### 🚩 StackOverflowError

  El ``StackOverflowError`` ocurre cuando la pila de ejecución (Stack) se agota. Cada vez que se llama a un método, se añade un "frame" al Stack; si estas llamadas se acumulan sin liberarse, el espacio asignado (que suele ser pequeño) se llena por completo. 

  El culpable más común es la **recursividad infinita**, donde un método se llama a sí mismo sin una condición de salida adecuada, o una cadena de llamadas entre métodos tan profunda que supera la capacidad de la pila. En esencia, es un error de **lógica de control de flujo**.

- #### 🚩 OutOfMemoryError

  Por otro lado, el ``Java.lang.OutOfMemoryError`` sucede cuando el Heap ya no tiene espacio para alojar nuevos objetos y el Garbage Collector es incapaz de liberar más memoria. 

  A diferencia del error anterior, este suele estar vinculado a la cantidad de datos que la aplicación intenta procesar simultáneamente. La causa principal suele ser una fuga de memoria (Memory Leak), que ocurre cuando se mantienen referencias activas a objetos que ya no son necesarios, impidiendo que el GC los elimine. También puede ocurrir simplemente si la aplicación requiere más memoria de la que se le asignó mediante los parámetros de inicio.

<br>

## 📂 Garbage Collector

El **Garbage Collector** es un proceso automático de la Java Virtual Machine encargado de la gestión de la memoria dinámica. 

Su función principal es actuar como un "recolector de residuos" que identifica y elimina los objetos en el **Heap** que ya no son accesibles por la aplicación.  
Al realizar esta tarea de forma autónoma, el GC libera al desarrollador de la responsabilidad de destruir objetos manualmente, lo que reduce drásticamente errores.

- ### ¿Cuándo se activa?

  El GC no funciona de manera continua, sino que la JVM decide cuándo es el momento óptimo para ejecutarse basándose en el estado de los recursos.  
  Generalmente, se dispara cuando el espacio en el **Heap** está lleno y no hay lugar para nuevas instancias. También puede activarse si el sistema detecta una baja disponibilidad de memoria RAM.

- ### ¿Cómo funciona?

  El funcionamiento del GC se basa principalmente en un proceso de dos fases llamado **Mark-and-Sweep** (Marcar y Barrer):

   - En la fase de **marcado**, el recolector recorre el grafo de objetos (todos los objetos que viven en la memoria Heap) empezando desde las "Raíces del GC" (*GC Roots*).  
   Todos los objetos que pueden ser alcanzados se marcan como "vivos".

   - En la fase de **barrido**, el GC examina el Heap y libera el espacio de aquellos objetos que no fueron marcados, tratándolos como basura.  
   Para optimizar este proceso, Java utiliza una "Hipótesis Generacional", dividiendo el Heap en zonas según la antigüedad de los objetos, bajo la premisa de que la mayoría de los objetos mueren jóvenes.