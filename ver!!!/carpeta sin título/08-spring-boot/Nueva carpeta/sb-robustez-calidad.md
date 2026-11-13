
# 📌 Robustez y Calidad

<br>

- [indice ❌](#-...)
- [indice ❌](#-...)
- [**Postman** para Pruebas de integración](#-postman)

<br>

## 📂 Postman

**Postman** es una herramienta para **probar APIs REST**. Es un software que permite simular el envío de solicitudes HTTP REST mediante diferentes métodos sin la necesidad de desarrollar una aplicación cliente o de contar con un front-end en particular.

Para comenzar a usarlo, se debe **descargar** desde su página oficial, instalarlo y realizar las configuraciones iniciales:  
🔗 [https://www.postman.com/downloads/](https://www.postman.com/downloads/),

>  ▶️ **link**  
> [¿Cómo descargar e instalar POSTMAN en Windows? | TodoCode](https://youtu.be/laZv3I9XN0w?si=AqOgwnTfoefudBxK)

<br>

### ▪︎ Pruebas con Postman
Vamos a intentar probar si nuestra API funciona correctamente y recibe los datos necesarios.

1. **Crear una nueva solicitud** y en primer lugar seleccionar el método HTTP que vamos a utilizar (en este caso `POST`).

2. **Indicar la URL de la API**, por ejemplo:  
   `localhost:8080/cliente`

3. En las pestañas inferiores, seleccionar **Body**, ya que los datos se enviarán mediante `@RequestBody`.

4. Elegir el formato **raw** y seleccionar **JSON** en el combobox de la derecha.

5. Una vez hecho esto, escribir manualmente simulando un objeto JSON simulando una entidad con los mismos atributos que la clase Java, y le asignaremos sus correspondientes valores. Por ejemplo:

```json
{
  "id": 1,
  "nombre": "Zlatan",
  "apellido": "Ibrahimovic"
}
```

<br>

Una vez que esta todo configurado, podemos hacer click en **Send** y esto enviará la solicitud `POST` a nuestra aplicación (obviamente esta debe estar siendo ejecutada).

Si todo llega correctamente, en la consola de salida del servidor que nos proporciona el IDE, podremos visualizar si efectivamente el `System.out.println` que colocamos, recibió y mostró los valores que recibimos.

Resultado en consola:

![Postman-2](https://github.com/Burzulo/MisNotas/blob/main/roadmap-java/img/postman-2.png?raw=true)

<br>
