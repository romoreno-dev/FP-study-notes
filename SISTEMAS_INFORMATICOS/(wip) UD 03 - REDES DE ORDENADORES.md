

## 1. Características de las redes de ordenadores

### 1.1. Sistemas de comunicaciones

### 1.2. Redes de ordenadores. Ventajas

### 1.3. Clasificación de las redes. Tipos de redes.

### 1.4. Tecnologías WAN


## 2. La arquitectura de red

### 2.1. Modelo OSI y protocolos TCP/IP

### 2.2. Protocolo de comunicación

### 2.3. Funcionamiento de arquitectura basada en niveles


### 2.4. TCP/IP

### 2.5. Nivel de acceso a red

### 2.6. Nivel de internet o de red

### 2.7 Nivel de transporte

### 2.8 Nivel de aplicación


## 3. Topologías de red y modos de conexión

### 3.1. Bus y anillo

### 3.2. Estrella

### 3.3. Modo infraestructura y modo ad-hoc

## 4. Componentes de una red informática

### 4.1. Clasificación de los medios de transmisión

### 4.2. Cableados y conectores

#### Cableado estructurado

### 4.3. Elementos de interconexión

### 4.4. Tarjetas de red y direccionamiento MAC

### 4.5. Conmutadores


### 4.6. Enrutadores

### 4.7. IDS


## 5. Redes inalámbricas 802.11

### 5.1. Tipos de redes 802.11. Características

### 5.2. El canal de red 802.11

### 5.3. SSID de red 802.11

### 5.4. Seguridad 802.11


## 6. Direccionamiento IP

### 6.1. Clases de direcciones

### 6.2. CIDR

### 6.3. Direcciones de uso especial

### 6.4. Direcciones privadas

### 6.5. Subredes


## 7. Seguridad

En un arquitectura de cortafuegos interviene:
- Router: Permite o deniega las comunicaciones. Debe estar especialmente protegido
- Red interna, que podría estar dividida en varias redes.
- Zona neutra: Red entre dos redes para dar más protección. En esta red debe ubicarse los servidores accesibles desde el exterior. Su objetivo es aislar la posible intrusión e impedir el acceso a la red interna. 
VLSM


Intenta mandar un paquete a un equipo de otra red.
Como no tiene puerta de enlace por defecto, ni ningún tipo de enrutamiento que enlace las dos redes entre sí... no puede mandarse.
Si los switches permitiesen el uso de redes virtuales, se podría hacer que se comunicasen entre sí.
Pero lo que se va a usar es un router para comunicar redes distintas entre sí.

El router pertenece a dos redes y comunica entre ellas


Router
- Enrutamiento: une red externa pública con red interna privada
- Acceso inalámbrico: Conecta de forma inalámbrica
- Switch: Conexión de varios equipos mediante cables
- Servidor DHCP: Asignación automática


### 7.1. Esquema de red básico

### 7.2. Esquema de red con zona neutra

### 7.3. Redes inalámbricas

## 8. Configuración de routers

### 8.1. Tablas de enrutado

### 8.2. Elementos de configuración de un router

### 8.3. Ejemplo de creación de tabla de enrutado


## 9. Servicios de red

Servicios que permiten crear la infraestructura de una red:
- Encaminamiento: Para que el servidor actúe como un router que encamine la comunicación entre dos o más redes.
- Servidor DHCP: Para asignar la configuración IP de los equipos que son clientes de la red. <small>(Cuando un portátil se conecta obtiene su IP a través del servidor DHCP  )</small>
- Servidor DNS: Para mantener la equivalencia entre un nombre y su IP

### 9.1. Servicio DHCP: 
- Gestiona la asignación de direcciones IP y de información de red en general de forma automática. Lo hace mediante un proceso `dhcpd` y un fichero de configuración `/etc/dhcpd.conf`
- Necesario por...: La administración de IPs y configuración de equipos en redes grandes, la gestión de direcciones en entornos con equipos móviles, entornos de trabajo de un ISP: sería necesaria una IP por equipo o alguna forma dinámica de asignar IPs a los equipos conectados en ese momento. 

- Datos mínimos que el DHCP proporciona un cliente:
```
- Dirección IP
- Máscara de red
- Puerta de enlace (Gateway)
- Dirección IP del servidor DNS
```

 - Dos formas de asignar:
	 - **Dinámica**: Direcciones IPs libres del rango de direcciones establecido por admin en el `/etc/dhcpd.conf`
	 - **Reserva por dirección IP**: En el fichero de configuración, para una determinada MAC se asigna una dirección IP <small>(útil por ejemplo en el caso de las impresores en red para no tener que configurar de nuevo todos sus clientes)</small>

### 9.2. Uso de DNS. Servicio DNS: 

El uso de nombres de dominio frente a IPs es ventajoso porque son más fáciles de recordar y ofrecen la flexibilidad de cambiar la máquina en la que están alojados.

Inicialmente la asociación de nombres con su IP se realizaba en un fichero `/etc/hosts` o en `System32/driver/etc/hosts` Pero esto provoca desincronización y descoordinación entre los equipos de la red.

#### Domain Name System (DNS)

Es un sistema de nombres jerárquico y distribuido para efectuar la traducción (resolución) entre nombres de dominio y direcciones IP.

#### Funcionamiento del DNS

El DNS tiene una estructura jerárquica en árbol en el que cada rama constituye un dominio de internet. Funciona delegando la responsabilidad de resolución mediante la designación de servidores de nombres autorizados (servidores DNS) para cada dominio (establecimiento de zonas).
<small>Similar a la organización de los sistemas de ficheros en árboles jerárquicos. En él el nombre absoluto del fichero es el formado por los distintos directorios recorridos hasta encontrar el fichero</small>

#### El nombre de dominio (FQDN)

El nombre completo del equipo (FQDN, Fully Qualified Domain Name)  es el resultante de recorrer todos los dominios por los que pasamos. (que incluye el nombre de la computadora y el nombre del dominio asociado a ese equipo).
Suele tener dos o más partes ("etiquetas") separadas por puntos. La jerarquía va de derecha a izquierda (www.example.com), teniendo el TLD, el subdominio (puede tener hasta 127 niveles y cada etiqueta hasta 63 caracteres, aunque el dominio no puede exceder los 255 caracteres). La parte final es el nombre de la máquina. `es.wikipedia.org` 

![[Pasted image 20231229105233.png]]

#### Los servidores de nombres autorizados (Servidores primarios)

Son servidores que tienen asignada la autoridad de resolución de nombres y gestionan la base de datos de zona

**Root**: Cima de la jerarquía. Representado por "." No se muestra en los DNS. Es el punto de partida para la resolución.

**Primer nivel, Dominios de nivel superior (TLD)**: Nombres de los nodos ya establecidos por divisiones geográficas (`.es`, `.uk`) u organizativas (`.com`, para empresas, `.int` para organizaciones de tratados internacionales, `.edu` para educativas, `.gov` del gobierno de EEUU, `.mil` del ejército de EEUU, `.name` nombres de personas, `.info` proveedores de información, `.web` servicios web ). Como es lógico, manejan las consultas sobre nombres de su TLD específico.

Cada rama recibe el nombre de dominio. La asignación de nombres de rama del árbol de primer nivel se delega en un responsable (empresa pública REDES) que a su vez delega la autoridad de resolución de los nombres en otras corporaciones. 

Hay dominios de segundo o tercer nivel (podrían existir más aunque no es habitual)


![[Pasted image 20231229110013.png]]

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
![[Pasted image 20231229113014.png]]
![[Pasted image 20231229114311.png]]
#### Comentarios adicionales 

El protocolo DNS transporta las peticiones y respuestas entre cliente y servidor mediante UDP. Solo se usa TCP cuando se requieren respuestas largas o cuando se intercambia información entre servidores (transferencia de zona)

El DNS resolver puede hacer consultas no recursivas (recibe toda la información), recursivas (pregunta a uno que luego pregunta a otro en su nombre...) o iterativas (pregunta a uno que le remite a otro, que le remite a otro...)

A veces hay "registros pegamento" (glue records) para evitar dependencias circulares. En delegaciones algunos servidores se identifican por nombre. (Si el servidor autorizado de `example.org` es `ns1.example.org` deberia resolverse primero el  `example.org` del autorizado, por lo que se provee la dirección IP para `ns1.example.org` "pegada")

Los nombres de host y las direcciones IP no necesariamente deben tener relación uno a uno (varios host pueden ser de una única IP, alojamiento virtual; un único host puede resolverse en muchas IPs para tolerancia a fallos y distribución de la carga)

Registrar un dominio: Lo puede hacer cualquier persona o empresa en nic.es o por un agente registrador acreditado. 


![[Pasted image 20231229112136.png]]

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

### 9.3. Servicio FTP: 

Permite la transferencia de archivos. El acceso puede ser anónimo (directorio público donde puede descargar lo que allí se ubica) o autorizado (directorio predeterminado en el que puede descargar y quizás subir archivos). Puede conectarse por línea de comandos, filezilla... 
### 9.4. Servicio web: 

Conocido como WWW (World Wide Web). Se encarga del almacenaje y difusión de información mediante distribución de páginas HTML. Proceso servidor (Apache, nginx...), proceso cliente (Firefox, Chrome...). 
El servidor almacena y sirve las páginas HTML. Los navegadores realizan la petición, la interpretan y la muestran al usuario Se comunican ambos mediante protocolo HTTP (orientado a conexión, solicitud-respuesta (sin estado)). La petición se hace por el localizador universal de recursos (URL)

### 9.5. Servicio de correo electrónico: 

Compuesto por varios subsistemas, cada uno con funcionalidad específica.

Funcionalidad: Composición del mensaje, transferencia de origen al destino, generación de informe del envío, visualización de correos recibidos, gestión de correos...

El cliente de correo electrónico proporciona interfaz para escribir, recibir, contestar mensajes...

Protocolos utilizados en el servicio:
- SMTP (Simple Mail Transport Protocol): Encargado de transporte de los mensajes de correo
- POP (Postal Office Protocol) e IMAP (Internet Message Access Protocol): Encargados de comunicar a los agentes de usuario (MUA) con los agentes de entrega de correo (MDA)

El servicio está constituido por:
	- Agente de acceso (AA): Conecta un agente de usuario al mensaje almacenado por protocolos como POP e IMAP
	- Cliente de correo electrónico (MUA); Mecanismos para lectura y composición del mensaje
	- Servidor de correo saliente (MTA) Recibe el correo electrónico y lo envía al servidor de entrada del dominio del receptor. Protocolos SMTP o IMAP
	- Servidor de correo entrante (MDA): Almacena los correos enviados a los buzones y cuando un cliente consulta su cuenta le envía los correos que ha recibido. Protocolos POP o IMAP. 

(Con el comando `mail` puede gestionarse en GNU/Linux)

### 9.6. Servicio de acceso remoto: 

Acceder de forma remota a un equipo a través de la red
- Acceso remoto en modo terminal: Telnet (Telecommunication NETwork) y SSH (Secure SHell). Más usado SSH. Telnet inseguro.
- Acceso remoto en modo gráfico: Servicio VNC (Windows / Linux) o de escritorio remoto (Terminal Server) en Windows. 

## 10. Diseño lógico y físico de una red

### 10.1. Ejemplos de redes simples