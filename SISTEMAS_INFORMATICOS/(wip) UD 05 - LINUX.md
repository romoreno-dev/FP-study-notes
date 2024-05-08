
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
- Root o supernumerario. Administrador y dueño del sistema. (Consejo: Solo usar esa cuenta para tareas específicas de administración)
- Usuarios normales. Inician sesión en el sistema y tienen funcionalidad limitada (en comandos y en ficheros)
- Usuarios asociados a servicios. No pueden iniciar sesión en el sistema. Establecer privilegios de un servicio. (Ej.: Servidor web con qué ficheros tiene acceso y, por tanto, qué ficheros están expuestos)


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


### B.1.2. Ficheros utilizados



### B.1.3. Interfaz gráfica


### B.1.4. Interfaz web. Webmin


## B.2. Sistema de ficheros

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

