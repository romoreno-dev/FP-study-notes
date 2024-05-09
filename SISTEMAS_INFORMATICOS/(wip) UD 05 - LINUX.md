
# A. INSTALACIÓN Y CONFIGURACIÓN
## A.1. Introducción


## A.2. Distribuciones


## A.3. Licencias de software


## A.4. Instalación de Ubuntu

### A.4.1. Características y versiones



### A.4.2. Requisitos hardware del sistema


### A.4.3. Instalando el sistema


## A.5. Primeros pasos

### A.5.1. X-Windows



### A.5.2. Intérprete de comandos


### A.5.3. Estructura de directorios


## A.6. GNOME. Personalización

### A.6.1. Escritorio GNOME


### A.6.2. Iconos de escritorio


### A.6.3. Configuración visual


### A.6.4. Barra de menús


### A.6.5. Lanzador


## A.7. Repositorios

### A.7.1. Añadir repositorios externos


## A.8. Actualizaciones

### A.8.1. Actualización de los repositorios

#### A.8.1.1. Actualizar /etc/apt/sources.list

### A.8.2. Actualización del sistema



## A.9. Instalación y desinstalación de software

### A.9.1. Synaptic

##### Opciones de Synaptic

### A.9.2. apt-get o apt

### A.9.3. Aptitude


### A.9.4. Ubuntu Software


### A.9.5. Snap


### A.9.6. Instalación manual


### A.9.7. Webmin


## A.10. Pasos documentados para instalar Ubuntu



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
- **Archivos normales**:
- **Directorios**
- **Especiales**
- 


### B.2.1. Particionamiento

#### Herramientas gráficas

#### Comando fdisk

#### Volúmenes lógicos

### B.2.2. Espacio en disco


## B.3. Permisos

### B.3.1. Notaciones simbólica y octal

### B.3.2. Establecer permisos

### B.3.3. Listas de control de acceso

## B.4. Arranque y parada

### B.4.1. Gestor de arranque de GNU/Linux

### B.4.2. Proceso de arranque y parada del sistema

### B.4.3. Servicios del sistema
### B.4.4. Procesos

### B.4.5. Programación de tareas

### B.4.6. Reinicio y parada del sistema


## B.5. Monitorización

### B.5.1. Herramientas y comandos básicos

### B.5.2. Directorio /proc

### B.5.3. Archivos de registro (syslog)


## B.6. Copias de seguridad

### B.6.1. Comandos básicos

#### Comando tar

#### Comando dd

#### Comando rsync

#### Backups con ISO y soportes ópticos


### B.6.2. Herramientas gráficas


## B.7. Particionamiento de una unidad de disco


## B.8. Proceso de arranque y parada del sistema (init)


------

# C. ADMINISTRACIÓN DE REDES

## C.1. Esquema básico de red

### C.1.1. Configuración de la red

#### Configuración de la red cableada


#### Configuración de la red inalámbrica


#### Ficheros de configuración


#### Comprobación


### C.1.2. Enrutamiento


#### Supuesto práctico


### C.1.3. DHCP

#### Supuesto práctico

## C.2. Recursos de acceso compartido (Samba)

Carpetas, impresoras...

### C.2.1. Gestión de usuarios

### C.2.2. Compartir carpetas


### C.2.3. Compartir impresoras



### C.2.4. Asistentes de configuración

### C.2.5. Cliente

## C.3. NFS

### C.3.1. Configuración del servidor


### C.3.2. Configuración del cliente

## C.4. Acceso remoto al sistema


### C.4.1. SSH

#### C.4.1.1. Servidor


#### C.4.1.2. Cliente



### C.4.2. VNC

#### C.4.2.1. Servidor


#### C.4.2.2. Cliente



### C.5. Servidor Web


#### C.5.1. Instalar PHP


#### C.5.2. Configuración


### C.6. Servidor FTP

