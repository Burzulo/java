# 📌 Git / GitHub

<br>

- [📌 Git / GitHub](#-git--github)
  - [📂 Diferencia entre Git y GitHub](#-diferencia-entre-git-y-github)
  - [📂 Configuración inicial](#-configuración-inicial)
  - [📂 Inicialización y Clonación](#-inicialización-y-clonación)
    - [✧ Inicialización](#-inicialización)
    - [✧ Clonación](#-clonación)
  - [📂 Estados del repositorio](#-estados-del-repositorio)
  - [📂 Añadir archivos al Staging Area](#-añadir-archivos-al-staging-area)
  - [📂 Confirmar los cambios](#-confirmar-los-cambios)
  - [**6**. Branches / Ramas](#6-branches--ramas)
  - [**7**. Repositorios Remotos](#7-repositorios-remotos)

<br>

## 📂 Diferencia entre Git y GitHub

* **Git** es un **sistema de control de versiones distribuido** que se ejecuta localmente. Su función principal es registrar el historial de cambios del código, permitiéndote volver a versiones anteriores si algo se rompe y/o controlar quién hizo cada modificación.
  
* **GitHub** es una **plataforma en la nube** que aloja repositorios remotos. Sirve para guardar un respaldo del proyecto en internet, compartir código y colaborar con otras personas de forma remota.

<br>

> [!NOTE]
> Cuando se trabaja con Git lo que se crea es un REPOSITORIO, un lugar donde se **guardan y administran** nuestros archivos. Hay dos tipos de repositorios: *Locales*, aquellos que se crean de forma “local” en nuestra PC y no necesariamente son compartidos y los *Remotos*, aquellos que se encuentran alojados en algún servidor externo y pueden ser accedido desde cualquier lugar.

<br>

## 📂 Configuración inicial

Tras instalar Git, se debe personalizar el entorno. Es necesario hacerlo solamente una vez en la computadora LOCAL y se mantendrán entre actualizaciones.

- **Abrir la terminal** (o Git Bash) en el ordenador e indicar nombre y correo electrónico para asociar la autoría de los cambios.
  
  - `$ git config --global user.name "Nombre"` -- para configurar el nombre de usuario globalmente
  - `$ git config --global user.email "example@email.com"` -- configura el correo electrónico globalmente

    > Es fundamental usar el mismo nombre y correo electrónico asociado a la cuenta de GitHub.

<br>

- **Verificar** que la configuración se guardó correctamente ejecutando:

  ```bash
  git config user.name
  git config user.email
  ```

  Al presionar enter en cada uno, la terminal devolverá el nombre y el correo guardados.

<br>

## 📂 Inicialización y Clonación

### ✧ Inicialización

Una vez creada la carpeta LOCAL desde CERO, para ubicarnos en ella e inicializar el repositorio hay dos opciones principales:

* **Desde la terminal** con el comando `cd`

  - Abrir la terminal o Git Bash.
  - Usar el comando `cd` (*Change Directory*) seguido de la ruta de la carpeta a la que se quiere ir. Por ejemplo: *En el Escritorio* `cd Desktop/MiProyecto`.
  - Se puede verificar en qué carpeta estamos ejecutando `pwd` o revisando la ruta que figura en la consola.

* **Desde VSC** (la forma más práctica)

  - Abrir Visual Studio Code.
  - En el menú superior, ir a **File > Open Folder** y seleccionar la carpeta del proyecto.
  - Abrir la terminal integrada yendo al menú superior en **Terminal > New Terminal**.
  - La terminal se abrirá ubicada automáticamente en la ruta de tu proyecto

<br>

Una vez que la terminal esté ubicada dentro de la carpeta elegida, ejecutar `git init`

<br>

> [!NOTE]
> Este comando creará la carpeta oculta `.git` e inicializará el repositorio local de forma correcta

<br>

### ✧ Clonación

Clonar un repositorio sirve para bajar a la computadora un proyecto que ya existe en GitHub. A diferencia de empezar un proyecto desde cero, el clonado descarga la carpeta completa con sus archivos, todo su historial de commits y deja el proyecto vinculado automáticamente con GitHub.

Para clonar un repositorio:

- Copiar la direccion URL en GitHub.
- Abrir en la terminal la carpeta destino en la máquina donde se quiera guardar el proyecto.
- Escribí `git clone` seguido de la URL copiada:
  
  ```
  git clone https://github.com/usuario/nombre-del-repositorio.git
  ```

- Por ultimo, para empezar a trabajar hay que entrar a la nueva carpeta creada:

  ```
  cd nombre-del-repositorio
  ```

<br>

## 📂 Estados del repositorio

Para entender cómo se mueve un proyecto en Git hay que conocer las **tres áreas de trabajo** que gestiona:

1. **Working Directory:** Es la carpeta real en el ordenador donde se crea, edita o borran archivos.
2. **Staging Area:** Espacio intermedio donde se colocan los archivos que ya están listos para la próxima versión.
3. **Repository:** El directorio interno donde Git almacena de forma permanente todos los *commits* y versiones del proyecto.

<br>

Los comandos de inspección permiten saber exactamente qué pasa entre estas áreas.

- `$ git status`  
  Comprueba el estado de los archivos en la carpeta respecto al ultimo commit (cambios, nuevos/eliminados o en que rama se está). Se utiliza antes de agregar archivos, después de agregarlos para confirmar que están en verde, y antes de hacer un commit o subir cambios.

- `$ git diff`  
  Muestra exactamente línea por línea qué se modificó, qué se agregó y qué se eliminó entre dos versiones.

  - `git diff` -- compara lo que se modifico en la carpeta de trabajo contra el ultimó commit guardado.
  - `git diff --staged` -- muestra el detalle exacto de las líneas añadidas o borradas en los archivos que ya están en el área de preparación, para revisarlos justo antes de comitear.
  - `git diff rama1 rama2` -- se utiliza para comparar dos ramas enteras y ver qué archivos o líneas difieren entre sí antes de unirlas

- `git log`  
  Muestra la lista histórica de todas los commits guardados en el repositorio con todos los detalles (quién hizo el cambio, cuándo y qué mensaje escribió). Se utiliza cuando es necesario ver qué cambios se hicieron en los últimos días o buscar el código identificador de una versión previa.

  - `git log --oneline` -- muestra el historial compactado en una sola línea por commit.
  - `git log --graph` -- dibuja las ramas y uniones con asteriscos y líneas en la terminal para ver cómo se bifurcó el desarrollo.

- `git branch`  
  Muestra la lista de todas las ramas locales existentes y resalta con un asterisco o color en cuál se esta parado. Se utiliza siempre que se quiera cerciorar en qué línea de desarrollo se esta trabajando antes de hacer modificaciones.

<br>

## 📂 Añadir archivos al Staging Area

- `git add`  
  
  Al editar o crear archivos, esos cambios solo existen en el disco local. Tras ejecutar `git add`, no se esta creando un commit definitivo ni alterando el historial permanente aun. Lo que hace es **preseleccionar y preparar** de manera provisional qué archivos y líneas exactas van a formar parte del próximo commit.
  
  - `git add .` -- el punto (`.`) hace referencia al directorio actual. Toma **todos** los archivos nuevos y modificados del proyecto y los envía juntos al Staging Area.
  - `git add archivo.extension` -- pasa al Staging Area **únicamente el archivo especificado**. Conviene usarlo cuando se modificaron varios archivos del proyecto pero se quiere guardar un commit atómico que solo contenga los cambios de ese archivo puntual.

<br>

> [!IMPORTANT]
> Para comprobar lo que va pasando en cada paso se utiliza `git status`. Antes de `git add` los archivos aparecen listados en color **rojo** pero luego de ejecutarlo esos archivos pasan a figurar en color **verde** bajo el apartado *"Changes to be committed"*.



<br>

## 📂 Confirmar los cambios

Tras el paso anterior, los cambios están preseleccionados y empaquetados para la próxima versión, pero **todavía no forman parte del historial permanente**. Por eso tras el `git add` se debe hacer un "punto de guardado" (*commit*).

- **Guardar la versión localmente**
  
  - `git commit -m "descripción"` -- este genera un código único (*Hash*) que identifica de forma irrepetible esa versión. Los cambios se almacenan permanentemente dentro de la carpeta LOCAL oculta `.git`. Y aunque el repositorio en GitHub ya esté creado, este commit **solo existe en LOCAL**.


- **Enviar los cambios**
  
  - `git push -u origin main` -- en este paso Git comprime y transfiere los objetos y commits a los servidores de GitHub a través de la conexión autenticada (por Token, SSH o navegador).  
  
  <br>

  > [!NOTE]
  > - `-u` -- crea un enlace permanente entre tu rama local actual y la rama correspondiente en GitHub.  
  > - `origin` -- alias estándar que se le asigna a la URL del repositorio en GitHub. Es para no tener que escribir la dirección web completa cada vez que se suba o baje código.  
  > - `main` -- Es el **nombre de la rama específica** al que se esta subiendo el commit.

-----------------------

## **6**. Branches / Ramas

Las ramas se pueden definir como “punteros” para cada uno de los cambios o versiones que se quieren armar en el proyecto o desarrollo.<br/>
Cada RAMA representa una LÍNEA INDEPENDIENTE de desarrollo.

Para realizar este manejo de versiones Git parte de una rama principal `main/master`, de la cual se desprenden todas las demás ramas que se pueden crear.

&nbsp;
![Branch](https://github.com/user-attachments/assets/1635b168-0839-4e08-8eb0-e8550441dc94)

&nbsp;
- `$ git branch` -- permite conocer en qué rama nos encontramos ubicados.

- `$ git branch nueva-rama` -- permite CREAR una nueva rama.

- `$ git checkout nombre-rama` -- permite CAMBIAR a una rama existente (Git antiguo).

- `$ git switch nombre-rama` -- permite CAMBIAR a una rama existente (Git moderno).
  
- `$ git merge` -- permite UNIFICAR dos ramas en una sola, para que ambas tengan los mismos archivos sin diferencias.

      $ git merge rama-origen rama-destino
  
  > Se debe estar en la rama a ACTUALIZAR para unificar.

- `$ git branch -m nombre-rama-ACTUAL nombre-rama-NUEVA` -- permite cambiar el NOMBRE de una rama.

- `$ git branch -d rama-a-eliminar` -- permite ELIMINAR una rama creada.

   > En caso de estar ubicados en la misma rama a eliminar, primero se debe cambiar a otra rama porque sino no lo permite.

&nbsp;

## **7**. Repositorios Remotos

........... FALTAN  !!!!!!!! ⚠️⚠️⚠️⚠️

&nbsp;
- `$ git push` -- permite PASAR el archivo al repositorio REMOTO.

      $ git push origin rama-a-pushear

   `origin` es el nombre del repositorio remoto por defecto<br/>
   `main` es por defecto el nombre de la rama (tambien podría ser master)

&nbsp;
> Hay que posicionarse dentro de la carpeta / directorio del proyecto

- `$ git pull` -- COPIA solo cambios puntuales en una rama puntual, para no copiar todo de nuevo.

      $ git pull origin rama-a-pullear

   `origin` es el nombre del repositorio remoto por defecto<br/>
   `main` es por defecto el nombre de la rama (tambien podría ser master)

&nbsp;
> [!NOTE]
> `origin` es simplemente un alias o apodo para la URL del repositorio remoto de donde se clona el proyecto.<br/>

> Es solo un nombre por convención que Git lo crea automáticamente. Se puede cambiar, pero la mayoría lo deja así por simplicidad.




git remote add <nombre> <url>	Añade un repositorio remoto.	
git push <nombre-remoto> <rama>	Envía cambios locales al repositorio remoto.	
git pull <nombre-remoto> <rama>	Obtiene los cambios de un repositorio remoto y los fusiona con la rama actual.	
git fetch <nombre-remoto>	Descarga cambios del remoto sin fusionarlos.	
git remote -v	Muestra los repositorios remotos configurados.