
## 1. Características de las redes de ordenadores

**Red informática**: Dos o más dispositivos conectados para compartir los componentes de su red y la información que pueda almacenarse en todos ellos. 

Otras definiciones: Conjunto de equipos informáticos conectados entre sí por medio de dispositivos físicos que envían y reciben impulsos eléctricos, ondas electromagnéticas o cualquier otro medio para el transporte de datos con la finalidad de compartir información y recursos. 

Para trabajar con redes es necesario conocer los sistemas de comunicación más usados, la arquitectura que las hace posible, los protocolos asociados, la forma de conectarlas y sus componentes. 

Algunas de las características más importantes de las redes de ordenadores son:
- **Conectividad**: Conexión entre diferentes dispositivos para compartir recursos propios o ajenos
- **Seguridad**
- **Optimización de costes**

Siempre útil la Wikipedia https://es.wikipedia.org/wiki/Red_de_computadoras
Y Slideshare https://es.slideshare.net/slideshow/sistema-de-comunicacin-redes-de-telecomunicaciones-presentation/651852
### 1.1. Sistemas de comunicaciones

**Sistema de comunicación** elementos que, siguiendo unas reglas, intervienen en la transmisión de señales, permitiendo el intercambio de información entre un emisor y un receptor.

Los elementos del sistema de comunicación: Emisor, Receptor, Canal (medio por el que se transmite la información con señales convenientemente codificadas mediante un conjunto de reglas que regulen su comunicación, protocolo de comunicación).

###### Clasificaciones
1. Según el **medio de transmisión**
	1. En línea o cableados
	2. Inalámbricos
2. Según la **direccionalidad de la transmisión**
	1. Simplex: Un solo sentido. Emite el emisor, recibe el receptor (Escuchar música por radio)
	2. Semidúplex: Comunicación en dos sentidos pero no de forma simultánea. Emitor emite, receptor recibe y ambos cambian los roles. (Walkie-talkie)
	3. Dúplex: Comunicación en ambos sentidos de forma simultánea. Ambos emisores y receptores a la vez. (Redes de ordenadores funcionan así)
3. Según la **forma de sincronizar las señales**
	1. Síncronas
	2. Asíncronas
4. Según la **naturaleza de la señal**
	1. Analógica
	2. Digital

**Equipo Terminal de Datos (ETD)**: Todos los equipos, ya sean emisores o receptores
**Equipo de Comunicación de Datos (ECD)**: Dispositivo que participa en la comunicación pero no es ni emisor, ni receptor. 
### 1.2. Redes de ordenadores. Ventajas

**Red de ordenadores o red informática**: Conjunto de equipos informáticos conectados entre sí por medio de dispositivos físicos que envían y reciben impulsos eléctricos, ondas electromagnéticas o cualquier otro medio para el transporte de datos con finalidad de compartir información y recursos.

Compartir recursos y la información, asegurar confiabilidad y disponibilidad de la información, asegurar velocidad de transmisión de los datos y reducir el coste general de estas acciones.

Las principales ventajas de la redes de ordenadores:
- Posibilidad de compartir recursos
- Posibilidad de compartir información
- Aumentar posibilidades de colaboración
- Facilitar la gestión centralizada
- Reducir costes

Los recursos no solo son internet. Pueden ser utilización de periféricos compartidos como impresores, discos duros de red, escáneres... o compartir software o compartir información (bases de datos compartidas, documentos que pueden leerse o elaborarse por usuarios diferentes). Servicios informáticos (computación en nube)

Una gestión centralizada de recursos mejora seguridad, optimiza prestaciones, sale más barato. 

Una buena planificación de la red reduce costes de implantación y mantenimiento.
### 1.3. Clasificación de las redes. Tipos de redes.

1. Por alcance o **extensión**:
	1. **Red de área personal** (PAN, Personal Area Network): Usada para la comunicación entre los dispositivos del ordenador cerca de una persona. Ej.: Conexión entre dos dispositivos por bluetooth o dos teléfonos móviles o unos auriculares inalámbricos con un ordenador.
	2. **Red de área local** (LAN, Local Area Network): Limitada a un área especial (cuarto, aula, edificio, avión). Esencial para la creación de redes más grandes.
	3. **Red de área campus** (CAN, Campus Area Network):  Conecta redes de áreas local a través de un área geográfica limitada. Se usa como extensión de la de LAN.
	4. **Red de área metropolitana** (MAN, Metropolitan Area Network): Red de alta velocidad que da cobertura a un área geográfica extensa. Áreas grandes con recursos adicionales a los que necesitaría una red local.
	5. **Red de área amplia** (WAN, Wide Area Network): Redes informáticas que se extienden sobre un área geográfica extensa. Podemos encontrar redes de comunicaciones que permiten el uso de Internet y el propio internet es una red WAN.
2. Según las **funciones** de sus componentes:
	1. **Redes de igual a igual**: Redes peer-to-peer. Ningún ordenador a cargo del funcionamiento de la red. Cada uno controla su propia información y puede funcionar como cliente o servidor según lo necesite. Cada usuario controla su propia seguridad. (Sistemas informáticos incluyen la posibilidad de trabajar así)
	2. **Redes cliente-servidor**: Existencia de uno o varios servidores que dan servicio al resto de ordenadores. Facilitan la gestión centralizada. Se necesitan sistemas operativos tipo servidor como Windows 2008 Server o GNU-Linux. Cualquier distribución Linux puede actuar como servidor aunque hay distribuciones recomendadas como Debian, Ubuntu server, Red Hat...
3. Según el **grado de difusión**: 
	1. Intranet: Red de computadoras que usa tecnología de red para usos comerciales, educativos o de otra índole de forma privada (no comparte sus recursos o su información con otras redes)
	2. Internet: Conjunto descentralizado de redes de comunicación interconectadas que usan la familia de protocolos TCP/IP garantizando que las redes físicas heterogéneas que la componen funcionen como una red única de alcance mundial. 
	
4. Según la **topología**, es decir, la cadena de comunicación usada por los nodos que forman una red para comunicarse, usualmente desde el punto de vista físico, aunque también se puede referir al lógico.

![](SISTEMAS_INFORMATICOS/Andalucía/resources/ud03-1.png)

Al **nivel físico**, forma en la que se conectan los ordenadores en una red,  pueden citarse topologías en bus, en anillo, en estrella, en árbol o jerárquica, en malla, doble anillo, mixta, totalmente conexa.

Es útil en la instalación de red hacer un **esquema de red** que muestre la ubicación de cada ordenador, equipo de interconexión y cableado; usando los planos del edificio o planta donde está ubicada la red.

----------------

**BUS**: Se usa un único cable troncal con terminaciones en los extremos. Los ordenadores de la red se conectan directamente a la red troncal. Las primeras redes Ethernet usaban esta topología con cable coaxial. Hay variantes en redes de televisión por cable, conexión troncal de redes de fibra óptica, instalación y operación de máquinas y equipamientos

**ANILLO**: Conecta cada ordenador o nodo con el siguiente y el último con el primero creando un anillo físico de conexión. Cada estación tiene un receptor y un transmisor que hace la función de repetidor pasando la señal a la siguiente estación. En este tipo de red la comunicación se da por el paso de un testigo, evitando eventuales pérdidas de información debidas a colisiones. Las redes locales Token-ring emplean una topología en anillo aunque la conexión física sea en estrella.

Hay topologías de anillo doble donde dos anillos permiten que los datos se envíen en ambas direcciones (redundancia, tolerancia a fallos). Usada en redes FDDI (Fiber Distributed Data Interfaces, usarse como red troncal que distribuye datos por fibra óptica. Algunas configuraciones de servidores también usan esta topoogía.)

**ESTRELLA:** Conecta todos los ordenadores a un nodo central (router, conmutador, switch, concetrado, hub). Las redes de área local modernas basadas en IEEE 802.3 usan esta topología. El equipo de interconexión central canaliza toda la información y por él pasan todos los paquetes (función de distribución, conmutación y control). El nodo central debe estar siempre activo o toda la red quedaría sin servicio. 

Ventajas: Topología tolerante a fallos. Si un ordenador se desconecta **no perjudica a toda la red**, facilita la incorporación de nuevos ordenadores a la red siempre que el nodo central tenga conexiones y permite prevenir conflictos de uso.

La topología en estrella se amplía en la de **estrella extendida o árbol** donde las redes en estrella se conectan entre sí. 
Si tiene un elemento de dónde se parte es **topología en estrella jerárquica**. Esto posibilita redes más amplias y se mantiene una jerarquía de conexiones, con un nodo que es el inicio de la jerarquía: Router y a partir de él red de área local que permite dar servicios a redes de área locales más pequeñas.

Muy usual en redes de área local: Principio de jerarquía es el router que conecta a internet y el resto switch que dan servicio a aulas, salas de ordenadores, despachos... Así a partir de una única conexión a Internet se puede dar servicio a varias redes o subredes locales, ahorrando costes. Si el equipo de interconexión de mayor jerarquía falla, la red ya no presta los servicios para los que fue diseñada. 

------------

La **topología lógica** o esquema lógico busca mostrar algunas características de la conexión:  uso de red, nombre de ordenadores, direcciones, aplicaciones. Un grupo de ordenadores podría estar formado por un único icono. Sirven para hacerse una idea de cómo estará conectada la red. 

4. Según el **tipo de conexión**
	1. **Redes cableadas**
	2. **Redes inalámbricas**. Con modo infraestructura (incluye punto de acceso), modo ad-hoc (no necesita punto de acceso)
	3. **Redes mixtas

-----------

En redes inalámbricas se sigue el estándar IEEE 802.11 que introduce el concepto de **modo de conexión**.

- **Modo infraestructura**: Equipos inalámbricos se conectan a red cableada ya existente. Usa un equipo de interconexión (**Punto de Acceso**) para que haga esta función o un router con características de punto de acceso. Suele usarse como acceso a la infraestructura del cable que permite la conexión a Internet (router de la compañía de telecomunicaciones). Todo el tráfico se canaliza a través del punto de acceso y todos los equipos inalámbricos deben estar dentro de la zona de cobertura para establecer comunicación entre ellos. 

- **Modo ad-hoc**: Permite conectar dispositivos inalámbricos entre sí sin equipo como punto de acceso. Cada dispositivo de red forma parte de red de igual a igual (peer to peer). Permite que se pueda compartir información entre equipos que se encuentren en un lugar determinado de forma puntual. 

- **Tercera opción**: Ambos modos de conexión combinados.

------------------

### 1.4. Tecnologías WAN

Las redes WAN (Wide Area Network) se extienden sobre regiones geográficas extensas. Pueden cubrir distancias de unos 100 o 1000 km dando servicio un país o un continente.

Internet da una WAN de alta velocidad, por lo que no es necesaria la existencia de redes privadas WAN, sino redes privadas virtuales (VPN, extensión segura de la red local LAN sobre una red pública o no controlada como internet) con mecanismos cifrados y otras técnicas seguras.

La WAN es una red punto a punto que utiliza conmutación de paquetes. Pueden usar sistemas de comunicación vía satélite o radio. 

Basan su funcionamiento en **técnicas de conmutación**, definibles como la forma en que un usuario y otro establecen la comunicación. Estas técnicas son:
- **Conmutación de circuitos**: Establecimiento de un enlace físico para la transmisión entre dos nodos, que se libera cuando finalice la comunicación en caso de usar una red conmutada opermanece si es una red dedicada
- **Conmutación de mensajes**: Tratamiento de bloques de información dotados de dirección de origen y de destino. La red almacena los mensajes hasta verificar que han llegado correctamente a su destino y proceden a su retransmisión o destrucción.
- **Conmutación de paquetes**: Dividir el mensaje en paquetes. La comunicación entre dos equipos implica la transmisión de los paquetes. Cada paquete es enviado de un nodo de la red al nodo siguiente. Cuando el nodo receptor recibe completamente el paquete, lo almacena y lo vuelve a emitir al nodo que le sigue. Este proceso se repite hasta que el paquete llegue al destino final. Para eso se usan los **datagramas** y los **circuitos virtuales.** Internet es una red de conmutación de paquetes basada en datagramas. 

La redes WAN suelen estar soportadas por redes públicas de telecomunicaciones que se suelen usar para conectarse a internet. Ejemplos:
- Red telefónica básica o red telefónica conmutada (RTB, RTC). Transmisión de datos a baja velocidad.
- Bucle de abonado digital asimétrico (ADSL). Línea de datos independiente de la línea de teléfono aprovechando el ancho de banda disponible por encima del requerido por el servicio telefónico 
- Telefonía móvil mediante UMTS o 3G 
- Internet por cable
## 2. La arquitectura de red

**Arquitectura de red**: Conjunto de capas o niveles junto con los protocolos definidos en cada una de estas capas que hacen posible que un ordenador se comunique con otro ordenador independientemente de la red en la que se encuentre. 

La arquitectura de red debe incluir información suficiente para que, al desarrollar un programa o diseñar un dispositivo, cada capa responda de forma adecuada al protocolo apropiado.

Tres factores importantes que debe tener en cuenta la arquitectura de red son:
- La **topología**, forma en que se conectan los nodos de una red y características físicas de las conexiones
- **Método de acceso a la red**, formas de compartir información y reglas para evitar su pérdida
- **Protocolos de comunicación**, reglas para favorecer la comunicación y establecer, mantener y permitir la utilización de la información.

### 2.1. Modelo de arquitectura de red por capas

La arquitectura de red se divide en niveles o capas para reducir la complejidad de su diseño. Cada uno de estos niveles tiene asociados uno o varios protocolos que definen las reglas de comunicación de la capa correspondiente. 

Se llama **pila de protocolos** o **jerarquía de protocolos** a la arquitectura de red que usa unos protocolos determinados.

Si imaginamos una arquitectura de red de cuatro niveles: Dos ordenadores tendrán  implementada la arquitectura. Cada nivel tiene implementados sus protocolos; puede decirse que las comunicaciones entre niveles iguales se hace a través de los protocolos correspondientes. Pero el flujo real de información con los datos que se quieren transmitir va de un ordenador a otro pasando por cada uno de los niveles. Es decir, los datos no se transfieren directamente de una capa a otra sino que cada capa pasa los datos e información de control a la capa adyacente, después pasa al medio de transmisión adecuado y, posteriormente, sucede lo mismo pero en sentido contrario en el otro ordenador.

Cada capa tiene unos servicios asignados y cada una tiene unas funciones, ocupándose solo de los datos e información de control que necesite según el protocolo utilizado.

Las capaz adyacentes tienen lo que se denomina **interfaz**, se definen las operaciones que la capa inferior ofrece a la superior. Es importante definir interfaces claras entre niveles.

Reglas:
- Cada nivel solo se comunique con el nivel superior o inferior
- Cada nivel inferior proporcione servicios al nivel superior

Las arquitecturas en capas facilitan compatibilidades de software y de hardware, modificaciones futuras, etc. 

### 2.2. Protocolo de comunicación

**Protocolo de comunicaciones**: Conjunto de reglas normalizadas para representación, señalización, autenticación y detección de errores necesario para enviar información a través de un canal de comunicación.

**Características principales de los protocolos**:
- Mensaje
- Codificación
- Formato
- Tamaño del mensaje
- Temporización

Se necesitan protocolos para:
- Identificar emisor y receptor
- Definir medio o canal a usar
- Definir lenguaje común a usar
- Definir forma y estructura de los mensajes
- Establecer velocidad y temporización de mensajes
- Definir codificación y encapsulación de mensajes

Algunas cuestiones que los protocolos de redes deben resolver son:
- El **enrutamiento**: Elegir, de las diferentes rutas para llegar a un mismo destino, una de ellas siendo deseable que se elija la mejor o más rápida.
- El **direccionamiento**: Definir direcciones de red que determinen a qué ordenador se quiere uno conectar o por dónde debe conectarse para llegar a un destino.
- La **necesidad de compartir un medio de comunicaciones**: Mecanismos de control de acceso al medio y orden en que se accede.
- La **saturación**: Evitar que el receptor del mensaje o los dispositivos intermedios se saturen. 
- El **control de errores**: Mecanismos de control. 

### 2.3. Funcionamiento de arquitectura basada en niveles. Modelo OSI.

El **Modelo OSI** (Open System Interconnection, Interconexión de Sistemas Abiertos) es el modelo de red creado por ISO en 1984. Define un marco de referencia para la definición de arquitecturas de interconexión en sistemas de comunicaciones.

Simplifica las actividades de red porque agrupa los procesos de comunicación en siete capas que realizan tareas diferentes. 

En sí no es una arquitectura, sino un referente para desarrollar arquitecturas.

Los siete niveles OSI son:

| Capa | Nombre                           | Funciones                                                                                                                                                                                                                                           |
| ---- | -------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 1    | Capa física o nivel físico.      | Conexiones físicas, incluyendo el cableado y los componentes necesarios para transmitir la señal.                                                                                                                                                   |
| 2    | Capa o nivel de enlace de datos. | Empaqueta los datos para transmitirlos a través de la capa física. El direccionamiento físico se define utilizando direcciones MAC. Se encarga del acceso al medio, el control de enlace lógico o LLC, de la detección de errores de transmisión... |
| 3    | Capa o nivel de red.             | Separa los datos en paquetes, determina la ruta que tomaran los datos y define el direccionamiento.                                                                                                                                                 |
| 4    | Capa o nivel de transporte.      | Se encarga de que los paquetes de datos tengan una secuencia adecuada y de controlar los errores.                                                                                                                                                   |
| 5    | Capa o nivel de sesión.          | Mantiene y controla el enlace entre los dos extremos de la comunicación.                                                                                                                                                                            |
| 6    | Capa o nivel de presentación.    | Determina el formato de las comunicaciones así como adaptar la información al protocolo que se este usando.                                                                                                                                         |
| 7    | Capa o nivel de aplicación.      | Define los protocolos que utilizan cada una de la aplicaciones para poder ser utilizadas en red.                                                                                                                                                    |

Relacionadas con el **hardware**: Capas 1, 2 y 3
Relacionadas con el **software**: Capas 5, 6 y 7
### 2.4. TCP/IP

 Protocolos TCP/IP se refiere a la arquitectura de red que contiene varios protocolos, entre ellos, el protocolo TCP (Transmision Control Protocol) y el protocolo IP (Internet Protocol).

Es la arquitectura más usada, base de las comunicaciones de Internet y sistemas operativos modernos.

Está formada por cuatro niveles:

| Capa | Nombre                                                                  | Funciones                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| ---- | ----------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 1    | Capa o nivel de acceso a la red, de enlace o también llamado de subred. | Se encarga del acceso al medio de transmisión, es asimilable a los niveles 1 y 2 del modelo OSI, y sólo especifica que deben usarse protocolos que permitan la conexiones entre ordenadores de la red. Hay que tener en cuenta que está arquitectura está pensada para conectar ordenadores diferentes en redes diferentes, por lo que las cuestiones de nivel físico no se tratan, y se dejan lo suficientemente abiertas para que se pueda utilizan cualquier estándar de conexión. Permite y define el uso de direcciones físicas utilizando las direcciones MAC.                                                 |
| 2    | Capa o nivel de red también llamada de Internet.                        | Al igual que la capa de red del modelo OSI, esta capa se encarga de estructurar la información en paquetes, determina la ruta que tomaran los paquetes y define el direccionamiento. En esta arquitectura los paquetes pueden viajar hasta el destino de forma independiente, pudiendo atravesar redes diferentes y llegar desordenados, sin que la ordenación de los paquetes sea responsabilidad de está capa, por tanto tampoco se encarga de los errores. El protocolo más significativo de esta capa es el protocolo IP, y entre sus funciones está la de dar una dirección lógica a todos los nodos de la red. |
| 3    | Capa o nivel de transporte.                                             | Es igual al nivel de transporte del modelo OSI. Se encarga de que los paquetes de datos tengan una secuencia adecuada y de controlar los errores. Los protocolos más importantes de esta capa son: TCP y UDP. El protocolo TCP es un protocolo orientado a conexión y fiable, y el protocolo UDP es un protocolo no orientado a conexión y no fiable.                                                                                                                                                                                                                                                                |
| 4    | Capa o nivel de Aplicación.                                             | Esta capa englobaría conceptos de las capas de sesión, presentación y aplicación del modelo OSI. Incluye todos los protocolos de alto nivel relacionados con las aplicaciones que se utilizan en Internet.                                                                                                                                                                                                                                                                                                                                                                                                           |

En algunos casos la capa de acceso a red se divide en capa de hardware o física y capa de enlace de datos (en este caso la arquitectura TCP/IP tendría cinco niveles en vez de cuatro)

![](SISTEMAS_INFORMATICOS/Andalucía/resources/ud03-2.png)
### 2.5. Nivel de acceso a red

**Nivel de acceso a red**: Convertir información suministrada por el nivel de red en señales que puedan ser transmitidas por el medio físico y convertir señales que llegan por el medio físico en paquetes de información manejables por el nivel de red.

TCP/IP originalmente no se preocupa demasiado del nivel físico. Solo de estandarizar los protocolos relacionados con el enlace de datos.

Considerar aquí las cuestiones relacionadas con las conexiones físicas en las redes locales, definidas por estándar Ethernet (características del cableado y señalización, formatos de las tramas de datos del nivel de enlace de datos).

También el **direccionamiento físico**: Subcapa del nivel de enlace de datos. El control de acceso al medio (MAC) para definir las direcciones MAC, identificador de 48 bits en forma hexadecimal dividida en 6 bloques de dos números hexadecimales separados por dos puntos.
Formato: `FF:FF:FF:FF:FF:FF`
- Los 24 bits más significativos (izquierda) determinan el fabricante, identificador único de organización
- Los 24 bis menos significativos (derecha) identfiican a una interfaz concreta. 
Ninguna tarjeta de red tiene la misma dirección física.

El protocolo que lo gestiona es el de resolución de direcciones (protocolo ARP) encuentra la dirección física (MAC) que tiene relación con la dirección lógica (dirección IP) -> Traduce de IP a MAC. El protocolo inverso es RARP  pero no es tan usado.

El formato de la unidad de información en este nivel es la **TRAMA** 

![](SISTEMAS_INFORMATICOS/Andalucía/resources/ud03-3.png)

En la trama tenemos los datos que recibimos de capas superiores, añadiéndole una cabecera con las direcciones MAC de origen y destino, junto con el tipo de trama Ethernet que se utiliza y una cola donde se agrega información para el control de errores.
### 2.6. Nivel de internet o de red


### 2.7 Nivel de transporte


### 2.8 Nivel de aplicación



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