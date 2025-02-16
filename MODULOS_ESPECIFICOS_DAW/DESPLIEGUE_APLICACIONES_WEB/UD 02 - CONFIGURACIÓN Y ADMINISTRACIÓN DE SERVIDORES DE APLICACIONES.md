
## 1. Introducción a las aplicaciones web y servidores de aplicaciones



## 2. Introducción a las aplicaciones web basadas en Java EE

### 2.1. Servlets y JSP

### 2.2. Estructura de una aplicación web

### 2.3. Empaquetado WAR de aplicaciones web

### 2.4. El descriptor de despliegue



## 3. Servidor de aplicaciones Tomcat

### 3.1. Instalación

#### 3.1.1. Instalación desde repositorio

#### 3.1.2. Instalación manual

### 3.2. Arquitectura de Tomcat

### 3.3. Configuración básica de Tomcat

### 3.4. Servir aplicación web con Tomcat

#### 3.4.1. Despliegue de una aplicación web

#### 3.4.2. Implementar el registro de acceso

#### 3.4.3. Sesiones persistentes

#### 3.4.4. Autenticación de usuarios

### 3.5. Integración de Tomcat con Apache

### 3.6. Seguridad


## 4. Gestor de aplicaciones web de Tomcat

### 4.1. Configuración del gestor de aplicaciones

### 4.2. Uso del gestor de aplicaciones de Tomcat


## 5. Servidor de aplicaciones Wildfly

**Wildfly** es un proyecto gratuito, de código abierto y escrito en Java que implementa un servidor de aplicaciones de Java EE (Jakarta EE)

Un **servidor de aplicaciones** implementa todas las funcionalidades de la especificación de Java EE: Es un contenedor de servlets y además un contenedor de EJB (Enterprise JavaBeans), entre otras funcionalidades.

docker run -d -p 8081:8080 -p 9991:9990 jboss/wildfly:latest /opt/jboss/wildfly/bin/standalone.sh -b 0.0.0.0 -bmanagement 0.0.0.0


### 5.1. Instalación y configuración básica

### 5.2. Aplicaciones empresariales

### 5.3. Despliegue de aplicaciones empresariales y aplicaciones web en Wildfly


## 6. Construcción y despliegue automático con Ant

### 6.1. Instalación y configuración de Ant

### 6.2. Archivo `build.xml`

### 6.3. Empaquetar una aplicación con Ant

### 6.4. Desplegar en Tomcat usando Ant


## 7. Seguridad en aplicaciones web





