(UF1 Desarrollo web en entorno servidor)

## 1. Modelos de programación en entornos cliente/servidor

En el desarrollo web se distinguen distintos **modelos de programación** según donde se realice la ejecución de código:
- **Programación del lado del servidor**: Permite interactuar a un cliente con un servidor, realizando peticiones y respuestas respectivamente para la gestión y consulta de páginas web de forma dinámica. Lenguajes de servidor: ASP, PHP, Perl, Python, JSP, servlets.
- **Programación del lado del cliente**: Tecnología que muestra el contenido recibido por el servidor. Lenguajes de cliente: JavaScript, XML o Applets (ya no se usan)
## 2. Generación dinámica de páginas web

- **Páginas webs dinámicas**: Son aquellas que durante su ejecución cambian la información que muestran al usuario. Cada vez que un usuario visita la página, el contenido se actualiza mediante programación y bases de datos. Será necesario que el administrador del sitio web pueda realizar los cambios necesarios en un panel de administración (CMS, Content Management System). No debe confundirse con aquella que tiene animaciones (como podría ser la tecnología Flash).  También hay tecnologías que pueden usarse como AJAX y Jquery para que resulte más interactiva y vistosa para el usuario. 
- **Páginas web estáticas:** Se desarrollan en HTML y CSS, sin ningún lenguaje de programación. Son páginas con contenido fijo que no se actualiza. La información podría modificarse pero es más laboriosos. Los cambios se realizan descargando el código, modificándolo y volviéndolo a subir al servidor.

**Características de una web estática**
- HTML 
- Económica
- Rápido desarrollo
- No tiene datos de páginas web
- Actualización de contenidos costosa
- Sin modificaciones
- El usuario no interacciona con los contenidos ofrecidos en la web

**Características de una web dinámica**
- Usa algún lenguaje de programación
- Desarrollo complejo, lento, laborioso. Mantenimiento del servidor costoso
- Permite mostrar datos de fuentes como una base de datos
- El administrador puede modificar el usuario fácilmente
- Ofrece la posibilidad de que el usuario modifique la vista

## 3. Lenguajes de programación en entorno web

Existen múltiples lenguajes que se usan en el desarrollo de una web.

**CSS**
Utilizado en las hojas de estilo. Archivos que definen las propiedades de todos los elementos de la web. Posibilita la creación de un diseño que hará más atractiva la web. La función principal de las hojas de estilo es separar la estructura de la web del diseño. La versión actual es CSS3.

**HTML**
Lenguaje de marcas que se encarga de definir el contenido de la web y cómo este se distribuye en el navegador web. La versión actual es HTML5, que incluye mejoras en relación con anteriores versiones como incorporación de elementos multimedia o creación de nuevas etiquetas.

**JavaScript**
Lenguaje de programación interpretado que aporta funcionalidad a HTML permitiendo al usuario interactuar con la página web.

**Applets**
Pequeños programas creados con Java a los que se puede acceder a través de un navegador web, aunque son independientes de este. Por eso no pueden interaccionar con otros elementos de la web. Ofrecen más funcionalidades que una web creada con JavaScript (en la época en la que se hicieron) y ya no están en uso.

**Flash**
Plataforma que utiliza el lenguaje de programación orientado a objecto ActionScript para crear animaciones y contenido multimedia en las páginas web. Esto tampoco lo usa nadie ya. 

**XML**
Lenguaje para el intercambio de datos de forma legible entre aplicaciones ya formen parte de la misma plataforma o de una plataforma distinta. El uso de este lenguaje permite compartir información de forma libre, fiable y fácil.

**JSON**
Lenguaje utilizado para el intercambio de datos de forma legible entre aplicaciones multiplataforma pero con uso menor en el entorno web (en la época en la que esto se escribió). JSON realiza intercambio mediante un análisis sintáctico (parser). Como ventaja, parser es más sencillo que las etiquetas XML.

## 4. Integración con los servidores web

Para **acceder a un servidor web** el usuario debe especificar el recurso al que quiere acceder, indicando la dirección URI correspondiente.
### 4.1. Dirección URI

La **dirección URI** es el identificador único de los recursos de la web, teniendo en cuenta que estos varían a lo largo del tiempo. La estructura de una URI es la siguiente:
- **Esquema**:  Especifica el protocolo de acceso al recurso. Suele ser el protocolo de Internet HTTP o HTTPS si es de modo seguro.
- **Autoridad:** Identifica la información necesaria para acceder al servidor (dominio en el que se encuentra)
- **Ruta:**  Camino que debe seguir una vez que se accede al servidor para llegar al recurso. Puede verse como la ruta del ordenador para llegar al fichero especificado. 
- **Consulta:** Información referente a una especificación del recurso. Este campo de la URI va precedido del símbolo `?`Autoridad y ruta se refieren a información jerárquica pero consulta está formada por conjuntos de clave=valor que identifican al recurso en el servidor.
- **Fragmento:** Identifica una parte del recurso. Se considera una subdirección dentro de la URI. Va precedido por el símbolo `#`. Debe considerarse que este campo es el que diferencia una dirección URL de una dirección URI.
![[Pasted image 20250513002947.png]]

### 4.2. Petición de un recurso a un servidor. Comunicación cliente-servidor al realizar petición para acceder a recurso

1. Primero, el usuario debe indicar la URL a la que quiere acceder en el navegador web para realizar la petición. El navegador decodifica esta URL para conocer cada uno de los campos de la dirección y abre conexión TCP/IP con el servidor correspondiente.
2. Después, es posible el envío de mensajes del protocolo HTTP. (HTTP tiene "tres" tipos de mensajes)
3. Finalmente, el servidor web devolverá la respuesta correspondiente al cliente y se cerrará la conexión TCP/IP.

**Tipos de mensajes del protocolo HTTP para ocmunicarse con el servidor**
- **GET**: Recoge datos del servidor
- **HEAD**: Recoge información sobre el recurso
- **POST**: Envía datos al servidor
- **PUT:** Reemplaza todas las representaciones actuales del recurso de destino con la carga útil de la petición
- **DELETE:** Borra un recurso específico
- **CONNECT:** Establece un túnel hacia el servidor identificado por el recurso
- **OPTIONS:** Describe las opciones de comunicación para el recurso de destino
- **TRACE:** Realiza una prueba de bucle de retorno de mensaje a lo largo de la ruta del recurso de destino
- **PATCH:** Aplica modificaciones parciales a un recurso 
## 5. Lenguajes de programación en entorno servidor

Se analizan las características de los principales lenguajes de entorno serviodr:

**PHP**
- **Permite la inserción de código en el servidor web**
- Se realiza con **ficheros con extensión `.php`*** mediante **etiquetas `<?php ?>`**
- Puede **incrustarse en un HTML** (es su forma más habitual), por lo que es muy usado en desarrollo web
- **No es un lenguaje compilado sino ejecutado** en el servidor, generando un HTML que luego es enviado al cliente

**Perl**
- Lenguaje de programación centrado en el desarrollo de programas que permitan la comunicación entre cliente y servidor (**CGI**, common gateway interface)
- La comunicación retorna como resultado **objectos MIME**
- Las aplicaciones **CGI** fueron de las **primeras en creación de webs dinámicas**
- Es un **lenguaje de programación interpretado**, por lo que cada petición del cliente pasa por la interpretación y ejecución de los scripts de código identificados por extensión `.pl`

**Python**
- **Lenguaje de programación interpretado** 
- Poderoso y **fácil de entender**
- Permite usar la **programación orientada a objetos**
- Es considerado de **alto nivel**, usa **frameworks** que se integran para permitir el desarrollo de aplicaciones web
- **Paradigma muy diferente a PHP y  más abstracto**
- La **extensión de sus archivos es `.py`**

**ASP**
- Tecnología web desarrollada y comercializada por Microsoft para crear webs dinámicas
- Usa **.NET Framework** para acelerar la creación de sitios webs
- Sus archivos tienen **extensión `.asp`**.
- **ASP es una tecnología dinámica que se ejecuta del lado del servidor**. Al igual que en PHP se necesita ejecutar los scripts para la generación de HTML devuelvo al cliente como respuesta de sus peticiones.
- Se utiliza el **lenguaje C#**

**JSP**
- Orientada a **desarrollar páginas webs con Java**
- Busca **crear aplicaciones web que se ejecuten en diferentes servidores**
- Necesario instalar un **motor JSP**, basado en los servlets de Java.
- La extensión de sus ficheros es `.jsp`. Contienen sentencias Java que se deben ejecutar en el servidor JSP
- Es **compilado**

**Servlets**
- **Objeto Java dentro del lenguaje de programación del mismo nombre**
- Sirve para crear páginas web. El servlet es un programa que admite peticiones utilizando el protocolo HTTP. Procesan las peticiones realizadas por los clientes para devolver un HTML como resultado.
- Son **capa intermedia entre navegadores y bases de datos**
- Se incluyen en servidores web como Apache o Apache Tomcat.

## 6. Integración con los lenguajes de marcas

A veces, el contenido que aparece en una página puede cambiar según el navegador en que se ejecuta.
Es necesario **esforzarse para conseguir una web que se adapte a todos los navegadores**. Esto se dificulta con la aparición de nuevas plataformas de conexión.

La **arquitectura CGI** busca hacer más fácil la interacción de los usuarios con las webs para ofrecer contenido dinámicos en las mismas.
Esta fue la primera arquitectura que permitió crear webs dinámicas y que permite ofrecer un esquema de peticiones entre cliente y servidor.

1. El cliente web realiza una petición con el protocolo HTTP
2. El módulo CGI a partir de esa petición que contiene los parámetros se comunica con la base de datos
3. La base de datos devuelve la información al módulo CGI que, con los datos, genera el resultado (un documento HTML)

Se caracteriza por el **dinamismo** al ver los valores recibidos por el módulo CGI, ya que dependiendo de los valores que el cliente ha introducido determina una operación u otra.

Se observan **vulnerabilidades** como: 
- que es **difícil controlar el acceso a los servicios**, ya que se trata de una comunicación sencilla de implementar y el contenido viaja vía HTTP.
- que **es complejo determinar qué elementos son accesibles**, no quedan la seguridad del todo garantizada
- con la llegada masiva de nuevas tecnologías han aumentado el número de peticiones y eso lo hace difícil de gestionar (problemas de **escalabilidad**)

**CGI no almacena el estado**. Una vez realizada la petición esta no es almacenada, ni tampoco los resultados obtenidos.

La **construcción de la invocación CGI** se hace manteniendo los formatos de construcción de una dirección URL.

**Tipos de CGI**
- **Contador de accesos**: Número de veces que se ha solicitado una página determina y guarda el valor en un fichero. Cada vez que se invoca, se incrementa.
- **Buscador:** Busca páginas que contengan coincidencias con un valor especificado y devuelve la localización encontrada. 
- **Correo:** Recoge los datos del usuario.
- **Colaboración:** Añade la posibilidad de generar nuevos enlaces o contenido en una determinada web y devuelve la localización del contenido.
- **Estadísticas:** Presenta un registro de log en un archivo que guarda las distintas estadísticas recogidas.
- **Administración:** Permite interactuar con el servidor y gestionar su comportamiento. 

## 7. Herramientas de programación

A la hora de escribir código es imprescindible elegir qué herramientas se usarán para construir estos ficheros de código.

**Características de las herramientas de programación**
- Poseen **gran cantidad de temas para personalizar** y diferenciar cada componente de un lenguaje
- Permite **diferenciar** métodos, variables, constantes, comentarios, etc.
- Ayudan a **visualizar el código de forma limpia** y ordenada. Cuentan con herramientas que facilitan la programación.
- Permiten la **integración** de plugins de lenguaje, funciones de autocompletado y sugerencias, tabulaciones automáticas de código, resaltar paréntesis y llaves concordantes, etc.
- Reconocen la **sintaxis** de la mayor parte de lenguajes de programación. 

**Tipos de herramientas**
- **Editor de texto plano**: Permite crear y modificar archivos de texto. Mediante caracteres especiales da algo de formato al archivo. Estos caracteres se denominan caracteres de control. Un ejemplo de ellos es Sublime Text.
- **IDE**: Programa que proporciona en un mismo entorno todas las herramientas necesarias para el desarrollo completo de una web. La elección de uno de ellos viene determinada a veces por si el software es libre o privado. O por la integración y las facilidades que se ofrecen con respecto al lenguaje empleado. Algunos IDEs son Eclipse,  Netbeans, Microsoft Visual Studio. Todo IDE tiene incluido un fichero de texto plano en el que se inserta el código.

