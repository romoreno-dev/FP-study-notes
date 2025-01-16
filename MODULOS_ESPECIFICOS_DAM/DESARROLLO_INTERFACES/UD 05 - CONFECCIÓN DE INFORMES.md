
El uso de informes es muy importante para mostrar a los usuarios de la aplicación información organizada en distintos formatos.
## 1. Informes incrustados y no incrustados en la aplicación

Las secciones ya definidas en un informe son: 
- Cabecera: Datos solo visibles en la primera página
- Cuerpo: Datos que se quieren mostrar
- Pie: Datos del pie
A partir de ellas se define la estructura más básica en la que vertebrar un informe. Se complica a medida que se van añadiendo datos agrupados, gráficos, subinformes,...

### 1.1. Instalación de Reporting Services

La herramienta **Reporting Services**, gratuita, ofrece una serie de plantillas determinadas para el entorno de desarrollo Visual Studio que están disponibles si están instaladas las opciones del software SQL Server. 

Servidores asociados a SQL Server tienen dos modos de autentificarse:
- **Seguridad Windows integrada**: Hace uso de las credenciales del usuario para autentificarse en el servidor. Las cuentas que se usan son cuentas locales del propio SO o del propio domino
- **Modo mixto**: Puede usar un modo de autenticación mediante usuario y contraseña. Una de las cuentas que se usa es la cuenta "sa" (superadministrador) que permite representar al administrador del servidor. 

Finalizado el proceso de instalación debe comprobarse si se han creado dos bases de datos nuevas en el servidor de BBDD con el prefijo "ReportServer". Serán las encargadas de guardar metadatos además de alguna configuración del servidor de informes. 

### 1.2. Creación de un informe

Visual Studio > Business Inteligence. 
Hay plantillas para crear los proyectos relacionados con explotación de datos como informes, migración y transformación de datos.  Se deben usar los llamados Reporting Services.

Estos tienen dos plantillas parecidas en estructura y en funciones. 
Aparta al usuario de detalles complejos para conseguir que la tarea sea lo más sencilla posible. 

La plantilla **Report Server Project** permite crear un proyecto sin ningún asistente, solo con los archivos necesarios para la solución.
Se obtiene una interfaz que cuenta con la estructura del proyecto como una imagen en la que se pueden ver tres carpetas. 

#### Primero: Selección de datos
Deben identificarse primero lo que se debe representar en el informe y los datos que van a ser necesarios para ellos y el origen de los datos. 
Con el identificador `DsAdventure` es posible representar una estructura que contenta todos los datos que se seleccionen. 

#### Segundo: Layout - Estructura visual
Los datos pueden representarse en:
 - Formato tabular
 - Estructura matriz
Pueden organizarse los datos generando distintas agrupaciones por páginas o grupo de datos.

El **Generador de consultas** es el asistente existente para la selección de datos y permite crear grupo de datos. 

Es conveniente que la organización  de los datos la ejecute el entorno del servidor de la BBDD para mayor optimización y rendimiento. 

#### Tercero: Exportación de la información

Se puede exportar a formatos como csv, pdf o a otras bases de datos. 
#### Cuarto: Organización del informe

Transmite un análisis de determinados aspectos a partir de los datos existentes. Se diferencia entre: 
- **Cabecera**: Al principio del documento
- **Cuerpo**: Repite la estructura tantas veces como tuplas haya en el origen de datos
- **Pie:** Se repite una vez al final del documento
(_Incluir una sección pulsando la zona del informe mediante botón derecho o con opción del menú Report_)

Cada sección creada debe tener su personalización.

**Añadir cabecera/pie**
Se pueden crear secciones haciendo uso de agrupación de datos, haciendo su cabecera y su pie.
Cada agrupación tiene cabecera y pie que puede usarse o no.
En la agrupación se tendrá que definir el campo o campos que se desean agrupar. En caso de que haya varios campos, se tiene que definir el orden en el que se realiza la agrupación.
El encabezado y el pie estarán en la fila superior e inferior adjuntas a los datos (obviamente...)

Cuando se crean grupos, puede llevar a confusión cuando existen distintas páginas ya que se puede perder visibilidad del campo por el que se agrupa. 
## 2. Creación de parámetros

Los **parámetros** permiten aumentar la funcionalidad de un informe dándole mayor flexibilidad para mostrar los datos. 
Se pueden crear ""informes activos"", que adaptan su información a los valores que se facilitan. 

**Propiedades**
- Tipo de valor a recibir
- Descripción para identificar qué tipo de datos se espera 
**Valores**
- Libres o de entre una lista de posibles valores (obtenidas de BBDD o de un conjunto cerrado; permite evitar los problemas típicos de introducir valores no esperados por la aplicación)
**Valores predeterminados**
- Funcionamiento en caso de no disponer de valor para evitar la aparición de excepciones no controladas. 
**Actualización de informes**
- Importante que se refresque el informe para que los datos se vayan almacenando. Así si el cliente solicita respuesta inmediata, obtendrá los datos más actuales. 

## 3. Creación de subinformes

Permite crear una **Relación jerárquica** entre varios informes. (Informe padre e informes hijos). Pueden tener una unión basada en los datos de forma que el informe principal facilita datos al subordinado mediante los parámetros de este último. 

Se puede iniciar a partir de dos _Dataset_  en los que hay un elemento de enlace. A partir del elemento aparece la opción de poder relacionar la información que hay entre ellos. 

1. Inicialmente **se define la estructura del informe** (tablas, listados, matrices)
Si se selecciona una tabla esta será más veloz que las demás estructuras disponibles y se rellenará los campos de forma automática simplemente arrastrando y soltando desde el Dataset.

2. En el subinforme puede usarse uno ya creado y el desarrollador se puede centrar en su aspecto visual. El resto puede ser igual ya que se comporta como un informe más con su origen de datos filtrado, parámetros formato,...

3. Seguidamente se definen las vías de comunicación entre el informe principal y el subinforme mediante parámetros. Esta definición de parámetros puede afectar al origen de datos por lo que es importante parametrizar la consulta.

4. En el informe principal, una vez insertado el subreport, se puede determinar de dónde obtener los valores facilitados como parámetros. Así se comunican informe principal y subinforme. El nombre del parámetro definido como entrada en el subinforme y el del parámetro que se facilita deben ser iguales. Si no, no se obtendrán los resultados esperados. 

## 5.4. Imágenes

Con las imágenes se consigue un informe más profesional y formal (¡no me digas!)

## 5.5. Informes incrustados y no incrustados en la aplicación

#### Integración de informes

Los informes **incrustados** son integrados en una determinada aplicación. Para ello se hace uso de un contenedor en la aplicación que muestra el contenido del informe (lo interpreta mostrando cómo se ha definido parámetros, layouts, filtros,...)

En las aplicaciones WPF se usa el contenedor `WindowsFormHost`. Permite usar controles `Windows Form`. Debe añadirse el control `ReportViewer` diferenciándolo (identificado mediante el ensamblado: `Microsoft.ReportViewer.WinForms`)

Al hacer la selección, deben elegirse librerías con las versiones adecuadas. 

En la codificación deben considerarse la definición de propiedades de control `ReportViewer` y el uso de las propiedades `LocalResport` en la que se puede seleccionar dónde comienzan los datos del informe. 

El acceso directo al informe en el caso de Reporting Services puede hacerse mediante el uso de HTTP. También puede visualizarse mediante el uso de controles que actúan como contenedores para mostrar diferente contenido web. 

## 5.6. Herramientas gráficas integradas y externas al IDE

Los **gráficos** son herramientas usadas para obtener información importante. **Se suelen usar en informes globales** dirigidos a conocer el estado de situación. Las tablas en cambio se usan en actividades de nivel menos importante (¿¿¿¿¿??????)

## 5.7. Filtrado de datos

Con el **filtrado de datos** se pueden especificar los filtros que se necesitan para los datos extraídos. 

Lo ideal es hacer desde el principio consultas optimizadas para el tipo de datos que se quieren mostrar en el informe.

Hay herramientas para perfeccionar los datos que se usan hasta acercarse a las necesidades especificadas por el diseñador. 

**Propiedades del Dataset**
Con el objeto `Dataset` se disponen de un conjunto de estructuras y datos seleccionables a partir de las bases de datos.
Se pueden identificar los nombres y las características que se pueden emplear en el informe. 
Se pueden filtrar datos, llevar a cabos operaciones diversas,...

## 5.8. Numeración de líneas, recuentos y totales

Existen **funciones resumen** de una serie de datos (vinculadas a las operaciones de agrupación `GROUP BY`). 
Por ejemplo puede crearse un informe para saber el número de líneas que tiene cada elemento. 
En lugar de hacer consulta que incluya el valor a buscar, se puede separar los datos y su origen de la representación.
Se podría crear una columna con la organización actual y realizar una búsqueda sobre una función o campo que ofrezca la posibilidad de mostrar la información deseada. 

Parámetro que facilita la expresión `RowNumber` en la que se puede especificar el conjunto de datos para contar las líneas correspondientes. Se puede poner en el informe un nuevo valor que ejecute la suma de todos los bonus generados. 

## 5.9. Librerías para la generación de informes, clases, métodos y atributos

_Reporting Services_ proporciona una API con funciones que permiten al desarrollador la integración en distintos tipos de aplicaciones. Es posible usarla en:
- **Servicios web SOAP con todas las funciones.** Informes con protocolo SOAP (Simple Object Access Protocol). Ofrece las diferentes propiedades del servidor de informes y permite crear nuevas herramientas personalizadas para usar en cualquiera de las partes del informe
- **Comandos basados en URL**. Envío de comandos al servidor de informes mediante una URL. Usados para introducir informes en una pagina web.
- **WMI (Windows Management Instrumentation)**. A través de la API facilitada por el sistema operativo es posible hacer uso de una serie de métodos que dependerán de los mecanismos de acceso definidos por la WMI. 
- **Extensiones modulares**: Personalización de las clases que se usa a la hora de crear, diseñar y visualizar informes.
- **Programación RDL**: Declarar informe mediante RDL (_Report Definition Language_) a través de XML. Se puede modificar y configurar el informe tanto en aspecto como en funciones. 


## 6. (Lo que importa de verdad) JasperReport


> No entra pero me parecía horrible el temario así que decidí meterlo

## 6.1. Introducción

Herramienta que consta de un poderoso motor para la generación de informes. Está escrita en Java, empaquetada en un JAR y puede usarse como librería. 
Es de código abierto y gratuita con licencia GPL. 
Permite generar informes de todo tipo en Java de una forma sencilla. En formatos PDF, XLS, HTML, RTF, CSV, XML...

Descarga: https://sourceforge.net/projects/jasperreports/files/jasperreports/

Una vez descargado en Netbeans se haría click en Tools > Libraries > New Library para añadir la librería.
En Classpath tab se añade el fichero `jasperreports-miversion.jar` de la carpeta `dist` y algunos `commons-....` que puedan ser necesarios. (beanutis, collections, digester, javaflow, logging). Igualmente se indica el directorio fuente (src) de JasperReport. 
En Javadoc se añade la carpeta API de jasperreports. 

Directorios al descomprimir:
- **build**: Librería JasperReports sin empaquetar
- **demo**: Ejemplos de uso de la librería. Algunos preparados para ser compilados con Ant
- **dist**: Librería empaquetada en fichero JAR 
- **docs**: Referencia rápida en formato XML
- **lib**: Librerías necesarias para JasperReports (exportar distintos formatos, incluir gráficos)
- **src**: Ficheros fuente de la librería

#### A. Diseño

Las plantillas de JasperReports son ficheros XML con extensión **.jrxml**. Es un archivo XML que mantiene la estructura de un archivo DTD definido en el motor de JasperReports.
Debe estar validada con
```xml
<!DOCTYPE jasperReport PUBLIC "-//JasperReports//DTD Report Design//EN" "http://jasperreports.sourceforge.net/dtds/jasperreport.dtd">
```

Puede ponerse en Maven con 
```xml
<dependency>  
    <groupId>net.sf.jasperreports</groupId>  
    <artifactId>jasperreports</artifactId>  
    <version>3.7.5</version>  
</dependency>
```

(Última versión **6.21.3**; 17 de abril de 2024)

Tiene las secciones:
- **title**: Título del informe
- **pageHeader**: Encabezado del documento
- **columnHeader**: Encabezado de las columnas
- **detail**: Detalle del documento. Cuerpo.
- **columnFooter**: Pie de la columna
- **pageFooter**: Pie del documento
- **summary**: Cierre del documento

```xml
<?xml version="1.0" encoding="UTF-8"?>
<jasperReport xmlns="http://jasperreports.sourceforge.net/jasperreports"
              xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
              xsi:schemaLocation="http://jasperreports.sourceforge.net/jasperreports http://jasperreports.sourceforge.net/xsd/jasperreport.xsd"
              name="reporte_ejemplo"
              pageWidth="595" pageHeight="842"
              columnWidth="555" leftMargin="20" rightMargin="20" topMargin="20" bottomMargin="20"
              uuid="ce7f8d0b-d7b7-4d3d-8b12-36240dc238b8">
    
    <!-- Título del informe -->
    <title>
        <band height="50">
            <staticText>
                <reportElement x="0" y="0" width="555" height="50" uuid="517e32af-64c4-4b82-860a-2d6506be0294"/>
                <textElement textAlignment="Center">
                    <font size="20" isBold="true"/>
                </textElement>
                <text><![CDATA[Título del Informe]]></text>
            </staticText>
        </band>
    </title>
    
    <!-- Encabezado de página -->
    <pageHeader>
        <!-- Aquí puedes colocar elementos como el nombre de la empresa, el logotipo, etc. -->
    </pageHeader>
    
    <!-- Encabezado de columnas -->
    <columnHeader>
        <band height="30">
            <!-- Definición de las cabeceras de las columnas -->
            <staticText>
                <reportElement x="0" y="0" width="100" height="30" uuid="062a35ff-8499-47e5-b61e-0bbec74a5ab0"/>
                <text><![CDATA[Nombre]]></text>
            </staticText>
            <staticText>
                <reportElement x="100" y="0" width="100" height="30" uuid="287c1601-8b21-4389-b26e-d6e8a0ec2330"/>
                <text><![CDATA[Apellido]]></text>
            </staticText>
            <staticText>
                <reportElement x="200" y="0" width="100" height="30" uuid="cc7ad76e-d167-4f48-b869-b5de16171e7b"/>
                <text><![CDATA[Edad]]></text>
            </staticText>
        </band>
    </columnHeader>
    
    <!-- Detalle del informe -->
    <detail>
        <band height="30">
            <!-- Aquí se colocarían los datos de cada registro -->
        </band>
    </detail>
    
    <!-- Pie de columna -->
    <columnFooter>
        <!-- Aquí puedes incluir sumarios o totales parciales para las columnas -->
    </columnFooter>
    
    <!-- Pie de página -->
    <pageFooter>
        <!-- Aquí se incluiría información como números de página, fechas, etc. -->
    </pageFooter>
    
    <!-- Resumen del informe -->
    <summary>
        <!-- Aquí se colocaría cualquier información de resumen o cierre del informe -->
    </summary>
</jasperReport>

```

#### B. Compilación

Debe compilarse tras el diseño. Se hace a través del método `compileReport()`. El diseño se transforma en objeto serializable de tipo net.sf.jasperreports.engine.JasperReport que se guarda en disco. 

#### C. Rellenar el informe con datos

Los métodos `fillReportXXXX()` realizan la carga de datos del informe, pasándole como parámetros el objeto de diseño (o el archivo que lo representa en formato serializado .jasper) y la conexión JDBC a la base de datos desde donde se obtendrá la información que se necesite. 

Se obtiene un objeto que representa al documento listo para ser impreso, un objeto serializable de tipo `JasperPrint`. Este objeto puede ser guardado en disco, impreso, enviado a pantalla, transformado en PDF, XLS, XSV...
#### D. Visualización

Se puede mostrar un informe por pantalla, imprimirlo, obtenerlo en tipo específico de fichero...

**Mostrar informe por pantalla**: `JasperViewer` que en su método `main()` recibe el informe a mostrar
**Imprimir el informe**: `JasperPrintManager` Métodos `printReport()`, `printPage()`, `printPages()`
**Exportar los datos a formato de archivo específico**: `exportReportXXX()`

## 6.2 JasperReports y NetBeans

- Crear proyecto de tipo Java Application y darle nombre
- Botón derecho sobre el nombre del proyecto > Properties > Categories > Libraries > Add Library > elegimos JasperReports-xxxx > Add Library > Ok
- Carpetas en las que se guardarán las plantillas y los informes generados. `report` y como subdirectorios `templates` y `results`. 
- Se crea plantilla File > Empty File . `HolaMundo.jrxml`con el siguiente código:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE jasperReport PUBLIC "-//JasperReports//DTD Report Design//EN" "http://jasperreports.sourceforge.net/dtds/jasperreport.dtd">
<jasperReport name="HelloReportWorld">
    <parameter name="author" class="java.lang.String"/>

    <detail>
        <band height="200">
            <staticText>
                <reportElement x="0" y="0" width="500" height="20"/>
                <text><![CDATA[Informe ¡Hola Mundo!]]></text>
            </staticText>
        </band>
    </detail>
    <columnFooter>
        <band height="200">
            <textField>
                <reportElement x="0" y="0" width="200" height="30"/>
                <textElement>
                    <font size="14" isBold="true"/>
                </textElement>
                <textFieldExpression><![CDATA["Autor: " + $P{author}]]></textFieldExpression>
            </textField>
        </band>
    </columnFooter>
</jasperReport>
```


- Y el código siguiente: 
```java
public class Main {
    public static void main(String[] args) throws Exception {
        String reportSource = "src/main/resources/reports/templates/HolaMundo.jrxml";
        String reportsDest = "src/main/resources/reports/results/HolaMundo";

        Map<String, Object> params = new HashMap<>();
        params.put("author","romoreno-dev");
        try {
            JasperReport jasperReport = JasperCompileManager.compileReport(reportSource);
            JasperPrint jasperPrint = JasperFillManager.fillReport(jasperReport, params, new JREmptyDataSource());

            JasperExportManager.exportReportToHtmlFile(jasperPrint, reportsDest+".html");
            JasperExportManager.exportReportToPdfFile(jasperPrint, reportsDest+".pdf");

            JasperViewer.viewReport(jasperPrint);
        } catch (JRException e) {
            System.out.println(e.getMessage());
        }
    }
}
```

- **JasperCompileManager.compileReport**: Toma la plantilla jrxml y la compila a bytecode (instancia `JasperReports`), serializable a disco como fichero jasper. Las plantillas compiladas pueden (y deben) reutilizarse sin recompilarlas salvo que cambie el código fuente de la plantilla. 
 
- **JasperFillManager.fillReport**: Toma el informe compilado (instancia `JasperReports`), unos parámetros definidos por el desarrollador y unos datos `JasperReports` y rellena la instancia informe con parámetros y datos retornando una instancia `JasperPrint`. Esta es una representación de objeto del informe completo. 
        
- **JasperExportManager.exportReportToHtmlFile**: Con la instancia `JasperPrint` y la ruta de destino de fichero  se crea fichero HTML con contenido del informe. 

Se admiten formatos PDF, XML, CSV (comma-separated values), XLS, RTF, fichero de texto y se pueden crear ficheros de formato personalizados para exportar con la API extensible de JasperReports. 

- **JasperExportManager.viewReport**. Muestra el informe generado en el visor **JasperReport Viewer.**

## 6.3. Ejemplitos JasperReport

### 6.3.1. Parámetros para personalizar informes 

``` java
Map<String, Object> parameters = new HashMap<>();
parameters.put("CUSTOMER_NAME", "Juan Pérez");
parameters.put("INVOICE_DATE", new Date());

JasperPrint jasperPrint = JasperFillManager.fillReport("fichero.jasper", parameters, connection);
JasperExportManager.exportReportToPdfFile(jasperPrint, "output.pdf");
```

```xml
<parameter name="CUSTOMER_NAME" class="java.lang.String"/>
<parameter name="INVOICE_DATE" class="java.util.Date"/>

<textField>
    <reportElement x="50" y="50" width="200" height="30"/>
    <textFieldExpression><![CDATA[$P{CUSTOMER_NAME}]]></textFieldExpression>
</textField>

<textField>
    <reportElement x="50" y="80" width="200" height="30"/>
    <textFieldExpression><![CDATA[new SimpleDateFormat("dd/MM/yyyy").format($P{INVOICE_DATE})]]></textFieldExpression>
</textField>
```

### 6.3.2 Subreport para incluir tablas de detalle

```java
parameters.put("SUBREPORT_DIR", "subreports/");

JasperPrint jasperPrint = JasperFillManager.fillReport("invoice.jasper", parameters, connection);
```

```xml
<subreport>
    <reportElement x="0" y="150" width="500" height="200"/>
    <subreportExpression><![CDATA[$P{SUBREPORT_DIR} + "invoice_items.jasper"]]></subreportExpression>
</subreport>
```


### 6.3.3 Gráficos para estadísticas

Ejemplo de un gráfico de barras que muestra impuestos aplicados:


```xml
<chart>
    <reportElement x="50" y="400" width="300" height="200"/>
    <chartTitleExpression><![CDATA["Impuestos Aplicados"]]></chartTitleExpression>
    <categoryDataset>
        <datasetRun subDataset="TaxDataset">
            <datasetParameter name="INVOICE_ID">
                <datasetParameterExpression><![CDATA[$P{INVOICE_ID}]]></datasetParameterExpression>
            </datasetParameter>
        </datasetRun>
    </categoryDataset>
    <barPlot>
        <valueAxisLabelExpression><![CDATA["Monto"]]></valueAxisLabelExpression>
    </barPlot>
</chart>

```

### 6.3.4. Cálculos dinámicos

```xml
<variable name="SUBTOTAL" class="java.lang.Double" calculation="Sum">
    <variableExpression><![CDATA[$F{PRICE} * $F{QUANTITY}]]></variableExpression>
</variable>
```

### 6.3.5. Exportación a diferentes formatos 

```java
// Exportar a PDF
JasperExportManager.exportReportToPdfFile(jasperPrint, "invoice.pdf");

// Exportar a Excel
JRXlsxExporter exporter = new JRXlsxExporter();
exporter.setExporterInput(new SimpleExporterInput(jasperPrint));
exporter.setExporterOutput(new SimpleOutputStreamExporterOutput("invoice.xlsx"));

SimpleXlsxReportConfiguration configuration = new SimpleXlsxReportConfiguration();
configuration.setOnePagePerSheet(true);
exporter.setConfiguration(configuration);

exporter.exportReport();
```

### 6.3.6. Estilos 

```xml
<style name="TitleStyle" isDefault="true">
    <font size="16" isBold="true"/>
    <textAlignment>Center</textAlignment>
</style>

<textField>
    <reportElement x="50" y="10" width="400" height="50" style="TitleStyle"/>
    <textFieldExpression><![CDATA["Factura"]]></textFieldExpression>
</textField>
```

### 6.3.7. Mostrar imágenes 

Estática:
```xml
<image>
    <reportElement x="50" y="10" width="200" height="100"/>
    <imageExpression><![CDATA["/path/to/image/logo.png"]]></imageExpression>
</image>
```

Dinámica:
```xml
<image>
    <reportElement x="50" y="10" width="200" height="100"/>
    <imageExpression><![CDATA[$P{LOGO_URL}]]></imageExpression>
</image>
```
### 6.3.8. Consultas y fields 

Las consultas extraen datos desde una fuente, y los `Fields` se usan para mapear los datos del resultado en el informe.

**Definir una consulta en el JRXML**

```xml
<queryString>
    <![CDATA[SELECT product_name, price, quantity FROM products WHERE invoice_id = $P{INVOICE_ID}]]>
</queryString>
```

**Mapear los campos (`Fields`)**

```xml
<field name="product_name" class="java.lang.String"/>
<field name="price" class="java.lang.Double"/>

<textField>
    <reportElement x="50" y="100" width="200" height="30"/>
    <textFieldExpression><![CDATA[$F{product_name}]]></textFieldExpression>
</textField>

<textField>
    <reportElement x="300" y="100" width="100" height="30"/>
    <textFieldExpression><![CDATA[$F{price}]]></textFieldExpression>
</textField>
```

Consulta con parámetros dinámicos:

En Java se pasa el parámetro:
```java
parameters.put("CUSTOMER_ID", 12345);
JasperPrint jasperPrint = JasperFillManager.fillReport("report.jasper", parameters, connection);
```

Y luego en el informe:
```xml
<queryString>
    <![CDATA[SELECT * FROM orders WHERE customer_id = $P{CUSTOMER_ID}]]>
</queryString>
```

### 6.3.9. Pasar parámetros al subreport 

En el informe principal:

```xml
<parameter name="INVOICE_ID" class="java.lang.Integer"/>

<subreport>
    <reportElement x="50" y="200" width="500" height="300"/>
    <subreportParameter name="INVOICE_ID">
        <subreportParameterExpression><![CDATA[$P{INVOICE_ID}]]></subreportParameterExpression>
    </subreportParameter>
    <subreportExpression><![CDATA["subreports/invoice_items.jasper"]]></subreportExpression>
</subreport>
```

En el subreport: 

```xml
<parameter name="INVOICE_ID" class="java.lang.Integer"/>

<queryString>
    <![CDATA[SELECT * FROM invoice_items WHERE invoice_id = $P{INVOICE_ID}]]>
</queryString>
```

### 6.3.10 Scriplets

Estas clases implementan la interfaz `JRScriptlet` o extienden la clase base `JRDefaultScriptlet`.

Los _scriplets_ en JasperReports son clases personalizadas que puedes usar para extender la lógica del informe. Estas clases implementan la interfaz `JRScriptlet` o extienden la clase base `JRDefaultScriptlet`. Esto te permite incluir lógica adicional en eventos específicos del ciclo de vida del informe y realizar operaciones avanzadas.

####  `afterReportInit`

Se invoca **después** de que el informe haya sido inicializado, pero antes de que se procesen los datos.
Usos comunes:
- Inicializar variables globales.
- Preparar datos o configuraciones antes de generar el informe.
- Conectar con APIs externas o servicios.

####  `beforeDetailEval`

Se ejecuta **antes de evaluar cada registro** en la sección de detalles del informe.

Usos comunes:
- Realizar cálculos dinámicos para cada registro.
- Modificar datos antes de mostrarlos en el informe.
- Validar o transformar campos en tiempo de ejecución.

```java
public class CustomScriptlet extends JRDefaultScriptlet {
    @Override
    public void afterReportInit() throws JRScriptletException {
        // Ejemplo: inicializar un valor global
        this.setVariableValue("GLOBAL_DISCOUNT", 10.0);
    }

    @Override
    public void beforeDetailEval() throws JRScriptletException {
        // Ejemplo: cálculos dinámicos por cada registro
        Double price = (Double) this.getFieldValue("price");
        Double discount = price * 0.10;
        this.setVariableValue("DISCOUNTED_PRICE", price - discount);
    }
    
	public String formatCurrency(Double amount) {
	 return String.format("$%.2f", amount); 
	 }
}
```

Para que JasperReports sepa que estás utilizando un scriptlet personalizado, debes declarar el parámetro especial `REPORT_SCRIPTLET` en el JRXML. Esto no siempre es necesario, pero es una buena práctica para evitar errores.
```xml 
<parameter name="REPORT_SCRIPTLET" class="net.sf.jasperreports.engine.JRScriptlet"/>
```


```xml
<scriptletClass>com.example.CustomScriptlet</scriptletClass>

<variable name="DISCOUNTED_PRICE" class="java.lang.Double" calculation="Nothing">
    <variableExpression><![CDATA[0.0]]></variableExpression>
</variable>

<textField>
    <reportElement x="300" y="150" width="100" height="30"/>
    <textFieldExpression><![CDATA[$V{DISCOUNTED_PRICE}]]></textFieldExpression>
</textField>

<textField>
    <reportElement x="50" y="100" width="200" height="30"/>
    <textFieldExpression><![CDATA[$P{REPORT_SCRIPTLET}.formatCurrency($F{price})]]></textFieldExpression>
</textField>
```

Otros métodos que puedes sobrescribir según tus necesidades:
- **`beforeReportInit`**: Se ejecuta antes de que el informe se inicialice. Útil para configurar parámetros o realizar operaciones previas.
- **`afterDetailEval`**: Se ejecuta después de evaluar cada registro en la sección de detalles. Útil para acumular datos o registrar información.
- **`beforePageInit` y `afterPageInit`**: Se ejecutan antes y después de que se procese cada página del informe. Útiles para configuraciones específicas por página.
- **`beforeColumnInit` y `afterColumnInit`**: Se ejecutan antes y después de procesar cada columna. Útiles para informes con columnas múltiples. (Cuando hablamos de columnas múltiples en JasperReports, nos referimos al diseño de informes que organiza los datos en varias columnas dentro de una página, como si fuera un catálogo o lista estilo periódico.)

