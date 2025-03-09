## 1. Arquitecturas web. Modelos.

- La **arquitectura web** (World Wide Web, www) de Internet da un modelo de conexión poderoso y flexible por el que cualquier equipo puede adaptarse a sus requerimientos. 
- Los **contenidos se localizan** gracias a los **web browsers** o buscadores que encuentran la información requerida con las peticiones enviadas a diversos servidores para que se les respondan las páginas que más se adaptan a los parámetros de búsqueda.
- El **contenido en la web se visualiza** siguiendo unos **estándares** que permiten a que los navegadores los interpreten correctamente (HTML, JavaScript, CSS,...)
- **Las operaciones de transferencia** también están estandarizadas. Cada servicio sigue una serie de **protocolos** que permiten abstraerse de la tecnología y del sistema operativo. De los más conocidos es el protocolo HTTP (HyperText Transfer Protocol, protocolo de transferencia de hipertexto) por el que un cliente puede visualizar páginas web.

**Características de la arquitectura web**
- **Escalabilidad**: Fácilmente es posible conectarse a distintos equipos de la red (servidores, enrutadores, switches) sin que la red se vea influida ni obligada a cambiar de forma constante. 
- **Separación de responsabilidades**: Se separan elementos: clientes y servidores; peticiones y respuestas. Así se permite el trabajo de forma más organizada y estructura, adaptándose a las necesidades. 
- **Amplia conectividad**: Servidores y administradores proveen conexión óptima y segura entre cualquier cantidad de nodos.
- **Recursos compartidos**: Se aprovechan los recursos que se comparten entre clientes



**Modelo de la arquitectura web**

**Funcionamiento de los servicios web**


## 2. Servidores web y de aplicaciones. Instalación y configuración básica.

### 2.1. Servidor web. Instalación de Apache en Linux

### 2.2. Servidor de aplicaciones. Instalación de Tomcat en Linux

### 2.3. Estructura y recursos que componen una aplicación web

#### El descriptor de despliegue





---

**XAML**: Solución completa y gratuita para crear un servidor local en el ordenador.
Permite desarrollar y probar aplicaciones web en un entorno controlado antes de implementarlas en un servidor en línea.
Está diseñado para ser fácil de instalar y de usar.
Se combina servidor web Apache, base de datos, lenguajes de programación y otras herramienta esenciales.
Sus características son:
- **Paquete de Software Todo-en-Uno**: XAMPP es un conjunto de herramientas de software que incluye Apache (servidor web), MySQL o MariaDB (BBDD), PHP y Perl.
- **Multiplataforma**. Diseñado principalmente para WIndows, macOS y Linux.
- **Fácil de instalar y de usar**
- **Entorno de pruebas local**: Permite probar y depurar aplicaciones web sin necesidad de un servidor en línea, reduciendo tiempos de carga y facilitando la iteración rápida.
- **Versatilidad para desarrollo**.Soporta PHP y Perl y puede configurarse para soportar otros lenguajes y herramientas. 

https://www.apachefriends.org/es
XAMPP for Windows (8.2.12 - PHP 8.2.12)
Apache corre en 80 (HTTP) y 443 (HTTPS)

**Servidor**: Programa informático dentro de un sistema operativo, identificándose con su número de proceso (PID)

Corre en: localhost   127.0.0.1
Se almacenan las webs dentro de `htdocs`


Si se consulta el fichero `phpinfo.php`, se puede ver toda la información del servidor con los módulos de Apache cargados y mucha más información.

```php
<?php phpinfo(); ?>
```

Para desplegar una página de ejemplo solo hay que mover el contenido a `htdocs`
Y, según el directorio, ese será su contexto:
http://localhost/backs/index.html
http://localhost/backs/street/index.html

### Módulos

#### Activar módulos
Los módulos se encuentran en `xampp\apache\modules`. Tienen extensión `.so`. 
Es necesario ir a xampp\apache\conf y abrir el archivo **httpd.conf**
Allí se busca el módulo que se quiera activar y se descomenta la línea.
Siempre reiniciar traslos cambios. 
#### mod_rewrite

Módulo útil para reescrituras de URLs.
Descomentar:
`LoadModule rewrite_module modules/mod_rewrite.so`

**Añadir reglas de reescritura**
Si se quiere habilitar archivos `.htaccess` para definir las reglas de reescritura debe esta habilitada en la parte del fichero correspondiente a `<Directory "C:/xampp/htdocs">` la regla: `AllowOverride All`

Los pasos a seguir son:
1.- **Crear archivo `.htaccess` en `xampp/htdocs`**
2.- Introducir la regla de redirección:
```
RewriteEngine On
RewriteRule ^about$ about.html [L]
RewriteRule ^.*/about$ about.html [L]
```

Esto significa que si la URL solicitada es `about` (sin la barra inclinada al final), Apache redirigirá a `about.html`. La `L` asegura que si esta regla se aplica, no se ejecutarán más reglas de reescritura después de esta.
Como vemos se puede poner la expresión regular que uno quiera. 

#### mod_ssl

Para utilizar protocolo HTTPS (comunicación SSL/TLS).
Descomentar:
`LoadModule ssl_module modules/mod_ssl.so`
Y la línea de la configuración para añadirla:
`Include conf/extra/httpd-ssl.conf`

**Verificar que el puerto SSL está configurado en**: 
`conf/extra/httpd-ssl.conf` tiene que estar `Listen 443`.

**Generar certificado**
Se hace mediante OpenSSL (Apache lo tiene incluido en su carpeta de binarios):
Ejecutando:
```powershell
# Generar clave privada
openssl genrsa -out server.key 2048
# Generar certificado autofirmado
openssl req -new -x509 -key server.key -out server.crt -days 365
```

Significado:
- `genrsa`: Genera una clave privada RSA.
- `-out server.key`: Guarda la clave privada en un archivo llamado `server.key`.
- `2048`: Especifica la longitud de la clave en bits (2048 bits es un estándar seguro).

- `req -new`: Crea una nueva solicitud de certificado.
- `-x509`: Indica que el certificado será **autofirmado** (no emitido por una CA externa).
- `-key server.key`: Usa la clave privada generada en el paso anterior (`server.key`).
- `-out server.crt`: Guarda el certificado en el archivo `server.crt`.
- `-days 365`: Especifica la validez del certificado (1 año).

Los ficheros `server.key` y `server.crt` se deben ubicar en:
```
C:\xampp\apache\conf\ssl.key\
C:\xampp\apache\conf\ssl.crt\
```

Y confirmar que en `httpd-ssl.conf` se apunta a los certificados que se han generado: 
```
SSLCertificateFile "C:/xampp/apache/conf/ssl.crt/server.crt"
SSLCertificateKeyFile "C:/xampp/apache/conf/ssl.key/server.key"
```


#### mod_expires

Módulo que permite controlar los encabezados de caducidad (headers de expiración) de las respuestas HTTP. Es útil para gestionar la caché del navegador indicándole cuánto tiempo deben almacenarse los archivos estáticos (imágenes, CSS, JavaScript) antes de solicitarlos de nuevo al servidor. 

Con él:
- se **mejora el rendimiento** al reducir la carga del servidor y el tiempo de carga de las páginas para los usuarios. 
- se **reduce el ancho de banda** al reutilizar recursos, evitando descargarlos repetidamente.
- se **mejora la experiencia del usuario** que experimenta un acceso más rápido a la web.

Los encabezados agregados son:
- `Expires`: Indica la fecha y hora hasta la cual el navegador
mantendrá en caché ese recurso (HTTP/1.0 )
- `Cache-Control`: Con max-age indica el tiempo (HTTP/1.1)
en segundos que el recurso será almacenado en caché (604800 segundos es
igual a 1 semana).

Usados juntos, Cache-Control tiene prioridad en HTTP/1.1 y posteriores. 

Descomentar:
`LoadModule expires_module modules/mod_expires.so`

Ejemplo de configuración que puede agregarse a Apache o al archivo `.htaccess` del sitio web:

```xml
<IfModule mod_expires.c>
	ExpiresActive On
	ExpiresByType image/jpg "access plus 1 month"
	ExpiresByType image/jpeg "access plus 1 month"
	ExpiresByType image/gif "access plus 1 month"
	ExpiresByType image/png "access plus 1 month"
	ExpiresByType text/css "access plus 1 week"
	ExpiresByType application/javascript "access plus 1 week"
	ExpiresByType text/html "access plus 0 seconds"
</IfModule>
```

- `ExpiresActive On`: Habilita el uso de `mod_expires`
- `ExpiresByType`: Define la política de expiración en función del MIMEType.  (1 month, 1 week, 1 day,...)

### Pruebas 
https://gtmetrix.com/
https://www.webpagetest.org/
Lighthouse
Analizan el tiempo de carga de un sitio web y verifican si los encabezados de caché están configurados correctamente. También dan información sobre los recursos y dicen si la caducidad de la caché está bien configurada en el servidor Apache. 


#### mod_userdir

Permite a los usuarios acceder a sus propios directorios personales a través de URLs específicas. Contenido alojado en subdirectorios dentro del home del usuario como por ejemplo: `http://example.com/~pepito`

Así:
- Cada usuario tiene su especio
- Se facilita la creación de sitios web por múltiples usuarios

```bash
# Activar el modulo userdir
sudo a2enmod userdir
# Crear usuario pepito
sudo adduser pepito
# Le damos permisos de sudo
sudo usermod -aG sudo pepito
# Iniciamos sesión (Se crea directorio personal y configuraciones basicas)
su - pepito
# Crear archivo HTML en directorio publico del usuario 
mkdir /public_html
echo "<h1> Hola desde el directorio</h1>" > /public_html/index.html
# Reiniciar Apache
systemctl restart apache2
```

¡Cuidado con los permisos!


#### mod_headers

Permite modificar encabezados HTTP de las respuestas y solicitudes que maneja el servidor. Así se puede ajustar el caché, controlar la seguridad o personalizar cómo los navegadores manejan las solicitudes.

**Funciones**
- Añadir, modificar eliminar encabezados HTTP
- Configurar políticas de seguridad como:
		- Content-Security-Policy
		- X-Frame-Options
- Controlar manejo de caché con Cache-Control. 

Habilitarlo:
`sudo a2enmod headers`

Edita tu archivo de configuración de Apache (`/etc/apache2/sites-available/000-default.conf` ) y
añade lo siguiente dentro de un bloque `<VirtualHost>`:
```xml
<IfModule mod_headers.c>
Header set Cache-Control "max-age=3600, must-revalidate"
</IfModule>

<!--navegador que almacene en caché el contenido
durante 1 hora (3600 segundos) y que debe validar la caché cuando expire.!-->
```























#### Tomcat
Corre en el 8080
Las aplicaciones web para Tomcat van en `\xampp\tomcat\webapps`

- Pongamos un directorio como "myapp". En él crear un archivo JSP llamado `index.jsp`
- En el directorio pongamos una carpeta `WEB-INF`




En **Apache Tomcat**, puedes desplegar aplicaciones de dos maneras principales:

1. **Aplicación en forma de directorio (exploded deployment)**
    
    - Puedes colocar tu aplicación de Java EE como un directorio con todos sus archivos ya extraídos en la carpeta `webapps/`.
    - Por ejemplo, si tu aplicación se llama `miapp`, deberías tener una estructura como esta dentro de `webapps/`:
```
tomcat/
├── webapps/
│   ├── miapp/
│   │   ├── WEB-INF/
│   │   ├── META-INF/
│   │   ├── index.jsp
│   │   ├── ...

```

    - Tomcat detectará automáticamente la aplicación y la desplegará.
2. **Desplegar un archivo `.war` (WAR deployment)**
    
    - Puedes colocar un archivo `.war` dentro del directorio `webapps/`.
        `tomcat/ ├── webapps/ │   ├── miapp.war`
    - Tomcat descomprimirá automáticamente el `.war` y lo desplegará.

### ¿Y qué pasa con los archivos `.jar`?

- Tomcat **NO** ejecuta directamente archivos `.jar` como lo haría **Spring Boot** u otro framework que use `java -jar app.jar`.
- Si tienes una aplicación como un **JAR ejecutable** (por ejemplo, una aplicación Spring Boot empacada como `miapp.jar`), lo correcto es ejecutarla con: `java -jar miapp.jar`  en lugar de desplegarla en Tomcat.

En **Apache Tomcat**, la administración de despliegues de archivos `.war` se realiza a través del **Tomcat Manager**, que requiere autenticación. La administración de usuarios y contraseñas se maneja en el archivo `tomcat-users.xml`.

### **¿Qué significan estos roles?**

- `manager-gui` → Permite acceder a la interfaz web del Manager.
- `manager-script` → Permite desplegar WARs vía línea de comandos o scripts.
- `manager-jmx` → Permite monitorizar Tomcat vía JMX.
- `manager-status` → Permite ver el estado del servidor.

## Acceder al Tomcat Manager

http://localhost:8080/manager/html


## Desplegar un `.war` vía línea de comandos

```bash
# Desplegar app
curl -u admin:admin -T miapp.war "http://localhost:8080/manager/text/deploy?path=/miapp&update=true"
# Eliminar app
curl -u admin:admin123 "http://localhost:8080/manager/text/undeploy?path=/miapp"
# Reiniciar app
curl -u admin:admin123 "http://localhost:8080/manager/text/reload?path=/miapp"
```


📌 Ruta: `$TOMCAT_HOME/conf/server.xml`

```
De (No escucha fuera de localhost)
<Connector port="8080" protocol="HTTP/1.1"
           connectionTimeout="20000"
           redirectPort="8443" />
A
<Connector address="0.0.0.0" port="8080" protocol="HTTP/1.1"
           connectionTimeout="20000"
           redirectPort="8443" />
```


```
De
<Host name="localhost"  appBase="webapps"
            unpackWARs="true" autoDeploy="true">
A
 <Host name=""  appBase="webapps"
            unpackWARs="true" autoDeploy="true">
```

Por defecto, Tomcat **bloquea el acceso al Manager desde IPs remotas**. Para permitir acceso desde cualquier IP:
`$TOMCAT_HOME/webapps/manager/META-INF/context.xml`
Y cambia `allow="..."` a: `allow=".*"`

         allow="127\.\d+\.\d+\.\d+|::1|0:0:0:0:0:0:0:1" />


Dejar eso en `webapp/prueba` como index.jsp

```jsp
<%@ page language="java" contentType="text/html; charset=UTF-8" pageEncoding="UTF-8"%> 

# ¡Hola desde Tomcat!

La hora actual es: <%= new java.util.Date() %>
```

Y cuando se entra en localhost:8080/prueba
Sale.



------

### Apache Ubuntu

```shell
# Actualizar paquetes
sudo apt update
# Instalar Apache
sudo apt install apache2
# Acceder a localhost/ (O hacer un curl)
curl localhost/
# Comprobar estado Apache
sudo systemctl status apache2
# Instalar modulo wsgi para usar pythonen Apache
sudo apt install apache2 python3 python3-pip
# Instalar mod_wsgi de Apache
sudo apt install libapach2-mod-wsgi-py3
# Habilitarlo
sudo a2enmod wsgi
# Crear app python
sudo mkdir /var/www/html/myapp
# Crear archivo python myapp.wsgi
sudo vim /var/www/html/pyapp/myapp.wsgi
# Cambiar sus permisos para asegurarnos de que se puede leer
sudo chown www-data:www-data /var/www/html/pyapp/myapp.wsgi  
sudo chmod 755 /var/www/html/pyapp/myapp.wsgi
```

```python
def application(environ, start_response):  
	status = '200 OK'  
	output = b'Hello, this is a Python application running on Apache!'  
	response_headers = [('Content-type', 'text/plain'),  ('Content-Length', str(len(output)))]  
	start_response(status, response_headers)  
	return [output]
```

Añadir a `sudo nano /etc/apache2/sites-available/000-default.conf`
La configuración para servir aplicación python: 

```
WSGIScriptAlias /pyapp /var/www/html/pyapp/myapp.wsgi  
<Directory /var/www/html/pyapp>  
Require all granted  
</Directory>
```

Reiniciar apache:
`sudo systemctl restart apache2`
Probar: localhost/pyapp
### Tomcat Ubuntu
```shell
sudo apt install openjdk-11-jdk
sudo apt install tomcat10 tomcat10-admin
sudo systemctl status tomcat10
sudo mkdir /var/lib/tomcat10/webapps/myapp
sudo vim /var/lib/tomcat10/webapps/myapp/index.jsp
sudo systemctl restart tomcat10
```


----

`tail -f /var/log/apache2/error.log`

El usuario de Apache suele ser `www-data`
### Permisos necesarios para `www-data`:

1. **Permisos de directorios**:
    
    - Apache necesita **permisos de ejecución** en los directorios para poder acceder a ellos. Sin los permisos de ejecución, Apache no podrá acceder a los contenidos dentro de los directorios.
    - También necesita **permisos de lectura** en los directorios para poder listar los archivos dentro de ellos si se necesita.
755
2. **Permisos de archivos**:
    
    - Apache necesita **permisos de lectura** para los archivos para poder servirlos a los usuarios.
644


---

#### Hosts Virtuales


1.- Crear estructura de directorios con los datos del sitio y revisar permisos.
El directorio `/var/www` albergará el document root (directorio superior donde Apache busca el contenido a mostrar).

```bash
# Crear directorio
sudo mkdir -p /var/www/despliegue.com/public.html
# Revisar propiedad
sudo chown -R $USER:$USER /war/www/despliegue.com/public_html
# Garantizar acceso de lectura a directorios webs comunes y archivos y carpetas
sudo chmod -R 755 /var/www
# Crear un index.html para el istio

```

2.- Configurar host virtual
Se copia el archivo predeterminado que indica cómo responde Apache a las solicitudes (`000-default.conf`) a un nombre especifico `despliegue.com.conf`

```xml
<VirtualHost *:80>
ServerAdmin webmaster@localhost
DocumentRoot /var/www/html
ErrorLog ${APACHE_LOG_DIR}/error.log
CustomLog ${APACHE_LOG_DIR}/access.log combined
</VirtualHost>
```

- Se modifica  `ServerAdmin` para que el administrador del sitio pueda recibir correos
- Se modifica `ServerName` para establecer el dominio base que debe coincidir con la definición del hostvirtual
- Se modifica `ServerAlias` que define los nombres adicionales. 

Quedando así: 

```xml
<VirtualHost *:80>
ServerAdmin admin@despliegue.com
ServerName despliegue.com
ServerAlias www.despliegue.com
DocumentRoot /var/www/despliegue.com/public_html
ErrorLog ${APACHE_LOG_DIR}/error.log
CustomLog ${APACHE_LOG_DIR}/access.log combined
</VirtualHost>
```

Habilitar el archivo host virtual y deshabilitar el sitio perdeterminado
```
sudo a2ensite despliegue.com.conf
sudo a2dissite 000-default.conf
```

Se modificará `etc/hosts` para probar el host virtual, añadiendo la IP del servidor y el nombre de dominio. 
`ip addr show`

```
127.0.0.1 localhost
127.0.1.1 guest-desktop
192.168.226.139 despliegue.com
```

### 1. **Hosts Virtuales en Apache**:

Un **host virtual** en Apache es una configuración que permite que un único servidor Apache sirva múltiples sitios web (o aplicaciones) desde la misma máquina, utilizando diferentes nombres de dominio o direcciones IP.

- **Definición**: En Apache, un "host virtual" es un bloque de configuración que asocia un nombre de dominio (por ejemplo, `mi-sitio.com`) o una dirección IP con un directorio específico en el sistema de archivos donde se encuentran los archivos del sitio web.
    
- **Configuración**: En Apache, los hosts virtuales se definen en archivos de configuración (generalmente en `/etc/apache2/sites-available/` en sistemas basados en Debian o `/etc/httpd/conf.d/` en sistemas basados en Red Hat). Un ejemplo de configuración de un host virtual podría ser:
    
    apache
    
    CopiarEditar
    
    `<VirtualHost *:80>     ServerAdmin webmaster@mi-sitio.com     DocumentRoot /var/www/mi-sitio     ServerName mi-sitio.com     ErrorLog ${APACHE_LOG_DIR}/error.log     CustomLog ${APACHE_LOG_DIR}/access.log combined </VirtualHost>`
    
    En este caso, Apache servirá el contenido de `/var/www/mi-sitio` cuando alguien acceda a `mi-sitio.com`.
    
- **Función principal**: Los hosts virtuales permiten que Apache sirva múltiples sitios web desde un solo servidor, basándose en el nombre de dominio que se usa para hacer la solicitud HTTP.

Cuando un cliente realiza una solicitud, por ejemplo, a través de un navegador, la solicitud HTTP contiene varias cabeceras, entre ellas la cabecera **Host**, que especifica el nombre de dominio o subdominio solicitado. Apache utiliza esta cabecera para determinar qué **host virtual** debe usar para servir el contenido adecuado.


### Proxy inverso


Un **proxy inverso** es un servidor que actúa como intermediario entre los clientes (por ejemplo, los navegadores de los usuarios) y uno o más servidores de backend. El proxy inverso recibe las solicitudes del cliente y las redirige a los servidores internos que realmente manejarán esas solicitudes (por ejemplo, un servidor de aplicaciones o un servidor web).

La principal diferencia entre un proxy directo y un proxy inverso es que, en un **proxy inverso**, el cliente nunca interactúa directamente con el servidor backend; en cambio, siempre se comunica con el proxy, que redirige las solicitudes según sea necesario.

**¿Por qué usar un Proxy Inverso?**

- **Balanceo de carga**: Distribuir solicitudes entre varios servidores backend.
- **Seguridad**: Ocultar la infraestructura interna de los usuarios.
- **Caché**: Mejorar el rendimiento almacenando en caché el contenido que se sirve de manera frecuente.
- **SSL Offloading**: Descartar la carga del cifrado SSL de los servidores backend y dejarlo a cargo del proxy

### ¿Se puede hacer un Proxy Inverso en Apache?

Sí, Apache también puede configurarse como un **proxy inverso**. Utiliza los módulos `mod_proxy` y `mod_proxy_http` para redirigir solicitudes a otros servidores o aplicaciones backend.

### Pasos para configurar un Proxy Inverso en Apache

**Habilitar los módulos necesarios**:

Para habilitar el proxy inverso en Apache, necesitas asegurarte de que los módulos `mod_proxy`, `mod_proxy_http` (para HTTP) y, si es necesario, `mod_ssl` (para HTTPS) estén habilitados. Si usas Apache en un sistema basado en Debian (como Ubuntu), puedes habilitarlos con los siguientes comandos:

```bash
sudo a2enmod proxy sudo a2enmod proxy_http sudo a2enmod ssl
```

**Configurar el Proxy Inverso**:

Supongamos que se tiene una aplicación backend corriendo en: `http://localhost:8080` y se quiere que Apache redirija las solicitudes de `http://mi-sitio.com` a esa aplicación.

```xml
<VirtualHost *:80>
	ServerName mi-sitio.com
	# Habilitar Proxy Inverso
	ProxyPass / http://localhost:8080/
	ProxyPassReverse / http://localhost:8080/
	# Opcional: Habilitar el logging
	ErrorLog ${APACHE_LOG_DIR}/error.log
	CustomLog ${APACHE_LOG_DIR}/access.log combined
</VirtualHost>
```

**ProxyPass**: Esta directiva le indica a Apache que redirija todas las solicitudes que lleguen a `/` en `http://mi-sitio.com` hacia `http://localhost:8080/`.

 **ProxyPassReverse**: Esta directiva se asegura de que cualquier respuesta que el servidor de backend envíe de vuelta se reescriba correctamente para que parezca que está llegando de Apache, no del servidor backend.

```
<VirtualHost *:80>
    ServerName app1.com

    ProxyPreserveHost On
    ProxyPass / http://localhost:8080/app1/
    ProxyPassReverse / http://localhost:8080/app1/
</VirtualHost>

<VirtualHost *:80>
    ServerName app2.com

    ProxyPreserveHost On
    ProxyPass / http://localhost:8080/app2/
    ProxyPassReverse / http://localhost:8080/app2/
</VirtualHost>
```


---

El comando: `sudo certbot --apache -d app1.com -d app2.com`

sirve para **generar y configurar certificados SSL gratuitos** usando **Let's Encrypt** en un servidor Apache.
1. **Solicita certificados SSL** para `app1.com` y `app2.com`.
2. **Configura automáticamente Apache** para usar HTTPS.
3. **Redirige el tráfico HTTP a HTTPS** (si lo confirmas en la instalación).
---















TOMATCAT 8080


### **Archivo de configuración: `server.xml`**

Ubicación típica:

bash

CopiarEditar

`<TOMCAT_HOME>/conf/server.xml`

Dentro de este archivo, encontrarás una sección como esta:

xml

CopiarEditar

`<Connector port="8080" protocol="HTTP/1.1"            connectionTimeout="20000"            redirectPort="8443" />`

- Aquí, `port="8080"` indica que Tomcat es


/var/lib/tomcat9


















### **¿Qué significan estos roles?**

- `manager-gui` → Permite acceder a la interfaz web del Manager.
- `manager-script` → Permite desplegar WARs vía línea de comandos o scripts.
- `manager-jmx` → Permite monitorizar Tomcat vía JMX.
- `manager-status` → Permite ver el estado del servidor.






























## 1. Arquitecturas web. Modelos

**Origen HTTP/HTML** 
- Finales de los 80. Científicos del CERN. Trabajan con PC no compatibles, no podían compartir su trabajo. 
- Tim Berners-Lee. Propuesta para desarrollar sistema de hipertexto sobre Internet. 
- Se desarrolla sobre protocolos TCP/IP (desde los 50, pruebas Arpanet). 
	- Formato de texto para representar documentos de hipertexto (HyperText Markup Language HTML)
	- Protocolo para intercambio de documentos (HyperText Transfer Protocol HTTP)

**Funcionamiento del navegador web**
- Se escribe dirección web


## 2. Servidores web y de aplicaciones. Instalación y configuración básica






## 3. Estructura y recursos web. Descriptor de despliegue




#### Proxy inverso Nginx

En `/etc/nginx/sites-available/default`

```json
server {
        listen 80;
        server_name llevalatarara.com;

        location / {
                proxy_pass http://localhost:9090/lluvia/;
                proxy_set_header Host $host;
                proxy_set_header X-Real-IP $remote_addr;
                proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
                proxy_set_header X-Forwarded-Proto $scheme;
        }
        error_log /var/log/nginx/mi-sitio-error.log;
        access_log /var/log/nginx/mi-sitio-access.log;
}
```

```json
# Configuración para HTTP (puerto 80)
server {
    listen 80;
    server_name llevalatarara.com;

    # Redirigir tráfico HTTP a HTTPS
    return 301 https://$host$request_uri;
}

# Configuración para HTTPS (puerto 443)
server {
    listen 443 ssl;
    server_name llevalatarara.com;

    # Ubicación del certificado SSL y la clave
    ssl_certificate /etc/nginx/ssl/server.crt;
    ssl_certificate_key /etc/nginx/ssl/server.key;

    # Seguridad SSL: protocolos y ciphers recomendados
    ssl_protocols TLSv1.2 TLSv1.3;
    ssl_ciphers 'ECDHE-ECDSA-AES128-GCM-SHA256:ECDHE-RSA-AES128-GCM-SHA256:DHE-RSA-AES128-GCM-SHA256';
    ssl_prefer_server_ciphers on;

    # Seguridad adicional
    add_header Strict-Transport-Security "max-age=31536000; includeSubDomains; preload" always;
    ssl_stapling on;
    ssl_stapling_verify on;
    ssl_session_cache shared:SSL:10m;
    ssl_session_timeout 10m;

    # Proxy inverso: Redirige tráfico a la aplicación en el puerto 9090
    location / {
        proxy_pass http://localhost:9090/lluvia/;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
    }

    # Archivos de log
    error_log /var/log/nginx/mi-sitio-error.log;
    access_log /var/log/nginx/mi-sitio-access.log;
}

```

**Explicación**
1. **Redirección de HTTP a HTTPS (en el puerto 80):**
    
    - La primera parte redirige todo el tráfico HTTP (`listen 80`) a HTTPS utilizando un redirección permanente (301).
    - Esto garantiza que los usuarios siempre usarán HTTPS al acceder a tu dominio, incluso si escriben `http://llevalatarara.com`.
2. **Configuración HTTPS (en el puerto 443):**
    
    - Aquí es donde configuramos Nginx para servir tráfico seguro con SSL (`listen 443 ssl`).
    - **`ssl_certificate` y `ssl_certificate_key`**: Se configuran con las ubicaciones de tu certificado SSL (`server.crt`) y la clave privada (`server.key`).
    - **Protocolos y ciphers**: Definimos qué protocolos y ciphers se usarán para asegurar la conexión.
        - `TLSv1.2` y `TLSv1.3` son los protocolos recomendados, mientras que los ciphers son elegidos para asegurar una transmisión fuerte.
    - **Seguridad adicional**: Se activan características como **HSTS**, **SSL Stapling** y el **caché de sesiones SSL** para aumentar la seguridad y mejorar el rendimiento.
3. **Proxy Inverso:**
    
    - La directiva `proxy_pass` envía el tráfico hacia `http://localhost:9090/lluvia/`, que es donde se está ejecutando tu aplicación.
    - Las directivas `proxy_set_header` aseguran que la información de los encabezados HTTP se pase correctamente a tu servidor backend.
4. **Archivos de log**:
    
    - Los archivos de log (`error_log` y `access_log`) están configurados para registrar los accesos y errores de tu servidor Nginx.

### **Pasos adicionales:**

1. Asegúrate de que el certificado y la clave SSL estén correctamente ubicados en `/etc/nginx/ssl/`.
    - Si no has creado la carpeta, puedes hacerlo con `sudo mkdir -p /etc/nginx/ssl/` y mover los archivos `server.crt` y `server.key` allí.
2. **Reiniciar Nginx** para aplicar los cambios:
    
    bash
    
    CopiarEditar
    
    `sudo systemctl restart nginx`




```
# Configuración para app1.com (con HTTPS)
server {
    listen 80;
    server_name app1.com;

    # Redirigir tráfico HTTP a HTTPS
    return 301 https://$host$request_uri;
}

server {
    listen 443 ssl;
    server_name app1.com;

    # Ubicación del certificado SSL y la clave
    ssl_certificate /etc/nginx/ssl/app1.crt;
    ssl_certificate_key /etc/nginx/ssl/app1.key;

    # Configuración de SSL
    ssl_protocols TLSv1.2 TLSv1.3;
    ssl_ciphers 'ECDHE-ECDSA-AES128-GCM-SHA256:ECDHE-RSA-AES128-GCM-SHA256:DHE-RSA-AES128-GCM-SHA256';
    ssl_prefer_server_ciphers on;

    # Seguridad adicional
    add_header Strict-Transport-Security "max-age=31536000; includeSubDomains; preload" always;

    # Proxy inverso: Redirige tráfico a la aplicación en el puerto 8080
    location / {
        proxy_pass http://localhost:8080/;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
    }

    # Logs de acceso y error
    error_log /var/log/nginx/app1-error.log;
    access_log /var/log/nginx/app1-access.log;
}

# Configuración para app2.com (con HTTPS)
server {
    listen 80;
    server_name app2.com;

    # Redirigir tráfico HTTP a HTTPS
    return 301 https://$host$request_uri;
}

server {
    listen 443 ssl;
    server_name app2.com;

    # Ubicación del certificado SSL y la clave
    ssl_certificate /etc/nginx/ssl/app2.crt;
    ssl_certificate_key /etc/nginx/ssl/app2.key;

    # Configuración de SSL
    ssl_protocols TLSv1.2 TLSv1.3;
    ssl_ciphers 'ECDHE-ECDSA-AES128-GCM-SHA256:ECDHE-RSA-AES128-GCM-SHA256:DHE-RSA-AES128-GCM-SHA256';
    ssl_prefer_server_ciphers on;

    # Seguridad adicional
    add_header Strict-Transport-Security "max-age=31536000; includeSubDomains; preload" always;

    # Proxy inverso: Redirige tráfico a la aplicación en el puerto 9090
    location / {
        proxy_pass http://localhost:9090/;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
    }

    # Logs de acceso y error
    error_log /var/log/nginx/app2-error.log;
    access_log /var/log/nginx/app2-access.log;
}

```



#### Quien usa mi puerto???
`sudo lsof -i :80`




### TOMCAT

## **🔹 Caso 1: Varias aplicaciones en Tomcat con distintos dominios**

```xml
<VirtualHost *:80>
    ServerName app1.com

    ProxyPreserveHost On
    ProxyPass / http://localhost:8080/app1/
    ProxyPassReverse / http://localhost:8080/app1/
</VirtualHost>

<VirtualHost *:80>
    ServerName app2.com

    ProxyPreserveHost On
    ProxyPass / http://localhost:8080/app2/
    ProxyPassReverse / http://localhost:8080/app2/
</VirtualHost>

```


## 🔹 Caso 2: Tomcat + Otros servidores en diferentes puertos**

```xml
<VirtualHost *:80>
    ServerName tomcat-app.com
    ProxyPass / http://localhost:8080/
    ProxyPassReverse / http://localhost:8080/
</VirtualHost>

<VirtualHost *:80>
    ServerName django-app.com
    ProxyPass / http://localhost:8000/
    ProxyPassReverse / http://localhost:8000/
</VirtualHost>

<VirtualHost *:80>
    ServerName node-app.com
    ProxyPass / http://localhost:3000/
    ProxyPassReverse / http://localhost:3000/
</VirtualHost>

```

## **🔹 Caso 3: Mismo dominio con subrutas**

Si prefieres que las apps sean accesibles como:

- `https://mi-sitio.com/app1`
- `https://mi-sitio.com/app2`


```xml
<VirtualHost *:80>
    ServerName mi-sitio.com

    ProxyPreserveHost On
    ProxyPass /app1/ http://localhost:8080/app1/
    ProxyPassReverse /app1/ http://localhost:8080/app1/

    ProxyPass /app2/ http://localhost:8080/app2/
    ProxyPassReverse /app2/ http://localhost:8080/app2/
</VirtualHost>

```


### Apache vs Nginx

La diferencia entre **Apache** y **Nginx** en términos de servidores web y su uso en proxy inverso, especialmente cuando trabajas con aplicaciones modernas como **React** o **Angular**, se refiere principalmente a su **arquitectura**, **rendimiento**, y cómo manejan las solicitudes. Vamos a desglosar esto en detalle para ayudarte a entender las principales diferencias y cómo se usan en el contexto actual.

### 1. **Diferencia entre Apache y Nginx:**

#### **Apache HTTP Server:**

- **Arquitectura basada en hilos (Thread-based)**: Apache es tradicionalmente un servidor **basado en procesos o hilos**, lo que significa que maneja cada solicitud con un nuevo hilo o proceso. Esto puede llevar a un alto consumo de memoria y un rendimiento menos eficiente bajo carga alta.
    
- **Configuración flexible**: Apache es altamente configurable y permite manejar sitios estáticos y dinámicos de manera efectiva, sobre todo con **mod_php** o integraciones con otros lenguajes (como **mod_python**, **mod_perl**, etc.). Esto lo hace un servidor muy versátil para aplicaciones tradicionales.
    
- **Manejo de PHP y aplicaciones dinámicas**: Apache se ha usado históricamente en muchas aplicaciones con **PHP**. A menudo se usa con **mod_php**, lo que le permite manejar solicitudes PHP de manera eficiente.
    
- **Manejo de tráfico**: Apache puede ser menos eficiente cuando se trata de manejar un gran número de solicitudes simultáneas, ya que cada nueva solicitud puede requerir un hilo o un proceso adicional.
    

#### **Nginx:**

- **Arquitectura basada en eventos (Event-based)**: Nginx se diseñó para ser **asíncrono** y basado en **eventos**. Usa un solo hilo para manejar múltiples conexiones, lo que le permite manejar un alto volumen de tráfico sin consumir mucha memoria. Esto lo hace mucho más eficiente que Apache en situaciones con alta carga o múltiples solicitudes simultáneas.
    
- **Optimizado para servir contenido estático**: Nginx es muy rápido sirviendo archivos estáticos (como imágenes, JavaScript, CSS, etc.) y, por tanto, es muy popular como **servidor de contenido estático** junto con un **proxy inverso**.
    
- **Proxy inverso y balanceador de carga**: Nginx es conocido por su capacidad de manejar **proxy inverso** y **balanceo de carga** de manera eficiente. Es común que Nginx maneje solicitudes y las redirija a servidores backend (como aplicaciones en Node.js, Ruby, o incluso Tomcat) de manera eficiente.
    
- **Manejo de aplicaciones modernas**: Nginx se utiliza ampliamente como proxy inverso para aplicaciones modernas que están construidas con tecnologías como **React**, **Angular**, **Vue.js**, **Node.js**, etc. Cuando tienes una aplicación **SPA (Single Page Application)** como React o Angular, el contenido estático se sirve a través de Nginx, y las solicitudes de API se redirigen a un servidor backend a través de un proxy inverso.
    

---

### 2. **Uso en Proxy Inverso:**

El **proxy inverso** se refiere a la práctica de un servidor (como **Nginx**) que maneja las solicitudes de los clientes y las redirige a otros servidores backend. Es muy útil cuando tienes **múltiples aplicaciones** corriendo en diferentes puertos o en diferentes servidores y quieres hacerlas accesibles a través de una URL única.

#### **Apache como Proxy Inverso:**

- Apache también puede ser configurado para trabajar como un proxy inverso usando el módulo **mod_proxy**.
- Aunque Apache puede hacer esto, a menudo no es tan eficiente como Nginx en términos de rendimiento, especialmente bajo cargas pesadas.

#### **Nginx como Proxy Inverso:**

- Nginx es muy eficiente como proxy inverso, ya que maneja las solicitudes entrantes y las pasa a un servidor backend (como una aplicación Node.js, un servidor de aplicaciones en Java, o un servidor de bases de datos).
- Nginx es comúnmente utilizado en configuraciones modernas donde el tráfico es direccionado a varios servicios backend, y es especialmente adecuado para aplicaciones que tienen una **arquitectura de microservicios**.

En el contexto de aplicaciones como **React** o **Angular**, Nginx puede servir la **parte estática** (los archivos **JavaScript**, **HTML**, **CSS**) y actuar como proxy para todas las **solicitudes de API** (que generalmente se manejan en un backend).

### 3. **¿Cómo corre Nginx y de qué está hecho?**

- **Nginx está escrito en C**, lo que le da una gran eficiencia en términos de rendimiento. Esto lo hace mucho más rápido que Apache en la mayoría de los casos.
- **Modo asíncrono y basado en eventos**: Nginx usa un modelo **basado en eventos** y **asincrónico**. Esto significa que puede manejar miles de conexiones concurrentes con un solo hilo de proceso, lo que lo hace ideal para manejar un alto volumen de tráfico.

Nginx funciona en una arquitectura de **trabajo no bloqueante**, lo que permite que maneje múltiples solicitudes de forma simultánea sin bloquear el hilo principal. Cuando Nginx recibe una solicitud, no espera a que esta se complete antes de procesar la siguiente. Esto es fundamental cuando se trabaja con muchas solicitudes simultáneas o cuando se usan tecnologías modernas basadas en **AJAX** o **WebSockets**.

### 4. **¿Qué hace Nginx?**

En resumen, **Nginx** se usa principalmente para:

- **Servir contenido estático** de manera eficiente (como imágenes, archivos CSS, JS, etc.).
- **Balanceo de carga**: Distribuir el tráfico entre varios servidores backend.
- **Proxy inverso**: Redirigir solicitudes de clientes hacia un servidor backend (como una aplicación Node.js, Java, PHP, etc.).
- **Enrutamiento de tráfico**: Redirigir el tráfico según el dominio o la URL.
- **Manejo de tráfico HTTPS**: Gestionar conexiones seguras a través de SSL/TLS.
- **Optimización de rendimiento**: Acelerar el tiempo de carga de las páginas mediante la manipulación de contenido en caché.

### 5. **Uso con Aplicaciones Modernas (React, Angular, etc.)**

En aplicaciones modernas que se desarrollan con **React**, **Angular**, o **Vue.js**, la arquitectura generalmente se basa en una **SPA (Single Page Application)**. Esto significa que el frontend (la aplicación de cliente) se sirve como **contenido estático** y se comunica con **APIs backend** a través de solicitudes HTTP.

- **Frontend** (React/Angular) se puede construir en un directorio estático (por ejemplo, usando `npm run build` para crear la versión de producción).
- **Backend** (API en Node.js, Django, Flask, etc.) proporciona los servicios de datos para la aplicación frontend.

En este escenario:

1. **Nginx** maneja las solicitudes entrantes de los usuarios, sirve los archivos estáticos (HTML, CSS, JS) del frontend.
2. Para las **solicitudes de API**, Nginx actúa como un proxy inverso y redirige las solicitudes a un servidor backend (Node.js, por ejemplo).
3. La configuración de Nginx es eficiente para manejar ambos casos: servir contenido estático y redirigir el tráfico a un servidor backend.

![[Pasted image 20250309183821.png]]


### Docker compose ejemplificado

```yaml
version: '3.8'

services:
  # 1. Angular App
  angular-app:
    image: nginx:alpine
    container_name: angular-app
    volumes:
      - ./angular/dist:/usr/share/nginx/html
    networks:
      - app-network
    ports:
      - "4200:80"  # Puerto donde Angular será accesible en localhost:4200
    restart: always

  # 2. React App
  react-app:
    image: nginx:alpine
    container_name: react-app
    volumes:
      - ./react/build:/usr/share/nginx/html
    networks:
      - app-network
    ports:
      - "3000:80"  # Puerto donde React será accesible en localhost:3000
    restart: always

  # 3. Spring Boot App (Java)
  spring-boot-app:
    image: openjdk:11-jdk
    container_name: spring-boot-app
    working_dir: /app
    volumes:
      - ./spring/target:/app
    networks:
      - app-network
    ports:
      - "8080:8080"  # Puerto donde Spring Boot se expone (por ejemplo: localhost:8080)
    command: java -jar /app/app.jar  # Suponiendo que ya tengas un archivo .jar
    restart: always

  # 4. Base de datos (MySQL)
  mysql-db:
    image: mysql:8.0
    container_name: mysql-db
    environment:
      MYSQL_ROOT_PASSWORD: root_password
      MYSQL_DATABASE: app_db
      MYSQL_USER: app_user
      MYSQL_PASSWORD: user_password
    networks:
      - app-network
    ports:
      - "3306:3306"
    restart: always

  # 5. Nginx como Proxy Inverso
  nginx-proxy:
    image: nginx:alpine
    container_name: nginx-proxy
    volumes:
      - ./nginx/default.conf:/etc/nginx/conf.d/default.conf  # Configuración de Nginx
    networks:
      - app-network
    ports:
      - "80:80"
      - "443:443"  # Si usas HTTPS
    depends_on:
      - angular-app
      - react-app
      - spring-boot-app
    restart: always

networks:
  app-network:
    driver: bridge
```



¡Ah, ahora entiendo! Estás hablando de **Nginx Proxy Manager**, una herramienta que hace todo el proceso de configuración de Nginx mucho más fácil mediante una interfaz gráfica, y efectivamente, genera automáticamente configuraciones de Nginx para ti.

### ¿Qué es Nginx Proxy Manager?

**Nginx Proxy Manager** es una herramienta basada en una interfaz gráfica que facilita la gestión de servidores Nginx, especialmente cuando se trata de configurar proxies inversos y certificados SSL de manera rápida y sencilla. Te permite configurar múltiples dominios, subdominios y certificados SSL, sin necesidad de escribir manualmente la configuración de Nginx.

### ¿Cómo lo hace automáticamente?

- **Generación de Configuraciones Nginx:** Cuando configuras un dominio o subdominio en Nginx Proxy Manager, él crea automáticamente las configuraciones adecuadas en Nginx, incluyendo las reglas de proxy inverso, y se asegura de que el tráfico se redirija correctamente a tus aplicaciones.
    
- **SSL Automático:** Puedes configurar Nginx Proxy Manager para que automáticamente obtenga un **certificado SSL gratuito** utilizando **Let's Encrypt**. En ese caso, se encarga de renovar el certificado de manera automática, sin necesidad de intervención manual.
    

### Pasos para configurar un proxy inverso en Nginx Proxy Manager:

1. **Instalar Nginx Proxy Manager:** Si aún no lo has hecho, puedes instalarlo fácilmente utilizando Docker. Aquí tienes un ejemplo de cómo hacerlo:
    
    bash
    
    CopiarEditar
    
    `docker-compose.yml version: '3' services:   app:     image: jc21/nginx-proxy-manager:latest     container_name: nginx-proxy-manager     restart: always     ports:       - "80:80"       - "443:443"       - "81:81"  # Esta es la interfaz web     volumes:       - ./data:/data       - ./letsencrypt:/etc/letsencrypt     environment:       - DB_SQLITE_FILE=/data/database.sqlite`
    
2. **Acceder a la Interfaz de Usuario:** Una vez que Nginx Proxy Manager está instalado y corriendo, puedes acceder a su interfaz web a través de `http://<tu-ip>:81` y configurarlo mediante la interfaz gráfica.
    
3. **Agregar un Proxy Inverso:** En la interfaz de Nginx Proxy Manager:
    
    - Haz clic en "Proxy Hosts".
    - Añade un nuevo **Proxy Host**. Para esto, necesitas proporcionar el nombre de dominio, la IP o el puerto de la aplicación a la que deseas redirigir el tráfico (por ejemplo, una aplicación en `localhost:9090`), y la configuración adicional para SSL.
4. **Configurar SSL:**
    
    - Al configurar el dominio, Nginx Proxy Manager tiene una opción para habilitar **SSL automático** usando Let's Encrypt. Solo debes poner tu dominio y marcar la casilla que dice algo como **"Request a new SSL certificate"**.
    - Esto generará y configurará el certificado SSL para tu dominio automáticamente.
5. **Configuración de Redirección HTTP a HTTPS:** Nginx Proxy Manager puede hacer esto por ti automáticamente, redirigiendo todo el tráfico HTTP hacia HTTPS para asegurar tu sitio.
    
6. **Guardar y Aplicar Configuraciones:** Después de agregar los detalles, haz clic en "Save" y Nginx Proxy Manager se encargará de crear las reglas de proxy inverso en el archivo de configuración de Nginx, además de gestionar las configuraciones de SSL.
    

### ¿Por qué usar Nginx Proxy Manager?

- **Fácil de usar:** Si no quieres estar editando archivos de configuración manualmente, la interfaz gráfica de Nginx Proxy Manager lo hace mucho más fácil.
- **SSL automático:** Solicita y renueva certificados SSL gratuitos con Let's Encrypt, sin necesidad de usar Certbot manualmente.
- **Multidominio y subdominios:** Puedes gestionar múltiples dominios y subdominios sin complicaciones.
- **Soporte para redirecciones, autenticación básica y otras opciones avanzadas:** Todo a través de una interfaz gráfica.


¡Claro! Te aclaro cómo funciona el **challenge** de Let's Encrypt y cómo se aplica en **Nginx Proxy Manager**.

### ¿Qué es un Challenge de Let's Encrypt?

Cuando solicitas un certificado SSL a través de **Let's Encrypt**, la autoridad certificadora (CA) necesita asegurarse de que tienes control sobre el dominio para el cual estás solicitando el certificado. **Eso es lo que se conoce como un "challenge"**.

Existen dos tipos principales de challenge que Let's Encrypt utiliza para validar que tienes control sobre el dominio:

1. **HTTP-01 Challenge (Desafío HTTP):**
    
    - Este desafío verifica que el servidor web al que se está solicitando el certificado puede servir un archivo específico en una URL determinada. Let's Encrypt revisa si puedes responder a una solicitud HTTP que apunte a un archivo temporal en tu servidor web.
    - Por ejemplo, Let's Encrypt te pide que pongas un archivo de verificación en tu servidor en una ruta como `http://tu-dominio.com/.well-known/acme-challenge/<token>`.
    - Si el servidor responde correctamente, significa que tienes control sobre el dominio y Let's Encrypt te emite el certificado.
2. **DNS-01 Challenge (Desafío DNS):**
    
    - Este desafío se utiliza generalmente cuando no se puede usar el HTTP-01 challenge (por ejemplo, en entornos donde no se puede hacer acceso HTTP). En este caso, debes agregar un registro TXT específico a la zona DNS de tu dominio.
    - Let's Encrypt valida la existencia de ese registro TXT y si lo encuentra, emite el certificado.


