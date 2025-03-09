
## 1. Definición

- **RabbitMQ** es un **sistema de mensajes de multiprotocolo**. 
- Fue uno de los primeros brokers de mensajes en implementar el protocolo estándar AMQP (Advanced Message Queue Protocol). Enfocado en la comunicación asíncrona basada en mensajes con garantía de entrega a través de confirmación de recepción de bróker a productor y de consumidor a bróker. 
- Escrito en Erlang/OTP

RabbitMQ facilita la comunicación entre productores y consumidores.
Para ello se utilizan: 
- **Exchanges**
- **Queues**
- **Bindings**: Asocian las colas a los exchanges mediante reglas.

**Productores** publican mensajes en RabbitMQ que son enrutados hacia colas a través de un **exchange**. Las colas almacenan los mensajes y los envían a los consumidores.

**Usos**
- **Integración asíncrona**: Comunicación de microservicios basada en eventos
- **Patrones de Publicación-Suscripción**: Envío de mensajes a múltiples destinatarios
- **Desacoplamiento y distribución de tareas**: Ej.: Aplicaciones de procesamientos de imágenes o generación de documentos.
- **Patrones de Request/Replay (RPC)**: Llamada a procesos remotos de forma asíncrona.

**Ventajas**
- Bróker de mensajes más usado en el mercado
- Código abierto, distribuido y escalable
- Ligero
- Alto rendimiento, fiable, tolerancia a fallos
- Escalado horizontal en clústeres
- Flexibilidad de enrutamiento (punto a punto, enrutamiento complejo con expresiones regulares,...)
- Soporta múltiples protocolos
- Soporta múltiples lenguajes
- Pueden extenderse con plugins

## 2. Instalación en Windows 10

www.rabbitmq.com

Aunque obviamente hay Docker, lo vamos a instalar con Chocolatey.
`choco install rabbitmq`

Abrimos **RabbitMQ Command Prompt** y comprobamos si está usándose con:
`rabbitmqctl status`  

Veremos que está activo el 
- rabbitmq_management (habilita la consola de admin de RabbitMQ)
En los listeners se verá que la comunicación HTTP con el broker es 15672 (acceso a consola de admin) --> `localhost:15672`
Usuario por defecto: guest, guest

Podrán verse allí los: Connections, Channels, Exchanges, Queues, Consummers, 

### Conceptos básicos

- **Mensaje**:  Unidad mínima de información que se transmite a través de un canal. Posee:
	- **Cabecera**: Metadatos (Formato del mensaje, origen, destino, etc.)
	- **Cuerpo**: Contenido del mensaje
- **Productor**: Aplicación que envía mensajes
- **Consumidor**: Aplicación que recibe mensajes
- **Canal de mensajes**: Conexión virtual entre productores y consumidores

## 3. Sistemas de mensajería o brokers

- Hacen de intermediarios para la comunicación entre aplicaciones.
-  Desacopla la comunicación productor-consumidor. El productor no envía directamente mensaje al consumidor sino que lo envía al broker (este, en el caso de RabbitMQ lo almacena en una cola para entregarlos al consumidor). El productor puede enviar mensajes sin necesidad de saber si hay consumidores, dónde se ubican o si están activos. 

- **Routers**: Componentes que determinan qué canales deben seguir los mensajes hasta llegar a los consumidores. Se encuentran dentro de los brókers. Utilizan para saberlo los metadatos que llevan los mensajes en la cabecera.

#### Patrones de comunicación más comunes

#### Patrón punto a punto
Asegura que cada mensaje sea recibido por un único consumidor. Suelen implementarlo usando una cola. En el caso de que haya varios consumidores, el broker los distribuye de forma de que cada mensaje sea recibido por un único consumidor. Ofrece garantía de entrega, manteniendo el mensaje en cola hasta que el consumidor confirma que lo ha recibido. Ej.: Tramitación de pedidos, procesado de imágenes, generación de documentos. 

**Ejemplo detallado**
- Cliente quiere generar factura
- Módulo "Servicio gestión de compras" manda mensaje al broker con los datos de la compra.
- Broker recibe y almacena el mensaje en cola confirmando al servicio de compras OK que a su vez se lo dice al cliente OK. "Gracias por su factura, en breve se la enviaremos por correo".
- Cuando el mensaje está listo para ser distribuido y el "Generador de facturas" está libre, el broker le envía copia al mensaje y mantiene este fuera de la cola hasta que el Generador de facturas confirma que ha procesado el mensaje. Entonces lo elimina.
- Si el Generador de facturas no confirma, el broker puede intentar reenviarlo o almacenarlo en cola de mensajes no procesados según la garantía de entrega que se quiera ofrecer.

![[Pasted image 20250309221358.png]]

#### Patrón Publicación/Subscripción

Que un productor pueda enviar mensajes de un tipo o categoría a todos los consumidores subscritos para ese tipo o categoría.

**Topic**: Tema, categoría, tipo específico de información
**Suscripción**: Acción (petición) que realiza un consumidor que desea recibir información de un topic.
El productor es un publicador y el consumidor es un suscriptor.

**Ejemplo detallado**
Sensor metereológico y aplicaciones que quieren recibir datos de temperatura.
Topic: Temperatura
Suscritas: Aplicaciones

Cuando el sensor publica un mensaje, el broker envía el mensaje a todos los subscriptores del topic.

![[Pasted image 20250309221745.png]]


## 4. AMQP y RabbitMQ

AMQP (Advanced Message Queueing Protocol): No solo se define un protocolo de red sino también la interacción entre productor/consumidor y broker. Esto permite interoperabilidad total entre brokers y clientes independientemente del lenguaje en el que esté implementados, siempre y cuando se use la misma versión de AMQP.

Versiones: AMQP 0-9-1. Existe una más moderna AMQP 1.0.

Se definen tres componentes necesarios:
- **Exchanges**: Destino inicial de todos los mensajes que se publican en el broker. Estos redirigen mensajes hacia las colas de mensajes a partir de la información contenidas en mentadatos.
- **Queues**: Almacenan los mensajes hasta ser enviados a consumidores.
- **Bindings**: Asociación entre cola y exchange. Indican al exchanges las colas que corresponden.

- **Connection**: Conexión física (TCP) entre productor/consumidor y brokers
- **Channel**: Conexión virtual entre productor/consumidor y broker. Puede haber varios canales compartiendo una conexión (multiplexado). Evita tener que abrir y cerrar TCP constantemente.
- **Virtual Host**: Agrupación lógica de componentes (productores, consumidores, exchanges, queues, permisos de usuario, bindings) permitiendo aislar componentes de distintos usuarios o aplicaciones. 


![[Pasted image 20250309222157.png]]

**Virtual Host**: Agrupa exchange, cola y binding. 
**Productor**: Procesa datos necesarios para generar documento.
**Consumidor**: Genera el PDF.

El metadato tiene: 
- Atributo "exchange": Indica a RabbitMQ qué exchange debe recibir el mensaje
- Atributo "routering-key": Indica al exchange a donde debe redirigir el mensaje

## 5. Exchange

**Direct exchange**: Al recibir un mensaje lo enruta a las colas asociadas a él mediante un binding-key que sea igual al routing-key contenido en la cabecera. 

**Fanout exchange:** 

**Topic exchange:**

**Headers exchange:**




















