
## 1. Introducción a la seguridad informática

**Seguridad**: Cualidad de seguro, estar libre y exento de todo daño peligro y riesgo.

En el caso de **Seguridad informática** nos referimos a cumplir las características de:
- **Confidencialidad**: Requiere que la información sea accesible solo por entidades autorizadas
- **Integridad**: Requiere que la información solo sea modificada por entidades autorizadas (escritura, cambio, borrado, creación, reenvío)
- **No repudio**: Protección de un usuario frente a otro que niegue que se realizó cierta comunicación. No repudio de origen (protege al receptor), no repudio de destino (protege al emisor)
- **Disponibilidad**: Recursos del sistema disponibles para las entidades autorizadas cuando se soliciten

Es importante que toda la organización tenga definida política de seguridad para establecer responsabilidades y reglas para evitar amenazas y minimizar los efectos de estas. 

Lo primero, identificar qué se quiere proteger: Hay tres elementos que pueden sufrir amenazas: hardware, software y datos- El más sensible son los datos (dependen de la organización y son el mayor activo de esta, no reemplezable). La seguridad debe entenderse a todos los niveles y aplicarse a todos los elementos. 
### 1.1. Amenazas de seguridad

**Amenaza**: Condición del entorno del sistema de información (persona, máquina) que, dada una oportunidad, podría producir una violación de la seguridad (confidencialidad, integridad, disponibilidad, uso legítimo)

Las amenazas de seguridad pueden caracterizarse modelando el sistema como un flujo de información desde una fuente (fichero, equipo) a un destino (fichero, usuario)-

Hay cuatro categorías generales de amenazas o ataques:
- **Interrupción**: Ataque a la **disponilidad**. Recurso del sistema es destruido o deja de estar disponible. Ej.: Destrucción de elemento hardware, cortar línea de comunicación, deshabilitar gestión de ficheros
- **Intercepción**: Ataque a la **confidencialidad**. Entidad no autorizada consigue acceso a un recurso. Ej.: Escuchar línea para registrar datos que circulen por la red y copia ilícita de ficheros o programas (intercepción de datos) o lectura de cabeceras de paquetes para desvelar usuarios implicados en la comunicación (intercepción de identidad)
- **Modificación**: Ataque a la **integridad**. Entidad no autorizada accede a un recurso y lo manipula. Ej.: Alterar programa para que funcione de forma diferente, modificar contenido de fichero o mensaje.
- **Fabricación**:  Ataque a la **autenticidad**. Entidad no autorizada inserta objetos falsificados en el sistema. Ej.: Inserción de mensajes espurios (basura) en una red o añadir registros a un fichero.

### 1.2. Ataques

Pueden clasificarse en
- **Ataques pasivos**: Atacante no altera la comunicación, solo la escucha o monitoriza. (Ver tráfico de equipo, obtener credenciales). Son difíciles de detectar. Pueden evitarse con el **cifrado** de la información.
- **Ataques activos**: Implican modificación del flujo de datos transmitido o creación de un falso flujo de datos. Puede ser **suplantación de identidad** (se hace pasar por usuario legítimo), **reactuación** (se reenvían mensajes legítimos), **modificación de mensajes**, **denegación de servicio** (saturar servicio para que no pueda usarse correctamente)
### Anexo Ataques

| Nombre                                           | Descripción                                                                                                                                                                                                                      |     |
| ------------------------------------------------ | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --- |
| **Sistemas**                                     |                                                                                                                                                                                                                                  |     |
| Explotar bugs del software                       | Utilizar fallos de seguridad en el software para atacar un sistema.                                                                                                                                                              |     |
| Romper contraseñas                               | Fuerza bruta o ataques basados en diccionarios que permiten obtener las contraseñas del sistema o de un determinado servicio.                                                                                                    |     |
| **Red**                                          |                                                                                                                                                                                                                                  |     |
| Barridos de ping                                 | Utilización del protocolo ICMP para determinar los equipos activos de una red.                                                                                                                                                   |     |
| Confianza transitiva                             | Aprovechar la confianza entre usuarios o equipos para tomar sus privilegios.                                                                                                                                                     |     |
| DNS spoofing                                     | Falsificación de una entrada DNS que apunta a un servidor no autorizad                                                                                                                                                           |     |
| DoS                                              | Ataque de denegación de servicio que consiste en saturar un sistema para impedir la utilización correcta del sistema.                                                                                                            |     |
| Hijacking                                        | Permite a un usuario robar una conexión de un usuario que ha sido autentificado en el sistema.                                                                                                                                   |     |
| Man in the middle                                | A través del ataque ARPspoofing el atacante se sitúa en medio de la comunicación entre varios equipos para realizar otros ataques, como sniffer, spoofing, phising etc.                                                          |     |
| Mensajes de control de red o enrutamiento fuente | Se envían paquetes ICMP para hacer pasar los paquetes por un router comprometido.                                                                                                                                                |     |
| Navegación anónima                               | No se considera directamente un ataque, pero la suelen utilizar los atacantes para realizar sus fechorías. Se denomina “navegación anónima” cuando un usuario utilizar diferentes servidores proxy para ocultar su dirección IP. |     |
| Phising                                          | Ataque informático que consiste en falsificar un sitio web para poder obtener las contraseñas de sus usuarios.                                                                                                                   |     |
| Reenvío de paquetes                              | Retransmisión de paquetes para engañar o duplicar un mensaje (p.ej. una transferencia).                                                                                                                                          |     |
| Sniffer                                          | Programa o equipo que registra todo el tráfico de una red. Se utiliza especialmente para obtener las contraseñas de los sistemas.                                                                                                |     |
| Spoofing                                         | El atacante envía paquetes con una dirección fuente incorrecta. Las respuestas se envían a la dirección falsa. Pueden usarse para: Acceder a recursos confiados sin privilegios Para DoS directo como indirecto o recursivo.     |     |
| **Servidores web**                               |                                                                                                                                                                                                                                  |     |
| Inyección SQL                                    | Ataque que consiste en modificar las consultas SQL de un servidor web para poder realizar consultas SQL maliciosas.                                                                                                              |     |
| LFI                                              | Ataque informático que consiste en hacer que un servidor ejecute un script que está alojado en el mismo servidor.                                                                                                                |     |
| RFI                                              | Ataque informático que consiste en hacer que un servidor ejecute un script que está alojado en una máquina remota.                                                                                                               |     |
| XSS                                              | Consiste en engañar al servidor web para que ejecute un script malicioso en el navegador del cliente que visita una determinada página.                                                                                          |     |
| **Aplicaciones**                                 |                                                                                                                                                                                                                                  |     |
| Crack                                            | Software que permite romper la protección de una aplicación comercial.                                                                                                                                                           |     |
| Keylogger                                        | Software o hardware que registra todas las pulsaciones de teclado que se realizan en el sistema.                                                                                                                                 |     |
| Rootkit                                          | Software que se instala en un sistema y oculta toda la actividad de un usuario (el atacante).                                                                                                                                    |     |
| Troyano                                          | Software que se instala en el ordenador atacado que permite al atacante hacerse con el control de la máquina.                                                                                                                    |     |
| Virus                                            | Software que se copia automáticamente y que tiene por objeto alterar el normal funcionamiento del equipo sin el permiso o el conocimiento del usuario.                                                                           |     |
| **Varios**                                       |                                                                                                                                                                                                                                  |     |
| Ingeniería social                                | Atacante que consiste en convencer a un usuario legítimo para que facilite información (contraseñas, configuraciones, etc.).                                                                                                     |     |
| Rubber-hosse                                     | Utilizar soborno o tortura para obtener una determinada información.                                                                                                                                                             |     |

### 1.3. Vulnerabilidades en el software

**Vulnerabilidad de software**: Fallo o hueco de seguridad detectado en un programa que podría ser usado por un atacante para realizar una acción maliciosa. 

En aplicaciones de envergadura se encarga a usuarios externos que usen la aplicación o a expertos de seguridad que la analicen (auditoría). 

Muchos fallos se descubrirán con la aplicación en producción y será necesario actualizar esta para evitar estas vulnerabilidades. 

Dos pilares:
- **Seguridad interna de la aplicación**: Programar de forma robusta para que el programa se comporte tal y como se espera. Deben gestionarse excepciones, validar entradas de datos y usar ficheros de registro.
- **Políticas de acceso**: Debe determinarse que acciones puede realizar la aplicación en el equipo para limitar el impacto de un posible ataque.

## 2. Programación segura

### 2.1. Excepciones

Una **excepción** es un evento que ocurre durante la ejecución de un programa, interrumpiendo el flujo normal de las instrucciones. Deben gestionarse las excepciones que puedan ocurrir en el programa para evitar fallos en la ejecución.

Ejemplo: Al leer un archivo y enviarlo es posible que el dispositivo no esté disponible, que no haya permisos de lectura, que el fichero no exista, que la red no esté disponible...

**Tipos de excepciones:**

La clase base de todas las excepciones es `Throwable`. De ella heredan:
- `Exception`: Clase base de todas las excepciones lanzadas por el código del programa. Son excepciones verificadas (checked exceptions, el desarrollador debe manejarlas explícitamente en su código ya sea mediante captura o declaración en la firma del método). Ej.: `IOException`, `SQLException`, `ClassNotFoundException`
-  `Error`: Clase base para condiciones anormales que se producen en tiempo de ejecución y que no se pueden manejar. Son condiciones graves y no recuperables. Ni se capturan, ni se manejan en el código del programa. Ej.: `OutOfMemoryError`, `StackOverflowError`, `AssertionError`

Dentro de las subclases de `Exception` está `RuntimeException`. Estas son **excepciones no verificadas** (unchecked exceptions). No están sujetas a la obligación de ser manejadas explícitamente por el desarrollador o declaradas en la firma del método. Ej.: `NullPointerException`, `ArrayIndexOutOfBoundsExceptions`, `ArithmeticException`

**Manejo**

Debe manejarse dentro de un bloque try-catch. Es posible indicar try-catch-finally.
Siendo estrictos podría hacer un try-finally. 
Es posible hacer try-with-resources en aquellas que implementan `AutoCloseable`. 
Es posible indicar varios tipos en el catch como
```java
catch (SomeException | AnotherException e)
```

**Arrojar**
- Puede arrojarse con `throw`
- Puede indicarse en la firma que será arrojada con `throws`
### 2.2. Validación de entradas

Los datos que introducen los usuarios son una vía importante de errores de seguridad y inconsistencia de datos.

Puede suceder **desbordamiento de buffer** (buffer overflow). Al desbordar el tamaño de una determinada variable, accediendo a regiones de memoria reservadas. 

Con la **validación de datos** se:
- **Mantiene la consistencia** de los datos. (Mismo formato, siempre)
- **Evita desbordamientos** de memoria. Al comprobar tamaño y longitud de campo.

Importante la validación del formato y la validación del tamaño de la entrada.

Java tiene la biblioteca `java.util.regex` para usar la clase `Pattern` y definir expresiones regulares que definen exactamente el formato de la entrada de datos. 

**Elementos para la validación de entradas**

|Elemento|Comentario.|
|---|---|
|x|El carácter x.|
|[abc]|Los caracteres a, b o c.|
|[a-z]|Una letra en minúscula.|
|[A-Z]|Una letra en mayúscula.|
|[a-zA-Z]|Una letra en minúscula o mayúscula.|
|[0-9]|Un número comprendido entre el 0 y el 9.|
|[a-zA-Z0-9]|Una letra en minúscula, mayúscula o un número.|

**Ejemplos de validación de entradas**

| Operador      | Comentario                                                                                                                                 |
| ------------- | ------------------------------------------------------------------------------------------------------------------------------------------ |
| [a-z]{2}      | Hay que introducir 2 letras en minúsculas.                                                                                                 |
| [a-z]{2,5}    | Hay que introducir de 2 a 5 letras en minúsculas.                                                                                          |
| [a-z]{2,}     | Hay que introducir más de 2 letras en minúsculas.                                                                                          |
| hola\|adios   | Es la operación OR lógica y permite indicar que se introduzca el texto "hola" o "adios".                                                   |
| XY            | Es la operación AND lógica y permite indicar que se deben introducir dos expresiones: X seguida de Y.                                      |
| e(n\|l) campo | Los delimitadores ( ) permite hacer expresiones más complejas. En el ejemplo, el usuario debe introducir el texto "en campo" o "el campo". |

```java
Patter mattern;
Matcher matcher;

// Patron de entrada que se debe cumplir
pattern = Pattern.compile("[0-9]{8}-[a-zA-Z]"); // DNI
pattern =Pattern.compile("Almería","Granada","Jaén","Málaga","Sevilla","Cádiz","Córdoba","Huelva"); // Provincias andaluzas

// Se pasa al evaluador de expresiones el texto a comprobar
matcher = pattern.matcher(textoComprobar);

// Se comprueba si hay alguna coincidencia dentro de toda la cadena ("1234 abcd 5678" ) lo toma como numero encontrado "\\d+"
return matcher.find() ? "Hay alguna coincidencia" : "No hay coincidencia"
// Se comprueba si es exacto ("1234") es numero encontrado "\\d+"
return matcher.matches() ? "Coincide exactamente" : "No coincide" 
```

### 2.3. Ficheros de registro o Logs

Los **ficheros de registro** o **logs** permiten almacenar registros sobre las acciones que realiza la aplicación, haciendo un registro detallado de lo que ocurre en el sistema. 

1. Importar clases del paquete:  `java.util.logging
2. Crear el log `Logger logger = Logger.getLogger("LogApp")`
3. Definido el logger debe vincularse a un archivo log en el sistema físico de archivos 

```java
Logger logger = Logger.getLogger("MyLog");
FileHandler fileHandler = new FileHandler("archivoLog.log", true); 
// True para que se añadan a los ya existentes.  En el momento en el que se hace, se crea el fichero

// Se añade el manejador del fichero al logger para poder vincular el manejador y escribir o añadir los registros.
logger.addHandler(fileHandler);
```

5. Establecer el formato del archivo

El formatter se indica así:

 ```java
fileHandler.setFormatter(formatter)
```

Puede ser 
 - Archivo de **texto simple** de 1 o 2 líneas.  `SimpleFormatter formatter = new SimpleFormater(); 
 - **Archivo XML** `XMLFormatter formatter = new XMLFormatter()`

- Uno **personalizado** extendiendo la clase `Formatter` y sobrescribiendo el método `format(LogRecord record)`. 
```java
    @Override
    public String format(LogRecord record) {
        StringBuilder sb = new StringBuilder();

        sb.append(dateFormat.format(new Date(record.getMillis())))
          .append(" ")
          .append(record.getLevel().getName())
          .append(": ")
          .append(formatMessage(record))
          .append(System.lineSeparator());

        if (record.getThrown() != null) {
            try {
                StringWriter sw = new StringWriter();
                PrintWriter pw = new PrintWriter(sw);
                record.getThrown().printStackTrace(pw);
                sb.append(sw.toString());
            } catch (Exception ex) {
                // Ignore
            }
        }
        return sb.toString();
    }
```

 
6.  Establecer el nivel de seguridad de la actividad que se quiere registrar 

Registros graves: `logger.setLevel(Level.SEVERE);`
Para registrar todos los eventos `logger.setLevel(Level.ALL)`
Para no registrar nada `logger.setLevel(Level.OFF)`

| Nivel   | Importancia |
| ------- | ----------- |
| SEVERE  | 7 (Máxima)  |
| WARNING | 6           |
| INFO    | 5           |
| CONFIG  | 4           |
| FINE    | 3           |
| FINER   | 2           |
| FINEST  | 1 (Mínima)  |
Por pantalla se visualizan SEVERE, WARNING, INFO y CONFIG (los otros no). 
Si no se quieren visualizar los mensajes de log por pantalla  se pone 
```java
logger.setUseParentHandlers(false);
```

7. **Ejemplo para registrarlo:**
`logger.log(Level.WARNING,"Mi primer log");`

#### Código

```java
    public static void main(String[] args) {

        Logger logger = Logger.getLogger("Milog");

        FileHandler fh;
        try {
            // Configuro el logger y establezco el formato
            fh = new FileHandler("MiLog3", true);
            logger.addHandler(fh);

            logger.setLevel(Level.SEVERE);

            SimpleFormatter formatter1 = new SimpleFormatter();
            //XMLFormatter formatter2 = new XMLFormatter();
            fh.setFormatter(formatter1);
            //logger.setUseParentHandlers(false);
            logger.log(Level.SEVERE, "Hola esto es un problemon");
        } catch (SecurityException e) {
            e.printStackTrace();
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
```
#### Resultado

Sin indicar formatter (o con XMLFormatter)

```xml
<?xml version="1.0" encoding="UTF-8" standalone="no"?>  
<!DOCTYPE log SYSTEM "logger.dtd">  
<log>  
<record>  
  <date>2024-05-23T18:42:01.284676800Z</date>  
  <millis>1716489721284</millis>  
  <nanos>676800</nanos>  
  <sequence>0</sequence>  
  <logger>Milog</logger>  
  <level>SEVERE</level>  
  <class>src.logs.LogPrueba</class>  
  <method>main</method>  
  <thread>1</thread>  
  <message>Hola esto es un problemon</message>  
</record>  
</log>
```

Con SimpleFormatter

```log
may. 23, 2024 8:42:45 P. M. src.logs.LogPrueba main  
SEVERE: Hola esto es un problemon
```

#### Uso de SLF4J 

Podría usarse SLF4J que es otro marco de logs:

```xml
    <!-- SLF4J API -->
    <dependency>
        <groupId>org.slf4j</groupId>
        <artifactId>slf4j-api</artifactId>
        <version>1.7.30</version>
    </dependency>

    <!-- SLF4J Simple (una implementación simple de SLF4J) -->
    <dependency>
        <groupId>org.slf4j</groupId>
        <artifactId>slf4j-simple</artifactId>
        <version>1.7.30</version>
    </dependency>
```


#### Uso de Log4J

```xml
<dependencies>
    <!-- Log4j Core -->
    <dependency>
        <groupId>org.apache.logging.log4j</groupId>
        <artifactId>log4j-core</artifactId>
        <version>2.14.1</version>
    </dependency>

    <!-- Log4j API -->
    <dependency>
        <groupId>org.apache.logging.log4j</groupId>
        <artifactId>log4j-api</artifactId>
        <version>2.14.1</version>
    </dependency>

    <!-- Log4j JUL Adapter -->
    <dependency>
        <groupId>org.apache.logging.log4j</groupId>
        <artifactId>log4j-jul</artifactId>
        <version>2.14.1</version>
    </dependency>
</dependencies>
```

Se puede crear un archivo de configuración para `Log4j` como `log4j2.xml` en `src/main/resources`

Solo a consola:
```xml
<?xml version="1.0" encoding="UTF-8"?>
<Configuration status="WARN">
    <Appenders>
        <Console name="Console" target="SYSTEM_OUT">
            <PatternLayout pattern="%d{HH:mm:ss.SSS} [%t] %-5level %logger{36} - %msg%n"/>
        </Console>
    </Appenders>
    <Loggers>
        <Root level="info">
            <AppenderRef ref="Console"/>
        </Root>
    </Loggers>
</Configuration>
```

A Consola y a Graylog:
```xml
<?xml version="1.0" encoding="UTF-8"?>
<Configuration status="WARN">
    <Appenders>
        <Gelf name="GelfAppender" server="udp:localhost" port="12201" version="1.1">
            <PatternLayout pattern="%d{HH:mm:ss.SSS} [%t] %-5level %logger{36} - %msg%n"/>
        </Gelf>
        
        <Console name="Console" target="SYSTEM_OUT">
            <PatternLayout pattern="%d{HH:mm:ss.SSS} [%t] %-5level %logger{36} - %msg%n"/>
        </Console>
    </Appenders>
    <Loggers>
        <Root level="info">
            <AppenderRef ref="GelfAppender"/>
            <AppenderRef ref="Console"/>
        </Root>
    </Loggers>
</Configuration>
```

Y configurar el redireccionamiento de logging a Log4J

```java
import org.apache.logging.log4j.LogManager;

public class MyApp {
    public static void main(String[] args) {
        // Redirigir la salida de JUL a Log4j
        LogManager.getLogManager().reset();
        java.util.logging.Logger rootLogger = java.util.logging.LogManager.getLogManager().getLogger("");
        rootLogger.addHandler(new org.apache.logging.log4j.jul.LogManager());
        
        java.util.logging.Logger logger = java.util.logging.Logger.getLogger(MyApp.class.getName());
        
        logger.info("This is an info message");
        logger.fine("This is a debug message");
        logger.severe("This is an error message");

        String name = "John";
        logger.log(java.util.logging.Level.INFO, "Hello, {0}!", name);
    }
}
```

## 3. Políticas de seguridad

### 3.1. Modelo de seguridad de Java

JDK 1.0: Modelo muy básico. Aplicaciones locales tenían total acceso a los recursos del sistema y aplicaciones remotas no tenían acceso total al sistema.
JDK 1.1.: Aplicaciones firmadas digitalmente podían acceder a recursos del sistema
JDK 1.2.: Se permiten establecer políticas de acceso en aplicaciones locales o remotas. Una vez que la aplicación está autorizada, se envían peticiones al SecurityManager para acceder a los recursos del sismtea

Las **políticas de seguridad** se pueden establecer utilizando los elementos:
- **Origen**: Usuario o ruta de acceso a la aplicación
- **Permisos**: Permiso de lectura/escritura, permiso de enviar o no...
- **Destino**: Destino al que afecta el permiso. Ej.: Ficheros es su ubicación
- **Acción**: Las que pueden realizarse sobre el recurso. Ej.: En el archivo de lectura, de escritura...

Los permisos más usados en Java:
- `PropertyPermission`: Permisos sobre información del sistema (sistema operativo, versión de Java, directorio home del usuario)
- `SocketPermission`: Permisos sobre las comunicaciones de red. Sobre una determinada IP o URL y/o el puerto de comunicaciones al que puede acceder
- `FilePermission`: Permisos de acceso al disco de una aplicación. A un determinado fichero o carpeta, de lectura o de escritura. 

### 3.2. Asegurar aplicaciones

En aplicaciones ejecutadas localmente el Security Manager está deshabilitado. 

Debe habilitarse con la opción `-Djava.security.manager`  (Se puede hacer en IntelliJ en VMOptions)
El código podrá acceder a datos no sensibles (versión del sistema, versión de java) pero otros como el directorio home del usuario o el de trabajo de java, no permitirá acceso de lectura produciéndose excepción. 

```bash
Caught exception java.security.AccessControlException: access denied ("java.util.PropertyPermission" "user.home" "read")
```


```java
class GetProps {
 
    public static void main(String[] args) { 
        /* Test reading properties w & w/out security manager */         
        String s;
 
        try {
            System.out.println("About to get os.name property value");
 
            s = System.getProperty("os.name", "not specified");
            System.out.println("  The name of your operating system is: " + s);
 
            System.out.println("About to get java.version property value");
 
            s = System.getProperty("java.version", "not specified");
            System.out.println("  The version of the JVM you are running is: " + s);
 
            System.out.println("About to get user.home property value");
 
            s = System.getProperty("user.home", "not specified");
            System.out.println("  Your user home directory is: " + s);
 
            System.out.println("About to get java.home property value");
 
            s = System.getProperty("java.home", "not specified");
            System.out.println("  Your JRE installation directory is: " + s);
 
         } catch (Exception e) {
            System.err.println("Caught exception " + e.toString());
        } 
    }
}
```

##### Configurar políticas de seguridad
Si se quiere acceder a `user.home` y `java.home` se tiene que:
- Ejecutar policytool para iniciar la herramienta que administra políticas de acceso
- En Archivo -> Abrir se busca el fichero java.policy que está en, por ejemplo, `C:\Archivos de programa\AdoptOpenJDK\jdk-11.0.9.11-hotspot\lib\security`
- "Agregar Entrada de Política" indicando el origen del fichero (la aplicación que quiere permitirse) por su ubicación (codebase) o por su firma (SignedBy). Se pulsa en agregar permiso y se agregan permisos  con los datos
```
- PropertyPermission = java.util.PropertyPermission.
- Nombre de Destino = user.home.
- Acciones = read
- PropertyPermission = java.util.PropertyPermission.
- Nombre de Destino = java.home.
- Acciones = read
```

Manualmente se crea un archivo y se guarda con extensión `.policy`
```
grant {
permission java.util.PropertyPermission "user.home", "read";
permission java.util.PropertyPermission "java.home", "read";
};
```

Luego puede indicarse al ejecutar:

`-Djava.security.policy=path/to/mi_politica.policy`

### 3.3. Firmar ficheros Jar

Los ficheros JAR (ARchive of Java) contienen componentes de Java y, opcionalmente, recursos de soporte.

Las políticas de seguridad puede especificarse por la persona que firma el fichero jar. 


```shell
#Compilamos
javac GetProps.java
#Crear fichero JAR
jar cvf GetProps.jar GetProps.class
#Generar par de claves (una privada y otra publica para firmar el fichero)
keytool –genkey –alias firmar –keypass hola00 –keystore DAM –storepass distancia
# Firmar el jar
jarsigner –keystore DAM –signedjar sGetProps.jar GetProps.jar firmar
# Exportar clave pública del certificado
keytool –export –keystore DAM –alias firmar –file Javier.cert
```

La clave privada se usa para firmar; la pública la usan los usuarios para comprobar que el fichero es correcto. 
- -alias firmar. Indica el alias que se va a utilizar para referirse al keystore, que es donde se van almacenar las llaves generadas.
- -keypass hola00. Especifica la contraseña de la llave privada.
- -keystore DAM. Indica el nombre del keystore que se esta creando o utilizando.
- -storepass distancia. Indica el password del keystore.

Al firmar el jar:
- -keystore DAM. Es el keystore creado anteriormente.
- -signedjar sGetProps.jar. Indica el fichero jar firmado.
- GetProps.jar Es el fichero jar a firmar.
- firmar. Es el alias que se ha creado anteriormente.

Se enviará el fichero jar firmado (`sGetProps.jar`) y el certificado `Javier.cert`
### 3.4. Usar ficheros Jar firmados

Se puede ejecutar la aplicación y dará problemas de seguridad
```bash
java –cp sGetProps.jar GetProps
java –Djava.security.manager –cp sGetProps.jar GetProps
```

Se puede importar el certificado
```bash
keytool –import alias Javier –file Javier.cert –keystore DAM
```
- -import alias Javier. Indica que se va a importar el certificado con el alias Javier.
- -keystore DAM. Indica el keystore donde se guarda el certificado

Y, tras esto, configurar las políticas de acceso.
Con policytool se inicia herramienta, se va al fichero java.policy y allí se indica el keystore que se va a usar. Agregar Entrada de Politica (origen del fichero por SignedBy escribiendo el usuario). Agregar permiso (agregando los mismos que se dieron más arriba).

Tras esto, ya funciona.

### 3.5. Herramientas de seguridad

- **policytool**: Herramienta gráfica para administrar las normas de seguridad de una instalación local de JDK. Se buscan las politicas, que por defecto están en `lib/security/java.policy`
- **keytool**: Administrar BBDD de claves y certificados del sistema
- **jarsigner** Firmar y verificar firma de ficheros jar  `jarsigner [opciones] Fichero.jar alias`

 Fichero.jar Es el fichero jar que se firma o verifica
 Alias. Es el alias de entrada al almacén de claves que contiene la clave privada que se utiliza para generar la firma. El almacén de claves es una base de datos de claves y certificados que mantiene la herramienta keytool.
 Opciones. Son las opciones que utiliza jarsigner y que podemos ver al ejecutar simplemente jarsigner.
