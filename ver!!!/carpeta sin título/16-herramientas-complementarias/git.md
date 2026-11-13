# 📌 GIT / GITHUB

<br>

- [Configuración Inicial](#-configuracion-inicial)
- [indice ❌](#-...)
- [indice ❌](#-...)
- [indice ❌](#-...)
- [Branches / Ramas ](#-branches)


<br>

Git es un **software de control de versiones** que registra los cambios realizados sobre un archivo o un conjunto de archivos a lo largo del tiempo. Este permite **gestionar distintas versiones de un mismo archivo**, pudiendo volver a una versión anterior o una más reciente cuando sea necesario.

#### ▫️ REPOSITORIO  
Cuando se trabaja con Git lo que se crea es un *repositorio*, es decir, un lugar donde se **guardan y administran** nuestros archivos.
  
Existen dos tipos de repositorios:

- *Locales*: son aquellos que se crean de forma “local” en nuestra PC y no necesariamente son compartidos.
- *Remotos*: son aquellos que se encuentran alojados en algún servidor externo y que puede ser accedido desde cualquier lugar. Ejemplo GitHub.

<br>

## 📂 Configuracion Inicial

Tras instalar Git en el sistema, se deben hacer algunas cosas para personalizar el entorno. Es necesario hacerlo solamente una vez en la computadora LOCAL y se mantendrán entre actualizaciones.

> Se pueden cambiar en cualquier momento volviendo a ejecutar los comandos correspondientes.

<br>

- `$ git config` ➙ permite obtener y establecer variables de configuración que controlan el aspecto y funcionamiento de Git

- `$ git config user.name "Nombre"` ➙ configura el nombre de usuario  
`$ git config user.email "email@example.com"` ➙ configura el correo electrónico  
`git config user.password "token"`

  > ⚠️ En el apartado password no va la contraseña de la cuenta sino el ***Acces Token*** que se haya creado



- `$ git config --list` -- muestra todas las propiedades que Git ha configurado.

-------
- Crear Repositorio

  > git init


- Configurar identidad del Usuario

  > git config user.name "nombre"  
  > git config user.email "email"  



<br>

## 📂 Branches

Las ramas se pueden definir como «punteros» para cada uno de los cambios o versiones que se quieren armar en el desarrollo del proyecto. Cada RAMA representa una LÍNEA INDEPENDIENTE de desarrollo lo que permite trabajar en nuevas funcionalidades sin afectar el código estable en la rama principal.

Git parte de una rama principal llamada `main / master`, de la cual se desprenden todas las demás ramas que se pueden crear.

<br>

![Branch](https://github.com/user-attachments/assets/1635b168-0839-4e08-8eb0-e8550441dc94)

<br>

- `$ git branch` ➙ Lista las ramas locales y resalta en la que estámos ubicados

- `$ git branch "nombre-nueva-rama"` ➙ permite CREAR una nueva rama.

- `$ git checkout "nombre-rama"` ➙ permite CAMBIAR a una rama existente (Git antiguo).

- `$ git switch "nombre-rama"` ➙ permite CAMBIAR a una rama existente (Git moderno).
  
- `$ git merge` ➙ permite UNIFICAR dos ramas en una sola, para que ambas tengan los mismos archivos sin diferencias.

  ````java
  // Se debe estar en la rama a ACTUALIZAR para unificar.

  $ git merge "rama-origen" "rama-destino"
  ````

- `$ git branch -m "nombre-rama-ACTUAL" "nombrerama-NUEVA"` ➙ permite cambiar el NOMBRE de una rama.

- `$ git branch -d rama-a-eliminar` ➙ permite ELIMINAR una rama creada.

   > En caso de estar ubicados en la misma rama a eliminar, primero se debe cambiar a otra rama porque sino no lo permite.
