
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

Las **copias de seguridad** (backups) consisten en la duplicación de archivos y datos importantes, almacenándolos en una ubicación segura para que puedan ser recuperados en caso de pérdida, daño o corrupción del original. 

Son una parte esencial de la gestión de datos en cualquier entorno informático.

Protegen contra riesgos como fallos de hardware, errores humanos, ciberataques o desastres naturales y son fundamentales para garantizar la continuidad del negocio y la preservación de información crítica. 

### 2.9.1. Importancia de las copias de seguridad

- **Protección contra pérdida de datos:** Los datos podrán ser recuperados ante cualquier incidente.
- **Garantía de continuidad del negocio:** Evita paradas operativas significativas, pérdida de ingresos y daños a la reputación. Se minimiza el tiempo de inactividad, permitiendo una rápida recuperación.
- **Cumplimiento normativo**: Se requiere en muchos lugares por regulación la existencia de copias de seguridad de ciertos tipos de datos.
- **Recuperación ante ataques cibernéticos:** En caso de un ataque ransomware, tener copia de seguridad recientes permite recuperar los datos sin pagar el rescate.
### 2.9.2. Aspectos que tener en cuenta al realizar copias de seguridad

- **Frecuencia:** La naturaleza de los datos (si cambian con frecuencia o no, su importancia) determinará la frecuencia con la que se deben hacer copias de seguridad.
- **Medios de almacenamiento:** Pueden almacenarse en una gran variedad de medios. Depende del volumen de datos, la velocidad de recuperación deseada y el presupuesto.
- **Ubicación de las copias de seguridad:** Las copias de seguridad deben almacenarse en una ubicación diferentes a los datos originales para protegerse contra desastres que afecten al sitio principal.
- **Seguridad:** Deben estar protegidas contra accesos no autorizados (cifrado de datos, controles de acceso y protección física de los medios de almacenamiento)
- **Automatización:** Deben automatizarse para evitar el riesgo de errores humanos y garantizar su regularidad y consistencia.
- **Verificación y prueba de recuperación:** Debe verificarse que los datos se han respaldado correctamente y realizar pruebas periódicas de recuperación para asegurar que pueden ser restaurados sin problemas.
### 2.9.3. Cómo realizar copias de seguridad en Windows 10

##### Método 1: Copias de seguridad con historial de archivos
**1. Acceder a historial de archivos**: Panel de control > Sistema y seguridad > Guardar copias de seguridad de tus archivos con historial de archivos
**2. Seleccionar la unidad de copia de seguridad**: Conectar un disco duro externo para almacenar las copias de seguridad. Hacer click en "Seleccionar unidad" y elegir la unidad de almacenamiento
**3. Configurar el historial de archivos**: Hacer click en "Activar" para iniciar el proceso de copia de seguridad. Se puede personalizar qué carpetas desean respaldarse, frecuencia de las copias y durante cuánto tiempo conservarlas.
**4. Restaurar archivos**: Desde "Historial de archivos" seleccionar "Restaurar archivos personales" para navegar y restaurar versiones anteriores de los archivos.

#### Método 2: Copias de seguridad y restauración (Windows 7)
**1. Acceder a copias de seguridad y restauración**: Panel de control > Sistema y seguridad > Copia de seguridad y restauración
**2. Configurar la copia de seguridad**: Hacer click en "Configurar copia de seguridad", seleccionar la unidad donde se desea almacenar la copia de seguridad. 
**3. Elegir qué respaldar**: Windows elige los archivos a respaldar o se pueden seleccionar manualmente
**4. Programar la copia de seguridad**: Se puede programar horario para que WIndows realice la copia de seguridad
**5. Restaurar archivos**: Con la misma herramienta se podrán restaurar con "Restaurar mis archivos"

#### Método 3: Copias de seguridad en la nube con OneDrive
**1. Configuración de OneDrive**: Acceder a la aplicación con la cuenta de Microsoft
**2. Seleccionar carpetas para respaldar**: En la configuración de OneDrive, seleccionar las carpetas que deseas respaldar
**3. Sincronización automática**: Archivos se sincronizarán automáticamente con OneDrive, proporcionando copia de seguridad en la nube accesible desde cualquier dispositivo

### 2.9.4. Cómo realizar copias de seguridad en Ubuntu

#### Método 1: Copias de seguridad Deja Dup (Backup)

**1. Instalar Deja Dup**
```bash
sudo apt install deja-dup
```
**2. Acceder a DejaDup abriendo la aplicación "Copias de seguridad"**
**3.Configurar la copia de seguridad**. Hacer click en "Almacenamiento" para seleccionar el destino y en "Carpetas" para indicar cuáles se desean incluir en la copia de seguridad.
**4.Programar la copia de seguridad**. En la pestaña "Programación"
**5.Iniciar y restaurar copia de seguridad**. Haciendo click en "Copia de seguridad ahora" para iniciar el proceso y en la pestaña "Restaurar" para indicar qué se desea recuperar.
#### Método 2: Copias de seguridad con rsync (Línea de comandos)
```bash
# 1. Instalar rsync
sudo apt install rsync
# 2. Realizar copia de seguridad
# a Permisos y tiempos copiados correctamente, v modo detallado, delete para eliminar archivos en destino que no existan en el origen
rsync -av --delete /ruta/origen /ruta/destino
# 3. Automarizar la copia de seguridad
# Mediante cron editando la tabla de cron con
crontab -e
```

Se agregará la siguiente línea para que, por ejemplo, se ejecute todos los días a las 2AM:
```nano
0 2 * * * rsync -av --delete /home/usuario/Documentos/media/usuario/backup/
```

#### Método 3: Copias de seguridad en la nube con herramientas de terceros

**1. Configuración del almacenamiento en la nube** (OneDrive, Dropbox)
**2. Rclone para múltiples servicios en la nube**

```bash
# 1. Instalar RClone
sudo apt install rclone
# 2. Configurar Rclone con el acceso a la cuenta de Google Drive, Dropbox, etc.
rclone config
# 3. Realizar copia de seguridad sincronizando carpeta local con almacenamiento en nube
rclone sync /ruta/origen remote:/ruta/destino
```
## 2.10. Configuración de sistemas operativos (Anexo 4)

La **configuración de un sistema operativo** es el proceso mediante el cual se ajustan los parámetros y componentes de un sistema, su rendimiento, seguridad y funcionalidad. 
Abarcan gestión de usuarios y grupos, asignación de permisos, seguridad del sistema, configuración de servicios y procesos y monitorización del rendimiento.

Su objetivo es adaptar el sistema operativo a las necesidades específicas del entorno en el que opera. 

La **correcta configuración** es clave para maximizar la eficiencia, garantizar la seguridad y asegurar la estabilidad de cualquier infraestructura informática. 

### 2.10.1. Usuarios y grupos

La correcta gestión de usuarios y grupos permite:
- **Seguridad**: Control de acceso basado en roles, asegurando que cada usuario solo realiza las acciones permitidas
- **Organización**: Facilitar la administración al asignar permisos y derechos a grupos e nlugar de individualmente
- **Control y auditoría:** Mantener registros claros de qué acciones han sido realizadas y por qué usuario
- **Facilidad de gestión:** Agrupar usuarios con roles similares, facilitando la asignación y gestión de permisos y recursos.

### 2.10.1.1. Usuarios y grupos en Windows 10

**Creación y gestión de usuarios y grupos en Windows 10**
**1. Acceder a la configuración de usuarios y grupos.** Panel de control // Configuración > Cuentas > Familia y otras personas
**2. Crear nuevo usuario.** Hacer click en "Agregar otra persona a este equipo". Se puede elegir entre agregar un usuario con una cuenta de Microsoft o con una cuenta local. Se introduce el nombre de usuario, la contraseña y una pregunta de seguridad. 
**3. Asignar usuario a grupos**. Pulsa Windows+X y seleccionar "Administración de equipos". En el menú de la izquierda, seleccionar "Usuarios y grupos locales > Usuarios". Hacer click sobre el usuario que se desea modificar y seleccionar "Propiedades". En la pestaña "Miembro de", agregar el usuario a uno o más grupos.

**Grupos comunes en Windows 10**
- **Administradores**: Usuarios con control total sobre el sistema, pueden instalar programas y cambiar configuraciones del sistema.  
- **Usuarios:** Usuarios estándar con permisos limitados, como ejecutar programas y usar la mayoría de los servicios del sistema
- **Invitados:** Usuarios con acceso muy limitado, utilizado principalmente para tareas de uso básico temporal.
### 2.10.1.2. Usuarios y grupos en Ubuntu

**Creación y gestión de usuarios y grupos en Ubuntu (interfaz gráfica)**
- En la configuración de usuarios: Configuración del sistema > Detalles > Usuarios
- Crear un nuevo usuario: Hacer click en "Desbloquear" e introducir la contraseña del administrador. Hacer click en + para crear un nuevo usuario. Introducir nombre de usuario, tipo de cuenta (administrador o usuario estándar) y la contraseña. Hacer click en añadir. 
- Asignar usuarios a grupos. Se hace desde terminal:

```shell
sudo usermod -aG nombre_grupo nombre_usuario
#Por ejemplo agregar a juan al grupo sudo
sudo usermod -aG sudo juan
```


**Creación y gestión de usuarios y grupos en Ubuntu (línea de comandos)**

```bash
# Crear nuevo usuario
sudo add user nombre_usuario
# Lo creara y pedira introducir la contraseña y detalles adicionales...
# Crear nuevo grupo
sudo groupadd nombre_grupo
# Asignar usuario a grupo
sudo usermod -aG nombre_grupo nombre_usuario
```

**Grupos comunes en Ubuntu**
- **sudo**: Susuarios con privilegios administrativos que pueden ejecutar comandos con permisos de root usando el comando `sudo`
- **adm**: Archivos del registro del sistema
- **dialout**: Pueden acceder a puertos serie y dispositivos USB

### 2.10.2. Permisos en un sistema operativo

Los permisos suelen asignarse a nivel de archivo o escritorio y se dividen generalmente en lectura, escritura y ejecución. (Como ya se vio en su momento)

**Asignar permisos en Windows 10**
- Acceder a las propiedades del archivo o carpeta
- Ir a la pestaña "Seguridad", allí hay una lista de usuarios y grupos que tienen acceso al archivo o carpeta seleccionados
- Modificar los permisos haciendo click en "Editar". Seleccionar usuarios o grupos a los que se les desea cambiar permisos. Se pueden marcar o desmarcar las casillas de control total, modificar, lectura y ejecución, lectura, escritura, entre otras opciones.
- Hacer click en agregar para asignar permisos a nuevos usuarios.
- Después darle a aplicar y luego a aceptar, para confirmar los cambios.

**Permisos comunes en Windows 10**
- **Control total**: Cualquier operación sobre el archivo, incluido cambios de permisos y toma de posesión
- **Modificar**: Cambiar contenido de archivo o carpeta
- **Lectura y ejecución**: Abrir archivos o ejecutar programas
- **Escritura**: Cambiar el contenido de los archivos o añadir nuevos archivos a una carpeta

**Permisos en Ubuntu**
Sigue modelo de tres niveles: Propietario, grupo y otros. Se gestionan generalmente desde la línea de comandos.

**Asignar permisos en Ubuntu (línea de comandos)**
```bash
# Visualizar permisos
ls -l
# Cambiar permisos
# usando el modelo usuario-grupo-mundo
# sabiendo que 4 lectura, 2 escritura, 1 ejecucion.
# r-- (4)  -w- (2)  --x (1)   rw- (6)  rwx (7)  r-x(5), etc.
sudo chmod 755 archivo
# Cambiar el propietario
sudo chown juan documento.txt
# Cambiar propietario y grupo del archivo
sudo chown juan:grupo documento.txt
```

**Asignar permisos en Ubuntu (interfaz gráfica)

- **Acceder a las propiedades** del archivo o carpeta
- **Ir a la pestaña permisos**, donde están divididos entre propietario, grupo y otros
- **Modificar permisos** usando los menús desplegables
- **Aplicar cambios haciendo clic en cerrar**

**Permisos comunes en Ubuntu
- **r (lectura):** Ver contenido de un archivo o listar un directorio
- **w (escritura):** Modificar archivo o cambiar contenido de directorio
- **x (ejecución):** Ejecutar un archivo como programa o script o acceder a un directorio

### 2.10.3. Seguridad en un sistema operativo

#### Mecanismos clave de control
La seguridad se controla a través de varios mecanismos clave:

- **Control de acceso**: Solo usuarios autorizados accedan a ciertos recursos
- **Actualización de seguridad**: Aseguran que el sistema operativo esté protegido contra vulnerabilidades descubiertas
- **Antivirus y protección contra malware**: Protege al sistema contra amenazas
- **Configuración de cortafuegos (firewalls)**: Filtra el tráfico de red entrante y saliente para evitar ataques
- **Encriptación de datos**: Protege la confidencialidad de los datos

La **buena gestión de la seguridad** implica monitorear constantemente el estado del sistema, actualizarlo regularmente y asegurarse de que las configuraciones de seguridad estén de forma óptima.

####  Importancia de la seguridad en los sistemas operativos

El sistema operativo es el núcleo que controla todo el funcionamiento. Si su seguridad se ve comprometida, todos sus datos y operaciones se ven gravemente afectados (pérdida de datos, interrupción del servicio, daños económicos y reputacionales, acceso no autorizado a información confidencial). 

- **Protección de la información**
- **Prevención de accesos no autorizados**
- **Mitigación de riesgos operatorios**
- **Cumplimiento normativo**
- **Resistencia ante ataques cibernéticos**

####  Ejemplos de casos de seguridad informática

- **Ataque Randomware WannaCry (2017)**
Afectó a más de 200000 ordenadores en 150 países. A través del sistema operativo Windows (vulnerabilidad EternalBlue) y había afectado a sistemas no actualizados. Encriptó los archivos y exigió un rescate en bitcoin para liberar datos afectando gravemente a hospitales, gobierno y empresas de todo el mundo.
¡¡Importante mantener los sistemas actualizados!!

- **Ataque a Equifax (2017)**
Equifax, importante agencia de crédito estadounidénse, se ve atacada por una vulnerabilidad no parcheada en Apache Struts. Se accedió a los datos de 147 millones de personas (números de seguridad social, direcciones, números de licencia de conducir). Por no implementar actualizaciones de software críticas.

- **Ataque Solarwinds (2020)**
Afectó a agencias gubernamentales y grandes empresas al comprometerse el software de administración de red Orion de SonarWinds, inyectando código malicioso en las actualizaciones del software. Más de 18000 clientes cargaron versiones comprometidas. Fue particularmente insidioso debido a su naturaleza en la cadena de suministro donde el software parecía legítimo.
¡¡Es importante la seguridad en todo el ecosistema de software desde el sistema operativo hasta las aplicaciones que se instalan en él!!

#### Seguridad en Windows 10

**1. Uso de Windows Defender**
Es el software de seguridad integrado en Windows para ofrecer protección en tiempo real.
Configuración > Actualización y seguridad > Seguridad de Windows > Protección contra virus y amenazas (asegurar que está monitoreando y realizando análisis regulares)

**2. Habilitar cortafuegos de Windows**
Está activado por defecto pero puede configurarse para tener mayor control del tráfico entrante y saliente. Se puede permitir o bloquear aplicaciones específicas y establecer reglas avanzadas de cortafuegos.
_Panel de control > Sistema y seguridad > Cortafuegos de Windows_

**3. Configuración de Bitlocker**
Bitlocker es herramienta de cifrado integrada en Windows que protege la información almacenada en los discos duros en caso de pérdida o robo.
_Panel de control > Sistema y seguridad > Cifrado de unidad BitLocker_.
Se puede activar para el disco deseado siguiendo los pasos para cifrarlo de tal forma que se garantizará que solo los usuarios autorizados con la clave de cifrado puedan acceder a los datos almacenados.

**4. Administración de cuentas de usuario y autenticación**
Configuración > Cuentas > Configurar contraseña fuerte, PIN, autenticación de dos factores
Desactivar las cuentas de invitado o las que no están en uso para evitar accesos no autorizados.

**5. Mantener el sistema actualizado**
Configuración > Actualización y seguridad > Windows Update
Asegurarse de que las actualizaciones de seguridad se instalan automáticamente.

#### Seguridad en Ubuntu
Ubuntu se beneficia de su estructura más segura por diseño con menos amenazas de software en comparación con Windows, pero sigue necesitando de buenas prácticas de seguridad en especial en servidores o entornos críticos.

```bash
# 1. Mantener el sistema actualizado
sudo apt update && sudo apt upgrade

# 2. Configurar cortafuegos UFW (Uncomplicated Firewall, que permite gestionar reglas de cortafuegos de Ubuntu)
sudo ufw enable
# Por ejemplo, permitamos las conexiones SSH
sudo ufw allow ssh
# Verificar estado del cortafuegos
sudo ufw status

# 3. Instalar software antivirus (opcional) como ClamAV
sudo apt install clamav
# Actualizar su base de datos
sudo freshclam
sudo clamscan -r /home

# 4. Encriptación de archivos y unidades
# Se ofrece la posibilidad en la instalación de Ubuntu de cifrar el disco completo usando LUKS. 
# Si no se hizo, pueden cifrarse directorios específicos usando herramientas como Gnome EncFS Manager o Cryptsetup
# Para cifrar con Gnome EncFS Manager, primero se instala
sudo apt install gnome-encfs-manager
# Se podran crear y gestionar carpetas cifradas a partir de la interfaz gráfica

# 5. Administración de permisos y usuarios con
chmod 
chown

# 6. Desactivar servicios innecesarios
# Listar servicios activos
sudo systemctl list-units --type=service
# Desactivar servicio
sudo systemctl disable nombre_servicio
```

### 2.10.4. Servicios y procesos

- Un **proceso** es una instancia de un programa que se está ejecutando. Se ejecuta en su propio espacio de memoria y tiene su propio estado, permitiendo que varios procesos se ejecuten simultáneamente sin interferir entre sí. La **administración de procesos** incluye el seguimiento de su estado, la asignación de recursos del sistema y la finalización de procesos no necesarios o que consumen demasiados recursos.
- Un **servicio** es un proceso que se ejecuta en segundo plano, sin interacción directa con el usuario. Da funcionalidades esenciales al sistema operativo / aplicaciones como gestión de red, impresión, actualizaciones automáticas o bases de datos. Se suelen iniciar al arrancar el sistema operativo y continúan ejecutándose mientras el sistema está en funcionamiento.

#### Diferencia entre servicios y procesos
- **Interacción con el usuario**. Procesos tienen interacción directa con el usuario y los servicios son en segundo plano
- **Inicio y gestión**: Procesos se inician y gestionan según necesidades del usuario y servicios se inician cuando el sistema arranca y funcionan continuamente hasta que se apaga. 
- **Función**: El proceso puede realizar cualquier tipo de tarea, incluida la ejecución de aplicaciones y el servicio está orientado a funciones que mantengan el sistema operativo funcionando correctamente como la gestión de redes o la seguridad.

#### Importancia de la gestión y monitorización de servicios y procesos
- **Optimización del rendimiento**: Evita que ciertos programas consuman demasiados recursos del sistema y degraden el rendimiento
- **Estabilidad del sistema**: Evita que algunos procesos o servicios se vuelvan inestables o consuman recursos de forma anormal
- **Seguridad**: Evita que existan puertas abiertas a ataques si los servicios no están configurados correctamente
- **Mantenimiento y diagnóstico**: Permite diagnosticar problemas como procesos bloqueados que están afectando al rendimiento y solucionarlos antes de que provoquen mayores fallos.

#### Gestión de servicios y procesos en Windows 10

Se gestionan  a través de herramientas integradas como el administrador de tareas y la consola de servicios (`services.msc`)

**Gestión de procesos en Windows 10**
Mediante el administrador de tareas Ctrl + Shift + Esc.  En "Procesos" se muestran todos los procesos que se están ejecutando junto con su consumo de CPU, memoria, disco y red. Puede finalizarse con "Finalizar tarea". En "Rendimiento" se ve una vista gráfica del uso de los recursos del sistema. 

**Gestión de servicios en Windows 10**
En el administrador de tareas se puede ver la pestaña "Servicios" con lista de los servicios en ejecución que pueden ser detenidos, instalados o reiniciados. 

En el cuadro de diálogo de Ejecutar (Win + R), escribiendo `services.msc` se puede acceder a la consola de servicios. Muestra una lista de todos los disponibles y pueden ser iniciados, detenidos, pausados o reiniciados y puede configurarse para iniciarse automáticamente, manualmente o desactivarlo desde las propiedades del servicio. 

#### Gestión de servicios y procesos en Ubuntu

Hay herramientas gráficas como **System Monitor**, aunque habitualmente se gestionan mediante el terminal. 

**Gestión (interfaz gráfica)**
Abriendo el Monitor del sistema (System monitor) desde el menú de aplicaciones y ver una lista de procesos en ejecución, su consumo y finalizarlo si es necesario. 

**Gestión terminal**

Se usará **systemd**, el sistema de inicio y gestión de servicios cuyo comando principal es `systemctl`

```bash
# Ver estado de un servicio
sudo systemctl status nombre_servicio
# Iniciar un servicio
sudo systemctl start nombre_servicio
# Detener un servicio
sudo systemctl stop nombre_servicio
# Reiniciar un servicio
sudo systemctl restart nombre_servicio
# Habilitar o deshabilitar servicios para que se inicien automaticamente con el sistema
sudo systemctl enable nombre_servicio
sudo systemctl disable nombre_servicio
```

### 2.10.5. Registros y logs

Los **registros o logs** son archivos donde los sistemas operativos almacenan información sobre eventos y actividades que ocurren durante su funcionamiento.
Pueden incluir detalles sobre inicio y cierre de sesión de usuarios, errores de software, mensajes del sistema, actividad de red,...
Son esenciales para monitorización, auditoría y diagnóstico de los sistemas operativos.

**Importancia de registros y logs**
- **Diagnóstico y resolución de problemas**: Identificar problemas, errores o fallos en el sistema y ver la causa. 
- **Auditoría de seguridad**: Seguimiento de las actividades y los accesos al sistema, identificación de comportamientos sospechosos. 
- **Monitoreo de rendimiento**: Identificar cuellos de botella, exceso de uso de recursos, comportamientos anómalos
- **Cumplimiento normativo**: Exigidas por la propia normativa el mantener registros detallados de la actividad del sistema.

**Diferencias de registros y logs**
- **Registros**: Logs de auditoría más formales o específicos
- **Logs**: Gama más amplia de eventos del sistema y actividades de las aplicaciones
Aunque, en la mayoría de los sistemas operativos son equivalentes.

**Aspectos clave en gestión de registros y logs**
- **Almacenamiento adecuado**: Debe asegurarse un almacenamiento eficiente, con cuidado en sistemas críticos donde las cantidades de datos puedan generar problemas de espacio.
- **Monitoreo constante**: El monitoreo en tiempo real de logs permite detectar incidentes de seguridad o fallos de forma inmediata.
- **Retención y rotación de logs**: Es necesario implementar políticas de rotación de logs que archivan o eliminan los logs antiguos después de cierto tiempo.
- **Centralización de logs**: En entornos grandes puede ser útil centralizar los logs de varios servidores o sistemas en un solo lugar para un análisis más eficiente y coherente.

**Gestionar registros y logs en Windows 10**

Windows 10 utiliza el visor de eventos (Event Viewer) para gestionar los registros del sistema.

- **Abrir el visor de eventos**. Win + X -> Visor de eventos
- **Navegar por las categorías**: **Registros de Windows** con eventos de aplicación, seguridad, configuración, sistema y eventos reenviados y **Registros de aplicaciones y servicios**
- **Ver detalles de los eventos**: Se selecciona una categoría y en el panel central se ve lista de eventos con detalles como hora, origen, categoría, nivel (informativo, advertencia, error)
- **Filtrar y buscar eventos**: Filtrar por nivel usando la opción "Buscar"
- **Archivar o eliminar logs**: "Guardar eventos como"  para archivar logs o "Borrar registro" para liberar antiguos y liberar espacio
- **Configurar auditoría de seguridad**: Acceder a los registros de seguridad que muestran eventos relacionados con la seguridad del sistema (inicios de sesión exitosos, cambios en configuraciones de seguridad, etc.)

**Gestionar registros y logs en Ubuntu**

Los logs se almacenan principalmente a través de archivos de texto que se almacena en el directorio `/var/log`

```bash
# Navegar por /var/log
ls /var/log

# Ver log especifico
cat /var/log/syslog

# Ver solo las ultimas lineas
tail /var/log/syslog

# Rotacion de logs con Logrotate (gestiona la rotacion automatica de logs, archivando, comprimiendo y eliminado logs antiguos segun configuracion definida)
# Las configuraciones de logrotate estan en /etc/logrotate.conf y en el directorio /etc/logrotate.d/
sudo logrotate -f /etc/logrotate.conf

# Monitoreo en tiempo real de logs
tail -f /var/log/syslog
```

En entornos grandes pueden **centralizar logs con rsyslog**, configurándose `rsyslog` para centralizar los logs en un solo servidor, monitorizándolos desde una única ubicación.

**Logs importantes en Ubuntu**
- `/var/log/syslog`: Registros generales del sistema, útil para la mayoría de diagnósticos 
- `/var/log/auth.log`: Eventos relacionados con autenticación como inicios de sesión e intentos fallidos
- `/var/log/dmesg`: Mensajes del Kernel útiles para resolver problemas de hardware o errores del sistema
- `/var/log/kern.log`: Específico para mensajes del Kernel

### 2.10.6. Monitorización de un sistema operativo

La **monitorización del sistema operativo** es el proceso mediante el que se observa y se registra el rendimiento, el uso de recursos y la actividad de los componentes en tiempo real o en intervalos regulares. El objetivo es asegurarse de que el sistema funciona correctamente, identificar cuellos de botella, problemas de rendimiento, incidentes de seguridad, fallos,... antes de que afecten de forma significativa a la operatividad.

**Razones de la monitorización de un sistema operativo**
- **Prevención de problemas**: Detección de anomalías antes de que produzcan fallos críticos.
- **Optimización del rendimiento**: Analizar cómo se usan los recursos, ayudando a optimizar el rendimiento al ajustar configuraciones, balancear cargas y priorizar procesos
- **Auditoría de seguridad**: Monitorizar registros de seguridad, accesos no autorizados, ataques cibernéticos,...
- **Garantía de disponibilidad**: Garantizar que los servicios (servidores web, base de datos) estén disponibles continuamente, minimizando la inactividad. 
- **Planeación de capacidad**: Anticipar necesidades futuras como la expansión de la capacidad de almacenamiento o la actualización de hardware cuando se identifica un patrón de crecimiento en el uso de recursos.

**Aspectos clave en la monitorización**
- **Métricas clave**: Identificar qué métricas deben monitorizarse para cada sistema en particular (uso de CPU, memoria, espacio en disco, actividad de red, número de procesos en ejecución)
- **Alertas**: Configurar alertas que avisen a administradores cuando ciertas métricas sobrepasen umbrales críticos permitiendo respuesta rápida ante incidentes
- **Historial y análisis**: Mantener un historial de los datos de monitorización es esencial para analizar tendencias y detectar patrones
- **Herramientas adecuadas**: Usar herramientas específicas para cada sistema que permitan monitorización efectiva y adaptada a las necesidades

**Herramientas de monitorización del sistema en Windows 10**

| Herramienta                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Administrador de tareas**:<br><br>- **Uso principal**: Monitorización básica en tiempo real del uso de recursos<br>- **Cómo acceder**: Ctrl + Shift + Esc o click derecho "administrador de tareas"<br>- **Métricas disponibles**: En "rendimiento" se puede ver el uso de CPU, memoria, disco, red y GPU en tiempo real. Muestra el número de procesos activos y los programas en ejecución que afectan al rendimiento del sistema                                                                                                                                 |
| **Monitor de recursos**:<br><br>- **Uso principal**: Vista más detallada del uso de recursos. Incluyendo procesos individuales y su imparto en CPU, disco, red, memoria<br>- **Como acceder**: En el administrador de tareas, pestaña rendimiento hay un "abrir monitor de recursos". O buscar "monitor de recursos" en el menú inicio<br>- **Métricas disponibles**: Desglosar el consumo de recursos por proceso y ver qué archivos o servicios están vinculados a esos procesos. También permite monitorear la actividad del disco y la red de forma detallada<br> |
| **Monitor de rendimiento**:<br><br>- **Uso principal**: Permite crear gráficos y recopilar datos históricos sobre rendimiento<br>- **Como acceder**: Win + R  perfmon <br>- **Métricas disponibles**: Seleccionar contadores como uso de CPU, uso de disco, actividad de red, tiempo de respuesta. Visualizarlos en tiempo real o configurarlos para ser registrados a lo largo del tiempo.                                                                                                                                                                           |
| **Visor de eventos**: <br><br>- **Uso principal**: Monitorización de eventos del sistema, seguridad y aplicaciones para ver posibles fallos.<br>- **Como acceder**: Win + X , visor de eventos<br>- **Métricas disponibles**: Registro de eventos con errores, advertencias, eventos de información y de seguridad                                                                                                                                                                                                                                                    |

**Monitorización del sistema en Ubuntu**

| **Herramientas de monitorización (Interfaz gráfica)**                                                                                                                                                                                                                                                                                                             |
| ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Monitor del sistema**:<br><br>- **Uso principal**: Monitorizar gráficamente el rendimiento del sistema<br>- **Cómo acceder**: **Monitor del sistema** desde el menú de aplicaciones<br>- **Métricas disponibles**: Gráficos en tiempo real de CPU, memoria, intercambio y red. Lista de procesos en ejecución. Posibilidad de finalizarlos desde esta interfaz. |
| **GNOME System Monitor**:<br><br>- **Uso principal**: Monitoriza recursos del sistema CPU, RAM, intercambio y red, gestión de procesos<br>- **Cómo acceder**: Ubuntu - GNOME<br>- **Métricas disponibles**: Gráficos visuales en tiempo real y gestión de procesos, similar al monitor del sistema                                                                |


| **Herramientas de monitorización (línea de comandos)**                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **top / htop**:<br><br>- **Uso principal**: Monitorización en tiempo real del uso de CPU, memoria y procesos en ejecución.<br>- **Cómo acceder**: Ejecutar comando `top`  o instalar htop más amigable (`sudo apt install htop`) y ejecutar `htop`<br>- **Métricas disponibles**: Muestra lista de procesos en ejecución, junto con consumo de CPU y memoria. Se pueden matar procesos directamente desde la herramienta (pulsa k, indica si quieres que se use la señal por defecto `SIGTERM` o la señal 9 (`SIGKILL`) para matarlo inmediatamente). |
| **vmstat**:<br><br>- **Uso principal**: Proporciona estadísticas sobre rendimiento del sistema, uso de CPU, memoria, I/O de disco, actividad del sistema<br>- **Cómo acceder**: Ejecutar `vmstat`<br>- **Métricas disponibles**: Muestra estadísticas sobre cantidad de memoria libre, carga de trabajo de la CPU, interrupciones y cambios de contexto                                                                                                                                                                                               |
| **iostat**:<br><br>- **Uso principal**: Monitoriza rendimiento del disco y de dispositivos de almacenamiento<br>- **Cómo acceder**: Ejecutar `iostat` (requiere instalar el paquete `sysstat)<br>- **Métricas disponibles**: Muestra estadísticas sobre uso de CPU y rendimiento de discos, permite identificar problemas de almacenamiento y de entrada-salida                                                                                                                                                                                       |
| **netstat**:<br><br>- **Uso principal**: Monitoriza actividad de red como conexiones activas y tráfico de red<br>- **Cómo acceder**: Ejecutar `netstat`<br>- **Métricas disponibles**: Muestra conexiones de red activas, estadísticas de interfaz de red y tablas de enrutamiento                                                                                                                                                                                                                                                                    |

(Recordatorio que no sirve para nada: Matar un proceso inmediatamente con `SIGKILL` es con `kill -9 pid_proceso`, en caso contrari oserá con `SIGTERM`)

 