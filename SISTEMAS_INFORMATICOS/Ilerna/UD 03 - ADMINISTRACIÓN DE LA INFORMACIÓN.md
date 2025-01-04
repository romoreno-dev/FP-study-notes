
## 3.1. Sistema de archivos

El **sistema de archivos** es el área del sistema operativo que se ocupa de gestionar la utilización de los medios empleados para almacenar información en las diferentes particiones del disco.

Se puede dividir en dos objetos fundamentales:
- **Archivos o ficheros**: Conjunto de datos ordenados en los que se almacena la información. Algunos son del sistema operativo empleados para trabajar internamente y otros generados por el usuario mediante aplicaciones. Permiten almacenar información en el disco y volver a leerla sin que el usuario se preocupe por cómo y dónde esta información se ha almacenado. Pueden ser diferenciados entre archivos ejecutables (funcionan por ellos mismos) y no ejecutables o archivos de datos (necesitan programa).
- **Directorios**: Es un contenedor que puede contener archivos y, a su vez, otros directorios. Ofrecen la posibilidad de clasificar los archivos y poner orden en el sistema. La estructura resultante es jerárquica y ramificada. (Estructura en árbol). Existe un directorio raíz (root) que engloba a todos los directorios y archivos.
## 3.2. Tipos de sistemas de archivos

Tras particionar el disco, en el momento de formatearlo suele elegirse el tipo de sistema de archivos. También con herramientas del propio sistema operativo será posible crear, eliminar y moficiar las particiones.

Los tipos de sistemas de archivos más utilizados son:
- **FAT32** (File Assignation Table, Tabla de Asignación de Archivos). Se considera un sistema universal, siendo heredado de MS-DOS y puede encontrarse en las primeras versiones de Windows. Pese a su antigüedad puede encontrarse con cierta frecuencia.
- **NTFS** (New Technology File System). Diseñado para versiones más recientes de Windows. Eficiencia y seguridad.
- **EXT2**, **EXT3**, **EXT4**. Son diferentes versiones del sistema de archivos encontradas principalmente en Linux. 

## 3.3. Gestión de sistemas de archivos comandos y entornos gráficos 

El gestor de archivos es una aplicación básica en cualquier sistema operativo.
En Windows puede accederse desde consola o desde entorno gráfico (Explorer). En Linux puede accederse desde consola o a través de programas gráficos (Nemo, Nautilus, Dolphin,...)

| Instrucción | Definición                    | Ejemplo                                    |
| ----------- | ----------------------------- | ------------------------------------------ |
| `DIR`       | Listar ficheros y directorios | `DIR unidad:\directorio\`                  |
| `CD`        | Desplazarse por las carpetas  | `CD unidad:\directorio\`                   |
| `MD`        | Crear directorio              | `MD Juegos`                                |
| `RD`        | Eliminar directorio           | `RD Juegos`                                |
| `COPY`      | Copiar ficheros               | `COPY ..\ruta_archivo ..\ruta_destino`     |
| `DEL`       | Borrar ficheros               | `DEL nombre_archivo`                       |
| `REN`       | Renombrar ficheros            | `REN nombre_original.txt nuevo_nombre.txt` |
| `MOVE`      | Mover ficheros                | `MOVE ..\ruta_archivo ..\ruta_destino`     |
Para ver el manual escribir **/?** tras la instrucción. Ej.: `COPY /?`. También hay herramientas como FreeCommander o UnrealCommander. 
## 3.4. Gestión de enlaces

Los sistemas operativos permiten crear **enlaces o vínculos** a ejecutables, carpetas y archivos. Son únicamente vías rápidas para acceder a la información.

En Windows se denominan accesos directos (creados con el botón secundario del ratón sobre el elemento que se desea vincular)

En Linux se podría hacer de forma gráfica, pero también usando el comando `ln` (Enlace soft)
```bash
ln -s nombre_archivo nombre_enlace
```

También se puede hablar de enlaces/marcadores/favoritos en un navegador web y del surgimiento de formas más sencillas de tener sincronizados los dispositivos para uso personal, gestionando los datos de los navegadores web en todos los dispositivos. 
## 3.5. Estructura de directorios de sistemas operativos libres y propietarios

**Linux**
En las distribuciones de Linux, los elementos clave del árbol de directorios son

| Directorio | Almacenamiento de...                                                                                |
| ---------- | --------------------------------------------------------------------------------------------------- |
| `/bin`     | Archivos binarios (ejecutables) con comandos esenciales que usará el usuario.                       |
| `/boot`    | Archivos de arranque de Linux (salvo archivos de configuración)                                     |
| `/dev`     | Archivos de hardware (ratón, teclado, disco duro,...)                                               |
| `/etc`     | Archivos de configuración                                                                           |
| `/home`    | Estructura de árbol en la que cada usuario tiene su propio subdirectorio                            |
| `/lib`     | Librerías y módulos del núcleo                                                                      |
| `/media`   | Información para medios extraíbles                                                                  |
| `/mnt`     | Monta los sistemas de archivos temporalmente                                                        |
| `/opt`     | Programas que instala el usuario (no forman parte del SO)                                           |
| `/proc`    | Información de los procesos y aplicaciones que se ejecutan en un momento determinado por el sistema |
| `/sbin`    | Archivos binarios con comandos que solo puede ejecutar el administrador                             |
| `/tmp`     | Archivos temporales                                                                                 |
| `/usr`     | Aplicaciones y recursos disponibles para los usuarios del sistema operativo                         |
| `/var`     | Archivos que cambian dinámicamente                                                                  |
| `/root`    | Es la `home` del usuario administrador `root`                                                       |

**Windows**
Su estructura de árbol predeterminada es la siguiente:

- **Windows**: Archivos del sistema operativo
- **Archivos de programa**: Se almacenan todos los programas instalados en el ordenador
- **Documents and settings**: Datos de los usuarios que acceden al equipo (escritorio, favoritos, etc)
	- **Archivos comunes**: Datos de programas que van a usar varios usuarios o aplicaciones
	- **Usuarios**: Carpetas de los diferentes usuarios
		- **Cookies**: Cookies de páginas webs
		- **Escritorio**: Contenidos del escritorio
		- **Favoritos**: Webs agregadas como favoritas
		- **Menú inicio**: Accesos directos del menú inicio
		- **Mis documentos**: Archivos del usuario

> Recordar que lo ideal es que los documentos de los usuarios se guarden en partición independiente al sistema operativo para que puedan estar salvaguardados mediante backups y respaldarse en caso de ser necesario
## 3.6. Búsqueda de información del sistema mediante comandos y herramientas gráficas 

Los **comodines** son símbolos que sirven para reemplazar cadenas de caracteres a la hora de realizar la búsqueda de información.

**DOS y Windows**
- **Asterisco (\*)** : Sustituye cadenas completas de caracteres. Puede usarse para reemplezar el nombre completo, alguna parte del nombre o su extensión.  Ej.: `DEL *.txt` elimina todos los documentos de texto.   
- **Interrogación (?)**: Reemplaza un solo carácter, pudiéndose poner varios símbolos de interrogación según las necesidades. Ej.: `DEL d??.txt` solo borrará archivos de texto que empiecen por la letra d y estén seguidos de dos caracteres  como (d03.txt, dat.txt,...)
El **comando de búsqueda en Windows** es `DIR [fichero a buscar] /s` (La flag `/s` buscará también en los subdirectorios)
Ej.: `DIR s*.doc*` busca archivos o directorios que comiencen por s y con extensión DOC, DOCX,...
Obviamente también puede usarse la herramienta gráfica del Explorador de Windows o software específicamente orientado a búsquedas como FileSearch.

**Linux**
El **comando de búsqueda en Linux** es `find`. Ej.:  `find *.odt`
Como herramienta gráfica se dispone de Nautilus, Krusader, Konqueror y demás administradores de archivos.
## 3.7. Identificación del software instalado mediante comandos y herramientas gráficas

**Windows**
Por herramientas gráficas en Windows se puede hacer en Panel de control > Programas > Programas y características. 
Desde el símbolo de sistema se puede ir a Archivos de programa y listar el directorio.

**Linux**
Se pueden consultar los paquetes instalados con las herramientas gráficas como el Centro de Software de Ubuntu que aporta el sistema o mediante el comando `dpkg`
## 3.8. Gestión de  la información del sistema. Rendimiento. Estadísticas

Obtención de datos cuantificables sobre el rendimiento...

**Windows**
Propiedades del Equipo > Evaluación de la experiencia en Windows con puntuaciones a diversos aspectos (gráficos, disco duro...) entre 1,0 y 7,9. Esta evaluación fue eliminada en la versión 8.1, pudiéndose visualizar ésta pero no de forma gráfica.

También hay más herramientas como el Monitor del rendimiento (Panel de control > Sistemas y seguridad > Herramientas administrativas > Monitor del rendimiento). Puede generar informes con los que pueden elaborarse estadísticas. 
También hay software específico como SiSoft Sandra.

**Linux**
Se puede monitorizar empleando la colección de herramientas específicas Sysstat. 

## 3.9. Montaje y desmontaje de dispositivos en sistemas operativos

El montaje y desmontaje de dispositivos generalmente se utiliza en Linux, estando también disponible en las últimas versiones de Windows.

Se denomina **unidad montada** a una partición asignada a una carpeta vacía de otra partición. En general a las unidades montadas se les asigna una etiqueta.

El montaje de dispositivos es útil cuando hay que compartir particiones o discos con grandes cantidades de usuario, ya que las unidades montadas ofrecen la posibilidad de ampliar las capacidades de almacenamiento de una unidad o partición.

Ejemplo: Se dispone de una carpeta de red DATOS en la que los usuarios guardan la información y se está llenando. Pero tenemos una unidad F: vacía. Se puede crear un directorio vacía llamado NOVIEMBRE en la carpeta DATOS y montar la unidad F: en dicho directorio. Así, los usuarios pueden guardar ficheros en DATOS\NOVIEMBRE aprovechando el espacio de la unidad F:.

#### 3.9.1. Windows
Panel de control > Sistema y seguridad > Herramientas administrativas > Administración de equipos > Almacenamiento > Administración de disco. 

**Montar**
Una vez listadas las particiones se hace clic con el botón derecho del ratón en la unidad que se quiere montar y se pulsa en "Cambiar la letra y rutas de acceso de unidad"
Se pulsa sobre "Agregar en Montar en la siguiente carpeta NTFS vacía" y se escribe la ubicación de la carpeta.
Tras aceptar los cambios la unida queda montada. 

**Desmontar**
Para desmontar, pulsar con el botón derecho del ratón sobre la unidad montada, hacer clic en "Cambiar la letra y rutas de acceso de unidad" y seleccionar "Quitar".

#### 3.9.2. Linux

Se utiliza el comando `mount`
Se le puede añadir la flag `-t` para indicar el tipo del sistema de archivos.

```shell
# MONTAR
# Estructura del comando
mount -t <sistema de archivos> <Dispositivo> <Punto de montaje>
# Montar el sistema ntfs de /dev/sda1 en /data/win
mount -t ntft /dev/sda1 /data/win

# DESMONTAR
# Estructura del comando
umount <Carpeta>
# Desmontar el sistema anterior usando el punto de montaje
umount /data/win
# Desmontar el sistema nateior usando el dispositivo
umount /dev/sda1
```

## 3.10. Automatización

Es recomendable automatizar muchas tareas rutinarias para que se ejecuten sin tener que estar pendiente de ellas.

##### En Windows 

**Copias de seguridad**
Windows incluye una función que permite crear copias de seguridad automáticas.

**Antivirus**
Todos los antivirus tienen opción de automatizar el análisis. En la seguridad interna de Windows se puede programar el análisis de Windows Defender.

**Otros**
Si la aplicación no da opciones, puede programarse igualmente usando herramientas como el Programador de tareas de Windows.
Panel de control > Sistema y seguridad > Herramientas administrativas > Administrador de equipos > Programador de tareas > Crear tarea.
Se puede definir qué tarea se ejecutará y en qué condiciones.

**Proceso por lotes**
Si las tareas deben completarse mediante comandos, puede utilizarse un **fichero de proceso de lotes**. Este tipo de archivos permite procesar la secunecia de comandos a partir de un archivo de texto sin formato (lanzar un script, vamos). 

- Inclusión de las tareas a automatizar en el fichero (Teclear los comandos correspondientes)
- Nombre del archivo: Nombrar el archivo con extensión `.bat`
- Programación de la ecuación del archivo mediante la pestaña Acciones del Programador de tareas.

(Aplicaciones como Advanced BAT 2 EXE Converter permiten convertir los archivos `.bat` en ejecutables `.exe`)

##### En Linux

Se puede utilizar el servicio `cron` para lanzar tareas regularmente en el momento especificado.

El demonio `cron` se ejecuta en segundo plano y verifica periódicamente si hay tareas programadas para ejecutarse.

- **Usuarios pueden definir tareas propias**:
    - Comando: `crontab -e` (edita las tareas del usuario actual).
    - Las tareas se guardan en `/var/spool/cron/crontabs/<usuario>`.
- **Tareas del sistema**:
    - Archivos en `/etc/cron.*` para tareas globales: - `/etc/cron.hourly`, `/etc/cron.daily`, `/etc/cron.weekly`, etc.

Un archivo crontab tiene entradas con el formato:
```
* * * * * comando
- - - - -
| | | | |
| | | | +--- Día de la semana (0 - 7, donde 0 y 7 = domingo)
| | | +----- Mes (1 - 12)
| | +------- Día del mes (1 - 31)
| +--------- Hora (0 - 23)
+----------- Minuto (0 - 59)
```

Por ejemplo:

- `0 5 * * * /path/to/script.sh`: Ejecuta el script todos los días a las 5:00 AM.
- `30 2 * * 1 /usr/bin/backup`: Realiza un respaldo cada lunes a las 2:30 AM.

## 3.11. Herramientas de administración de discos. Particiones y volúmenes. Desfragmentación y revisión

**Administración de particiones**

Se debe tener privilegios de administrador.

En Windows pueden modificarse particiones desde
Panel de control > Sistema y seguridad > Herramientas administrativas > Administración de equipos > Almacenamiento > Administración de discos
En el área inferior de la pantalla se pueden crear nuevas particiones, eliminar y redimensionar.

En Linux alguna de las herramientas utilizadas para la gestión de particiones son: Gparted, Pysdm, Partitionmanager.

**Desfragmentación y revisión**

Los constantes procesos de creación, borrado y modificación de archivos provocan la fragmentación de los ficheros que lleva a una ralentización del acceso a los datos, ya que los cabezales de los discos se ven obligados a desplazarse continuamente para acceder a la información, siendo necesario en ocasiones **desfragmentar**. También suele ser necesario **comprobar si hay errores** en el propio disco o partición.

En Windows puede desfragmentarse una partición en las Propiedades de la misma (A través de Equipo). En Herramientas, hacer clic en Desfragmentar ahora.
También existe una opción para analizar el disco en busca de errores en Herramientas > Comprobar ahora.

En Linux no es preciso desfragmentar las particiones en el sistema de ficheros que utilizan las versiones actuales.
Si se desea buscar errores en las mismas, puede hacerse mediante el comando `fsck`
