(UF1 Servidor Web y Transferencia de Archivos)
## 1. Arquitecturas web. Modelos.

- La **arquitectura web** (World Wide Web, www) de Internet da un modelo de conexión poderoso y flexible por el que cualquier equipo puede adaptarse a sus requerimientos. 
- Los **contenidos se localizan** gracias a los **web browsers** o buscadores que encuentran la información requerida con las peticiones enviadas a diversos servidores para que se les respondan las páginas que más se adaptan a los parámetros de búsqueda.
- El **contenido en la web se visualiza** siguiendo unos **estándares** que permiten a que los navegadores los interpreten correctamente (HTML, JavaScript, CSS,...)
- **Las operaciones de transferencia** también están estandarizadas. Cada servicio sigue una serie de **protocolos** que permiten abstraerse de la tecnología y del sistema operativo. De los más conocidos es el protocolo HTTP (HyperText Transfer Protocol, protocolo de transferencia de hipertexto) por el que un cliente puede visualizar páginas web.

**Origen HTTP/HTML** 
- Finales de los 80. Científicos del CERN. Trabajan con PC no compatibles, no podían compartir su trabajo. 
- Tim Berners-Lee. Propuesta para desarrollar sistema de hipertexto sobre Internet. 
- Se desarrolla sobre protocolos TCP/IP (desde los 50, pruebas Arpanet). 
	- Formato de texto para representar documentos de hipertexto (HyperText Markup Language HTML)
	- Protocolo para intercambio de documentos (HyperText Transfer Protocol HTTP)

**Características de la arquitectura web**
- **Escalabilidad**: Fácilmente es posible conectarse a distintos equipos de la red (servidores, enrutadores, switches) sin que la red se vea influida ni obligada a cambiar de forma constante. 
- **Separación de responsabilidades**: Se separan elementos: clientes y servidores; peticiones y respuestas. Así se permite el trabajo de forma más organizada y estructura, adaptándose a las necesidades. 
- **Amplia conectividad**: Servidores y administradores proveen conexión óptima y segura entre cualquier cantidad de nodos.
- **Recursos compartidos**: Se aprovechan los recursos que se comparten entre clientes

**Modelo de la arquitectura web**

La arquitectura de un sitio web la forman la:
- Gestión de los sistemas de organización y estructuración de los contenidos
- El de recuperación de información
- La visualización de los contenidos por parte del cliente.

**Según cómo se implementan** se puede dividir en varias capas:
- **Capa de presentación**: Presenta la información al usuario y acepta inputs y outputs enviándolas a la capa de negocio.
- **Capa de negocio:** Capa que gestiona la lógica de la aplicación, recibe peticiones de los usuarios y desde donde se envían las respuestas. Se verifica en ella que las reglas se cumplen.
- **Capa de acceso a datos:**  Capa más interna. Formada por los gestores de bases de datos. Se estructura de forma que se almacenen los datos de forma organizada para que la información pueda ser fácil y rápidamente consultadas.

**Según su orden de aparición**
- **Modelo 1**: Originalmente las aplicaciones se diseñaban en HTML. El usuario recibía la respuesta del servidor a su petición. Presentación, negocio y acceso a datos se encuentran en un mismo archivos. 
- **Modelo 1.5:** Uso de Java como lenguaje orientado a objetos con comunicación cliente-servidor. Se usan "lenguajes" como JSP o servlets con servidores web como Tomcat. Surge el concepto de _página web dinámica_ a partir de los parámetros de petición enviados por le navegador. Capas de presentación, negocio y acceso a datos están en las páginas JSP, facilita la programación de las capas creando separación de responsabilidades.
- **Modelo 2:** Uso del patrón MVC en las aplicaciones anteriores. Hay un controlador de la navegación de la aplicación, quedan la capa de negocio en el interior de los archivos creados por Java, pudiendo encapsular varios objetos.
- **Modelo 2X:** Necesidad de realizar aplicaciones para poder atender a varios clientes y en varios canales como tablet, móvil, ordenador. Para los distintos positivos se usa XSL y se transforman en XML. 

**Según la organización y comunicación entre sus nodos**
- **Cliente-servidor**: Está basado en el flujo de datos entre ordenadores (clientes) que solicitan un servicio a un ordenador u ordenadores centrales (servidor). Hay diferentes configuraciones y estructuras del lado del servidor para proveer de servicios a los clientes, produciéndose siempre flujo de información cliente-servidor. 
	- Ventaja: Dos roles perfectamente definidos
	- Inconveniente: Cuellos de botella ante alta demanda de información

- **Peer to peer**: Modelo de igual a igual (P2P). Los nodos de la red hacen la función de servidor y a su vez de cliente frente a todos los equipos de la misma red. Forman una especie de colmena en la que todos se comunican con todos, pasando de tener un único canal de transmisión de datos a disponer de tantos como la red permita. 
	- Ventaja: Eficiencia
	- Inconveniente: Es más complicada de comprender y de diseñar

**Funcionamiento de los servicios web**
Se necesitan tres elementos principales:
- **Proveedor del servicio web**: Realiza el diseño, desarrollo y puesta en marcha para su uso.
- **Consumidor del servicio:** Elemento que accede a dicho recurso.
- **Agente del servicio:** Hace la función de enlace para que el proveedor y el consumidor de encuentren. Enlaza los criterios de búsqueda con los servicios del proveedor. 

## 2. Servidores web y de aplicaciones. Instalación y configuración básica.

### 2.1. Servidor web. Apache

Un **servidor web** es aquel que se ejecuta continuamente en el servidor a la espera de peticiones por parte de un cliente de la red y responde a este con contenido de una página web. Para su visualización se necesita la aplicación de un navegador web. 

La instalación de un servicio web puede hacerse:
- **Instalación de un sistema operativo servidor** (propietario o libre) **y posteriormente de un servicio web mediante un gestor de dominio**. (Ej.: Instalación de Apache)
- **Instalar una aplicación que hace que la propia máquina sea un servidor web**. (Ej.: Uso de XAMPP o Docker)

**Apache** es uno de los servidores más utilizados. Es de código abierto y gratuito y está disponible para Windows y GNU/Linux.

**Características de Apache**
- Se caracteriza por estar **estructurado en módulos**
- Cada módulo tiene una función referida a un aspecto de la aplicación web.
- Los módulos se configuran en el **archivo .httpd**, en él están los módulos instalados cuya funcionalidad debe ser activada al arrancar el servidor.

Existe:
- **Módulo base**: Se encarga de funcionalidades básicas
- **Multiprocesos:** Se encargan de las peticiones, aceptándolas y ejecutándolas
- **Adicionales:** Añaden funcionalidad al servidor

La **licencia Apache** permite la distribución de derivados de código abierto y cerrado a partir de su código fuente original. 

#### 2.1.1. Instalación de servidor web Apache en Linux Ubuntu

1.- Actualizar el índice local de paquetes:
```shell
sudo apt get update
sudo apt get upgrade
```
2.- Instalar el paquete apache2:
```shell
sudo apt install apache2
```
3.- Recordar los comandos del proceso
```shell
# Verificar estado
sudo systemctl status apache2
# Parar servicio
sudo systemctl stop apache2
# Iniciar servicio
sudo systemctl start apache2
# Reiniciar servicio
sudo systemctl restart apache2
# Recargar Apache debido a cambios en la configuracion sin tener que reiniciar el servicio y perder las conexiones activas
sudo systemctl reload apache2
# Configurar Apache para iniciarse como SERVICIO
sudo systemctl enable apache2
# Desactivar Apache para que no se inicie como servicio
sudo systemctl disable apache2
```
4.- Acceder a la página por defecto de Apache
```shell
# Si no se sabe, utilizar el comando hostname
hostname -I
# Entrar por el navegador o por
curl http://ip_del_servidor
```

5.- Comprobaremos que se ha creado la carpeta **/var/www/html** y que su propietario es el usuario con el que se inició la sesión (¿root?). Dicha carpeta será el directorio raíz del contenido del servidor establecido por defecto en su configuración en `/etc/apache2/sites-available`

Para desplegar una página de ejemplo solo hay que mover el contenido a `/var/www/http`

#### 2.1.2. Instalación de servidor web Apache en Xampp

**XAMPP** puede ser descargado de https://www.apachefriends.org/es
Versión actual: XAMPP for Windows (8.2.12 - PHP 8.2.12)

Comprende una solución completa y gratuita para crear un servidor local en el ordenador.
Permite desarrollar y probar aplicaciones web en un entorno controlado antes de implementarlas en un servidor en línea.
Está diseñado para ser fácil de instalar y de usar.
Se combina servidor web Apache, base de datos, lenguajes de programación y otras herramienta esenciales.
Sus características son:
- **Paquete de Software Todo-en-Uno**: XAMPP es un conjunto de herramientas de software que incluye Apache (servidor web), MySQL o MariaDB (BBDD), PHP y Perl.
- **Multiplataforma**. Diseñado principalmente para WIndows, macOS y Linux.
- **Fácil de instalar y de usar**
- **Entorno de pruebas local**: Permite probar y depurar aplicaciones web sin necesidad de un servidor en línea, reduciendo tiempos de carga y facilitando la iteración rápida.
- **Versatilidad para desarrollo**.Soporta PHP y Perl y puede configurarse para soportar otros lenguajes y herramientas. 


Si se consulta el fichero `phpinfo.php`, se puede ver toda la información del servidor con los módulos de Apache cargados y mucha más información.

```php
<?php phpinfo(); ?>
```

Para desplegar una página de ejemplo solo hay que mover el contenido a `htdocs`
Y, según el directorio, ese será su contexto:
http://localhost/backs/index.html
http://localhost/backs/street/index.html

### 2.2. Servidor de aplicaciones

Un **servidor de aplicaciones** es una herramienta que proporciona aplicaciones o programas a los clientes de la red mediante una conexión HTTP.
A nivel de software es un programa informático dentro de un sistema operativo y queda identificado por su número de proceso (PID).
También permite centralizar en un equipo las aplicaciones necesarias para toda la red para gestionar mejor el acceso a datos.

Integridad de datos + Centralización de aplicaciones --> Más eficiente

Se producen actualizaciones más cómodas al centrarse todas las aplicaciones en el equipo. Ejs.: Aplicaciones web, de comercio electrónico, herramientas para gestionar el contenido web.

#### 2.2.1. Instalación de servidor web Tomcat en Linux Ubuntu

**Forma más sencilla:**

```shell
# Instalar Java
sudo apt install openjdk-11-jdk
# Instalar Tomcat
sudo apt install tomcat10 tomcat10-admin
# Comprobar estado
sudo systemctl status tomcat10
# Subir aplicación
sudo mkdir /var/lib/tomcat10/webapps/myapp
sudo vim /var/lib/tomcat10/webapps/myapp/index.jsp
# Reiniciar Tomcat
sudo systemctl restart tomcat10
```

---
**Forma del libro:**
**Tomcat** es un servidor que incluye tanto el servicio web (Servidor Apache) como el servidor de aplicaciones.
Más formalmente se le denomina "_contenedor de servlets_". Gestiona las peticiones HTTP y peticiones JSP o servlets. 

**1.- Instalación JDK y variables de entorno**
Es necesario tener instalado el JDK de Java y tener variables de entorno para saber dónde está instalado:
```bash
# Declarada en la sesion del terminal
JAVA_HOME=/usr/lib/jvm/java-6-openjdk/jre/
PATH=$PATH:$JAVA_HOME/bin
# Declarada en la sesion del terminal, pero ahora disponible tambien para subprocesos
export PATH JAVA_HOME
```

- Si quieres que las variables de entorno estén disponibles **globalmente** para todos los usuarios, agrega las líneas de exportación en `/etc/profile`.
- Si solo te interesa para **tu usuario** específico, agrégalas en `~/.bashrc` o `~/.bash_profile`.

```bash
# Despues de haberlas añadido a /etc/profile hacer
source /etc/profile
```

**2.- Instalación de Tomcat**
Se utiliza el archivo guardado.
```bash
tar xvzf apache-tomcat-X.X.XX.tar.gz
```

**3.- Gestión del servicio**
La gestión se realiza mediante un script llamado **Catalina**. Pueden usarse los comandos de la siguiente forma:

```shell
# Arrancar Tomcat
./bin/catalina.sh start
# Detener Tomcat
./bin/catalina.sh stop
```

**4.- Ver la página de inicio de Tomcat**
Suele correr en el puerto 8080. `127.0.0.1:8080`

### 2.3. Estructura y recursos que componen una aplicación web. El descriptor de despliegue

Un **servlet** es un archivo escrito en Java encargado de realizar un servicio dentro de un servidor web.
Más claramente: Un **Servlet** es un componente de servidor escrito en Java que **procesa solicitudes HTTP** y **genera respuestas dinámicas** para el cliente.

Se debe:
- Tener un servidor de aplicaciones como **Apache Tomcat** para ejecutar el servlet.
- Debe estar empaquetado y desplegado dentro de una **aplicación web** (en un archivo WAR o directamente en un directorio dentro de Tomcat).

La **estructura de directorios de una aplicación** debe cumplir:
- El directorio raíz debe tener el nombre de la aplicación.
- Contener los directorios **META-INF** y **WEB-INF** de uso exclusivo para el desarrollador.

```
mi-aplicacion-web/
├── pom.xml                        (archivo de configuración de Maven)
└── src/
    └── main/
        ├── java/                    (código fuente Java)
        │   └── com/
        │       └── ejemplo/
        │           ├── controller/   (controladores, por ejemplo, Servlets)
        │           ├── service/      (lógica de negocio)
        │           ├── dao/          (acceso a datos)
        │           └── model/        (modelos de la base de datos)
        ├── resources/               (archivos de configuración y recursos)
        │   ├── application.properties   (configuración aplicación, conex BBDD)
        │   ├── logback.xml            (configuración de logs)
        │   ├── persistence.xml        (archivo de configuración de JPA/Hibernate)
        │   ├── messages.properties    (resource bundle para internacionalización)
        │   └── static/                (archivos estáticos como imágenes, CSS, JS)
        ├── webapp/                   (páginas web y recursos web)
        │   ├── index.jsp             (página principal, si usas JSP)
        │   ├── jsp/                  (otras páginas JSP)
        │   ├── WEB-INF/
        │   │   ├── web.xml            (descriptor de despliegue)
        │   │   ├── beans.xml          (Para Inyeccion de dependencias CDI)
        │   │   ├── classes/           (archivos `.class` compilados)
        │   │   ├── lib/               (librerías `.jar` necesarias)
        │   │   └── tlds/              (si usa JSP Tag Libraries)
        │   └── static/                (archivos estáticos accesibles desde la web)
        │       ├── css/               (hojas de estilo)
        │       ├── js/                (JavaScript)
        │       └── images/            (imágenes estáticas)
        └── test/                      (tests unitarios, pruebas de integración)
            └── java/
                └── com/
                    └── ejemplo/
                        ├── controller/   (tests para los controladores)
                        ├── service/ (tests de la lógica de negocio) 
                        └── dao/ (tests de acceso a datos)
```


#### 2.3.1. Directorio META-INF

Contiene metadatos que dan información importante sobre aplicación, configuración y otras propiedades.
Por ejemplo:

- Archivo `MANIFEST.MF`: Tiene información sobre el contenido del **archivo JAR** como versiones, dependencias y clases principales de arranque para la ejecución. Es obligatorio en JAR y opcional en WAR.
```
Manifest-Version: 1.0
Created-By: 1.8.0_251 (Oracle Corporation)
Main-Class: com.miempresa.MiClasePrincipal
```

- Algunos frameworks pueden tener aquí **archivos de configuración** como: 
	- `applicationContext.xml` de Spring
	- `persistence.xml` de JPA con las unidades de persistencia y su configuración


#### 2.3.2. Directorio WEB-INF

Es un directorio obligatorio en una aplicación web Java (WAR). Tiene:
- archivos de configuración esenciales para ejecutar la aplicación web
- archivos **no accesibles directamente desde el navegador**.
Por ejemplo:

- `web.xml`: Conocido como **descriptor de despliegue** es un archivo de configuración utilizado en las aplicaciones web Java (específicamente en aplicaciones que se empaquetan en **archivos WAR**) para describir cómo deben ser configuradas y gestionadas ciertas funcionalidades del servidor de aplicaciones en el que se va a desplegar la aplicación. **Resulta fundamental para definir filtros, servlets, listeners y otros componentes del ciclo de vida de la aplicación** Es obligatorio aunque puede ser sustituido por anotaciones en el código también. 
- `classes/`: Contiene archivos `.class` compilados de la aplicación Java.
- `lib/`: Contiene librerías ( .jar) que la aplicación necesita para funcionar
- Archivos de configuración adicionales: Propiedades, configuracione,s archivos de seguridad.

**Ejemplo de descriptor de despliegue (web.xml)**

```xml
<?xml version="1.0" encoding="UTF-8"?>
<web-app xmlns="http://java.sun.com/xml/ns/javaee"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://java.sun.com/xml/ns/javaee
             http://java.sun.com/xml/ns/javaee/web-app_3_0.xsd"
         version="3.0">

    <!-- Configuración de Servlets -->
    <servlet>
        <servlet-name>MiServlet</servlet-name>
        <servlet-class>com.miempresa.MiServlet</servlet-class>
        <load-on-startup>1</load-on-startup>
    </servlet>
    
    <servlet-mapping>
        <servlet-name>MiServlet</servlet-name>
        <url-pattern>/miServlet</url-pattern>
    </servlet-mapping>

    <!-- Otros componentes de la web (listeners, filtros, etc.) -->
</web-app>
```

**Ejemplo de Servlet**


```java
import java.io.*;
import javax.servlet.*;
import javax.servlet.http.*;

public class MiServlet extends HttpServlet {

    // Método que maneja la solicitud GET
    @Override
    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        // Llamamos al método común para procesar la solicitud GET
        handleRequest(request, response);
    }

    // Método que maneja la solicitud POST
    @Override
    protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        // Llamamos al método común para procesar la solicitud POST
        handleRequest(request, response);
    }

    // Lógica común para manejar tanto GET como POST
    private void handleRequest(HttpServletRequest request, HttpServletResponse response) throws IOException {
        // Establecer el tipo de contenido de la respuesta como HTML
        response.setContentType("text/html");

        // Obtener el PrintWriter para escribir la respuesta
        PrintWriter out = response.getWriter();

        // Si la solicitud es GET, mostramos el formulario
        if (request.getMethod().equalsIgnoreCase("GET")) {
            showForm(out);
        } 

        // Si la solicitud es POST, procesamos los datos enviados
        else if (request.getMethod().equalsIgnoreCase("POST")) {
            processFormData(request, out);
        }
    }

    // Muestra el formulario cuando se hace una solicitud GET
    private void showForm(PrintWriter out) {
        out.println("<html>");
        out.println("<head><title>Formulario GET y POST</title></head>");
        out.println("<body>");
        out.println("<h1>Formulario de Contacto</h1>");
        out.println("<form method='POST' action='miServlet'>");
        out.println("Nombre: <input type='text' name='nombre'><br>");
        out.println("Correo: <input type='text' name='correo'><br>");
        out.println("<input type='submit' value='Enviar'>");
        out.println("</form>");
        out.println("</body>");
        out.println("</html>");
    }

    // Procesa los datos del formulario enviados mediante POST
    private void processFormData(HttpServletRequest request, PrintWriter out) {
        String nombre = request.getParameter("nombre");
        String correo = request.getParameter("correo");

        out.println("<html>");
        out.println("<head><title>Formulario Enviado</title></head>");
        out.println("<body>");
        out.println("<h1>Formulario Enviado</h1>");

        if (nombre != null && correo != null) {
            out.println("<h3>Datos recibidos:</h3>");
            out.println("Nombre: " + nombre + "<br>");
            out.println("Correo: " + correo + "<br>");
        } else {
            out.println("<p>Hubo un error en el envío de los datos.</p>");
        }

        out.println("</body>");
        out.println("</html>");
    }
}
```


#### 2.3.3. Archivos empaquetados

- **JAR** (Java ARChive):  Agrupa archivos y recursos de una aplicación de Java. Común para aplicaciones de Java SE. Es ejecutable mediante `java -jar archivo.jar`. El `META-INF/MANIFEST.MF` contiene datos como la clase principal.  Es usado en aplicaciones de consola, bibliotecas compartidas, distribución de utilizadades,...
- **WAR** (Web ARchive): Usado para aplicaciones de Java EE. Contiene todos los recursos para desplegar una aplicación web en Tomcat, Wildfly, Glassfish. 
- **EAR** (Enterprise ARchive):  Formato para aplicaciones Java EE completas que puede incluir tanto componentes web (WAR) como componentes de negocio (JAR). Puede tener módulos como aplicaciones web, EJBs y otros servicios. Estos tienen un archivo de despliegue `application.xml` que describe los módulos y sus configuraciones. 

#### 2.3.4. Relación entre Servlets y JSP

1. El cliente (navegador) hace una solicitud HTTP.
2. El **Servlet** recibe la solicitud, realiza alguna lógica de negocio o de procesamiento, y luego pasa el control a una **JSP** para mostrar el resultado al usuario.
3. La **JSP** genera contenido HTML dinámico (que puede incluir datos procesados por el Servlet) y lo envía de vuelta al cliente.

- **Servlets** pueden establecer atributos en la solicitud (`request.setAttribute("clave", valor)`) que luego son utilizados por las **JSPs** para generar contenido dinámico.
- Una vez que el Servlet ha procesado la solicitud, puede redirigir o incluir una JSP usando los métodos `RequestDispatcher.forward()` o `RequestDispatcher.include()`.

```java
@WebServlet("/procesarDatos")
public class MiServlet extends HttpServlet {
    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        String mensaje = "¡Hola desde el Servlet!";
        
        // Pasar el dato a la JSP
        request.setAttribute("mensaje", mensaje);
        
        // Redirigir a la JSP
        RequestDispatcher dispatcher = request.getRequestDispatcher("/mostrarDatos.jsp");
        dispatcher.forward(request, response);
    }
}
```

```jsp
<%-- mostrarDatos.jsp --%>
<html>
<head><title>Mostrar Datos</title></head>
<body>
    <h1>${mensaje}</h1>  <!-- Usando EL (Expression Language) para mostrar el mensaje -->
</body>
</html>

```


#### 2.3.5. Archivo beans.xml

El archivo **`beans.xml`** debe colocarse dentro del directorio **`META-INF/`** en aplicaciones de tipo **JAR** o en **`WEB-INF/`** para aplicaciones **WAR**.
Se utiliza en el contexto de CDI (Context and Dependency Injection) de JavaEE/Jakarta EE permitiendo:
- Habilitar CDI. Es necesario este archivo para que los contenedores de CDI (servidor de aplicaciones) reconozcan que la aplicación usa CDI.
- Configuración de beans. Actualmente es mínimo pero puede usarse para definir el modo de activación de CDI u otras características.

**Ejemplo beans.xml**
```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://xmlns.jcp.org/xml/ns/javaee"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee
                           http://xmlns.jcp.org/xml/ns/javaee/beans_1_1.xsd"
       version="1.1">
</beans>
```

- **`<beans>`**: Es el elemento raíz del archivo, que define el espacio de nombres y la versión de CDI.
- **`<alternatives>`**: Este elemento se utiliza para declarar clases que deben ser tratadas como alternativas a otras implementaciones de beans. Esto permite la personalización del comportamiento de la aplicación. Por ejemplo, se puede especificar que una clase debe ser utilizada en lugar de otra a través de un mecanismo de inyección de dependencias.
- **`<scan>`**: Controla el comportamiento del descubrimiento automático de beans por parte del contenedor CDI. Si `enabled="false"`, el contenedor no buscará beans automáticamente, lo que significa que los beans deben ser explícitamente definidos en el archivo **`beans.xml`** o en la configuración de clases de la aplicación.
```xml
`<scan enabled="false"/>`
```

- `<decorators>` y `<interceptors>`: Estos elementos permiten especificar qué clases actúan como decoradores o interceptores dentro de CDI. Los decoradores permiten modificar el comportamiento de un bean, y los interceptores permiten modificar la ejecución de métodos de un bean.
