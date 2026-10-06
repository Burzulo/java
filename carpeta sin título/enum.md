# 📌 Enumeraciones (enum)

<br>

- [Definición y Propósito](#-)
- [herencia implicita de ``java.lang.Enum``](#-)
- [Estado en Enums](#-)

<br>

## 📂 Definición y Propósito

Un ENUM es un **tipo de dato especial** en Java que permite definir un **grupo fijo de constantes** con nombres específicos. Cada constante en un ``enum`` es una instancia única de ese ``enum``.

Los ``enums`` en Java son, básicamente, una forma de definir un conjunto fijo de constantes, como los días de la semana, los meses del año, o los estados de un semáforo.

### ▫️ ¿Por qué se usan?
Se usan para representar **valores que no cambian**. Por ejemplo, si estás trabajando con los días de la semana, se puede definir un ``enum`` que contenga todos los días: ``Lunes``, ``Martes``, ``Miércoles``... 
 Así, nos aseguramos de que las únicas opciones válidas para un día de la semana sean estas y que no haya posibilidad de que se ingresen otras.

````java
public enum DiaSemana {
    LUNES, MARTES, MIERCOLES, JUEVES, VIERNES, SABADO, DOMINGO
}
````

Es vital entender que **cada constante es un objeto único** (`LUNES` es un objeto, `MARTES` es otro, y no solo una variable).

<br>

> ⚠️ **IMPORTANTE**  
> Ojo ! de acuerdo donde se quieran usar los ``enums`` es el lugar donde se deben declaran (Ej: si se quieren usar en todo el código va fuera del ``Main``).



### ▫️ Seguridad
La principal razón de ser de `enum` es garantizar la **Seguridad de Tipos (Type Safety)**. Es decir, que una variable declarada como `DiaSemana` solo pueda contener uno de los siete objetos `DiaSemana` (LUNES, MARTES, etc.), y no un `int` o un `String` cualquiera. Esto previene errores en tiempo de ejecución.

<br>
<br>

> ▶️📚 **links**  
> [ENUMS en Java | Todo Code](https://youtu.be/khY9QhgL5S8?si=PXcm0STzmrzU9liG)
