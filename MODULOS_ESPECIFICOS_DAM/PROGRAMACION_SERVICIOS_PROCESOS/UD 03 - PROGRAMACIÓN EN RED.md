
## 1. Comunicaciones en red

### 1.1. Conceptos básicos

#### Arquitectura de red
La **arquitectura de red** se divide en niveles o capas para reducir la complejidad de su diseño. Cada uno de estos niveles tiene asociados uno o varios protocolos que definen las reglas de comunicación de la capa correspondiente. 

Se llama **pila de protocolos** o **jerarquía de protocolos** a la arquitectura de red que usa unos protocolos determinados.

Si imaginamos una arquitectura de red de cuatro niveles: Dos ordenadores tendrán  implementada la arquitectura. Cada nivel tiene implementados sus protocolos; puede decirse que las comunicaciones entre niveles iguales se hace a través de los protocolos correspondientes. Pero el flujo real de información con los datos que se quieren transmitir va de un ordenador a otro pasando por cada uno de los niveles. Es decir, los datos no se transfieren directamente de una capa a otra sino que cada capa pasa los datos e información de control a la capa adyacente, después pasa al medio de transmisión adecuado y, posteriormente, sucede lo mismo pero en sentido contrario en el otro ordenador.

Cada capa tiene unos servicios asignados y cada una tiene unas funciones, ocupándose solo de los datos e información de control que necesite según el protocolo utilizado.

Las capaz adyacentes tienen lo que se denomina **interfaz**, se definen las operaciones que la capa inferior ofrece a la superior. Es importante definir interfaces claras entre niveles.

Reglas:
- Cada nivel solo se comunique con el nivel superior o inferior
- Cada nivel inferior proporcione servicios al nivel superior

Las arquitecturas en capas facilitan compatibilidades de software y de hardware, modificaciones futuras, etc. 

#### Protocolo de comunicación
**Protocolo de comunicaciones**: Conjunto de reglas normalizadas para representación, señalización, autenticación y detección de errores necesario para enviar información a través de un canal de comunicación.
### 1.1.1. Modelo OSI. (Capas)

A principios de los 80 se produce un gran crecimiento en cantidad y tamaño de las redes, muchas empresas tomaron conciencia de las ventajas de usar tecnologías de conexión. En esta expansión, surgieron dificultades para intercambiar información. 

ISO investigó los modelos de conexión existentes para encontrar un conjunto de reglas aplicables de forma general a todas las redes. Con base a eso, se desarrolló un modelo de red (modelo de referencia OSI), 

El **Modelo OSI** (Open System Interconnection, Interconexión de Sistemas Abiertos) es el modelo de red creado por ISO en 1984. Define un marco de referencia para la definición de arquitecturas de interconexión en sistemas de comunicaciones.

Simplifica las actividades de red porque agrupa los procesos de comunicación en siete capas que realizan tareas diferentes. 

Cualquier sistema en red puede ser fraccionado de cara a analizar la comunicación, aislar problemas y resolver incidencias.

Los siete niveles OSI son:

| Capa | Nombre                           | Funciones                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| ---- | -------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 1    | Capa física o nivel físico.      | **Topología de red** y conexiones globales de la computadora hacia la red (medio físico y forma de transmitir información). <br><br>Conexiones físicas, incluyendo el cableado y los componentes necesarios para transmitir la señal.                                                                                                                                                                                                       |
| 2    | Capa o nivel de enlace de datos. | **Direccionamiento físico**, del acceso al medio, de detección de errores, de distribución ordenada de tramas y de control del flujo.<br><br>Empaqueta los datos para transmitirlos a través de la capa física. El direccionamiento físico se define utilizando direcciones MAC. Se encarga del acceso al medio, el control de enlace lógico o LLC, de la detección de errores de transmisión...                                            |
| 3    | Capa o nivel de red.             | **Enrutamiento** entre una o más redes. Hacer que los datos lleguen de origen a destino aunque no estén conectados directamente.<br><br>Separa los datos en paquetes, determina la ruta que tomaran los datos y define el direccionamiento.                                                                                                                                                                                                 |
| 4    | Capa o nivel de transporte.      | Efectuar el **transporte de datos** de la máquina origen a la de destino, independizándolo de la red física que se use. <br><br>Se encarga de que los paquetes de datos tengan una secuencia adecuada y de controlar los errores.                                                                                                                                                                                                           |
| 5    | Capa o nivel de sesión.          | **Mantiene y controla el enlace entre los dos extremos de la comunicación.** que están transmitiendo datos. Asegura que la misma pueda efectuarse para las operaciones definidas de principio a fin, reanudándolas en caso de interrupción.                                                                                                                                                                                                 |
| 6    | Capa o nivel de presentación.    | **Representación de la información**. Aunque los equipos tengan diferentes representaciones internas, los datos lleguen de forma reconocible. <br><br>Es la primera en trabajar más el contenido que el cómo se establece la comunicación. Se trata semántica, síntaxis de datos transmitidos. Cifrar datos y comprimirlos. <br>Determina el formato de las comunicaciones así como adaptar la información al protocolo que se este usando. |
| 7    | Capa o nivel de aplicación.      | Permite que las aplicaciones accedan a los servicios de las demás capas.<br><br>Define los protocolos que utilizan cada una de la aplicaciones para poder ser utilizadas en red e intercambiar datos. <br>Hay tantos protocolos como aplicaciones distintas; su número crece sin parar.                                                                                                                                                     |

Relacionadas con el **hardware**: Capas 1, 2 y 3
Relacionadas con el **software**: Capas 5, 6 y 7

##### Resumencillo

>**Capa 1 - Capa física**:  Agrupa lo físico relacionado con la interconexión de sistemas en red. Cables de datos, de fibra, conectores, terminaciones... 
Problemas: Cables correctamente introducido, cables no están sueltos, no están doblados, bien crimpados, tarjeta de red correcta, etc.
>
**Capa 2 - Capa de enlace de datos**: Transferencia de datos entre dos sistemas directamente o entre ambos sistemas a través de una red. Conmutadores, switches, bridges, etc. Estándares 802.3 (Ethernet) 802.11 (Wi-Fi)
Subcapa LLC (Control de Enlace Lógico): De eléctrico a binario
Subcapa MAC (Control de Acceso al Medio): Paquetes de datos de una tarjeta o interfaz de red de un sistema a otro de un sistema.
Problemas: Además de transmitir, corrige problemas cuando puede. Debido a la capa física por interferencias de radiofrecuencia, baja ASNR,... 
>
**Capa 3 - Capa de red**: Decidir el camino físico por el que irán los datos
Enrutamiento de los routers (switches de capa 3). Protocolo OSPF (ruta más rápida que deben seguir los datos para alcanzar su destino)
Direcciones IP forman parte de esta capa. Paquetes pasan de unos a otros enrutadores identificando sus extremos por la IP.
Problemas: Paquetes tardan mucho (host o nodos no enrutados debidamente)
>
**Capa 4 - Capa de transporte**: Controla la transmisión de los datos.  Coordina el tránsito e intercambio de datos (velocidad, cantidad de datos, destino, puertos, respuesta al llegar la información). Define puertos a utilizar. 
Protocolo TCP
Protocolo UDP
Problemas: Paquete no alcanza el destino por puerto no abierto
>
--Con IP y puertos puede crearse un socket y establecer sesiones entre sistemas, dispositivos, aplicaciones...
>
>
**Capa 5 - Capa de sesión**: Establece diálogo entre los sistemas que intercambian datos. Capacidad del sistema de establecer o no comunicación bidireccional. 
Protocolo NetBIOS, RPC, PPTP, PAP.
>
**Capa 6 - Capa de presentación**: Presenta los datos con cierto formato para que sean visibles para la aplicación en la que se mostrará. 
Encriptado y cifrado / Desencriptado de datos... 
>
**Capa 7 - Capa de aplicación**: Comunicación entre la aplicación y la red
Protocolos HTTPS, DNS, FTP, SMTP.
Navegadores web, aplicaciones que hacen uso de la red...
>

### 1.1.2. Modelo TCP/IP. (Capas)

En 1969, la agencia ARPA (Advanced Research Projects Agency) del Departamento de Defensa de los Estados Unidos inició un proyecto de ineterconexión de ordenadores mediante redes telefónicas. 

La red debía poder resistir la destrucción de parte de su infraestructura de forma que dos nodos pudiesen seguir comunicados siempre que hubiese alguna ruta que los uniese.  Esto se consiguió en 1972 creando una red de conmutación de paquetes llamada **ARPAnet**. La conmutación de paquetes unida al uso de topologías malladas por múltiples líneas punto a punto dio lugar a una red altamente fiable y robustas.

Se probaron más formas de transmisión de datos (enlaces radio y satélite). Los protocolos existentes tenían problemas para interoperar con estas redes por lo que se diseñó un nuevo conjunto o pila de protocolos (nueva arquitectura de red) y se denominó **TCP/IP** (protocolo de control de transmisión/protocolo de internet), nombre que provenía de los dos protocolos más importantes que componían la pila. A la nueva red de fusión de ARPA net con redes basadas en otras tecnologías de transmisión se llama Internet.

TCP/IP es más pragmática que OSI. Fue a la inversa que OSI. No hubo estudio y definición de protocolos sino que primero se hicieron los protocolos y luego se definió el modelo como descripción de los ya existentes.

OSI se usa para describir arquitecturas como TCP/IP. TCP/IP solo describe la suya propia. 


TCP/IP es la arquitectura más usada, base de las comunicaciones de Internet y sistemas operativos modernos.

Está formada por cuatro niveles:

| Capa | Nombre                 | Funciones                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           | Resumen                          |
| ---- | ---------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------- |
| 1    | **Capa host-enlace**   | Permite comunicar el ordenador con el medio que conecta el equipo a la red. Para ello convierte la información en impulsos físicos y permite la conexión entre los ordenadores de la red. **Direccionamiento físico** con direcciones MAC                                                                                                                                                                                                                                                                                                                                                                                                           | MAC<br>Señal<br>Trans. binaria   |
| 2    | **Capa de red**        | Eje de la arquitectura TCP/IP. Permite que los equipos envíen paquetes en cualquier red y viajen de forma independiente a su destino (que puede estar en una red diferente). Los paquetes incluso pueden llegar en orden diferente al que se enviaron. Las capas superiores los reordenarán si se necesita. Se define un formato de paquete y protocolo oficial llamado IP. <br><br>La capa de red entrega paquetes a su destino. Decide qué camino tienen que seguir los paquetes (encaminamiento) y evitar al congestión. <br><br>**Direccionamiento lógico** o direccionamiento por IP, ya que se envía un mensaje a la dirección IP de destino. | Direccionamiento de red          |
| 3    | **Capa de transporte** | Permite que los equipos lleven a cabo una conexión. Se define el protocolo **TCP** (Transmission Control Protocol) y protocolo **UDP** (User Datagram Protocol). El protocolo TCP es orientado a conexión y fiable. El protocolo UDP es no orientado a conexión y no fiable. <br><br>Se realiza **direccionamiento por puertos**. Gracias a la capa de red, los paquetes viajan del equipo origen al de destino y esta capa se encarga de que la información llegue a la aplicación adecuada por un puerto determinado.                                                                                                                             | Gestión de puertos<br>TCP<br>UDP |
| 4    | **Capa de aplicación** | Engloba las funcionalidades de las capas de sesión, presentación y aplicación del modelo OSI. Incluye todos los protocolos de alto nivel relacionados con las aplicaciones (HTTP, FTP, TELNET)                                                                                                                                                                                                                                                                                                                                                                                                                                                      | HTTP, FTP, POP3, SSH             |

En algunos casos la capa de acceso a red se divide en capa de hardware o física y capa de enlace de datos (en este caso la arquitectura TCP/IP tendría cinco niveles en vez de cuatro)

### 1.1.3. Conexiones TCP/UDP

La capa de transporte establece reglas para la conexión entre dos dispositivos.

Desde la capa de red, la información se recibe en forma de paquetes desordenados. La capa de transporte debe manejarlos y obtener un único **flujo de datos**. (La capa de red no se preocupa ni del orden, ni de los errores; es aquí donde se mirará eso)

Es el encargado de transferencia libre de errores entre emisor y receptor y de mantener el flujo de red. Proporcionar transporte de datos confiable de la capa origen a destino, independientemente de la red física.

Dos tipos:
- **TCP**: Orientado a conexión. Flujo de bytes originado en una máquina se entrada sin errores en el destino. El flujo entrante de bytes **se fragmenta en mensajes** y pasa cada uno a la capa de red. 
  El proceso TCP receptor **reensambla los mensajes recibidos** para formar el flujo de salida. TCP **también se encarga del control de flujo** para asegurar que un emisor rápido no pueda saturar a un receptor lento. 

- **UDP**: Protocolo sin conexión, para aplicaciones que no necesitan asignación de secuencia ni control de flujo TCP y desean usar los suyos propios. También para consultas de petición y respuesta cliente-servidor y en aplicaciones donde la velocidad es más importante que la entrega precisa (transmisiones de voz o de vídeo; streamings...)
### 1.1.4. Puerto de comunicación

En la capa de red se consigue que vaya de un equipo origen a un destino a través de la IP.
Debe saberse en la comunicación entre aplicaciones, a qué aplicación se conectará. 

Se definen **direcciones de transporte** en la que **los procesos están a la escucha de solicitudes de conexión** en unos puntos terminales llamados **puertos**.

La autoridad encargada de asignar los puertos que tienen algún tipo de uso a aplicaciones particulares es la IANA (Internet Assigned Numbers Authority). Hay tres rangos de puertos establecidos:

- **Puertos conocidos \[0, 1023]**: Puertos reservados a aplicaciones de uso estándar como 21 - FTP, 22 - SSH....
- **Puertos registrados \[1024, 49151]**: Puertos asignados por IANA a servicios específicos o aplicaciones. Pueden ser usados por los usuarios libremente, sin ningún problema.
- **Puertos dinámicos \[49152, 65535]**: Puertos no puede ser registrado. Su uso es para conexiones temporales.  

Una aplicación que usa un puerto debe usar puertos en el rango 1024-49151.

### 1.1.5. Nombres en internet

Los equipos informáticos se comunican por dirección IP, pero es más fácil usar dominios la ser más fáciles de recordar y al poder cambiar la máquina en la que se alojan sin cambiar las referencias a él.

El DNS (Sistema de Resolución de Nombres) hace que se disponga de uno o más servidores encargados de resolver los nombres de los dominios pertenecientes a su ámbito, consiguiendo la centralización necesaria para la sincronización de los equipos, un sistema jerárquico que permite una administración focalizada y descentralizada y un mecanismo de resolución eficiente. 

Es posible comunicarse por dirección IP o por entrada DNS. Si se pone entrada DNS, el equipo resuelve su dirección IP a partir del servidor DNS que use. 

#### Domain Name System (DNS)

Es un sistema de nombres jerárquico y distribuido para efectuar la traducción (resolución) entre nombres de dominio y direcciones IP.

#### Funcionamiento del DNS

El DNS tiene una estructura jerárquica en árbol en el que cada rama constituye un dominio de internet. Funciona delegando la responsabilidad de resolución mediante la designación de servidores de nombres autorizados (servidores DNS) para cada dominio (establecimiento de zonas).
<small>Similar a la organización de los sistemas de ficheros en árboles jerárquicos. En él el nombre absoluto del fichero es el formado por los distintos directorios recorridos hasta encontrar el fichero</small>

#### El nombre de dominio (FQDN)

El nombre completo del equipo (FQDN, Fully Qualified Domain Name)  es el resultante de recorrer todos los dominios por los que pasamos. (que incluye el nombre de la computadora y el nombre del dominio asociado a ese equipo).
Suele tener dos o más partes ("etiquetas") separadas por puntos. La jerarquía va de derecha a izquierda (www.example.com), teniendo el TLD, el subdominio (puede tener hasta 127 niveles y cada etiqueta hasta 63 caracteres, aunque el dominio no puede exceder los 255 caracteres). La parte final es el nombre de la máquina. `es.wikipedia.org` 

#### Los servidores de nombres autorizados (Servidores primarios)

Son servidores que tienen asignada la autoridad de resolución de nombres y gestionan la base de datos de zona

**Root**: Cima de la jerarquía. Representado por "." No se muestra en los DNS. Es el punto de partida para la resolución.

**Primer nivel, Dominios de nivel superior (TLD)**: Nombres de los nodos ya establecidos por divisiones geográficas (`.es`, `.uk`) u organizativas (`.com`, para empresas, `.int` para organizaciones de tratados internacionales, `.edu` para educativas, `.gov` del gobierno de EEUU, `.mil` del ejército de EEUU, `.name` nombres de personas, `.info` proveedores de información, `.web` servicios web ). Como es lógico, manejan las consultas sobre nombres de su TLD específico.

Cada rama recibe el nombre de dominio. La asignación de nombres de rama del árbol de primer nivel se delega en un responsable (empresa pública REDES) que a su vez delega la autoridad de resolución de los nombres en otras corporaciones. 

Hay dominios de segundo o tercer nivel (podrían existir más aunque no es habitual)

#### Servidores secundarios

Servidores que pueden resolver requerimientos de una zona, pero obtienen información de otro servidor.

Para garantizar la disponibilidad del servicio, existen varios servidores independientes que realizan el mismo servicio de forma que la autoridad de resolución de zona recae en un servidor pero este puede permitir que otros responsan a los requerimientos de los clientes. 

Los secundarios obtienen los datos del servidor primario mediante la "transferencia de zona" (traspaso de todos los pares dirección IP  nombre simbólico que gestiona el servidor). Cada vez que se modifica un dato del primario, debe transmitirse a los secundarios para el correcto funcionamiento del sistema. 
#### Servidores caché

Responden a peticiones de resolución consultando las peticiones almacenadas en memoria y si no se corresponde con ninguna de ellas, inician el proceso de resolución. Así, por ejemplo, se descargan los servidores raíz y estos solo participan una fracción pequeña de todas las solicitudes. Los servidores caché los resultados de consultas DNS durante un tiempo determinado en la configuración del registro del nombre de dominio en cuestión. También tienen incorporado el algoritmo recursivo para resolver nombres.

#### Proceso de resolución DNS
```
- Usuario escribe nombre de dominio en el navegador web
- Navegador hace consulta al servidor DNS local del sistema operativo (DNS resolver, DNS iterator, DNS resolutor). Si está en caché lo devuelve.
- Si el servidor DNS local no tiene registros en caché, este hace la consulta a/los servidor/es DNS que tiene configurados (el de su proveedor ICP o el del administrador de la red de la organización...)
- Si el DNS resolver no tiene registros en caché, le pregunta al servidor de nombres raíz. Este le da como respuesta la dirección de un servidor de primer nivel (TLD)
- El DNS resolver le pregunta al servidor TLD. Este le responde con la dirección del servidor de nombres autorizado para el nombre de dominio (le remite a servidores de la organización).
- Los servidores DNS autorizados guardan registros DNS de los nombres de dominio necesarios para la resolución. El administrador de red  podría haber puesto tantas zonas como considere oportuno. La operación se repite de forma iterativa hasta recibir respuesta autorizada.
- El DNS resolver obtiene el registro y lo almacena en su caché local para que, si alguien más busca el sitio, la información ya esté allí. 
- El DNS resolver envía la información a la computadora.
```

#### Comentarios adicionales 

El protocolo DNS transporta las peticiones y respuestas entre cliente y servidor mediante UDP. Solo se usa TCP cuando se requieren respuestas largas o cuando se intercambia información entre servidores (transferencia de zona)

El DNS resolver puede hacer consultas no recursivas (recibe toda la información), recursivas (pregunta a uno que luego pregunta a otro en su nombre...) o iterativas (pregunta a uno que le remite a otro, que le remite a otro...)

A veces hay "registros pegamento" (glue records) para evitar dependencias circulares. En delegaciones algunos servidores se identifican por nombre. (Si el servidor autorizado de `example.org` es `ns1.example.org` deberia resolverse primero el  `example.org` del autorizado, por lo que se provee la dirección IP para `ns1.example.org` "pegada")

Los nombres de host y las direcciones IP no necesariamente deben tener relación uno a uno (varios host pueden ser de una única IP, alojamiento virtual; un único host puede resolverse en muchas IPs para tolerancia a fallos y distribución de la carga)

Registrar un dominio: Lo puede hacer cualquier persona o empresa en nic.es o por un agente registrador acreditado. 

#### Tipos de registro DNS

* Registro tipo A: Asociar nombre con IP
* Registro tipo CNAME: Alias entre dos registros (www.mec.es igual que ftp.mec.es)
* Registro MX: Indica donde está el servidor de correo electrónico. Se asocia a otro nombre y permite asignar prioridades (MX10 primer servidor, MX20 segundo...)

|Registro|Función|
|---|---|
|SOA|Inicio de autoridad. Fija los parámetros de la zona.|
|NS|Servidor de nombre. Nombre de un servidor autorizado para el dominio.|
|A|Dirección de anfitrión. Asigna a un nombre una dirección.|
|CNAME|Nombre canónico. Establece un alias para un nombre verdadero.|
|MX|Intercambio de correo. Especifica qué máquinas intercambian correo.|
|TXT|Texto arbitrario. Forma de añadir comentarios.|
|PTR|Puntero. Permite la conversión de una dirección a nombre.|
|HINFO|Descripción de la computadora. CPU y S.O.|
|WKS|Servicios públicos disponibles en la computadora.|

-----------

### 1.1.6. Modelos de comunicaciones

- El **modelo cliente/servidor** está compuesto por un servidor que ofrece una serie de servicios y unos clientes que acceden a dichos servicios a través de la red. (WWW: Servidor que aloja web y clientes que solicitan al servidor una web)

- **Sistema de Información Distribuido**: Conjunto de equipos que interactúan entre sí y pueden trabajar a la vez como cliente y servidor. Desde el punto de vista externo es igual que el cliente/servidor ya que el cliente ve al Sistema de Información Distribuido como una entidad. Internamente los equipos del sistema de información distribuido interactúan entre sí (como servidores y clientes de forma simultánea) para compartir información, recursos, realizar tareas...

## 2. Sockets 

Los **sockets** permiten la **comunicación entre procesos de diferentes equipos de una red**. 
**Un socket es un punto de información por el cual un proceso puede recibir o enviar información**

Otras definiciones:
- Definición: Un socket es un punto final de un enlace de comunicación de dos vías entre dos programas que se ejecutan a través de la red.
- El cliente y el servidor deben ponerse de acuerdo sobre el protocolo que utilizarán.

- **Orientado a conexión:** Establece un camino virtual entre servidor y cliente, fiable, sin pérdidas de información ni duplicados, la información llega en el mismo orden que se envía.
            
- **No orientado a conexión:** Envío de datagramas de tamaño fijo. No es fiable, puede haber pérdidas de información y duplicados, y la información puede llegar en distinto orden del que se envía. No se guarda ningún estado del cliente en el servidor, por ello, es más tolerante a fallos del sistema.

Es necesario tener claro qué tipo de socket se quiere crear (TCP o UDP).

El paquete `java.net` de Java proporciona las clases `Socket`, `ServerSocket`, `DatagramSocket` y `DatagramPacket` para estas cosillas.

--------

### Clase `Socket`

**Constructores**
–public Socket ()
–public Socket (InetAddress address, int port)
–public Socket (String host, int port)
–public Socket (InetAddress address, int port, InetAddress localAddr, int localPort)
–public Socket (String host, int port, InetAddress localAddr, int localPort)

- address / localAddr: dirección IP de la máquina remota / local.
- port / localPort: puerto de la máquina remota / local.
- host: nombre de la máquina remota
En el caso del primer constructor crea un socket sin conexión.


**Servicios de la clase Socket**

public InetAddress getInetAddress(): Devuelve la dirección IP de la máquina en la que estamos conectados.

public int getPort(): Devuelve el puerto de la máquina remota.

public void close():  Cierra el canal de comunicación.

public InputStream getInputStream(): Devuelve el canal de lectura del socket.

public OutputStream getOutputStream(): Devuelve el canal de escritura del socket.

Ademas JAVA proporciona dos llamadas para saber la @IP y puerto local (getLocalAddress() y getLocalPort())


--------
### Clase `ServerSocket`

**Constructores**:
public ServerSocket (int port)
public ServerSocket (int port, int backlog)
public ServerSocket (int port, int backlog, InetAddress bindAddr)

- port: puerto de la máquina servidora.
- backlog: tamaño de la cola de espera, en el primero es 50.
- bindAddr: dirección IP local que se hará pública mediante el bind.
El constructor ServerSocket se encarga de hacer el bind y el listen.

**Servicios de la clase ServerSocket**

public Socket accept(): Devuelve el socket resultado de aceptar una petición, para llevar a cabo la comunicación con el cliente.

public void close() Cierra el canal de comunicación.

public InetAddress getInetAddress(): Devuelve la dirección IP de la máquina local.

public int getLocalPort(): Devuelve el puerto de la máquina local


--------

### Comunicación cliente-servidor

- Para la transmisión de datos entre cliente y servidor se utilizarán las clases DataInputStream (recibir datos) y DataOutputStream (enviar datos)
- Estas clases disponen de métodos para leer y escribir datos en el socket:

–read/writeBoolean
–read/writeChar
–read/writeDouble, read/writeFloat, read/writeInt, read/writeLong, read/writeShort
–read/writeUTF (leer/escribir cadenas de caracteres)

- Para envíar los datos se utiliza el método flush() de la clase DataOutputStream.

--------------

### Clase DatagramSocket

**Constructores**:
public DatagramSocket ()
public DatagramSocket (int port)
public DatagramSocket (int port, InetAddress laddr)

- port: puerto de la máquina.
- laddr: dirección IP local que se hará pública mediante el bind.
- El constructor DatagramSocket se encarga de hacer el bind.
- El primer constructor coge un puerto libre.

**Servicios de la clase DatagramSocket**

public void connect(InetAddress address, int port): Conecta el socket a la máquina remota con la @IP address y puerto port.

public void close() Cierra el canal de comunicación.

public void disconnect(): Desconecta el socket.

public InetAddress getInetAddress(): Devuelve la @IP de la máquina remota.

public int getPort():

- Devuelve el puerto de la máquina remota.
- Tambien hay dos llamadas para saber la @IP y puerto local (getLocalAddress() y getLocalPort()).
- Servicios de la clase DatagramSocket

public void send(DatagramPacket p): Envía un datagrama a la máquina remota, por el socket asociado.

public void receive(DatagramPacket p): Recibe un datagrama de otra máquina, por el socket asociado.

-------

### Clase DatagramPacket

**Constructores:**
public DatagramPacket (byte[ ] buff, int length)
- Construye un DatagramPacket para recibir paquetes en el buffer buff, de longitud length
public DatagramPacket (byte[ ] buff, int length, InetAddress address, int port)
- Construye un DatagramPacket para envíar paquetes con datos del buffer buff, de longitud length, a la @IP address y el puerto port.

**Servicios**:

Para la actualización y consulta de los diferentes campos de un DatagramPacket disponemos de los siguientes métodos: set/getAddress, set/getData, set/getLength, set/getPort

-------

### 2.1.- Sockets TCP

- El **servidor** utiliza un **puerto por el que recibe las peticiones de los clientes**. **Habitualmente** un **puerto bajo** \[1 - 1023]
- Cuando el **cliente** hace la conexión con el servidor se crea un nuevo socket que es el **encargado de permitir el envío y recepción** de datos entre el cliente/servidor. El puerto se crea de forma **dinámica** y es un puerto alto \[49152-655335]. Así **el puerto por el que se reciben las conexiones cada libre** y **cada comunicación tiene su propio socket**.

¿La transmisión de datos HTTP es por el puerto 80?
La **petición** se realiza por el **puerto 80** pero **la transferencia de datos** se realiza por un **puerto superior.**

### 2.1.1 Servidor

- **Publicar puerto**: Con `ServerSocket`, indicando donde se reciben las conexiones. 

```java
ServerSocket serverSocket = new ServerSocket(puerto);
```

- **Esperar peticiones**. A la espera de que se conecte el cliente. Cuando se conecta el cliente, se crea el socket de cliente por donde se envían y reciben los datos.  (Lo suyo que lo haga en bucle para que el no finalice solo tras la llamada de un cliente)

```java
Socket clientSocket = serverSocket.accept();
```

- Envío y recepción de datos. Flujo stream de entrada y de salida

- Cierre de socket de cliente. 
```java
clientSocket = close();
```


**Ejemplo**
```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.io.OutputStream;
import java.net.ServerSocket;
import java.net.Socket;

public class SimpleServer {
    public static void main(String[] args) {
        int port = 8066; // Publicar puerto

        try (ServerSocket serverSocket = new ServerSocket(port)) {
            System.out.println("Servidor escuchando en el puerto " + port);

            while (true) {
                // Esperar peticiones
                Socket clientSocket = serverSocket.accept();
                System.out.println("Cliente conectado: " + clientSocket.getInetAddress());

                // Crear flujos de entrada y salida
                BufferedReader input = new BufferedReader(new InputStreamReader(clientSocket.getInputStream()));
                OutputStream output = clientSocket.getOutputStream();

                // Leer datos del cliente
                String request = input.readLine();
                System.out.println("Petición del cliente: " + request);

                // Procesar petición y enviar respuesta
                String response;
                if (request.equals("hola")) {
                    response = "Hola, cliente!";
                } else {
                    response = "Comando no reconocido.";
                }

                output.write((response + "\n").getBytes());
                output.flush();

                // Cerrar flujos y socket del cliente
                input.close();
                output.close();
                clientSocket.close();
            }
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```


### 2.1.2 Cliente

- **Conectarse con el servidor**. Mediante un objeto de la clase socket para conectarse con un servidor a un puerto específico. Una vez realizada la conexión se crea el socket donde se realiza la comunicación.

```java
Socket scoket = new Socket(host, puerto);
```

- **Envío y recepción de datos**. Flujo de entrada y de salida

- **Cierre del socket

```java
socket.close();
```

**Ejemplo**


```java
import java.io.*;
import java.net.*;

class Cliente {

    static final String host = "localhost";
    static final int puerto = 8066; // Puerto en el que está escuchando el servidor

    public Cliente() {
        try {
            // Me conecto al servidor en un determinado puerto
            Socket sCliente = new Socket(host, puerto);

            // Crear flujo de salida para enviar datos al servidor
            OutputStream output = sCliente.getOutputStream();
            PrintWriter writer = new PrintWriter(output, true);

            // Crear flujo de entrada para recibir datos del servidor
            InputStream input = sCliente.getInputStream();
            BufferedReader reader = new BufferedReader(new InputStreamReader(input));

            // Enviar una solicitud al servidor
            String request = "hola";
            writer.println(request);
            System.out.println("Enviado al servidor: " + request);

            // Leer la respuesta del servidor
            String response = reader.readLine();
            System.out.println("Respuesta del servidor: " + response);

            // Cierro los flujos y el socket
            writer.close();
            reader.close();
            sCliente.close();

        } catch (IOException e) {
            System.out.println(e.getMessage());
        }
    }

    public static void main(String[] args) {
        new Cliente();
    }
}
```

### 2.1.3 Ejemplos

**Servidor acepta tres clientes de forma secuencial (no concurrente) y les indica qué cliente son** 

```java
import java.io.DataOutputStream;
import java.io.IOException;
import java.io.OutputStream;
import java.net.*;

class Servidor {
    static final int puerto = 2000;

    public Servidor() {
        try {
            ServerSocket skServidor = new ServerSocket(puerto);

            System.out.println("Escucho el puerto " + puerto);
            for (int nCli = 0; nCli < 3; nCli++) {
                Socket sCliente = skServidor.accept();
                System.out.println("Sirvo al cliente " + nCli);
                OutputStream aux = sCliente.getOutputStream();
                DataOutputStream flujoSalida = new DataOutputStream(aux);
                flujoSalida.writeUTF("Hola cliente " + nCli);
                sCliente.close();
            }
            System.out.println("Ya se han atendido 3 peticiones de clientes.");
        } catch (IOException e) {
            System.out.println(e.getMessage());
        }
    }

    public static void main(String[] arg) {
        new Servidor();
    }
}
```


```java
import java.io.*;
import java.net.*;

class Cliente {
    static final String HOST = "localhost";
    static final int Puerto=2000;

    public Cliente( ) {
        try{
              Socket sCliente = new Socket( HOST , Puerto );
              InputStream aux = sCliente.getInputStream();
              DataInputStream flujoEntrada = new DataInputStream( aux);
              System.out.println( flujoEntrada.readUTF() );
              sCliente.close();
        } catch( Exception e ) {
              System.out.println( e.getMessage() );
        }
    }

    public static void main( String[] arg ) {
        new Cliente();
    }
}
Para co
```

###  2.2 Sockets UDP


En los **sockets UDP** no se crea una conexión. Simplemente se envían mensajes de forma individual y no se garantiza la recepción o envío de mensajes. 

Para utilizar sockets UDP en Java tenemos la clase `DatagramSocket` y para recibir o enviar los mensajes se utiliza clase `DatagramPacket`. 

Cuando se recibe o envía un paquete se hace con la siguiente información:
- mensaje
- longitud del mensaje
- equipo
- puerto.

#### 2.2.1 Receptor de mensajes UDP

- **Iniciar el socket en un puerto para recibir mensajes**
```
DatagramSocket datagramSocket = new DatagramSocket(puerto);
```

- **Recibir mensajes**
```
byte[] cadena = new byte[1000];
DatagramPacket datagramPacket = new DatagramPacket(cadena, cadena.length);
datagramSocket.receive(datagramPacket);
```

#### 2.2.2 Emisor de mensajes UDP

- Se inicializa `DatagramSocket`  y se crea un mensaje `DatagramPacket` indicando mensaje, longitud, equipo, puerto. 
```java
DatagramSocket dategramSocket = new DatagramSocket();
DatagramPacket mensaje = new DatagramPacket(mensaje, longitud, equipo, puerto);
```

(Dirección del equipo obtenida con `InetAddress equipo = InetAddres.getByName("loquesea")`)

- Una vez creado se envía con `send()` y se cierra el socket
```java
datagramSocket.send(mensaje);
datagramSocker.close()
```

#### 2.2.3 Ejemplos 

```java
mport java.net.*; 
import java.io.*; 

public class ReceptorUDP { 

  public static void main(String args [] ) { 
    // Sin argumentos 
    if (args.length != 0) { 
      System.err.println("Uso: java ReceptorUDP"); 
    } 
    else try{ 
      // Crea el  socket 
      DatagramSocket sSocket = new DatagramSocket(1500); 

      // Crea el espacio para los mensajes 
      byte [] cadena = new byte[1000] ; 
      DatagramPacket mensaje = new DatagramPacket(cadena, cadena.length); 

      System.out.println("Esperando mensajes..");
      while(true){
           // Recibe y muestra el mensaje 
           sSocket.receive(mensaje); 
           String datos=new String(mensaje.getData(),0,mensaje.getLength());
           System.out.println("	Mensaje Recibido: " +datos);
      }
    } catch(SocketException e) { 
      System.err.println("Socket: " + e.getMessage()); 
    } catch(IOException e) { 
      System.err.println("E/S: " + e.getMessage()); } 
  } 
}
```

```java
import java.net.*; 
import java.io.*; 

public class EmisorUDP { 

  public static void main(String args [] ) { 
    // Comprueba los argumentos
    if (args.length != 2) { 
      System.err.println("Uso: java EmisorUDP maquina mensaje"); 

    } 
    else try{ 
      // Crea el socket 
      DatagramSocket sSocket = new DatagramSocket(); 

      // Construye la dirección del socket del receptor 
      InetAddress maquina = InetAddress.getByName(args[0]); 
      int Puerto = 1500; 

      // Crea el mensaje
      byte [] cadena = args[1].getBytes(); 
      DatagramPacket mensaje = new DatagramPacket(cadena,args[1].length(), maquina, Puerto); 

      // Envía el mensaje 
      sSocket.send(mensaje); 

      // Cierra el socket 
      sSocket.close(); 
    } catch(UnknownHostException e) { 
      System.err.println("Desconocido: " + e.getMessage()); 
    } catch(SocketException e) { 
      System.err.println("Socket: " + e.getMessage()); 
    } catch(IOException e) { 
      System.err.println("E/S: " + e.getMessage()); 
    } 
  } 
}
```


```shell
javac ReceptorUDP.java
javac EmisorUDP.java

java ReceptorUDP
java EmisorUDP localhost hola
```

--------------



## 3. Aplicaciones cliente-servidor

### 3.1 Paradigma cliente/servidor

El modelo **cliente/servidor** es un paradigma por ser actualmente el más usado en las comunicaciones entre equipos. Ofrece gran flexibilidad, interoperabilidad y estabilidad para el acceso a recursos de forma centralizada. El término se acuñó en los 80.

Definición formal: Se trata de una arquitectura distribuida que permite a los usuarios finales obtener acceso a recursos de forma transparente en entornos multiplataforma. Los recursos suelen ser datos aunque podría ser acceso a dispositivos hardware, tiempo de procesamiento...

El modelo se compone de:

 **Cliente**: Proceso que permite interactuar con el usuario, realizar peticiones, enviarlas al servidor y mostrar datos al cliente. Es la interfaz que usa para interactuar con el servidor. (front-end). Sus funciones son:
- Interactuar con el usuario
- Procesar peticiones para ver si son válidas y evitar peticiones maliciosas al servidor
- Recibir resultados del servidor
- Formatear y mostrar resultados

**Servidor**: Proceso encargado de recibir y procesar peticiones de los clientes para permitir acceso a algún recurso (back-end). Sus funciones son:
- Aceptar peticiones de los clientes
- Procesar peticiones
- Formatear y enviar resultado a clientes
- Procesar la lógica de la aplicación y realizar validaciones de datos
- Asegurar consistencia de la información
- Evitar que las peticiones de los clientes interfieran entre sí
- Mantener seguridad del sistema. 

El servidor es una entidad que realiza unas tareas y las ofrece a los clientes.

Suelen usarse interfaces gráficas (cliente) y la administración de datos, seguridad, integridad, trabajo pesado lo realiza el servidor. Es, en definitiva, una extensión de la programación modular que divide la funcionalidad en dos módulos (más fácil desarrollo y mejor mantenimiento)

#### 3.1.1 Características básicas

- Combinación de cliente que interactúa con el usuario y servidor que interactúa con los recursos compartidos.
- Trabajo del procesamiento para el servidor; Interacción con el usuario para el cliente
- Relación entre procesos, pueden ejecutarse en uno o varios equipos distribuidos a lo largo de la red
- Relación de muchos a uno entre clientes y servidor
- Los clientes son procesos activos que realizan peticiones de servicios a los servidores (procesos pasivos que están a la espera)
- Las comunicaciones se realizan estrictamente por intercambio de mensajes
- Los clientes pueden usar sistemas heterogéneos que permite conectar clientes y servidores independientemente de sus plataformas
- Distinción de funciones basada en el concepto de "servicio"

#### 3.1.2 Ventajas y desventajas

**Ventajas**
- Uso de **clientes ligeros** (pocos requisitos hardware) porque el servidor realiza todo el procesamiento
- Facilita la **integración entre sistemas diferentes** y **comparte información permitiendo interfaces amigables al usuario**
- Se favorece el uso de **interfaces gráficas interactivas** para los clientes para interactuar con el servidor. **Mejora** con respecto al modelo centralizado que normalmente solo transmite datos, **se aprovecha mejor el ancho de banda de red**.
- Mantenimiento y **desarrollo de aplicaciones rápido**
- **Estructura inherentemente modular** que facilita** integración de nuevas tecnologías** y **crecimiento de la infraestructura computacional**.
- Contribuye a proporcionar **soluciones locales a los diferentes departamentos de la organización **pero permitiendo la integración de información relevante a nivel global.
- **Acceso a recursos centralizado**
-** Clientes acceden de forma simultánea** compartiendo información entre sí


**Inconvenientes**
- **Mantenimiento de sistemas más difícil** porque implica interacción de diferentes partes de software y de hardware. **Dificulta el diagnóstico de errores**
- Necesarias **estrategias para manejo de errores** del sistema
- Importante **mantener seguridad del sistema**
- **Debe garantizarse la consistencia de la información**. **Usar mecanismos de sincronización** para evitar que un cliente modifique datos sin que lo sepan los demás clientes. 

¿Qué proceso es el encargado de poder atender las peticiones de varios usuarios de forma concurrente?
Las respuesta el cliente y el servidor es la correcta ya que para atender un usuario es necesario un cliente y para que se puedan atender de forma simultánea debe trabajar también el servidor.

#### 3.1.3 Modelos

Los modelos Cliente/Servidor **se clasifican a partir del número de capas (tiers)** que tiene la infraestructura del sistema. 
Se pueden tener:

**1 capa (1-tier)**: El proceso cliente/servidor se encuentra en el mismo equipo. Realmente no es modelo cliente/servidor porque no hay comunicación por red. 

**2 capas (2-tiers)**: Modelo tradicional. Servidor y clientes bien diferenciados. Problema: El sistema no es escalable. Puede sobrecargarse con número alto de peticiones por parte de los clientes.


**3 capas (3-tiers)**: Para mejorar el rendimiento. Se añade una nueva capa de servidores. Por ejemplo se dispone de:
- **Servidor de aplicación**: Encargado de interactuar con los clientes y enviar peticiones de procesamiento al servidor de datos
- **Servidor de datos**: Recibe peticiones del servidor de aplicación, las procesa y devuelve su resultado al servidor de aplicaciones para que lo envíe al cliente. Para mejorar el rendimiento se pueden añadir los servidores de datos que sean necesarios. 


**n capas (n-tiers)**: Se pueden añadir capas adicionales de servidores para separar la funcionalidad de cada servidor y mejorar el rendimiento del sistema. 

#### 3.1.4 Programación


Pasos que realiza el servidor:
- **Publicar el puerto**:  Se indica el puerto por el que se reciben las conexiones
- **Esperar peticiones**: Servidor queda a la espera de que se conecte un cliente. Al conectarse un cliente, se crea el socket del cliente por el que se envían y se reciben los datos. 
- **Envío y recepción de datos**: Para recibir datos se crea un flujo de entrada (`InputStream`), el servidor la procesa y envía los resultados al cliente con un flujo de salida (`OutputStream`).
- **Cierre del socket del cliente** finalizada la comunicación.

Pasos que realiza el cliente
* **Conectarse con el servidor**: Se usa un `Socket` para conectarse a un puerto de un servidor y luego se crea otro socket por dónde se realiza la comunicación.
* **Envío y recepción de datos**: Se crea `InputStream` y `OutputStream`
* **Cierre del socket**

![](PROGRAMACION_SERVICIOS_PROCESOS/resources/ud03-1.png)

### 3.2 Optimización de sockets

Al usar los sockets debe asegurarse:
- **Atender múltiples peticiones simultáneamente**
- **Seguridad**: Evitar pérdida de información, filtra peticiones de los clientes para asegurar que estén bien formadas y llevar control sobre las transacciones de los clientes
- **Mecanismos para monitorizar los tiempos de respuesta** del servidor a los clientes para ver el comportamiento del sistema. 

#### 3.2.1 Atender múltiples peticiones simultáneas

Para que múltiples clientes usen el servidor de forma simultánea es necesario que la parte que atiende al cliente (zona coloreada) se atienda de forma independiente para cada cliente. En vez de ejecutar todo el código de forma secuencial se pone un bucle while por eso, para que cada vez que se realice la conexión de un cliente se cree un hilo de ejecución que atienda al cliente. Así habrá tantos hilos como clientes se conecten al servidor de forma simultánea.

```java
while (true) {
    // Se conecta un cliente
    Socket skCliente = skServidor.accept();
    System.out.println("Cliente conectado");

    // Atiendo al cliente mediante un thread
    new Servidor(skCliente).start();
}
```

![](PROGRAMACION_SERVICIOS_PROCESOS/resources/ud03-2.png)

![](PROGRAMACION_SERVICIOS_PROCESOS/resources/ud03-3.png)

#### 3.2.2. Threads

Para crear ejecución concurrente  en el servidor, este debe ser una clase que herede de `Thread`. El código que atiende al cliente debe estar dentro de `run()`

```java
import java.net.Socket;
import java.io.*;
import java.net.*;

class Servidor extends Thread {

    Socket skCliente;
    static final int puerto = 2000;

    public Servidor(Socket sCliente) {
        skCliente = sCliente;
    }

    public static void main(String[] arg) {
        try {
            // Inicio el servidor en el puerto
            ServerSocket skServidor = new ServerSocket(puerto);
            System.out.println("Escucho el puerto " + puerto);
            while (true) {
                // Se conecta un cliente
                Socket skCliente = skServidor.accept();
                System.out.println("Cliente conectado");

                // Atiendo al cliente mediante un thread
                new Servidor(skCliente).start();
            }
        } catch (Exception e) {;
        }
    }

    public void run() {
        try {
            // Creo los flujos de entrada y salida
            DataInputStream flujoEntrada = new DataInputStream(skCliente.getInputStream());
            DataOutputStream flujoSalida = new DataOutputStream(skCliente.getOutputStream());

            // ATENDER PETICIÓN DEL CLIENTE
            flujoSalida.writeUTF("Se ha conectado el cliente de forma correcta");

            // Se cierra la conexión
            skCliente.close();
            System.out.println("Cliente desconectado");
        } catch (Exception e) {
            System.out.println(e.getMessage());
        }
    }
}
```

Y si quiere verse (otra vez) un ejemplo básico de cliente:

```java
import java.io.*;
import java.net.*;

class Cliente {
    static final String HOST = "localhost";
    static final int Puerto = 2000;
    public Cliente() {
        try {
            Socket sCliente = new Socket(HOST, Puerto);

            // Creo los flujos de entrada y salida
            DataInputStream flujoEntrada = new DataInputStream(sCliente.getInputStream());
            DataOutputStream flujoSalida = new DataOutputStream(sCliente.getOutputStream());

            // TAREAS QUE REALIZA EL CLIENTE
            String datos = flujoEntrada.readUTF();
            System.out.println(datos);

            sCliente.close();
        } catch (Exception e) {
            System.out.println(e.getMessage());
        }
    }

    public static void main(String[] arg) {
        new Cliente();
    }
}
```

#### 3.2.4 Pérdida de información

La pérdida de paquetes en comunicaciones de red es un factor muy importante a tener en cuenta. 
Para evitarla, cada vez que se envía un paquete el receptor envía al emisor un paquete de confirmación ACK (acknowledgement).

Si el mensaje no llega correctamente al receptor, nunca hay confirmación. El emisor considera que se ha producido un error en el envío del paquete y vuelve a enviarlo. Este es un método bastante lento ya que para enviar un nuevo paquete debería esperar el ACK del anterior.

Realmente los paquetes se envían de forma simultánea sin esperar confirmación. Los paquetes pueden no llegar ordenados, ni los paquetes ACK ordenados o puede perderse alguno. 

Se debe llevar control de paquetes enviados y confirmados. Se utiliza un vector en el que se indica si un paquete se ha enviado correctamente o no.
El vector se desplaza hasta llegar al primer mensaje no enviado correctamente y enviarlo.
El tamaño del vector influye en el rendimiento: Cuanto mayor sea el tamaño, más mensajes se pueden enviar concurrentemente. 

#### 3.2.5 Transacciones

Deben evitarse en entornos cliente/servidor:
- **Operaciones no autorizadas**: El servidor no puede procesar una orden a la que el cliente no tiene acceso 
- **Mensajes mal formados**: Es posible que el cliente envíe mensajes mal formados o incompletos que produzcan error de procesamiento dejando "colgado el servidor".

El flujo de información y comportamiento del servidor debe ser modelado con **diagramas de estados o autómatas**. 

Un autómata es una representación gráfica y lógica del estado del sistema y las transiciones entre estos estados basadas en las entradas recibidas.

1. **Estado Inicial**: El punto de partida del servidor.
2. **Transiciones**: Los cambios de estado que ocurren en respuesta a comandos o eventos específicos.
3. **Estados**: Las diversas situaciones o configuraciones en las que puede estar el servidor en un momento dado.
4. **Comandos/Entradas**: Las instrucciones o datos enviados por el cliente que provocan transiciones entre estados.
5. **Estados Finales**: Los puntos en los que el servidor finaliza ciertas operaciones o la conexión.


- **Estado y Comando**: El servidor utiliza variables como `estado` para rastrear su posición actual y `comando` para capturar las instrucciones del cliente.
- **Transiciones**: Basándose en el `comando` recibido, el servidor cambia de un `estado` a otro, ejecutando operaciones específicas y asegurándose de que solo se realicen las acciones permitidas.
- **Validación**: Cada comando se valida para asegurarse de que es bien formado y autorizado antes de procesarlo, evitando así errores y acciones no autorizadas.

Ejemplo: El servidor se inicia en el estado 0 y directamente envía al cliente el mensaje _Introduce el comando_. El cliente puede enviar los comandos:

- _ls_ que va al estado 2 mostrando el contenido del directorio y vuelve automáticamente al estado 1.
- _get_ que le lleva al estado 3 donde le solicita al cliente el nombre del archivo a mostrar. Al introducir el nombre del archivo se desplaza al estado 4 donde muestra el contenido del archivo y vuelve automáticamente al estado 1.
- _exit_ que le lleva directamente al estado donde finaliza la conexión del cliente (estado -1).
- Cualquier otro comando hace que vuelva al estado 1 solicitándole al cliente que introduzca un comando válido.

### Beneficios
#### 3.2.6 Monitorizar tiempos de respuesta

En el comportamiento de la aplicación Cliente/Servidor son los tiempos de respuesta del servidor. Desde que el cliente realiza una petición hasta que recibe su resultado intervienen dos tiempos que deben ser monitorizados: 

- **Tiempo de procesamiento**: Tiempo que el servidor necesita para procesar la petición del cliente y enviar los datos
- **Tiempo de transmisión**: Tiempo que tardan los mensajes en llegar a su destino a través de la red. 

El tiempo de procesamiento basta medir el tiempo que transcurre en el servidor mientras procesa la solicitud del cliente. 
Para el tiempo de transmisión debe enviar un mensaje con el tiempo del sistema al cliente. El cliente debe calcular su tiempo y compararlo con el tiempo recibido. Para comparar los tiempos ambos equipos deben tener sus relojes de sistema sincronizados a través de algún servicio de tiempo (NTP). En Windows la sincronización es automática y en GNU/Linux se hace ejecutando este comando `/usr/sbin/ntpdate -u 0.centos.pool.ntp.org`

Otra forma de calcular el tiempo de transmisión es usando el comando `ping`. Figura el tiempo para que el cliente origen acceda al servidor. 

### Ejemplo!!!!!!!!!!!!!!!!!!!!!!!!!!!!


## 4. Puertos de red

Los números de puerto en el rango de 0 a 1023 son los llamados _puertos bien conocidos_ (_well-known port_) o también denominados _puertos de sistema_. Son usados por protocolos bien conocidos. Se necesita permiso de administrador.

Entre 1024 y 49151 son puertos registrados, usados por cualquier aplicación. 

Entre 49152 y 65535 son puertos dinámicos o privados. Se asignan de forma dinámica a aplicaciones del cliente al iniciarse la conexión. Se usan en conexiones peer to peer.

| Puerto/protocolo | Nombre         | Descripción                                                                                                                                                                                                                                                                                                                                                                           |
| ---------------- | -------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| n/d / GRE        | gre            | GRE (protocolo IP 47) Enrutamiento y acceso remoto                                                                                                                                                                                                                                                                                                                                    |
| n/d / ESP        |                | IPSec ESP (protocolo IP 50) Enrutamiento y acceso remoto                                                                                                                                                                                                                                                                                                                              |
| n/d / AH         |                | IPSec AH (protocolo IP 51) Enrutamiento y acceso remoto                                                                                                                                                                                                                                                                                                                               |
| 1/tcp            | tcpmux         | Multiplexor TCP                                                                                                                                                                                                                                                                                                                                                                       |
| 5/tcp            | rje            | Entrada de trabajo remota                                                                                                                                                                                                                                                                                                                                                             |
| 7/tcp            | echo           | Protocolo [Echo](https://es.wikipedia.org/wiki/Echo_(inform%C3%A1tica) "Echo (informática)") (Eco) Responde con eco a llamadas remotas                                                                                                                                                                                                                                                |
| 9/tcp            | discard        | Protocolo [Discard](https://es.wikipedia.org/w/index.php?title=Discard&action=edit&redlink=1 "Discard (aún no redactado)"), elimina cualquier dato que recibe, sirve para la evaluación de conexiones                                                                                                                                                                                 |
| 11/tcp           | systat         | Servicio del sistema para listar los puertos conectados                                                                                                                                                                                                                                                                                                                               |
| 13/tcp           | daytime        | Protocolo [Daytime](https://es.wikipedia.org/wiki/Daytime "Daytime"), envía la fecha y hora actuales                                                                                                                                                                                                                                                                                  |
| 17/tcp           | qotd           | [Quote of the Day](https://es.wikipedia.org/wiki/QOTD "QOTD"), envía la cita del día                                                                                                                                                                                                                                                                                                  |
| 18/tcp           | msp            | Protocolo de envío de mensajes                                                                                                                                                                                                                                                                                                                                                        |
| 19/tcp           | chargen        | Protocolo [Chargen](https://es.wikipedia.org/wiki/Chargen "Chargen") o **Generador de caracteres**, envía flujos infinitos de caracteres                                                                                                                                                                                                                                              |
| 20/tcp           | ftpS-data      | [FTPS](https://es.wikipedia.org/w/index.php?title=File_Transfer_Protocol_Shield&action=edit&redlink=1 "File Transfer Protocol Shield (aún no redactado)") File Transfer Protocol (Protocolo de Transferencia de Ficheros) - datos                                                                                                                                                     |
| 21/tcp           | ftp-control    | [FTP](https://es.wikipedia.org/wiki/File_Transfer_Protocol "File Transfer Protocol") File Transfer Protocol (Protocolo de Transferencia de Ficheros) - control                                                                                                                                                                                                                        |
| 22/tcp           | ssh            | [SSH](https://es.wikipedia.org/wiki/SSH "SSH"), [scp](https://es.wikipedia.org/wiki/Secure_Copy "Secure Copy"), [SFTP](https://es.wikipedia.org/wiki/SFTP "SFTP")                                                                                                                                                                                                                     |
| 23/tcp           | telnet         | [Telnet](https://es.wikipedia.org/wiki/Telnet "Telnet") manejo remoto de equipo, inseguro                                                                                                                                                                                                                                                                                             |
| 25/tcp           | smtp           | [SMTP](https://es.wikipedia.org/wiki/SMTP "SMTP") Simple Mail Transfer Protocol (Protocolo Simple de Transferencia de Correo)                                                                                                                                                                                                                                                         |
| 37/tcp           | time           | [Time Protocol](https://es.wikipedia.org/wiki/Time_Protocol "Time Protocol"). Sincroniza hora y fecha                                                                                                                                                                                                                                                                                 |
| 39/tcp           | rlp            | Protocolo de ubicación de recursos                                                                                                                                                                                                                                                                                                                                                    |
| 42/tcp           | nameserver     | Servicio de nombres de Internet                                                                                                                                                                                                                                                                                                                                                       |
| 43/tcp           | nickname       | Servicio de directorio [WHOIS](https://es.wikipedia.org/wiki/WHOIS "WHOIS")                                                                                                                                                                                                                                                                                                           |
| 49/tcp           | tacacs         | Terminal Access Controller Access Control System  <br>para el acceso y autenticación basado en TCP/IP                                                                                                                                                                                                                                                                                 |
| 50/tcp           | re-mail-ck     | Protocolo de verificación de correo remoto                                                                                                                                                                                                                                                                                                                                            |
| 53/tcp and udp   | domain         | [DNS](https://es.wikipedia.org/wiki/DNS "DNS") Domain Name System (Sistema de Nombres de Dominio), por ejemplo [BIND](https://es.wikipedia.org/wiki/BIND "BIND")                                                                                                                                                                                                                      |
| 53/udp           |                | [FaceTime](https://es.wikipedia.org/wiki/FaceTime "FaceTime")                                                                                                                                                                                                                                                                                                                         |
| 63/tcp           | whois++        | Servicios extendidos de [WHOIS](https://es.wikipedia.org/wiki/WHOIS "WHOIS") (WHOIS++)                                                                                                                                                                                                                                                                                                |
| 66/tcp and udp   | Oracle SQLNet  | Software de red que permite acceso remoto  <br>entre los programas y la [base de datos Oracle](https://es.wikipedia.org/wiki/Oracle_Database "Oracle Database").                                                                                                                                                                                                                      |
| 67/udp           | bootps         | [BOOTP](https://es.wikipedia.org/wiki/BOOTP "BOOTP") BootStrap Protocol (servidor), también usado por [DHCP](https://es.wikipedia.org/wiki/DHCP "DHCP")                                                                                                                                                                                                                               |
| 68/udp           | bootpc         | [BOOTP](https://es.wikipedia.org/wiki/BOOTP "BOOTP") BootStrap Protocol (cliente), también usado por [DHCP](https://es.wikipedia.org/wiki/DHCP "DHCP")                                                                                                                                                                                                                                |
| 69/udp           | tftp           | [TFTP](https://es.wikipedia.org/wiki/TFTP "TFTP") Trivial File Transfer Protocol (Protocolo Trivial de Transferencia de Ficheros)                                                                                                                                                                                                                                                     |
| 70/tcp           | gopher         | [Gopher](https://es.wikipedia.org/wiki/Gopher "Gopher")                                                                                                                                                                                                                                                                                                                               |
| 79/tcp           | finger         | [Finger](https://es.wikipedia.org/wiki/Finger_(protocolo) "Finger (protocolo)")                                                                                                                                                                                                                                                                                                       |
| 80/tcp           | http           | [HTTP](https://es.wikipedia.org/wiki/HTTP "HTTP") HyperText Transfer Protocol (Protocolo de Transferencia de HiperTexto) ([WWW](https://es.wikipedia.org/wiki/WWW "WWW"))                                                                                                                                                                                                             |
| 88/tcp           | kerberos       | [Kerberos](https://es.wikipedia.org/wiki/Kerberos "Kerberos") Agente de autenticación                                                                                                                                                                                                                                                                                                 |
| 95/tcp           | supdup         | Extensión del protocolo [Telnet](https://es.wikipedia.org/wiki/Telnet "Telnet")                                                                                                                                                                                                                                                                                                       |
| 101/tcp          | hostname       | Servicios de nombres de host en máquinas SRI-NIC                                                                                                                                                                                                                                                                                                                                      |
| 107/tcp          | rtelnet        | Telnet remoto                                                                                                                                                                                                                                                                                                                                                                         |
| 109/tcp          | pop2           | [POP](https://es.wikipedia.org/wiki/Post_Office_Protocol "Post Office Protocol")2 Post Office Protocol ([Correo electrónico](https://es.wikipedia.org/wiki/Correo_electr%C3%B3nico "Correo electrónico"))                                                                                                                                                                             |
| 110/tcp          | pop3           | [POP3](https://es.wikipedia.org/wiki/POP3 "POP3") Post Office Protocol ([Correo electrónico](https://es.wikipedia.org/wiki/Correo_electr%C3%B3nico "Correo electrónico"))                                                                                                                                                                                                             |
| 111/tcp          | sunrpc         | [sunrpc](https://es.wikipedia.org/wiki/Sunrpc "Sunrpc")                                                                                                                                                                                                                                                                                                                               |
| 113/tcp          | auth           | [ident](https://es.wikipedia.org/w/index.php?title=Ident&action=edit&redlink=1 "Ident (aún no redactado)") (auth) antiguo sistema de identificación                                                                                                                                                                                                                                   |
| 115/tcp          | sftp           | [SFTP (Simple FTP)](https://en.wikipedia.org/wiki/File_Transfer_Protocol#Simple_File_Transfer_Protocol) Protocolo de transferencia de archivos simple                                                                                                                                                                                                                                 |
| 117/tcp          | uupc-path      | Servicios de rutas de Unix-to-Unix Copy Protocol (UUCP)                                                                                                                                                                                                                                                                                                                               |
| 119/tcp          | nntp           | [NNTP](https://es.wikipedia.org/wiki/NNTP "NNTP") usado en los grupos de noticias de [usenet](https://es.wikipedia.org/wiki/Usenet "Usenet")                                                                                                                                                                                                                                          |
| 123/udp          | ntp            | [NTP](https://es.wikipedia.org/wiki/NTP "NTP") Protocolo de sincronización de tiempo                                                                                                                                                                                                                                                                                                  |
| 135/tcp          | epmap          | [epmap](https://es.wikipedia.org/w/index.php?title=Epmap&action=edit&redlink=1 "Epmap (aún no redactado)")                                                                                                                                                                                                                                                                            |
| 137/udp          | netbios-ns     | [NetBIOS](https://es.wikipedia.org/wiki/NetBIOS "NetBIOS") Servicio de nombres                                                                                                                                                                                                                                                                                                        |
| 138/udp          | netbios-dgm    | [NetBIOS](https://es.wikipedia.org/wiki/NetBIOS "NetBIOS") Servicio de envío de datagramas                                                                                                                                                                                                                                                                                            |
| 139/tcp          | netbios-ssn    | [NetBIOS](https://es.wikipedia.org/wiki/NetBIOS "NetBIOS") Servicio de sesiones                                                                                                                                                                                                                                                                                                       |
| 143/tcp          | imap           | [IMAP](https://es.wikipedia.org/wiki/IMAP "IMAP")4 Internet Message Access Protocol ([Correo electrónico](https://es.wikipedia.org/wiki/Correo_electr%C3%B3nico "Correo electrónico"))                                                                                                                                                                                                |
| 161/udp          | snmp           | [SNMP](https://es.wikipedia.org/wiki/SNMP "SNMP") Simple Network Management Protocol                                                                                                                                                                                                                                                                                                  |
| 162/udp          | snmptrap       | [SNMP-trap](https://es.wikipedia.org/wiki/SNMP#Trap "SNMP")                                                                                                                                                                                                                                                                                                                           |
| 174/tcp          | mailq          | Cola de transporte de correos electrónicon MAILQ                                                                                                                                                                                                                                                                                                                                      |
| 177/tcp          | xdmcp          | [XDMCP](https://es.wikipedia.org/wiki/XDMCP "XDMCP") Protocolo de gestión de displays en [X11](https://es.wikipedia.org/wiki/X11 "X11")                                                                                                                                                                                                                                               |
| 178/tcp          | nextstep       | Servidor de ventanas [NeXTStep](https://es.wikipedia.org/wiki/NeXTStep "NeXTStep")                                                                                                                                                                                                                                                                                                    |
| 179/tcp          | bgp            | [Border Gateway Protocol](https://es.wikipedia.org/wiki/Border_Gateway_Protocol "Border Gateway Protocol")                                                                                                                                                                                                                                                                            |
| 194/tcp          | irc            | [Internet Relay Chat](https://es.wikipedia.org/wiki/Internet_Relay_Chat "Internet Relay Chat")                                                                                                                                                                                                                                                                                        |
| 199/tcp          | smux           | SNMP UNIX Multiplexer                                                                                                                                                                                                                                                                                                                                                                 |
| 201/tcp          | at-rtmp        | Enrutamiento [AppleTalk](https://es.wikipedia.org/wiki/AppleTalk "AppleTalk")                                                                                                                                                                                                                                                                                                         |
| 202/tcp          | at-nbp         | Enlace de nembres AppleTalk                                                                                                                                                                                                                                                                                                                                                           |
| 204/tcp          | at-echo        | Echo AppleTalk                                                                                                                                                                                                                                                                                                                                                                        |
| 206/tcp          | at-zis         | Zona de información AppleTalk                                                                                                                                                                                                                                                                                                                                                         |
| 209/tcp          | qmtp           | Protocolo de transferencia rápida de correo (QMTP)                                                                                                                                                                                                                                                                                                                                    |
| 210/tcp          | z39.50         | Base de datos NISO Z39.50                                                                                                                                                                                                                                                                                                                                                             |
| 213/tcp          | ipx            | El protocolo de intercambio de paquetes entre redes (IPX)                                                                                                                                                                                                                                                                                                                             |
| 220/tcp          | imap3          | [IMAP](https://es.wikipedia.org/wiki/IMAP "IMAP") versión 3                                                                                                                                                                                                                                                                                                                           |
| 245/tcp          | link           | Servicio LINK / 3-DNS iQuery                                                                                                                                                                                                                                                                                                                                                          |
| 347/tcp          | fatserv        | Servicio de administración de cintas y archivos FATMEN                                                                                                                                                                                                                                                                                                                                |
| 363/tcp          | rsvp_tunnel    | Túnel RSVP                                                                                                                                                                                                                                                                                                                                                                            |
| 369/tcp          | rpc2portmap    | Portmapper del sistema de archivos Coda                                                                                                                                                                                                                                                                                                                                               |
| 370/tcp          | codaauth2      | Servicios de autenticación del sistema de archivos Coda                                                                                                                                                                                                                                                                                                                               |
| 372/tcp          | ulistproc      | UNIX LISTSERV                                                                                                                                                                                                                                                                                                                                                                         |
| 389/tcp          | ldap           | [LDAP](https://es.wikipedia.org/wiki/LDAP "LDAP") Protocolo de acceso ligero a Directorios                                                                                                                                                                                                                                                                                            |
| 427/tcp          | svrloc         | Protocolo de ubicación de servicios (SLP)                                                                                                                                                                                                                                                                                                                                             |
| 434/tcp          | mobileip-agent | Agente móvil del Protocolo Internet                                                                                                                                                                                                                                                                                                                                                   |
| 435/tcp          | mobilip-mn     | Gestor móvil del Protocolo Internet                                                                                                                                                                                                                                                                                                                                                   |
| 443/tcp          | https          | [HTTPS](https://es.wikipedia.org/wiki/HTTPS "HTTPS")/[SSL](https://es.wikipedia.org/wiki/Transport_Layer_Security "Transport Layer Security") usado para la transferencia segura de páginas web                                                                                                                                                                                       |
| 444/tcp          | snpp           | Protocolo simple de Network Pagging                                                                                                                                                                                                                                                                                                                                                   |
| 445/tcp          | microsoft-ds   | Microsoft-DS ([Active Directory](https://es.wikipedia.org/wiki/Active_Directory "Active Directory"),  <br>compartición en [Windows](https://es.wikipedia.org/wiki/Windows "Windows"), gusano [Sasser](https://es.wikipedia.org/w/index.php?title=Sasser&action=edit&redlink=1 "Sasser (aún no redactado)"), Agobot)  <br>o también es usado por Microsoft-DS compartición de ficheros |
| 465/tcp          | smtps          | [SMTP](https://es.wikipedia.org/wiki/SMTP "SMTP") Sobre [SSL](https://es.wikipedia.org/wiki/Transport_Layer_Security "Transport Layer Security"). Utilizado para el envío de correo electrónico ([Correo electrónico](https://es.wikipedia.org/wiki/Correo_electr%C3%B3nico "Correo electrónico"))                                                                                    |
| 500/udp          |                | [IPSec](https://es.wikipedia.org/wiki/IPSec "IPSec") ISAKMP, Autoridad de Seguridad Local                                                                                                                                                                                                                                                                                             |
| 512/tcp          |                | [exec](https://es.wikipedia.org/w/index.php?title=Exec&action=edit&redlink=1 "Exec (aún no redactado)")                                                                                                                                                                                                                                                                               |
| 513/tcp          |                | [Rlogin](https://es.wikipedia.org/wiki/Rlogin "Rlogin")                                                                                                                                                                                                                                                                                                                               |
| 514/udp          |                | [syslog](https://es.wikipedia.org/wiki/Syslog "Syslog") usado para logs del sistema                                                                                                                                                                                                                                                                                                   |
| 515/tcp          |                | usado para la impresión en windows                                                                                                                                                                                                                                                                                                                                                    |
| 520/udp          | rip            | [RIP](https://es.wikipedia.org/wiki/Routing_Information_Protocol "Routing Information Protocol") Routing Information Protocol (Protocolo de Información de Enrutamiento)                                                                                                                                                                                                              |
| 521/udp          | ripng          | [RIP](https://es.wikipedia.org/wiki/Routing_Information_Protocol "Routing Information Protocol") Routing Information Protocol IPv6 (Protocolo de Información de Enrutamiento Internet v6)[2](https://es.wikipedia.org/wiki/Anexo:Puertos_de_red#cite_note-2)​                                                                                                                         |
| 587/tcp          | smtp           | [SMTP](https://es.wikipedia.org/wiki/SMTP "SMTP") Sobre [TLS](https://es.wikipedia.org/wiki/Transport_Layer_Security "Transport Layer Security")                                                                                                                                                                                                                                      |
| 591/tcp          |                | [FileMaker](https://es.wikipedia.org/wiki/FileMaker "FileMaker") 6.0 _(alternativa para HTTP, ver puerto 80)_                                                                                                                                                                                                                                                                         |
| 631/tcp          |                | [CUPS](https://es.wikipedia.org/wiki/Common_Unix_Printing_System "Common Unix Printing System") sistema de impresión de Unix                                                                                                                                                                                                                                                          |
| 666/tcp          |                | identificación de [Doom](https://es.wikipedia.org/wiki/Doom_(videojuego_de_1993) "Doom (videojuego de 1993)") para jugar sobre TCP                                                                                                                                                                                                                                                    |
| 690/tcp          |                | VATP ([Velneo Application Transfer Protocol](https://es.wikipedia.org/wiki/Velneo_Application_Transfer_Protocol "Velneo Application Transfer Protocol")) Protocolo de comunicaciones de Velneo                                                                                                                                                                                        |
| 993/tcp          | imaps          | [IMAP](https://es.wikipedia.org/wiki/IMAP "IMAP")4 sobre [SSL](https://es.wikipedia.org/wiki/Transport_Layer_Security "Transport Layer Security") ([Correo electrónico](https://es.wikipedia.org/wiki/Correo_electr%C3%B3nico "Correo electrónico"))                                                                                                                                  |
| 995/tcp          |                | POP3 sobre [SSL](https://es.wikipedia.org/wiki/Transport_Layer_Security "Transport Layer Security") ([Correo electrónico](https://es.wikipedia.org/wiki/Correo_electr%C3%B3nico "Correo electrónico"))                                                                                                                                                                                |

## Puertos desde 1024 hasta 49151

|Puerto/protocolo|Nombre|Descripción|
|---|---|---|
|1001/tcp||[SOCKS](https://es.wikipedia.org/wiki/SOCKS "SOCKS") Proxy|
|1194/udp||[OpenVPN](https://es.wikipedia.org/wiki/OpenVPN "OpenVPN") Puerto por defecto en NAS Synology y QNAP|
|1337/tcp||suele usarse en máquinas comprometidas o infectadas|
|1352/tcp||IBM Lotus Notes/Domino RCP|
|1433/tcp||[Microsoft-SQL-Server](https://es.wikipedia.org/wiki/Microsoft_SQL_Server "Microsoft SQL Server")|
|1434/tcp||Microsoft-SQL-Monitor|
|1494/tcp||[Citrix MetaFrame](https://es.wikipedia.org/w/index.php?title=Citrix_MetaFrame&action=edit&redlink=1 "Citrix MetaFrame (aún no redactado)") Cliente IC|
|1512/tcp||[WINS](https://es.wikipedia.org/wiki/Windows_Internet_Naming_Service "Windows Internet Naming Service") Windows Internet Naming Service|
|1521/tcp||[Oracle](https://es.wikipedia.org/wiki/Oracle "Oracle") puerto de escucha por defecto|
|1701/udp||Enrutamiento y Acceso Remoto para VPN con L2TP.|
|1720/udp||[H.323](https://es.wikipedia.org/wiki/H.323 "H.323")|
|1723/tcp||Enrutamiento y Acceso Remoto para VPN con PPTP.|
|1761/tcp||[Novell](https://es.wikipedia.org/wiki/Novell "Novell") Zenworks Remote Control utility|
|1812/udp y tcp||[RADIUS](https://es.wikipedia.org/wiki/RADIUS "RADIUS") authentication protocol, `radius`|
|1813/udp y tcp||[RADIUS](https://es.wikipedia.org/wiki/RADIUS "RADIUS") accounting protocol, `radius-acct`|
|1883 tcp||MQTT protocol|
|1863/tcp||[MSN Messenger](https://es.wikipedia.org/wiki/MSN_Messenger "MSN Messenger")|
|1935/tcp||[FMS](https://es.wikipedia.org/wiki/FMS "FMS") Flash Media Server|
|2049/tcp||[NFS](https://es.wikipedia.org/wiki/Network_File_System "Network File System") Archivos del sistema de red|
|2082/tcp||[cPanel](https://es.wikipedia.org/wiki/CPanel "CPanel") puerto por defecto|
|2083/tcp||[CPanel](https://es.wikipedia.org/wiki/CPanel "CPanel") puerto por defecto sobre [SSL](https://es.wikipedia.org/wiki/Transport_Layer_Security "Transport Layer Security")|
|2086/tcp||[Web Host Manager](https://es.wikipedia.org/w/index.php?title=Web_Host_Manager&action=edit&redlink=1 "Web Host Manager (aún no redactado)") puerto por defecto|
|2427/udp||Cisco [MGCP](https://es.wikipedia.org/wiki/MGCP "MGCP")|
|3000/tcp||[React](https://es.wikipedia.org/wiki/React "React")|
|3030/tcp and udp||[NetPanzer](https://es.wikipedia.org/w/index.php?title=NetPanzer&action=edit&redlink=1 "NetPanzer (aún no redactado)")|
|3074/tcp||[Xbox Live](https://es.wikipedia.org/wiki/Xbox_Live "Xbox Live")|
|3074/udp||[Xbox Live](https://es.wikipedia.org/wiki/Xbox_Live "Xbox Live")|
|3128/tcp||[HTTP](https://es.wikipedia.org/wiki/HTTP "HTTP") usado por [web caches](https://es.wikipedia.org/w/index.php?title=Web_cache&action=edit&redlink=1 "Web cache (aún no redactado)") y por defecto en [Squid cache](https://es.wikipedia.org/w/index.php?title=Squid_cache&action=edit&redlink=1 "Squid cache (aún no redactado)")|
|3128/tcp||[NDL-AAS](https://es.wikipedia.org/w/index.php?title=NDL-AAS&action=edit&redlink=1 "NDL-AAS (aún no redactado)")|
|3306/tcp||[MySQL](https://es.wikipedia.org/wiki/MySQL "MySQL") sistema de gestión de bases de datos|
|3389/tcp||RDP ([Remote Desktop Protocol](https://es.wikipedia.org/wiki/Remote_Desktop_Protocol "Remote Desktop Protocol")) Terminal Server|
|3396/tcp||[Novell](https://es.wikipedia.org/wiki/Novell "Novell") agente de impresión NDPS|
|3690/tcp||[Subversion](https://es.wikipedia.org/wiki/Subversion "Subversion") (sistema de control de versiones)|
|3799/udp||[RADIUS](https://es.wikipedia.org/wiki/RADIUS "RADIUS") CoA -change of authorization|
|4200/tcp||Angular, puerto por defecto|
|4443/tcp and udp||[AOL Instant Messenger](https://es.wikipedia.org/wiki/AOL_Instant_Messenger "AOL Instant Messenger") (sistema de mensajería)[3](https://es.wikipedia.org/wiki/Anexo:Puertos_de_red#cite_note-3)​|
|4662/tcp||[eMule](https://es.wikipedia.org/wiki/EMule "EMule") (aplicación de compartición de ficheros)|
|4672/udp||[eMule](https://es.wikipedia.org/wiki/EMule "EMule") (aplicación de compartición de ficheros)|
|4899/tcp||RAdmin (Remote Administrator),  <br>herramienta de administración remota (normalmente [troyanos](https://es.wikipedia.org/wiki/Troyano_(inform%C3%A1tica) "Troyano (informática)"))|
|5000/tcp||[Universal plug-and-play](https://es.wikipedia.org/wiki/UPnP "UPnP")|
|5001/tcp||Agente v6 [Datadog](https://es.wikipedia.org/wiki/Datadog "Datadog")[4](https://es.wikipedia.org/wiki/Anexo:Puertos_de_red#cite_note-4)​|
|5060/udp||[Session Initiation Protocol](https://es.wikipedia.org/wiki/Session_Initiation_Protocol "Session Initiation Protocol") (SIP)|
|5190/tcp||[AOL](https://es.wikipedia.org/wiki/AOL "AOL") y [AOL Instant Messenger](https://es.wikipedia.org/wiki/AOL_Instant_Messenger "AOL Instant Messenger")|
|5222/tcp||[Jabber/XMPP](https://es.wikipedia.org/wiki/Extensible_Messaging_and_Presence_Protocol "Extensible Messaging and Presence Protocol") conexión de cliente|
|5223/tcp||[Jabber/XMPP](https://es.wikipedia.org/wiki/Extensible_Messaging_and_Presence_Protocol "Extensible Messaging and Presence Protocol") puerto por defecto para conexiones de cliente SSL|
|5269/tcp||[Jabber/XMPP](https://es.wikipedia.org/wiki/Extensible_Messaging_and_Presence_Protocol "Extensible Messaging and Presence Protocol") conexión de servidor|
|5432/tcp||[PostgreSQL](https://es.wikipedia.org/wiki/PostgreSQL "PostgreSQL") sistema de gestión de bases de datos|
|5517/tcp||[Setiqueue](https://es.wikipedia.org/w/index.php?title=Setiqueue&action=edit&redlink=1 "Setiqueue (aún no redactado)") proyecto SETI@Home|
|5631/tcp||[PC-Anywhere](https://es.wikipedia.org/w/index.php?title=PC-Anywhere&action=edit&redlink=1 "PC-Anywhere (aún no redactado)") protocolo de escritorio remoto|
|5632/udp||[PC-Anywhere](https://es.wikipedia.org/w/index.php?title=PC-Anywhere&action=edit&redlink=1 "PC-Anywhere (aún no redactado)") protocolo de escritorio remoto|
|5400/tcp||[VNC](https://es.wikipedia.org/wiki/VNC "VNC") protocolo de escritorio remoto (usado sobre [HTTP](https://es.wikipedia.org/wiki/HTTP "HTTP"))|
|5500/tcp||[VNC](https://es.wikipedia.org/wiki/VNC "VNC") protocolo de escritorio remoto (usado sobre [HTTP](https://es.wikipedia.org/wiki/HTTP "HTTP"))|
|5600/tcp||[VNC](https://es.wikipedia.org/wiki/VNC "VNC") protocolo de escritorio remoto (usado sobre [HTTP](https://es.wikipedia.org/wiki/HTTP "HTTP"))|
|5700/tcp||[VNC](https://es.wikipedia.org/wiki/VNC "VNC") protocolo de escritorio remoto (usado sobre [HTTP](https://es.wikipedia.org/wiki/HTTP "HTTP"))|
|5800/tcp||[VNC](https://es.wikipedia.org/wiki/VNC "VNC") protocolo de escritorio remoto (usado sobre [HTTP](https://es.wikipedia.org/wiki/HTTP "HTTP"))|
|5900/tcp||[VNC](https://es.wikipedia.org/wiki/VNC "VNC") protocolo de escritorio remoto (conexión normal)|
|6000/tcp||[X11](https://es.wikipedia.org/wiki/X11 "X11") usado para X-windows|
|6112/udp||[Blizzard](https://es.wikipedia.org/wiki/Blizzard_Entertainment "Blizzard Entertainment")|
|6129/tcp||[Dameware](https://es.wikipedia.org/w/index.php?title=Dameware&action=edit&redlink=1 "Dameware (aún no redactado)") Software conexión remota|
|6346/tcp||[Gnutella](https://es.wikipedia.org/wiki/Gnutella "Gnutella") compartición de ficheros (Limewire, etc.)|
|6347/udp||[Gnutella](https://es.wikipedia.org/wiki/Gnutella "Gnutella")|
|6348/udp||[Gnutella](https://es.wikipedia.org/wiki/Gnutella "Gnutella")|
|6349/udp||[Gnutella](https://es.wikipedia.org/wiki/Gnutella "Gnutella")|
|6350/udp||[Gnutella](https://es.wikipedia.org/wiki/Gnutella "Gnutella")|
|6355/udp||[Gnutella](https://es.wikipedia.org/wiki/Gnutella "Gnutella")|
|6667/tcp||[IRC](https://es.wikipedia.org/wiki/IRC "IRC") [IRCU](https://es.wikipedia.org/w/index.php?title=IRCU&action=edit&redlink=1 "IRCU (aún no redactado)") Internet Relay Chat|
|6881/tcp||[BitTorrent](https://es.wikipedia.org/wiki/BitTorrent "BitTorrent") puerto por defecto|
|6969/tcp||[BitTorrent](https://es.wikipedia.org/wiki/BitTorrent "BitTorrent") puerto de tracker|
|7100/tcp||Servidor de Fuentes [X11](https://es.wikipedia.org/wiki/X11 "X11")|
|7100/udp||Servidor de Fuentes [X11](https://es.wikipedia.org/wiki/X11 "X11")|
|7659/tcp y udp||[Polypheny](https://es.wikipedia.org/w/index.php?title=Polypheny&action=edit&redlink=1 "Polypheny (aún no redactado)") interfaz de usuario (sistema de gestión de bases de datos)|
|8000/tcp||[iRDMI](https://es.wikipedia.org/w/index.php?title=IRDMI&action=edit&redlink=1 "IRDMI (aún no redactado)") por lo general, usado erróneamente en sustitución de 8080.  <br>También utilizado en el servidor de streaming ShoutCast.|
|8080/tcp||[HTTP](https://es.wikipedia.org/wiki/HTTP "HTTP") [HTTP-ALT](https://es.wikipedia.org/w/index.php?title=HTTP-ALT&action=edit&redlink=1 "HTTP-ALT (aún no redactado)") ver puerto 80. [Tomcat](https://es.wikipedia.org/wiki/Tomcat "Tomcat") lo usa como puerto por defecto.|
|8118/tcp||[privoxy](https://es.wikipedia.org/wiki/Privoxy "Privoxy")|
|9009/tcp||[Pichat](https://es.wikipedia.org/w/index.php?title=Pichat&action=edit&redlink=1 "Pichat (aún no redactado)") peer-to-peer chat server|
|9898/tcp||Gusano Dabber (troyano/virus)|
|10000/tcp||[Webmin](https://es.wikipedia.org/wiki/Webmin "Webmin") (Administración remota web)|
|19226/tcp||[Panda Security](https://es.wikipedia.org/wiki/Panda_Security "Panda Security") Puerto de comunicaciones de Panda Agent.|
|12345/tcp||[NetBus](https://es.wikipedia.org/wiki/NetBus "NetBus") [en:NetBus](https://en.wikipedia.org/wiki/NetBus "en:NetBus") (troyano/virus)|
|25565/tcp||[Minecraft](https://es.wikipedia.org/wiki/Minecraft "Minecraft") Puerto por defecto usado por servidores del juego.|
|31337/tcp||[Back Orifice](https://es.wikipedia.org/wiki/Back_Orifice "Back Orifice") herramienta de administración remota (por lo general troyanos)|
|41121/tcp|tentacle|Protocolo de transferencia utilizado por [Pandora FMS](https://es.wikipedia.org/wiki/Pandora_FMS "Pandora FMS").[5](https://es.wikipedia.org/wiki/Anexo:Puertos_de_red#cite_note-5)​|
|42000/tcp||Utilizado por [_Percona Monitoring Management_](https://es.wikipedia.org/wiki/Percona#Productos "Percona") para recoger [métricas generales](https://es.wikipedia.org/wiki/M%C3%A9trica_del_software "Métrica del software").[6](https://es.wikipedia.org/wiki/Anexo:Puertos_de_red#cite_note-Percona-Monitoring-Managament-6)​|
|42001/tcp||Utilizado por _Percona Monitoring Management_ para recabar datos de desempeño.[6](https://es.wikipedia.org/wiki/Anexo:Puertos_de_red#cite_note-Percona-Monitoring-Managament-6)​|
|42002/tcp||Utilizado por _Percona Monitoring Management_ para recabar métricas de [MySQL](https://es.wikipedia.org/wiki/MySQL "MySQL").[6](https://es.wikipedia.org/wiki/Anexo:Puertos_de_red#cite_note-Percona-Monitoring-Managament-6)​|
|27017/tcp||Utilizado por _Percona Monitoring Management_ para recabar métricas de [MongoDB](https://es.wikipedia.org/wiki/MongoDB "MongoDB").[6](https://es.wikipedia.org/wiki/Anexo:Puertos_de_red#cite_note-Percona-Monitoring-Managament-6)​|
|42004/tcp||Utilizado por _Percona Monitoring Management_ para recabar métricas de [ProxySQL](https://es.wikipedia.org/w/index.php?title=ProxySQL&action=edit&redlink=1 "ProxySQL (aún no redactado)").[6](https://es.wikipedia.org/wiki/Anexo:Puertos_de_red#cite_note-Percona-Monitoring-Managament-6)​|
|45003/tcp||[Calivent](https://es.wikipedia.org/w/index.php?title=Calivent&action=edit&redlink=1 "Calivent (aún no redactado)") herramienta de administración remota SSH con análisis de paquetes.<br><br>smb /tcp/udp 137-19,445|
