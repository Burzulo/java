#  📌 Responses – en Spring Boot

En una API REST, una vez que el servidor procesa la petición del cliente, debe **enviar una respuesta HTTP** que incluya el resultado de la operación.  
En Spring Boot, las respuestas pueden enviarse de forma sencilla con la anotación `@ResponseBody` o de manera más controlada con la clase `ResponseEntity`.

<br>

## 🏷️ @ResponseBody

`@ResponseBody` permite que el valor devuelto por un método del controlador se escriba directamente en el cuerpo de la respuesta HTTP, evitando la necesidad de renderizar una vista. Spring Boot convierte automáticamente objetos Java en JSON o XML según la configuración y las cabeceras solicitadas por el cliente.

Así el método **GET** a través de la annotation `@ResponseBody` **conforma un objeto para la devolución de un mensaje**.

Suponiendo que tenemos una lista de clientes, y mediante una solicitud GET se desea devolver estos clientes que se encuentran en ella. Para ello se crea un método `traerClientes()` y lo mapeamos con la annotation `@ResponseBody`.

```java
@RestController
public class HolaController {
    
   @GetMapping ("/cliente/traer")
   @ResponseBody
   public List<Cliente> traerClientes() {

      List<Cliente> listaClientes = new ArrayList<Cliente>();   // Se crea lista de prueba y agregan registros
      listaClientes.add(new Cliente(1L, "Zlatan", "Ibrahimovic"));         
      listaClientes.add(new Cliente(2L, "Cristiano", "Ronaldo"));
      listaClientes.add(new Cliente(3L, "Lionel", "Messi"));

      return listaClientes;   // Se devuelve la lista mediante ResponseBody
   }
}
```

<br>

Una vez realizado esto, se ejecuta la aplicación y simulamos una solicitud **GET** mediante **POSTMAN**, se verá que se reciben como resultado los 3 objetos Java creados en el endpoint en el body de la `response` que obtenemos.

```bash
GET localhost:8080/cliente/traer
```

**Body**

```json
[
   {
      "id": 1,
      "nombre": "Zlatan",
      "apellido": "Ibrahimovic"
   },
   {
      "id": 2,
      "nombre": "Cristiano",
      "apellido": "Ronaldo"
   },
   {
      "id": 3,
      "nombre": "Lionel",
      "apellido": "Messi"
   }
]
```

De esta manera se pueden devolver los objetos o listas de objetos creados en nuestra lógica en el cuerpo de las `responses`, para que así el cliente que esté haciendo la consulta, pueda recibirlos en formato JSON y hacer uso de los mismos.

<br>

## 🏷️ ResponseEntity

@ResponseBody no es la única forma de devolver mensajes desde el controlador, como otra opción existe `ResponseEntity`. La diferencia principal es que `ResponseEntity` **administra todo el paquete completo** de una respuesta HTTP, es decir, **puede manipular** el cuerpo, la cabecera o incluso los códigos de estado, **haciendo que la respuesta brindada sea totalmente personalizada**. Este ofrece un control más completo.

Un ejemplo de una respuesta con `ResponseEntity` con un Status Code puede verse en la imagen a continuación:

```java
@RestController
public class HolaController {

   @GetMapping ("/pruebaresponse")
   ResponseEntity<String> traerRespuesta() {
      return new ResponseEntity<>("Esto es un mensaje Response Entity", HttpStatus.OK);
   }
}
```

<br>

Al probar con Postman el endpoint que se acaba de hacer con `ResponseEntity`, se obtiene el siguiente resultado, donde además de ver el status code 200 (establecido mediante `HttpStatus.OK`) se verá el mensaje personalizado que hayamos seleccionado.

<br>

![Response Entity](https://github.com/Burzulo/MisNotas/blob/main/MisNotas/roadmap-java/imagenes/response-entity.png?raw=true)

> 💡 **NOTA**  
> Como detalle a tener en cuenta, es que `ResponseEntity` no es una annotation como `@ResponseBody`, sino que se trata de una clase especial que se puede utilizar.
