La **administración de dominios** permite centralizar, simplificar y agilizar las tareas de gestión. 
Se llama **dominio** a una estructura lógica que agrupa dispositivos, usuarios y servicios bajo una única administración centralizada.

Así a la hora de administrar redes, se crea un dominio en un equipo servidor al que se conectan equipos clientes. Veamos primero en qué consiste la "estructura cliente-servidor"
## 4.1. Estructura cliente-servidor

La **arquitectura cliente-servidor** surge en los años 80 y se mantiene actualmente las redes TCP/IP. Un equipo cliente, necesita un equipo servidor para realizar alguna de las funciones asignadas.
El cliente y el servidor pueden ser, desde el punto de vista físico, equipos diferentes (¡o iguales!). Es decir, una computadora puede ser cliente y servidor a la vez dependiendo del software.

- **Cliente**: Precisa de servicios
- **Servidor:** Proporciona servicios

Desde el punto de vista lógico, el cliente y el servidor son elementos separados que establecen su comunicación mediante la red de comunicaciones y colabora para completar las tareas de forma conjunta.

El cliente hace una petición al servidor y este le da una respuesta. El servidor procesa la petición y brinda el servicio.
## 4.2. Protocolo LDAP

Se denomina **LDAP** (Lightweight Directory Access Point) a un protocolo ligero de acceso a directorios distribuidos en una red, especialmente utilizado en las empresas. Este tiene una estructura cliente-servidor que se emplea para acceder a servicios de directorio.

En sí es un protocolo, no es un software. Define cómo se organiza y accede a los datos pero no es una herramienta o aplicación.

Puede considerarse como una base de datos pensada para almacenar directorios. En la base la información se organiza de forma jerárquica de tipo árbol, similar a un árbol genealógico. Sus elementos clave son: 
- **DN** (Distinguished Name): Identificador único de cada objeto en el directorio
- **Objetos**: Entidades como usuarios, grupos o dispositivos
- **Atributos**: Propiedades de un objeto (nombre, correo, contraseña,...)

**Ejemplo de jerarquía LDAP**
```
dc=empresa,dc=com   # Dominio raíz
├── ou=Usuarios     # Unidad organizativa
│   ├── cn=Juan     # Usuario
│   ├── cn=Maria    # Usuario
├── ou=Grupos       # Unidad organizativa
    ├── cn=Admins   # Grupo
```

- **`dc`**: Domain Component.
- **`ou`**: Organizational Unit.
- **`cn`**: Common Name.

**Características y funcionalidades del protocolo LDAP**
- **Acreditación de usuarios**: Los usuarios pueden acceder a sus cuentas desde cualquier equipo en red acreditado mediante LDAP.
- **Búsqueda de datos**: Los usuarios pueden usar LDAP como una guía virtual que les da los datos de contacto de otros usuarios de forma sencilla. Usado con frecuencia en organizaciones como universidades, administraciones públicas, empresas, etc.
- **Centralización de la administración**: La gestión de cuentas de usuario y permisos asociados están centralizadas.
- **Posibilidad de replicar la base de datos**: Una vez configurada la BBDD LDAP, puede replicarse. Así, se pueden configurar diversos servidores LDAP sincronizados. Cuando la red y la cantidad de usuarios crecen rápidamente, la red puede balancear la carga entre varios servidores.
- **Gran rapidez en lectura y escritura de datos**: Esto sucede incluso cuando se da un gran volumen de accesos simultáneos. 

En definitiva, cuando uno de los clientes LDAP se conecta al servidor LDAP el cliente puede consultar o modificar directorios. Obviamente en el segundo caso el servidor verificará que el usuario cuente con permisos necesarios.

**Linux**
Puede instalarse el paquete OpenLDAP y sus utilidades con:
```shell
sudo apt-get install slapdldap-utils
```

**Windows**
Puede usarse OpenLDAP.

En cualquier caso, Microsoft se refiere a su implementación del servicio de directorio en red como **Active Directory**. Esta es una implementación propietaria de Microsoft basada en LDAP (y otros como Kerberos)


En las versiones más recientes de Windows Server, LDAP se instala por defecto conjuntamente con Active Directory.
Aunque en Windows 10 no puede instalarse Active Directory, sí puede gestionarse remotamente a través de la red mediante la aplicación Sitios y servicios de Active Directory, a través del menú Inicio.

#### Autenticación LDAP

El comando `ldapsearch` se utiliza para interactuar con servidores LDAP desde sistemas Linux.
```shell
# Estructura
ldapsearch -x -D "uid=usuario,ou=Usuarios,dc=empresa,dc=com" -W -H ldap://servidor_ldap -b "dc=empresa,dc=com"

# Ejemplo
ldapsearch -x -D "uid=juan,ou=Usuarios,dc=empresa,dc=com" -W -H ldap://ldap.empresa.com -b "dc=empresa,dc=com"
```

- `-x`: Usar una conexión simple (no segura).
- `-D`: Especifica el **DN** (Distinguished Name) del usuario para autenticar. Este es el identificador único del usuario en el directorio LDAP. Generalmente, se representa como algo así: `"uid=usuario,ou=Usuarios,dc=empresa,dc=com"`.
- `-W`: Solicita la contraseña del usuario de forma interactiva.
- `-H`: Indica la URL del servidor LDAP (por ejemplo, `ldap://servidor_ldap` o `ldaps://servidor_ldap` si usas una conexión segura).
- `-b`: Define la **base de búsqueda** dentro del directorio LDAP (por ejemplo, `"dc=empresa,dc=com"`).

Este comando pedirá la contraseña de `juan`, y si las credenciales son correctas, te devolverá una lista de atributos y valores del directorio LDAP.


--------------

Probemos en Java (por probar):
```java
import javax.naming.Context;
import javax.naming.NamingException;
import javax.naming.directory.DirContext;
import javax.naming.directory.InitialDirContext;
import java.util.Hashtable;

public class LdapAuthentication {

    public static void main(String[] args) {
        // Configuración de la conexión LDAP
        String ldapUrl = "ldap://servidor_ldap:389"; // URL del servidor LDAP (sin SSL)
        String ldapUser = "uid=juan,ou=Usuarios,dc=empresa,dc=com"; // DN del usuario
        String ldapPassword = "mi_contraseña"; // Contraseña del usuario

        // Propiedades del contexto LDAP
        Hashtable<String, String> env = new Hashtable<>();
        env.put(Context.INITIAL_CONTEXT_FACTORY, "com.sun.jndi.ldap.LdapCtxFactory");
        env.put(Context.PROVIDER_URL, ldapUrl);
        env.put(Context.SECURITY_AUTHENTICATION, "simple"); // Autenticación simple
        env.put(Context.SECURITY_PRINCIPAL, ldapUser); // Usuario (DN completo)
        env.put(Context.SECURITY_CREDENTIALS, ldapPassword); // Contraseña

        try {
            // Crear el contexto LDAP
            DirContext ctx = new InitialDirContext(env);
            
            // Si la autenticación es exitosa, se imprime este mensaje
            System.out.println("Autenticación exitosa.");
            
            // Cerrar la conexión
            ctx.close();
        } catch (NamingException e) {
            // Si las credenciales son incorrectas o hay algún error
            System.out.println("Error de autenticación: " + e.getMessage());
        }
    }
}
```


---------

Probemos en Spring

```xml
<!-- Spring Boot Starter Security (incluye Spring Security LDAP) -->
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-security</artifactId>
    </dependency>
    
    <!-- Dependencia específica para Spring LDAP -->
    <dependency>
        <groupId>org.springframework.ldap</groupId>
        <artifactId>spring-ldap-core</artifactId>
    </dependency>
```

```
# Configuración LDAP
spring.ldap.urls=ldap://servidor_ldap:389
spring.ldap.base=dc=empresa,dc=com
spring.ldap.username=uid=usuario,ou=Usuarios,dc=empresa,dc=com
spring.ldap.password=mi_contraseña
spring.security.ldap.auth.search-base=ou=Usuarios,dc=empresa,dc=com
spring.security.ldap.auth.search-filter=uid={0}
```

- **`spring.ldap.urls`**: Dirección del servidor LDAP.
- **`spring.ldap.base`**: El **base DN** de la búsqueda.
- **`spring.ldap.username`** y **`spring.ldap.password`**: Credenciales para conectar con el servidor LDAP.
- **`spring.security.ldap.auth.search-base`**: El **DN de búsqueda** para buscar al usuario.
- **`spring.security.ldap.auth.search-filter`**: El **filtro de búsqueda** para buscar al usuario, `{0}` será reemplazado con el nombre de usuario proporcionado.

```java
import org.springframework.context.annotation.Configuration;
import org.springframework.security.config.annotation.web.builders.HttpSecurity;
import org.springframework.security.config.annotation.web.configuration.EnableWebSecurity;
import org.springframework.security.config.annotation.web.configuration.WebSecurityConfigurerAdapter;
import org.springframework.security.ldap.authentication.LdapAuthenticationProvider;
import org.springframework.security.ldap.authentication.LdapAuthenticationProviderConfigurer;
import org.springframework.security.ldap.userdetails.UserSearchBean;

@Configuration
@EnableWebSecurity
public class SecurityConfig extends WebSecurityConfigurerAdapter {

    @Override
    protected void configure(HttpSecurity http) throws Exception {
        http
            .authorizeRequests()
                .antMatchers("/login").permitAll()  // Permite el acceso al login sin autenticación
                .anyRequest().authenticated()     // Requiere autenticación para otras páginas
            .and()
            .formLogin()
                .loginPage("/login")  // Página de login personalizada
                .permitAll();
    }

    @Override
    protected void configure(AuthenticationManagerBuilder auth) throws Exception {
        // Configuración de LDAP para autenticación
        auth
            .ldapAuthentication()
                .userDnPatterns("uid={0},ou=Usuarios,dc=empresa,dc=com")  // Filtro para usuarios
                .groupSearchBase("ou=Groups,dc=empresa,dc=com")  // Filtro para grupos
                .contextSource()
                    .url("ldap://servidor_ldap:389/dc=empresa,dc=com")
                    .managerDn("cn=admin,dc=empresa,dc=com")  // Usuario administrador de LDAP
                    .managerPassword("admin_password")       // Contraseña del administrador
                .and()
                .passwordCompare()
                    .passwordEncoder(new org.springframework.security.crypto.bcrypt.BCryptPasswordEncoder()) // Codificación de contraseñas
                    .passwordAttribute("userPassword");  // Atributo LDAP donde se guarda la contraseña
    }
}
```

## 4.3. Concepto de dominio. Subdominios. Requisitos necesarios para montar un dominio

La palabra dominio es polisémica en el contexto de los sistemas informáticos. Debemos diferenciar entre:
- **Dominio en redes**: Determinado grupo de ordenadores que están conectados y que han otorgado a uno de los equipos de dicha red la gestión de los usuarios, sus privilegios de acceso y otros datos.
- **Dominios en Internet**: Parte principal de una determinada dirección web (No es lo que estamos viendo aquí)

Igual sucede con la palabra subdominio.
- **Subdominio en redes**: Subgrupos o subclasificaciones dentro del dominio. Su creación implica la creación de un dominio de segundo nivel, anidado dentro del dominio primario que en Active Directory por ejemplo se denomina Bosque. La nueva estructura está relacionada con la primera pero cuenta con características propias (se usa con fines administrativos o para separar los diversos bloques de una organización)
- **Subdominio en Internet**: Hace referencia a la parte de la dirección web que antecede al dominio y que queda separado de este por un punto. Se emplea para compartimentar grandes sitios webs en diferentes áreas. También puede hacerse para pruebas y desarrollo de nuevas páginas, para no alterar la estructura básica de la web y que el posicionamiento en motores de búsqueda no se vea afectado.

### 4.3.1. Creación de un dominio de red

Para crear un dominio de red debe disponerse de un sistema operativo orientado a servidor (como Windows Server o Ubuntu Server). 

### 4.3.1.1. Windows Server
Para configurar el dominio en un Windows Server actual deben instalarse los roles necesarios para gestionar el dominio de red.

**Roles del servidor**
Al instalar Windows Server deben seleccionarse en "_Seleccionar roles de servidor_" los roles:
- Rol DNS del servidor -> "_Servidor DNS_"
- Roles AD/DS (Active Directory / Domain Services)  -> "_Servicios de dominio e Active Directory_"
- Rol DHCP -> "_Servidor DHCP_"
Todos ellos proporcionarán las funcionalidades de control que ofrecen los sistemas Windows. 

**Configurar la infraestructura del dominio**
Una vez instalados, debe configurarse toda la infraestructura del dominio.

- Configuración del servicio DNS: Estableciendo un servidor principal de dominio y un usuario administrador. El servidor y el usuario a utilizar deben tener los privilegios necesarios (**principales del bosque**, siempre que sea el primero y no una instalación dentro de un dominio ya establecido), que serán relevantes para configuraciones de escalabilidad del servicio en caso de que fuese necesario. Para finalizar la instalación, debe promoverse el servidor a controlador de dominio, donde se establecerán características como el nombre de dominio y se recomienda poner un nombre que sea concreto y orientativo (Ej.: "Midominio.local"). Para buen funcionamiento de este, debe generar las zonas de búsqueda directa e inversa en el servicio DNS.

- Configuración del servicio DHCP: Establecer el rango IP a proporcionar a los equipos clientes conectados con el servicio DHCP. 

- En esas configuraciones se realizaran todas las del dominio (reservas de direcciones, configuraciones de correo electrónico, configuraciones de usuarios del dominio,..)

### 4.3.1.2. Ubuntu Server

Para crear un dominio en Ubuntu primero se configurará el servidor DNS.
```bash
sudo apt-get install -y bind9
```

A continuación se editarán los archivos de configuración de `/etc/bind/`
- name.conf
- name.conf.options (opciones de bing y comunicación entre la red privada)
- name.conf.local (zonas de búsqueda)
- zones.rfc1918 (zonas de búsqueda)
Se deben configurar allí todos los parámetros de configuración del servicio (que dependerán de la distribución de Linux que se utilice).

En `/var/cache/bind` estarán los ficheros para configurar las direcciones de los equipos conectados al dominio. 

### 4.3.2. Creación de un dominio de Internet

Se debe contratar el servicio de alguna de las empresas que se dedica a este fin. Ej.: 1 and 1, Hostalia, ESdominios.
La administración del dominio se realiza de manera remota, a través del navegador web con la información proporcionada por la empresa a través de la que se contrata el servicio.

## 4.4. Conceptos clave de Active Directory

Dentro de esta herramienta de Microsoft para gestionar servidores y administrar en ellos usuarios, grupos, etc. se deben conocer los siguientes conceptos clave:
- **Directorio**: Repositorio en el que se guarda toda la información referente a usuarios, grupos, recursos, etc.
- **Objeto**: Cualquiera de los componentes que conforman el directorio (usuarios, grupos, impresoras, carpetas compartidas,...). Cada objeto puede tener sus características y un nombre que permita identificarlo.
- **Dominio**: Conjunto de objetos dentro del directorio que conforman un subconjunto administrativo. Dentro de un **bosque** puede haber varios dominios. Cada uno de ellos puede tener su propio conjunto de objetos y unidades administrativas.
- **Controlador de dominio**: Comprende el conjunto de objetos del directorio para un determinado dominio. Es decir, en un determinado dominio puede haber varios controladores de dominio. 

> - El **controlador de dominio** (dc) es el servidor que **gestiona** el acceso a los recursos dentro de ese dominio. Su tarea principal es almacenar la base de datos de **Active Directory** (si estamos hablando de un entorno Windows) o una estructura equivalente, que contiene la información sobre los usuarios, grupos, computadoras y demás recursos dentro del dominio.
> - Además, se encarga de la **autenticación** de los usuarios, verificando que sus credenciales sean correctas cuando intentan acceder a los recursos del dominio.
> - En un **dominio** pueden existir **varios controladores de dominio**. La razón de esto es la **redundancia** y la **disponibilidad**.
> - **Todos los controladores de dominio** en un dominio tienen una copia de la base de datos de **Active Directory** (o la estructura de datos correspondiente). Estos controladores se **replican entre sí** para mantener la consistencia de los datos. Es decir, si un usuario es agregado o modificado en un controlador de dominio, esa información se replica en los demás controladores del dominio.
> - si tienes **varios controladores de dominio**, uno en cada sucursal, cuando un usuario en una sucursal intenta iniciar sesión, el controlador de dominio local se encargará de autenticarlo. Si ese controlador de dominio tiene algún problema, el usuario podrá ser autenticado por un **controlador de dominio en otra ubicación**, ya que la base de datos se replica entre todos los controladores.

- **Árboles:** Son conjuntos de dominios relacionados dentro del bosque que comparten un espacio de nombres jerárquico, poseen una raíz común. Se organizan jerárquicamente y su jerarquía se refleja en los nombres. Por ejemplo los dominios "todo.es" y "parte.todo.es" forman parte del mismo árbol. Sin embargo, "otraparte.es", no forma parte de ese árbol.

- **Bosque:** Acabar todos los dominios dentro de su ámbito, que están interconectados por relaciones de confianza. Todos los dominios de un bosque confían automáticamente entre sí y los distintos árboles pueden compartir recursos entre sí. Un bosque contiene siempre al menos un dominio, que ejerce de raíz del bosque.

>- Un **bosque** es el nivel más alto de organización en una estructura de **Active Directory** (AD). Es un conjunto de **uno o más dominios** que están relacionados entre sí mediante relaciones de confianza y comparten una misma configuración global. Todos los dominios dentro de un bosque tienen una **relación de confianza bidireccional automática**. Esto significa que los usuarios autenticados en un dominio pueden acceder a recursos en otros dominios del mismo bosque, siempre y cuando tengan los permisos adecuados.
>- Un árbol puede tener el dominio raíz `empresa.com` y subdominios como `ventas.empresa.com`.
> - Otro árbol en el mismo bosque puede tener un dominio raíz como `corporativo.org` con subdominios como `ti.corporativo.org`.

- **Unidades organizativas:** Son contenedores de objetos que permiten organizarlos jerárquicamente en subgrupos dentro del dominio. Se pueden definir estructuras lógicas que faciliten la organización y hagan que la administración sea más sencilla.

- **Relaciones de confianza:** Método de comunicación entre dominios, árboles y bosques que reige la seguridad de la red. Gracias a ellas, los usuarios de Active Directory pueden autenticarse en otro dominio del directorio. Las relaciones de confianza pueden ser:
	- **Unidireccionales**: En una única dirección
	- **Bidireccionales**: En ambas direcciones
	- **Transitivas**: La confianza se propaga. "Si Uno confía en Dos y Dos confía en Tres, se deduce que Uno confía en Tres".

- **Delegación de control entre dominios:** Permite a los usuarios de un dominio administrar recursos de otro dominio. Para ello se necesita que entre los dos dominios se haya establecido una relación de confianza. La delegación de control solo se realizará a usuarios en los que se confíe plenamente.

En Active Directory se pueden establecer distintos tipos de grupos. Estos se emplean para reunir a usuarios, equipos y otros tipos de cuentas en entidades administrativas.

## 4.5. Administración de cuentas. Cuentas predeterminadas

**Active Directory**
Una vez creado el directorio en Active Directory, interesa crear las cuentas de usuario para asignarlas a las distintas personas que van acceder a la red.

Las cuentas de usuario son elementos de una base de datos de directorio a los que se les asigna de forma automatizada unos identificadores para garantizar la seguridad. Tras dar de alta a los usuarios, estos pueden acceder y utilizar los recursos del dominio que tengan asignados. 

**Las cuentas se pueden gestionar** en Server Manager > Local Server.
Las acciones de agregar y eliminar usuarios se llevan a cabo en el apartado "Usuarios y equipos de Active Directory"
Esta herramienta del sistema permite gestionar usuarios y grupos de forma muy parecida a las versiones de cliente de Windows.

**También se pueden gestionar desde ese apartado** los equipos enlazados al dominio u otros servidores que gestionen la red. 

Al instalar el sistema operativo se generan unas cuentas predeterminadas al crear el dominio. En el listado de usuarios del Centro de administración de Active Directory de Windows Server se encuentran tres cuentas predterminadas:
- Administrador
- Invitado
- Asistente de ayuda
La instalación de los servicios de red y de dominio crea grupos de usuario por defecto y se les asigna un usuario administrador que tendrá los privilegios de este tipo de usuario en todo el dominio.

Las cuentas de usuarios del dominio suelen estar vinculadas a ciertos equipos para mejorar el rendimiento de la red, aunque con ellas podemos acceder a cualquier equipo que esté conectado al dominio, teniendo los permisos necesarios. (Estaciones de trabajo de inicio de sesión: El usuario puede iniciar sesión en Todos los equipos / Los siguientes equipos)

----

**Linux**

Respecto a añadir usuarios ya se han comentado los comandos
```bash
# Crear cuenta de usuario
sudo adduser usuario
# Eliminar cuenta de usuario
sudo deluser usuario
```

## 4.6. Contraseñas. Bloqueos de cuenta. Cuentas de usuarios y equipos

Cuando una persona que usa la red (que tiene Active Directory) inicia sesión en el dominio, se comprueban sus credenciales en el directorio.
Tienen su nombre de usuario y su propia contraseña. Si varios usuarios comparten una misma cuenta, su seguridad queda comprometida.

(Active Directory > Configuración de seguridad local > Directiva de bloqueo de cuentas). Para impedir infinitos intentos de acceder, se pueden definir una serie de parámetros que bloquearán el acceso cuando se cumpla una condición. (Umbral de bloqueos de cuenta). Por ejemplo, se puede definir que a los tres intentos de Inicio de sesión la cuenta quede bloqueada.
Otros parámetros como "Duración de bloqueos de cuenta" o "Restablecer la cuenta de bloqueos después de", permitirán restaurar la cuenta pasado un tiempo. 
También se puede bloquear si el usuario mantiene su sesión iniciada demasiado tiempo, etc.

## 4.7. Perfiles móviles y obligatorios

Los perfiles permiten asignar características como archivos y carpetas que usan los usuarios y su configuración del escritorio.
Los perfiles por defecto suelen ser locales, es decir, se generan en el equipo en el que el usuario inicia sesión.  (C:\Usuarios\nombre_usuario)

Pueden crearse **perfiles móviles** que consisten en que el usuario tenga acceso a su perfil, independientemente del equipo en el que inicie sesión. Así se evita configurar aplicaciones, dispone de sus documentos, etc. 
Para ello el perfil se almacena en un directorio del servidor de modo que quede compartido en red. (Apartado Usuarios y equipos de Active Directory. 
Propiedades > Perfil > Ruta de acceso al Perfil) y se escribe ahí la información de la ubicación de la información.

Los **perfiles obligatorios** se definen por el hecho de ser de solo lectura y solo poder ser modificado por un administrador (cuando el usuario inicie sesión se cargará su perfil pero no se guardará ninguna configuración o dato cuando este cierre sesión). 

Si se quiere que el perfil móvil sea obligatorio, al introducir la información correspondiente a la ruta de acceso en el perfil se le agrega la extensión `.man`. 
Para convertir un perfil móvil en un perfil obligatorio se accede al archivo `ntuser.dat` y se le cambia la extensión por `ntuser.man`.
## 4.8. Carpetas personales

También puede crearse en el servidor un directorio general en el que cada usuario almacene su información personal en una subcarpeta de trabajo propia (que, a menudo, tendrá su nombre). 
Este espacio compartido frecuentemente aparecerá en los equipos cliente como una unidad de red.

Estas carpetas personales se asignan en Windows Server desde Usuarios y equipos de Active Directory. En el Perfil de los usuarios, se activa la opción Carpeta particular y se elige la carpeta.

Para que el usuario vea el área de almacenamiento compartido que se le ha asignado en el servidor como una unidad de almacenamiento en su árbol de directorios local, se hace clic en Conectar y se selecciona una letra de unidad (por ejemplo "Z").

Los directorios que se indiquen para los usuarios del dominio han de ser, lógicamente, recursos compartidos del servidor.

Estos directorios son visibles para los usuarios que se indiquen, aunque se podrían asignar directamente a grupos de usuarios para agilizar el proceso. Los permisos deben ser muy bien definidos ya que por defecto vendrán con control total. 
## 4.9. Plantillas de usuario. Variables de entorno

**Plantillas de usuario**
Las **plantillas de usuario** permiten definir una serie de características comunes que posteriormente pueden aplicarse a un gran número de usuarios, ahorrando gran cantidad de trabajo. 
Ej.: Se crea una plantilla de usuario etiquetada como Marketing, se rellenan sus datos y es aplicada a todos los usuarios del departamento de marketing.

En Windows se hace una vez más desde Usuarios y equipos de Active Directory. Se crea un nuevo usuario **y se marca la casilla que desactiva la cuenta ya que va a emplearse como una plantilla**. 

Una vez creados los usuarios, se accede a sus propiedades y se asignan el perfil que se ha definido.

**Variables de entorno**
Las **variables de entorno** forman un conjunto de valores que se ejecutan al inicio de la sesión del usuario y afectan al comportamiento de comandos y procesos.

Por ejemplo la equivalencia `%TMP%`, que lleva a `\\Users\Nombre_usuario\AppData\Local\Temp` está definida por una variable de entorno.
Las variables de entorno pueden editarse en Windows Server mediante Administración de equipos > Administración del equipo > Propiedades > Opciones avanzadas > Variables de entorno > Configuración.

**Windows**
Las variables de Windows más comunes son:
- `%APPDATA%`: Directorio de las carpetas ocultas para datos de aplicaciones
- `%USERPROFILE%`: Directorio del usuario de la sesión
- `%WINDIR%`: Ruta por defecto de instalación de Windows
- `%PROGRAMFILES%`: Directorio que almacena la instalación de los programas
- `%TIME%`: Hora actual del sistema
Los usuarios del sistema pueden editar y crear variables de este tipo. Determinados programas también necesitan crearlas para gestionar sus recursos. 

**Linux**
En el caso de Linux se encuentran:
- `SHELL`: Ruta al intérprete de comandos
- `LANG`: Idioma del sistema
- `HOME`: Directorio actual del usuario
Dichas variables se modifican desde tres archivos de texto del sistema:
`/etc/environment`:  Variables independientes del intérprete de comandos
`/etc/profile`: Variables válidas para todas las shells interactivas que exijan login. Para definir solo variables de usuario, el directorio es en `~/.bash_profile`
`/etc/bash.bashrc`:  Variables válidas para todas las shells interactivas no logueadas. Para definir variables de usuario el directorio es en `~/.bashrc`.

```shell
# Definir variable temporal solo para la sesión actual 
export MI_VARIABLE="valor"
# Definir alias temporal
alias nombre_alias="comando"
```

**Variable permanente**
Edita el archivo de configuración del shell:
- **Para Bash**: `~/.bashrc` o `~/.bash_profile`
- **Para Zsh**: `~/.zshrc`
Agrega la línea:
`export MI_VARIABLE="valor"`

Luego, aplica los cambios:
`source ~/.bashrc`

**Alias permanente**
`alias nombre_alias="comando"`

Luego, aplica los cambios.
`source ~/.bashrc`

## 4.1.0 Administración de grupos. Tipo. Estrategias de anidamiento. Grupos predeterminados

La gestión de grupos se lleva a cabo mediante Usuarios y equipos de Active Directory.

**Tipos de grupos**
Se distingue entre:
- **Grupos de distribución**: Pensados solamente para usarlos con aplicaciones de correo electrónico.
- **Grupos de seguridad**: Para administrar permisos de acceso a los diversos recursos de la red

También se pueden clasificar según el ámbito entre:
- **Grupos de ámbito universal**: Pueden usarse en cualquier parte de un mismo bosque. Tras definir un grupo universal se le pueden asignar usuarios, anidarlos y usar listadas de control de acceso para definir permisos.
- **Grupos de ámbito global**: Pueden usarse en cualquier dominio, pero sus miembros solo pueden hacer acciones en el dominio en el que está dado de alta el grupo global.
- **Grupos de ámbito local:** Los miembros pueden realizar acciones en cualquier dominiom, pero sus permisos solo son efectivos para recursos del dominio con el que fue creado el grupo. 

> ## **Ámbitos de Grupos en Active Directory**
>
> **Grupos Universales (Universal Groups)**
    - **Uso**:
        - Diseñados para **gestionar permisos en todo el bosque** (o incluso entre bosques con relaciones de confianza).
        - Utilizados para agrupar usuarios y grupos de **múltiples dominios**.
    - **Características**:
        - Los **miembros** pueden ser usuarios o grupos de cualquier dominio dentro del bosque.
        - Requieren que los controladores de dominio actúen como **Catálogo Global** (Global Catalog) para almacenar y replicar estos grupos.
        - Ideales para permisos que afectan a varios dominios.
    - **Ejemplo**:
        - Un grupo llamado `TodosRRHH_Universal` agrupa a los usuarios de Recursos Humanos de varios dominios para gestionar permisos en recursos compartidos globales, como una aplicación empresarial.
>
> **Grupos Globales (Global Groups)**
    - **Uso**:
        - Diseñados para **agrupar usuarios de un mismo dominio**.
        - Utilizados para **asignar permisos en otros dominios** del bosque.
    - **Características**:
        - Los **miembros** solo pueden ser usuarios o grupos del mismo dominio.
        - **Permiten ser miembros** de otros grupos (como grupos locales del dominio) en cualquier dominio del bosque.
    - **Ejemplo**:
        - Un grupo llamado `Ventas_Global` contiene todos los usuarios del departamento de ventas en un dominio. Este grupo puede ser añadido como miembro de un grupo local del dominio en otro dominio, otorgando acceso a recursos externos.
>
>
>  **Grupos Locales del Dominio (Domain Local Groups)**
    - **Uso**:
        - Diseñados para **gestionar permisos dentro de un dominio específico**.
        - Utilizados principalmente para otorgar acceso a recursos específicos (como carpetas compartidas, impresoras, etc.) dentro del dominio.
    - **Características**:
        - Los **miembros** pueden ser de cualquier dominio del bosque, incluso de otros bosques o de directorios externos (como cuentas externas o grupos).
        - **Asignación de permisos**: Recursos locales del dominio.
    - **Ejemplo**:
        - Un grupo llamado `ImpresorasHR_Local` se usa para dar acceso a la impresora en el departamento de Recursos Humanos dentro de un dominio específico.

**Resumidísimo**
>- **Grupos Locales del Dominio**:
    - Otorgan acceso a **recursos dentro de un dominio específico**.
    - Pueden incluir usuarios y grupos de cualquier dominio.
>- **Grupos Globales**:
    - Agrupan usuarios del **mismo dominio**.
    - Sirven para asignar permisos en **otros dominios**.
>- **Grupos Universales**
    - Agrupan usuarios y grupos de **múltiples dominios**.
    - Se usan para recursos a nivel de **bosque** o global.

Para una mejor gestión en Active Directory está el "Centro de administración de Active Directory" que tiene una interfaz gráfica amigable para gestionar los parámetros a aplicar en los grupos. 

**En Windows hay una serie de grupos creados de forma predeterminada:**
- Administradores
- Operadores de copia de seguridad
- Operadores criptográficos
- Usuarios de COM distribuido
- Invitados
- IIS_IUSRS
- Operadores de configuración de red
- Usuarios del registro de rendimiento
- Usuarios del monitor del sistema
- Usuarios avanzados
- Usuarios de escritorio remoto
- Replicador
- Usuarios
- Ofrecer aplicaciones auxiliares de asistencia remota

**Linux**
En Linux no hay mucho que decir. Por interfaz gráfica o por consola.
```shell
# Crear grupo
sudo addgroup nombreGroup
# Borrar grupo
sudo delgroup nombreGroup
```

**Anidamiento**
Los grupos pueden anidarse entre sí. Consiste en hacer un grupo miembro de otro, detal modo que utilice sus características.
## 4.11. Instalación de Windows Server y Ubuntu Server

**Windows Server 2019:**
1. Configuramos la BIOS para que se inicie desde el DVD.
2. Insertamos el disco de instalación de Windows Server 2019 y reiniciamos el PC.
3. Al iniciar, seleccionamos el idioma de la instalación.
4. Elegimos Instalar.
5. Elegimos la edición de Windows 2019.
6. Aceptamos la licencia del contrato.
7. Llegado este momento, podemos elegir entre Modo Recomendado o Modo Avanzado. Elegimos Modo Avanzado.
8. A continuación, llega el momento de elegir la partición del disco donde instalar el sistema operativo. Si queremos hacer la partición, entonces elegimos Nuevo, Tamaño de la partición y Formatear.
9. A partir de este paso, se instalará el sistema operativo y por último tendremos que reiniciar.
10. Escribimos la contraseña para el usuario administrador. Una vez iniciada la sesión, ya podemos empezar con la configuración básica de la administración del servidor.

**Ubuntu Server 20**
1. Configuramos la BIOS para que se inicie desde el DVD.
2. Insertamos el disco de instalación y reiniciamos el PC.
3. Al iniciar, seleccionamos el idioma, país y la zona horaria.
4. Elegimos el Hostname.
5. Creamos la cuenta para usuario y su contraseña.
6. Elegimos el cifrado de la carpeta.
7. Ahora llega el momento de elegir el particionado del disco.
8. Le damos a Instalar.
9. Elegimos la configuración de las instalaciones.
10. Configuramos el gestor de arranque.
11. Hecho esto, GRUB se instalará en el sector de arranque de la partición.
12. Tras reiniciar el PC y entrar por primera vez con la cuenta administrativa, actualizamos el sistema tecleando lo siguiente:
```shell
sudo apt-get update
sudo apt-get upgrade
```
Hecho esto el sistema ha quedado instalado. Ya puede modificarse el archivo `/etc/hosts` para configurar Ubuntu Server como servidor.
