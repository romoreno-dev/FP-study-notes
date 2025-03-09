
## 1. Configuración del servicio de transferencia de archivos. Permisos y cuotas

## 2. Tipos de usuarios y accesos al servicio

## 3. Modos de conexión del cliente

## 4. Protocolo de transferencia de archivos seguro FTPS

## 5. Utilización de herramientas gráficas

## 6. Utilización del servicio de transferencia de archivos desde el navegador

## 7. Utilización del servicio de transferencia de archivos en el proceso de desarrollo de la aplicación web


FTP (File Transfer Protocol): Transferencia de archivos entre el cliente y el servidor. Subida, modificación o descarga de archivos en Internet.

Una vez instalado y configurado se esperan las peticiones para transferir los archivos.

FTPS: FTP con cifrado SSL/TLS. 

**Configuración el FTP**
- Cliente FTP: Realiza conexión de control por puerto TCP 1024, solicita la transferencia de archivos estableciendo conexión al FTP por puerto 21
- Servidor: Transfiere datos solicitados por cliente. 

**Tipos de usuarios**
- Usuarios anónimos: Accesos y permisos limitados. 
- Usuarios del sistema: Usuarios que define el servidor. Tienen los permisos creados para ello. 
- Usuarios virtuales: Pueden no ser usuarios del sistema. Con credenciales para su conexión.


**Modos de conexión**
- Modo activo
- 

![[Pasted image 20250309161152.png]]

SSL implícifo o FTPS
SSL Explícito o FTPES. 

![[Pasted image 20250309161224.png]]

-----------


127.0.0.1   local local 

14147

--

### Instalar servidor FTP en Ubuntu

**vsftpd**

`sudo apt install vsftpd`

Veamos el fichero: `/etc/vsftpd.conf` para:
- Habilitar acceso local y subir archivos:
```
local_enable=YES
write_enable=YES
```

- Configurar permisos de archivos y directorios:
```
file_open_mode=0777
# Todos los usuarios podran acceder
```

- Se crea un usuario de prueba que acceda solo a su directorio personal.
`sudo adduser usuarioftp`

- Se prueba la conexión `ftp localhost`.  Y el usuario usuarioftp
Se sube un archivo con:
`put archivo.txt`
Se descarga con:
`get archivo.txt`


------
--------

### Windows Server + FTP 

SACAR  DEL TALLER LA TEORIA!!!!!!!!!!!!!






