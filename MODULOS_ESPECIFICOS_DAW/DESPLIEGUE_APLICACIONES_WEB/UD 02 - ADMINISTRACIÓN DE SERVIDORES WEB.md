
## 1. Configuración avanzada del servidor web

## 2. Módulos: Instalación, configuración y uso

### 2.1. Módulos en Linux

### 2.2. Módulos en Windows

## 3. Servidores virtuales. Creación, configuración y utilización

## 4. Autenticación y control de acceso

### Autenticación HTTP access

### Autenticación HTTP Digest


## 5. Protocolo HTTPS

## 6. Certificadores. Servidores de certificados

## 7. Despliegue de aplicaciones sobre servidores web




Peso de la información (webp)



```php
<!DOCTYPE html>
<head>

<head>
```

El cliente no ve la informacion del servicodr


Módulos Apache
- Estabilidad
- Dipsonibilidad
- Escalabilidad

Módulos Apache
Archivos `.so` son los módulos compilados.
Para poder usar un módulo en Ubuntu había que bajarse el código fuente y compilarlo 


**Taller módulos apache**
Apache en XAMPP
- `mod_ssl`: Añadir soporte para SSL/TLS Apache
- `mod_expires` : Establecer fecha de caducidad para contenido estático. Gestión del caché.
Apache en Ubuntu
- `mod_userdir`: Cada usuario de un sistema tenga su propio directorio público accesible desde Web
- `mod_headers`: Modificación de los encabezados HTTP que envía apache, útil para configuraciones de seguridad, control de caché. 

**Host Virtual**
Permiten a un servidor:
- Alojar múltiples sitios web
- Servir diferentes contenido para solicitudes HTTP del cliente
- Que el equipo responda a diferentes direcciones IP usando aplicación como Apache.
Configurar un servidor web para manejar múltiples dominios en un único servidor de forma eficiente o para configurar diferentes hosts virtuales para sesiones de hosting dedicadas. 





Apache Administrator's Handbook O'reilly
Writing Apache Modules with Perl and C

---------

Taller pdf con los pasos
Video pdf

Nginx. Servidor web alternativa a apache.


----------------
-----------

**SSL (Secure Sockets Layer)** es un protocolo de seguridad que se usa para establecer una conexión segura y encriptada entre un cliente (navegador web) y un servidor (servidor web). Ha sido reemplazado hoy día por su sucesor TLS (Transport Layer Security) pero el término sigue empleándose para referirse a esta seguridad.

**Funciones principales de TLS/SSL**
- **Encriptación**: Información encriptada. No puede ser leída, ni modificada por terceros.
- **Autenticación**: Permite verificar que el servidor con el que se produce la comunicación es realmente quien dice ser; mediante el uso de certificados digitales emitidos por una entidad de certificación confiable (CA)
- **Integridad**: Asegura que los datos no han sido alterados durante el tránsito. Llegan de forma íntegra.

**Funcionamiento**
1. **Handshake**: El cliente se conecta al servidor que tiene SSL/TLS. El servidor responde enviando su certificado digital con su clave pública. El cliente verifica la autenticidad del certificado con una entidad de certificación (CA) y, si es válido, usa la clave pública para encriptar una clave secreta que enviará al servidor.
2. **Encriptación**: El servidor recibe la clave secreta encriptada y ambas partes pueden usarse para cifrar la comunicación.
3. **Comunicación segura**: Durante toda la sesión los datos estarán encriptados. 

**Importancia**
- **Protección de datos sensibles**: Esencial en tiendas online, bancos, redes sociales.
- **Confianza del usuario**: Al usuario se le indica mediante un icono de candado en la barra de direcciones del navegador y el uso del protocolo https que la conexión es segura.
- **Posicionamiento en motores de búsqueda**: Los motores de búsqueda priorizan sitios web que usan SSL/TLS (HTTPS) y penalizan a los que no lo hacen (HTTP).

---
---


#### Nginx Ubuntu

```shell
sudo apt install nginx
sudo systemctl start nginx
sudo systemctl status nginx
sudo vim /etc/nginx/sites-available/default
```

En
`listen 80 default_server;` 
Poner
`listen 8080 default_server;`

Y que el bloque `root` apunte a `/var/www/html`

En `/var/www/html`
Crear archivo HTML.





---

Despliegue de aplicaicón web

`localhost/phpmyadmin`

- Crear BBDD almaMater con utf8_spanish_ci












