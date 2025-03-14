(UF2 Servidores de Aplicaciones Web)
## 0. Mecanismos de seguridad en la administración de servidores de aplicaciones

El **servidor de aplicaciones** da un conjunto de aplicaciones a los clientes conectados a él.

**Ventajas**:
- Centralización de aplicaciones
- Disminución en la complejidad de la implementación
**Inconvenientes:**
- Más expuestos a ataques externos. Como ataques a la computadora cliente, ataques al equipo servidor, ataques al flujo de información que se transmite. 

**Mínimos de seguridad que es recomendable garantizar**
- **Cliente**: Seguridad de los navegadores y software para Internet.
- **Servidor:** Acreditación del acceso, control de los usuarios. Los permisos deben corresponderse con los roles asignados por el administrador de red.
- **Tránsito de la información:** Asegurar que la información no será leída, modificada o destruida por personas ajenas al dominio. Asegurar la seguridad en el canal.

**Mecanismos para garantizar la seguridad**
- **Autenticación**: Permite identificar y verificar que el usuario que accede al sistema es una persona habilitada en el sistema. Se podría introducir un usuario y contraseña o incluso llegar a usar certificado digital.
- **Autorización**: Permite verificar que el usuario tiene acceso a las funcionalidades acordes a su rol.
- **Validación de entradas** introducidas por el usuario y de sentencias SQL a ejecutar sobre la base de datos. 

**Orientaciones para mejorar la seguridad de las aplicaciones web alojadas en el servidor**
- Deshabilitar servicios y cuentas que no se utilicen
- Actualizar el sistema operativo y las aplicaciones (tendrán mecanismos de defensa ante las amenazas recientes)
- Reforzar políticas de contraseñas seguras
- Utilizar cortafuegos actuales
- Monitorizar archivos de registro con periodicidad
- Llevar control del mecanismo de cifrado que se utiliza para la encriptación de los datos en la transmisión
- Cumplir normas de seguridad establecidas en las políticas de seguridad del sistema. 

## 1. Arquitectura y configuración básica del servidor de aplicaciones

Más claramente: Un **servlet** es un componente de servidor escrito en Java que **procesa solicitudes HTTP** y **genera respuestas dinámicas** para el cliente. Proporcionan propiamente las funcionalidades a la aplicación web. Las "aplicaciones servlet" se pueden desplegar en diferentes servidores web (contenedores de servlets) manteniendo su funcionalidad y sin sufrir ninguna modificación de código.

Sabemos que se llama **directorio raíz** a aquel del que cuelgan los demás directorios del árbol.
En este caso se tienen ficheros HTML (páginas estáticas) y JSP (páginas dinámicas). 
En las páginas dinámicas existen subcarpetas con ficheros **servlets**, **beans**, **librerías** y ficheros estáticos.

En el despliegue se considerará:
- El uso de comprimidos **WAR** con todo lo necesario del despliegue
- La edición de **archivos XML** como la configuración del servidor en  **server.xml**  y el descriptor de despliegue de la aplicación en **web.xml**.

**La nomenclatura de las carpetas:**
- **www** alojará archivos para ejecutarse ante una petición web
- **bin** alojará ficheros ejecutables
- **src** alojará el código fuente

**Despliegue en Tomcat de aplicaciones en forma de directorio (exploded deployment)****
- Copiar la carpeta **www** en directorio **webapps**
- Crear árbol de directorio con una carpeta principal que se llame como la aplicación a ejecutar y en su interior la carpeta **WEB-INF** con otras internas **lib** (con los .jar) y **classes** (con el bytecode compilado por la JVM).
- Dentro de **WEB-INF** estará el descriptor de despliegue **web.xml** con las rutas de los servlets y las configuraciones usadas en la aplicación.

## 2. Administración de aplicaciones web

Para el despliegue de la aplicación en el servidor, este debe **tener iniciados los servicios de servlets y JSP**.  Esto quiere decir: es necesario un servidor de aplicaciones que sea compatible con Java EE (Apache Tomcat, Wildfly, GlassFish, Jetty...)

Se deben tener las **variables de entorno**
- **JAVA_HOME**: Ruta de los archivos del JDK de Java
- **CATALINA_HOME**: Ubicación de los scripts de Tomcat

La especificación 2.2 de los Servlets estandarizó los pasos a seguir para que el despliegue de aplicaciones se pueda llevar a cabo en varios servidores y tener un código de Java verdaderamente portable. Ya se ha comentado (¡¡¡como 20000 veces en este material de mierda que estoy resumiendo!!!) que es posible hacerlo mediante archivos WAR o copiando el directorio a la carpeta **$CATALINA_HOME/webapps** 

## 3. Autenticación de usuarios. Dominios de seguridad para la autenticación

**Engine**: (Motor) es el **componente central del servicio Catalina** que **gestiona todas las aplicaciones web** en un servidor.
- Es el **núcleo de procesamiento** de Tomcat dentro de un `<Service>`.
- Contiene uno o varios **hosts virtuales (`<Host>`)**, que representan diferentes dominios o aplicaciones dentro del servidor.
- Puede incluir **válvulas (Valves)** para filtrar y procesar las solicitudes antes de que lleguen a los Hosts y Contextos.

**Válvula**: Son componentes propios de Tomcat (no tienen uso general en JavaEE) que se configuran en el `servlet.xml` y que permiten realizar operaciones previas a la entrega de la solicitud a un servlet o JSP. Se insertan en medio del flujo de procesado de una petición web, capturando la acción y permitiendo realizar alguna acción o preprocesado antes de que pase al siguiente componente de Tomcat. 
**Permiten asociar una instancia de una clase de Java a un contenedor Catalina**. 
Se implementan en la interfaz `org.apache.catalina`
Podría por ejemplo ponerse una válvula en un `<Engine>` para capturar todas las peticiones antes de trasladarlas al componente anidado `<Host>`.

Las válvulas pueden ponerse:
- Dentro de un Engine
- Dentro de un Host
- Dentro del contexto de una aplicación web, llevándose a cabo el procesado requerido antes de acceder al contenido o componente web correspondiente. 


Algunas de ellas son:
- **Access Log Valve**: Ficheros log para información de los clientes como sesión o autenticación se usuarios
- **Remote Address Filter**: Permite el acceso de la IP del cliente que cumpla una expresión regular dada
- **Request Dumper**: Herramienta de depuración que describe detalles de los registros log
- **Single Sign On (SSO)** Permite la identificación de un usuario desde cualquier dispositivo conectado a la red. (Es decir, le permite iniciar sesión una sola vez y accede desde diversos lugares sin identificarse nuevamente)

Veamos el ejemplo de un **service.xml** con válvulas:

```xml
<Server port="8005" shutdown="SHUTDOWN">
    
    <Service name="Catalina">
        
        <!-- Definición del Engine -->
        <Engine name="Catalina" defaultHost="localhost">
            
            <!-- Válvula para registrar accesos en todas las aplicaciones -->
            <Valve className="org.apache.catalina.valves.AccessLogValve"
                   directory="logs"
                   prefix="engine_access_log"
                   suffix=".txt"
                   pattern="%h %l %u %t \"%r\" %s %b" />

            <!-- Válvula para bloquear accesos desde IPs no autorizadas -->
            <Valve className="org.apache.catalina.valves.RemoteAddrValve"
                   allow="192.168.1.*" />

            <!-- Definiendo un Host dentro del Engine -->
            <Host name="localhost" appBase="webapps" unpackWARs="true" autoDeploy="true">
                
                <!-- Válvula específica para este Host -->
                <Valve className="org.apache.catalina.valves.RequestDumperValve" />
                
                <!-- Aplicación web dentro del Host -->
                <Context path="/miApp" docBase="miApp" reloadable="true"/>
            </Host>
        </Engine>
    </Service>
</Server>

```

En la válvula puede observarse:
- Atributo **className**: Obligatorio. Indica la válvula a utilizar.
- Atributo **directory**: Indica carpeta en la que se guardarán los registros de acceso (directorio logs en carpeta base de instalación de Tomcat)
- Atributo **prefix**: Como comenzará el nombre del archivo donde se guardarán los logs de la válvula. Añadirá automáticamente después de eso la fecha de creación del archivo
- Atributo **suffix**: Extensión del archivo de log
- Atributo **pattern**: Formato de cada evento registrado. (%h nombre del equipo o IP, %u usuario remoto, %t fecha y hora, %r primera línea de peticion HTTP, %s código de estado HTTP de la respuesta generada, %b cantidad de bytes enviados al cliente sin incluir la información del protocolo HTTP en sí mismo).

El registro de acceso sería habitual configurarlo de forma exclusiva para una aplicación web. Para ello se metería una válvula dentro del contexto de la aplicación (META-INF/context.xml).
## 4. Administración de sesiones. Sesiones persistentes.

Una **sesión** es un conjunto de información que la aplicación wbe almacena para cada cliente (productos incluidos, datos introducidos por última vez en un formulario, nivel de privilegios,...)

En un servidor Tomcat, las sesiones están configuradas por defecto para su mantenimiento ante posibles pérdidas de conexión o reinicios con el servidor (cookies y similares por parte de los usuarios en las páginas web).
Además, se puede **ampliar el control sobre dichas sesiones**.

Las sesiones inactivas pero no caducadas se pueden almacenar en disco para liberar la memoria de control de las sesiones y recursos de memoria asociados.

Las sesiones activas se almacenan en disco al detener el servidor. Y se recuperan una vez reiniciado. 

Las sesiones que superen un tiempo definido, son copiadas automáticamente para evitar bloqueos de esta.

Para la gestión de las sesiones persistentes debe realizarse la configuración del elemento como un subelemento dentro de la misma sesión. Así se puede especificar si se quiere que se apliquen a todas las funciones o solo a algunas en concreto.

Globalmente: `/conf/context.xml`. (Aunque no es lo recomendable)
Localmente en una aplicación concreta: Adaptar el `/META-INF/context.xml` correspondiente a la aplicación. 

**Ejemplito**
```xml
<Context>
    <Manager className="org.apache.catalina.session.PersistentManager" pathname="SessionesAppEjemplo.ser">
        
        <!-- Guardar sesiones en disco si están inactivas -->
        <Store className="org.apache.catalina.session.FileStore"/>
        
        <!-- Elimina sesiones inactivas después de 30 minutos -->
        <MaxIdleBackup>30</MaxIdleBackup>

        <!-- Elimina sesiones definitivamente después de 24 horas -->
        <MaxActiveSessions>1000</MaxActiveSessions>

    </Manager>
</Context>
```

Existen dos gestores de sesiones en Tomcat:
- **StandardManager**: Permite a las aplicaciones crear y borrar información de sesión y además guarda la sesiones activas en disco cuando Tomcat se reinicia (el usuario final no notará esto). Por defecto, sino se indica gestor de sesiones se crea un gestor StandardManager y el archivo en caso de apagar el servidor es `SESSIONS.ser`. 
- **PersistenceManager**: Amplía la funcionalidad de StandardManager. Realiza lo mismo y además almacena de forma persistente las sesiones que no están en uso y que todavía no están caducadas en disco o en una base de datos. Esto mejora el rendimiento ya que libera recursos de memoria. Ej.: Si un usuario puso varios productos en un carrito y salió de la página varias horas después o varios días pueden recuperarse  ofrecerle al usuario tal y como lo tenía.

 Para cambiar el gestor de sesiones se indica con el atributo `className` y para el archivo el atributo `pathname`.

Ejemplo:
Usar un `PersistenceManager` indicandole que se guarden las sesiones activas en disco al apagar el servidor (`<Store>`), indicando el máximo número de sesiones activas (`<MaxActiveSession>`, siendo -1 ilimitado), y `minIdleSwap`/`maxIndleSwap` como intervalo de tiempo mínimo que debe esperarse para almacenar una sesión inactiva de forma persistente. Tambien con `Store` se indica cómo y donde almacenar las sesiones activas que no están en uso. Debe indicarse un `FileStore` (en disco) o un `JDBCStore` (BBDD).

## 5. Autenticación de usuarios

Para establecer mecanismo estandar a través del descriptor de despliegue, permitiendo autenticar diferentes componentes de la aplicación web en lo que se denominan diferentes reinos (fichero `WEB-INF/web.xml`).

Definición de roles:
```xml
<security-role>
	<description>Usuario normal</description>
	<role-name>usuario</role-name>
</security-role>
```

Cómo realizar la autenticación desde el navegador
```xml
<login-config>
	<auth-method>BASIC</auth-method>
	<realm-name>EjemploWebApp</realm-name>
</login-config>
```

En el descriptor de despliegue deben incluirse qué recursos están limitados por el control de acceso:
(Se limita a todos los recursos permitiendo solo a los usuarios con el rol usuario)
```xml
<security-constraint>
	<display-name/>
	<web-resource-collection>
		<description/>
		<url-pattern>/*</url-pattern>
	</web-resource-collection>
	<auth-contraint>
		<description/>
		<role-name>usuario</role-name>
	</auth-contraint>
</security-constraint>
```

Los usuarios y sus contraseñas se indican con el 
```xml
<Realm className="org.apache.catalana.realm.UserDatabaseRealm" resourceName="UserDatabase"/>
```

Este componente se puede ubicar en tres niveles diferentes (Engine, Host o Context). 
Puede configurarse en server.xml o en META-INF/context.xml, según el ámbito que donde se desee que se aplique la configuración. 

## 5. Archivos de registro de acceso y filtro de solicitudes

Los ficheros de registro son importantes.
En Apache se configuran en la configuración por defecto. 
- **Linux:** `/var/log/apache2/` o `/var/log/httpd/`
-  **Windows:** `C:\xampp\apache\logs\` (en XAMPP)
Directiva **ErrorLog** que define la ruta del fichero, junto con **LogNivel** que indica nivel de prioridad.

En Tomcat.
- **Linux & Windows:** `TOMCAT_HOME/logs/` (Ej: `/opt/tomcat/logs/` o `C:\tomcat\logs\`)

## 6. Configuración del servidor de aplicaciones para la cooperación con servidores web

Desde Tomcat Web Manager (127.0.0.1:8080/manager/html) puede verse el listado de aplicaciones en el Gestor de Aplicaciones, donde pueden iniciarse, desplegarse,...

## 7. Despliegue de aplicaciones en el servidor de aplicaciones

Para el despliegue de aplicaciones en este libro asqueroso propone el uso de "Apache Ant bajo Linux". 

Será necesario habilitar el acceso a Tomcat Web Manager y usar credenciales de un usuario que tenga **manager-script** (porque se va a hacer en modo texto).

Para ello en el fichero `tomcat-users.xml` se debe declarar el usuario de forma parecida a esto:
```xml
<user username=”tomcatscript” password=”despliegue” roles=”manager-script”/>
```

Las aplicaciones desplegadas se podrán ver usando el comando **list**

En Eclipse se puede configurar el software Ant para que este pueda interactuar con el modo texto del servidor.

En el cliente se crea un fichero **build.xml** que define las tareas de Ant. Y en ese mismo proyecto se añade el fichero .war y las listas de aplicaciones desplegadas.
Finalmente se inician las aplicaciones para que se puedan desplegar.

---

También se podría configurar el servidor mediante Eclipse y Ant. Con Windows > Preferences > Ant > Runtime. Seleccionando Ant Home Entries y pulsando el botón para añadir ejecutable .jar añadiendo las librerías:
1. Catalina-ant.jar
2. Tomcat-coyote.jar
3. Tomcat-util.jar
4. Tomcat-juli.jar

El fichero `build.xml` se puede crear mediante Eclipse. Si abrimos la tarea de Ant y se cambia su configuración en la propiedad `ManagerUrl` cuyo valor sería la dirección del servidor y la carpeta `Manager/Text`.

Finalmente, probar la tarea con la opción "Crear War" y eligiendo el fichero correspondiente. Tras ello se ejecuta con "Run As".

Algunas etiquetas son: 
- **project**: Solo uno. Se corresponde con la aplicación Java
- **target**: Tareas que se quieren aplicar a la aplicación en algún momento. Se puede hacer que unos targets dependan de otros.
- **task**: Código ejecutable que se aplicará a la aplicación. Puede tener propiedades como el classpath. Ant tiene muchas tareas básicas ya como compilación y eliminación de ficheros temporales pero puede extenderse el mecanismo de ser necesario
- **property**: Parámetro clave-valor que se necesita para procesar la aplicación. 

**Ejemplito del archivo**
```xml
<?xml version="1.0" encoding="UTF-8"?>
<project name="DeployTomcat" basedir="." default="deploy">

    <!-- Definir la propiedad de la URL del Manager de Tomcat -->
    <property name="tomcat.manager.url" value="http://localhost:8080/manager/text"/>
    <property name="tomcat.username" value="admin"/>
    <property name="tomcat.password" value="admin"/>

    <!-- Definir el directorio de la aplicación y el archivo WAR -->
    <property name="webapp.dir" value="path/to/your/webapp"/>
    <property name="war.file" value="${webapp.dir}/your-webapp.war"/>

    <!-- Tarea para compilar la aplicación y crear el archivo WAR -->
    <target name="create-war">
        <echo message="Creating WAR file..."/>
        <war destfile="${war.file}" webxml="${webapp.dir}/WEB-INF/web.xml">
            <fileset dir="${webapp.dir}">
                <exclude name="WEB-INF/web.xml"/>
            </fileset>
        </war>
    </target>

    <!-- Tarea para desplegar el WAR en Tomcat -->
    <target name="deploy" depends="create-war">
        <echo message="Deploying WAR to Tomcat..."/>
        <http
            url="${tomcat.manager.url}/deploy?path=/your-app&war=file:${war.file}"
            username="${tomcat.username}"
            password="${tomcat.password}"
            method="POST"/>
    </target>

    <!-- Tarea para detener la aplicación en Tomcat -->
    <target name="undeploy">
        <echo message="Undeploying application from Tomcat..."/>
        <http
            url="${tomcat.manager.url}/undeploy?path=/your-app"
            username="${tomcat.username}"
            password="${tomcat.password}"
            method="POST"/>
    </target>

</project>

```

## 8. Seguridad en el servidor de aplicaciones. Configuración del servidor de aplicaciones con soporte SSL/T

Debe tenerse habilitado el servicio SSL en el host por defecto y configurar la aplicación para que solo permita conexiones HTTP.

**1.- Crear almacén de clave con certificado SSL**. Se usa la herramienta keytools para certificado autofirmado y guardarlo en el almacén de claves. Se introducirá la clave estándar y las clases asociadas al alias en el servidor durante el proceso de generación. 
**2.- Configurar conector SSL del servidor de aplicaciones**: Editando el fichero `server.xml`. Se escuchará en puertos 8080 (HTTP) y 8443 (HTTPS)
**3.- Para solo admitir HTTPS**: Debe editarse la configuración en la propia aplicación y poner:
```xml
<user-data-constraint>
<transport-guarantee>CONFIDENTIAL
</transport-guarantee></user-data-constraint>
```

Es posible hacer la comprobación estableciendo una conexión HTTP a la aplicación: de esta forma, el servidor la redirige automáticamente a una petición segura HTTPS.

## 9. Wildfly

Wildfly implementa un servidor de aplicaciones Java EE. Mientras que Tomcar solo es servidor web y contenedor de servlets, Wildfly es servidor de aplicaciones que implementa todas las funcionalidades de la especificación JavaEE. 

**Instalación**
```shell
# Primero descargarlo de la pagina oficial
# Luego se copia a donde se quiera instalar y se descomprime
sudo tar xvfz wildfly-13.0.0.Final.tar.gz
# Se crea el usuario que ejecutara wildfly
sudo adduser --no-create-home --disabled-passdword --disabled-login wildfly
# Darle permisos a la carpeta que contiene wildfly para que pertenezca al usuario 
sudo chown wildfly:wildfly opt/wildfly-13.0.0.Final --recursive
# Configurar variables de entorno
export WILDFLY_HOME=/opt/wildfly-13.0.0.Final
export PATH=$PATH:$WILDFLY_HOME/bin
# Ejecutar wildfly
sudo -u wilfly -i standalone.sh
# Instalar wildfly como servicio si se quiere (se proporcionan los scripts wildfly-init.sh)
# Configurar archivo /etc/default/wildfly con la informacion necesaria para ejecutar wildfly (carpeta JDK, carpeta wildfly, nombre de usuario con el que se ejecutara, modo de ejecucion (standalone), archivo de configuracion para el modo de ejecucion (standalone.xml))
sudo update-rc.d wildfly defaults
```

**Despliegue de aplicaciones**
Debe elegirse un usuario de gestión Management User que será un usuario dentro del realm conocido como ManagementRealm
Para ello se ejecuta **add-user.sh**
```
sudo -i -u wildfly /opt/wildfly-13.0.0.Final/bin/add-user.sh
```

Con eso ya será posible entrar en http://localhost:8080/console