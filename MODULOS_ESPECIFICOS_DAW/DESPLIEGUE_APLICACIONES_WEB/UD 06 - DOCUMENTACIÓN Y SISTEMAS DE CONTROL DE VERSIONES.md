(UF4 Control de Versiones y Documentación)
Peso de la información (webp)
## 1. Documentación

## 2. Herramientas externas para la generación de documentación. Instalación, configuración y uso

**Funcionamiento de phpDocumentor**

**Instalación de phpDocumentor**

**Configuración de phpDocumentor**

## 3. Instalación, configuración y uso de JavaDoc

**Instalación de Javadoc**

**Documentando con Javadoc**

**Creación y uso de plantillas de código**

## 4. Sistema de control de versiones. Seguridad de los sistemas de control de versiones

### 4.1. Conceptos básicos

### 4.2. Procedimiento habitual

### 4.3. Sistemas de control de versiones centralizados y distribuidos

## 5. Git como sistema de control de versiones

### 5.1. Funcionamiento

### 5.2. Instalación de Git


### 5.3. Configuración de Git

### 5.4. Seguridad y documentación en Git


#### Quien usa mi puerto???
`sudo lsof -i :80`



ip addr show


icepush

Si buscas fiabilidad y un manejo eficiente de mensajes entre microservicios, RabbitMQ puede ser una buena opción. Si estás manejando grandes volúmenes de eventos y necesitas escalabilidad, Kafka es probablemente la mejor opción.
Usar **RabbitMQ** (o **Kafka**, aunque esto sería más adecuado en sistemas de alta demanda) puede **desacoplar** la generación del documento y su envío del flujo principal de la API.


### **Método 1: Usando `javap` (El Más Preciso)**

Primero, extrae el `.war` o `.jar` y busca un archivo `.class` dentro:

bash

CopiarEditar

`unzip archivo.war -d carpeta_extraida find carpeta_extraida -name "*.class" | head -n 1`

Ahora, usa `javap` en un archivo `.class` para ver su versión:

bash

CopiarEditar

`javap -verbose carpeta_extraida/alguna_clase.class | grep "major"`

Salida esperada:

yaml

CopiarEditar

`major version: 55`


find /ruta/al/directorio -type f -name "*.class" -exec javap -verbose {} \; 2>/dev/null | grep "major version" | awk '{print $3}'



--------

Diferencia
META-INF
y WEB-INF


Las carpetas **`WEB-INF`** y **`META-INF`** son directorios importantes en los archivos `.war` (y otros archivos empaquetados en Java), pero tienen propósitos distintos. Aquí te explico las diferencias principales:

### **1. `WEB-INF`**

- **Ubicación**: Solo se encuentra dentro de aplicaciones web basadas en **Servlets** o **JSP**. Es un directorio clave en un archivo `.war` (Web Application Archive).
    
- **Propósito**: Contiene información y configuraciones esenciales para el funcionamiento de la aplicación web.
    
- **Contenido típico**:
    
    - **`web.xml`**: El archivo de configuración de la aplicación web, que define los servlets, filtros, listeners, y otros parámetros relacionados con el ciclo de vida de la aplicación.
    - **`classes/`**: Contiene los archivos `.class` de Java (el código fuente compilado).
    - **`lib/`**: Contiene las bibliotecas externas (archivos `.jar`) que la aplicación web necesita.
    - **`tld/`** (opcional): Archivos de descripción de bibliotecas de etiquetas personalizadas para JSP.
- **Accesibilidad**: El contenido de `WEB-INF` no es accesible directamente desde el navegador web. Es decir, no se puede acceder a través de una URL. Es solo para uso interno de la aplicación.
    

### **2. `META-INF`**

- **Ubicación**: Se encuentra en todos los archivos empaquetados en formato **JAR**, **WAR**, **EAR** (Enterprise Archive), y otros archivos de Java. En un archivo `.war`, normalmente se encuentra a nivel de la raíz del archivo.
    
- **Propósito**: Almacena metadatos del archivo y la aplicación en general. Estos metadatos pueden ser usados por el entorno de ejecución o herramientas de construcción.
    
- **Contenido típico**:
    
    - **`MANIFEST.MF`**: El archivo que contiene información sobre el paquete o archivo, como la versión del archivo, la clase principal (si es un archivo JAR ejecutable), dependencias, y otros atributos de metadatos.
    - **`services/`**: Puede contener archivos de configuración relacionados con servicios en Java (como **ServiceLoader**).
    - Otros archivos de metadatos relacionados con herramientas, frameworks, y servicios.
- **Accesibilidad**: El contenido de `META-INF` es accesible para el entorno de ejecución, pero **no está destinado a ser servido directamente** por el servidor web. Se usa principalmente para información interna de la aplicación y configuraciones.
### **Resumen de Diferencias**:

|Característica|`WEB-INF`|`META-INF`|
|---|---|---|
|**Ubicación**|Solo en aplicaciones web `.war`|En archivos `.jar`, `.war`, `.ear`|
|**Propósito**|Contiene archivos y configuraciones web (servlets, JSP, clases, bibliotecas)|Contiene metadatos del archivo (como el `MANIFEST.MF`)|
|**Accesibilidad**|No accesible desde el navegador, solo para la aplicación|No accesible desde el navegador, solo para herramientas y el entorno de ejecución|
|**Ejemplos de Archivos**|`web.xml`, `classes/`, `lib/`|`MANIFEST.MF`, `services/`|

En resumen:

---

Numero de paginas en VIM

- `:set number`
- - `:syntax on`


Si quieres dejarlo permanente, añade esto a tu archivo `~/.vimrc`:

- set number
- `syntax on`

Buscar en que linea se encuentra algo: 

`/<palabra>`


##
Eliminar programa
`sudo apt --purge remove vsftpd`
### Buscar ficheros

find /ruta/de/búsqueda -type f -name "archivo.txt"

------
https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/net/URLConnection.html#setConnectTimeout(int)

connection.setConnectTimeout(getTimeoutInSeconds() * 1000);
connection.setReadTimeout(getTimeoutInSeconds() * 1000);


----

Codigo virgulilla 
AltGr + 4

--
Permisos directorio
ls -ld /path/to/directory

--
pwd donmdeestyo

---

```(En ambos casos si no existe, se crea)
# Se sobreescribe
echo "<h1> Hola desde el directorio</h1>" > /public_html/index.html
# Se añade a lo que haya
```

---

`curl -I http://localhost`

```
 -d, --data <data>          HTTP POST data
 -f, --fail                 Fail silently (no output at all) on HTTP errors
 -h, --help <category>      Get help for commands
 -i, --include              Include protocol response headers in the output
 -o, --output <file>        Write to file instead of stdout
 -O, --remote-name          Write output to a file named as the remote file
 -s, --silent               Silent mode
 -T, --upload-file <file>   Transfer local FILE to destination
 -u, --user <user:password> Server user and password
 -A, --user-agent <name>    Send User-Agent <name> to server
 -v, --verbose              Make the operation more talkative
 -V, --version              Show version number and quit


```


`sudo systemctl enable vsftpd`

https://www.udemy.com/course/guia-completa-de-docker-kubernetes-con-spring-boot/learn/lecture/32376018?start=0#overview

https://www.udemy.com/course/rabbitmq-para-programadores-java/learn/lecture/22579604#reviews


https://www.udemy.com/course/curso-completo-junit-mockito-spring-boot-test/learn/lecture/26048280?start=156#overview

https://www.udemy.com/course/master-en-css-responsive-sass-flexbox-grid-y-boostrap-4/learn/lecture/16693858?start=0#overview

https://www.udemy.com/course/master-en-php-sql-poo-mvc-laravel-symfony-4-wordpress/learn/lecture/11933206?start=0#overview

https://www.udemy.com/course/rabbitmq-in-practice/?couponCode=KEEPLEARNING


```
docker run -it --rm --name rabbitmq -p 5672:5672 -p 15672:15672 rabbitmq:4.0-management
```


RabbitMQ

### **Descomprimir el archivo `.tar.gz`:**

bash

CopiarEditar

`tar xvzf apache-tomcat-X.X.XX.tar.gz`

- **`tar`** es un comando para **archivar** y **descomprimir** archivos en sistemas Unix/Linux.
- **`xvzf`** son opciones que indican:
    - `x`: Extraer (descomprimir) el archivo.
    - `v`: Verbose (mostrar detalles mientras descomprime).
    - `z`: Usar gzip (especifica que el archivo está comprimido con gzip).
    - `f`: Indica que se está trabajando con un archivo de nombre específico (en este caso, `apache-tomcat-X.X.XX.tar.gz`).

Por lo tanto, el comando descomprime el archivo `apache-tomcat-X.X.XX.tar.gz` (donde `X.X.XX` es la versión de Tomcat) en el directorio actual.


