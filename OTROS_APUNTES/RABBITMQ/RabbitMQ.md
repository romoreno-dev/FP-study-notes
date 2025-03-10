
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

Los **exchanges** son los componentes que reciben los mensajes enviados al bróker (junto con la dirección de enrutamiento, routing key) y los redirigen hacia las colas.
Pueden ser:
- Durables. Hasta que son eliminados explícitamente
- Temporales. Hasta que el bróker se apaga o se reinicia
- Autodestruibles. Dejan de existir cuando no quedan colas asociadas a ellos.

**Exchanges predefinidos por el protocolo AMQP**
Cada tipo tiene algoritmo de nerutamiento específico. 

- **Direct exchange**: 
- **Fanout exchange:** 
- **Topic exchange:** 
- **Headers exchange:** 
## 6. Direct exchange

Enruta los mensajes a las colas basándose en una coincidencia exacta entre la **routing key** del mensaje y la **binding key** de la cola.

**Algoritmo de enrutamiento**
- La cola es asociada al exchange mediante routing-key K
- Exchange recibe mensaje con routing-key K
- Cola recibe mensaje si K = R

**Direct exchange predefinidos**
1. **amq.direct**:  Los mensajes son enrutados a las colas que tienen el mismo **binding-key** que la **routing-key** del mensaje.
2. **exchange por defecto (sin nombre)**: No tiene configuración explícita de bindings. Cualquier mensaje enviado al exchange (`""`) se dirige a la cola cuyo nombre coincide exactamente con la `routing-key` del mensaje. 

![[Pasted image 20250310000614.png]]

**Usos y ejemplos** 
- **Enviar mensajes a receptores específicos**: Sistema de notificaciones donde distintos usuarios reciben mensajes específicos.  `admin_queue`, `support_queue`, `client_queue`
- **Distribuir tareas entre múltiples consumidores**: Sistema de procesamiento de imágenes en el que múltiples trabajadores procesan en paralelo. Se usa un exchange para balancear carga entre workers. 
- **Patrones request/reply asíncrono**: Un cliente necesita hacer una consulta a un servidor y recibir respuest en otro momento. Habrá un direct exchange para requests y otro para response. 

## 7. Fanout exchange

Al recibir un mensaje lo envía a todas las colas asociadas a él, ignorando el routing-key del mensaje. Es un **envío incondicional**.

**Algoritmo de enrutamiento**
- Exchange recibe un mensaje
- Todas las colas asociadas al exchange reciben el mensaje

**Fanout exchange predefinido**
- **amq.fanout**

![[Pasted image 20250310001624.png]]

Se dan tres colas asociadas al fanout exchange ("facturas", "inventario", "envios") en un sistema de pedidos. El exchange envía copia de pedidos a todas sus colas asociadas. Los mensajes no llevan routing-key, porque no lo necesitan y las colas tampoco lo tienen. 

**Usos y ejemplos** 
- **Sistemas de notificación**
- **Comunicación de eventos globales**: Rankings online, competiciones deportivas, metereología.
- **Patrones publicador-suscriptor**: Múltiples colas cuyos suscriptores necesitan procesar los mensajes de diferente manera.

## 8. Topic exchange

Las colas se asocian mediante **patrones de coincidencia** (expresiones regulares). Lo enruta mediante el **routing-pattern** que se encuentre en la **routing-key** del mensaje. Estas son palabras delimitadas por puntos (.).

Ej.: `esp` ,  `esp.and.sev`.

Las colas se asocian al exchange mediante su pattern con palabras y metacaracteres (`*` una palabra, `#` varias palabras delimitadas por puntos ).

**Ejemplos de routing-patterns**
- `mes.*.sec`: Primera palabra mes y tercera sec. La segunda puede ser combinación alfanumérica. Ej.: `mes.segunda2palabra.sec`
- `mes.#`: Primera palabra mes. Y número variable de palabras. Ej.: `mes.segunda.2.3.ruta`
- `*.cad.#`: Primera palabra la que sea. Seguida por cad. Y número variable de palabras.

**Algoritmo de enrutamiento**
- Cola asociada a exchange mediante routing-pattern K
- Exchange recibe mensaje con routing-key R
- Cola recibe mensaje si patrón K detecta a R

**Fanout exchange predefinido**
- **amq.topic**




**Headers exchange:** Enrutar mensajes en base a headers.


## 9. Headers exchanges


## 10. Queues
- Almacenan los mensajes
- Asociadas a exchange por binding
- Estructuras FIFO (First In First Out). Aún así el orden de entrega no está garantizado (salvo que solo hubiese un consumidor) porque dependiendo del número de consumidores conectados, las transacciones en consumidores, las prioridades de mensajes o la implementación de optimizaciones puede darse un orden u otro.

- Las colas son declaradas por las aplicaciones cliente. 
- Sus atributos obligatorios son:
	- name (Nombre)
	- durable (Durable o temporal). Si es durable lo almacena en disco duro; si es temporal en memoria RAM.
	- exclusive. La cola puede ser utilizada únicamente por una conexión y se eliminará cuando esta se cierre.
	- auto-delete. La cola será eliminada cuando deje de haber consumidores conectados
- Otros atributos opcionales almacenadas en el atributo arguments (diccionario de pares clave-valor):
	- type (classic o quorum)
	- TTL (time to live)
	- longitud máxima


## 11. Bindings

Asocian la cola y el exchange. Indica a los exchanges las colas a las que enviar los mensajes. Suelen ser indicados por aplicaciones clientes.

Sus atributos pueden ser:
- routing-key (direct exchange)
- routing-pattern (topic exchange)
- headers (header exchange)

## 12. Mensajes
Unidad mínima de información procesada en el broker.

Contiene:
- Cabecera: Propiedades y metadatos predefinidos que describen el mensaje. Algunos siguen el protocolo AMQP y otras acordadas entre productores y consumidores por una especificación.
- Cuerpo: Contenido del mensaje en formato binario

Propiedades:
- delivery-mode: Indica si el mensaje se queda en memoria una vez que llega a la cola o si debe ser almacenado en disco
- content-type: Formato de datos del mensaje. Mimetype (application/json, application/xml). Útil para serializar/deserializar.
- content-encoding: Si se ha aplicado codificación/compresión al cuerpo del mensaje. Ej.: base4, gzip.
- timestamp: Cuando fue creado el mensaje
- routing-key: Usada por direct-exchange y topic-exchange
- headers: Usada por headers-exchange. Contiene la tabla de cabeceras
- message-id: Identificador único del mensaje
- correlation-id: Suele usarse para indicar el message-id del mensaje relacionado o el identificador de la transacción u operación
- app-id: Aplicación que genera el mensaje
- priority: Prioridad del mensaje
- expiration: Marca de tiempo para indicar cuándo expira el mensaje. RabbitMQ lo descartará pasado ese tiempo.
- type: Tipo de mensaje. Para describir su contenido si no viniese en content-type por ejemplo.
- reply-to: Nombre de la cola o routing-key a utilizar para responder al mensaje en un patrón request-reply. 

## 13. El primer productor

Usar cliente Java de RabbitMQ para implementar el primer productor.
Se enviará al direct exchange por defecto sin nombre. Se asociará a una cola cuyo routing-key sea igual al binding-key nombre de la cola. 


```xml
 <dependencies>
        <!-- Cliente RabbitMQ -->
        <dependency>
            <groupId>com.rabbitmq</groupId>
            <artifactId>amqp-client</artifactId>
            <version>5.25.0</version>
        </dependency>
        <dependency>
            <groupId>org.slf4j</groupId>
            <artifactId>slf4j-simple</artifactId>
            <version>1.7.36</version>
        </dependency>
    </dependencies>
```


- Se usa `ConnectionFactory` como proveedor de conexiones. Viene con los valores de RabbitMQ por defecto. 
- La conexión se obtiene con `factory.newConnection`.
- El canal se crea con `connection.createChannel()`
- La cola se crea con `channel.queueDeclare(nombreCola, durable, exclusive, autodelete, arguments)`
- Para enviar mensaje al exchange se usa `channel.basicPublish(exchange, routingName, props, bytes[])`

```java
public class ProductorSimple {  
  
    public static void main(String[] args) throws IOException, TimeoutException {  
        final var message = "Hola a todos";  
  
        ConnectionFactory factory = new ConnectionFactory();  
        factory.setHost("localhost");  
        factory.setPort(5672);  
        factory.setUsername("guest");  
        factory.setPassword("guest"); 
        try (            // Abrir conexion AMQ  
                         Connection connection = factory.newConnection();  
                         // Establecer canal  
                         Channel channel = connection.createChannel()) {  
 
  
            String queueName = "primera-cola";  
  
            // Crear cola  
            channel.queueDeclare(queueName, false, false, false, null);  
  
            // Enviar mensaje al exchange ""  
            channel.basicPublish("", queueName, null, message.getBytes());  
        } catch (Exception e) {  
            System.out.println(e.getMessage());  
        }  
    }  
}
```


## 14. El primer consumidor





















