
## 1. Introducción

Se hace importante hacer un estudio de las necesidades y requisitos para la adquisición de un ERP (Identificación de los procesos más importantes de la empresa y de qué forma pueden llevarse a cabo). Se podrían contratar a consultoras externas que analicen y hagan un informe final con recomendaciones de implantación del software para, con este estudio, tomar la decisión de adquirir una u otra aplicación.

Las fases del **proceso de selección, implantación y puesta en marcha** del ERP se pueden definir como: 
- **Selección del ERP**: Basándose en los procesos clave de la empresa, qué tareas se repiten y pueden ser automatizadas, qué necesidades son deseables en el nuevo sistema informático, qué módulos pueden responder a estas necesidades. (Empresa o consultora externa)
(Por el proveedor del ERP)
- **Implantación**: Cambios y adaptaciones en la aplicación que necesite la empresa.
- **Puerta en marcha**: Instalación del programa en producción y resolución de problemas de implantación
- **Cierre y finalización**: Revisión final del sistema, comprobando su funcionamiento.

Software como servicio: Servicio ofrecido por proveedor en forma de suscripción mensual que incluye equipos servidores, mantenimiento del sistema, hosting y soporte. Para pequeñas empresas que por bajo costo tienen completo e integrado sistema de gestión.

### 1.1. Tipos y necesidades de las empresas

Expresas susceptibles de implantar un ERP son:
- **Pequeña y mediana empresa**: Gestión de clientes, proveedores, productos; Compras, ventas y almacén.
- **Sector servicios**: Gestión por proyectos (Módulo específico control y seguimiento de proyectos)
- **Tiendas y restaurantes**: Venta de productos con terminales de puntos de venta en lectores de código de barras o dispositivo táctil. Interfaz táctil y amigable. Categorías de productos, múltiples pedidos y métodos de pago.
- **Ayuntamientos**: Gestión de proyectos y contabilidad en departamentos, control de compras y stocks, recursos humanos, atención al ciudadano (CRM) con portales del municipio, padrón, gestión de tasas
- **Venta telefónica**: Módulo de CRM importante para la información resultante del contacto telefónico con el cliente.
## 2. Selección del sistema ERP

Análisis previo -> Elección del ERP y de los módulos que mejor se adaptan a los requerimientos. 
### 2.1. Análisis inicial

En el análisis inicial se estudia cómo funcionan las áreas de la empresa (Compras, Ventas, Marketing y gestión de relaciones con el cliente, Logística y Recursos humanos). 
Se cubren:

1. **Estructura de información o datos maestros**: Datos que necesita la aplicación para trabajar con el sistema
2. **Procesos de negocio**: Estudio de los procesos o tareas de cada área de la empresa y de qué herramientas usan para su comunicación. Verificar si los procesos del ERP se adaptan con los requeridos
3. **Informes necesarios**: Informes dentro de los que incorpore en el ERP o nuevos que se adapten a los requisitos
4. **Traspaso de información**: Analizar la migración de los sistemas de gestión que usa la empresa al nuevo ERP considerando la estructura y característica de los datos a traspasar, campos que necesita el ERP para funcionar, verificar introducción de los datos necesarios para que funcione el ERP.
5. **Planificación de la implantación**: Adecuada gestión de implantación para que sea sistemática y organizada. 
Reflejar cada proceso e información a registrar y centralizar.
Forma de gestionar la implantación como proyecto dentro de toda la estructura de la empresa.

### 2.2. Módulos a conocer

¿Qué módulos del ERP se pueden usar?

Pueden ser
- **Módulo base**: Se instala con la aplicación. Opciones mínimas para funcionar
- **Módulos precargados**: Cargados durante la instalación del sistema. Están disponibles para ser instalados en cualquier momento
- **Módulos no precargados**: No aparecen en la lista de módulos, necesitan primero ser cargados en la aplicación.
- También hay **módulos especiales de un país** como los archivos de localización española para llevar a cabo tareas comunes de cualquier empresa como ventas, compras, productos, almacén, contabilidad, facturación, plan contable...

Tras el análisis inicial se plantearán qué módulos deben activarse para cubrir todos los aspectos funcionales.

Los más destacables son:
- **Accounting and Finance - Contabilidad y finanzas** :
- **CRM - Gestión de clientes**: 
- **Sale - Ventas**: 
- **Purchase Management - Compras**: 
- **Inventory Management - Inventario**: 
- **Manufacturing - Fabricación**: 
- **Point of sale - Punto de venta**: 
- **Recursos humanos**: 
- **Mass Mailing Campaigns - Campañas publicitarias**: 
- **E-commerse - Comercio electrónico**: 
- **Website Builder - Construcción de sistios web (CMS, Sistema gestor de contenidos)**: 

## 3. Módulos no precargados

Los módulos se muestran con color relativo al tema del módulo y botón en color gris y claro desactivado con la inscripción instalado.
Los que pueden instalarse aparecen con "Instalar". Simplemente debe instalarse y configurar los parámetros necesarios con la información necesaria.
### 3.1. Respaldo del sistema

Antes de modificar el ERP es conveniente hacer copia de seguridad del sistema por si el nuevo módulo deja el sistema inestable. Gestionar bases de datos > Copia (Backup)

El archivo comprimido se guardará en nuestro equipo y se restaurará, dado el caso, con Restore Database. 

### 3.2. Instalación de módulos no protegidos

**Descargarlo en internet y cargarlo en el sistema**
Se descarga el módulo desde la web de aplicaciones http://www.odoo.com/apps
Se descarga módulo con Download y después se copia descomprimido en el directorio addons de Oddo. 

En el modo desarrollador de Odoo se clicka en Actualizar lista de aplicaciones y ya entonces se podrá ver. 
## 4. Distribución de  módulos

También se pueden descargar módulos no precargados mediante el sistema de control de versiones. Odoo Community Association (OCA) coordina las contribuciones mediante varios repositorios de Github en https://github.com/OCA
### 4.1. Sistemas de control de versiones

Git funciona con flujos de trabajo compuestos por tres estados:
- Modificado: Cambios en un archivo
- Preparado: Se le indica a Git que lo hemos modificado
- Confirmado: Se confirman los cambios
### 4.2. Gestionar repositorios
Absurdo describirlo.

## 5. Catálogo de la base de datos

El **catálogo del sistema** es el lugar donde el SGBD del ERP almacena la información.
Está formado por metadatos sobre las estructuras de datos e información interna para el funcionamiento.
Hay dos fuentes:
- information_schema: estructuras definidas según ANSI_SQL, ubicadas en el esquema propio
- pg_catalog: Catalogos propios de PostgreSQL. Estructuras particulares de PostgreSQL que pueden cambiar según la versión usada y se identifican con el prefijo pg_*

El catálogo pg_database almacena información sobre las BBDD disponibles.
No suelen modificarse manualmente sino con instrucciones SQL (ej.: CREATE DATABASE inserta fila en pg_database y crea BBDD en disco)
### 5.1. Estructura de la base de datos

Con el ERP puede accederse a la estructura de la base de datos desde el menú de "Técnico / Estructura de la base de datos" solo visible entrando en modo desarrollador.
Destacan las pestañas:
- **Modelos**: Modelos de BBDD y crear nuevos
- **Campos**: Campos asociados a los modelos, crear, editar
- **Restricciones del modelo**
- **Relaciones many2many:** Relaciones establecidas, nombre y objeto
- **Modelos referenciables**: Referenciar con nombre los objetos. Ej.: account.invoice se referencia con nombre Factura
- **Precisión decimal **de los campos numéricos con los que trabaja la base de datos.

## 6. Implantación en la empresa

En el Proyecto de Implantación de un ERP se incluye:
- La adaptación de la aplicación a los requerimientos
- Formación de usuarios 
- Traspaso de datos
- Configuración del programa
- Pruebas de usuarios
- Pruebas definitivas y revisión

**Riesgos de implantación e integración de ERP**:
- Finalización fuera del plazo previsto
- Sobrepasar presupuesto asignado
- Funcionamiento no esperado
- Acontecimientos imprevistos que impidan el desarrollo del proyecto

Llevar a cabo un proyecto de implantación ordenado y controlado siempre es recomendable, ya que minimiza los riesgos de implantación del ERP.
Debe hacerse adecuada gestión del riesgo para solucionar posibles problemas. Debe llevarse con éxito en la parte técnica pero la metodología también debe ser aceptada por los usuarios o igualmente supondrá un fracaso.

### 6.1. Consultas necesarias para obtener información

En la implantación el proveedor de ERP debe:
- Diseño adaptación del programa
- Puesta en marcha
- Soporte

Si el análisis llevado a cabo antes de la selección del ERP fue exhaustivo, gran parte de la información recabada sirve para confeccionar los requerimientos necesarios en la implantación. Aún así recomendable consultar Datos de la empresa, Clientes, Proveedores, Productos, Almacén, información de Compra-Venta (tarifas, formas de pago), Información financiera (plan contable, impuestos).

### 6.2. Creación de objetos en el ERP

Puede tener que añadirse campos a objetos existentes o crear objetos nuevos. Puede ser que se necesiten bases de datos diferentes, cada BBDD es una empresa distinta.

La modificación de objetos puede hacerse
- Con pgAdmin tabla, columna, clave foránea, regla, evento
- Desde Odoo con Técnico/Estructura de la base de datos / Modelos para introducir nombre del objeto, objeto, descripción de los campos, tipo de los campos, permiso de acceso

### 6.3. Creación de informes y gráficos personalizados

Diferenciamos entre:
- Informes estadísticos: Informes y gráficos dinámicos según las opciones que seleccionemos para ser mostrados por pantalla
- Documentos imprimibles: Documento PDF a partir de los datos seleccionados. Pueden generarse con el lenguaje de programación de la aplicación, con herramientas ofimáticas para descargar, modificar y subir o con un motor de informes (exportar el objeto desde la aplicación y a partir de ahí construir el informe, caso de JasperReports con iReport)

### 6.4. Traspaso de datos

Necesario volcar toda la información del sistema antiguo al nuevo ERP. Es muy importante. La información de la empresa es muy valiosa y la mala gestión puede paralizar toda la organización. Debe estudiarse el formato de almacenamiento del software origen y destino para llevar a cabo una buena importación (conseguir emparejamiento entre ambos)

Tareas a realizar:
- Unificar formato y contenido de los datos: Unir información dispersa o distribuida en un único archivo
- Eliminar duplicidad de datos
- Mejorar codificación de la información: Introducir o corregir cosas que falten para conseguir mayor calidad de datos.
- Guardar los datos con el formato de exportación elegido
- Introducción de datos de las tablas secundarias: si se necesitan algunos datos antes de poder hacer la improtación
- Realizar la importación

En Odoo consideremos:
- Los ficheros CSV deben separarse por punto y coma
- El separador de texto en el CSV debe ser comillas dobles
- La primera fila del CSV debe contener los nombres de los campos en el idioma dado en las preferencias de la aplicación
- Revisar los datos de las tablas secundarias. (Si el campo no existe en la tabla secundaria... ejemplo importamos empresas con una categoría Cliente y esta no existe en res.partner.category)
### 6.5. Planificación de la implantación

Figuras clave:
- Dirección o Responsables de la empresa: Toma de decisiones en el proyecto. Debe estar plenamente implicada en el mismo
- Jefe de proyecto: De la empresa o agente externo. Valida, verifica y hace interlocutor entre todos los miembros
- Responsable de migración: Conoce bien el sistema antiguo y las necesidades a cubrir con el nuevo
- Equipo de consultoría: Realizan labores de análisis inicial de proceso y requisitos, propuesta de solución, instalación y configuración del sistema, formación de usuarios y programación a medida de los módulos que se necesiten.

Etapas: 
- Análisis de procesos y enfoque de solución
- Planificación del proyecto (tiempos y coste)
- Fase de instalación (traspaso de datos, inicio de programación, formación a responsables)
- Fase de consultoría (formación a usuarios e instalación de módulos)
- Fase de pruebas (antiguo en paralelo con el nuevo)
- Puesta en marcha
- Revisión de funcionalidades y realización de ajustes
- Finalización del proyecto
## 7. Configuración del sistema 

Establecer parámetros del sistema para que se ajusten a las necesidades de la empresa. Adaptación de informes, consultas y otros objetos.

Los cambios en la configuración se hacen desde la interfaz del cliente, modificando la forma general en qué funciona y las diferentes herramientas de análisis usadas. También se puede cambiar la apariencia, asignar funciones a usuarios, establecer qué operaciones se pueden realizar.

Es importante configurar el derecho de acceso a la información con políticas para los diferentes usuarios. 
Evitar que usuarios inexpertos hagan cambios no adecuados en la aplicación, introduzcan incongruencias o actúen de mala fe.
### 7.1. Control de acceso

Hay **usuarios** y **grupos**, pudiendo un usuarios pertenecer a uno o más grupos que determina qué menús puede visualizar y a qué tablas de la base de datos puede acceder.

Lo primero es configurar los grupos (importante que sean representativos). Desde Ajustes -> Usuarios y Compañías. Allí a qué módulos se da acceso a los distintos usuarios.

Para accesos a cada usuario en la ficha de cada uno aparecen varias pestañas y en Permisos de acceso y pulsando sobre el botón editar, modificarlos.

Ejemplo: Grupo **Comercial** con acceso solo a algunos menús de **Empresas** y ninguna nformación contable.
Los usuarios del **Departamento de Ventas** se hacen miembros del grupo **Comercial**:

Se puede crear un **Responsable de Ventas** con acceso a los permisos de **Comercial** y además a las comisiones de venta.
### 7.2. Cambiar la apariencia del sistema

Al modificar la apariencia debe valorarse la necesidad real de hacerlo porque puede suponer tener que formar de nuevo a los usuarios y actualizar la documentación.

Al modificar el componente, puede ser interesante duplicarlo, así se mantendrá el componente original si se necesita volver atrás.
## 8. Puesta en marcha y finalización del proyecto

Se hacen las pruebas definitivas de todos los módulos con dos posibles formas:
- Pruebas de funcionamiento en paralelo: Permite evaluar desajustes y, si todo coinciden, abandonar el antiguo sistema. Provoca entradas de datos duplicadas y coste e nel tiempo.
- Bloqueo del sistema antiguo y puesta en marcha con el ERP del sistema implementado. Si no se ha probado el nuevo puede fallar en la puesta en marcha.

La elección de uno u otro depende de la bondad de las pruebas realizadas: Debe ser una fase exhaustiva y organizada con sumo cuidado. Así, sí podría ponerse en marcha el nuevo directamente. 

Pasado un tiempo prudencial de la puesta en marcha se puede dar por finalizada la implantación. Debe hacerse revisión final para ver si:
- Se han alcanzado los objetivos previstos
- El funcionamiento de los módulos es adecuado
- Los usuarios están formados
- Se ha cumplido el presupuesto o hay desviaciones
- No hay errores, sobrecargas, imprevistos en el sistema. 
### 8.1. Factores de éxito y fracaso en la implantación de un ERP

### Factores de éxito
- Buena dirección del proyecto
- Dotación de medios adecuada
- Implicación y compromiso de toda la organización

### Factores de fracaso
- Falta de liderazgo del equipo directivo: No hay objetivos claros o no existe compromiso de cambio al nuevo sistema
- Resistencia al cambio: Desconfianza en los consultores externos, poca o mala formación, hábitos de trabajo
- Consultores inexpertos sin formación o sin experiencia
- Software ERP poco flexible
- Software ERP con interfaz poco amigable
- Funcionalidad que se atribuyó al ERP pero que este no contempla
- Falta de capacidad y/o recursos técnicos y/o humanos del proyecto

Debe analizarse cuáles son los puntos críticos y solucionarlos poco a poco empezando por los más necesarios. Concienciar a todo el personal de que la implantación no es proceso trivial y que requiere colaboración de todos los que vayan a usarla.

### 8.2. Comenzar con la gestión

Configurado e implantado el sistema deben introducirse datos, crear, configurar todos los módulos.

Según cada empresa se necesitará más o menos parámetros. 

**Gestión de compra-venta**

Compras proveedores, Clientes ventas

1.-Crear clientes /proveedores.
2.-Categorías de productos.
3.-Crear productos.
4.-Crear el stock inicial.
5.-Crear una orden de compra - venta.

**Gestión de almacén**

Almacén: Localización física de elementos de stocks. Albaranes de entrada, de salida e internos. De entrada para recepción, de salida para salida de productos, internos para movientos entre almacenes. 

1.-Crear estructura. 
2.-Crear categorías de productos.
3.-Crear productos.
4.-Crear el stock inicial.
5.-Establecer reglas de abastecimiento.
6.-Comprobar los niveles de stock.

**Gestión de contabilidad**: Información fluir en tiempo real junto con los sistemas de compras. Se abastece de configuración de ejercicios y periodos, diarios, plan contable, impuestos, plazos y tipos de pago y de la actividad diaria del sistema. 

1.-Configuración.
2.-Gestión de facturas.
3.-Gestión de asientos.
4.-Gestión de la conciliación.
5.-Generación de informes.
6.-Cierre de periodos fiscales.
7.-Cierre del año fiscal.

**Gestión de los recursos humanos:** Creación, modificación y mantenimiento de empleados y contratos, control de asistencia, gestión de nóminas

1.-Configuración de asistencia.
2.-Configuración de la empresa.
3.-Configuración de los contratos.
4.-Alta de contratos y empleados.
5.-Gestión de la asistencia.
6.-Nóminas.
7.-Informes.

**Gestión de las relaciones con los clientes**: Según características de la empresa. 

1.-Configuración.
1.1.-Crear iniciativa.
1.1.1.-Crear oportunidad.
1.1.2.-Convertir a presupuesto.
1.2.-Reclamaciones.
1.3.-Ayuda.

### 8.3. Comercio electrónico o e-commerce

Es la compra y venta de productos o servicios a través de medios electrónicos. Consiste en compra y venta entre personas y empresas, aunque también en la adquisición de artículos virtuales.

**Ventajas**:
- **Mejoras en la distribución**: Costos de distribución o ventas que tienden a cero, entregas de inmediato
- **Comunicaciones comerciales por vía electrónica**: Fidelización de clientes mediante dialogo asincrónico a la conveniencia de ambas partes
- **Beneficios operacionales**: Reducción de errores, tiempo, sobrecostes en tratamiento de información. Mercados y segmentos nuevos. Ventajas en las ventas. Mayor facilidad para entrar en nuevos mercados. 
- **Facilidad para fidelizar** clientes

**Características**:
- **Ubicuidad**: Siempre disponible. Marketspace, realizar compras en cualquier lugar.
- **Alcance global**: Llega a todo el mundo
- **Estándares universales**: XML, HTML, CSS...
- **Riqueza**: Una sola experiencia de consumo y mensaje de comercialización
- **Interactividad**: Interacción con el usuario
- **Densidad de información**: Mayor prevalencia, precisión y actualidad. Información abundante, económica y precisa. 
- **Personalización/adecuación**
- **Tecnología social**: Generación de contenido por parte del usuario en redes socciales