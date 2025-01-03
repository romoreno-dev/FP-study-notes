
## 2.1. Administración de usuarios y grupos locales

El **software de base** es el programa encargado de controlar el ordenador.
Al administrar un sistema multiusuario es fundamental saber cuáles son los usuarios y los grupos para crearlos de forma organizada y estructurada. También deben considerarse contraseñas y restricciones que cada usuario o grupo, por seguridad, puedan tener. 

**Cuenta de usuario**: Es mediante la cual se identifica y autentifica un individuo con el sistema. 

El **usuario administrador** (root) es el encargado de dar acceso a los usuarios  y controlar todas las operaciones que vayan a desarrollarse a través de las cuentas. No tiene límites al trabajar sobre el sistema.

**Permisos**: Pueden establecerse permisos a la hora de trabajar con ficheros como:
- **Lectura**: Puede abrir y leer los contenidos del fichero
- **Escritura**: Puede realizar modificaciones sobre el fichero
- **Ejecución**: Puede ejecutar el fichero

**Permisos en Linux** 

Pueden consultarse con `ls -l` 
Pueden modificarse con `chmod`
`- - - - - - - - - -`

El primer grupo de tres son los permisos rwx del propietario `- rwx --- ---`
El segundo grupo de tres son los permisos rwe  del grupo `- --- rwx ---`
El tercer grupo de tres controla los permisos rwx del mundo (permisos globales) `- --- --- rwx`


Pueden crearse permisos:
- **Para asignar recursos** a ciertos usuarios (como el uso de una impresora)
- **Para la gestión simplificada de usuarios** no teniendo que definir los permisos de forma individualizada. 

## 2.2. Seguridad de cuentas de usuario

En nuestro propio equipo, normalmente estaremos como administradores con todos los privilegios. Pero es importante iniciar sesión como admin solo si las operaciones a desarrollar lo requieren.

Siempre que sea posible se deben tener en cuenta las siguientes pautas:
- **Cuenta de administrador**: Cambiar nombre de la cuenta y asignar contraseña segura
- **Cuentas de invitado:** Mantenerlas deshabilitadas porque muchas veces comprometen la seguridad al no necesitar ninguna contraseña. Tienen los mismo privilegios que un usuario estándar pero anonimizada. 
- **Cuentas de usuario**: Asignar solo los permisos estrictamente necesarios. 

Se puede usar una cuenta de usuario sin privilegios para iniciar sesión sin comprometer la seguridad y, cuando sea necesario, utilizar el comando "Ejecutar como administrador" que pedirá la contraseña de la cuenta de administración. Esto en casos en los que se necesiten privilegios: Cambios en la configuración, instalar aplicación, dar de alta nuevo usuario. Cuando finalicen estas tareas, seguir trabajando con la cuenta estándar. 

## 2.3. Seguridad de contraseñas

Las contraseñas son claves para proteger las cuentas de usuario y la información almacenada en equipos y en red. Debe mantenerse la confidencialidad de las mismas. 

**Características de contraseñas para que sean más fiables**
- **Número de caracteres**: Mínimo de ocho caracteres. A mayor cantidad, mayor seguridad
- **Tipo de caracteres**: Contener diferentes tipos de símbolos, mayúsculas, minúsculas, números y caracteres no alfanuméricos (Como $ # etc)
- **Elección de términos**: No deben contener datos muy obvios como nombres de familiares o de la empresa,... ni palabras que se encuentren en diccionarios para evitar técnicas de fuerza bruta (introducción automatizada y masiva de términos del diccionario hasta dar con el correcto)
- **Renovación periódica de la contraseña**: Deben cambiarse con regularidad. Las nuevas deben ser significativamente distintas de las anteriores.

> En Windows 10 se puede habilitar y modificar contraseñas entrando en el Panel de Control >  Cuentas de usuario y protección infantil > Cuentas de usuario 


**Administración de perfiles locales de usuario**

En los sistemas operativos multiusuario pueden definirse perfiles, cada uno de los cuales tiene una serie de archivos con información relativa a la configuración de ese usuario específico. En ellos se suele almacenar:
- Configuración del escritorio del usuario
- Configuración de las aplicaciones a las que tiene acceso
- Accesos a carpetas, impresoras en red, etc.

El perfil de los usuarios habitualmente se crea automáticamente al darlos de alta o al iniciar sesión por primera vez. Sin embargo, las características del perfil varían en función de las necesidades de la persona que lo usa. El administrador debe crear perfiles idóneos y asignarlos a las cuentas (en Windows se hace en Panel de control > Cuentas de usuario > Perfiles de usuario)

## 2.4. Configuración del protocolo TCP/IP. Direcciones IP y máscaras de subred

**Dirección IP**: Permite identificar a cada equipo. Toda dirección IP consta de cuatro números enteros de 4 bytes (32 bits) separados por puntos que pueden variar entre 0 y 255.
La dirección IP identifica unívocamente al equipo de una red: En una misma red no pueden existir dos direcciones IP e iguales (irrepetible y único)
Formato: `W.X.Y.Z`.  Ej.: 192.168.1.6

Debe considerarse

- **Dirección de red**: Son los primeros bits de la dirección IP. Todos los equipos pertenecientes a la misma red contienen la misma dirección de red. Los equipos que pertenecen a una misma red pueden comunicarse de forma directa, sin ninguna intermediación. 

- **Dirección del equipo**: Son los últimos bits de la dirección IP, distintos para cada equipo.

- **Máscara de red (máscara de subred):** Permite determinar qué parte corresponde a la red y cuál al equipo. Esta es una dirección IP que tiene asignado el valor de 255 para todos los bytes de la dirección de red y 0 para todos los bytes de la dirección del equipo.

Si las direcciones de los equipos son `192.168.0.X`, su máscara de subred es `255.255.255.0`

Así, existen tres **clases de redes**:
- **Direcciones IP de clase A**: Máscara de red `255.0.0.0`  `/8` (Binario `11111111.00000000.00000000.00000000`)   8 bits red + 24 bits host
- **Direcciones IP de clase B:** Máscara de red `255.255.0.0` `/16
 (Binario `11111111.11111111.00000000.00000000`) 16 bits red + 16 bits host
- **Direcciones IP de clase C:**  Máscara de red `255.255.255.0` `/24` (Binario `11111111.11111111.11111111.00000000`) 25 bits red + 8 bits host

El **subnetting**, la **división en subredes** facilita la identificación de los equipos conectados a una red, especialmente cuando los equipos son muy numerosos. Para hacerlo, se usa la máquina de subred.

El subnetting plantea que si una red de una clase determinada desperdicia muchas direcciones IP, esta puede ser dividida en subredes más pequeñas que aprovechen mejor el espacio de direccionamiento.

Si se tiene una red dada, se obtienen dos subredes cogiendo un único bit de los reservados para direccionar hosts, ya que con él pueden representarse dos números.
Si son tres subredes, se necesita un bit más (pudiendo llegar a obtenerse cuatro subredes).

Cuantos más bits de hosts sean tomados para crear subredes, menos hosts podrá albergar cada una.

- **Rango de direcciones IP:** `1.0.0.0` a `126.0.0.0`
    - `127.x.x.x` está reservado para pruebas de loopback. Esto significa que cualquier dirección dentro de este rango se utiliza para que un dispositivo se comunique consigo mismo, sin que los paquetes salgan a la red.
- **Rango de direcciones IP:** `128.0.0.0` a `191.255.0.0`
- **Rango de direcciones IP:** `192.0.0.0` a `223.255.255.0`

> 2^n -2 es el número de bits reservados para hosts. Se restan 2 porque el primero se usa para identificar la red (**dirección de red**) y el último para la IP de broadcast (**dirección de broadcasts**)

**Cantidad de redes por cada clase**
- **Clase A**: 7 bits para direccionar redes -> 2^7 redes
- **Clase B:** 14 bits para direccionar redes -> 2^14 redes 
- **Clase C:** 21 bits para direccionar redes -> 2^21 redes

En Clase A, el **primer bit del primer octeto siempre es 0**. Esto deja **7 bits restantes en el primer octeto** para identificar redes.
En Clase B, los **primeros dos bits del primer octeto siempre son 10**. Esto deja **14 bits restantes** en los dos primeros octetos para identificar redes.
En Clase C, los **primeros tres bits del primer octeto siempre son 110**. Esto deja **21 bits restantes** en los tres primeros octetos para identificar redes.

**Cantidad de hosts por cada clase**
- **Clase A**: 24 bits para direccionar hosts -> 2^24 - 2 hosts
- **Clase B:** 16 bits para direccionar hosts -> 2^16 - 2 hosts 
- **Clase C:** 8 bits para direccionar hosts -> 2^8 - 2 hosts


**¿Y el `0.0.0.0`?**
- **Propósito:** Representa una dirección "no especificada". Se usa para indicar que un dispositivo no tiene una dirección IP asignada, o como una forma de referirse a "todas las direcciones disponibles" en ciertas configuraciones.
- **Uso común:**
    1. **Dirección por defecto en dispositivos:** Antes de que un dispositivo obtenga una dirección IP (por ejemplo, mediante DHCP), su IP puede aparecer como `0.0.0.0`.
    2. **Routing y configuraciones de red:** En una tabla de enrutamiento, `0.0.0.0` puede usarse como una "ruta por defecto", lo que significa "cualquier destino no especificado".

**Direcciones IP**
- **Dirección IP privada**: La posee cada equipo que se conecta a la red a través del protocolo TCP/IP. Puede asignarse de forma manual o automática a través del DHCP.
- **Dirección IP pública**. Dirección que se usa para identificarse en la red en otras redes externas como Internet. Asignada por el proveedor de Internet. En principio no puede ser configurada.

Las IPs públicas asignadas por el ISP puede ser:
- **Estática**: Es fija, siempre es la misma. Suelen cobrar por este servicio ya que permite un mayor control y permite asignar la IP a un nombre de dominio, pudiendo publicar el sitio web y que siempre esté accesible.
- **Dinámica**: La dirección es asignada cada vez que nos conectamos a la red. Se modifica. 

Además de IPv4 (4000 millones de direcciones distintas), también existe IPv6 con muchísimas más. 

-----
### 2.4.1. Ejercicios de subnetting
#### Ejercicio 1

**Tienes la dirección IP 192.168.1.0/24, y necesitas dividirla en 6 subredes iguales. Responde las siguientes preguntas:

**1. ¿Cuántos bits adicionales necesitas tomar prestados de los bits de host para crear las 6 subredes?**
**2. ¿Cuál será la nueva máscara de subred en notación CIDR?**
**3. ¿Cuántos hosts utilizables habrá en cada subred?**
**4. Enumera las direcciones de red para cada subred.**
**5. Para la tercera subred, proporciona:**
**- La dirección de red.**
**- La dirección de broadcast.**
**- El rango de direcciones IP disponibles para hosts.**

1. Para tener 6 subredes necesito tener al menos 2^n = 2^3 = 8 -> 3 bits reservados del host
2. La nueva máscara de subred será 11111111.11111111.11111111.11100000
		Que en decimal es `255.255.255.224`     `/27`
3. Habrá 2^n - 2 = 2^5 - 2 hosts = 30 hosts
4. Enumeremos las direcciones de red para cada subred

En cada subred tendremos 2^5 direcciones (30)

Empezamos por 255.255.255.0 e iremos incrementando de 32 en 32. 

192.168.1.0/27
192.168.1.32/27
192.168.1.64/27
192.168.1.96/27
192.168.1.128/27
192.168.1.160/27

5. En la tercera subred

192.168.64.0/27

Dirección de red  192.168.1.64
Dirección de broadcast 192.168.1.95
Disponibles de 192.168.64.1 a 192.168.1.94

---------
#### Ejercicio 2

**Red**: **192.168.10.0/24**  
**Requerimiento**: Tienes que dividir esta red en subredes y asignar direcciones de subred a diferentes departamentos de una empresa.

**Especificaciones**:

1. El **Departamento de Ventas** necesita **60 hosts**.
2. El **Departamento de TI** necesita **30 hosts**.
3. El **Departamento de Marketing** necesita **10 hosts**.
4. El **Departamento de Finanzas** necesita **4 hosts**.

 **Paso 1: Determinar el número de bits necesarios para cada subred**

Para saber cuántos bits tomar prestados para crear subredes que satisfagan los requerimientos de cada departamento, usamos la fórmula:

**Subred para el Departamento de Ventas (60 hosts):**

Para 60 hosts:
26−2=62 hosts utilizables(con 6 bits para hosts)2^6 - 2 = 62

Por lo tanto, necesitamos una subred con **6 bits para hosts**, es decir, una máscara **/26** (porque de los 32 bits de una dirección IP, restamos 6 bits de host, lo que nos deja con 26 bits para la red).

 **Subred para el Departamento de TI (30 hosts):**

Para 30 hosts:
25−2=30 hosts utilizables(con 5 bits para hosts)2^5 - 2 = 30
Necesitamos **5 bits para hosts**, lo que nos lleva a una subred con una máscara **/27**.

**Subred para el Departamento de Marketing (10 hosts):**

Para 10 hosts:

24−2=14 hosts utilizables(con 4 bits para hosts)2^4 - 2 = 14 

Necesitamos **4 bits para hosts**, lo que da una máscara **/28**.

**Subred para el Departamento de Finanzas (4 hosts):**

Para 4 hosts:

23−2=6 hosts utilizables(con 3 bits para hosts)2^3 - 2 = 6
Necesitamos **3 bits para hosts**, lo que da una máscara **/29**.

**Paso 2: Dividir la red original en subredes**

La red original es **192.168.10.0/24**. Vamos a dividirla en subredes más pequeñas según los requisitos de cada departamento.

**Subred 1: Departamento de Ventas (60 hosts)**

- **Máscara de subred:** /26 (6 bits de host)
- **Dirección de red:** **192.168.10.0**
- **Dirección de broadcast:** **192.168.10.63**
- **Rango de hosts utilizables:** **192.168.10.1** a **192.168.10.62**

**Subred 2: Departamento de TI (30 hosts)**

- **Máscara de subred:** /27 (5 bits de host)
- **Dirección de red:** **192.168.10.64**
- **Dirección de broadcast:** **192.168.10.95**
- **Rango de hosts utilizables:** **192.168.10.65** a **192.168.10.94**

**Subred 3: Departamento de Marketing (10 hosts)**

- **Máscara de subred:** /28 (4 bits de host)
- **Dirección de red:** **192.168.10.96**
- **Dirección de broadcast:** **192.168.10.111**
- **Rango de hosts utilizables:** **192.168.10.97** a **192.168.10.110**

**Subred 4: Departamento de Finanzas (4 hosts)**

- **Máscara de subred:** /29 (3 bits de host)
- **Dirección de red:** **192.168.10.112**
- **Dirección de broadcast:** **192.168.10.119**
- **Rango de hosts utilizables:** **192.168.10.113** a **192.168.10.118**


----------------

#### Ejercicio 3

**La red original es 172.16.0.0/16. Vamos a dividirla en subredes según las necesidades de los departamentos.**

**Subred 1: Departamento de Ventas (300 hosts)**

- **Máscara de subred:** **/23** (9 bits para hosts)
- **Dirección de red:** **172.16.0.0**
- **Dirección de broadcast:** **172.16.1.255**
- **Rango de hosts utilizables:** **172.16.0.1** a **172.16.1.254**

**Subred 2: Departamento de TI (100 hosts)**

- **Máscara de subred:** **/25** (7 bits para hosts)
- **Dirección de red:** **172.16.2.0**
- **Dirección de broadcast:** **172.16.2.127**
- **Rango de hosts utilizables:** **172.16.2.1** a **172.16.2.126**

**Subred 3: Departamento de Marketing (50 hosts)**

- **Máscara de subred:** **/26** (6 bits para hosts)
- **Dirección de red:** **172.16.2.128**
- **Dirección de broadcast:** **172.16.2.191**
- **Rango de hosts utilizables:** **172.16.2.129** a **172.16.2.190**

**Subred 4: Departamento de Finanzas (20 hosts)**

- **Máscara de subred:** **/27** (5 bits para hosts)
- **Dirección de red:** **172.16.2.192**
- **Dirección de broadcast:** **172.16.2.223**
- **Rango de hosts utilizables:** **172.16.2.193** a **172.16.2.222**

## 2.5. Servicio de Nombres de Dominio (DNS)

Los **servidores DNS** permiten evitar recordar la IP del equipo al que nos queremos conectar, facilitando escribir directamente el nombre de dominio.

El estado de los servidores DNS puede realizarse por la consola de comandos del equipo. 

```powershell
ipconfig /all
```

```bash
ifconfig /all
```

Se mostrará la IP del servidor DNS en `Servidores DNS`

Y se le puede realizar un ping:  `ping 80.58.61.250`

Para comprobar el funcionamiento, puede hacerse ping a una URL y ver cómo la resuelve de forma correcta mostrando su IP. 

## 2.6. Archivos de configuración de red

La configuración del equipo en la red:

**En Windows**
1. En el **Panel de control > Redes e Internet > Centro de redes y recursos compartidos > Ver redes activas**. Se observa la conexión por la que nos podemos enlazar a la red y se hace click en ella. 
2. En **Propiedades de adaptador** se elige **Protocolo de internet (TCP/IP v4)**  (Podría operarse también con v6)
3. Ahí puede configurarse la dirección IP, la máscara de subred y los servidores DNS.

**En Linux**
Se almacena en `/etc/network/interfaces`

## 2.7. Optimización de sistemas para ordenadores portátiles. Archivos de red sin conexión

Los ordenadores portátiles tienen características especiales que deben ser tenidas en cuenta en la instalación de sistemas operativos y en la protección contra intrusiones:

- **Mayor vulnerabilidad**: Al salir con regularidad de hogares y oficinas, la información es más vulnerable a intrusiones. Si tienen acceso inalámbrico a la red, la vulnerabilidad se duplica ya que el intruso podría acceder a toda la red.
- **Menor rendimiento y otras características**: Aunque se van equiparando a los sobremesa, tienen menor rendimiento que estos en algunos sentidos aún. 

**Optimización de seguridad frente a vulnerabilidades**
Por eso es conveniente tener en cuenta las siguientes premisas:
- **Habilitar contraseñas adicionales**: Además de contraseña de inicio de sesión, habilitar la de la BIOS e instalar software adicional de protección.
- **Sistemas de autenticación fuertes:** Uso de lectores de huellas o de tarjetas inteligentes que aumenten la seguridad.
- **Encriptación de unidades de disco**: El **cifrado de unidad BitLocker** de **Windows** 10 permite encriptar discos para que no sean accesibles sin contraseña.

**Optimización del rendimiento**
Para mejorar el rendimiento se pueden cambiar algunas configuraciones:
- **Desactivar los sonidos del sistema** (Hardware y sonido)
- **Eliminar aplicaciones que no se usen** (Agregar o quitar programas)
- **Desactivar efectos visuales** (Propiedades de Equipo)
- **Desactivar programas que se cargan al inicio** (Win+R MSConfig)

**Archivos de red sin conexión**
- Los archivos que se encuentren accesibles en la red dejarán de estar disponibles al abandonar esta. Hay ciertas herramientas para prevenir el problema como la selección en Windows 10 sobre el archivo o carpeta y habilitación de la opción "Siempre disponible sin conexión"
## 2.8. Principales comandos de sistemas operativos libres y propietarios

Todos los sistemas operativos contemplan diferentes formas de manejo mediante instrucciones en el sistema, pudiendo realizar todas las operaciones que permite el sistema operativo. 
Los entornos de texto agilizan las peticiones, evitando consumir tantos recursos como los entornos gráficos.
Los comandos pueden consultarse en las páginas oficiales de cada sistema, pero algunos de los más utilizados son:

| Comando    | Comando    | Descripción                               |
| ---------- | ---------- | ----------------------------------------- |
| `cd`       | `cd`       | Moverse de directorio                     |
| `dir`      | `ls`       | Mostrar contenido del directorio          |
| `rm`       | `remove`   | Eliminar                                  |
| `mv`       | `move`     | Mover                                     |
| `cp`       | `copy`     | Copiar                                    |
| `mkdir`    |            | Crear directorio                          |
| `fsutil`   | `touch`    | Crear fichero                             |
| `ipconfig` | `ifconfig` | Información de las direcciones del equipo |
| `/?`       | `help`     | Ayuda                                     |

## 2.9. Copias de seguridad (Anexo 3)
//todo 



## 2.10. Configuración de sistemas operativos (Anexo 4)
//todo




