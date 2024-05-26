
## 1. Introducción

Una **red de ordenadores** es un sistema de comunicaciones que conecta ordenadores y otros equipos informáticos entre sí para compartir información y recursos. 

**Ventajas de usar una red de ordenadores**: 
Así los usuarios pueden hacer mejor uso de ellos y mejorar el rendimiento global del sistema u organización. 
- Reducción en presupuesto para software y hardware
- Posibilidad de organizar grupos de trabajo
- Mejoras en administración de equipos y aplicaciones
- Mejoras en integridad de los datos
- Más seguridad para acceder a la información
- Más facilidad de comunicación

Un **servicio en red** es un software que da funcionalidad o utilidad al sistema. Suelen estar basados en protocolos y estándares. Son los responsables de esas ventajas de la red de ordenadores.

**Clasificación de servicios en red según finalidad**
- **Administración / Configuración**: Administración y gestión de configuraciones de los distintos equipos de red (DHCP y DNS)
- **Acceso y control remoto**: Permitir la conexión de usuarios a la red desde lugares remotos, verificando su identidad y controlando su acceso (Telnet y SSH)
- **De ficheros**: Ofrecer grandes capacidades de almacenamiento para descongestionar o eliminar discos de las estaciones de trabajo permitiendo almacenamiento y transferencia de ficheros (FTP)
- **Impresión**: Compartir de forma remota impresoras de alta calidad, capacidad y coste entre múltiples usuarios
- **Información**: Servir ficheros en función de sus contenidos o información para ser procesada por aplicaciones (HTTP)
- **Comunicación**: Comunicación entre usuarios mediante correo electrónico (SMTP)

Algunos servicios en red toman como nombre el del protocolo del nivel de aplicación en que se basa: Servicio FTP se basa en protocolo FTP. 

## 2. Protocolos de comunicaciones del nivel de aplicación

El conjunto de protocolos TCP/IP constituye el modelo más importante sobre el que se basa la comunicación de aplicaciones en red. Gracias a Internet, redes locales y corporativas.

La capa de aplicación ocupa el nivel superior e **incluye los protocolos de alto nivel relacionados con los servicios en red**. 

Esta define los protocolos (normas y reglas) que utilizan las aplicaciones para intercambiar datos. 

**Protocolos estándar del nivel de aplicación**
- **FTP**: Transferencia de ficheros
- **Telnet**: Acceder a máquinas remotas a través de una red. Manejar computadora mediante intérprete de comandos.
- **SMTP**: Transferir correo electrónico. Protocolo POP para almacenar mensajes en sus versiones POP2 (dependiente de SMTP para enviar mensajes) y POP3 (independiente de SMTP)
- **HTTP**: Transferencia de hipertexto
- **SSH**: Gestionar remotamente a otra computadora de red de forma segura
- **NNTP**: Transferencia de noticias (Network News Transfer Protocol)
- **IRC**: Chat Basado en Internet
- **DNS**: Traducir direcciones de red

### 2.1. Comunicación entre aplicaciones

TCP/IP funciona con modelo cliente/servidor.
- **Cliente** : Ejecutado por el usuario. Solicita un servicio al servidor. Inicia la comunicación
- **Servidor**: Se ejecuta en una máquina y ofrece servicio (FTP, web, SMTP) a uno o múltiples clientes. Está a la escucha esperando peticiones, las acepta y como respuesta da el servicio solicitado.

**En la capa de aplicación las aplicaciones se comunican a través de la red con otros programas.**

Los procesos de esta capa son aplicaciones específicas que pasan los datos al nivel de aplicación en el formato que internamente use el programa, codificado de acuerdo a un protocolo estándar. 

Una vez los datos han sido codificados en un protocolo estándar de aplicación, pasan hacia abajo al siguiente nivel de la pila de protocolos TCP/IP.

En el **nivel de transporte** las aplicaciones hacen uso de TCP y UDP y están asociados un número de puerto: HTTP (80), FTP (21), SSH (22), Telnet (23), DNS (53), IMAP (143), 443 (HTTPS), 445 (Active Directory), 990 (FTPS)...

En el caso de World Wide Web la **comunicación HTTP**...:
- Cliente: Aplicaciones que permiten consultar webs
- Servidor: Aplicaciones que suministran páginas webs
- Al introducir el usuario una dirección web en el navegador (URL), este solicita por el protocolo HTTP una web al servidor que ejecuta en la máquina donde está la página
- El servidor web envía la página por Internet al cliente que la solicitó y este último la muestra al usuario.

Los dos extremos dialogan siguiendo un **protocolo de aplicación**:
- Cliente solicita www.dominio.es mediante GET HTTP/1.0
- Servidor contesta HTTP/1.0 200 OK y envía el HTML solicitado.

### 2.2. Conexión, transmisión, desconexión

**Los protocolos de aplicación se comunican con el nivel de transporte mediante un API** denominada API Socket. 
Java lo implementa en las clases del paquete `java.net` como `Socket` y `ServerSocket`

Socket Java: Representación de conexión para la transmisión de información entre dos ordenadores distintos o entre un ordenador y sí mismo. Abstracción a medio nivel que permite no centrarse en lo que pasa en capas inferiores.

El **socket** se caracteriza por:
- El protocolo usado
- Dirección IP local del proceso cliente
- Dirección IP remoto del proceso servidor
- Puerto local
- Puerto remoto

Se siguen los siguientes pasos:
- Se crean sockets en el cliente y el servidor
- Servidor establece el puerto por el que proporciona el servicio
- Servidor permanece a la escucha de peticiones de clientes
- Cliente conecta con servidor
- Servidor acepta conexión
- Intercambio de datos
- Cliente o servidor o ambos cierran la conexión

### 2.3. DNS y resolución de nombres

DNS (Domain Name Server)
Las computadores conectadas a la red TCP/IP se identifican por dirección IP. La IPv4 tienen 4 bytes sin signo separados por puntos.
Los nombres de dominio (www.dominio.com) y el servicio DNS buscan traducir o resolver nombres en las direcciones IP de cada equipo conectado a la red, para localizar y direccionar estos equipos dentro de la red.

Ventajas:
- Varios dominios pueden compartir una dirección IP
- Un dominio puede corresponderse a diferentes IP
- Cualquier servicio de red puede cambiar de nodo sin cambiar el nombre de dominio.

### 2.4. Protocolo FTP

FTP(File Transfer Protocol)

Prestaciones:
- Permite intercambio de archivos entre máquinas remotas a través de la red
- Consigue conexión y transferencia de datos muy rápida

Deficiencias:
- Información y contraseñas transmitidas en texto plano. Para conseguir una mayor velocidad de transferencia. -> El atacante podría capturar el tráfico y acceder al servidor o apropiarse de los archivos transferidos.

Para salvar este problema, puede encriptarse todo el tráfico de información a través del protocolo no estándar SFTP (con SSH) o de FTPS (con SSL). 

**Funcionamiento del servicio FTP**
El servidor da servicio a través de dos puertos:
- **Puerto 20**: Transferencia de datos
- **Puerto 21**: Transferencia de órdenes de control como conexión y desconexión
**El cliente se conecta al servidor con un puerto local mayor de 1024 y tomando como puerto destino del servidor el 21**. 

**Características del servicio FTP**
- Un usuario remoto al servidor FTP puede conectarse como usuario del sistema (cuenta de acceso), usuario genérico (cuenta anonymous), usuario virtual (no requiere cuenta local del sistema)
- El acceso al sistema de archivos es limitado según el usuario que se conecte y sus privilegios. Por ejemplo el usuario anónimo solo tendrá acceso al directorio público que establece el administrador por defecto.
- El servicio FTP soporta dos modos de conexión:
	- Modo activo: Forma nativa de funcionamiento. Se establecen dos conexiones distintas: La petición de transferencia por parte del cliente y la atención de dicha petición, iniciada por el servidor. Si el cliente está protegido por un cortafuegos, debe configurarlo para que se permita esta petición de conexión entrante a través de un puerto que normalmente por seguridad está cerrado.
	- Modo pasivo: El cliente inicia la conexión pero el problema del cortafuegos se traslada al servidor.

### 2.5. Protocolos SMTP y POP3

SMTP (Simple Mail Transfer Protocol)

El correo electrónico permite a los usuarios enviar y recibir mensajes y archivos rápidamente a través de la web. 

- El servidor mantiene cuentas de los usuarios y buzones
- Los clientes de correo gestionan descargas de mensajes y elaboración
- Servidor SMTP usa puerto 25
- Protocolo SMTP se encarga del transporte del correo saliente desde la máquina del usuario remitente hasta el servidor que almacena los mensajes de los destinatarios. 
- Usuario remitente redacta su mensaje, lo envía a su servidor. De allí va al servidor del destinatario que lo descarga en el buzón de la máquina local mediante protocolo POP3 o consulta vía web (IMAP)

### 2.6. Protocolo HTTP

HTTP (Hypertext transfer protocol)

Normas que posibilitan la comunicación entre servidor y cliente, transfiriendo páginas HTML. Método más común de intercambio de información en la Wordl Wide Web.

HTTP define tanto la sintaxis como la semántica que usan clientes y servidores para comunicarse.
- Es protocolo con esquema petición-respuesta
- Por defecto usa puerto 80
- Al cliente que efectúa la petición se le conoce como **user agent**
- A la información transmitida se le llama recurso y se identifica mediante un localizador uniforme de recurso (URL)
- Los recursos pueden ser archivos, resultado de ejecución de un programa, consulta a base de datos, traducción de un documento.
- HTTP es protocolo sin estado, no recuerda nada relativo a llamadas previas.

**Funcionamiento del protocolo HTTP**
- Usuario especifica en el cliente web la dirección del recurso a localizar con el formato `http://direccion[:puerto][:ruta]`
- Cliente web descompone información de URL diferenciando protocolo, IP o nombre de dominio, puerto y otros parámetros
- Cliente web establece conexión al servidor y solicita el recurso web por mensaje al servidor encabezado por un método, por ejemplo, **GET /organizacion.html HTTP/1.1** y otras líneas
- Servidor contesta con mensaje encabezado con la línea **HTTP/1.1. 200 OK** (por ejemplo o cualquier codigo de respuesta HTTP)
- Cliente web interpreta código recibido
- Se cierra la conexión 

Más información sobre protocolo HTTP en https://developer.mozilla.org/es/docs/Web/HTTP

## 3. Bibliotecas de clases y componentes Java

Java
- Tiene extensas capacidades de interconexión TCP/IP.
- Soporta diferentes niveles de conectividad en red.
- Facilita la creación de aplicaciones cliente/servidor y generación de servicios en red

Abrir URL, invocar métodos remotos, trabajar con sockers...

La API Java proporciona:
- **java.net** Clases para servicios de red, servidores y clientes
- **java.rmi** Implementar interfaz de control remoto (RMI)
- **javax.mail** Correo electrónico
También se dispone de bibliotecas externas como las proporcionadas por Apache Commons para protocolos Telnet, FTP, FTP sobre HTTP...

### 3.1. Objetos predefinidos del paquete `java.net`

El paquete `java.net` puede dividirse en dos niveles.

**API de bajo nivel**
- **Direcciones**: Identificadores de red (direcciones IP).  Clase `InetAddress`, implementa dirección IP
- **Sockets**: Mecanismos básicos de comunicación bidireccional de datos
	- Clase **`Socket`**: Extremo de conexión bbidireccional
	- Clase **`ServerSocket`**: Socket para escuchar y aceptar peticiones de clientes
	- Clase **`DatagramSocket`**: Socket para envío y recepción de datagramas
	- Clase **`MulticastSocket`**: Socket datagrama para enviar paquetes multidifusión
- **Interfaces**: Interfaces de red
	- Clase **`NetworkInterface`**: Interfaz de red compuesta de nombre y lista de direcciones IP asignadas a esa interfaz

**API de alto nivel** (Mayor abstracción, facilita la creación de programas que accedan a recursos de red)
- **URI** Identificador de recursos universal. Clase `URI`
- **URL** Localizador de recursos universal. Clase `URL`
- **Conexiones**: Con el recurso apuntado por URL
	- Clase **`URLConnection`** Superclase de todas las que representan enlace de comunicaciones entre aplicación y URL
	- Clase **`HttpURLConnection`** Una `URLConnection` con soporte para HTTP

### 3.2. Clase`InetAddress`

`InetAddress` da objetos para manipular direcciones IP, nombres de dominio. Para resolver host a IP y viceversa.

**Obtención de instancia**
Se consigue una instancia de `InetAddress` con los métodos estáticos:

```java
// InetAdress con direccionamiento del equipo en la red local (no localhost)
InetAddress.getLocalHost()
// InetAdress con los datos de direccionamiento del host pasado (nombre o IP valido)
InetAddress.getByName(String host)
// Array de InetAdress con los datos de direccionamiento del host pasado (mismo domunio puede tener mas de una IP a su disposición) 
InetAddress.getAllByName(String host)
```

Si no puede resolver, arrojarán `UnknownHostException`

**Métodos**

- **getHostAddress()**: Devuelve la IP en una cadena de texto
- **getAddress()**: Devuelve array con los grupos de bytes de la IP correspondiente
- **getHostName()**: Devuelve nombre del host en cadena de texto
- **isReachable(int tiempo)**: Devuelve si la dirección es alcanzable en el tiempo indicado

```java
var inetaddress = InetAddress.getByName("8.8.8.8");
inetaddress.getHostAddress(); // 8.8.8.8
inetaddress.getAddress(); // [8][8][8][8]
inetaddress.getHostName(); // dns.google
inetaddress.isReacheable(100); // true

InetAddress.getLocalHost()
```

### 3.3. Programación con URL

La URL representa la dirección a un recurso de la World Wide Web (archivo, directorio, consulta a BBDD, resultado de ejecución).

Se divide en:
- **Protocolo**. No solo http o https. También ftp, mailto, ldap, file, enws, gopher, telnet, ws, data...
- **Host**: Host del servidor
- **Puerto**: Puerto en el servidor para conectarse. Si no se especifica es el puerto por defecto para el protocolo
- **Ruta**: Path al recurso en el servidor
- **Referencia**: Fragmento de alguna parte específica del recurso

La clase `URL` de Java permite representar una URL. 
Con ella se podrá establecer una conexión e invocar métodos apropiados para obtener el contenido del recurso.

### 3.4. Crear y analizar objetos `URL`

**Creación**

- A partir de todos o de alguno de los elementos que forman parte de una URL
`URL(String protocol, String host, int port, String file)`

- A través de cadena especificada
`URL(String cadenaEspecificada)`

- A través de una rula relativa pasada como parámetro y agregada al primer parámetro
`URL(URL context, String spec)`

- Incluyendo un manejador de protocolo que conoce cómo comunicarse con el servidor
`URL(URL context, String host ,int port, String file, URLStreamHandler handler)`
`URL(URL context, String spec, URLStreamHandler handler)`

**Analizar**
Se puede descomponer `URL` con los métodos
- **getProtocol()**: Protoolo
- **getHost()**: Host
- **getPort()**: Puerto, si no está especificado -1
- **getDefaultPort()**: Puerto por defecto, si no lo tiene -1
- **getFile()** Fichero de URL, cadena vacía si no xiste
- **getRef()**  Referencia de URL, null si no la tiene
### 3.5. Leer y escribir a través de `URLConnection`

El objeto `URLConnection` se puede usar para leer y escribir hacia el recurso al que hace referencia el objeto `URL`

- **url.openConnection()** Devuelve objeto `URLConnection` que representa a la conexión con el recurso remoto al que se refiere la URL
- **url.openStream()** Abre conexión y devuelve un `InputStream` para la lectura de esa conexión. (Es como hacer `openConnection().getInputStream()`)

```java
    public static void main(String[] args) {
        String urlString = "http://www.google.es";
        String filePath = "archivo_local.txt";

        try {
            // Crear el objeto URL
            URL url = new URL(urlString);

            // Obtener una conexión con el recurso especificado
            URLConnection urlConnection = url.openConnection();

            // Abrir conexión con la URL
            BufferedReader in = new BufferedReader(new InputStreamReader(urlConnection.getInputStream()));
            BufferedWriter out = new BufferedWriter(new FileWriter(filePath));

            // Manejar los flujos necesarios para realizar la lectura
            String inputLine;
            while ((inputLine = in.readLine()) != null) {
	            System.out.println(inputLine)
                out.write(inputLine);
                out.newLine();
            }

            // Cerrar los flujos
            in.close();
            out.close();

            System.out.println("Archivo descargado y guardado en: " + filePath);
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```


**Con HttpUrlConnection** 

```java
            URL url = new URL(urlString);

            // Abrir conexión con la URL
            connection = (HttpURLConnection) url.openConnection();
            connection.setRequestMethod("GET");
((Map)connectionProperties).put("Param", "Esto va en el header de la request");

            // Verificar que la respuesta sea HTTP 200 OK
            int responseCode = connection.getResponseCode();
            System.out.println(connection.getHeaderField("LaRespuestaEnElHeader"))
            if (responseCode == HttpURLConnection.HTTP_OK) {
                reader = new BufferedReader(new InputStreamReader(connection.getInputStream()));

                // Manejar los flujos necesarios para realizar la lectura
                String inputLine;
                while ((inputLine = reader.readLine()) != null) {
                    System.out.println(inputLine);
                }
                
            } else {
                System.out.println("Error en la conexión, código de respuesta: " + responseCode);
            }
```

**Enviar algo en el body**

```java
        try {
            // Crear el objeto URL
            URL url = new URL(urlString);
            HttpURLConnection connection = (HttpURLConnection) url.openConnection();

            // Configurar la conexión
            connection.setRequestMethod("POST");
            connection.setRequestProperty("Content-Type", "application/json; utf-8");
            connection.setRequestProperty("Accept", "application/json");

            if (connectionProperties != null) {
                for (Map.Entry<String, String> entry : connectionProperties.entrySet()) {
                    connection.setRequestProperty(entry.getKey(), entry.getValue());
                }
            }

// doInput indica que se leeran datos en la conexion, por defecto esta a true
            connection.setDoOutput(true); // Indica que va a enviar datos a traves de la conexion (por defecto esta a false)

            // Escribir el JSON en el OutputStream
            try (OutputStream os = connection.getOutputStream()) {
                byte[] input = jsonString.getBytes(StandardCharsets.UTF_8);
                os.write(input, 0, input.length);
                os.flush();
            }

            // Leer la respuesta del servidor
            int responseCode = connection.getResponseCode(); // Aqui llamada HTTP
            System.out.println("Código de respuesta: " + responseCode);

            if (responseCode == HttpURLConnection.HTTP_OK) {
                BufferedReader in = new BufferedReader(new InputStreamReader(connection.getInputStream(), StandardCharsets.UTF_8));
                String inputLine;
                StringBuilder response = new StringBuilder();

                while ((inputLine = in.readLine()) != null) {
                    response.append(inputLine);
                }
                in.close();

                // Imprimir la respuesta del servidor
                System.out.println("Respuesta del servidor: " + response.toString());
            } else {
                System.out.println("Error en la conexión, código de respuesta: " + responseCode);
            }

            connection.disconnect();
```

Podría ser buena práctica llamar a `disconnect()` solo para indicar al gestor de conexiones que ya no la necesito, aunque este podrá reutilizarla. 

---

Como es obvio, la llamada HTTP se produce en el momento en el que se intenta leer algo con el `inputStream`, `getResponseCode` o lo que sea...

### 3.6. Trabajar con contenido de una URL

Métodos de utilidad
- **connect()** Establece conexión
- **getContentType()** Valor del campo de cabecera Content-Type
- **getContentLength()**
- **getLastModified()** Última fecha de modificación del recurso

## 4. Programación de aplicaciones cliente

### 4.1. Programación de cliente HTTP

**Con Sockets** 

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.io.OutputStreamWriter;
import java.io.PrintWriter;
import java.net.Socket;

public class SimpleHttpClient {
    public static void main(String[] args) {
        String host = "www.example.com"; // Cambia esto al host al que deseas conectarte
        int port = 80; // Puerto HTTP estándar

        try {
            // Conectar al servidor HTTP
            Socket socket = new Socket(host, port);
            System.out.println("Conectado a " + host + ":" + port);

            // Enviar la solicitud HTTP al servidor
            PrintWriter out = new PrintWriter(new OutputStreamWriter(socket.getOutputStream()), true);
            out.println("GET / HTTP/1.1");
            out.println("Host: " + host);
            out.println(); // Una línea en blanco indica el final de la solicitud HTTP

            // Leer la respuesta del servidor
            BufferedReader in = new BufferedReader(new InputStreamReader(socket.getInputStream()));
            String line;
            while ((line = in.readLine()) != null) {
                System.out.println(line);
            }

            // Cerrar la conexión
            socket.close();
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```

### 4.2. Bibliotecas para programar cliente FTP

Para programar clientes FTP se puede usar el paquete de la API de Apache `org.apache.commons.net.ftp` con las clases
- `FTP`: Funcionalidades básicas para implementar cliente FTP
- `FTPReplay`: Permite almacenar valores devueltos por el servidor como código de respuesta a las peticiones del cliente
- `FTPClient`: Encapsula la funcionalidad para almacenar y recuperar archivos de servidor FTP, encargándose de los detalles de bajo nivel para interaccionar con el servidor. Hereda de `SocketClient`
- `FTPClientConfig` Alternativa de configurar objetos `FTPClient`
- `FTPSClient`: FTP seguro sobre SSL

```xml
<dependency>
    <groupId>commons-net</groupId>
    <artifactId>commons-net</artifactId>
    <version>3.9.0</version>
</dependency>
```

### 4.3. Programación de cliente FTP

Se creará mediante la clase `FTPClient`

1. Realizar conexión de  cliente con servidor con método `connect(InetAddress host)`, abriendo socket conectado al host remoto en puerto por defecto
2. Comprobar conexión `getReplyCode()` con código de respuesta indicativo de éxito o fracaso
3. Validar usuario. Con el método **login** `login(String usuario, String password)`
4. Realizar operaciones contra el servidor como listar los ficheros disponibles `listNames()` o recuperar el contenido de un fichero remoto con `retrieveFile(String rutaRemota, OutputStream ficheroLocal)` y transferirlo al equipo local para escribirlo en el fichero local
5. Desconexión con `disconnect()` o `logout()`

Pueden generarse `SocketException` al superar tiempo de espera (timeout) en conexión al servidor o  `IOException` si no se tiene acceso al fichero. 

```java
import org.apache.commons.net.ftp.FTPClient;
import java.io.IOException;

public class SimpleFTPClient {
    public static void main(String[] args) {
        String server = "ftp.example.com";
        int port = 21;
        String user = "username";
        String password = "password";

        FTPClient ftpClient = new FTPClient();
        
        try {
            // Realizar la conexión con el servidor
            ftpClient.connect(server, port);
            int replyCode = ftpClient.getReplyCode();
            if (!FTPClient.isPositiveCompletion(replyCode)) {
                System.out.println("No se pudo conectar al servidor FTP");
                return;
            }

            // Validar usuario
            boolean success = ftpClient.login(user, password);
            if (!success) {
                System.out.println("Inicio de sesión fallido");
                return;
            }

            // Listar archivos en la carpeta remota
            String[] files = ftpClient.listNames();
            System.out.println("Archivos en la carpeta remota:");
            for (String file : files) {
                System.out.println(file);
            }

            // Desconexión del servidor
            ftpClient.logout();
            ftpClient.disconnect();
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```


### 4.4. Programación de cliente Telnet


Servidor escucha en el puerto 23. Funcionamiento en modo texto.
Es inseguro. En su lugar se usa SSH.
Se puede también con el API de Apache gracias a la clase `TelnetClient`

- **Clase TelnetClient.** Permite implementar un terminal virtual para el protocolo Telnet. Hereda de la clase SocketClient.
    - El método `connect() `realiza la conexión al servidor .
    - Los métodos `getInputStream()` y `TelnetClient.getOutputStream()` permiten a través de objetos `InputStream()` y `OutputStream()` enviar y recibir datos a través de la conexión Telnet.
    - El método `disconnect()` cierra la conexión al servidor, así como los flujos de entrada y salida y el socket abiertos.

```java
public static void main(String[] args) throws IOException {
    TelnetClient telnet = new TelnetClient();
    telnet.connect("rainmaker.wunderground.com");


    StringBuilder wholeBuffer = new StringBuilder();
    Expect expect = new ExpectBuilder()
            .withOutput(telnet.getOutputStream())
            .withInputs(telnet.getInputStream())
            .withEchoOutput(wholeBuffer)
            .withEchoInput(wholeBuffer)
            .withExceptionOnFailure()
            .build();

    expect.expect(contains("Press Return to continue"));
    expect.sendLine();
    expect.expect(contains("forecast city code--"));
    expect.sendLine("SAN");
    expect.expect(contains("X to exit:"));
    expect.sendLine();

    String response = wholeBuffer.toString();
    System.out.println(response);

    expect.close();
}
```

### 4.5. Programación de cliente SMT

**Basado en sockets**

import java.net.*;
import java.io.*;

class smtpCliente {
    public static void main( String args[] ) {
        Socket s = null;
        DataInputStream sIn = null;
        DataOutputStream sOut = null;

        // Abrimos una conexión con breogan en el puerto 25
        // que es el correspondiente al protocolo smtp, e intentamos
        // abrir los streams de entrada y salida
        try {
            s = new Socket( "breogan",25 );
            sIn = new DataInputStream( s.getInputStream() );
            sOut = new DataOutputStream( s.getOutputStream() );
        } catch( UnknownHostException e ) {
            System.out.println( "No conozco el host" );
        } catch( IOException e ) {
            System.out.println( e );
            }

        // Si todo está inicializado correctamente, vamos a escribir
        // algunos datos en el canal de salida que se ha establecido
        // con el puerto del protocolo smtp del servidor
        if( s != null && sIn != null && sOut != null )
            {
            try {
                // Tenemos que respetar la especificación SMTP dada en
                // RFC1822/3, de forma que lo que va en mayúsculas
                // antes de los dos puntos tiene un significado especial
                // en el protocolo
                sOut.writeBytes( "MAIL From: froufe@arrakis.es\n" );
                sOut.writeBytes( "RCPT To: froufe@arrakis.es\n" );
                sOut.writeBytes( "DATA\n" );
                sOut.writeBytes( "From: froufe@arrakis.es\n" );
                sOut.writeBytes( "Subject: Pruebas\n" );
                // Ahora el cuerpo del mensaje
                sOut.writeBytes( "Hola, desde el Tutorial de Java\n" );
                sOut.writeBytes( "\n.\n" );

                // Nos quedamos a la espera de recibir el "Ok" del
                // servidor para saber que ha recibido el mensaje
                // correctamente, momento en el cual cortamos
                String respuesta;
                while( ( respuesta = sIn.readLine() ) != null )
                    {
                    System.out.println( "Servidor: "+respuesta );
                    if( respuesta.indexOf( "Ok" ) != -1 )
                        break;
                    }

                // Cerramos todo lo que hemos abierto
                sOut.close();
                sIn.close();
                s.close();
              } catch( UnknownHostException e ) {
                System.out.println( "Intentando conectar: "+e );
            } catch( IOException e ) {
                System.out.println( e );
                }
            }
        }
    }


**Con la API JavaMail**

```xml
<dependency>
    <groupId>javax.mail</groupId>
    <artifactId>javax.mail-api</artifactId>
    <version>1.6.2</version>
</dependency>
```

Tenemos 

Clase `Session`: Sesión de correo. Propiedades que usa `javax.mail` para el correo
- `getDefaultIntance()`: Sesión por defecto si no fue configurada. Debe pasarse parámetro con protocolo, servidor smtp, puerto para socket de sesión y tipo, usuario, puerto smtp
Clase `Message`: Modela mensaje de correo electrónico
- `setFrom()`: Atributo from del mensaje, dirección del emisor
- `setRecipients()`: Tipo y direcciones de destinatarios
- `setSubject()`: Asunto del mensaje
- `setText()`: Texto o cuerpo
Clase `Transport`: Transporte de mensaje. Herencia de la clase `Service` para funcionalidades de mensajería como conexión, desconexión, transporte, almacenamiento
- `send()` Envio del mensaje a direcciones indicadas.


```java
Properties prop = new Properties();
prop.put("mail.smtp.host", host);
prop.put("mail.smtp.port", port);
prop.put("mail.smtp.auth", "true");
            
Session session = Session.getInstance(prop,
            new Authenticator() {
                @Override
                protected PasswordAuthentication getPasswordAuthentication() {
                    return new PasswordAuthentication(from, pass);
                }
            });
            
MimeMessage message = new MimeMessage(session);
message.setFrom(new InternetAddress(from));
message.setRecipients(Message.RecipientType.TO, InternetAddress.parse(to));
message.setSubject(subject);

Multipart multipart = new MimeMultipart();
MimeBodyPart messageBodyPart = new MimeBodyPart();
if(body != null) {
     messageBodyPart.setText(body);
     messageBodyPart.setContent(body, "text/html; charset=utf-8");
    multipart.addBodyPart(messageBodyPart);
}

if (fileList != null && !fileList.isEmpty()) {
    for(File file : fileList) {
        BodyPart mbp = new MimeBodyPart();
        FileDataSource fds = new FileDataSource(file.getAbsolutePath());
        mbp.setDataHandler(new DataHandler(fds));
        mbp.setFileName(file.getName());
	    multipart.addBodyPart(mbp);
         }
 }
message.setContent(multipart);

Transport.send(message)
```


Hoy día se puede hacer más fácil por ejemplo en Spring Boot

```xml
<dependency>
	<groupId>org.springframework.boot</groupId>
	<artifactId>spring-boot-starter-mail</artifactId>
</dependency>
```

```java
var javaMailSender = new JavaMailSenderImpl();
javaMailSender.setHost(host);
javaMailSender.setPort(port);
javaMailSender.setUsername(from);
javaMailSender.setPassword(pass);

MimeMessage message = javaMailSender.createMimeMessage();

MimeMessageHelper helper = new MimeMessageHelper(message, true);
helper.setFrom(mailCredentials.user());
helper.setTo(to);
helper.setSubject(subject);
helper.setText(body, true);

if (fileList != null && !fileList.isEmpty()) {
	for (File file : fileList) {
		helper.addAttachment(file.getName(), file);
	}
}

javaMailSender.send(message);
```

## 5. Programación de servidores

El servidor debe:
- Atender a multitud de peticiones que pueden ser concurrentes en el tiempo -> Programación usando Threads
- Optimizar el tiempo de respuesta -> Monitorización de tiempos de proceso y transmisión del servidor

La clase `ServerSocket` es la que se usa para crear  servidores.

### 5.1. Programación de servidor HTTP

### Estructura del protocolo HTTP

>Línea inicial
>Líneas de cabecera
>Un salto de línea ("\\n")
>Cuerpo

### Request al servidor

La línea inicial contiene  el método HTTP usado, el fichero y la versión del protocolo. Por ejemplo para http://www.midominio.com/users

```
GET users HTTP/1.1
```

### Response del servidor

La línea inicial contiene la versión, el código de respuesta y el valor.

Por ejemplo:
```
HTTP/1.1 200 OK
HTTP/1.1 404 Not found
```

Las líneas de cabecera envían información sobre el objeto que va a recibir como cuerpo. Tienen formato Etiqueta: valor
- Content-Type: Indica al cliente el tipo de contenido, tipo de medio (MIME) del objeto que se enviará como cuerpo. Los más usados
	- text/html: HTML
	- text/plain: Texto sin formato
	- application/json
	- application/xml
	- image/gif
	- image/jpeg
	- application/pdf
	- multipart/form-data: Formularios HTMl. Archivos y datos binarios
```
Content-Type: text/html
Content-Type: text/html;charset=UTF-8
Content-Type: application/pdf
```

- Content-Length: Tamaño del objeto que se envía como cuerpo del mensaje de respuesta. 
```
Content-Length: 1024
```

- Date: Es opcional. Pero muchos servidores HTTP usan esa cabecera para indicar el inicio de la transmisión del cuerpo del mensaje de respuesta. Se suele obtener justo antes de enviar la línea de separación. El formato es obligatorio:
```
Date: Sat, 25 Feb 2012 12:41:18 GMT
```

```java
import java.util.Date;
import java.util.Locale;
import java.util.TimeZone;
import java.text.DateFormat;
import java.text.SimpleDateFormat;
String getDateValue(){
   DateFormat df = new SimpleDateFormat(
   "EEE, d MMM yyyy HH:mm:ss z", Locale.ENGLISH);
   df.setTimeZone(TimeZone.getTimeZone("GMT"));
   return df.format(new Date());
}
```


Todo junto:

```
HTTP/1.1 200 OK
Content-Type: text/html;chatset=UTF-8
Content-Length: 1024
Date: Sat, 25 Feb 2012 12:41:18 GMT

<head>
	<title>Hello</title>
</head>
<body>
	<h1>Hello World</h1>
</body>
```

### 5.2. Creación del servidor implementando comunicaciones simultáneas

Para crear un servidor HTTP o servidor web, el esquema básico a seguir será:

- Crear un `ServerSocket` asociado al puerto 80 (puerto por defecto para el protocolo HTTP).
- Esperar peticiones del cliente.
- Aceptar la petición del cliente.
- Procesar petición (intercambio de mensajes según protocolo + transmisión de datos).
- Cerrar socket del cliente.

**Ejemplo**

- Al poner en tu navegador http://locahost:8066, te dará la bienvenida.
- Al poner en tu navegador http://localhost:8066/quijote, mostrará un párrafo de el Quijote.
- Al poner en tu navegador una URL diferente a las anteriores, como por ejemplo http://localhost:8066/a, mostrara un mensaje de error.

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.io.OutputStream;
import java.net.ServerSocket;
import java.net.Socket;

public class SimpleWebServer {
    public static void main(String[] args) {
        int portNumber = 8066; // Puerto 8066 como se especifica en tus requisitos

        try (ServerSocket serverSocket = new ServerSocket(portNumber)) {
            System.out.println("Servidor web iniciado en el puerto " + portNumber);

            while (true) {
                Socket clientSocket = serverSocket.accept();
                System.out.println("Conexión entrante desde " + clientSocket.getInetAddress());

                // Procesar la solicitud en un nuevo hilo para permitir múltiples conexiones
                new Thread(() -> {
                    try {
                        handleRequest(clientSocket);
                    } catch (IOException e) {
                        e.printStackTrace();
                    }
                }).start();
            }
        } catch (IOException e) {
            e.printStackTrace();
        }
    }

    private static void handleRequest(Socket clientSocket) throws IOException {
        BufferedReader input = new BufferedReader(new InputStreamReader(clientSocket.getInputStream()));
        OutputStream output = clientSocket.getOutputStream();

        String requestLine = input.readLine();
        System.out.println("Petición recibida: " + requestLine);

        String[] requestParts = requestLine.split(" ");
        String method = requestParts[0];
        String url = requestParts[1];

        String response;
        if (url.equals("/") || url.equals("/index")) {
            response = "HTTP/1.1 200 OK\r\nContent-Type: text/html\r\n\r\n<h1>Bienvenido</h1>";
        } else if (url.equals("/quijote")) {
            response = "HTTP/1.1 200 OK\r\nContent-Type: text/plain\r\n\r\nAquí iría un párrafo de El Quijote.";
        } else {
            response = "HTTP/1.1 404 Not Found\r\nContent-Type: text/html\r\n\r\n<h1>Error 404: Not Found</h1>";
        }

        output.write(response.getBytes());
        output.flush();

        input.close();
        output.close();
        clientSocket.close();
    }
}
```

### 5.3. Ejemplo de monitorización de tiempo de transmisión

```java
import java.io.*;
import java.net.*;

public class TiempoTransmisionHTTP {
    public static void main(String[] args) {
        String urlString = "http://www.ejemplo.com/archivo.html"; // Cambia esto por la URL del recurso que quieres medir
        try {
            URL url = new URL(urlString);
            URLConnection conn = url.openConnection();
            
            // Obtener la fecha de inicio de transmisión del servidor
            long inicioTransmision = conn.getDate();
            if (inicioTransmision == 0) {
                System.out.println("No se pudo obtener la fecha de inicio de transmisión del servidor.");
                return;
            }
            
            // Descargar el recurso para simular la transmisión
            InputStream in = conn.getInputStream();
            ByteArrayOutputStream out = new ByteArrayOutputStream();
            byte[] buffer = new byte[1024];
            int length;
            while ((length = in.read(buffer)) != -1) {
                out.write(buffer, 0, length);
            }
            out.close();
            in.close();
            
            // Calcular el tiempo de transmisión
            long finTransmision = System.currentTimeMillis();
            long tiempoTransmision = finTransmision - inicioTransmision;
            
            System.out.println("Tiempo de transmisión: " + tiempoTransmision + " milisegundos");
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```
