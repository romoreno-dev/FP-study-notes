
## 5.1. Equipos de dominio

En el Active Directory de un determinado dominio es donde se conserva aquella información referente a las cuentas de usuarios y grupos globales. 
Con los dominios de red se pueden centralizar recursos y administrarlos con más facilidad. 
Aunque hasta ahora se ha visto una estructura cliente-servidor (un servidor al que se conectan varios clientes), es claro que esta estructura puede complicarse bastante si, por ejemplo, se tiene que sincronizar entre dos servidores.

En un dominio cada elemento se representa como una entidad individual a la que se le pueden asignar unos atributos. Estos elementos pueden contenedor otros elementos y es la unión de todo esto la que define el esquema de dominio y forma parte de su equipamiento.

**Elementos del dominio**
Entre sus elementos podemos mencionar:
- **Equipos y recursos físicos:** Forman parte del hardware (ordenadores, impresoras, escáneres, monitores)
- **Recursos lógicos**: Todo elemento lógico administrado por el dominio (directorios de trabajo compartidos en la red)
- **Usuarios y grupos:** Personas que se gestionan  a través el dominio y son parte del sistema
- **Servicios**: Administración de correo electrónico, acceso a FTP,..

## 5.2. Permisos y derechos

En Active Directory se establece cómo va a acceder al sistema cada usuario y grupo y las características particulares de dicho acceso.

**Derechos (Privilegios)**
Los **derechos** son los atributos que se asignan a usuarios y grupos para acceder al sistema y tener control sobre características particulares de cada acceso. Se especifica qué acciones pueden autorizar a llevar a cabo los usuarios y los grupos. (Inicio de sesión, copias de seguridad, etc.)

Aparece en Active Directory como **Derecho de usuario o Userright**

**Permisos**
Los **permisos** son el derecho o características con las que puede accederse a un recurso compartido dependiendo del usuario o grupo. En el caso de los recursos el dominio concede o deniega el acceso y establece cómo debe llevarse a cabo. (lectura, modificación, ejecución, eliminación,...)

## 5.3. Administración del acceso a recursos. Samba. NFS

Hay más posibilidades en la administración el acceso a recursos además de Usuarios y equipos de Active Directory.

### 5.3.1. Samba

Programa de libre implementación que suele usarse en sistema de tipo Unix. Por ejemplo sistemas de tipo Linux permiten instalarlo para **proporcionar sus servicios a clientes basados en Windows**. (Software que permite que equipos Linux se muestren como servidores o ejerzan de clientes en redes Windows) Mediante Samba se puede llevar a cabo una administración completa de los servicios de archivos y de impresión.

Soporta listas de control de acceso, se pueden especificar los derechos y permisos de los usuarios a través de:
- Linux: Del propio servidor Linux
- Windows: De una interfaz gráfica o de la herramienta Winbindd que también permite. 

Samba dispone de una base de datos propia de usuarios. Como usan recursos del servidor es necesario que estén dado de alta en Linux (deben disponer cuenta en Linux y cuenta en Samba). 

Los usuarios en Samba se gestionan mediante **smbpassws**
```shell
# Creacion de usuario Samba
sudo smbpasswd -a <usuario>
# Eliminar usuario Samba
sudo smbpasswd -x <usuario>
# Deshabilitar usuario Samba
sudo smbpasswd -d <usuario>
# Habilitar usuario Samba
sudo smbpasswd -e <usuario>
# Manual Samba
man smbpasswd
```

**SWAT**
SWAT (Samba Web Administration Tool) es la herramienta de administración web de Samba que permite configurar Samba en modo gráfico. Aunque es más sencillo hacerlo con el programa Webmin o editan el fichero `smb.conf`
### 5.3.2. NFS

El **sistema de archivos en red** (NFS, Network File System) es un protocolo, herramienta que se utiliza para configurar redes basadas en un servidor de dominio cuando se emplea Linux.

Consta de dos partes: servidor y cliente. Con él se puede conseguir que los ordenadores pertenecientes a una red local accedan a archivos remotos de forma transparente, tal que a nivel de usuario los perciban como usuarios locales.
NFS participa en estructura cliente-servidor: Clientes acceden de forma remota y a través de la red a información almacenada en el equipo servidor. 

## 5.4. Permisos de red. Permisos locales. Herencia. Permisos efectivos

Los equipos administrados a través de la red puede compartir sus recursos con los demás ordenadores tanto si son del propio servidor, como si son clientes o estaciones de trabajo. No solo desde el servidor pueden asignarse permisos, sino que también desde las estaciones de trabajo pueden definirse localmente con la opción "Compartir".
Ahí se pueden definir las características del nuevo recurso compartido:
- Nombre: Nombre que se asigna al recurso elegido y que no tiene por qué coincidir con el que tiene. 
- Usuarios: Usuarios que podrán acceder al recurso
- Permisos: De lectura, escritura, etc.

Cuando se trabaja con red que tiene Active Directory probablemente se hayan definido permisos desde el servidor y se hayan dado a los usuarios que vayan a acceder a la red.
¿Qué sucede en este caso? Que **solo los usuarios que cumplan los requisitos definidos en el servidor y los requisitos definidos cliente tendrán acceso a la carpeta compartida y podrán realizar acciones sobre su contenido**

La sección **Permisos efectivos** de **Configuración avanzada** lista los permisos que se concederán al grupo o usuario seleccionado, atendiendo a los permisos concedidos a través de la pertenencia a un grupo.

Para saber cuáles son los permisos más efectivos deben tenerse en cuenta los factores:
- **Grupo general**: Grupo general al que pertenece y los permisos en él
- **Grupo local**: Grupo local al que pertenece y los permisos en él

En cualquier caso, el acceso a los recursos compartidos se puede denegar mediante los permisos de recurso compartido. 
Cuando se usa la sección **Permisos efectivos** para tratar de determinar qué permisos tiene un usuario para acceder a un recurso determinado del dominio ,tal vez los resultados que se muestren en la ventana no equivalgan a las autorizaciones reales con las que cuenta el usuario para el recurso (suele darse cuando se ejecutan herramientas administrativas de manera remota desde el servidor de recursos)

Para prevenir estas incoherencias debe comprobarse de forma local cuáles son los permisos efectivos en el equipo que hospeda el recurso. Debe confirmarse que la cuenta de administrador que se usa está en el mismo dominio que el recurso.

Considerar también: Que los permisos se propagan desde los elementos que se administran, influyendo en sus elementos primarios (permisos heredados). Debe tenerse en cuenta para que la asignación de permisos mantenga una coherencia.

Por ejemplo en Active Directory, los permisos heredados se distinguen porque al examinar los permisos de un elemento, sus casillas de verificación aparecen sombreadas: Ha heredado permisos del elemento principal (directorios se estructuran en forma de árbol).
A partir de ahí, para que los permisos se adecúen a lo que necesite se puede:
- Cambios de configuración en el elemento principal que brinda la herencia, luego el secundario heredará sus permisos
- Configuración directa del permiso: Puede elegir "Permitir" o "Denegar" para reemplazar el permiso heredado
- Eliminar la herencia: Desactivaremos la casilla de verificación etiquetada como "Heredar" del objeto principal y las entradas de permisos relativas a los objetos secundarios. En adelante, el elemento dejará de heredar permisos del objeto principal.
## 5.5. Delegación de permisos

El administrador tiene permisos previos y a los usuarios se les conceden solo los necesarios para completar sus tareas.

La **delegación de permisos** es un mecanismo mediante el cual se concede a un usuario determinado o a un grupo completo el permiso para realizar una operación particular. 

La delegación puede llevarse a cabo por distintas vías, siendo la más habitual la delegación por pertenencia a un grupo. Si englobamos a un usuario sin permisos en un grupo que tenga permisos, este los adquiere por delegación.

La característica de delegación frecuentemente se puede configurar. En Windows Server se realiza mediante la Consola de administración de directivas de grupo (GPMC). Al desplegar Objetos de directiva de grupo en el dominio que contiene el elemento al que se desea añadir o quitar permisos, se hará clic en GPO. El apartado Delegación permitirá ajustar la característica. 

## 5.6. Listas de control de acceso (ACL Access Control List)

Las **listas de control de acceso** se utilizan para asignar permisos de forma habitual. Con ellas se pueden asignar permisos a otros usuarios distintos al propietario y a grupos que no sean el propio grupo al que pertenece el propietario.

También se pueden usar para filtrar el tráfico en lo referente a la seguridad informática. Desde su configuración es posible realizar tareas como:
- Aumentar el rendimiento de la red limitando el tráfico. Ej.: Política corporativa que no permita la reproducción e vídeos, que consume tráfico de red
- Configurar el acceso de un host a una determinada área de la empresa y evitar que cualquier otro hosts acceda a ella
- Bloquear el tráfico de redes sociales y limitar solo al tráfico de correo electrónico
- Permitir a diferentes usuarios acceder a determinados tipos de archivos.

Además de lo hablado de los permisos de Lectura, Escritura y Ejecución, en las redes de sistemas Linux ya sabemos que hay tres figuras que son el Owner, Group, Other. 

Por regla general, si se estructuran usuarios y grupos de forma correcta en el servidor, esto como administrador será suficiente para que cada usuario tenga el acceso que precisa y nada más. Si hay escenarios más complicados se pueden acudir a otras alternativas.

**Caso práctico**
>Imaginemos que disponemos de un servidor que ejecuta
Windows Server y que deseamos sustituirlo por uno que
ejecutará Ubuntu.
>
>En nuestro supuesto, parte de los equipos clientes conectados
a la red seguirán ejecutando Windows, pero en adelante será el servidor Linux el que les proporcioneservicios de impresión, de servidor de archivos, etc. Este escenario complica las asignaciones.
>
Gracias a Samba podemos habilitar listas de control de acceso. De este modo, podemos asignar permisos de manera mucho más dinámica, porque a las tres figuras que hemos listado en relación con los archivos, se les agregan nuevas
posibilidades:
>
Las que ya habíamos visto:
Owner
Group
Other
>
Se le pueden añadir:
Usuarios específicos: podemos agregar usuarios que tendrán acceso al recurso a nivel individualizado. Es más, podemos decidir qué permisos tendrán.
Grupos específicos: en esta sección podemos agregar un listado de grupos.
>
En definitiva, las listas de control de acceso amplían los elementos a los que asignar permisos hasta cinco.

Para poder usar las listas de control de acceso en Linux deben cumplirse dos condiciones:
- **Soporte por parte del kernel de Linux de nuestra instalación**
- **Soporte por parte del sistema de archivos**: El sistema de archivos debe montarse con el atributo ACL. 
## 5.7. Directivas de grupo. Derechos de usuarios. Directivas de seguridad. Objetos de directiva. Ámbitos de las directivas. Plantillas

Las **directivas de grupo** son propias de Windows Server y permiten especificar un conjunto de reglas que se van  aplicar de forma general a las cuentas de usuario y a las de equipo.

Es un mecanismo orientado a la simplificación de Active Directory, gracias al cual puede ejercerse un control sobre lo que pueden y no pueden hacer los usuarios. Permiten definir sus derechos y ampliar la seguridad.

Se usan frecuentemente en redes de dimensiones modestas y, de hecho, no tendría por qué usarse Active Directory.

En Windows 10 puede accederse con el comando `gpedit.msc`. Esto abre el "Editor de directivas de grupo local". En el panel izquierdo muestra los elementos u objetos sobre los que se puede actuar para asignar o general derechos. 

Si se escribe: 
`{gpedit.msc /gpcomputer: “nombreDeEquipo”}`
El objeto de la directiva de grupo es "nombreDeEquipo" (local)

Si se escribe:
`{gpedit.msc /gpcomputer:”nombreDeEquipo.dominio.com”}`
El objeto de la directiva de grupo se refiere a la almacenada en Active Directory

**Plantillas**
En las herramientas para editar directivas de grupo se permite crear y editar plantillas en las que se pueden compendiar características que luego se aplicarán mediante su asignación en bloque, facilitando el trabajo. 