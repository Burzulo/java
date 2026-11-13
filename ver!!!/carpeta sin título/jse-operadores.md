# 📌 Operadores

<br>

[Operadores](#-)  
[Operador Ternario](#-operador-ternario)

<br>

Un **operador** es un **símbolo o palabra clave** que indica que se debe efectuar una determinada operación. Estas operaciones pueden ser de asignación, aritméticas, condicionales, relacionales, entre otras. En programación, los operadores son la herramienta básica para transformar datos y expresar lógica.

Dependiendo del resultado obtenido en la evaluación de una expresión se puede hablar de expresiones aritméticas y expresiones lógicas

<br>

- ### Aritméticos  
  Los operadores aritméticos realizan operaciones matemáticas básicas

  | Nombre | Representación | Sintaxis |
  | :---: | :---: | :---: |
  | Suma | ``+`` | a + b |
  | Resta | ``-`` | a - b |
  | Multiplicación | ``*`` | a * b |
  | División | ``/`` | a / b |
  | Módulo / Resto | ``%`` | a % b |

<br>

- ### Unarios  
  Los unarios necesitan un único operando para realizar su función

  | Nombre | Representación | Sintaxis |
  | :---: | :---: | :---: |
  | Incremento (pre/post) | ``++`` | ++a / a++ |
  | Decremento (pre/post) | ``--`` | --a / a-- |
  | Identidad / Negación aritmética | ``+/-`` | -a / +a |
  | Negación lógica | ``!`` | !cond |

  > ``!cond``: ``cond`` es el nombre de una variable (abreviatura de "condición"), para que funcione, ``cond`` debe ser de tipo booleano (``true`` / ``false``), y ``!`` Es el operador ``NOT``.

<br>

- ### Relacionales:  
  Se usan para comparar valores y devuelven booleanos

  | Nombre | Representación | Sintaxis |
  | :---: | :---: | :---: |
  | Mayor que | ``>`` | a > b |
  | Menor que | ``<`` | a < b |
  | Mayor o igual que | ``>=`` | a >= b |
  | Menor o igual que | ``<=`` | a <= b |
  | Igual a | ``==`` | a == b |
  | Distinto de | ``!=`` | a != b |

<br>

- ### Condicionales / Lógicos:  
  Se usan para comparar valores y devuelven booleanos

  | Nombre | Representación | Sintaxis |
  | :---: | :---: | :---: |
  | AND | ``&&`` | a && b |
  | OR | ``||`` | a || b |
  | NOT | ``!`` | !a |

<br>

### ✧ Operador Ternario

Es un operador en programación que **permite tomar decisiones SIMPLES basadas en una condición y asignar un valor a una variable o expresión en función de si la condición es verdadera o falsa**.

Posee tres principales partes en su estructura:

- *Condición* » Una expresión que se evalúa como verdadera o falsa.
- *Valor_si_verdadero* » El valor que se asignará a la variable si la condición es verdadera.
- *Valor_si_falso* » El valor que se asignará a la variable si la condición es falsa.  

<br>

Este operador se caracteriza por su sintaxis compacta y su capacidad para simplificar la escritura de condicionales simples en una sola línea de código.

````java
variable = (condición) ? valor-si-verdadero : valor-si-falso;
````

<br>

> [!IMPORTANT]  
> La principal limitación del operador ternario (``? :``) es que debe retornar un valor y, por lo tanto, no se puede utilizar para ejecutar bloques complejos de código que no devuelvan nada.