(UF3 Aplicaciones Web)

(Página 57)
## 1. DNS. Resolución de nombres. Proceso de resolución de un nombre de dominio

El DNS (Domain Name System) es un sistema de nomenclatura jerarquico descentralizado para dispositivos conectados a redes IP. Su función más importante es la **resolución de nombres:** traducir los nombres en direcciones IP de los equipos conectados a la red.

Se trata de un servicio cliente/servidor aunque se diferencia de otros en que estos se ejecutan por sí mismos sin necesidad de una aplicación exterior. 

Cuando una aplicación pide conectarse con un dispositivo remoto por nombre, el cliente DNS solicitante manda una petición a uno de los servidores DNS para resolverla. 

El servidor DNS usa una base de datos distribuida y **jerárquica**. Si consideramos una URL `http://www.google.es` se ve que los puntos separan dominios y subdominios comenzando desde derecha a izquierda (dominios de primer, segundo, tercer nivel,...):
- `.es`: Dominio de primer nivel. Servidor español.
- `google`: Subdominio. Dominio de segundo nivel bajo `.es`
- `www`:  Subdominio. Dominio de tercer nivel que identifica el equipo donde está catalogada la página web. Es el dominio www que el servidor DNS redirecciona a la IP del servidor web.
Por su parte `http://` es el protocolo que permite la visualización en el navegador.

Los dominios deben cumplir los siguientes requisitos:
- Solo estar compuestos  de letras, números y guiones
- No empezar y terminar en guiones
- Tener menos de 63 caracteres y tener más de uno o dos (según el dominio de primer nivel)

### 1.1. Funcionamiento del servicio DNS

1. El navegador solicita "[www.midominio.com](http://www.midominio.com)".
2. El sistema operativo consulta primero el archivo `hosts` en busca de una entrada correspondiente.
    - Si se encuentra una entrada como **"192.168.1.10 [www.midominio.com](http://www.midominio.com)"**, el sistema utiliza esa IP.
3. Si no se encuentra una entrada en el archivo `hosts`, el sistema realiza una consulta al **servidor DNS** configurado (por ejemplo, el servidor DNS de tu proveedor de Internet o uno público como Google DNS o Cloudflare DNS). Si lo tiene cacheado, responde con la IP. Si no, comienza su consulta a los DNS. 
4. **Raíz del DNS (Root DNS Server)**. Los servidores root están en la parte más alta de la jerarquía DNS. Existen 13 servidores root DNS distribuidos globalmente. No conocen la IP pero saben qué servidores tienen la autoridad para resolver los dominios de primer nivel (.com, .org, net).  ("No sé quien es www.midominio.com pero te diré qué servidor sabe resolver dominios.com" --> Redirecciona a servidor TLD)
5. **Servidor TLD (Top-Level Domain server)**. Gestiona dominios de primer nivel (.com, .org, .net). Ante la consulta de www.dominio.com el servidor TLD responde con la dirección de servidores authorizative para ese dominio
6. **Servidores Autoritarios (Authorizative DNS servers)**: Tienen la información definitivba del dominio. Almacenan los registros DNS (como registro A que asocia el dominio con una IP), este responde con la dirección IP de www.midominio.com.

![[Pasted image 20250313001842.png]]
```css
[Tu navegador] ---> [Resolver DNS] ---> [Root DNS Servers] ---> [TLD DNS Servers (.com, .org, etc.)] ---> [Authoritative DNS Servers] ---> [IP Address]
```

Los **registros DNS** son entradas dentro de los servidores autoritativos que proporcionan la información sobre cómo traducir un dominio a una IP. Los más comunes son:

- **Registro A**: Asocia un dominio con una dirección IP (para sitios web).
- **Registro MX**: Asocia un dominio con servidores de correo electrónico.
- **Registro CNAME**: Permite alias en los dominios.
- **Registro NS**: Indica qué servidores DNS son responsables de un dominio.

### 1.2. Información sobre DNS

Se tienen los comandos `nslookup` (Consultas rápidas de DNS) y `dig` (Consultas más detalladas. )

```shell
nslookup www.elhuevodechocolate.com
Server:         10.255.255.254
Address:        10.255.255.254#53

Non-authoritative answer:
www.elhuevodechocolate.com      canonical name = elhuevodechocolate.com.
Name:   elhuevodechocolate.com
Address: 46.231.5.42
```

- **Server**: El servidor DNS que se utilizó para resolver la consulta fue **`10.255.255.254`**. Este es el servidor DNS que respondió a la consulta.
- **Address**: La dirección IP del servidor DNS es **`10.255.255.254`**, y está utilizando el puerto **53** (que es el puerto estándar para consultas DNS).

- **Non-authoritative answer**: Esta parte significa que la respuesta proviene de un servidor DNS que no es el **servidor autoritativo** para el dominio. Es decir, el servidor DNS consultado (en este caso **`10.255.255.254`**) no es el que tiene la autoridad final sobre la zona de **`elhuevodechocolate.com`**, sino que tiene esta información en caché (o la ha obtenido de otro servidor).
- Si fuera una **respuesta autoritativa**, el resultado habría sido etiquetado como **"authoritative answer"**. Esto indica que la respuesta fue directamente obtenida del servidor DNS que tiene la autoridad sobre ese dominio.
- El **nombre** final resuelto es **`elhuevodechocolate.com`**, que es el dominio real al que apunta el alias **`www.elhuevodechocolate.com`**.
- La **dirección IP** correspondiente a **`elhuevodechocolate.com`** (y, por lo tanto, también a **`www.elhuevodechocolate.com`**) es **`46.231.5.42`**.


```shell
~$ dig www.elhuevodechocolate.com

; <<>> DiG 9.18.18-0ubuntu0.22.04.1-Ubuntu <<>> www.elhuevodechocolate.com
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 55266
;; flags: qr rd ra; QUERY: 1, ANSWER: 2, AUTHORITY: 0, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 512
;; QUESTION SECTION:
;www.elhuevodechocolate.com.    IN      A

;; ANSWER SECTION:
www.elhuevodechocolate.com. 14400 IN    CNAME   elhuevodechocolate.com.
elhuevodechocolate.com. 14400   IN      A       46.231.5.42

;; Query time: 150 msec
;; SERVER: 10.255.255.254#53(10.255.255.254) (UDP)
;; WHEN: Thu Mar 13 00:15:38 CET 2025
;; MSG SIZE  rcvd: 85
```

- **status: NOERROR**: Esto significa que la consulta se resolvió correctamente sin errores.
    
- **flags: qr rd ra**: Estas son banderas que indican el tipo de respuesta.
    - **qr**: Respuesta de consulta (es una respuesta a una consulta).
    - **rd**: Recursión solicitada (significa que se hizo una consulta recursiva).
    - **ra**: Recursión disponible (indica que el servidor DNS puede realizar consultas recursivas).
- **QUERY: 1**: Se hizo una consulta.
    
- **ANSWER: 2**: Hubo dos respuestas en la sección de respuesta.
    
- **AUTHORITY: 0**: No hay servidores de autoridad especificados en la respuesta (no hay una sección de autoridad).
    
- **ADDITIONAL: 1**: Hay una sección adicional de datos.

- La consulta que se realizó: `www.elhuevodechocolate.com` con el tipo de registro **A** (dirección IP).

- Esta es la respuesta que se obtuvo:
1. **CNAME (Canonical Name)**:
    - **`www.elhuevodechocolate.com. 14400 IN CNAME elhuevodechocolate.com.`**
    - Esto significa que **`www.elhuevodechocolate.com`** es un alias (un CNAME) para **`elhuevodechocolate.com`**. En otras palabras, cuando consultas `www.elhuevodechocolate.com`, el DNS te dice que debes mirar a `elhuevodechocolate.com` para obtener la dirección IP.
2. **A (Address Record)**:
    - **`elhuevodechocolate.com. 14400 IN A 46.231.5.42`**
    - Esto indica que **`elhuevodechocolate.com`** se resuelve a la dirección IP **46.231.5.42**.



**Instalación**




**Configuración**



## 2. Parámetros de configuración y registros del servidor de nombres afectados en el desarrollo

**Configuración de la zona de resolución directa**



**Comprobar la configuración**



## 3. Servicios de directorios. Características y funcionalidad

**Organización del directorio LDAP**



## 4. Archivos básicos de configuración. Interpretación y uso




## 5. Adaptación de la configuración del servidor de directorios para el desarrollo de la aplicación. Usuarios centralizados




