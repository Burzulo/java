## 📌 Protocolo HTTP

&nbsp;

Un **protocolo** es un **conjunto de reglas** que se debe seguir para poder obtener o lograr un determinado resultado o acceder a un **determinado recurso** o **servicio**.

En las comunicaciones entre clientes y servidores existen distintos protocolos de comunicación para que puedan entenderse entre sí. Uno de los más utilizados es el **protocolo HTTP**, el protocolo utilizado actualmente para acceder a internet. Las siglas **HTTP** significan **«Hypertext Transfer Protocol»**.

HTTP permite que las solicitudes (**requests**) y respuestas (**responses**) entre clientes y servidores, tengan un determinado **formato a seguir** y respetar para que puedan comunicarse sin inconvenientes.

&nbsp;

![http](https://github.com/user-attachments/assets/cb5c26ad-04ca-4666-bf7f-029e73277d7d)
<p align="center">
Proceso de comunicación HTTP
</p>

&nbsp;

### 🔹 Request
Una request o solicitud es el **mensaje** que se lleva a cabo desde un cliente **hacia un servidor** para poder acceder a un determinado servicio.

Una request que se lleva a cabo en una comunicación que utiliza el protocolo HTTP tiene una serie de partes con una funcionalidad distinta:

- *Método*: indica bajo qué método HTTP se envía un mensaje. Los más conocidos: GET, POST, PUT y DELETE.

- *URL*: dirección donde se encuentra el servidor y a la cual el cliente está enviando la solicitud o request.

- *Header*: contiene atributos o especificaciones necesarias para una correcta comunicación.

- *Body*: campo opcional para incluir objetos, textos o datos que son necesarios transmitir en la solicitud.

Como en toda red de datos, los **mensajes** entre clientes y servidores se **transmiten mediante paquetes**, donde cada uno de ellos cuentan con las partes que se acaban de mencionar.

&nbsp;

### 🔹 Response
En el protocolo HTTP, las respuestas o responses, al igual que las requests, tienen un **formato particular** que les permiten transportar la información necesaria para **atender a las solicitudes recibidas**.

La estructura de las respuestas es muy similar a la de las solicitudes, tienen la particularidad de contar con un «Status Code» («código de estado») que ayuda a que el cliente comprenda si se pudo procesar correctamente la solicitud en el servidor.

Las principales partes de una respuesta son:

* *Status Codes*: código particular que indica información particular sobre si se pudo concluir con la solicitud enviada o no. Este código, dependiendo del tipo que sea, puede comunicar diferentes situaciones.</br>
</br>Entre los más comunes se encuentran:

  * *Códigos de rango 100*: son respuestas de tipo informativas. Generalmente se utilizan para informar que una solicitud está siendo procesada.
  
  * *Códigos de rango 200*: utilizados para comunicar que una solicitud fue procesada correctamente.
  
  * *Códigos de rango 300*: utilizados para informar que se producirá una redirección.
  
  * *Códigos de rango 400*: utilizados para representar errores causados principalmente por la solicitud del cliente. Entre los más conocidos se encuentra el error 404 Not Found.
  
  * *Códigos de Rango 500*: utilizados para manifestar errores pero que fueron causados por el servidor. Uno de los más conocidos es el error 500 Internal Server Error.

* *Header o cabecera*: misma función que en las requests.

* *Body o cuerpo*: campo opcional con la misma función que las requests.

&nbsp;

### 🔹 Arquitectura REST y métodos HTTP
**REST** (Representational State Transfer) es un estilo de arquitectura de software que **define o establece un conjunto de estándares, propiedades y buenas prácticas** que se pueden implementar sobre HTTP.

Su principal función es permitir que un desarrollo web pueda operar con otros mediante sus estándares a través de internet o de una red. La característica que destaca a REST es el hecho de que es “stateless”, es decir, un protocolo que no posee estado.

En base a la arquitectura REST, en el protocolo HTTP existen varios métodos o verbos que pueden ser utilizados para las comunicaciones de las solicitudes, donde cada uno de ellos tiene una finalidad en particular.

&nbsp;

| MÉTODO | FUNCIONALIDAD |
| :----: | ----- |
| GET |Solicita una representación de un recurso específico.</BR>Las peticiones que usan el método GET solo deben recuperar datos.|
| POST | Envía una entidad a un recurso en específico, causando a menudo un cambio en el estado o efectos secundarios en el servidor. "Agregar información" |
| PUT |**Reemplaza** todas las representaciones actuales del recurso de destino con la carga útil de la petición. Este método permite reemplazar "varios elementos de un recurso a la vez".|
| DELETE | **Borra** un recurso en específico.|
| PATCH | Aplica **modificaciones parciales** a un recurso. Realiza modificaciones más "puntuales". |

&nbsp;

▶️ [Protocolo HTTP | Todo Code](https://youtu.be/l2MihYAj0Iw?si=iknUcUAVLlWpFXL0)<br/>
