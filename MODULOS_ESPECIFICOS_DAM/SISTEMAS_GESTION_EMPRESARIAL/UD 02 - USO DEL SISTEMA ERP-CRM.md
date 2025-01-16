
## 1. Primeros pasos con el ERP

### 1.1. Acceso al ERP

Accedemos a Oddo en **IpServidor:8069**.

Debe estar arrancado `/opt/odoo/odoo`  `./odoo-bin`

Se muestra la pantalla de Aplicaciones y se accede como Administrador.
Se pueden instalar los módulos de los que se compone Odoo.

Al abrirlo por primera vez solicita:
- Nombre base dedatos
- Usuario o correo
- Idioma
- Contraseña de inicio de sesión

Se pulsa en "Crear base de datos"
Debe tenerse localizado el archivo de configuración de Odoo.

Reinicio:
En Windows se puede acceder a los servicios locales y allí buscar odoo-server y con eso deternerlo y reiniciar
### 1.2. Definición del módulo
Módulo: Programa que se realiza para cubrir una función de la aplicación.
Toda la funcionalidad de un ERP está contenida en sus distintos módulos.

Los módulos se caracterizan por:
- Instalación - desinstalación mediante asistentes
- Configuración o parametrización de los módulos para su adaptación al entorno de producción
- Generación de informes por cada módulo
- Incorporación de niveles de seguridad (módulos solo accesibles por administrador)
- Interconexión entre los módulos, información compartida entre ellos
- Posibilidad de incluir textos y comentarios en las opciones del programa
- Adaptación de menús de los módulos de las necesidades de cada usuario

### 1.3. Entorno modular de un ERP

El diseño del ERP es modular. Hay un módulo o conjunto de módulos base necesarios para que funcione la aplicación, alrededor de los que se sitúan módulos adicionales que se van desarrollando según la necesidad concreta.

## 2. Tipos de módulos

La **funcionalidad o módulo base*** normalmente contempla los siguientes aspectos:
- Configuración de la aplicación
- Gestión de los datos maestros Introducción de datos para que funcionen los procesos de gestión
- Establecimiento del idioma o importación de traducciones
- Seguridad: Gestión de usuarios y accesos
- Administración de módulos: Para instalar nuevos módulos.

Adicionalmente al módulo base destacan:
- Gestión contemple y financiera
- Operaciones de compra: Compras y almacén
- Operaciones de venta
- Facturación, cobros y pagos
- Gestión comercial
- Gestión de personal
- Gestión de las relaciones con el cliente (CRM, Customer Relatioship Management)

- Productos
- Inventario
- Proveedores
- Gestión de proyectos
- Gestión de informes y estadísticas

### Contabilidad y finanzas (Account)

Recoge y automatiza todas las operaciones contables de la compañía centralizándolas para su consulta publicación o control. 
Cubre la contabilidad general, análisis contable y decostes, gestión de impuestos, presupuestos, facturas, tanto de clientes como deproveedores.

**Debe estar integrado con los módulos de compras y ventas para evitar duplicidades**. Así también se pueden obtener facturas de clientes y proveedores desde pedidos de venta y compra o albaranes de salida y entrada, respectivamente. 

También **debe estar integrado con el resto de módulos del ERP para realizar una gestión integral de la compañía.**

Las facturas tienen asientos contables. A través de los asientos contables se reflejan movimientos entre cuentas de una empresa. Movimiento de la cuenta bancaria a la cuenta de efectivo para tener más dinero en Caja. 

http://www.youtube.com/embed/01BUNlA5UQU
http://www.youtube.com/embed/Qu6R3yNKR60 (No precargado Odoo 12 Accounting report)
http://www.youtube.com/embed/RS8zTRBy82U

Las funcionalidades básicas de este módulo son:
- Contabilidad general.
- Contabilidad analítica / costes.
- Gestión de impuestos.
- Presupuestos.
- Facturas de clientes y proveedores.
- Extractos de cuentas bancarias.
- Informes contables.


Para la realización de tareas contables en el ERP será necesario:
- Completar la información de la empresa.
- Introducir las cuentas bancarias.
- Selección del Plan de Cuentas.
- Selección de los impuestos necesarios para la gestión.
- Datos de clientes, proveedores y productos.
 - Saldos iniciales.
- Definición de usuarios para la contabilidad.

### Compras (Purcharse Management)

Aprovisionamiento para poder vender. Operaciones de solicitudes de presupuesto a proveedor, recepción de precios, creación de pedidos de compra, con indicación de precios, plazos de entrega...

Este módulo automatizar el flujo de trabajo de lasórdenes de compra, incluye la gestión de proveedores, y el control de productos y facturas,en lo relativo a la generación de facturas en base a órdenes de compra o productosrecibidos, creación manual de facturas e importar líneas desde órdenes de compra, etc.

- Seguimiento de tarifas de sus proveedores.
- Conversión de tarifas en órdenes de compra.
- Gestionar entregas parciales del proveedor.
- Gestión de reclamaciones a proveedor.
- Generación automática de borradores de pedidos de compra.

En Odoo las órdenes de compra pueden crearse como tal o pueden provenir de
Solicitudes de Cotización o de Licitaciones de Compra .Las órdenes de compra generarán una factura del proveedor. Mediante el menú Compra/Pedidos de Compras. Crearemos un nuevo presupuesto que se convertirá en un pedido de compras.

### Ventas (Sale)

Este módulo, eje principal del ERP, gestiona todas las operacionesrelacionadas con la venta de los productos de la empresa, como la creación de órdenes deventa, facturas de venta configurables, facturas en reparto, gestión de stock disponible, etc.

Similar a compras pero para ventas. 

- Creación de pedidos de venta.
- Revisión de los pedidos en sus distintos estados.
- Confirmación de envío.
- Definición de formas de pago por pedido y fecha de facturación.
- Gestión y cálculo de gastos de envío de un pedido.
- Albaranes automáticos desde pedido.
- Albaranes de envíos parciales.

### Facturación

Generación de datos que tengan que ver con facturación de productos y servicios a los clientes: facturas de venta, albaranes tarifas. Contempladas diversas formas de cobro y pago.

- Configuración de formas de pago de Clientes o cobro de proveedores .
- Facturas automáticas desde pedido o albarán.
- Generación automática de efectos de cobro y pago.
- Gestión de recibos, órdenes de pago y transferencias.
- Importación de extractos bancarios.
- Envío telemático de remesas al banco.
- Gestión de bancos propios, bancos de Clientes y bancos de proveedores.

En la mayoría de las ocasiones las facturas son generadas automáticamente desde diferentes procesos del sistema, aunque también esposible generarlas manualmente. De esta forma, no son necesarias crearlas manualmente, sino que los diferentes procesos generan facturasen Borrador, y éstas deben ser aprobadas por el usuario de sistema que corresponda y enviadas al cliente.

Existen diferentes maneras de automatizar la creación de la factura del cliente en Odoo. Dependiendo de las características de la empresa que utilicemos, podemos optar por una de las siguientes maneras para crear facturas:
- **Orden de venta -> Factura**. La factura se crea basándose en una orden de venta.
- **Orden de venta -> Entrega -> Factura**. En lugar de facturar basándose en una orden de venta, se factura basándose en cantidades entregadas. De esta manera, se permiten órdenes de venta parciales, facturándose sólo lo que se ha entregado.
- **Suscripciones -> Facturas**.Para suscripciones, una factura se activa periódicamente, de forma automática. La frecuencia de la facturación y de los servicios/productos facturados están definidos en el contrato.
- **Orden de comercio electrónico -> Factura**. Cuando se trabaja con comercio electrónico la factura se activará una vez que se recibe el pago.
- **Creación manual de la factura**. También se pueden crear facturas manuales sin utilizar ninguno de los métodos anteriores. Por ejemplo, para reembolsos, para hacer descuentos o facturar algo no relacionado con el negocio principal de la empresa.
### Almacén / Inventario (Inventory Management)

Módulo para la gestión del almacenes, nosproporciona diferentes métodos de inventario, gestiona el valor del stock, además podemoscrear reglas de reordenación automáticas, gestionando la historia y la planificación

Permite gestionar las existencias de productos en almacen.
- Definición de múltiples almacenes.
- Gestión de la rotación de inventario y niveles de stock.
- Traspasos entre almacenes.
- Codificar y numerar productos de distinta forma.
- Definir compras de un producto a distintos proveedores.

### Gestión de personal

Planificación y realización de nóminas de los empleados, altas, bajas, contratos, control de horarios, datos de personal, sistema de remuneraciones, comisiones...

- Gestión de empleados y calendario de vacaciones.
- Gestión de contratos de empleados.
- Gestión de beneficios.
- Gestión de ausencias.
- Gestión de producción o rendimiento.
- Gestión de perfiles y responsabilidades.

Podemos incluir aquí un conjunto de módulos que permiten gestionarlos recursos humanos de una empresa. Destacan el módulo de Directorio de Empleados(Employee Directory), Gestión de vacaciones y ausencias (Leave Management) o el deProductividad (Productivity) que proporciona herramientas para priorizar tareas, compartirdocumentos e incrementar la productividad el empleado.

A veces no tendrá módulo de RRHH y será llevado con conceptos contables relacionados y gestión de comisiones a través del módulo comercial.

### Gestión de las relaciones con el cliente (CRM)

CRM (Customer Relationship Management)  es muy importante en el ERP. Incluye todo lo relacionado con la relación comercial con clientes o posibles clientes.
Busca tener información **centralizada** para optimizar los procesos de gestión.
Hay aplicaciones únicamente destinadas a la gestión CRM. En ERP Odoo existe un módulo independiente de CRM. 

Módulo para la gestión de las relaciones con los clientes,gestionando la adecuada atención a los ya existentes, así como, la gestión eficiente declientes potenciales, oportunidades, peticiones, campañas, etc. Gestiona tareas como lacomunicación, asignación, resolución y notificación. Con este módulo nos aseguramos quetodos los casos de nuestros clientes obtengan una atención y seguimiento igual yadecuado. Además, extrae información precisa de todos los datos registrados para la ayudaen la toma de decisiones.

- Datos identificativos del contacto.
- Segmentación de clientes en función de múltiples criterios.
- Determinación de clientes reales y potenciales.
- Gestión de llamadas.
- Calendario de encuentros.
- Generación y seguimiento de campañas de marketing.
- Seguimiento de acciones comerciales.
- Enlace con otros documentos y procesos de la aplicación.
- Herramientas de productividad: editor de documentos, sincronización de contactos y calendario, envíos masivos por correo electrónico, mensajería sms o fax, etc.
- Estadísticas diversas.

Los módulos más avanzados de gestión de las relaciones con el cliente pueden incluso incorporar una **Extranet**, para la conexión por parte de clientes (y proveedores) con el sistema de la empresa, y así poder consultar la información a la que ésta les dé acceso.

El módulo de CRM en Odoo funciona creando flujos de venta para un cliente dado. Utiliza diversas herramientas en las relaciones con losclientes que deberemos configurar para adaptarlas a nuestra empresa.

Un flujo de venta está definido por un importe estimado de venta, la probabilidad de realizarla y el cliente relacionado. El flujo de venta pasa por los siguientes estados (pueden ser definidos por el usuario):

- **Nuevo**: Estado del flujo en el momento de su creación.
- **Calificado**: Una vez validado el flujo de venta pasa al estado calificado.
- **Propuesta**: Se realiza un presupuesto basado en ese flujo.
- **Negociación**: El flujo pasa al estado de negociación cuando el prespuesto es aprobado por el cliente y se quieren negociar los términosde la venta.
- **Ganado**: Cuando el presupuesto se materializa en una venta.

### Fabricación (Manufacturing))
Módulo para la gestión de la fabricación. Incluye la creaciónde lista de materiales, procesar órdenes de fabricación, vender conjunto de proeuctos comoun kit o la gestión de productos semiacabados.

### Punto de venta (Point of sale, TPV)
Este módulo incluye varios de los procesos de laempresa como son creación de una orden de compra, una devolución o la modificación dela forma de pago en el momento mismo de realizar la venta, simplificando operaciones talescomo el cálculo automático de la devolución de dinero en una venta, o permitir al usuario lacreación de la factura de forma automática, entre otras.

### Campañas publicitarias (Mass Mailing Campaings)

Gestionaremos las campañaspublicitarias, utilizando varios métodos de comunicación, creando campañas personalizas,de forma que aumenten las ventas y se promocione la empresa.
## Comercio electrónico (e-commerce)

Nos suministra las herramientas necesarias parahacer una proyección mayor de los artículos y productos de nuestra empresa, mostrando deforma muy visual las características de los mismo, conectando con los clientes a través deinternet. Permite crear filtros y categorías de productos, así como todas sus características,logotipo, etc. Actualmente un módulo imprescindible en nuestro ERP.

### Constructor de sitios web (Website Builder)

Nos permite el diseño de sitios web deforma simple. Nuestra web así podrá integrar herramientas como e-commerce, blog, etc.
### Localización española

Adaptar ERP a las leyes y normas de cada país en:
- Plan General Contable Español
- Módulo de Impuestos, tipos de IVA
- Validación de datos (CIF, NIF, cuentas bancarias)
- Inclusión de datos maestros, datos sobre provincias de España
- Traducción al español

## 3. Operaciones de gestión y consulta de la información

La información contenida en ERP se trata con SGBD (DBMS) que ofrecen programas para acceder y gestionar los datos.

La base de dados del ERP es de gran tamaño. Almacena datos, vistas, otros elementos. Es necesaria una organización entre sus componentes (nomenclatura o normativas que deben seguir los desarrolladores a la hora de modificar el código fuente  o esquema: colocar un prefijo para saber a qué modulo pertenecen, establecer una serie de campos como obligatorios)
### 3.1. Elementos de una base de datos

Los conceptos habituales:
- Tablas
- Campos o atributos
- Filas o registros
- Vista
- Relación
- Consulta

- Procedimiento almacenado: Función o procedimiento almacenado físicamente n una BBDD que hace una tarea simple sobre los datos (disparadores, triggers)
- Formulario: Documento digital para manejar los datos, almacenándolos y procesándolos posteriormente
- Informe: Exposición de los datos presentados de forma fácil de analizar e imprimir

### 3.2. Administración de las bases de datos
Odoo dispone forma de administrar la base de datos del ERP aunque se puede hacer también desde el gestor de base de datos (como pgAdmin).

Necesario introducir:
- Nombre de conexión
- Servidor
- Puerto
- Base de datos de Mantenimiento (base de datos inicial con la que nos conectamos)
- Nombre de usuario
- Clave

### 3.3. Consultas de acceso a datos

Para acceder a la información, solicitando un extracto.
Necesario:
- Seleccionar las tablas o vistas sobre las que va a actuar la consulta
- Establecer relación entre tablas o vistas en caso de que la aplicación n ola proporcione
- Seleccionar campos a mostrar
- Ejecutar
## 4. Técnicas de optimización de consultas

Optimización: Modificar un sistema para mejorar su eficiencia o el uso de los recursos disponibles.

Al manejar grandes cantidades de datos el resultado puede tomar un tiempo considerable y ser poco óptimo. Como técnicas de optimización mencionamos:
- **Diseño de tablas**: Asegurar que no hay duplicidad de datos y que se aprovecha el almacenamiento
- **Campos**: Ajustar el espacio de los campos al máximo para no desperdiciar
- **Índices**: Búsquedas a velocidad superior pero no debemos indexarlo todo porque ocupan más y tardan en actualizar. Podría estudiarse si deben usarse si es un campo usado como criterio de búsqueda o si es una clave ajena en otra tabla.
- **Optimizar sentencias**
- **Optimizar la base de datos**

### 4.1. Conexión directa con PostgreSQL

```shell
sudo su postgres
psql
\h # Ayuda
\l # Bases de datos existentes
\c [nombre_bd] # Conectar con la BBDD
\d # Tablas existentes en la BBDD
\d [nombre_tabla] # Descripcion de la tabla
VACCUM VERBOSE ANALYZE [tabla] # Limpia y analiza Bases de datos
\q # Salir
```
### 4.2. Sistemas batch inputs. Generación de programas de extracción y procesamiento de datos

**Batch-input** procede del el uso en sistemas SAP de un método usado para transferir grandes cantidades de datos a un sistema ERP. 
Requieren programas tanto par la generación del archivo como para el procesamiento posterior.

Hay dos forma de hacer un batch-input:
- **Método clásico**: Asíncrono. Se procesan los datos pero se actualizan más tarde. Genera archivo de mensajes o logs para tratar errores a posteriori.
- **Método call transaction**: Método online usado para dar de alta rápidamente pocos registros. Es síncrono, no genera logs y es mucho más rápido pero solo sirve para pocos datos.

El proceso de batch-input tiene dos fases:
- **Fase de generación**: Genera el archivo batch-input con los datos a introducir o modificar
- **Fase de procesamiento**: El archivo batch-input se ejecuta haciéndose efectivas las modificaciones en base de datos

## 5. Extracción de datos en sistemas ERP

La extracción de datos puede hacerse usando diferentes sistemas.-
Muchas veces con herramientas ofimáticas que se conectan a la aplicación ERP para obtener información de la BBDD y volcarla en la aplicación.

Hay procesos más complicados (Procesos de Business Intelligence) que:
- transforman y combinan los datos para extraer la información
- la convierten en potentes indicadores
- la muestran en diversos formatos gráficos

Según el origen de los datos y el tipo de información se pueden usar:
- **Consultas e informes**: Datos en una sola base de datos y se extraen a partir e una consulta SQL. La aplicación facilita informes predefinidos aunque se pueden generar personalizados usando la aplicación o herramientas externas como JasperReports
- **Almacenes de datos**:  La extracción de datos se hace desde diferentes sistemas y distintas bases de datos, creando almacenes de datos para homogeneizar e integrar la información. 
- **Cubos multidimensionales**: Un cubo n-dimensional es un conjunto de datos multidimensionales organizados en ejes y celdas que maneja la información de la base de datos relacional. También hay bases de dados multidimensionales (sin necesidad de almacenar primero en relacionales y luego usar cubos)

En ocasiones la extracción no se hace en tiempo real para evitar disminución en la velocidad de respuesta. Primero se extrae la información y luego es manipulada podría haber alguna leve diferencia entraer la información manipulada y el contendido en BBDD.
### 5.1. Importar y exportar datos

La importación y exportación de datos se hace a través de los mecanismos provistos por la aplicación. Muchas veces en formato CSV en el que las columnas se separan por comas (o punto y coma donde la coma sea separador decimal) y las filas por saltos de línea.

La herramientas debe permitir seleccionar los campos a importar y volcar dicha información en el objeto deseado. Se podrán importar en una sola tabla o varias. 

La exportación igual: En el objeto a exportar se elige "Exportar" y se genera el archivo que puede abrirse por cualquier aplicación ofimática o, en el caso del CSV, incluso por editor de textos sencillo.

Se puede exportar datos desde los formularios también. Permitiendo más campos a exportar que la vista de árbol.
### 5.2. Copias de seguridad

Deben programarse copias de seguridad de las bases de datos periódicamente.
Odoo da un Gestor de bases de datos  al que puede accederse permitiendo realizar copia completa en formato comprimido.
Se podría hacer copia de seguridad y tener entorno de producción y otro de pruebas.

También se pueden hacer a través del gestor PgAdmin.

## 6. Auditoría y control

Debe haber herramientas que permitan hacer un seguimiento de los datos del equipo servidor donde están las aplicaciones.

Datos instantáneos del rendimiento del sistema (procesador, memoria, dispositivos entrada salida) o recogerlos y almacenarlos en ficheros históricos que informen sobre carencias y cuellos de botella del sistema. 

### 6.1. Auditoría por ficheros

Odoo tiene su fichero de configuración `odoo.conf` y allí están los parámetros:
- `syslog`: Linux auditoría
- `logrotate`: Sistema rote los archivos de log
- `logfile`: Localización de ficheros de log
En la carpeta del servidor está PostgreSQL y en el fichero de configuración de la base de datos `postgresql.conf` se describe la terminología para los distintos parámetros:
- FILE LOCATIONS: Colocar archivos de configuración en otro lugar
- ERORR_REPORTING_AND_LOGGING Configurar aspectos sobre creación de ficheros de auditoría con métodos como stderr, csvlog, syslog (eventlog en Windows), así se puede establecer lista de destinos de registros separados por comas; por defecto solo se registrará en stderr.
- RUNTIME STADISTICS: Estadísticas de uso sobre el sistema para determinar el rendimiento.

### 6.2. Control del rendimiento

Se permiten instalar módulos para recoger datos y mostrar informes de análisis y monitorización del rendimiento en el sistema ERP.
### 6.3. Trazas del sistema

La actividad queda registrada en los logs. Puede querer examinarse las trazas para realizar control de acceso (quien entra, qué comandos ejecuta, qué errores muestran)
También para resolver posibles problemas ante falllos de funcionamiento.

El fichero `odoo.log`
- En Linux se guardan en /var/log
- En Wndows  se encuentra en el directorio base de instalación en la carpeta server.

Serán necesarios permisos de root para poder visualizar estos ficheros. 
