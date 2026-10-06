# 📌 Estructuras de Control: Selección

<br>

- [Condicional Simple: `SI - ENTONCES`](#-condicional-simple)
- [Condicional Doble: `SI - ENTONCES - SINO`](#-condicional-doble)
- [Condicionales Anidados: decisiones múltiples en cascada](#-condicionales-anidado)
- [Selección Múltiple: `SEGÚN / CASO` (Switch lógico)](#-selección-múltiple)


<br>

Las estructuras de selección permiten que un algoritmo rompa su ejecución secuencial para adaptarse a diferentes escenarios. En ingeniería, esto se conoce como **flujo de control dinámico**. La base de todas estas estructuras es la **evaluación de una expresión booleana** (una pregunta que solo puede ser ``true`` o ``false``).

## 📂 Condicional Simple

### 🔖 Estructura ``SI - ENTONCES``

La selección simple es el bloque de construcción básico de la lógica condicional. Su propósito es ejecutar un grupo de instrucciones **únicamente si** se cumple una condición específica. Si la condición no se cumple, el programa ignora esas instrucciones y sigue su curso como si nada hubiera pasado. En términos de diseño, se utiliza para "activar" funcionalidades especiales bajo ciertas circunstancias.

#### ▫️ Ejemplo en Pseudocódigo

````text 
Algoritmo VerificarDescuento
    Definir montoCompra Como Real
    Escribir "Ingrese el total de su compra:"
    Leer montoCompra
    
    // Solo si la compra supera los 100, se aplica un mensaje
    Si montoCompra > 100 Entonces
        Escribir "¡Felicidades! Ha ganado un cupón para su próxima visita."
    FinSi
    
    Escribir "Gracias por su compra. Total: ", montoCompra
FinAlgoritmo
````

<br>

## 📂 Condicional Doble

### 🔖 Estructura ``SI - ENTONCES - SINO``

A diferencia de la simple, la estructura doble plantea una bifurcación obligatoria: el algoritmo debe elegir entre **dos caminos mutuamente excluyentes**. Es decir, o se ejecuta el bloque del "Entonces" o se ejecuta el bloque del "Sino", pero jamás ambos. 

Esta estructura es fundamental para manejar estados binarios (encendido/apagado, aprobado/reprobado, activo/inactivo) de manera robusta.

#### ▫️ Ejemplo en Pseudocódigo

````text
Algoritmo ControlDeCalificaciones
    Definir nota Como Real
    Escribir "Ingrese la nota final del alumno:"
    Leer nota
    
    Si nota >= 60 Entonces
        Escribir "Estado: APROBADO"
    Sino
        Escribir "Estado: REPROBADO"
    FinSi
FinAlgoritmo
````

<br>

## 📂 Condicionales Anidado

### 🔖 Selección en Cascada

En la ingeniería de software real, los problemas rara vez son binarios. A menudo, una decisión depende del resultado de una decisión anterior. Los condicionales anidados permiten evaluar múltiples criterios en orden jerárquico. 

Es vital cuidar la indentación (sangría) del código, ya que cada "Sino" corresponde al "Si" inmediatamente superior. Una cascada mal diseñada puede generar errores de lógica difíciles de detectar.

#### ▫️ Ejemplo en Pseudocódigo

````text
Algoritmo ClasificarClima
    Definir temperatura Como Entero
    Escribir "Ingrese la temperatura actual en grados Celsius:"
    Leer temperatura
    
    Si temperatura > 30 Entonces
        Escribir "El clima es Cálido."
    Sino
        Si temperatura >= 15 Entonces
            Escribir "El clima es Templado."
        Sino
            Escribir "El clima es Frío."
        FinSi
    FinSi
FinAlgoritmo
````

<br>

## 📂 Selección Múltiple

### 🔖 Estructura ``SEGÚN / CASO``

Cuando una variable puede tomar varios valores constantes y discretos (ejemplo los días de la semana), el uso de múltiples condicionales anidados se vuelve ineficiente y difícil de leer. La estructura de selección múltiple simplifica esto al comparar una sola variable contra una lista de valores posibles. Si hay una coincidencia, se ejecuta el bloque correspondiente. Es la forma más limpia de implementar lógica basada en estados o selecciones de usuario.

#### ▫️ Ejemplo en Pseudocódigo

````text
Algoritmo MenuOperaciones
    Definir opcion Como Entero
    Escribir "--- SISTEMA DE ARCHIVOS ---"
    Escribir "1. Abrir archivo"
    Escribir "2. Guardar archivo"
    Escribir "3. Eliminar archivo"
    Escribir "Seleccione una opción (1-3):"
    Leer opcion
    
    Segun opcion Hacer
        1:
            Escribir "Abriendo el sistema de archivos..."
        2:
            Escribir "Guardando cambios en el disco..."
        3:
            Escribir "¡Advertencia! Eliminando archivo permanentemente..."
        De Otro Modo:
            Escribir "Opción no válida. Intente nuevamente."
    FinSegun
FinAlgoritmo
```