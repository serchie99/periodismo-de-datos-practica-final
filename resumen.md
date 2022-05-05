# Resumen de la asignatura
Creado por Sergio Real Rivas

En el siguiente documento vamos a realizar un resumen de todos los contenidos de la asigntura y los sucesivos trabajos que hemos ido entregando en aula global.

## Instalación de un programa de emulación de la terminal

Dado que mi ordenador pertenece a Windows he tenido que instalar dos programas diferentes de emulación de la terminal necesario para entregar las prácticas del curso. Concretamente, WSL (Windows Subsystem for Linux) y posteriormente Cygwin.

### WSL: instalación de ubuntu

Primero tuvimos que instalar la terminal WSL. Para ello se hace con PowerShell una terminal creada por la propia compañía de Windows.
El procedimiento es el siguiente: (1) Abres una nueva sesión como administrador. (2) Ejecutas el comando `wsl --install -d Ubuntu`. Con esto le decimos que con el comando `(--install)` queremos instalarlo y con la distribución `(-d)` Ubuntu. (3) Reinicias el ordenador. (4) Instalas Ubuntu desde descargas e introduces el usuario y la contraseña para crear un usuario UNIX, que basicamente es el usuario administrador.

### Cygwin: Unix en Windows

Una vez que instalamos WSL, procedimos a instalar Cygwin. Tuvimos que descargarla desde su propia página [web](https://www.cygwin.com/). 
El procedimiento fue: (1) Descargas el programa y lo ejecutamos. (2) Lo primero que veríamos sería que el propio programa preguntaba desde dónde queríamos instalarlo y teníamos que seleccionar la opción de "instalar desde internet". (3) Luego tuvimos que elegir en dónde queriamos instalarlo y establecimos la ruta que viene por defecto. (4) Elegimos el "mirror" y seleccionamos el dominio `.es` al estar en España. (5) Y por último, instalamos los paquetes `libcurl4`, `wget`, `ca-certificates-letsencrypt`, `lynx`, `nano` y `openssl`.

## Configuración del programa

Una vez instalados ambos programas, configuramos algunos parámetros para facilitar su uso. 

### Establecer un alias

Primero teníamos que crear un alias en la terminal para evitar tener que escribir toda la ruta de nuestra carpeta. De esta manera, en vez de escribir `cd ‘/mnt/c/Users/usuaria/Documentos/Apuntes/Periodismo de Datos/’`, escribimos `micasa` y el propio programa nos llevaría a esta ruta. 
Para ello, editamos el archivo de configuración de Bash y en la línea de comandos que aparece escribimos `echo` y enviamos la salida con `>>` al final del archivo `.bashrc`: `echo “alias micasa=“cd ‘/mnt/c/Users/usuario/Documentos/Apuntes/Periodismo de Datos/’” >> $HOME/.bashrc`. De esta manera, cada vez que accedamos a cualquiera de la dos terminales y escribamos el alias nos reconducirá de manera automática a la ruta que hayamos asignado anteriormente. Si queremos comprobar el archivo de configuración del alias tenemos que utilizar `cat $HOME/.bashrc` y lo editamos `nano $HOME/.bashrc`.

### Cambiar la home de Cygwin a la de Windows

Desde la terminal Cygwin cambiamos la ruta de "casa" de nuestro usuario para que sea la propia de Windows. 
Para ello, editamos el archivo `nsswith.conf` con `nano`: `nano /etc/nsswith.conf` poniendo `db_home: windows` al final del archivo. Guardamos con CTRL+O y cerramos con CTRL + X y después cerramos el programa y volvemos a entrar. Esto nos servirá para que se actualice. Finalmente con el comando `pwd` tenemos que comprobar que nos aparezca `/cygdrive/c/Users/usuario`.

### Configuración de git

En esta parte tuvimos que configurar el usuario de GitHub en la terminal. Esto ayuda a vincular los cambios que se produzcan en nuestros archivos locales con mi propio repositorio que encontramos en GitHub cada vez que crease una práctica. 
Para ello: (1) Abrimos la terminal y escribimos el comando `git config --global user.name nuestrousuario` que en este caso "nuestrousuario" es "serchie99". (2) Escribimos el comando `git config --global user.email correogithub` que en este caso una vez más sería el correo que hemos utilizado para creear la cuenta en GitHub.

## Configuración de un programa de edición de texto

Lo siguiente que hicimos fue aprender a editar los textos de nuestros archivos desde la propia terminal.
Para ello, utilizamos el programa de edición de texto de Linux que es`nano`. Para que funcione es necesario ajustar la resolución de la pantalla del ordenador que utilizo y así conseguimos que aparezca el número de líneas.
El procedimiento consiste en utilizar los siguientes comandos: (1) `nano $HOME/.nanorc`. (2) #Ajustar el texto de pantalla. (3) `set softwrap`. (4) #Numerar las líneas. (5) `set linenumbers`
Con esto conseguimos ajustar el texto correctamente

Posteriormente, para configurar el programa de edición de texto en Cygwin.
Para ello: (1) copiamos el archivo de configuración de `nano` con `cp /etc/nanorc .nanorc`. (2) Lo editamos el archivo con `nano .nanorc`. (3) Buscamos con CTRL + W “linenumbers” y en la línea (`# set linenumbers`) quitamos la #. (4) Buscamos con CTRL + W “softwrap” y en la línea (`# set softwrap`) quitamos la #

## Configuración y funcionamiento de un gestor de paquetes/programas del emulador de la terminal

Según [Wikipedia](https://es.wikipedia.org/wiki/Sistema_de_gesti%C3%B3n_de_paquetes) "es una colección de herramientas que sirven para automatizar el proceso de instalación, actualización, configuración y eliminación de paquetes de software". 
Es decir, para instalar programas y herramientas que provienen del sistema UNIX. 
Con Ubuntu por ejemplo, es `apt` (viene instalado por defecto) y Cygwin tiene `apt-cyg` (tienes que instalarlo). Para instalar este último tenemos que usar (1) `lynx -source rawgit.com/transcode-open/apt-cyg/master/apt-cyg > apt-cyg` y (2) `install apt-cyg /bin`.

## Versión del lenguaje de Shell utilizado

Para consultar la versión del lenguaje de Shell utilizado en cualquiera de las dos termianles, tenemos que utilizar la variable de entorno `$0` y la consultamos con `echo $0, a lo que nos responderá qué Shell usamos que será Bash.
Para comprobar la versión de lenguaje de Bash hay dos maneras: o usamos la variable de entorno `$BASH_VERSION`, con `echo`; o mediante el propio `bash`, especificamos la opción `--help`: `bash --help`

## La variable de entorno Path

Para consultar la variable de entorno `$PATH` tenemos que usar `echo $PATH`. La terminal nos devolverá las rutas en las que se encuentran los programas instalados que puede ejecutar la terminal. Separados por dos puntos `(:)` aparecen los directorios donde la terminal va a buscar los programas para poder ejecutarlos cuando lo indiquemos así a través de los comandos.

## Comandos utilizados

- `pwd`: donde estoy 
- `ls [ruta del directorio]`: ruta del directorio
- `cd` = cambiar de directorio 
- `mv  [origen] [destino]`: comando para mover archivos o para renombrar archivos o directorios. 
- `cp [origen] [destino]`: para copiar un archivo o carpeta a otra
- `man`: es el comando del manual de la terminal. `Q` para salir del manual.
- `mkdir [nombre carpeta]`: comando con el que creamos una carpeta
- `cat`: con este comando visualizamos un archivo desde la misma terminal. 
- `echo` = la terminal con este comando nos lo devuelva un texto. Por ejemplo, si queremos saber cuál es nuestra variable de entorno home debemos poner `echo $HOME`. 
- `env` = visualizamos con este comando todas las variables de entorno. Al ser tantas debemos escribir `env | less` para ver de manera más asequible este enorme listado. 
- `nano` = se abre con el  programa de edición de texto nano que nos permite crear o editar los textos 
*Comandos Git = aunque muchos se han explicado con anterioridad, en este punto detallamos algunos nuevos y recordamos el resto.* 
- `git clone` = comando con el que clonamos un repositorio remoto en nuestro directorio local.
- `git config` = con este comando definimos los valores de configuración de git.Como hemos visto anteriormente: `git config --global user.name`;  `git config --global user.email`;  `git config --global set-editor nano`.
- `git status` = comando que nos muestra el estado del directorio de trabajo y del área de entorno. Nos permite ver los cambios que se han realizado, los que se han reparado o no, en los que Git no puede vincular etc. 
- `git add “nombre-archivo”` o `git add .` = este comando nos permite añadir los cambios del directorio al entorno de ensayo, es decir con este comando le dices a Git las actualizaciones que quieres realizar. A través del argumento `.` añades todos los nuevos archivos, cambios etc. 
- `git commit -m “lo que comiteamos” ` o `git commit .` = con este comando realizamos el commit es decir el cambio que hemos realizado se verá con esta acción en GitHub. A través del argumento `.` añades todos los nuevos archivos, cambios etc. 
- `git push` =  se usa este comando para cargar el contenido del repositorio local al repositorio remoto de Github (en nuestro caso) . Este paso es el último que realizaremos para actualizar los cambios que veíamos en `Git Status`.
- `git pull` =  permite actualizar los contenidos de los repositorios. 
- `git remote -v`






























