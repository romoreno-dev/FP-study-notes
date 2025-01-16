
# A. INSTALACIÓN Y CONFIGURACIÓN
## A.1. Introducción

Linux fue concebido por Linus Torvalds, que empezó trabajando sobre el código fuente de Minix (pequeño UNIX desarrollado por Andy Tanembaum) para lograr un Unix mínimo, capaz de ejecutar al menos un shell. 

Primero fue la versión 0.02 (la 0.01 nunca llegó a ser compilada). La primera versión estable del kernel (1.0) Linux fue evolucionando a ritmo vertiginoso. 

La mascota oficial de Linux se llama Tux, fue creada por Larry Ewing en 1996. 
## A.2. Distribuciones

Una distribución es un sistema GNU/Linux formado por: el kernel (licenciado bajo GPL, General Public License), un conjunto de aplicaciones de sistema y una colección de programas de usuario listos para instalar. 

Muchísimas iniciativas han creado su propia distribución naciendo, evolucionando, derivando en otras distribuciones. La diversidad permite que diversas personas puedan usar GNU/Linux de acuerdo a sus necesidades. 

Entre las más usadas: Debian, Ubutu, Linux Mint, Linux Manjaro, Kubuntu, Fedora, Tails, OpenMandriva, Gentoo Linux, Puppy Linux, PCLinuxOS, Solus, elementary_OS, openSUSE, Slackware, Sabayron Linux, SLAX, CentOS.

Un minuto de silencio para que recordemos al difunto y gran Guadalinex (2004-2018). (Y a GnuLinEx de Extremadura). 
## A.3. Licencias de software

El germen de todo GNU/Linux son las licencias de software libre. 
Public General License (GNU GPL) es licencia creada por la Free Software Foundation en 1989. Busca garantizar la libertad de compartir y modificar el software. 

Dentro de las licencias libres hay dos opciones:
- **Dominio público**: El software está disponible para otras personas pero no el código fuente.
- **Licencia libre**: El código fuente está a disposición. Otros programadores pueden modificar, mejorar o adaptar el software a sus necesidades.

El software publicado bajo GPL debe cumplir cuatro libertades:
- Libertad 0. Ejecutar el programa bajo cualquier propósito
- Libertad 1. Estudiar el funcionamiento del programa y adaptarlo a las necesidades
- Libertad 2. Redistribuir copias
- Libertad 3. Mejorar el programa y luego distribuirlo. 
El resultado debe seguir siendo libre. GPL Versión 3 (2007) es la versión en vigor.

Las licencias **Creative Commons** están inspiradas en GPL pero buscan facilitar el uso y la distribución garantizando la autoría.
## A.4. Instalación de una distribución: Ubuntu

### A.4.1. Características y versiones

"Linux for human beings"

- Una de las distribuciones Linux más populares
- Ofrece un número cuidadosamente seleccionado de paquetes provenientes de Debian
- Conserva eficaz sistema de almacenamiento de paquetes permitiendo instalación y desinstalación de un modo fácil y limpio. 
- Viene con un número pequeño de aplicaciones fundamentales de alta calidad
- Entorno de trabajo cuidado y robusto
- Publicación regular cada seis meses. Con soporte por Canonical durante nueves meses. Las LTS con soporte durante cinco años en escritorio y servidor.

### A.4.2. Requisitos hardware del sistema

GNU/Linux tiene un asistente que guía el proceso de instalación. 
Requisitos mínimos... (Por ejemplo para Ubuntu Desktop 20.04 LTS):
> 1. Microprocesador de doble núcleo 2Ghz
> 2. RAM 4GB
> 3. 25 GB de espacio en disco duro
> 4. Puerto USB o DVD
> 5. Acceso a internet recomendable

### A.4.3. Instalando el sistema

Ubuntu Desktop (escritorio), Ubuntu Server (servidores), Ubuntu for IoT board (Internet de las cosas), Ubuntu Cloud (servidor en nube) (Workstation (estación de trabajo) y Server (servidor))

Existe asistente que guía todo el proceso de instalación.
En forma automática Ubuntu crea una única partición incluyendo en ella el área de intercambio (swap). De forma manual debe analizarse qué particiones se crearan.
Buena práctica es separar en particiones independientes la /home del sistema / y, respecto a crear partición swap, hay que considerar las características del equipo y su uso.

##### Pasos instalar Ubuntu

- Probar o instalar
- Indicar distribución del teclado
- Indicar aplicaciones que se desean instalar
- Particionamiento del sistema
- Zona horaria
- Cuenta de usuario
- Reiniciar ahora
## A.5. Primeros pasos

### A.5.1. X-Windows

**X-Windows** (Sistema de ventanas) es el entorno gráfico usado por sistemas Unix. Desarrollado a mediados de los 80 en el MIT ha dado lugar a diversos sucesores en su grupo de desarrollo. 
Proporciona una GUI con el manejo de ventanas, cuadros de diálogo, botones y menú.

El protocolo de comunicaciones no es el más óptimo. Por eso sistemas como **Wayland** están comenzando a implementarse por defecto en algunas distribuciones Linux. El no soporte en Wayland de los drivers de NVIDIA evita su uso al 100%.

Ambos son interfaces gráficas completas compuestas por dos elementos principales: 
- **Servidor**: Mostrar visualmente los elementos de la pantalla de forma independiente al sistema operativo
- **Gestor de ventanas**: Gestión y administración de las ventanas mostradas para las aplicaciones, apariencia, creación, colocación en pantalla.

El diseño en dos partes lleva a diferentes implementaciones de gestores de ventanas. El servidor es altamente portable y permite usar los tres principales **entornos de escritorio** GUI:
- GNOME (simplicidad)
- PlasmaKDE
- Xfc
### A.5.2. Intérprete de comandos o shell

Es una interfaz entre el usuario y el sistema que permite interactuar directamente con el sistema y los ficheros de configuración.

Recibe órdenes del usuario a través de la línea de comandos, las interpreta, las ejecuta y muestra su resultado. 

Se muestra `romoreno-dev@ubuntu-VirtualBox~$`  el nombre de usuario, el nombre del equipo, el directorio actual (~ es el directorio personal del usuario /home/romoreno-dev), el tipo de usuario $ (normal) # (administrador del sistema). 

- Para ejecutar una tarea de forma puntual como administrador puede usarse `sudo <comando>`
- Para ejecutar múltiples tareas se puede obtener un intérprete de administrador o root ejecutando `sudo bash` o `su`
- Para salir de root: `exit`

De forma predeterminada la contraseña de root está bloqueada en Ubuntu. Debe establecerse una contraseña con `sudo passwd root`
Se puede deshabilitar root con `sudo passwd -dl root`

Importante saber que existe el manual: `man apt-get`

https://blog.desdelinux.net/mas-de-400-comandos-para-gnulinux-que-deberias-conocer/

### A.5.3. Estructura de directorios

Árbol jerárquico de directorios compuesto por ficheros. Se forma mediante un sistema de ficheros raíz (file system root) y un conjunto de ficheros montables. 

El sistema de ficheros es una estructura de directorios completa. Para usarlo hay que montarlo, es decir, enlazarlo a la estructura de directorios ya existente.

Los sistemas de ficheros se montan automáticamente cada que se inicia el sistema operativo. Al conectarse el usuario, se encuentra un único árbol de directorios formados por los sistemas de ficheros montados en ese instante. 
## A.6. GNOME. Personalización

Este apartado sobra bastante...
### A.6.1. Escritorio GNOME

1. Barra de menús
	1. Aplicaciones
	2. Menú aplicaciones
	3. Calendario y notificaciones
	4. Menú de acceso universal
	5. Menú del sistema
2. Lanzador (Dock. Acceso rápido a las aplicaciones)
3. botón aplicaciones
4. Fondo de escritorio
### A.6.2. Iconos de escritorio

Aparecen por defecto la carpeta personal del usuario y la papelera. (Herramienta Retoques, Gnome Tweaks)

Se pueden crear accesos directos (lanzadores) a determinados programas o aplicaciones. Al pegar aparece el icono de la aplicación pero hay que permitir que se ejecute haciendo click con el botón derecho y pulsando en Permitir lanzar. 
También en Preferencias>Comportamiento>Mostrar acción para crear enlaces simbólicos y entonces aparecerá "Crear enlace". 
### A.6.3. Configuración visual

- **Fondo de escritorio**: Se puede afinar con opciones de su estilo... Centered, Scaled, Spanned, Stretched, Wallpaper, Zoom.
- **Resolución de pantalla**: Orientación. Resolución. Escala. Escalado fraccionario. 
- **Luz nocturna**
- **Temas**
- **Tipografías**
- **Fondo de pantalla de bloqueo**

### A.6.4. Barra de menús

- Esquina activa de la vista de actividades
- Calendario y notificaciones
- Menú de acceso universal

### A.6.5. Lanzador

El equivalente al "lanzador" es la "barra de tareas"
El **lanzador** es una barra de iconos situada en el lado izquierdo de la pantalla al iniciar sesión que ofrece acceso rápido a las aplicaciones usadas con más frecuencia.

**Soporte de idiomas**.
## A.7. Repositorios

Ubuntu utiliza una tecnología de instalación de aplicaciones basada en paquetes, cada paquete es un archivo comprimido con extensión ".deb" que contiene información del producto, archivos de programa, bibliotecas, iconos, documentación y scrip de configuración.

Los gestores de paquetes usan esos archivos para localizar, instalar, actualizar y eliminar programas.

Algunos paquetes se instalan sin más, pero a veces es necesario que haya otros relacionados (dependencias). El gestor de aplicaciones resolverá sus dependencias, de modo que instalará también cualquier otro que sea necesario. 

Un **repositorio** es un sitio web que contiene paquetes de software. Las herramientas de instalación de programas automáticamente localizan y obtienen los paquetes desde estos repositorios. Este método evita tener que buscar manualmente aplicaciones o actualizaciones. 

El software de los repositorios Ubuntu se cataloga en:
- **Main** (Soportado oficialmente y mantenido por Canonical): Paquetes soportados por equipo de desarrollo de Ubuntu por 18 meses como mínimo. 100% libre.
- **Universe** (Mantenido por comunidad): 15000 paquetes, también 100% libre procedentes de Debian y adaptados a Ubuntu.
- **Restricted** (Copyright restringido): Paquetes no libres que Ubuntu selecciona por considerar  importantes (drivers privativos para tarjetas de red, modem, tarjetas de vídeo...)
- **Multiverse** (Software no libre): No son libres al 100% o sufren algún tipo de restricción. 

Es habitual que estemos conectados a varios repositorios por lo que el sistema mantiene un índice general con la lista de programas disponibles sumando todos los repositorios. 
Si un mismo paquete se encuentra en varios repositorios, listará el que tenga la versión más reciente. 

### A.7.1. Añadir repositorios externos

Si no está en los repositorios de Ubuntu o Canonical puede ser porque son programas no libres o no de código abierto, porque los terceros no han contactado con Canonical para incluirlos en los repositorios o porque no hay versión estable.

Para incluir la dirección de un repositorio:

##### **Editar el archivo sources.list**. 
En el archivo /etc/apt/sources.list se indica dónde se deben buscar los paquetes que se instalan con los gestores de paquetes.

Se añade al final del documento la dirección del nuevo repositorio y la de las fuentes "deb" y "deb-src" 

```
deb hhtp://dirección_del_servidor/nombre_carpeta nombre_de_version (main / universe / multiverse / main restricted)_
```

##### De forma gráfica con Software y actualizaciones

Pa que decir na.
## A.8. Actualizaciones

### A.8.1. Actualización de los repositorios

Los repositorios varían a lo largo del tiempo añadiendo nuevos paquetes o versiones de los mismos. 

Se ejecuta comando para actualizar la lista de paquetes disponibles en el sistema así como las últimas versiones de los repositorios definidos en /etc/apt/sources.list pero no instala ni actualiza ningún paquete. 

```shell
sudo apt update
```

#### A.8.1.1. Actualizar /etc/apt/sources.list

A veces al usar `apt`, `apt-get` o `synaptic` se puede producir un error porque no está actualizado el archivo que contiene el lugar donde se encuentran los paquetes (sources, fuentes).

La actualización del archivo /etc/apt/sources.list no es una operación que se realice habitualmente, ya que cuando instalamos el sistema en este archivo se incluyen los repositorios correspondientes a la versión que estamos instalando y estos repositorios no se suelen alterar, por lo que con realizar apt update suele ser suficiente para mantenerlos.

Esta operación puede ser útil si el archivo /etc/apt/sources.list ha quedado corrupto o se ha borrado y al intentar instalar algún paquete mediante _apt_ recibimos algún mensaje de error.

```shell
cd /etc/apt
# Copia de seguridad
cp sources.list sources.list_copia
# Eliminar y crear uno vacio
rm sources.list
touch sourceslist
# Se buscan las fuentes que se quieren utilizar  y se incluyen http://repogen.simplylinux.ch.](http://repogen.simplylinux.ch/) 
sudo apt update
```

### A.8.2. Actualización del sistema

###### A través de Actualización de software (/usr/bin/update-manager)
###### Desde el gestor de paquetes Synaptic
```shell
sudo apt install synaptic
```

###### Desde el terminal

```shell
sudo apt upgrade # Actualizacion predeterminada que actualiza solo los paquetes instalados. No podra ser marcada si la ultima version del paquete depende de paquetes no instalados o hay conflictos con los ya instalados
sudo apt dist-upgrade # Resuelve conflicto entre paquetes de forma inteligente
```


###### Comandos apt-get

| **Opción**     | **Descripción**                                                                                                                                     |
| -------------- | --------------------------------------------------------------------------------------------------------------------------------------------------- |
| _update_       | Obtiene una nueva lista de paquetes actualizando las descripciones de los paquetes que hay en la base de datos local.                               |
| _upgrade_      | Actualiza el sistema con actualizaciones disponibles. No elimina paquetes previamente instalados, ni instala paquetes previamente no seleccionados. |
| _dist-upgrade_ | Actualiza todo entre ramas de desarrollo. Con -u vemos TODOS los paquetes a actualizar.                                                             |

###### Actualización de versión de Ubuntu

`dist-upgrade` es el proceso de pasar de una versión de ubuntu a una nueva. Saltar versiones no es recomendable. Debe hacer copia de seguridad de los datos, hacer instalación limpia o actualización progresiva a las nuevas versiones.

Generalmente se recomienda instalar la última versión de ubuntu. La versión puede conocerse ejecutando `lsb_release -a`

## A.9. Instalación y desinstalación de software

Las primeras versiones de Linux no disponía de interfaz gráfica. La forma tradicional de instalación era mediante los paquetes de forma manual en modo terminal. Actualmente se puede hacer con interfaces como GNOME o Plasma DKE en modo gráfico.

El programa puede estar formado por diversos paquetes (dependencias). Los gestores de paquetes facilitan la búsqueda instalación y desinstalación de paquetes de software.

### A.9.1. Synaptic

Gestor de paquetes. No viene instalado por defecto. 
##### Opciones de Synaptic
Secciones, Estado, Origen, Filtros ajustables...
### A.9.2. apt-get o apt

Permiten instalar o desinstalar por líneas de comando usando los repositorios de /etc/apt/sources.list

```shell
# Actualizar repositorios de /etc/apt/sources.list
sudo apt-get update
sudo apt update
# Actualizar el sistema con todas las dependencias
sudo apt-get -f upgrade
sudo apt upgrade
# Localizar paquete o término en alguno de los repositorios. Puede usarse algo asi como php*
sudo apt-cache search <paquete>
sudo apt search <paquete>
# Consultar informacion de un paquete
sudo apt-cache show <paquete>
sudo apt show <paquete>
# Instalar paquete
sudo apt-get install <paquete>
sudo apt install <paquete>
# Desinstalar paquete
sudo apt-get remove <paquete>
sudo apt remove <paquete>
# Desintalar archivos de configuracion
sudo apt-get purge <paquete>
sudo apt purge <paquete>
```


### A.9.3. Aptitude

Gestor de paquetes por líneas de comandos sencillo de utilizar.
Aptitude es mejor que apt. Es un administrador de paquetes de alto nivel. 

```shell
apt install aptitude
aptitude
```

### A.9.4. Ubuntu Software

Forma simple de instalar y desinstalar aplicaciones (Explorar, Instalado, Actualizaciones)
### A.9.5. Snap

Paquete `snap` agrupa una aplicación y todas sus dependencias en un único archivo comprimido que funciona sin modificaciones en muchas distribuciones Linux diferentes.
Es necesario tener el demonio `snapd`. 

Se ve si está instalado:
`snap version`

Los paquetes snap se pueden buscar e instalar desde Snap Store (web o aplicación, conocida también como Ubuntu Software) o desde el terminal.

```shell
# Consultar los snaps instalados
snap list
# Busqueda de Snap
snap find "media player"
# Consultar informacion de un snap
snap info vlc
# Instalacion de un snap
sudo snap install vlc
# Actualizar un snap instalado
sudo snap refresh vlc
# Eliminar un snap
sudo snap remove vlc
```

### A.9.6. Instalación manual

La instalación de una aplicación puede hacerse directamente a partir del código fuente o a través de la aplicación compilada (paquete) que contiene los archivos binarios complementarios y de configuración para ejecutarse.

**A través de paquete**

```shell
# Instalar un paquete
sudo dpkg -i <nombrepaquete>
# Buscar el nombre
dpkg-query -s <paquete>
# Desinstalar
dpkg -r <nombrepaquete>
```

**A través del código fuente**
```shell
# (Primero instalaremos las herramientas de compilacion)
sudo apt install build-essential
```

Después descargar el código fuente. Descompromirlo. Acceder. Ejecutar el script `./configure` (que comprueba características del sistema y crea el Makefile), ejecutar makefile con `make install` . Para desinstalar `make clean`

### A.9.7. Webmin

Webmin es para administrar el sistema a través de un navegador web.
```shell
# Instalacion manual del paquete de la web oficial
sudo dpkg -i <nombre_paquete>
```

O instalación gráfica haciendo click en el paquete y pulsando instalar.
Webmin estará en https://localhost:10000
Tras loguearse, en la página principal se muestra resumen del sistema y se puede acceder a las diversas herramientas de administración.

------
# B. ADMINISTRACIÓN BÁSICA DEL SISTEMA

## B.1. Administración de usuarios

GNU/Linux es multiusuario: Con línea de comandos o con conexiones remota. 
El acceso al equipo/recursos se controla con cuentas de usuarios y grupos.

Tipos de usuarios:
- Root /supernumerario/superusuario. Administrador y dueño del sistema. (Consejo: Solo usar esa cuenta para tareas específicas de administración). Controla la administración de cuentas, ejecuta tareas de mantenimiento, puede detener el sistema, instalar o reconfigurar kernel, controladores...
- Usuarios normales. Inician sesión en el sistema y tienen funcionalidad limitada (en comandos y en ficheros). Solo tienen privilegios completos en su directorio de trabajo o HOME. UID superior a 500 (superior a 1000).
- Usuarios especiales o asociados a servicios. No pueden iniciar sesión en el sistema (cuentas de nologin). Permiten establecer privilegios de un servicio. (Ej.: Servidor web con qué ficheros tiene acceso y, por tanto, qué ficheros están expuestos). "Cuentas del sistema". Ej.: bin, daemon, adm, kp, sync, shutdown, mail, operator, squid, apache. Según la cuenta asumen algún privilegio de root. Se crean con la instalación de Linux o de la aplicación. UID entre 1 y 100.

Los usuarios del sistema tienen:
- Identificador de usuario (UID)
- Identificador de grupo (GID)

root tiene ambos identificadores en 0
usuario creado en la instalación usualmente 1000
el resto mayor a 0 (y usualmente consecutivos a 1000 salvo indicación).

La administración del sistema puede hacerse:
- **Interfaces gráficas**: Interfaz de administración de x-Windows, web de administración webmin
- **Terminal del sistema**: Pueden administrarse totalmente desde aquí. Con gran flexibilidad, con creación de scripts...
- **Ficheros de configuración**: La que mayor control ofrece. Debe conocerse muy bien el sistema.
El usuario root no puede iniciar sesión en entorno gráfico tras la instalación.

### B.1.1. Intérprete de comandos

`adduser`: Añadir un usuario. Pide contraseña, nombre completo, dirección..   

`useradd` : Dar de alta una cuenta sin interacción con el usuario. Indicamos: UID, grupos a los que pertenecerá, descripción...   
- -g: Grupo principal al que pertenecerá el usuario (Debe estar creado)
- -G: Grupo o grupos por comas al que pertenecerá el usuario (Deben estar creado)
- -u: Identificador del usuario
- -m: Directorio del usuario si no existe (nombre del usuario)
- -d: Cambiar directorio por defecto del usuario (/home/usuario)
- -s: Asigna intérprete de comandos al usuario (/bin/bash)
- -c: Comentarios al usuario

`usermod`: Modificar propiedades de una cuenta   
- -c: Añade o modifica el comentario
- -d: Modifica el directorio de trabajo
- -e: Fecha de expiración de cuenta
- -g: Cambia grupo principal
- -G: Establece otros grupos
- -I: Cambia el login
- -L: bloquea cuenta de usuario
- -s: Cambia shell por defecto
- -u: Cambia UID de usuario
- -U: Desbloquea cuenta bloqueada

`userdel`: Eliminar usuario  
`deluser`: Eliminar un usuario. No se elimina su directorio personal.   
Con las flag:
- -r: Elimina cuenta, directorio de trabajo, archivos, directorios
- -f: Elimina cuenta, directorio de trabajo... aunque esté logueado.

 `passwd` cambia contraseña del usuario actual
 `passwd nombre_usuario` cambia contraseña del usuario  

 `chage`: Periodos de vigencia de las contraseñas   
 `id`: Información sobre usuario y grupos a los que pertenece el usuario  
 `who`: Usuarios conectados al sistema  
 `w`: Usuarios y procesos  
`users`: Usuarios registrados en el sistema  
 `su`: Cambio de usuario   
 `sudo`: Comando como root   

 `whoami`: Indica el nombre del usuario   

`groups`: Grupos a los que pertenece el usuario. Grupos principales y secundarios.   
`addgroup`: Añade grupo    
`addgroup usuario grupo`: Añade cuenta de usuario a grupo ya existente    
`groupadd`: Añade grupo    
`groupdel`: Borra grupo    
`groupmod`: Modificar propiedades de un grupo (-g group ID to GID, -n nombre...)    
`newgrp`: Cambia grupo primario del usuario    

```bash
sudo useradd pablo -g usuarios -G profesores -u 2500 -s /bin/bash -m
sudo passwd pablo
su pablo
id
groups
############################
addgroup usuario grupo
```

`pwconv`: Crea y actualiza fichero `/etc/shadow`  
`pwunconv`: Desactiva el fichero `/etc/shadow` (Contraseñas y periodos de vigencia)  
### B.1.2. Ficheros utilizados

Distinguimos entre:  
- Ficheros para guardar información de usuarios y grupos  
- Ficheros con valores predeterminados que usa el sistema.  

**Información de usuarios y grupos se encuentran en los ficheros:**

**/etc/passwd** Listado de todas las cuentas de usuarios.
- Archivo ASCII creado al momento de la instalación
- Una línea para cada usuario

```bash
root:x:0:0:root:/root:/bin/bash
sergio:x:501:500:Sergio González:/home/sergio:/bin/bash
```

- Campo 1: Nombre del usuario, identificador de inicio de segión (login)
- Campo 2: x - Contraseña encriptada del usuario (se está haciendo uso de `/etc/shadow` y, si no, se vería algo así como ghy675gjuXCc12r5gt78uuu6R ). Antiguamente se almacenaban aquí pero este archivo puede ser leído por cualquier usuario (solo modificado por root)
- Campo 3: UID del usuario. 
- Campo 4: GID del grupo
- Campo 5: Comentarios o nombre completo
- Campo 6: home del usuario (tras iniciar sesión)
- Campo 7: Shell que el usuario usa de forma predeterminada

**/etc/shadow**: Contraseñas y periodos de vigencia. Solo puede ser leído por `root`. La línea puede ser como sigue:

```shell
root:ghy675gjuXCc12r5gt78uuu6R:10568:0:99999:7:7:-1::
sergio:rfgf886DG778sDFFDRRu78asd:10568:0:-1:9:-1:-1::
```

- Campo 1: Nombre de la cuenta de usuario
- Campo 2: Contraseña cifrada o encriptada, un `*` indica (nologin)
- Campo 3: Días epoch (desde 1/01/1970) hasta cuando la contraseña se cambió por última vez
- Campo 4: Días que deben transcurrir hasta que la contraseña se pueda a cambiar
- Campo 5: Días tras los cuales se cambia la contraseña (-1, nunca). 
- Campo 6: Días antes de la expiración de contraseña para avisar al usuario
- Campo 7: Días después de la expiración en que la contraseña se inabilita
- Campo 8: Fecha de caducidad de la cuenta. En días epoch
- Campo 9: Reservado

**/etc/group**: Grupos activos y usuarios que pertenecen  

```shell
sergio:x:502:ventas,supervisores,produccion
cristina:x:503:ventas,sergio
```

- Campo 1: Usuario
- Campo 2: Contraseña del grupo
- Campo 3: GID
- Campo 4: Opcional, lista de grupos a la que pertenece el usuario

**/etc/login.defs**

- Número máximo de días que una contraseña es válida PASS_MAX_DAYS
- El número mínimo de caracteres en la contraseña PASS_MIN_LEN
- Valor mínimo para usuarios normales cuando se usa useradd UID_MIN
- El valor umask por defecto UMASK
- Si el comando useradd debe crear el directorio home por defecto CREATE_HOME

##### Archivos de configuración
`.bash_profile`: Alias, variables, configuración del ENTORNO al iniciar sesión.    
`.bash_logout`: Acciones, programas, scripts al cerrar sesión.
`.bashrc`: Como `.bash_profile`, indicando programas o scripts a EJECUTAR

 `pwconv` y `pwunconv`: Desactiva la protección de /etc/shadow

---------

Si no se especifican valores al dar de alta al usuario, usa los valores por defecto.

Estos son:
`/etc/default/useradd`: Shell que se utiliza por defecto, directorio home de los usuarios...    

Al crear usuario, si no se especifica a cual pertenece, se crea grupo con el nombre de usuario siendo este su grupo principal.   

### B.1.3. Interfaz gráfica

En Menú del sistema > Configuración > Usuarios. O en Aplicaciones tecleando "Usuarios".
"Desbloquear" e introducir contraseña. Hay opción de añadir usuario... Se puede seleccionar tipo de cuenta, nombnre completo, inicio de sesión, contraseña. (Gestión limitada).
Para más, instalar las `gnome-system-tools`. Desde la opción Software de Ubuntu, introducir "users and groups" con funcionalidad parecida que ofrece gestión avanzada. 

-------

Menú de ambiente gráfico algún programa para indicar cuáles se deben arrancar al iniciar sesión en modo gráfico. (sesiones, sessions)
Entorno XWindow a utilizar (entorno escritorio KDE, Gnome, manjeador de ventanas Xfce o Twm, con fichero escondido donde vendrá configuración para ese entorno)
### B.1.4. Interfaz web. Webmin

Webmin es una herramienta de configuración de sistemas. Puede acceder por navegador (https://localhost:10000).  Tiene módulos que actúan sobre los archivos de configuración ofreciendo interfaz amigable.
## B.2. Sistema de ficheros

Estructura de árbol jerárquico de directorios (Filesystem Hierarchy Standard). Formado por un sistema de ficheros raíz (file system root) y un conjunto de sistemas de ficheros montables.

Para Linux, todo es un archivo, por eso "montar" y "desmontar". Los volúmenes o particiones son también directorios en los que se monta el volumen o partición (/media). 

```bash
ls -l /dev/sd*  # Todo lo que empiece por sd
```

```shell
brw------- 1 root root 8,  0 May  9 22:47 /dev/sda
brw------- 1 root root 8, 16 May  9 22:47 /dev/sdb
brw------- 1 root root 8, 32 May  9 22:47 /dev/sdc
```

**Tipo de disco duro**: s (SATA Serial Advanced Technology Attachment SCSI Small Computers System Interface) h (IDE Integrated Device Electronics). 
**Letras**: a,b,c... primero, segundo, tercero
**Número**: Número de partición del disco duro (Número entre 1 y 4 a las particiones primarias/extendidas y a partir de 5 para particiones lógicas.)

Administración del sistema de ficheros: Linux empezó con Ext2. Sustituido con nuevas versiones (Ext4 última versión). Otro sistema ReiserFS que evita la pérdida de datos con un journal o registro.

-----------

- Distingue entre mayúsculas y minúsculas.
- La extensión no le importa.
- Los caracteres se pueden escapar con comillas simples, dobles comillas o escapar el espacio en blanco. 
```shell
mkdir 'mis documentos'
mkdir "mis documentos"
mkdir mis\ documentos
```

Se ocultan archivos empezándolos por punto o listándolos en `.hidden`. Y solo se verán al hacer `ls -a`

##### Tipos de archivos
- **Archivos normales**: Texto, datos binarios.
- **Directorios**: Contenedor del resto de archivos.
- **Especiales**:
	- De bloque: Se refieren a dispositivos físicos. Están en `/dev`. `ls -l /dev | grep "^b"`
	- De carácter: Flujo de entrada salida. El terminal. `/dev/null` para desechar.
	- Tubería (Pipes FIFO). 
	- Simbólicos: Puntero a otro archivo o directorio. (Sincronización en la nube)
	- Socket: Pasar información entre aplicaciones.

##### Listar archivos

Al listarlos, indica tipo de archivo y permisos que tiene.
La primera letra es d(directorio), -(regulares), b(de bloque), c(de carácter), l(enlaces simbólicos), n(archivos de red), p(archivos pipe), s(archivos socket).

El número a continuación es el número de enlaces duros a ese archivo.   
Usuario y grupo propietario del archivos.   
Tamaño del archivo.   
Mes, día, hora y minutos.   
Nombre del archivo.

##### Crear directorio
`mkdir midirectorio`
`~`, directorio de inicio `.` directorio actual `..` directorio padre
Para directorios en cadena `-p`

##### Borrar directorio o archivo
`rm`, `rm -r` (recursivo), `rm -f`(forzar borrado), `rm -rf`(forzar borrado recursivo). `rm -rf /` (Borra todo el árbol de directorios)

##### Copiar directorio o archivo
Copiar un archivo en otro: `cp /home/lorenzo/ejemplo1 ejemplo2`
Copiar un archivo en otro directorio: `cp /home/lorenzo/ejemplo1 /home/lorenzo/directorio`

##### Mover directorio o archivo
No es necesario indicarle que lo debe hacer de forma recursiva.
`mv /home/lorenzo/archivo.txt /home/lorenzo/directorio/archivo.txt`

##### Renombrar
`mv /home/lorenzo/archivo.txt /home/lorenzo/otro_archivo.txt`

##### Enlaces duros y simbólicos

- **Enlaces duros: Hace referencia física al mismo nodo de archivo** en el sistema de archivos que el sistema original. Son referencias adicionales. No hay diferencia entre el archivo y el enlace en términos de contenido o ubicación. Tiene también mismo número de inode que lo identifica. Si se elimina un enlace duro el archivo sigue existiendo siempre que haya un enlace duro apuntando a él. 

```shell
ln archivo_original enlace_duro
```

- **Enlaces simbólicos: Es una referencia lógica al archivo.** Contiene ruta del archivo al que apunta. Puede contener cualquier ubicación del sistema de archivos. Tienen su propio numero de inode y se almacenan como archivos separados. Si se elimina el enlace simbólico, el archivo original sigue existiendo siempre que haya al menos otro enlace (duro o simbólico) apuntando a él. Si se elimina el archivo original el enlace simbólico es un enlace roto que no apunta a ningún archivo. 

```shell
ln -s archivo_original enlace_simbolico
```

Los enlaces duros se ven con `ls -l` (Como se ha comentado).
Los enlaces simbólicos se pueden ver con `ls -F` que listará el enlace simbólico con una arroba al final `enlace_simbolico@`
##### Directorios interesantes

| Nombre | Descripción                                                        |
| ------ | ------------------------------------------------------------------ |
| /      | Raíz                                                               |
| /usr   | Archivo existentes (documentación, comandos, juegos, librerías)    |
| /bin   | Comandos que pueden usar todos los usuarios                        |
| /sbin  | Comandos del administrador o roout                                 |
| /dev   | Dispositivos de la máquina                                         |
| /home  | Cuentas de usuarios                                                |
| /lib   | Librerías del sistema                                              |
| /var   | Información variables. Logs del sistema. Correo local...           |
| /tmp   | Temporal                                                           |
| /etc   | Configuración global de programas                                  |
| /root  | Cuenta administrador                                               |
| /boot  | Arranque del sistema                                               |
| /media | Punto de montaje para sistemas de archivos montados localmente     |
| /mnt   | Antiguo punto de montaje para sistemas montados localmente         |
| /proc  | Sistema de archivos virtual de información de procesos y de kernel |
##### Archivos conocidos
- /etc/apt/sources.list: Lista de repositorios para añadir aplicaciones (universe, multiverse)
- /etc/X11/xorg.conf: Entorno gráfico
- /etc/fstab: Acceso a sistemas de archivos del sistema
- /etc/passwd: Uso de usuarios, contraseñas con permisos y grupos que pertenecen a cada usuario. 
- /etc/readahead/boot y /etc/readhead/desktop: Rutas de todos los archivos cargados en memoria durante el inicio del sistema 

### B.2.1. Particionamiento

Define cómo se van a usar los diferentes discos duros del equipo dividiéndolos en particiones permitiendo que funcione como si se tratase de dos o más discos independientes, sin interferir en el otro sistema operativo y coexistiendo en el mismo disco duro. De hecho, ambos sistemas pueden compartir particiones siempre y cuando el sistema de archivos sea compatible en ambos sistemas como exFAT y NTFS en el caso de Linux y Windows.

El particionamiento podría realizarse con herramientas gráficas o con el comando `fdisk`. 

En los servidores se recomienda un sistema RAID para que no se pierda información del sistema en caso de rotura. 

Tipos de particiones:
- **Particiones primarias**: Divisiones primarias del disco. Puede haber entre 1-4. O entre 1-3 y una extendida. La _partición primaria_ puede reconocerse como partición de arranque y tener un sistema operativo (**partición activa**, sistema operativo o gestor de arranque que se va a iniciar). Tienen un sector de arranque (boot) en el primer sector de la partición. Si hay varios sistemas operativos, la partición activa tiene un gestor de arranque para presentar al usuario los sistemas operativos instalados.
- **Partición extendida**: Actúa como primaria. Puede tener varias unidades lógicas en su interior. Se rompe la limitación de cuatro particiones primarias. No soporta un sistema de archivos directamente y no puede crearse sin haber creado previamente una partición primaria.
- **Particiones lógicas**: Se hacen dentro de una partición extendida y se forma con un tipo de sistema de archivos. 

Puede haber las siguientes particiones lógicas:
- **Partición de arranque (/boot):** Almacena núcleo del sistema operativo y archivos de arranque. Necesaria solo en sistema RAID.
- **Partición /swap:** Memoria virtual cuando no hay suficiente RAM para almacenar la información que se procesa. Cantidad recomendada depende de la cantidad de memoria RAM.
- **Partición raíz /**: Contiene el sistema operativo. Punto de montaje del resto de particiones. Cualquier otro archivo del sistema es subdirectorio de esta partición.
- **Partición de usuario /home**: Datos de cada usuario en carpetas independientes. Si no se crea estará por defecto en la partición raíz. Si se hace, se puede actualizar el resto del sistema sin perder información de los usuarios.

| Partición mínima | Partición intermedia | Partición avanzada |
| ---------------- | -------------------- | ------------------ |
| /swap            | /boot                | /boot              |
| /                | /swap                | /swap              |
|                  | /                    | /                  |
|                  |                      | /home              |
###### Bios y particiones
Según placa base el equipo puede tener BIOS Clásica (azul) o BIOS UEFI (interfaz gráfica más desarrollada). Eso ha llevado a poder usar la tabla de particiones de MBR (Master Boot Record) a GPT (GUID Partition Table). Depende del firmware del ordenador.

Enlaces de ampliación que no me da vida para ver:
https://www.muycomputer.com/2018/07/06/bios-y-uefi-guia/
https://www.muycomputer.com/2020/02/05/gpt-mejor-que-mbr-linux-windows/
https://ubunlog.com/uefi-y-ubuntu/
https://help.ubuntu.com/stable/ubuntu-help/disk.html.es
https://gparted.org/display-doc.php?name=help-manual&lang=es
https://ubunlog.com/como-redimensionar-la-particion-de-linux-ubuntu/
#### Herramientas gráficas

Ubuntu Desktop permite administrar el sistema de ficheros desde Sistema > Administración > Utilidad de Discos. Pueden crearse, modificarse o eliminar las particiones de discos duros del sistema. Se puede instalar desde el administrador de software gnome-disk-utility.

Otra herramienta potente es GParted para realizar operaciones que alteren las particiones del disco duro (internas, avanzadas).. Permite planificar los cambios sin que sean aplicados y después confirmarlos. Se puede manipular particiones sin ningún sistema en el PC (GParted Live). Tiene selección de disco duro, barra de espacio, listado de particiones (sí, absurdo escribir esto pero vamos a poner esto en el resumen por si acaso).
#### Comando fdisk

- -l Ver particiones existentes en el sistema `sudo fdisk -l`
- La jerarquía de particiones con `sudo lsblk -fm`
- Ver información de un disco específico `sudo fdisk -l /dev/sda`
- Ver todas las opciones `sudo fdisk /dev/sda` y pulsar m para entrar en la ayuda
- Igualmente `fdisk /dev/sda` y pulsar p
- Eliminar una partición. Seleccionar el disco (`sudo fdisk /dev/sda2`y pulsar d). Introducir el número de la partición y pulsar w para confirmar la acción.

#### Volúmenes lógicos

- El volumen físico (**P**hysical **V**olumen) es cada uno de los componentes físicos que forman parte de un grupo de volúmenes. Puede ser disco entero o particiones. 
- Grupo de volúmenes (**V**olumen **G**roup) es el grupo de volúmenes físicos que trabajan como una única unidad. Similar al disco entero en la partición tradicional.
- Volumen lógico (**L**ogical **V**olumen): Trozos lógicos en los que se puede dividir un grupo de volumen. Similar a la partición tradicional.

Debe instalarse el LVM (Administrador de Volúmenes Lógicos) `apt-get install lvm2`

Ventajas:
- No hay restricción física de espacio de disco (pueden agregarse varias particiones físicas a un único volumen)
- Los volúmenes se redimensionan con comandos sin tener que dar formato o crear particiones en los discos
- Forma sencilla de copiar sus datos (volúmenes lógicos en espejo)
- Operaciones sobre volumen lógico sin desmontar el sistema de archivos.

- `lvmdiskscan`: Discos visibles del sistema
- `pvcreate, vgcreate, lvcreate`: CREAR volúmenes físicos, grupos de volúmenes y volúmenes lógicos respectivamente
- `vgextend, lvextend`: Modificar grupos de volúmenes y volúmenes lógicos respectivamente
- `pvdisplay`: Información sobre dispositivos físicos
- `vgs`, `vgdisplay`: Información sobre grupo de volúmenes
- `lvdisplay`: Información sobre un volumen lógico.

También se pueden gestionar volúmenes lógicos a través de la Webmin.

Ejemplo
```
Volumen físico: /dev/sdb
Grupo del volumen: grupo1
Volúmenes lógicos: archivos (50%VG) y home (50%VG)
```

### B.2.2. Espacio en disco

 `df`: Espacio libre en unidades y particiones. Se pueden usar comandos como
 - `df -h` De forma legible
 - `df -i` Con los i-nodos
 - `df -h /home`: De la partición que se pida (/home en este caso)
 - `df -t ext4`: De las particiones con ese sistema de archivos (ext4 en este caso)

`du`: Espacio que usan los directorios o archivos específicos. -a Cada archivo del directorio local. -ac Cada achivo del directorio local y el total del directorio.  `du -ms /datos`. Espacio de /datos en Megabytes.

- `lsblk`: Información de dispositivos, unidades y particiones
- `blklid`: Información de particiones
- `fsck`: Estado y reparar un sistema de ficheros
- `mkfs`: Formato a partición o volumen lógico

### Repasando comandos...

- Veamos qué discos duros y particiones tiene el sistema `fdisk -l`
- Entremos con fdisk en el segundo disco duro `fdisk /dev/sdb`
- Veamos los comandos disponibles m
- Creemos una partición en el sistema n
- Tipo de partición a crear (primaria p, extendida e)
- Número de partición primaria (1)
- Tamaño de la partición.  Número del último cilindro o tamaño en megabytes (1000M)
- Veamos la tabla de particiones (p)
- Formateemos la partición `mkfs /dev/sdb1`
- Creamos un directorio `mkdir /datos`
- Montamos la partición:
	- Manualmente con `mount /dev/sdb1 datos`. Permite montarlo de forma puntual. Si se reinicia el ordenador se pierde el punto de montaje.
	- automáticamente editando `/etc/fstab`. Esto lo monta con efectos permanentes. Se incluye la línea `/dev/sdb1 /datos ext2 defaults 0 0`. Se montará automáticamente al reiniciar o se puede ejecutar `mount /datos`. 
- Para ver si está montada `mount`  o `df`

## B.3. Permisos

Hay tres tipos de permisos:
- Ejecución (X). Ejecutarlo  o pasar por él
- Lectura (R). Leer o leer ficheros
- Escritura (W). Escribir o crear ficheros

Hay tres tipos de roles. El archivo pertenece al usuario y al grupo:
- Usuario
- Grupo
- Mundo. Los demás usuarios

### B.3.2. Establecer permisos

Los permisos se establecen con el comando `chmod`
`chmod {a, u, g, o} {+, -} {r, w, x} nombre del archivo`

**u:** corresponde al dueño del archivo
**g:** corresponde al grupo
**o** o **a:** corresponde al resto de los usuarios, **a** para todos (all) y **o** para otros (others)

**r:** lectura
**w:** escritura
**x:** ejecución

### B.3.1. Notaciones simbólica, binaria y octal octal

**Notación simbólica**
**+:** autoriza
**-:** desautoriza
**=:** resetea los permisos

Ejempo: 
```bash
# Voy separando por comas
chmod u+rw-x,g+rw-x,o+r-wx *.txt
# Si usuario y grupo tienen los mismos, se lo puedo dar junto
chmod ug+rw-x,o+r-wx *.txt
# O bien
chmod ug=rw,o=r *.txt
```

También se aceptan permisos de **forma binaria y octal**

|  | PERMISO | NOTACIÓN SIMBÓLICA | NOTACIÓN OCTAL |
|---|---|---|---|
| PROPIETARIO (u) | Lectura (r) | u+r ó u-r | 400 (100 ggg ooo) |
|  | Escritura (w) | u+w ó u-w | 200 (010 ggg ooo) |
|  | Ejecución (x) | u+x ó u-x | 100 (001 ggg ooo) |
| GRUPO (g) | Lectura (r) | g+r ó g-r | 040 (uuu 100 ooo) |
|  | Escritura (w) | g+w ó g-w | 020 (uuu 010 ooo) |
|  | Ejecución (x) | g+x ó g-x | 010 (uuu 001 ooo) |
| RESTO (o) | Lectura (r) | o+r ú o-r | 004 (uuu ggg 100) |
|  | Escritura (w) | o+w ú o-w | 002 (uuu ggg 010) |
|  | Ejecución (x) | o+x ú o-x | 001 (uuu ggg 001) |

El **cambio de propietario o grupo** se hace con `chown (propietario):(grupo) (archivo)`. 
Puede actuarse sobre varios fichereros a la vez.

Con -R se pueden dar permisos al directorio y a todos los datos que contenga. Por ejemplo `chmod 777 /datos -R`

Gráficamente: Los permisos pueden cambiarse. Y respecto al grupo, solo se puede cambiar el grupo al que pertenece el archivo. Botón derecho sobre el archivo, permisos.

### B.3.3. Listas de control de acceso (ACL)

Las Listas de Control de Acceso permiten definir conjuntos de permisos a usuarios y grupos de forma individualizada.
Se especifica la asignación de los permisos de lectura, escritura, ejecución `[Tipo]:[Calificador]:ListaPermisos[,...]`

- `getfacl`: Lista de control de acceso a fichero o directorio
- `setfacl`: Asigna, modifica, elimina lista de control de acceso

Para añadir condición al ACL debe usar -m. Para eliminar entrada de la lista ACL a un directorio o fichero -x. Veamos ejemplo
```shell
# Añadimos condición
setfacl -m user:uantonio:rwx miFicherito.sh
# Podemos ver que lo tiene haciendo
getfacl miFicherito.sh
```

Sabemos que el fichero tiene una ACL asociada cuando vemos un + al final de la lista de permisos en vez de un punto.
## B.4. Arranque y parada

Cuando se inicia el equipo primero inicia la BIOS para detectar y acceder al hardware. Después el gestor de arranque (Linux GRUB GRand Unified Bootloader). Si se inicia un sistema GNU/Linux se accede al directorio /boot donde carga el kernel y se ejecuta el proceso `systemd` que inicia los servicios para que el sistema funcione correctamente.

(En versiones anteriores el proceso systemd era sustituido por el proceso init)

### B.4.1. Gestor de arranque de GNU/Linux

Gestor de arranque: Encargado de iniciar cualquier sistema operativo usado en el sistema.
En GNU/Linux ahora es GRUB (Grand Unfiied Bootloader) y antes era LILO (Linux Loader). 
GRUB fue diseñado por Erich Stefan Boleyn. 

Deben tenerse cuidado con las operaciones del gestor de arranque porque podría dañarse el arranque del sistema. Aunque hay utilidades de recuperación de arranque (Super GRUB Disk) que permite realizar operaciones en el MBR (Master Boot Record o Registro de Arranque Principal) de forma segura. 

LILO, GRUB, GRUB 2 (completamente nuevo).
GRUB usa el archivo de configuración `/boot/grub/grub.cfg` que se genera de forma automática al ejecutar el comando `update-grub` o `grub-mkconfig`

La configuración del archivo se hace modificando los scripts de `/etc/grub.d` y del fichero `etc/default/grub`. Cada script se encarga de una parte de la configuración:
- 00_header: Configuraciones de archivo /etc/default/grub, aspectos visuales, tiempo de espera , sistema por defecto
- 01_users: asignar contraseña al gestor de arranque
- 05_debian_theme: imagen de fondo, colores de texto, temas
- 10_linux: kernel y entradas necesarias
- 30_os-prober: entradas para otros sistemas operativos que haya en otras particiones
- 40_custom: agregar entradas de forma manual

Algunos de los parámetros de /etc/default/grub son:
- GRUB_DEFAULT=0 Elegir el sistema operativo (orden en /boot/grub/grub.cfg). Empieza en 0.
- GRUB_SAVEDEFAULT=true Configura por defecto el último sistema elegido por el usuario
- GRUB_HIDDEN_TIMEOUT=0 Segundos que el GRUB espera sin mostrarse en pantalla (por si solo hay un sistema operativo no lo muestra directamente)
- GRUB_TIMEOUT=10 Segundos para que el usuario elija opción (-1, infinito)
- GRUB_TERMINAL=console El sistema arranco en modo consola

En /boot/grub/grub.cfg está menuentry, cada segmento de código delimitado por esa palabra define un arranque en grub.

Más parámetros de Grub: https://www.ticarte.com/contenido/grub-2
Modificar algunos parámetros de GRUB: https://ubunlog.com/cambiar-color-e-imagen-fondo-grub/
Poner contraseña a Grub: https://www.megamanuales.es/como-poner-contrasena-al-grub-2/
Herramienta gráfica Grub Customizer: https://atareao.es/software/utilidades/modificar-el-menu-de-arranque-de-ubuntu/
Systemd-boot, alternativa a Grub: https://www.linuxadictos.com/systemd-boot-una-alternativa-a-grub.html

### B.4.2. Proceso de arranque y parada del sistema (systemctl)

Una vez encontrado el kernel e iniciado este. El sistema operativo se carga, se inicia el hardware, los discos duros se preparan, se asignan direcciones IP y servicios. Se ejecuta el programa  `systemd` (antes `init`). Este programa es un gestor de sistema y servicios para Linux. Trabaja con unidades (servicios, dispositivos, puntos de montaje, particiones, sockets, areas de intercambio).  Algunas operaciones son:
- `systemctl` o `systemctl list-units`: Unidades activas
- `systemctl status`: Estado del sistema. Ej.:  `systemctl status mariadb.service`
- `systemctl failed<code>`: Unidades que han fallado
- `systemctl list-unit-files`: Ficheros de las unidades que están en /lib/systemd/system y /etc/systemd/system
- `systemctl list-units-files --type=target`: Systemd usa el concepto de targets que se nombran con un propósito determinado aunque podrían usar más de una opción al mismo tiempo. Con `init` se usaba el concepto de runlevels (niveles de ejecución 0-6)

Podemos iniciar, parar, comprobar estado, recargar, reiniciar unidades. Basta con poner `systemctl` y los argumentos start, stop, status, restart o reload y la unidad sobre la que se quiere hacer la acción.
`systemctl start sshd.services`
`systemctl stop sshd.services`

- `journalctl`: Registro de systemctl (en cambinación grep o usando flags como -b (arranque), -f (nuevos), `-u <unidad>`, `_PID=<proceso>`...
Uso de systemd: https://atareao.es/tutorial/trabajando-con-systemd/

Más información sobre los targets: https://wiki.archlinux.org/title/Systemd_(Espa%C3%B1ol)#Targets

Ejecución de programas al inicio del sistema mediante /etc/rc.local.  https://ubuntuperonista.blogspot.com/2018/05/como-activo-etcrclocal-con-systemd-en.html

### B.4.2.bis. Proceso de arranque y parada del sistema (init, deprecado)

Ya no se usa. 
El programa `init` inicia el sistema operativo para lo cual:
- Comprueba sistemas de ficheros
- Monta sistemas de ficheros permanentes
- Activa zona de memoria swap
- Activa servicios demonios del sistema
- Activa la red
- Inicia servicios de red del sistema
- Limpia los ficheros temporales
- Habilita el login a los usuarios

SysV es un modo de definir qué estado debe tener el equipo en un momento determinado. Para eso usa los modos de ejecución o runlevels. Usa siete modos (del 0 a 6) y cada distribución los usa para diferentes fines aunque hay varios niveles comunes.
- 0 Apaga el equipo
- 1 Modo monousuario
- 6 Reiniciar el equipo
- 2-5 Multiusuario
El nivel de ejecución del sistema por defecto se puede cambiar con `env DEFAULT_RUNLEVEL=2`
Para ver cuál se tiene ejecutar `runlevel`
Para cambiar manualmente el nivel de ejecución del sistema ejecutar `telinit 3`

Cada nivel de ejecución tiene asociado un directorio que especifica servicios que se deben ejecutar o parar (/etc/rc0.d /etc/rc1.d) Los scripts pueden verse mirando el contenido del directorio. Hay enlaces simbólicos a scripts de /etc/init.d y hay letra S (Inicia) o K (para) el servicio correspondiente y el orden. 

Para ver opciones de un servicio determinado puede ejecutarse directamente. 
`/etc/init.d/apache2 stop`

Realizados todos los pasos que establece el nivel de ejecución se procesa el fichero /etc/rc.local que es un cajón de sastre donde se escriben todos los comandos que el sistema ejecuta al iniciarse. 
### B.4.3. Servicios del sistema

Se ejecutan en segundo plano (servicio o demonio), ofreciendo una funcionalidad. (servidor web, servidor ftp, gestión de conexiones de red, monitorización del sistema, hardware del equipo...)
Se pueden parar, ejecutar, reanudar, establecer los que se ejecutan al iniciar el sistema...

- `systemctl status nombre_servicio`: Ver el estado
- `systemctl list-unit-files --type=service`: Listar servicios del sistema
- `systemctl start nombre_servicio`: Iniciar el servicio

Algunas de las palabras clave: start, stop, reload, restart, enable, disable, is-active, is-enabled, is-failed, list-dependencies, show.  Para ver la configuración: cat. 

**El nombre del servicio termina en .service.** 

Algunos servicios pueden seguir siendo administrador con `service`. Por ejemplo `service apache2 start`
También se podría con `/etc/init.d/apache2 start`
### B.4.4. Procesos

Puede haber procesos vinculados a servicios o demonios y procesos que ejecuta el usuario. 

- `ps`: Muestra los procesos asociados con el terminal actual. Se muestra su identificador PID, terminal donde se ejecuta (TTY Teletypewriter), tiempo de uso de CPU Central Processing Unit (TIME) y comando que ejecuta (CMD)
- `ps -A`: Muestra todos los procesos del sistema
- `ps -aux`: muestra los procesos de forma detallada. USER, PID, %CPU, %MEM (Porcentaje de memoria física usada), VSZ (Memoria virtual del proceso medida en KB), RSS (Memoria física no swapeada en KB), TT (terminal que controla el proceso), STAT (código de estado del proceso), STARTED (fecha de inicio), TIME (tiempo de CPU acumulado), COIMMAND (comando  con todos sus argumentos que ejecuta el proceso). 
- `kill <PID>`: Termina proceso, realiza limpieza acción de cierre
- `kill -9 <IDProceso>`: Envía señal SIGKILL de terminación forzosa
- `pstree`: Árbol de procesos del programa
- `pstree -p`; Árbol de procesos con identificador


Significado de las señales: https://manpages.ubuntu.com/manpages/bionic/es/man7/signal.7.html

### B.4.5. Programación de tareas

Programar la ejecución de un programa en un momento determinado (copia de seguridad, enviar un fichero, comprobar seguridad del sistema, enviar un informe...)

1º Comprobamos que el servicio esté en ejecución: `systemctl status cron.service`. `service cron status`. 

2º Se modifica el fichero de cron: `crontab -e`

```bash
# .---------------- minuto (0 - 59)
# |   .------------- hora (0 - 23)
# |   |   .---------- día del mes (1 - 31)
# |   |   |   .------- mes (1 - 12) o jan,feb,mar,apr ... (los meses en inglés)
# |   |   |   |    .---- día de la semana (0 - 6) (Domingo = 0 o 7) OR               |   |   |   |    |       sun,mon,tue,wed,thu,fri,sat (los días en inglés)
# |   |   |   |    |                               
# |   |   |   |    |
  *   *   *   *    *  User(debe tener permisos de script) Comando a ejecutar
```


Ejemplo:
```shell
# Cada 10 minutos
*/10 * * * * sh /home/romoreno-dev/monitoring.sh
# Todos los días a las 00:00
*/0 0 * * * /root/comprobar_seguridad.sh
# El primer dia del mes
*/* * * 1 * /root/copia_seguridad.sh
```

También se puede guardar el script en las carpetas de configuración de cron:
- /etc/cron/cron.hourly: Cada hora
- /etc/cron/cron.daily: Diariamente
- - /etc/cron/cron.weekly:  Semanalmente
- - /etc/cron/cron.monthly:  Mensualmente

Los scripts que ejecuta crontab solo pueden se modificados por root. 
Los scripts de esas carpetas se sabe cada cuanto se ejecutan por el script guardado en /etc/crontab

Con
- `crontab -l` Pueden verse las tareas programadas para el usuario con el que trabajamos
- `crontab -r`: Eliminar tareas programadas

También está anacron que permite ejecutar tareas al inicio del sistema https://www.solvetic.com/tutoriales/article/3964-como-programar-tareas-usando-anacron-linux/

### B.4.6. Reinicio y parada del sistema

Como todo, se puede hacer de forma gráfica (dándole al botoncito) o por el terminal.
Existen comandos como `halt`, `power off`, `reboot` y `shutdown`

```shell
# Detener sistema de forma segura y dejarlo en estado de parada
sudo halt
# Similar a halt
sudo poweroff
# Reinicia el sistema de forma segura
sudo reboot

# Veamos shutdown (Es obligatorio poner el argumento time).
# La flag -h indica que se detengan todos los servicios y procesos
# Apaga a las 14.30
sudo shutdown -h 14:30
# Apaga en 30 minutos
sudo shutdown -h +30
# Reinicia a las 14.30
sudo shutdown -h 14:30
# Reinicia ya
sudo shutdown -r 14:30

# Cancelar la parada
sudo shutdown -c
```

## B.5. Monitorización del sistema

Herramienta gráfica de monitorización "Monitor del sistema"
La monitorización de forma automática de muchos equipos puede hacerse con herramientas como Nagios y Centreon.

### B.5.1. Herramientas y comandos básicos

Los comandos se pueden clasificar en 
- Procesos
- Almacenamiento: E/S del subsistema de almacenamiento
- Memoria. Espacio de memoria real y swap.
- Red. Uso de interfaces de red.
- Polivalentes: Subsistemas del equipo

#### Procesos

| Comando | Descripción            |
| ------- | ---------------------- |
| `ps`    | Estado de los procesos |

#### Almacenamiento

| Comando | Descripción                                           |
| ------- | ----------------------------------------------------- |
| `df`    | Espacio libre del sistema de ficheros                 |
| `du`    | Espacio ocupado a partir de un determinado directorio |

#### Memoria

| Comando | Descripción                                                                 |
| ------- | --------------------------------------------------------------------------- |
| `free`  | Memoria física, espacio de swap libre, estado de los buffers, memoria caché |
| `pmap`  | Uso de memoria por parte de un proceso                                      |

#### Red

| Comando      | Descripción                                                               |
| ------------ | ------------------------------------------------------------------------- |
| `ifstat`     | Estadística de tráfico de entrada y salida de las interfaces de red       |
| `iftop`      | Conexiones de red del equipo                                              |
| `iptraf`     | Estadísticas de red en tiempo real                                        |
| `netstat`    | Tablas de rutas, interfaces de red, conexiones establecidas               |
| `ping`       | Estado de una conexión                                                    |
| `traceroute` | Camino que sigue un paquete para establecer comunicación con destinatario |
#### Polivalentes

| Comando   | Descripción                                                                                                                    |
| --------- | ------------------------------------------------------------------------------------------------------------------------------ |
| `dstat`   | Estadísticas de CPU, uso de disco, red, paginación, estado del sistema                                                         |
| `iostat`  | Carga de CPU y de disco duro                                                                                                   |
| `top`     | Actividad del sistema en tiempo real. Carga del sistema operativo. Grado de uso de CPU. Memoria y swap. Procesos en ejecución. |
| `vmstat`  | Procesos en ejecución, memoria, operaciones de E/S de disco, uso CPU. Es clásica en los sistemas.                              |
| `who`     | Tiempo que lleva activo el sistema, carga, actividad de los usuarios                                                           |
| `xosview` | Aplicación gráfica uso de CPU, memoria, cantidad de carga, red, interrupciones, swap...                                        |

#### Más comandos...

| Comando   | Descripción                                                                                                                                                                                                                                                                                      |
| --------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `uptime`  | Monitoriza la carga del sistema (hora, tiempo que lleva operativo, número de usuarios conectados, valor medio de la carga en el último minuto, últimos 5 minutos, últimos 10 minutos. 1 procesador carga con valor de 1 indica 100% de la CPU; 2 procesadores 100% de carga es valor de 2, etc.) |
| `time`    | Tiempo de ejecución de un programa. Permite conocer cómo se distribuye la ejecución de su código en modo usuario en supervisor                                                                                                                                                                   |
| `top`     | Actividad de los procesos. La información se actualiza por defecto cada 5 segundos (personalizable)                                                                                                                                                                                              |
| `ps`      | Actividad de los procesos                                                                                                                                                                                                                                                                        |
| `vmstat`  | Actividad de la memoria                                                                                                                                                                                                                                                                          |
| `free`    | Actividad de la memoria. Memoria física y swap.                                                                                                                                                                                                                                                  |
| `who`     | Actividad de los usuarios del sistema                                                                                                                                                                                                                                                            |
| `lsof`    | Listar todos los archivos abiertos y procesos que los usan (de disco, de red, tuberías, dispositivos y procesos)                                                                                                                                                                                 |
| `tcpdump` | Analiza los paquetes en red. Captura o filtra paquetes TCP/IP que se recibieron o han sido transferidos en una interfaz específica a través de una red.                                                                                                                                          |
| `netstat` | Conexiones de red a puertos del sistema, paquetes de red, estadísticas entrantes y salientes y de interfaz.                                                                                                                                                                                      |
| `htop`    | Como top pero permite gestión de procesos, teclas de acceso directo, vistas vertical y horizontal... (más avanzado)                                                                                                                                                                              |
| `iptraf`  | Monitor del tráfico IP que pasa a través de la red. Flags TCP, detalles ICMP, TCP / avería tráfico UDP, conexión TCP, cuenta Byne.                                                                                                                                                               |

### B.5.2. Directorio /proc

Como ya se ha comentado el kernel de Linux almacena información relativa a su funcionamiento en archivos de `/proc`. Para analizar el comportamiento del sistema se puede acudir a consultar estos archivos (Las herramientas comentadas obtienen sus datos de esta fuente). Por ejemplo:
- **Estado de la memoria** /proc/meminfo
- **Información sobre el procesador** /proc/cpuinfo
- **Sistema de comunicaciones** /proc/net
- **Datos referentes a proceso** En subdirectorios como /proc/pid_del_proceso.
### B.5.3. Archivos de registro (syslog)

Puede haber fallos varios en el servidor (problemas de hardware, fallo en servicio), fallos de autentificación, usos del servicio..
Eso se almacena en los archivos de registro o archivos log del directorio `/var/log`.
Ejemplos `/var/log/syslog` `/var/log/messages`. Si el servicio genera muchos mensajes, lo normal es que sean escritos en fichero o carpeta separada (apache /var/log/httpd o servidor de correo /var/log/mail).

El registro de todos los mensajes del sistema se hace por el servicio `syslogd` o `rsyslogd` que no es exclusivo del sistema sino que con `syslog` también pueden registrarse mensajes propios.

Puede accederse por interfaz gráfica, línea de comandos, webmin...

- /var/log/message: registros de mensajes generales del sistema.
- /var/log/auth.log: registros de autenticación.
- /var/log/kern.log: registros del kernel.
- /var/log/cron.log: registros de crond.
- /var/log/maillog: registros del servidor de mails.
- /var/log/utmp or /var/log/wtmp : registro de inicio y cierre de sesión.
- /var/log/btmp: registros con intentos fallidos de inicio del sistema.
- /var/log/cups/: registros relacionados con el sistema de impresión cups.

Ya se ha comentado que con `systemd` se puede tener gestión centralizada y recuperar los registros de sus elementos gestionados con `jopurnald`

Ejemplo `journalctl -u mariadb.service`

-u indica que es una unidad. Si es más de una unidad hay que poner una a continuación de la otra (con los -u concatenando ` journalctl -u cups.service -u NetworkManager.service`)

Más opciones: https://diocesanos.es/blogs/equipotic/2015/03/30/journalctl-logs-del-sistema-en-los-nuevos-linux/
## B.6. Copias de seguridad

Para realizar copias de seguridad podríamos distinguir entre:

- **Los comandos y herramientas básicas**: Con ellos se pueden realizar copias de seguridad de un equipo de forma individual. 
- **Herramientas avanzadas**: Permiten centralizar y administrar todas las copias de seguridad de un sistema en un único servidor. Como **amanda** o **bacula** (Windows y GNU Linux)
- **Clonación de discos duros**: Copia exacta de un disco duro o partición para restaurarlo en otro equipo de características similares. Útil cuando se quiere hacer copia exacta de un servidor o restaurar muchos con la misma configuración. Entre las más importantes: Clonezilla (usa como motor gparted), Clone Maxx, Dubaron DiskImage, g4U, NFGdump, Norton Ghost, Partition Saving, Partimage, WinDD. 

Muchas veces las herramientas de UNIX/Linux para copias de seguridad pueden tener problema a la hora de recuperar ficheros cuando se trata de software propietario. Es necesario el propio programa para hacerlo. 
Lo suyo es usar herramientas estándar para realizar las copias de seguridad de las máquinas. 
### B.6.1. Comandos básicos

#### Comando tar

 Copiar ficheros individuales o directorios en un único fichero ("contenedor"). Fue creado en su día para crear ficheros de cinta (intercambio de ficheros entre un disco y una cinta magnética).

Los ficheros con extensión ".tar" son empaquetados
Los ficheros con extensión ".tar.gz" o ".tgz" son comprimidos (ocupan menos espacio que el contenido)

Opciones:

| Nombre | Descripción                               |
| ------ | ----------------------------------------- |
| c      | Crea un contenedor                        |
| v      | Modo verboso                              |
| z      | Comprime o descomprime el fichero (gzip)  |
| j      | Comprime o descomprime el fichero (bz2)   |
| f      | Nombre del contenedor                     |
| x      | Extrae ficheros del contenedor<br>        |
| t      | Testea ficheros almacenados en contenedor |
| r      | Añade ficheros al final del contenedor    |
- Empaquetarlo con **"cvf"** (o **"cf"**, recuerda que la v no es obligatoria)
- Comprimirlo con **"cvzf"** 
- Extraerlo con **"xvf"**  o con **"xvzf"** si estaba comprimido. Se puede indicar el fichero a extraer. Si no se hace, se extraerán todos.

El parámetro `--exclude=` permite ignorar fichero o conjunto de ficheros con determinada extensión.
`tar -czvf /ruta/archivo.tgz --exclude=\*.{jpg,gif,png,wmv,flv,tar.gz,zip} /ruta/archivo`

Comandos tar: https://esgeeks.com/comandos-tar-para-comprimir-y-extraer-archivos/

```shell
# Copiar directorio /home/ubuntu a /home/copia.tar (Opcion v no es necesaria pero es util para ver el proceso de empaquetamiento del fichero)
tar -cvf /home/copia.tar /home/ubuntu

# Comprimir la informacion guardada
tar -cvzf /tmp/backup.tar /etc/passwd
# Se pueden poner multiples ficheros o directorios
tar -cvzf /tmp/backup.tar /etc/passwd /etc/hosts*
#----------------------------------

# Para recuperar (indicando cual quier o extraer)
tar -xvf /tmp/backup.tar /etc/passwd
# Para recuperar (Si esta comprimido)
tar -xvzf /tmp/backup.tar /etc/passwd

# Veamos el contenido
tar -tvf /ruta/archivo.tar
# Veamos el contenido si esta comprimido
tar -tvzf /ruta/archivo.tgz

# Solo introducir archivos que empiecen por A
tar -cvf comprimir.tar A*

# No usar ruta relativa
tar -czvf /ruta/archivo.tgz -C/ruta/archivo .

# Agregar al tar existente
tar --append --file=archivo.tar nuevoarchivo.extension
```

#### Comando dd

Para realizar copias exactas (bit a bit) de discos duros, particiones o fihceros.

`dd if=fichero_origen of=fichero_destino`

(Veamos qué ficheros hay antes con fdisk -l) Y ya pues... `dd if=/dev/sda of=/dev/sdb`
#### Comando rsync

Para sincronizar carpetas de forma incremental y trabajar con datos comprimidos y cifrados. Técnica de delta encoding (compresión diferencial), sincroniza archivos y directorios entre dos máquinas de una red (se envían por SSH) o dos ubicaciones en una misma máquina, minimizando el volumen de datos transferidos. 

```shell
rsync --avz /carpeta_origen /carpeta_destino
rsync --avz /carpeta_origen 192.168.0.9:/carpeta_destino
```

#### Backups con ISO y soportes ópticos

También se pueden hacer copias de seguridad sobre soportes ópticos (discos compatos). Para ello se debe crear una imagen ISO y luego se graba el fichero al DVD.
- Para crear: `genisoimage`  (xorrisofs, mkisofts, xorriso)
- Para grabar: `wodin` (cdrskin, xorriso)

```shell
mkdir /copia
sudo genisoimage -o /copia/imagen.iso /home
wodin -v -eject dev=/dev/cdrom -dao /copia/imagen.iso
```

La imagen ISO podría montarse en un directorio del sistema:
`mount -o /copia/imagen.iso /media/imagen`

### B.6.2. Herramientas gráficas

Como Déjà-Dup, Brasero, Clonezilla, Bacula.


------

# C. ADMINISTRACIÓN DE REDES

## C.1. Esquema básico de red

Ejemplo de requerimientos de un esquema de red:
- Configurar iptables para dar acceso a Internet a los clientes de la red interna
- Configurar el DHCP para que asigne de forma automática las direcciones de la 10.0.0.100 a la 10.0.0.254. El resto las asignará el administrador de red manualmente.
- Impresora de red con dirección MAC (AA:BB:CC:DD:EE:FF) a la que se le quiere asignar siempre la IP 10.0.0.254
- Configurar servidor de nombres para el dominio miempresa.com. Crear los  registros www.miempresa.con, ftp.miempresa.com que apuntan a 10.0.0.1. 
- Configurar servicios web y FTP para un propio servidor de páginas web y FTP.

### C.1.1. Configuración de la red

Configuremos las interfaces de red del servidor (actúa como enrutador) y de los clientes. Puede configurarse manual o automáticamente a través del servidor DHCP.
#### Configuración de la red cableada

Con `ifconfig` podemos consultar la configuración de las interfaces de red. El problema es que estos datos no quedarán guardados y al reiniciar el equipo se perderá la configuración.
##### Configurar interfaz de red
Para configurar la interfaz de red hay que asignarle una dirección IP con su máscara de red. 
Ejemplo: Configuramos 182.168.1.2 con máscara 255.255.255.0 y el parámetro up para indicar que la tarjeta debe activarse (puede omitirse, al asignar los parámetros de red se activará por defecto)
```shell
sudo ifconfig eth0 192.168.1.2 netmask 255.255.255.0 up
```

##### Activar interfaz de red
Con el parámetro up.
```shell
sudo ifconfig eth0 up
```
##### Desactivar interfaz de red
Con el parámetro down.
```shell
sudo ifconfig eth0 down
```

Para que el equipo pueda conectarse a una red diferente como Internet necesita una puerta de enlace. 
Para la puerta de enlace 192.168.0.1 asociada a eth0:
```shell
route add -net 0/0 gw 192.168.0.1 eth0
```

También puedes configurar todo esto con Sistema > Preferencias > Conexiones de red
#### Configuración de la red inalámbrica

Conocida la interfaz de red inalámbrica, se podría hacer con `iwconfig` parecido a esto:

```
iwconfig wlan0 essid nombre_de_red key contraseña
```

O, obviamente por interfaz gráfica.
#### Ficheros de configuración

Si se quiere que los datos permanezcan, deben guardarse en los ficheros de configuración.
Los cambios se aplican en las interfaces de red reiniciando el servicio o haciendo un reload ejecutando 
`/etc/init.d/networking force-reload`
### /etc/network/interfaces

La configuración de interfaces de red se guarda aquí. Ahí se podría ver en el ejemplo que la interfaz de red eth0 se conecta a internet y la eth1 pertenece a la red interna.

```/etc/network/interfaces
auto eth0
iface eth0 inet dhcp

auto eth1
iface eth1 inet static
address 10.0.0.1
netmask 255.255.255.0
network 10.0.0.0
broadcast 10.0.0.255
# gateway 10.0.0.1
```

eth0 obtiene la dirección IP de forma automática o ejecutando `dhclient eth0`

### /etc/hostname

Guarda el nombre del equipo.

### /etc/hosts

Resolución DNS local que guarda nombre y dirección IP de máquinas locales.
### /etc/resov.conf

Se establecen los servidores de resolución DNS. 

#### Comprobación

La conexión a internet puede comprobarse con el comando `ping
```shell
ping www.google.es
```

También se puede hacer de forma gráfica. Hay "herramientas de red" que permiten hacer ping a un determinado equipo, ver el estado de las conexiones (usando `netstat`), comprobar ruta entre el entre el equipo y el equipo remoto con `traceroute`, explorar los puertos de un equipo para ver si están abierto, información sobre los usuarios usados en un equipo de red con `finger`, detalles del propietario del dominio `whois`.

### C.1.2. Enrutamiento

Los cortafuegos de GNU/Linux evolucionan desde sencillos filtros de paquetes hasta los motores de inspección de paquetes de estado (SPI) que realiza:
- Filtrado de paquetes: Analiza cada paquete del tráfico y decide en base a las reglas qué hacer con él. También se puede modificar el paquete o marcarlo para que otros programas decidan qué hacer.
- Traducción de red (NAT): Simultáneamente el filtrado traduce las direcciones de forma que varios equipos puedan compartir una IP pública.

La evolución de los cortafuegos pasa por:
- ipfwadm (Linux 2.0)
- ipchains (Linux 2.2)
- iptables (Linux 2.4)
- nftables

iptables se divide en varias tablas en las que existen diferentes cadenas. Las más importantes son:
1. filter: Tabla para filtrado de las comunicaciones formada por:
	- INPUT: Filtran paquetes entrantes
	- OUTPUT: Filtran paquetes salientes
	- FORWARD: Filtran paquetes que pasan por equipo pero con origen y destino diferentes
2. nat: Traducción de direcciones de red con dos pilas o listas:
	- POSTROUTING: Comunicaciones desde red interna al exterior (interior acceso a internet)
	- PREROUTING: Comunicaciones de red externa a red interna (exterior acceso a servidor interno)
3. mangle: Reglas para alteración de los paquetes de red especializados.

Cada regla tiene información específica sobre direcciones de origen y destino, protocolos, números de puertos y otras características. 
Cada paquete llega a la parte superior de la pila que le corresponda y se le van aplicando reglas de esa pila secuencialmente hasta que exista una coincidencia. Momento en el cual se acepta, descarta, rechaza o reenvía.
Si no coincide con ninguna de las reglas, pasa a directiva predeterminada que normalmente descarta el paquete. 

![](SISTEMAS_INFORMATICOS/Andalucía/resources/ud05-1.png)

Entre los tipos de cortafuegos o firewall podríamos mencionar:
- **Filtrado de paquetes stateless**: Se examina encabezados de paquete para permitir o denegar el tráfico. Sin relación con flujos de tráfico precedentes. 
- **Filtrado de paquetes stateful**: Tabla de estado que hace seguimiento de las sesiones que atraviesan el firewall y en función de ella hace inspección de cada paquete que atraviesa el dispositivo. Se asume que si se permite inicio de conexión, cualquier conexión adicional será permitida.
- **Filtrado de paquetes stateful con inspección SPI  (Stateful Packwet Inspection) y control de aplicaciones**: Son firewalls stateful que incorporan motores de análisis de tráfico que suman servicios adicionales. Reensamblan en memoria las sesiones de la capa de transporte para realizar inspección de protocolos de capa de aplicación para permitir filtrado de protocolos y contenidos. Pueden verificar protocolos de aplicación para eliminar paquetes que no se conformen con el funcionamiento estándar del protocolo,
- **Sistemas de prevención de intrusos en la red NIPS (Network Intrusion Prevention Systems)**:  analizan tráfico de red para bloquear tráfico malicioso. Se asienta en base de datos de ataques que debe ser actualizada periódicamente. Dependen de las actualizaciones. Son mecanismos permisivos. 
- **Gateway de aplicaciones (proxy):** Intermediario y reenviar requerimientos de capa de aplicación y respuestas entre clientes y servidores. Permite filtrado y seguimiento muy granular tanto de solicitudes como de respuestas.

#### C.1.2.1 La iptables

Comandos básicos:
- `iptables -L`: Estado de la tabla predeterminada (filter)
- `iptables -t nat -L`: Estado de la tabla NAT
- `iptables -F`: Limpia la tabla de cortafuegos
- `iptables -P <cadena> <accion>`: Establece acción predeterminada sobre una pila. Por ejemplo si se quiere que por defecto el router deniegue todo el tráfico de la pila FORWARD (iptables -P FORWARD DROP)

- `iptables -A <parametros> -j <accion>`: Regla para que el cortafuegos realice una acción sobre el tráfico determinado.

Las acciones -j pueden ser:
- ACCEPT: Acepta el tráfico
- DROP: Elimina el tráfico
- REJECT: Rechaza el tráfico e informa al equipo de origen
- LOG -log-prefix "IPTABLES_L" Registra el tráfico que cumple los criterios en /var/log
- MASQUERADE: Enmascaramiento del tráfico (NAT) de forma que la red interna sale al exterior con la dirección externa del router
- DNAT --to `<ip>`: Para que desde el exterior se tenga acceso a un servidor de la red interna.

Los parámetros para especificar las reglas de iptables pueden ser:

|Elemento|Sintaxis|Ejemplo|Descripción|
|---|---|---|---|
|Interfaz|`-i <interfaz>`|`-i eth0`|Interfaz de entrada.|
||`-o <interfaz>`|`-o eth1`|Interfaz de salida.|
|Dirección|`-s <dir_red>`|`-s 10.0.0.0/24`|Red de origen.|
||`-d <dir_red>`|`-d 0/0`|Red de destino.|
|Puerto|`-p <tipo>`|`-p TCP`|Tipo de protocolo. Las opciones son: TCP, UDP o ICMP.|
||`--dport <puerto>`|`-p TCP --dport 80`|Indica el puerto de destino. En el ejemplo, se hace referencia al puerto de destino http (80/TCP).|
||`--sport <puerto>`|`-p UDP --sport 53`|Indica el puerto de origen. En el ejemplo, se hace referencia al puerto de destino DNS (53/UDP).|
|Estado|`-m state --state <tipo>`|`-m state --state ESTABLISHED`|Indica el estado de la conexión. Los posibles estados son: NEW, INVALID, RELATED y ESTABLISHED.|
|Acción|`-j <acción>`|`-j ACCEPT`|Indica la acción que se va a realizar con un determinado tráfico. Las posibles acciones son: ACCEPT, DROP, REJECT, LOG, DNAT y MASQUERADE.|

Algunas reglas pueden ser, de la más general a la más específica, para permitir el tráfico que reenvía el router:
```shell
iptables -A FORWARD -j ACCEPT # Permite todo el tráfico
iptables -A FORWARD -s 192.168.0.0/24 -j ACCEPT # Permite solo el tráfico de la red interna 192.168.0.0/24
iptables -A FORWARD -s 192.168.0.0/24 -p TCP -dport 80 -j ACCEPT # Permite solo el tráfico de la red interna 192.168.0.0/24 en el puerto 80
```

Al configurar el cortafuegos, ejecutar para guardar al configuración de iptables
`iptables-save>etc/iptables.rules`

También podría modificarse directamente y cargar su configuración ejecutando:
`iptables-restore < etc/iptables.rules`

Finalmente, modificar el fichero /etc/network/interfaces y escribir al final:
`pre-up iptables-restore < etc/iptables.rules`

También hay muchas interfaces gráficas que te ahorran todo este trabajo: Webmin,Dwall, FireHOL, Firestarter, Firewall Builder, Guarddog, KMyFirewall, Shorewall.

Sería posible bloquear visitantes por país, ver más en https://www.ip2location.com/free/visitor-blocker

#### C.1.2.2 Supuesto práctico de firewall

La rule de iptables tiene:
- **matches**: Condiciones que el paquete debe satisfacer. Por ejemplo la interfaz por la que entró el paquete (eth0, eth1) o qué tipo de paquete es (ICMP, TCP, UDP) o el puerto del destino del paquete o con -s una IP De origen.... 
- **target**: Acciones que se toman cuando el paquete coinciden. Se especifican con -j (--jump) y pueden ser cadenas definidas por el usuario, targets integrados como ACCEPT, DROP, QUEUE, RETURN; extensiones de targets como REJECT y LOG. 

```shell
# Para que el sistema actúe como enrutador se debe habilitar el reenvío de paquetes de kernel:
echo "1" > /proc/sys/net/ipv4/ip_forward
# Podemos limpiar todas las reglas predeterminadas y existentes (eliminar la tabla de filter)
iptables -F
iptables -t nat -F
# Podemos indicar que la red interna tiene salida al exterior por NAT (aislando la red interna del exterior)
iptables -t nat -A POSTROUTING -s 10.0.0.0/24 -d 0/0 -j MASQUERADE
# Podemos permitir todo el tráfico de la red interna y denegar lo demás 
iptables -A FORWARD -s 10.0.0.0/24 -j ACCEPT
iptables -A FORWARD -m state --state RELATED,ESTABLISHED -j ACCEPT
iptables -A FORWARD -j DROP
# Guardar la configuracion del cortafuegos
iptables-save >/etc/iptables.rules
```
- Y modifica el fichero /etc/sysctl.conf para establecer la variable net.ipv4.ip_forward=1.

La red interna sólo tiene acceso al exterior para ver páginas web (puerto 80/TCP) y para la resolución de nombres (53/UDP y 53/TCP). Además, se va a permitir la entrada desde fuera a un servidor web interno que se encuentra en la dirección 10.0.0.100.

```shell
# Podemos limpiar todas las reglas predeterminadas y existentes:
iptables -F
iptables -t nat -F
# Podemos indicar que la red interna tiene salida al exterior por NAT (aislando la red interna del exterior)
iptables -t nat -A POSTROUTING -s 10.0.0.0/24 -d 0/0 -j MASQUERADE
# Permitimos solo el tráfico web (80 TCP), DNS (53 UDP y 53 TCP) y denegamos lo demas
iptables -A FORWARD -s 10.0.0.0/24 -p TCP --dport 80 -j ACCEPT
iptables -A FORWARD -s 10.0.0.0/24 -p TCP --dport 53 -j ACCEPT
iptables -A FORWARD -s 10.0.0.0/24 -p UDP --dport 53 -j ACCEPT
iptables -A FORWARD -m state --state RELATED,ESTABLISHED -j ACCEPT
iptables -A FORWARD -j DROP
# Redirige el trafico web que entra por eth0 al servidor de la red interna
iptables -t nat -A PREROUTING -i eth0 –p tcp --dport 80 -j DNAT -- to 10.0.0.100:80
# Guardar configuracion del cortafuegos
iptables-save >/etc/iptables.rules
```

Modificar `/etc/network/interfaces` escribiendo al final:
`pre-up iptables-restore </etc/iptables.rules`

### C.1.3. DHCP

El servidor DHCP se encarga de gestionar asignación de direcciones IP, máscara de red, puerta de enlace y servidor DNS. Para ello necesita un proceso `dhcpd` y un fichero de configuración (`etc/dhcpd.conf`). Se incluye en este fichero: 
- Rango de direcciones IP a ortorgar
- Asociación fija de direcciones IP mediante el uso de MAC
- Periodo de validez de asignaciones
- Servidores de nombres y wins
- Autoridad o no para asignar IP

Hay dos métodos de asignación:
- **Asignación dinámica**: Direcciones IPs libres de rango establecido por el administrador en el fichero. Permite reutilización dinámica de direcciones IP.
- **Asignación por reservas o estática**: El dispositivo siempre tiene la misma dirección IP. Se asigna la IP a la dirección MAC. Útil para dispositivos como una impresora en red que no debe cambiar de IP. 

#### Supuesto práctico

Instalamos el servidor DHCP 
`apt-get install isc-dhcp-server`

Se va a configurar el DHCP para asignar dinámicamente IP a la red 10.0.0.0/24 y para realizar una reserva al MAC /AA:BB:CC:DD:EE:FF) para que siempre tenga la dirección IP 10.0.0.254

Parámetros generales del servidor y comunes a equipos de red, información para que sepa cómo comportarse. Se quiere que el tiempo máximo de asignación de IP sea de una semana:

```/etc/dhcp/dhcpd.conf
authoritative;     
one-lease-per-client on;
server-identifier 10.0.0.1;
`ddns-update-style interim;
default-lease-time 600;
max-lease-time 604800;
```

Se introducen los parámetros generales que se transmitirán a los clientes. La red 10.0.0.0 con máscara 255.255.255.0 tiene como puerta de enlace IP 10.0.0.1 y quiere usar servidores 8.8.8.8 y 194.224.52.36. El rango de direcciones asignables por DHCP es de 10.0.0.100 a 10.0.0.254.

```/etc/dhcp/dhcpd.conf
subnet 10.0.0.0 netmask 255.255.255.0 {
    range 10.0.0.100 10.0.0.254;
    option domain-name-servers 8.8.8.8, 194.224.52.36;
    option domain-name "miempresa.com"; <br />    option routers 10.0.0.1;
    option broadcast-address 10.0.0.255;
 }
```

La reserva de la IP 10.0.0.254 para el portátil con MAC AA:BB:CC:DD:EE:FF
```/etc/dhcp/dhcpd
host portatil {
    hardware ethernet AA:BB:CC:DD:EE:FF;
    fixed-address 10.0.0.254;
}
```

La interfaz de red donde se quiere que el dhcp ofrezca sus servicios. Es necesario que el fichero `/etc/default/isc-dhcp-server` contenga `INTERFACES="eth1"`

```shell
# Consulto que esta bien ejecutando
dhcpd eth1
# Se configura para que se inicie automáticamente al iniciar el equipo con sysv-rc-conf
apt-get install sysv-rc-conf
sysv-rc-conf
# Se marca con una X. Buscar usc-dhcp y marcarlo para el nivel de ejecucion actual
# Para saber la ejecucion actual se puede conocer con runlevel
```

Las asignaciones realizadas pueden consultarse en `/var/lib/dhcp/dhcpd.releases` donde se indica los datos para cada conceción de dirección IP.

No olvides: isc-dhcp-server (Nombre del servicio) /etc/dhcp/dhcpd.conf (Fichero de configuración) /var/lib/dhcp/dhcpd.releases (Concesiones de direcciones) dhcpd dhclient (Comandos más usados)

Recuerda que DHCP permite que los clientes obtenga IP de forma automática, optimiza las direcciones, realiza reservas pero no tiene por qué influir en la seguridad.

## C.2. Recursos de acceso compartido (Samba)

Samba es una colección de programas que hacen que Linux sea capaz de usar el protocolo SMB, base para compartir ficheros e impresoras en una red de Windows.

Se compone de tres paquetes:
- samba-common (archivos comunes)
- samba-client (cliente)
- samba (servidor)

```shell
# Instalemos cliente y servidor
apt-get install samba smbclient
# Iniciemos el servidor
service samba start
```

Hay que dar de alta a los usuarios del sistema y configurar los recursos a compartir. 
### C.2.1. Gestión de usuarios

Los usuarios y contraseñas de Samba se administran con `smbpasswd` -a (Añadir) -x (Eliminar)
Para dar de alta un usuario en samba este tiene primero que existir en el sistema. 

```shell
smbpasswd -a pepe
smbpasswd -x juan
```

Para ver usuarios y contraseñas (antes /etc/samba/smbpasswd) se pueden ver con `pdbwdit -w -L`

### C.2.2. Compartir carpetas

Se debe modificar el fichero de  configuración de samba /etc/samba/smb.conf 

La opciones más usadas para compartir carpetas son:

|Opción.|Comentario.|
|---|---|
|[ recurso ]|Nombre del recurso compartido.|
|browseable|Indica si se puede explorar dentro del recurso. Los posibles valores son _no_ y _yes_.|
|comment|Proporciona información adicional sobre el recurso (no afecta a su forma de operar).|
|create mode|Especifica los permisos por defecto que tienen los ficheros creados.|
|directory mode|Especifica los permisos por defecto que tienen los directorios creados.|
|force user|Especifica el usuario propietario que tienen los ficheros y carpetas que se crean.|
|force group|Especifica el grupo propietario que tienen los ficheros y carpetas que se crean.|
|guest ok|Indica si se permite el acceso a usuarios anónimos. Los posibles valores son _no_ y _yes_.|
|path|Carpeta a compartir.|
|public|Indica si el directorio permite el acceso público. Los posibles valores son _no_ y _yes_.|
|read only|Indica que el directorio es sólo lectura. Los posibles valores son _no_ y _yes_.|
|valid users|Indica los usuarios que pueden acceder a la carpeta. Para añadir un grupo entonces hay que poner el nombre del grupo precedido de la @.|
|writable|Indica que se puede modificar el contenido de la carpeta.|
|write list|Indica los usuarios que pueden modificar el contenido.|

```smb.conf
# Accesible publicamente para todos los usuarios
[publico]
        path = /home/usuario/publico 
        public = yes 
        read only = yes
        
# Accesible solo por algunos, con diversos permisos de lectura y escritura
 [miscosas]
        path = /datos/
        comment = “Datos y aplicaciones”
        valid users = juan, encarni,@master
 
        writeable = yes
        write list = juan
        read list = juan,@master
 
        force user = juan
        force group = juan
        create mode = 770
        directory mode = 770
```

Los permisos deben haberse establecido en el fichero de configuración y también en el sistema de ficheros.

Para que se apliquen los cambios, se reinicia `service samba restart`
### C.2.3. Compartir impresoras

Se pueden compartir impresoras conectadas al equipo para ser usadas por todos los clientes de la red mediante cups o mediante samba.

**Cups** es el servidor de impresión que viene por defecto instalado en Ubuntu. Dispone de interfaz gráfica accesible desde un navegador http://localhost:631.

**Samba**: Hay que añadir un recurso siguiendo esta estructura:
```
[printers]     
    comment = All printers 
    path = /var/spool/samba 
    browseable = no
    printable = yes 
    public = no
    writable = no
    create mode = 0700
```

|Parámetro.|Comentario.|
|---|---|
|comment|Proporciona información sobre la sección (no afecta a la operación).|
|path|Especifica la ruta de acceso a la cola de impresión o spool (que por defecto es /var/spool/samba). Es posible crear un directorio de spool para Samba y hacer que apunte a él.|
|browseable|Como con los directorios raíz, si indica NO se asegura de que sólo pueden ver las impresoras los usuarios autorizados.|
|printable|Se debe poner _YES_, si no se hace así no funcionarán las impresoras.|
|public|Si se pone _YES_, cualquier usuario podrá imprimir (en algunas redes se pone _NO_ para evitar la impresión excesiva).|
|writable|Las impresoras no son escribibles, por lo tanto escriba NO.|

El acceso a GNU/Linux desde Windows el nombre compartido es el nombre de la impresora Linux en el fichero printtab. Deberá acceder a `\\smbserver\HTP_laserjet`

**Impresoras que disponen de tarjeta de red**: Permiten imprimir directamente sin necesidad de servidor.
### C.2.4. Asistentes de configuración

Como siempre se puede con interfaz gráfica en webmin (Samba Windows File Sharing) o con system-config-samba.

### C.2.5. Cliente

Como cliente para acceder a ficheros compartidos que hay en otros servidores puede hacerse com smbclient (similar a serrvidor FTP para acceder a recurso remoto compartido, no permitiendo uso de comandos normales de Unix para manipular los ficheros) y smbprint.

La forma más sencilla es montando una carpeta y así accediendo al contenido del recurso de la misma forma que con cualquier otra:
```shell
mkdir /prueba
mount -t cifs –o user=usuario,pass=contrasena //10.0.0.1/recurso /prueba
```

(La ultima es el directorio en el que se va a montar el recurso compartido)

| Nombre del servicio:      | samba4                              |
| ------------------------- | ----------------------------------- |
| Fichero de configuración: | /etc/samba/smb.conf                 |
| Comandos más utilizados:  | smbpasswd smbclient pdbedit mount   |
| Puertos utilizados:       | 137/UDP, 138/UDP, 139/TCP y 445/TCP |
## C.3. NFS

NFS permite que equipos GNU/Linux compartan carpetas entre sí. Se basa en modelo cliente/servidor. Un servidor comparte una carpeta para que los clientes la puedan usar. El cliente monta la carpeta compartida, pudiéndola usar normalmente como si fuera una carpeta más.

Para instalarlo: ` apt-get install nfs-kernel-server nfs-common`

### C.3.1. Configuración del servidor

Se indica qué directorios se desea compartir.
Debe modificarse 
- **/etc/exports** Para indicar los directorios locales que se van a exportar a sistemas retomos. Las líneas tienen el siguiente formato `<directorio> <IP>/<MÁSCARA>(opciones) <IP>/<MÁSCARA>(opciones)...` Se puede compartir con opciones de solo lectura (ro) o lectura y escritura (re); comunicando al usuario los cambios de sofrma síncrona (sync) o asíncrona (async), permitiendo que no se comprueba el camino hasta el directorio que se exporta en caso de que no haya permiso (no_subtree_check),, root_squash (acceso del admin con prigilegios de usuario anónimo), all_squash (todos acceso como usuario anónimo, no se mantienen UID y GID de ningún usuario)

`/datos 192.168.20.9/24(rw,sync,root_squash) 192.168.20.8/24(ro)`

- **/etc/host.allow** y **/etc/host.deny** se indica a qué máquinas se les permite o deniega el acceso. Debe denegarse a todos los equipos el acceso y concederlo solo a los que lo necesiten. 

 **/etc/host.deny** `rpcbind: ALL`
 **/etc/host.allow** `rpcbind: <IP>/MÁSCARA<br />nfs: <IP>/MÁSCARA`

E iniciamos el servicio

```shell
service nfs-kernel-service start
```
### C.3.2. Configuración del cliente

El directorio debe montarse al iniciar el equipo `mount 192.168.20.100:/datos /prueba`
Se puede decir (rw, modo lectura/escritura; hard, si al copiar un fichero se pierde la conexión vuelva a iniciar copia del fichero cuando se encuentre activo, intr evita que las aplicaciones se queden colgadas al intentar escribir en la carpeta si no está activa. 

| Nombre del servicio:     | nfs                 |
| ------------------------ | ------------------- |
| _Carpetas compartidas:_  | /etc/exports        |
| Comandos más utilizados: | mount               |
| Puertos:                 | 2049/TCP y 2049/UDP |

## C.4. Acceso remoto al sistema

Los más usados son:
- Telnet: Acceso remoto de forma no segura
- Open SSH: Por terminal de forma segura, comunicaciones cifradas
- VNC: Por entorno gráfico

### C.4.1. SSH

Permite conectarse de forma segura a un servidor para poder administrarlo.
Ofrece transmisión de ficheros, protocolo FTP seguro, uso como transporte de otros servicios...

Establece una comunicación cifrada entre cliente y servidor mediante un **algoritmo de cifrado robusto (128 bits)** que se usará en todos los intercambios de datos.

`service` es adecuado para gestionar servicios básicos (status, start, reload, restart y stop)
`systemctl` son llamadas directas con mayor opción de control

```shell
# Instalamos
apt-get install ssh # Instalar
systemctl status ssh # Estado
systemctl start ssh # Inicia
systemctl stop ssh # Para
```

Opciones como fail2ban que cuando se realizan 5 intentos fallitos de autentificación en el sistema se comunica con iptables y bloquea la IP.

#### C.4.1.1. Servidor

Usa `/etc/ssh/sshd_config` . No suele ser necesario configurarlo. Los parámetros más importantes son
```
# Puertos y direccion de escucha
Port 22
ListenAddress 0.0.0.0
# Permitir login con root
PermitRootLogin no
# Usuarios permitidos o denegado, incluso indicando el equipo anfitrion
AllowUsers cesar sonia@10.0.0.2
DenyUsers pepe
# Al autenticarse mostrar contenido de /etc/motd
PrintMotd yes
# Al autenticarse, indicar un fichero a mostrar
Banner /etc/issue.net
# Evita la conexión de usuarios de equipos conocidos en fichero ./ssh/know_host
# Reenvío de puertos (tunnlehing) que un usuario externo alcance un puerto en una direccion IP privada de una LAN desde el exterior a través de router con NAT habilitada, puede deshabilitarse esta posibilidad
Decir si se permite reenvío de TCP
IgnoreUserKnownHosts no
GatewayPorts no
AllowTcpForwarding yes
# Uso de subsistema para otra aplicacion como ftp
Subsystem sftp /usr/lib/openssh/sftp-server
# Deshabilitar SSH sin contraseña
PasswordAuthentication no
ChallengeResponseAuthentication no
UsePAM no
```

Recordatorio: Siempre tras actualizar `systemctl restart ssh`
#### C.4.1.2. Cliente

Simplemente se conecta `ssh username@ip`

Si se usa Windows puede usarse Putty. o OpenSSH

Con `scp` se pueden copiar rficheros en equipos remotos: `scp /etc/passwd 10.0.0.2:/root.`

#### Conexión sin contraseña: Clave pública y privada

Ofrece un inicio de sesión fácil y no interactivo. Es más seguro ya que funciona con criptografía de clave pública-privada. Permite mejor gestión de autenticación y autorización.

Veamos si existe alguna: `ls -al ~/.ssh/id_*.pub`

`ssh-keygen -t rsa`  (De tipo RSA, protocolo para generar claves. Es el predeterminado así que puede ponerse `ssh-keygen` y ya)

La clave predeterminada es de 2048 bits, pero puede cambiarse el valor a 4096 bits.
`ssh-keygen -t rsa -b 4096`

Se pedirá el archivo donde se guardará la clave `/home/.ssh/id_rsa`
Se pedirá la passphrase: Cadena de caracteres usada para cifrar la clave privada.

La clave pública queda guardada en `/home/.ssh/id_rsa.pub`

La clave pública debe copiarse en una máquina de destino usando:

**El comando ssh-copy-id**
`ssh-copy-id remote_username@remote_IP_Address`
La clave pública SSH generada se añadirá al archivo authorized_keys del equipo remoto. 

**Usando SSH**
`cat ~/.ssh/id_rsa.pub | ssh remote_username@remote_ip_address "mkdir -p ~/.ssh && cat >> ~/.ssh/authorized_keys"`

**Manualmente**
Aregar manualmente el contenido del archivo **id_rsa.pub** al archivo **~/.ssh/authorized_keys** del servidor remoto.

```shell
cat ~/.ssh/id_rsa.pub
mkdir -p ~/.ssh
echo SSH_public_key >> ~/.ssh/authorized_keys
chmod -766 ~/.ssh
```
### C.4.2. VNC

Programa con licencia GPL usando modelo cliente/servidor para ver pantalla del equipo remoto y controlarlo desde uno o varios clientes y desdecualquier ubicación.

#### C.4.2.1. Servidor

Paquete vino da acceso remoto a escritorio en Ubuntu. Se puede compartir, compartir pantalla. Permitir conexiones para controlar la pantalla. Las conexiones deben solicitar acceso. Solicitar una nueva contraseña. Redes...
#### C.4.2.2. Cliente

- Remmina. (Linux)
- Vinragre (Linux)
- tigerVNC (Windows)

### C.5. Servidor Web Apache

El servidor de Apache trabaja normalmente en los puertos 80 y 443. 

Podemos instalar apache `sudo apt-get install apache2`
Al final del proceso Ubuntu lo iniciará. Comprobamos. `sudo systemctl status apache2`

El directorio más significativo de Apache es /var/www/html donde se publica el contenido web. 
#### C.5.1. Instalar PHP

Con `apt-get install php5`
Se puede crear un fichero PHP situándolo en el directorio raíz del servidor web `vim /var/www/html/info.php`

```php
<?php
   phpinfo();
?>
```

#### C.5.2. Configuración

La configuración de Apache se almacena en /etc/apache2

Fichero /etc/apache2/ports.conf

```apache2.conf
# Puertos de escucha de comunicaciones
Listen *:80
Listen *:443
```


Fichero /etc/apache2/apache2.conf
```
# Usuario y grupo al que pertenecen los procesos que ejecuta el servidor
User www-data
Group www-data
```

Carpeta /etc/apache2/sites-available : Configuración de cada uno de los sitios web de apache (por defecto default y default-ssl). Tienen esta estructura:
```
<VirtualHost *:80>
     ServerAdmin servermaster@localhost
     # Servername www.miempresa.com # comentado en default
     DocumentRoot /var/www/html
     DirectoryIndex index.html default.html
</VirtualHost>
```

```
```- ServerAdmin es el correo electrónico del administrador del sitio web.
- Servername es el nombre FQDN del sitio web. Para el dominio default no se indica ningún nombre, pero para atender peticiones específicas de dominios (por ejemplo, www.miempresa.com) sí se debe establecer.
- DocumentRoot. Indica la ubicación donde se encuentra las páginas web del sitio.
- DirectoryIndex. Indica el nombre de los ficheros que envía por defecto el servidor web.
```

#### Crear certificado SSL autofirmado para Apache

```
# Recuerda que a veces habra un firewall y hay que darlepermiso
sudo ufw allow "Apache Full"

# Habilitar mod_ssl
sudo a2enmod ssl
# Reiniciar
sudo systemctl restart apache2
# Con OpenSSL crear certificado
sudo openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout /etc/ssl/private/apache-selfsigned.key -out /etc/ssl/certs/apache-selfsigned.crt
```

- `openssl`: es la herramienta de línea de comandos para crear y administrar certificados, claves y otros archivos de OpenSSL.
- `req -x509`: especifica que deseamos usar la administración de la solicitud de firma de certificados (CSR) X.509. El “X.509” es un estándar de infraestructura de claves públicas al que se adhieren SSL y TLS para la administración de claves y certificados.
- `-nodes`: indica a OpenSSL que omita la opción para proteger nuestro certificado con una frase de contraseña. Necesitamos que Apache pueda leer el archivo, sin intervención del usuario, cuando se inicie el servidor. Una frase de contraseña evitaría que esto suceda porque tendríamos que introducirla tras cada reinicio.
- `-days 365`: esta opción establece el tiempo durante el cual el certificado se considerará válido. En este caso, lo configuramos por un año. Muchos navegadores modernos rechazarán cualquier certificado válido por más de un año.
- `-newkey rsa:2048`: especifica que deseamos generar un nuevo certificado y una nueva clave al mismo tiempo. No creamos la clave que se requiere para firmar el certificado en un paso anterior, por lo que debemos crearla junto con el certificado. La parte `rsa:2048` le indica que cree una clave RSA de 2048 bits de extensión.
- `-keyout`: esta línea indica a OpenSSL dónde colocar el archivo de clave privada generado que estamos creando.
- `-out`: indica a OpenSSL dónde colocar el certificado que creamos.

Complete las solicitudes de forma adecuada. La línea más importante es la que solicita `Common Name`. Debe introducir el nombre de host que utilizará para acceder al servidor o a la IP pública del servidor. Es importante que este campo coincida con lo que pondrá en la barra de direcciones de su navegador para acceder al sitio, ya que un error de concordancia causará más errores de seguridad.

Los dos archivos que creó se ubicarán en los subdirectorios correspondientes en `/etc/ssl`.

Abra un nuevo archivo en el directorio /etc/apache2/sites-available:

```
sudo nano /etc/apache2/sites-available/your_domain_or_ip.conf
```

```
<VirtualHost *:443>
   ServerName your_domain_or_ip
   DocumentRoot /var/www/your_domain_or_ip

   SSLEngine on
   SSLCertificateFile /etc/ssl/certs/apache-selfsigned.crt
   SSLCertificateKeyFile /etc/ssl/private/apache-selfsigned.key
</VirtualHost>
```

Más info: https://www.digitalocean.com/community/tutorials/how-to-create-a-self-signed-ssl-certificate-for-apache-in-ubuntu-20-04-es

| Nombre del servicio:        | apache2 (Ubuntu)                                       |
| --------------------------- | ------------------------------------------------------ |
| Operaciones con el servicio | service apache2 [ start \| stop \| restart \| reload ] |
| Fichero de configuración:   | /etc/httpd/conf/httpd.conf                             |
| Directorio web:             | /var/www/html (Ubuntu)                                 |
| Comandos más utilizados:    | htpasswd                                               |
| Puertos:                    | 80/tcp y 443/tcp                                       |

### C.6. Servidor FTP

Vsftpd es un servidor FTP pequeño que debe ser, obviamente, instalado. `apt-get install vsftpd`

Se configura en /etc/vsftpd.conf

- **listen**: Si se inicia el servicio con el sistema o no.
- **anonymous_enable.** Si se permite que usuarios anónimos puedan conectarse al servidor.
- **local_enable.** Para poder conectarse con los usuarios locales del servidor donde está instalado.
- **write_enable.** Si los usuarios pueden escribir y no sólo descargar.
- **local_umask.** Los permisos con los que se suben los archivos. Lo típico es 022, lo que establece los permisos a 755, lo más típico en servidores FTP.
- **chroot_local_user.** Si los usuarios están encerrados en sus directorios.
- **chroot_list_enable.** Si ciertos usuarios locales, especificados en el siguiente parámetro, pueden navegar por todo el árbol de directorios del servidor
- **chroot_list_file.** Indica el fichero donde están listados los usuarios que pueden navegar hacía arriba por los directorios del servidor.

Para comprobar que funciona, puede uno conectarse al servidor simplemente poniendo `ftp localhost`

(si no permitiese acceso desde el exterior podría ser debido a que el router no permite el paso del servidor FTP)

