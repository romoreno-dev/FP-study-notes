

Aplicación que funcione en red, con múltiples clientes accediendo al servidor -> considerar protocolos de comunicaciones, puertos de comunicaciones, sockets TCP, sockets UDP, modelo cliente/servidor, threads, gestionar bien las transacciones, monitorizar tiempos de respuesta. 



A través de dirección IP y de un puerto (a que ordenador van y dentro del ordenador a qué programa)

TCP/IP es anterior al modelo OSI

Modelo OSI: Su objetivo es ordenar (aislar) en diferentes niveles los procesos de comunicación en red entre diferentes sistemas. Cualquier sistema en red puede ser fraccionado de cara a analizar la comunicación, aislar problemas y resolver incidencias.

Niveles superiores utilizan los servicios de los niveles inferiores.


Capa 1 - Capa física:  Agrupa lo físico relacionado con la interconexión de sistemas en red. Cables de datos, de fibra, conectores, terminaciones... 
Problemas: Cables correctamente introducido, cables no están sueltos, no están doblados, bien crimpados, tarjeta de red correcta, etc.

Capa 2 - Capa de enlace de datos: Transferencia de datos entre dos sistemas directamente o entre ambos sistemas a través de una red. Conmutadores, switches, bridges, etc. Estándares 802.3 (Ethernet) 802.11 (Wi-Fi)
Subcapa LLC (Control de Enlace Lógico): De eléctrico a binario
Subcapa MAC (Control de Acceso al Medio): Paquetes de datos de una tarjeta o interfaz de red de un sistema a otro de un sistema.
Problemas: Además de transmitir, corrige problemas cuando puede. Debido a la capa física por interferencias de radiofrecuencia, baja ASNR,... 

Capa 3 - Capa de red: Decidir el camino físico por el que irán los datos
Enrutamiento de los routers (switches de capa 3). Protocolo OSPF (ruta más rápida que deben seguir los datos para alcanzar su destino)
Direcciones IP forman parte de esta capa. Paquetes pasan de unos a otros enrutadores identificando sus extremos por la IP.
Problemas: Paquetes tardan mucho (host o nodos no enrutados debidamente)

Capa 4 - Capa de transporte: Controla la transmisión de los datos.  Coordina el tránsito e intercambio de datos (velocidad, cantidad de datos, destino, puertos, respuesta al llegar la información). Define puertos a utilizar. 
Protocolo TCP
Protocolo UDP
Problemas: Paquete no alcanza el destino por puerto no abierto

-- Con IP y puertos puede crearse un socket y establecer sesiones entre sistemas, dispositivos, aplicaciones...


Capa 5 - Capa de sesión: Establece diálogo entre los sistemas que intercambian datos. Capacidad del sistema de establecer o no comunicación bidireccional. 
Protocolo NetBIOS, RPC, PPTP, PAP.

Capa 6 - Capa de presentación: Presenta los datos con cierto formato para que sean visibles para la aplicación en la que se mostrará. 
Encriptado y cifrado / Desencriptado de datos... 

Capa 7 - Capa de aplicación: Comunicación entre la aplicación y la red
Protocolos HTTPS, DNS, FTP, SMTP.
Navegadores web, aplicaciones que hacen uso de la red...







Es falso ya que la petición se realiza por el puerto 80 pero la transferencia de datos se realiza por un puerto superior.

Pasos que realiza el servidor:
- **Publicar el puerto**:  Se indica el puerto por el que se reciben las conexiones
- **Esperar peticiones**: Servidor queda a la espera de que se conecte un cliente. Al conectarse un cliente, se crea el socket del cliente por el que se envían y se reciben los datos. 
- **Envío y recepción de datos**: Para recibir datos se crea un flujo de entrada (`InputStream`), el servidor la procesa y envía los resultados al cliente con un flujo de salida (`OutputStream`).
- **Cierre del socket del cliente** finalizada la comunicación.

```java
try {
	var puerto = 9090;
	// Publicar el puerto
	ServerSocket serverSocket = new ServerSocket(puerto); // throw IOException

	// Esperar peticiones y crear socket de cliente
	Socket clientSocket = serverSocket.accept(); //throw IOException
	
	// Envío y recepción de datos
	
	// Cierre
	clientSocket.close();

} catch (IOException ignore) {
}
```


Pasos que realiza el cliente
* **Conectarse con el servidor**: Se usa un `Socket` para conectarse a un puerto de un servidor y luego se crea otro socket por dónde se realiza la comunicación.
* **Envío y recepción de datos**: Se crea `InputStream` y `OutputStream`
* **Cierre del socket**




Para utilizar sockets UDP en Java tenemos la clase DatagramSocket y para recibir o enviar los mensajes se utiliza clase DatagramPacket. Cuando se recibe o envía un paquete se hace con la siguiente información: mensaje, longitud del mensaje, equipo y puerto.

`DatagramPacket`

`DatagramSocket`





1.- Comunicaciones en red
1.1.- Conceptos básicos
1.1.1.-Modelo OSI. (Capas)
1.1.2.-Modelo TCP/IP (Capas)
1.1.3.-Conexiones TCP/UDP
1.1.4.-Puerto de comunicación
1.1.5.-Nombres en internet
1.1.6.-Modelos de comunicaciones
1.2.- Sockets TCP
1.2.1- Servidor
1.2.2- Cliente
1.2.3- Flujo de entrada y salida
1.2.4- Ejemplo 1(I)
1.3 Sockets UDP
1.3.1 Receptor
1.3.2 Emisor
1.3.3 Ejemplo 2

2.- Aplicaciones cliente-servidor

2.1 Paradigma cliente/servidor
2.1.1 Características básicas
2.1.2 Ventajas y desventajas
2.1.3 Modelos
2.1.4 Programación
2.1.5 Ejemplo 3
2.2 Optimización de sockets
2.2.1 Atender múltiples peticiones simultáneas
2.2.2. Threads
2.2.3 Ejemplo 4
2.2.4 Pérdida de información
2.2.5 Transacciones
2.2.6 Ejemplo 5
2.2.7 Monitorizar tiempos de respuesta
2.2.8 Ejemplo 6

https://www.daypo.com/psp3.html#test


Máquinas de estados finitos

Estados: Situacion en la que una variable permanece invariante.

1. **Estados:** El autómata tiene un conjunto finito de estados posibles. En cualquier momento, el autómata se encuentra en uno de estos estados.
    
2. **Entradas:** Hay un conjunto finito de símbolos llamados "entradas" que pueden afectar el estado del autómata. Cuando se proporciona una entrada, el autómata realiza una transición de estado.
    
3. **Transiciones:** Cada combinación de estado y entrada está asociada con una transición específica que indica a qué estado se moverá el autómata cuando se encuentre en ese estado y reciba esa entrada.
    
4. **Estado inicial:** El autómata comienza en un estado inicial específico.
    
5. **Estados de aceptación:** Puede haber uno o más estados de aceptación. Si el autómata termina en uno de estos estados después de procesar una secuencia de entradas, se considera que ha aceptado esa secuencia.


