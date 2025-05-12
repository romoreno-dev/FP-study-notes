(UF4 Servicios web. Páginas dinámicas interactivas. Webs híbridas)

## 1. Ejecución de código cliente y servidor

Para ejecutar una aplicación es necesario o bien:
- publicar el dominio en Internet para que este sea accesible desde una web
- o ejecutar dicha aplicación para uso personal dentro del equipo

Los diferentes archivos son alojados en un servidor con una dirección IP de acceso a la web.

El cliente abre el navegador y selecciona la dirección o nombre vinculado a la aplicación web, comenzando la ejecución del código cliente.

Los diferentes archivos de código de la aplicación se ejecutan de forma automática en respuesta a la petición de un servicio por parte del cliente  o se ejecutan periódicamente los scripts programados para ello.

Así, el código asociado al **cliente** se corresponde con todos los aspectos web, así como la información que el cliente incluye en los elementos habilitados permitiendo al servidor componer la totalidad de la web a mostrar según se realizan peticiones. Se podría entender que el cliente es capaz de generar nuevas porciones de código que el servidor interpretará para mostrar los resultados de forma dinámica en cada una de las solicitudes realizadas.

El **servidor** es el encargado de ejecutar los ficheros o scripts que el evento del servicio web ha solicitado. Dependen de forma general del cliente ya que están asociadas a elementos de una web. 

Existen algunos scripts que se ejecutan de forma automática, estos servicios suelen tener carga elevada de procesamiento de datos o se aplican en la comprobación de algunas reglas de configuración general de aplicación, es decir, servicios relacionados con los administradores del sitio web. Por eso, la ejecución es controlada y monitorizada periódicamente.
## 2. Librerías y tecnologías relacionadas

El desarrollo de una web dinámica se debe especificar y programar usando una tecnología que determinará cuáles son los requisitos que permiten ejecutar una aplicación.

Algunas de las **tecnologías** empleadas y **requisitos** necesarios:
- **ASP**. Sistema operativo Windows con servidor web IIS
- **ASP.NET**. Windows como sistema operativo, con IIS y el framework de .NET
- **PHP**. Sistema operativo indiferente pero el servidor necesita tener instalado el módulo PHP que permita interpretar el código. Habitualmente se tiene PHP sobre Linux y Apache.
- **JSP**. Permite su uso sobre cualquier sistema operativo. Necesita unservidor web como Apache Tomcat o Sun Java System Web Server y alguna versión de J2SDK.

Para realizar las pruebas se necesita tener un **servidor local** instalado o un **hosting** que permita la gestión del sitio web.
Si se quieren realizar de forma local hay tecnologías que permiten emular un servidor dentro de un equipo proveyendo todo el software necesario para programar, por ejemplo, en PHP y MySQL:
- easyPHP
- XAMPP
- WAMP

Las **librerías enfocadas a la ejecución** dentro de la interfaz de la web (librerías: su uso depende del lugar de aplicación) son:
- **Jquery**: Librería de JavaScript cuyo objetivo es facilitar al máximo el trabajo con JavaScript
- **ReactJS**: Librería JavaScript del lado del cliente que permite desarrollar interfaces de usuario
- **PolymerJS:** Framewoork que combina HTML, CSS y JavaScript para crear componentes web
- **Boostrap:** Framework para la creación de webs con diseño responsive basado en HTML5 y CSS3
- **ATLAS**: Framework que integra una serie de librerías para el desarrollo del lado del servidor

## 3. Generación dinámica de páginas interactivas

Una **página web interactiva** es aquella capaz de cambiar su aspecto y comportamiento en función de las peticiones que el cliente va realizando.

Para realizar estos cambios y que pasen desapercibidos para el usuario, se neceista ejecutar partes del código en el propio navegador.

**El navegador manda una petición al servidor**: se ejecuta código en el servidor y esto genera una página web que será enviada de nuevo al navegador. La página web modificará su aspecto mostrando al cliente la nueva información obtenida.

Este proceso da nombre a este tipo de páginas webs ya que continuamente se generan nuevas páginas webs con base a las peticiones realizadas por el cliente.

La creación de este tipo de web se basa en el uso del lenguaje HTML pero es necesario combinarlo con otros como PERL CGI, PHP, JavaScript o ASP, que ayudarán a dar dinamismo a los elementos e interacciones del usuario.

Se busca como **objetivo** proporcionar al usuario información completamente actualizada en cada momento. Los usuarios son parte involucrada en la creación de contenido, pudiéndose ver como **web colaborativa** en la que el cliente añade comentarios, respuestas, elementos de compra a un carrito o filtra determinado tipo de contenido permitiendo a los desarrolladores añadir gran cantidad de funcionalidades y características a la web.

Las **cookies** son datos que identifican a un navegador. Ayudan al dinamismo de los sitios web. El navegador almacena en estos archivos los datos que el servidor le envía y se produce reenvío de estos datos desde el navegador al servidor.
Por medio de ellas un servidor puede identificar a un usuario durante la navegación dentro de todos los dominios del sitio web. Algunos datos dinámicos a mostrar son: el nombre de usuario, el número de productos que contiene el carrito de compra, el idioma establecido para ver el contenido del sitio web.


## 4. Obtención remota de información. Formularios

Para mostrar los datos que han sido enviados desde un determinado enlace se pueden usar métodos que usan etiquetas HTML como PHP.
Se produce una espera en la visualización de los datos ya que probablemente primero deben ser validados por el servidor.

Si se desea ver los datos al momento se utilizarán formularios. Los formularios son procesados en el navegador y son el paso previo a la obtención de los permisos para hacer uso de los servicios web. Los formularios pueden ser programados en HTML, Perl, PHP, Java o .NET.

La obtención de la información se produce de forma sencilla: todos los formularios tiene un método de envío (suele ejecutarse a través de un botón de la interfaz). La información es validada primero, es decir, se comprueban los datos antes de guardarlo en base de datos. Se pueden añadir estructuras de control que permitan una mejor validación de la información que se va a enviar. Así, se consigue una correcta persistencia en las tablas de la BBDD. Una vez se han validados, los datos se envían al servidor. 

## 5. Modificación dinámica de la estructura de la página web

A diferencia de las páginas webs estáticas, las dinámicas **no tiene el contenido ya fijado**. Es decir, las páginas que se mostrarán aún no han determinado qué información verá el usuario. Cuando se envían los datos al servidor, este devuelve una web con una parte del contenido ya creado y el resto del contenido lo obtiene de diferentes sitios.

El **intérprete de lenguaje** instalado en el servidor es el **encargado de transformar la información del usuario en la obtención de información asociada a dicha petición** por lo que la web va cambiando su aspecto según el usuario va ejecutando una serie de eventos.

Ejemplos de webs dinámicas: Ventas, carritos de compra, interacción en tiempo real, noticias, blogs, foros,...

## 6. Programación de aplicaciones web

Hay una serie de **fases** que estructuran la creación completa de una aplicación web. Describen el recorrido general para su creación y programación:
1. **Identificación del sitio donde se alojará el código** de la aplicación y **definición del lenguaje de programación en el que se desarrollará** tanto para el cliente como para el servidor
2. **Diseño y construcción de la interfaz de usuario**. Suele crearse la interfaz antes que la lógica de negocio (?¿a diferencia de la creación de software??¿)
3. **Creación de la arquitectura de la base de datos**. Se debe escoger el intérprete del lenguaje y gestor de cliente encargado de la ejecución de sentencias SQL en BBDD como MySQL
4. **Desarrollo del código de la aplicación** donde se aplica la lógica de negocio. Determina la funcionalidad de la aplicación web
5. **Publicación de la web**: Se identifica el nombre que permitirá que todos los clientes accedan a ella para que la página sea accesible.
6. **Pruebas y mantenimiento**: Se da tras la publicación. Pueden encontrarse situaciones que mejorar o algún problema. La fase deberá ser repetida cada vez que se realice una corrección o mejora de la web.

Las tecnologías más usadas en la programación de aplicaciones web son HTMl y JavaScript (cliente) y del PHP,C#,Java (JavaEE con Web Beans o servlets) y ASP.NET (servidor)

Las **programación de una aplicación web** conlleva gran variedad de tecnologías estando su desarrollo dividido en la parte profesional en dos tipos de **especialidades**:
- **Front-end**: Conlleva el desarrollo de todos los aspectos relacionados con el diseño de la aplicación web, la creación de todas las interfaces de los sitios web del dominio 
- **Back-end**: Programación del lado del servidor. Desarrollo de toda la lógica de la aplicación que procesa los datos y los almacena en base de datos. 

----
En PHP se utilizan dos variables superglobales para recolectar datos
de formularios; $_GET y $_POST.
La forma que tienen estas variables superglobales de funcionar es
mediante la creación de una matriz con todos los pares de clave y
valor del formulario, que quedan así almacenados para que cualquier
función o clase puede tener fácil acceso a ellos. La diferencia
entre ambos es que, mientras que $_GET recibe las variables mediante
parámetros de URL, por lo cual son públicamente visibles y,
además, están limitadas en cuanto al número de caracteres (2000),
$_POST lo hace a través del método POST HTTP, que es invisible a
los demás y no tiene límites en cuanto a la cantidad de información
que es posible transmitir.
La ventaja del primer método es que es posible marcar la URL como
favorito del navegador, mientras que el segundo garantiza la privacidad
de los datos enviados

```html
<!DOCTYPE HTML>
<html>
	<body>
		<form action=”respuesta.php” method=”post”>
			Nombre: <input type=”text” name=”nombre”><br>
			E-mail: <input type=”text” name=”email”><br>
			<input type=”submit”>
		</form>
	</body>
</html>
```

Como podemos observar, la acción llama al archivo respuesta.php
usando el método POST. Dentro de dicho archivo, podemos colocar
el siguiente código:

```html
<!DOCTYPE HTML>
<html>
	<body>
		Hola, <?php echo $_POST[“nombre”]; ?><br>
		Tu dirección de correo es <?php echo $_POST[“email”]; ?>
	</body>
</html>
```