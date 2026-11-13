#  📌 Inversión de Control (IoC)

<br>

- [❌ Concepto de Beans y Application Context](#-...)
- [Inyección de Dependencias (DI): mediante `Constructor`, `Setter` y `@Autowired`](#-inyeccion-de-dependencias)
- [Resolución de Ambigüedad: `@Primary` y `@Qualifier`](#-resolucion-de-ambiguedad)

<br>

Un aspecto clave y muy característico de **Spring** como **framework** es la utilización de la **IoC**. La *Inversión de Control* es un principio de diseño que cambia la forma tradicional en la que el código controla el flujo de una aplicación. En lugar de que el programador cree y administre directamente los objetos y sus dependencias, esa responsabilidad se invierte y pasa a un contenedor o framework (como Spring Framework).

Entonces en lugar de que el programador a través de la aplicación lleve el control del flujo de la misma, sera el framework quien lo haga. Tal como lo dice su nombre, **LOS ROLES DE CONTROL SE INVIERTEN**.

````java
// Flujo normal de trabajo
Aplicación ⟹ [llama] ⟹ Framework

// Flujo mediante inversión de control
Aplicación ⟸ [llama] ⟸ Framework

````

### ▫️ Aplicación

En Java «puro», el desarrollador crea los objetos manualmente. Aquí el **control está en sus manos**, el decide qué instancia crear y cuándo:

```java
Service servicio = new Service();
Controller controlador = new Controller(servicio);
```

Pero para aplicar el concepto de IoC, el framework tiene que entender qué es lo que hace la aplicación o de qué manera funciona. Para ello, el framework le requiere a la aplicación una serie de datos que puede estar expresada de diferentes maneras dependiendo del lenguaje de programación, en **Java**, por ejemplo, lo expresamos mediante las **``Annotations``**.

En Spring, el desarrollador solo declara qué necesita y el framework se encarga de crear, inicializar e inyectar esos objetos automáticamente:

```java
//ejemplo 

@Controller
public class MiControlador {

    @Autowired
    private MiServicio servicio;
}
```

<br>

> 💡 **NOTA**  
>
> Uno de los principales «problemas» que trata la **IoC** es la *creación o instanciación innecesaria de objetos mediante la sentencia ``new``*; mediante la IoC, el framework se asegura de crear los objetosy los pone a disposición de la aplicación mediante otro concepto muy importante conocido como **Inyección de Dependencias**.

<br>

## 📂 TITULO SECUNDARIO !!!!!!!!!!!!!!!!!!!!!!!!!!!!!!

texto ...............


> 💡 **NOTA**  
> En esencia, un **Bean** es un objeto de Java (una instancia de clase) que es instanciado, ensamblado y administrado por el Contenedor de Inversión de Control (IoC) de Spring. Spring es quien se encarga de todo su ciclo de vida, desde su creación hasta su destrucción.  
> 
> Cuando decimos que un objeto es un Bean, significa que Spring lo conoce y puede inyectarlo en otras partes de la aplicación donde se necesite, facilitando la implementación del principio de Inyección de Dependencias (DI).
>

...............................................

<br>

## 📂 Inyeccion de Dependencias

Mejor conocida como ***DI (dependency inyection)***, es un **PATRÓN DE DISEÑO** que está orientado al manejo de los objetos de una aplicación. Su principal objetivo es el de **mantener las capas de una aplicación lo más desacopladas posible entre sí**.

Para poder lograr esto, la inyección de dependencias permite que cada una de las partes del programa que se esté desarrollando sea **independiente** y que **no se comuniquen entre si mediante instancias, sino mediante interfaces**.

Se entiende entonces que la inyección de dependencias busca desacoplar lo máximo posible la relación entre clases o capas, pero… 

¿Qué es una dependencia? Una dependencia es una relación que puede existir entre una o varias clases, donde generalmente una (o varias) dependen de otra principal.

```java
// Ejemplo de dependencia entre clases

            ➙ Clase 2
    Clase 1 ➙ Clase 3 
            ➙ Clase 4

    | Las clases 2, 3 y 4 dependen de la clase 1
```

> ⚠️ **IMPORTANTE**  
> La DI en ningun momento buscar crear o utilizar la palabra `new` para instanciar sino que lo que hace es recibir los objetos y reasignarlos para seguir **REutilizando** los mismos.

<br>

### ▫️ Representación a nivel código

Supongamos que tenemos el modelado de un lavadero de autos, donde existe una clase llamada `ServicioLavado` de la cual dependen otras dos clases, `ServicioNormal` y `ServicioPremiun`:

````java
ServicioLavado ➙ ServicioNormal
               ➙ ServicioPremiun
````

Ambas dependen fuertemente de `ServicioLavado`. Esto, a nivel código se ve reflejado:

````java
public class ServicioLavado {

    ServicioNormal serviNorm; // genera dependencia
    ServicioPremiun serviPrem; // genera dependencia

}
````

Como se observa en ambas, tanto `ServicioNormal` como `ServicioPremiun` dependen de `ServicioLavadado` y es ésta clase quien tiene la responsabilidad de inicializar a ambos servicios en su constructor, sin embargo, si se aplica inyección de dependencias, se podría delegar esta responsabilidad que tiene `ServicioLavado` a otra clase, como por ejemplo, la clase `main` que tenga el proyecto.

Ahora bien, **¿Cómo se aplica la inyección de dependencias?** existen diferentes maneras de hacerlo, sin embargo hay 3 que son las más comunes:

- Mediante un constructor
- Mediante un setter
- Mediante la Annotation `@Autowired`

<br>

### 🔖 DI mediante un Constructor

Es el propio constructor de una clase el encargado de inyectar la dependencia.

Teniendo en cuenta el ejemplo anterior, se observa como el constructor crea las instancias de ambos tipos de servicios dentro de él; en la *inyección de dependencias mediante un constructor*, **éste únicamente recibirá como parámetros los objetos ya creados y los asignará según corresponda**.

> Generalmente cuando se crean constructores con parámetros de forma automática mediante IDEs, ya se proporciona de igual manera la inyección de dependencias sin la necesidad de tener que implementarla manualmente.

<br>

```java
public class ServicioLavado {

    ServicioNormal serviNorm; // genera dependencia
    ServicioPremiun serviPrem; // genera dependencia

    public ServicioLavado(ServicioNormal serviNorm, ServicioPremiun serviPrem) {
        this.serviNorm = serviNorm;
        this.serviPrem = serviPrem;
    }
}
```

<br>

### 🔖 DI mediante un Setter

Los métodos `getter` y `setter` permiten obtener o setear valores a los atributos de los objetos que sean creados, de igual manera los métodos ``set`` permiten inyectar dependencias, donde a partir de la recepción de un objeto como un parámetro este se asigna.

> Generalmente cuando se crean setters de forma automática mediante IDEs, ya se proporciona de igual manera la inyección de dependencias sin la necesidad de tener que implementarla manualmente.

<br>

```java
public class ServicioLavado {

    ServicioNormal serviNorm; // genera dependencia
    ServicioPremiun serviPrem; // genera dependencia

    public void setServiNorm(ServicioNormal serviNorm) {
        this.serviNorm = serviNorm;
    }

    public void setServiPrem(ServicioPremiun serviPrem) {
        this.serviPrem = serviPrem;
    }
}
```

<br>

### 🔖 DI mediante `@Autowired`

Así como Java permite realizar inyección de dependencias de forma genérica mediante setters o constructores, Spring como framework ofrece una annotation para hacerlo. Ésta es conocida como `@Autowired`.

Cuando se trabaja con una arquitectura multicapas donde es posible de que exista una dependencia entre los objetos de las mismas, `@Autowired` es de gran ayuda.

### ▫️ Ejemplo

Supongamos que tenemos un sistema creado con Spring Boot para un blog, en donde tenemos una clase llamada `Posteo`, con los atributos `id`, `titulo` y `autor`.

```java
// Clase Posteo

package com.inyeccion.ejemploAutowired.model;

import lombok.Getter;
import lombok.Setter;

@Getter @Setter
public class Posteo {

    private Long id;
    private String titulo;
    private String autor;

    public Posteo(Long id, String titulo, String autor) {
        this.id = id;
        this.titulo = titulo;
        this.autor = autor;
    }
}
```

Por otro lado, contamos también con una clase llamada `PosteoRepository` donde contamos con un método que nos devuelve la lista de todos los posteos existentes.

```java
// Clase PosteoRepository

@Repository
public class PosteoRepository {

    public List<Posteo> traerTodos() {

        List<Posteo> listaPosteos = new ArrayList<Posteo>();

        // se crean dos objetos para simular una lista
        listaPosteos.add(new Posteo (1L, "¿Como formatear una PC?", "Gonzalo"));
        listaPosteos.add(new Posteo (2L, "¿Como mantener la seguridad?", "Pedro"));

        return listaPosteos;
    }
}
```

Por último, contamos también con un `controller` que recibe una solicitud `GET` para recibir todos los posteos mediante el path «`/posteos`».

```java
@RestController
public class PosteoController {

    // el autowired inyecta la dependencia sin necesidad de crear un nuevo objeto
    @Autowired
    PosteoRepository repository;

    @GetMapping ("/posteos")
    public List<Posteo> traerTodos () {

        return repository.traerTodos();
    }
}
```

<br>

Como se ve, estan bien divididas las 3 tareas:

- `Controller` se encarga de recibir la solicitud.
- La clase `Posteo`, es el model que se necesita para trabajar con objetos de ese tipo.
- `PosteoRepository` cumple como si fuese una «base de datos» que ofrece los distintos posteos con los que contamos.

<br>

Ahora, como podemos ver en el ``controller``, ya no es esta capa la encargada de traer todos los posteos y devolverlos, sino que es el `repository` quien lo hace… 

¿Y cómo se logra esto? Creando un objeto de `PosteoRepository` SIN INSTANCIARLO, sino que lo mapeamos mediante `@Autowired`. `@Autowired` en este caso se va a encargar de crear la instancia necesaria y delegar la responsabilidad de traer los datos al repositorio, para que desde el método «`traerTodos`» de nuestro controller, podamos acceder a los datos que nos brinda.

De esta manera, una vez que levantemos nuestra aplicación y se haga la solicitud en cuestión, recibiremos como respuesta los posteos que teníamos en el repository

```bash
// Respuesta a request de lista de Posteos

GET localhost:8080/posteos
````

```json
[
    {
        "id" : 1,
        "titulo" : "¿Como formatear una PC?",
        "autor" : "Gonzalo"
    },
    {
        "id" : 2,
        "titulo" : "¿Como mantener la seguridad?",
        "autor" : "Pedro"
    }
]
```

<br>

## 📂 Resolucion de Ambiguedad

En Spring, la Inyección de Dependencias automática, facilitada por anotaciones como ``@Autowired``, se basa en encontrar un único Bean compatible para una interfaz o clase dada. La ambigüedad surge cuando **Spring encuentra múltiples implementaciones del mismo tipo** (la misma interfaz) en el Contenedor IoC y no sabe cuál elegir.

Las anotaciones ``@Primary`` y ``@Qualifier`` son las herramientas estándar de Spring para resolver este conflicto, dando al desarrollador el control explícito sobre la elección del Bean.

<br>

### ▫️ El Problema: Ambigüedad

Consideremos una interfaz y dos implementaciones:

````Java
public interface ServicioNotificacion {
    void enviarMensaje(String mensaje);
}

// Implementación 1
@Service 
public class SmsServicio implements ServicioNotificacion {
    // ... lógica de SMS
}

// Implementación 2
@Service 
public class EmailServicio implements ServicioNotificacion {
    // ... lógica de Email
}
````

````java
// Clase que inyecta la dependencia: Spring genera un error aquí

@Component
public class Cliente {

    @Autowired
    private ServicioNotificacion notificador; // Spring no sabe si inyectar SmsServicio o EmailServicio
}
````

Al intentar arrancar la aplicación, Spring lanzará una excepción indicando que hay Beans de tipo ``ServicioNotificacion`` (2 encontrados) y que no puede resolver la dependencia.

<br>

### 🔖 Solución 1: ``@Primary``

La anotación ``@Primary`` se utiliza para designar una de las implementaciones como la **preferida o por defecto**. Si hay ambigüedad, Spring siempre seleccionará el Bean marcado con ``@Primary``.

La anotation se coloca sobre la **clase de implementación**. Y es ideal para escenarios donde una de las implementaciones se usa en la vasta mayoría del proyecto.

#### ▫️  Ejemplo

````Java
@Service 
public class SmsServicio implements ServicioNotificacion {
    // ...
}

@Service 
@Primary
public class EmailServicio implements ServicioNotificacion {
    // ... lógica de Email, se convierte en la opción por defecto.
}

// Cliente ahora inyectará EmailServicio

@Component
public class Cliente {
    @Autowired
    private ServicioNotificacion notificador; 
    // Ahora 'notificador' es una instancia de EmailServicio
}
````

<br>

### 🔖 Solución 2: ``@Qualifier``

La anotación ``@Qualifier`` permite al desarrollador **especificar exactamente el nombre** del Bean que desea inyectar en un punto concreto. Esta es la solución más explícita y se utiliza cuando no hay un solo valor por defecto, o cuando se necesita una implementación diferente a la principal.

Se utiliza tanto en la declaración de la clase Bean como en el punto de inyección. El nombre del Bean por *defecto en Spring* es el nombre de la clase, comenzando con minúscula (ej. ``SmsServicio`` se convierte en ``smsServicio``).

#### ▫️ Ejemplo

Primero, la implementación debe tener un nombre de Bean claro (generalmente ya lo tienen con ``@Service``, ``@Component``, etc.):

````Java
@Service("sms")
public class SmsServicio implements ServicioNotificacion { /* ... */ }

@Service("correo")
public class EmailServicio implements ServicioNotificacion { /* ... */ }
````

Luego, en el punto de inyección, se usa ``@Qualifier`` para nombrar el Bean deseado:

````Java
@Component
public class ProcesadorFacturas {
    
    // Inyecta específicamente la implementación etiquetada como "correo"
    @Autowired
    @Qualifier("correo") 
    private ServicioNotificacion notificadorEmail; 

    // Inyecta específicamente la implementación etiquetada como "sms"
    @Autowired
    @Qualifier("sms") 
    private ServicioNotificacion notificadorSms; 

    // ...
}
````

<br>

> ⚠️ **IMPORTANTE** > *Regla de Prioridad*  
> Cuando se usan ambas anotaciones, ``@Qualifier`` siempre tiene prioridad sobre ``@Primary``. Si una dependencia tiene un ``@Qualifier`` específico, Spring ignorará cualquier Bean marcado con ``@Primary`` y solo buscará el Bean que coincida exactamente con el nombre especificado en el calificador.