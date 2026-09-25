
&nbsp;
## **1**. Configuración inicial

Tras instalar Git en el sistema, se deben hacer algunas cosas para personalizar el entorno. Es necesario hacer estas cosas solamente una vez en la computadora LOCAL y se mantendrán entre actualizaciones.<br/>  
> Se pueden cambiar en cualquier momento volviendo a ejecutar los comandos correspondientes.

&nbsp;
- `$ git config` -- permite obtener y establecer variables de configuración que controlan el aspecto y funcionamiento de Git.

- `$ git config --global user.name "Nombre"` -- configura el nombre de usuario globalmente.

- `$ git config --global user.email "email@example.com"` -- configura el correo electrónico globalmente.

  > Esto es importante porque los "commits" de Git usan esta información, y es introducida de manera inmutable en los commits que se envían. Sólo se necesita hacer esto UNA vez si se especificas la opción `--global`.

- `$ git config --list` -- muestra todas las propiedades que Git ha configurado.

&nbsp;

## **2**. Inicialización y Clonación

- `$ git init` -- inicializa un nuevo repositorio Git en el directorio LOCAL actual.	
  
- `$ git clone` -- COPIA TODO el repositorio tal cual está y se descarga. Se suele utilizar para copias de CERO

      $ git clone URL-repositorio
  
  > Primero se debe crear el directorio LOCAL donde se descargará y se abre en la terminal.

&nbsp;

## **3**. Estados del repositorio

- `$ git status` -- comprueba el estado de los archivos en la carpeta (cambios, nuevos o eliminados).

- `$ git diff` -- permite conocer las diferencias entre dos ramas y muestra las diferencias entre sus contenidos.

      $ git diff rama-uno rama-dos
  
  > EL ORDEN IMPORTA, en el ejemplo anterior muestra lo que hay en rama-dos y no está en rama-uno. <br/>
  > Si se realiza al reves se vera lo contrario.

- `$ git log` -- muestra el historial de TODOS los commits del proyecto (quién hizo el cambio, cuándo y qué mensaje escribió)  
        `$ git log --oneline` -- muestra el historial resumido en una sola línea por commit.

&nbsp;

## **4**. Añadir archivos al Staging Area

> [!NOTE]
> El Staging Area es un archivo sencillo, generalmente almacenado en el directorio de Git, que recopila información acerca de lo que va a estar presente en la próxima confirmación, listo para ser enviados al repositorio de Git.

- `$ git add` -- agrega de manera PROVISORIA el archivo al repositorio.

   `$ git add archivo.extension` -- agrega el archivo seleccionado  
   `$ git add .` -- agrega TODOS los archivos aun NO subidos

&nbsp;

## **5**. Confirmar Cambios

Cuando se hacen cambios en los archivos, no se guardan automáticamente en el historial. Por eso tras el `$ git add` se debe hacer un "punto de guardado" (commit).

&nbsp;
- `$ git commit -m “MENSAJE”` -- agrega de manera DEFINITIVA el archivo al repositorio, mas un mensaje sobre el cambio realizado.
  
  > Con esto los cambios quedan guardados en el historial del REPOSITORIO LOCAL, en la propia máquina.

&nbsp;
> [!IMPORTANT]
> Para subirlo a un repositorio remoto (GitHub) debemos usar `$ git push` así los cambios se reflejan en el repositorio online.

&nbsp;

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

&nbsp;

## **Referencias**

▶️ [Git Add + Git Commit + Git Push -Todo Code-](https://youtu.be/osO_eYMIKxM?si=a4s96ESawDaCkmCN/)<br/>
▶️ [Github Access Token -Todo Code-](https://youtu.be/2nzOI-ynXF4?si=-FOlRTch5Bad-bF5)<br/>
▶️ [Git Clone + Git Pull -Todo Code-](https://youtu.be/IWnW0svZ9JQ?si=OecPx5YavLWl-ScZ)<br/>
▶️ [Branches (Ramas) -Todo Code-](https://youtu.be/gjKKtQVVCZU?si=lZ7d840yuPmrOns1)<br/>
▶️ [Diff y Merge / Trabajando con branches -Todo Code-](https://youtu.be/W8rwULnu9nA?si=AfwbtAhCLFcRzoDl)<br/>

&nbsp;

📚 [Listado de comandos de Git](http://codigoelectronica.com/blog/listado-de-comandos-de-git)<br/>
📚 [Fundamentos de Git](https://git-scm.com/book/es/v2/Fundamentos-de-Git-Obteniendo-un-repositorio-Git)<br/>

&nbsp;
