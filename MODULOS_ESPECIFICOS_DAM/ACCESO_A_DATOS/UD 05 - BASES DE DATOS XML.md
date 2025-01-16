
## 1. Introducción. Comparativa con BD relacionales

Según el nivel de estructuración se puede diferenciar:
- **Datos estructurados**. Tienen un formato estricto. Toda la información recogida se ajusta al mismo formato. Ej.: Datos tabulados en filas y columnas de una tabla.
- **Datos desestructurados**. No tienen ninguna estructura. Ej.: Documento de texto o un archivo de vídeo.
- **Datos semi-estructurados**. Tienen cierta estructura, pero no toda la información recogida tiene la misma forma, y además puede ir variando de manera dinámica.

Bases de datos relacionales son apropiadas para datos estructurados. Pero en la actualidad en muchas situaciones interesa almacenar grandes volúmenes de datos no estructurados e incluso integrarlos con datos estructurados. 

#### Utilización de XML para almacenamiento de información

- XML es lenguaje bien formado.
- Extensible. Permite ampliar el lenguaje con nuevas etiquetas y definición e lenguajes neuvos
- Fácil de leer
- Autodescriptivo
- Intercambiable. Portable
- Para su lectura e interpretación es necesario un parser.
- Ha sido ampliamente aceptado y adoptado para almacenar e intercambiar información. 

 **Base de datos XML**: Colección de documentos XML (<small>archivo en el sistema de archivos con cadena válida XML</small>) en la que cada uno representa un registro. Buscan una estrategia para almacenar y recuperar datos pocos estructurados con la misma eficiencia que las relacionales. 

----------

**Principios ACID de las bases de datos relacionales**

| Atomicidad   | Asegura que la transacción se completa o no sin quedarse a medias. |
| ------------ | ------------------------------------------------------------------ |
| Consistencia | Se asegura que los datos son correctos .                           |
| Aislamiento  | Independencia de las transacciones                                 |
| Durabilidad  | Persistencia de la transacción ante cualquier fallo.               |

**Los sistemas más modernos se basan en el principio BASE**

| Basic Availability     | Disponibilidad de los datos es la PRIORIDAD                                                         |
| ---------------------- | --------------------------------------------------------------------------------------------------- |
| Soft state             | Se prioriza la propagación de datos. Inconsistencias se dejan a agentes externos                    |
| Eventually consistency | Se acepta que las inconsistencias temporales siempre que acaben progresando a estado final estable. |

**NOSQL frente a SQL**

| NoSQL                     | SQL                                                                            |                                                                |
| ------------------------- | ------------------------------------------------------------------------------ | -------------------------------------------------------------- |
| Lenguaje de consultas     | Cassandra-->CQL<br><br>MongoDB-->JSON<br><br>BigTable-->GQL                    | Lenguaje SQL                                                   |
| Modelos de almacenamiento | Sistemas clave-valor, objetos o grafos                                         | estructuras fijas, tablas.                                     |
| Operaciones JOIN          | No son deseables por la sobrecarga al disponer de un volumen de datos grande . | Se realizan normalmente.                                       |
| Arquitectura distribuida  | Compartida en varias máquinas, mecanismos de tablas Hash distribuidas.         | Centralizadas en una sola máquina o estructura máster-esclavo. |

### 1.1. Documentos XML. Centrados en datos y centrados en documentos

El almacenamiento de datos se podría dividir en dos categorías:

**Centrados en los datos**
- Muchos elementos, poco contenido
- Estructura bien definida y esquemas de datos estructurados o semiestructurados (factura, albarán, pedidos, ficha)
- Muchos datos de pequeño tamaño
- Dirigidos a su por máquinas (automática)
- Apropiados para publicidad
- Los datos pueden actualizarse
- Planos. Poca importancia al orden. 

**Centrados en el texto, contenido documentos**
- Pocos elementos, mucho contenido
- Estructuras impredecibles en tamaño y contenido
- Poco estructurados
- Orientados a humanos
- Enfocados a sistemas documentales y de gestión de contenidos (libros de texto, manuales, informes) 

### 1.2. Opciones de almacenamiento

  
Para almacenar documentos XML, las opciones son:

1. **Almacenamiento directo en el sistema de archivos**: Limitado en operaciones y funcionalidad.
2. **Almacenamiento en una base de datos existente** (relacional, orientada a objetos, objeto-relacional):
    - **En una columna tipo BLOB dentro de una tabla**: Se almacena el conjunto estático. Es adecuado para contenido estático que será modificado con el reemplazo del documento concreto. Almacenar el documento completo en formato de texto es fácil de implementar pero limita consultas y búsqueda de contenido. 
    - **Mapeo basado en tablas u objetos**: Requiere transformación para ajustarlo a la estructura de la BBDD, conlleva pérdida de información y dificulta consultas complejas. Su formato no es intacto yn o se recupera de forma intacta. No es posible controlar todas las estructura del documento. 
3. **Almacenamiento en una base de datos nativa XML**:
    - Conserva el documento intacto.
    - Mejor opción, especialmente para documentos basados en texto.


Actualmente, cada vez las BD ofrecen posibilidades de almacenamiento XML. Se habla de BD XML-compatible o BL XML-enabled. 

**Hay dos tipos de sistemas que soporten documentos XML: **
- BD XML-compatibles: Desglosan documento XML en modelo relacional o de objetos
- BD XML Nativas. Respetan la estructura del documento. Permiten hacer consultas sobre la estructura y recuperar el documento tal cual fue insertado originalmente. 

**BD XML Nativas proporcionan modelo de datos propio** mientras que **BD XML-compatible ya tiene un modelo de datos** y **añade una capa de software** que de alguna manera almacena documentos XML y recupera los datos generando nuevos documentos.

**BD XML nativa** debe manejar todos los tipos de documentos posibles y **BD XML-compatible solo puede manejar los que encajan con su modelo definido**. 

Rounald Bourret es uno de los más importantes investigadores sobre BD XML. 

## 2. Bases de datos nativas XML


Las bases de datos nativas XML siguen evolucionando (aunque existen desde hace años). Una BD XML (NXD, Native XML Database) debe cumplir las siguientes propiedades:
- **Define un modelo lógico de datos XML**: Estableciendo elementos significativos de forma que el modelo pueda almacenarse y recuperarse de forma intacta; con todos sus componentes. Debe tener en cuenta elementos, atributos, texto, secciones CDATA y preservar el orden en el documento.
- **Documento XML es la unidad lógica de almacenamiento**: Unidad mínima de almacenamiento
- **No hay modelo de almacenamiento físico subyacente concreto**: Pueden construirse en bases de datos relacionales, jerárquicas, orientadas a objetos o en formatos propietarios
- **Permiten tecnologías de consulta y transformación propias de XML** Como XML, XQuery, XPath, XSLT.

**Ventajas**
- Acceso y almacenamiento de información directamente en formato XML, sin necesidad de código adicional
- Almacenamiento de datos heterogéneos
- Motor de búsqueda de alto rendimiento
- Facilidad para incorporar nuevos XML al repositorio

**Inconvenientes**
- Dificultad para indexar documentos al hacer búsquedas
- Las información XML se almacena como un documento o un conjunto de nodos. Las síntesis para formar nuevas estructuras puede ser compleja o lenta.

**¿Cuándo es imprescindible?**
- Documentos con anidamientos profundos
- Importancia de preservar integridad del documento
- Búsqueda frecuente de contenido

### 2.1. Estrategias de almacenamiento

Según el tipo de almacenamiento:

- **Almacenamiento basado en texto**: Almacenar el documento XML entero en forma de texto (fichero de texto) y dar funcionalidad de BBDD para acceder a él. Se aplican técnicas de comprensión, se usan índices adicionales para mejorar el acceso y pueden definirse sobre BD tradicionales o sistemas de ficheros. Posibilidades:
	- Almacenar documento como binario largo (BLOB) en BBDD relacional o mediante fichero y dar índices sobre el documento que aceleren el acceso
	- Almacenar el documento en almacén adecuado con índices, soportes de transacciones...


- **Almacenamiento basado en modelo**: Definir un modelo de datos lógico como DOM para la estructura jerárquica de los documentos XML y almacenar el modelo binario del documento en almacén existente o específico. Posibilidades:
	- Traducir el DOM a tablas relacionales (elementos, atributos, entidades
	- Traducir el DOM a objetos en BDOO
	- Utilizar almacén creado para esta finalidad.

- **Soluciones específicas para gestión de documentos XML**: 
##### Ejemplos de BD XML Nativas
Sistema relacional: eXist, DBCOM, XDB
Sistema orientado a objetos: Ozone, MindSuite XDB
Sistema propietario: XIndice, Virtuoso, Tamino XML Server, Base X

**Ventajas de BD XML Nativas**
- No necesitan mapeo adicional
- Conservan la integridad de los documentos
- Permiten almacenar documentos heterogéneos


#### Reglas de transformación de bases de datos relacional a XML. Creación del DTD.

La estructura XML debe acomodar clases primarias, secundarias, tablas y columnas. Pueden existir muchas variaciones de esquemas XML para representar la misma base de datos relacional. 

El proceso de traducción de BBDD relacional a XML podría seguir los siguientes pasos:
- **Crear el esquema XML:** con un elemento para cada tabla y los atributos para cada columna no clave.  Columnas que no permiten valores nulos deben ser marcadas como requeridas; Columnas que permiten valores nulos deben ser marcadas como opcionales. En lugar de atributos podrían anidarse las columnas como elementos pero eso puede dar problemas si existe el mismo nombre de columna en más de una tabla. 

* **Crear claves primarias en el esquema XML:** Para las columnas que son claves primarias puede agregarse un atributo con un ID. Y en el esquema XML definirlo como de tipo ID. Pueden surgir problemas de colisión al crear las claves en el XML porque el ID necesita ser único en todo el documento. Podría añadirse el nombre del elemento (nombre de la tabla), al valor la clave primaria (valor del atributo) para que sea único a través del documento XML.

* **Establecer relaciones de clave migrada o foránea**: Se puede anidar bajo el elemento padre, un ID de esquema XML puede ser usado para apuntar a la estructura XML correspondiente conteniendo un IDREF. 

Se caracterizan por: 
- **Almacenamiento de documentos en colecciones.** Base de datos estructurada en colecciones (conjunto de documentos), de modo que es estructura de árbol donde cada documento pertenece a una única colección. 
- **Validación de documentos**
- **Consultas**:  Utilizando el lenguaje **XQuery**
- **Indexación XML**: Índices que aceleran las consultas
- **Identificadores únicos**: Asociados a cada documento XML
- Actualizaciones y borrados:
	- Almacenamiento basado en texto: Almacena el documento XML entero en forma de texto y proporciona forma de acceder a él
		- Posibilidad 1: Lo almacena como BLOB en base de datos relacional por fichero y da índices que aceleren el acceso a la información
		- Posibilidad 2: Almacena en un almacén adecuado con índices, soporte para transacciones, etc
	- Almacenamiento basado en el modelo: Almacena modelo binario del documento (DOM) en almacen existente o específico
		- Posibilidad 1: Traduce el DOM a tables relacionales (elementos, atributos, entidades)
		- Posibilidad 2: Traduce el DOM a objetos en BBDDOO
		- Posibilidad 3: Usa almacen para esta finalidad

Características bases de datos nativas: Consultas, Creación de índices y Creación de identificadores únicos.
Los triggers son de bases de datos relacionales. 

### 2.1. Colecciones y documentos

La BD XML tiene estructura jerárquica organizada en colecciones y documentos XML. La estructura jerárquica comienza con un **nodo raíz (\/)** del que parten:

- **Colecciones**: Conjunto de documentos agrupado normalmente en función de la información que contienen. Puede contener otras colecciones. 
- **Documentos**: Información XML. Información de otro tipo (non-XML-data)

Al comparar con BBDD relacionales o sistema de archivos es fácil ver que las colecciones juegan el papel de tablas o directorios y los documentos el de filas o ficheros.

Depende de la implementación pero en general:
- Cada colección puede tener más de un `DOCTYPE` asociado
- El elemento raíz del documento XML define a qué `DOCTYPE` está asociado el documento. Si no posee ninguno, se crea dinámicamente pudiéndose así almacenar documentos sin formato definido
- La colección puede tener asociado un schema con información tanto física como lógica. La parte lógica define las relaciones y propiedades de los documentos XML y la física información sobre el almacenamiento e indexación de los mismos.
- Se pueden almacenar documentos no-XML con el `DOCTYPE` `non-XML`

### 2.2. Gestores nativos XML comerciales y libres

**Comerciales o de código propietario**
- **TaminoXML** server. Software AG. Uno de los primeros. Documentos separados an base de datos propia y no se transforman en otro modelo
- **TEXT TML** de Isiasoft. Permite almacenar en formato nativo. Y sin DTD. Incluye API para Java, WebDAV, OLE DB, .NET. Da índices según la estructura de documento. Permite uso de varios indices al mismo tiempo. 
- **Qizx.** Escrita en Java. Almacena datos usando representación basada en modelo de XPath. Permite almacenar sin DTD. La representación usa comprensión por lo que el documento y los índices suelen ocupar menos espacio que el original. Tiene XQuery, extensiones (XUpdate), API para Java.
- **Base X**

**Libre**
- **eXist** Sistema de almacenamiento propio (árboles B +, archivos paginados). Puede ejecutarse como servidor de bases de datos independiente, biblioteca de Java embebida o en el motor servlet de aplicación web.  Soporta XQuery, extensiones y API de Java. Permite almacenar sin DTD. 

---
  
Falso. Un XML Group Library no es equivalente a una base de datos XML (BD XML). Un XML Group Library es una biblioteca o conjunto de herramientas diseñadas para manejar y procesar documentos XML de manera eficiente. Puede proporcionar funcionalidades para analizar, manipular, validar y transformar documentos XML, pero no ofrece capacidades de almacenamiento persistente como una base de datos XML. Una base de datos XML, por otro lado, es un sistema de gestión de bases de datos diseñado específicamente para almacenar y recuperar datos en formato XML de manera eficiente.
## 3. Base de datos eXist

### 3.1. Instalación y arranque

Como se ha comentado eXist (no sé donde han dejado al pobre Base X que tanto lo querían en Lenguaje de marcas Tema 6):
- Es libre de código abierto
- Su motor está escrito en Java
- Soporta estándares de consulta XPath, XQuery, XSLT, indexación de documentos, soporte de actualización.

Debería tener al menos Java 8, 200 MB de espacio y al menos 512 MB para ejecuar. 

- Se descarga el .jar y se instala.
- Se arranca desde el acceso directo del escritorio.
- Se arranca el servidor en "start server"

Se plantean las opciones: 
- Opción **eXide**: (Open eXide): Se abrirá navegador directamente con la herramienta para crear y borrar colecciones, abrir nuevos documentos y realizar consultas
- Opción **dashboard**: Se presenta administrador de aplicaciones de la BD. n ella encontramos aplicaciones como **_eXist-bd documentation_**, que contiene la documentación, _**eXide-Xquery**_ el entorno para realizar consultas y _**eXist-bd Demo Apps**_ la aplicación de demostración. En cuanto a los plugins encontramos el gestor de colecciones _**Collections**_ , el gestor de Backups _**Backup,**_ el gestor de usuarios _**User Manager**_ y el gestor de paquetes _**Package Manager.**_ En conclusión la parte de aplicaciones es la que va a gestionar la base de datos a nivel de consultas y la parte de plugin es la que gestiona la parte administrativa.
- Seleccionar el **cliente Java**. Se abrirá una ventana. Se introduce nombre de usuario y contraseña de la instalación, conexión (Remote) y URL (debe aparecer puerto 8080 o, si está ocupado, cambiar a 8083). Grabar nombre de conexión y se le da a conectar. 

### 3.2. Gestión BD XML mediante eXist

En la carpeta `eXist\webapp\WEB-INF\data` están los archivos más importantes de la BBDD encontrándose:
- **collections**: Jerarquía de colecciones y su relación con los documentos. Cada uno tiene un identificador único que se rellena junto con su índice
- **dom.dbx**: Almacén de datos nativo. Se almacenan los nodos del documento de acuerdo al modelo DOM de W3C.

Más información sobre el modelo DOM: https://www.w3.org/2005/03/DOM3Core-es/introduccion.html

#### El cliente Java eXist

Se observa dentro de ese precioso cliente hecho con Java Swing lo siguiente:
- Crear colección: Crear colección
- Cargar documento: Carga un XML con el que se va a trabajar
- Comprobar contexto: Verificar que el documento se encuentra dentro del contexto sobre el que se va a trabajar.
- Consulta BD con XPath
- Visor de colecciones y documentos

## 4. Lenguaje XQuery

**XQuery** (como ya vimos en Lenguaje de Marcas Tema 6) es un lenguaje de consulta diseñado para extraer información de colecciones de datos expresadas en XML. Sus características:
- **Basado en XPath** y se fundamenta en él para realizar la selección de información y la iteración
- **Lenguaje declarativo**: En vez de ejecutar una lista de comandos como en un lenguaje procedimental clásico, cada consulta es una expresión que es evaluada y devuelve un resultado al igual que SQL.

**XQuery** es a **XML** lo mismo que **SQL** a las **bases de datos relacionales**

XQuery incluye conceptos en su modelo como jerarquia y orden de los datos que no están presentes en el relacional. El orden es importante aquí. 

**Principales expresiones de XQuery**
- Expresiones XPath: Para navegar por los documentos
- Expresiones FLWOR (For, Let, Where, Order, Return): Para iterar por los elementos de un conjunto de datos
Y más expresiones:
- Constructores para generar nodos y contenido dinámico
- Condicionales (IF, THEN, ELSE) para resultados en base a condiciones
- Cuantificadores SOME, ANY para checkear existencia de algún elemento que cumpla una condición
- Listas a las que aplicar operadores (UNION) y funciones ade agregación (AVG, COUNT...)

#### **Requerimientos técnicos que cumple XQuery:**
- Lenguaje declarativo
- Independiente del protocolo de acceso (archivo local, servidor BBDD, archivo XML)
- Consulta y resultados: Respetar modelo XML
- Consulta y resultados: Ofrecer soporte para namespaces
- Soportar XML-Schema y DTO
- Independiente de la estructura del documento
- Soportar tipos simples (enteros y cadenas) y complejos (nodo compuesto)
- Soportar cuantificadores universales (para todo) y existenciales (existe)
- Soportar operaciones sobre jerarquías de nodos y secuencias
- Combinar información de múltiples fuentes en una consulta
- Manipular datos independientemente del origen de estos
- Lenguaje independiente de la sintaxis (varias sintaxis distintas para expresar la misma consulta)

#### **Aplicaciones:**
- Recuperar información a partir de datos XML
- Transformar estructuras de datos XML en otras estructuras
- Ofrecer alternativa a XSLT para hacer transformaciones de datos en XML, HTML, PDF


## 4.1. XPath

Lenguaje, no basado en XML, que permite localizar o acceder a una parte de un documento XML

- Se basa en una relación de parentesco entre los nodos del documento:  representación del documento XML llamada árbol de nodos o modelo de datos XPath
- Inicialmente diseñado para ser usado con XSLT y XPointer. Hoy día es usado en XSLT, XML Schema, XQuery, Xlink, Xpointer, Xforms...
- Su notación es **similar a las rutas de los ficheros**, salvo que XPath está diseñado para selecciones múltiples.

El documento XML en primer lugar debe ser procesado por un analizador o parser XML que:
- verifica que el documento XML está bien formado
- lo valida contra el DTD / XSD correspondiente
- construye el árbol de nodos
### 4.1.1. Modelo de datos de XPath: El árbol de nodos

Un árbol es una estructura que representa una serie de elementos (nodos) unidos por líneas (vértices). Entre dos nodos cualesquiera solo ha y un único camino y ninguno de ellos forma un bucle. Tiene forma de copa de árbol invertida. 

Hay siete distintos tipos de nodos.

- **Nodo raíz**: Primer nodo del árbol. No tiene padre. No debe confundirse con el elemento raíz del documento XML. Tiene como hijos al ejemplar (elemento raíz del XML) y, en su caso, los comentarios e instrucciones que formen parte del prólogo XML. Se indentifica con "/".
- **Nodos elemento**: Hay uno por cada elemento XML. Tienen un solo padre que puede ser otro nodo elemento o el nodo raíz. Pueden tener un identiificador único, para lo cual debe estar declarado de tipo ID en su DTD o en el XML Schema asociado.
- **Nodos atributo***: Almacenan los atributos del documento XML. El nodo atributo está asociado a un único nodo elemento que es padre de este. Desde el punto de vista del nodo elemento no se considera a sus atributos como nodos hijos. Los nodos atributos son nodos hoja, no pueden tener nodos hijos. 
- **Nodos texto** (o contenido): Almacenan los valores alfanuméricos de los contenidos de los elementos XML. Son nodos hoja (sin hijos). Los valores de los atributos no se almacenan en un nodo texto.
- **Nodos de comentario**  y **Nodo de instrucciones de proceso.** Se generan para elementos con comentario e instrucciones de proceso. Son hijos del elemento en el que aparezcan o del nodo raíz si están situados fuera del elemento raíz. Por estos elementos el nodo raíz del modelo no coincide con el elemento raíz del documento ya que puede haber comentarios o instrucciones fuera del raíz.
- **Nodo espacio de nombres**: Cada nodo elemento puede tener un conjunto asociado de nodos espacios de nombres, uno para cada uno de los distintos prefijos de espacio de nombres incluyendo, si es el caso, el espacio de nombres por defecto. Tiene un funcionamiento parecido a los atributos. El nodo espacio de nombres tiene un único nodo elemento como padre. Desde el punto de vista del nodo elemento no son considerados como nodos hijos de este. Son nodos hoja. 

(Las etiquetas permiten estructuras la información del documento XML pero no son consideradas nodos)

----------


![](LENGUAJE_MARCAS/resources/ud05-1.png)

![](resources/ud05-3.png)

Observa que del nodo raíz (que no corresponde con el elemento raíz del XML) cuelga el ejemplar y el comentario.  También que los valores de los atributos no aparecen en nodos texto sino junto al identificador del atributo en el nodo atributo (identificador y valor).

### 4.1.1.1. Las relaciones entre nodos

En primer lugar definamos:

- **Nodo actual**: El que se menciona al evaluar una expresión XPath
- **Nodo contexto**: Cada expresión está formada por subexpresiones que se evalúan antes de resolver la siguiente. Los nodos obtenidos tras evaluar una expresión, usada para evaluar la siguiente son el nuevo contexto. -> Es el nodo en el que nos posicionamos para establecer una relación.
- **Tamaño del contexto**: Número de nodos que se evalúan en un momento dado en una expresión XPath. 

Hay trece relaciones entre nodos que serán usadas como ejes en los pasos de localización.

**EJES**:
- **self**: Nodo de contexto 
- **child**: Hijos del nodo de contexto
- **descendant**: Hijos del nodo de contexto y todos sus descendientes
- **descendant-or-self**: Nodo contexto y sus descendientes
- **parent**: Padre del nodo contexto, si lo hay
- **ancestor**: Ancentros del nodo de contexto: Padre, padre de su padre,... Incluye al nodo raíz salvo que el nodo contexto sea el nodo raíz.
- **ancestor-or-self**: Nodo de contexto y sus ancestros. Incluirá siempre al nodo raíz. 
- **preceding**: Nodos del mismo documento que el nodo contexto que están antes de este según el orden del documento excluyendo ancestros, nodos atributo y nodos de espacios de nombres
- **preceding-sibling**: Hermanos precedentes del nodo contexto; Si el nodo contexto es un nodo atributo o un nodo espacio de nombres este eje está vacío.
- **following**: Todos los nodos del mismo documento que el nodo contexto que están después de este según el orden del documento, excluyendo los descendientes y los nodos atributo y nodos de espacios de nombres
- **following-sibling**: Hermanos del nodo contexto. Si el nodo contexto es un nodo atributo o nodo espacio de nombres, este eje está vacío.

![](resources/ud05-4.png)


- **attribute**: Atributos del nodo contexto. Es vacía si el nodo contexto no es un nodo elemento (otros no pueden tener atributos)
- **namespaces**: Nodos espacio de nombres del nodo contexto. Relación será vacía si el nodo contexto no es nodo elemento (otros no pueden tener espacios de nombres)

### 4.1.2. Expresiones de la sintaxis de XPath y su resultado

Es parecida a la que se usa en los árboles de directorios y archivos de los sistemas operativos. 

Se tiene una versión completa:

```xpath
descendant-or-self::curso[position()=1]/child::grupo[position()=2]/child::alumno[last()]/child::nombre/child::node()
```

Y una **versión simplificada** (Que es la que habitualmente se usa):

```xpath
//curso[1]/grupo[2]/alumno[last()]/nombre/text()
```

En la expresión XPath se pueden usar llamadas a funciones, operaciones matemáticas y operaciones lógicas.

El camino de localización XPath se evalúa devolviendo un resultado que puede ser: 
- **Conjunto de nodos (node-set)**. Una lista de nodos. El orden en el que aparecen en la lista es el mismo en que aparecen en el documento. Se devuelve cuando los operadores usados seleccionan nodos del modelo. Se considera que todos los elementos del node-set son hermanos, independientemente de lo que fuesen originalmente. Los subárboles de un nodo no se consideran elementos del conjunto (hijos de los nodos del node-set, que son accesibles)  
	Los nodos pueden ser de 7 tipos: Elemento, Atributo, Texto, Espacio de nombres, Instrucción de procesamiento, Comentario, Raíz, Booleano, Número y Cadena.
- **boolean**: Valor verdadero o falso, devuelto con operadores lógicos o de comparación
- **number**: Un número en punto flotante. Se devuelve con operadores numéricos. 
- **string**: Cadena de caracteres. Cuando se seleccionan nodos de texto, comentarios o atributos. 

Existen como palabras reservadas:
- Los ejes: `ancestor`, `ancestor-or-self`, `descendent`, `descendent-or-self`, `following`, `following-sibling`, `namespace`, `parent`, `preceding`, `preceding-sibling`, `self`
- Los selectores de nodos: `node()`, `text()`, `comment()`, `procesing-instruction()`
- Operaciones lógicas: `and`, `or`, `not()`
- Operaciones matemáticas: `div`, `mod`

Los siguientes símbolos tienen una función definida:
- Agrupación de operaciones con paréntesis `()`
- Predicados con corchetes `[]`
- Abreviatura elemento actual `.`
- Abreviatura elemento padre `..`
- Abreviatura atributo `@`
- Todos los tipos de nodos `*`
- Separador eje-selector `::`
- Separador de pasos de localización `/`
- Abreviación del paso `descendant-or-self::node()` `//`
- Referencia a variable `$`
- Unión de conjuntos de nodos `|`
- Coma `,`
- Operaciones lógicas: `=', ' !=', '<', '>', '<=', '>='
- Operaciones matemáticas `+`, ' -', `*`

También se usan:
- Nombres cualificados de los identificadores del documento XML
- Nombres de las funciones
- Nombres de referencias a variables (anteponiendo $)
- Números y literales (Con comillas simples o dobles, posibilidad de anidar alternando comillas)


Ejemplo: Alumnos de 2 ESO A

`/child::colegio/child::curso[@nivel="2"]/child::grupo[@orden="A"]/child::alumno
`
`//colegio/curso[@nivel="2"]/grupo[@orden="A"]/alumno`

Ejemplo: Alumnas llamadas Ana

`descendant-or-self::alumno[nombre="Ana"]
`
`//alumno[nombre="Ana"]`

Ejemplo: Nombre del con la nota más alta

`descendant-or-self::alumno[child::nota_media=max(/descendant-or-self::nota_media)]/child::nombre
`
`descendant-or-self::alumno[nota_media=max(//nota_media)]/nombre`

### 4.1.3. Caminos de localización y pasos de localización 

![](resources/ud05-5.png)

- Los **caminos de localización** son la ruta que hay que seguir por el árbol de datos para localizar un nodo. No son lo más común en XPath, pero sí lo más importante. 
- Están compuestos por **pasos de localización** separados entre sí por `/`.
- Los pasos de localización se separan en **eje** y **selector de nodos**  por `::`. En algunos pasos de localización hay instrucciones entre corchetes `[]` después del selector de nodos que reciben el nombre de **predicados**

Los caminos de localización pueden ser:
- Absolutos: Comienzan en el nodo raíz. Fácilmente reconocible por empezar con la barra simple: `/child::colegio/child::curso/child::grupo/attribute::*`
- Relativo: Relativo al nodo contexto que esté posicionado en un determinado lugar: `child::grupo/atribute::*`

Es posible usar el operador de unir para unir el resultado de dos caminos de localización para que devuelvan conjuntos de nodos: `descendant-or-self::apellidos | descendant-or-self::nota_media`

Dentro de los **pasos de localización**:
- El eje: Especifica relación jerárquica entre los nodos seleccionados por el paso de localización y el nodo contextual
- Selector de nodos o prueba de nodos: Especifica el tipo de nodo de los nodos seleccionados por el paso de localización
- Predicados: Usan expresiones lógicas para refinar el conjunto de nodos seleccionados. 

#### Ejes
Respecto a los ejes, recordar que para seleccionar atributos o espacios de nombres deben usarse de forma explícita los ejes `::attribute` o `::namespace`, ya que no estarán contenidos en los otros ejes. 
#### Selectores de nodos
Cada eje tiene un tipo principal de nodos. Si un eje pùede contener elementos, el nodo principal son los elementos. Si no, son los que el eje contenga (attribute atributos; namespace espacios de nombres; el resto elementos).

Los selectores de nodos son
- Nombre cualificado (QName)
- Todos `*`
- `text()`
- `comment()`
- `processing-instruction()`
- `node()`
También se han añadido en versiones posteriores
- `element()`
- `attribute()`
- `document-node()`

`child::alumno` Selecciona los elementos alumno hijos del nodo contexto. Si no lo tiene, selecciona un conjunto de nodos  vacíos.
`attribute::nivel`. Selecciona el atributo nivel del nodo contexto. Si no lo tiene, selecciona un conjunto de nodos vacío.
`text()` Para cualquieer nodo de texto.  `child::text()`, nodos de texto hijos del nodo contexto
`comment()` Cierto para cualquier nodo comentario
`procesing-instruction()`, puede tener un argumento literal; verdadero para cualquier instrucción de procesamiento con nombre igual al literal
`node()` Cierto para cualquier nodo

Ejemplos:
`/descendant-or-self::alumno/child::nombre`  (Elementos `<nombre>`)
`/descendant-or-self::grupo/attribute::*`  (Atributos de `<grupo>`)
`/descendant-or-self::apellidos/text()` (Texto del elemento de apellidos)
`/descendant-or-self::colegio/child::comment()` (Comentarios del elemento colegio)
`/descendant-or-self::grupo/child::node()` (Todos los elementos contenidos en el `<grupo>`)

#### Sintaxis abreviada

`child::` puede ser omitida en los pasos   `child::colegio/child::curso`  equivale a `/colegio/curso`

`attribute::` puede abreviarse como `@`   `[attribute::orden="A"]` equivale a `@attribute=orden"A"`

`//` es abreviatura de `descendant-or-self::node()`  `/descendant-or-self::node()/child::alumno` equivale a `//alumno`.  Igualmente `child::curso/descendant-or-self::node()/child::alumno`equivale a `curso//alumno`

`descendant-or-self::node()/child::nota_media` se abrevia en  `//nota_media`
child::colegio/child::curso/attribute::etapa se abrevia en  `colegio/curso/@etapa`   (camino relativo)
`descendant-or-self::alumno/parent::node()/attribute::*` se abrevia en  `//alumno/../@*`
`self::node()/descendant::telefono` se abrevia en  `./descendant::telefono `  (camino relativo)
### 4.1.4. Predicados

Los predicados filtran un conjunto de nodos con respecto a un eje y a un selector de nodos para producir un nuevo conjunto de nodos. 
El paso del localización puede tener cero, uno o más predicados en cascada.
Un camino de localización `grupo[2]` es equivalente a `grupo[position()=2`] .

Ejemplos:
a) Primer alumno de 2 ESO A.
`//curso[@nivel="2"]/grupo[@orden="A"]/alumno[1]`
b) Apellidos de los alumnos con nota superior a 8.
`//alumno[nota_media>8]/apellidos` 
c) Nombre de los alumnos que no nacieron en el 2017 y tienen media superior a 7.
`//alumno[anno_nac!=2017][nota_media>7]/nombre`
`//alumno[anno_nac!=2017 and nota_media>7]/nombre`
d) Apellidos de los alumnos que nacieron en el 2019 y que están suspensos.
`//alumno[anno_nac=2019 or nota_media<5]/apellidos`

### 4.1.3. Funciones

#### Funciones de conjuntos de nodos
- `last()`: Último de los nodos del contexto seleccionado. 

```xpath
//alumno[position()=1]/nombre 
//alumno[1]/nombre
```

- `position()`: Posición del nodo actual dentro de los nodos del contexto seleccionado (inicializa en 1)

```xpath
//curso[@nivel="2"]//alumno[last()]/(nombre|apellidos)
```

- `count(node-set)`: Número de nodos del conjunto de nodos pasado como argumento

```xpath
count(//alumno[anno_nac=2018])
//curso[@nivel="2"]/grupo/count(alumno)
count(//curso[@nivel="1"]/grupo/alumno)
```

* `name(?node-set)`: Nombre cualificado del nodo del conjunto de nodos pasado como argumento. Si no se pasa argumento, toma el nodo contexto como argumento. Si no se declara espacio de nombres da el mismo resultado que `local-name()`
* `local-name(?node-set)`: Nombre local (sin URI) del espacio de nombres del nodo del conjunto de nodos pasado por argumento. Si no se pasa el argumento toma nodo contexto como argumento
* `namespace-uri(?node-set)`: Devuelve la URI del espacio de nombres, si nel nombre local de los nodos pasados como argumento. Si no se pasa, toma el nodo contexto como argumento.
* `id(object)`: Selecciona elementos mediante el identificador único. Los nodos deben estar declarados con ese ID en el DTD o XSD.
#### Funciones de cadenas de caracteres

- `string(object?)`: Convierte objeto en cadena de caracteres
- `concat(...)`: concatenación de argumentos
- `starts-with(string, with)`: si comienza por la segunda cadena
- `contains(string, contains)`: si contiene la segunda cadena
- `substring-before(string, string)`: subcadena de la primera cadena que precede a la aparición de la segunda
- `substring-after(string, string)`: subcadena de la primera cadena que sigue a la aparición de la segunda
- `substring(string, number, ?number)`: substring comienza en posición especificada en el segundo y tiene longitud especificada en el tercero
- `string-length(string?)`: Longitud
- `normalize-space(string?)`: normalización de espacios en blanco
- `translate(string, string, string)`: el primer argumento se traducen las apariciones del segundo con lo indicado en el tercero

Ejemplos:
a) Alumnos que su nombre comiencen por 'Al'
`//alumno[starts-with(nombre,"Al")]`
b) Nombre y apellidos de los alumnos que se apelliden 'Carmona' tanto de primero como de segundo apellido.
`//alumno[contains(apellidos,"Carmona")]/(nombre|apellidos)/text()`
c) Del texto "En un lugar de la Mancha" extrae todo lo que hay delante de 'de'.
`substring-before("En un lugar de la Mancha","de")`
d) Del texto "En un lugar de la Mancha" extrae todo lo que hay detrás de 'de'.
`substring-after("En un lugar de la Mancha","de")`
e) Del texto "En un lugar de la Mancha" extrae todo lo que hay detrás de 'de'.
`substring-after("En un lugar de la Mancha","de")`
f) Del texto "En un lugar de la Mancha" extrae todo lo que hay a partir del carácter número 9.
`substring("En un lugar de la Mancha",9)`
g) Del texto "En un lugar de la Mancha" calcula el número de caracteres que tienes. 
`string-length("En un lugar de la Mancha")`
h) Normaliza un texto, quitando los espacios iniciales y finales y poniendo un único espacio entre palabras.
`normalize-space(" Esto    es      una   prueba      ")`
g) Sustituir los caracteres en el primer texto que aparecen en el segundo texto por los del tercero.
`translate("abcdefghi","bdg","BDG")`

#### Funciones lógicas y numéricas

- `boolean(object)`: Argumento convertidfo a booleano
- `not(boolean)`
- `true()`
- `false()`
- `lang(string)` Verdadero o falso si el lenguaje del nodo especificado en `xml:lang` es igual que o sublenguaje del especificado como argumento
- `number(object?)`: Pasa a número
- `sum(node-set)`: Suma de los nodos del conjunto de nodos
- `floor()`: Redondeo hacia abajo
- `ceiling()`: Redondeo hacia arriba
- `round()`: Número más proximo al argumento y que sea entero

### 4.1.3. Estrategias de uso

- Buscar en el XML la posición del atributo y del elemento que se pregunten
- Ver cuál debe ser el resultado que queremos obtener y partir de ahí.
- Posicionar predicado:
	- Ponerlo en el primer elemento padre común
	- Mezclar ambos caminos de localización
- Simplificar

Al trabajar con información en distintos niveles es importante no usar doble barra en mitad de los caminos de localización ya que la búsqueda la reiniciará desde el elemento raíz y no con el elemento ya establecido. 

A veces habrá que hacer consultas anidadas.

A veces no querremos repetidos (esto se puede hacer con ayuda del eje `preceding`
`//alumno[not(nombre=preceding::nombre)]/nombre`

-------------------

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE universidad>
<universidad>
    <nombre>Universidad de Victoria</nombre>
    <pais>España</pais>
    <carreras>
        <carrera id="c01">
            <nombre>I.T. Informática</nombre>
            <plan>2003</plan>
            <creditos>250</creditos>
            <centro>Escuela de Informática</centro>
        </carrera>
        <carrera id="c02">
            <nombre>Dipl. Empresariales</nombre>
            <plan>2001</plan>
            <creditos>275</creditos>
            <centro>Facultad de Ciencias Sociales</centro>
        </carrera>
        <carrera id="c03">
            <nombre>Dipl. Relaciones Laborales</nombre>
            <plan>2001</plan>
            <creditos>280</creditos>
            <centro>Facultad de Ciencias Sociales</centro>
        </carrera>
        <carrera id="c05">
            <nombre>Lic. Biologia</nombre>
            <plan>2001</plan>
            <creditos>175</creditos>
            <centro>Facultad de Ciencias Experimentales</centro>
            <subdirector>Alonso Pérez</subdirector>
        </carrera>
        <carrera id="c06">
            <nombre>Lic. Humanidades</nombre>
            <plan>1980</plan>
            <creditos>475</creditos>
            <centro>Facultad de Humanidades</centro>
            <subdirector>Jesús Martínez</subdirector>
        </carrera>
    </carreras>
    <asignaturas>
        <asignatura id="a01" titulacion="c01">
            <nombre>Ofimática</nombre>
            <creditos_teoricos>3</creditos_teoricos>
            <creditos_practicos>1.5</creditos_practicos>
            <trimestre>l</trimestre>
        </asignatura>
        <asignatura id="a02" titulacion="c01">
            <nombre>Ingeniería del Software</nombre>
            <creditos_teoricos>6</creditos_teoricos>
            <creditos_practicos>1.5</creditos_practicos>
            <trimestre>2</trimestre>
        </asignatura>
        <asignatura id="a03" titulacion="c02">
            <nombre>Me la invento</nombre>
            <creditos_teoricos>6</creditos_teoricos>
            <creditos_practicos>1.5</creditos_practicos>
            <trimestre>2</trimestre>
        </asignatura>
    </asignaturas>
    <alumnos>
        <alumno id="e01">
            <apellido1>Rivas</apellido1>
            <apellido2>Santos</apellido2>
            <nombre>Víctor Manuel</nombre>
            <sexo>Hombre</sexo>
            <estudios>
                <carrera codigo="c01" />
                <asignaturas>
                    <asignatura codigo="a01" />
                    <asignatura codigo="a03" />
                    <asignatura codigo="a05" />
                </asignaturas>
            </estudios>
        </alumno>
        <alumno id="e02" beca="si">
            <apellido1>Pérez</apellido1>
            <apellido2>García</apellido2>
            <nombre>Luisa</nombre>
            <sexo>Mujer</sexo>
            <estudios>
                <carrera codigo="c02" />
                <asignaturas>
                    <asignatura codigo="a02" />
                    <asignatura codigo="a01" />
                </asignaturas>
                <proyecto>Web de IBM.com</proyecto>
            </estudios>
        </alumno>
    </alumnos>
</universidad>
```

**1 - Nombre de la Universidad:**
`/universidad`

**2 - País de la Universidad:**
`/universidad/pais`

**3 - Nombres de las Carreras:**
`/universidad/carreras/carrera/nombre`
`universidad/carreras/carrera/nombre`
`/universidad/carreras/carrera/nombre/text()`

**4 - Años de plan de estudio de las carreras:**
`/universidad/carreras/carrera/plan`

`/universidad//carrera/plan`  (Dentro de Universidad hay un elemento carrera, puede haber intermedios, no tiene por qué ser hijos directos)

`/universidad//*/carrera/plan` 

**5 - Nombres de todos los alumnos:**

`//alumnos/alumno/nombre`  (Cualquier estructura pero que después encuentre eso)

**6 - Identificadores de todas las carreras:**

`//carreras/carrera/@id`

**7 - Datos de la carrera cuyo id es c01:**
Hagamos un predicado (filtro):

`//carreras/carrera[@id='c01']`

Nombre de la carrera cuyo id es c01: `//carreras/carrera[@id='c01']/nombre`

Contenido del elemento carrera (llaves): `//carreras/carrera[@id='c01']/*`

**8 - Centro en que se estudia de la carrera cuyo id es c02:**

`/universidad/carreras/carrera[@id='c02']/centro`
`//carreras/carrera[@id='c02']/centro`
`//carreras/carrera/centro[../@id='c02']`

----
(Ojo, filtro en carrera y no en carreras. Porque si filtro en carreras, no va a encontrar un hijo id )

`//carreras[carrera/@id='c02']/carrera/centro`  Aquí estoy preguntando ¿existe alguna carrera con identificador c02, sí; pues pinto todas. 

**9 - Nombre de las carreras que tengan subdirector:**
`//carreras/carrera[subdirector]/nombre/text()
`
**10 - Nombre de los alumnos que están haciendo proyecto:**
`//alumnos/alumno[estudios/proyecto]/nombre/text()`

`//alumnos/alumno[./estudios/proyecto]/nombre` 
 `//alumnos/alumno[.//proyecto]/nombre` (Partiendo del directorio actual, que busque descendientes)
----
MAL Ruta absoluta: (Ojo, aqui uso ruta absoluta y le estoy preguntando que exista algún proyecto en TODO EL ARBOL. Cuidado con las rutas absolutas)
`//alumnos/alumno[//proyecto]/nombre`

**11 - Nombre de las carreras en las que hay algún alumno matriculado:**
`//carreras/carrera[@id=//alumnos/alumno//carrera/@codigo]/nombre/text()`
`//carreras/carrera[@id=//alumnos/alumno/estudios/carrera/@codigo]/nombre/text()`

**12 - Apellido y nombre de alumnos con beca:**

```
//alumnos/alumno[./@beca="si"]/nombre | 
//alumnos/alumno[./@beca="si"]/apellido1 |
//alumnos/alumno[./@beca="si"]/apellido2
```

**13 - Nombre de las asignaturas de la titulación c04:**

`//asignaturas/asignatura[./@titulacion="c01"]/nombre/text()`

**14 - Nombre de las asignaturas de segundo trimestre**

`//asignaturas/asignatura[./trimestre="2"]/nombre/text()`
`//asignaturas/asignatura[trimestre="2"]/nombre/text()`

**15 - Nombre de las asignaturas que no tienen 6 créditos teóricos:**

`//asignaturas/asignatura[creditos_teoricos!="6"]/nombre/text()`
`//asignaturas/asignatura[not(creditos_teoricos="6")]/nombre/text()`
`//asignaturas/asignatura[not(creditos_teoricos=6)]/nombre/text()`

**16 - Código de la carrera que estudia el último alumno:**
(Inicializa en "1")
`//alumnos/alumno[last()]//carrera/@codigo`

(El penúltimo) `//alumnos/alumno[last()-1]//carrera/@codigo`

(Las que no son 1) `//alumnos/alumno[position()!=1]//carrera/@codigo`

**17 - Código de las asignaturas que estudian mujeres:** 

`//alumnos/alumno[sexo="Mujer"]/estudios/asignaturas/asignatura/@codigo` (Se repetirian)

Mejor, sin repetir códigos
`//asignaturas/asignaturas[@id=//alumnos/alumno[sexo="Mujer"]//asignatura/@codigo]/@id`



### Modelo de datos

En Xquery el orden en el que se encuentren los datos es importante. No es igual buscar etiqueta `<B>`  dentro de `<A>`  o todas las etiquetas `<B>`  del documento. 

La entrada y salida de consulta XQuery se definen según un modelo de datos que proporciona representación abstracta de uno o más documentos XML y que se basa en:
- Definición de secuencia como **colección ordenada de 0 o más items.** Además es **heterogénea**. Pero una **secuencia nunca puede ser el item de otra secuencia.**
- **Orden del documento**. Orden en el que los nodos aparecerían si se representase la jerarquía en formato XML. (Si el primer carácter de un nodo precede al primer carácter de otro nodo, también lo precederá en el orden)
- Contempla **valor especial llamado "error value"** al evaluar expresión que contiene un error.

### 4.2. Consultas XQuery

Una consulta en XQuery es una expresión que lee una secuencia de datos en XML y devuelve otra secuencia de datos XML. donde:

- Una secuencia es un conjunto ordenado de 0 o más items
- Un item es cualquier tipo de nodo del árbol XMl o un valor autómico.

Las funciones que se pueden invocar para **referirnos a colecciones y documentos dentro de la BD** son las siguientes:

- collection(/ruta): indicamos el camino para referirnos a una colección.
- doc(/ruta/documento.xml): indicamos el camino de un documento dentro de una colección.
------------

- El valor de la expresión es secuencia heterogénea de nodos y valores atómicos.
- Formada por expresiones y palabras simples unidas mediante palabras reservadas.
- **Xpath es lenguaje declarativo** para localizar nodos y fragmentos. XQuery está sobre la base de Xpath. **Toda expresión XPath también es consulta Xquery válida.**
- **Comentarios entre `(:  :)`**
- ***Caracteres  `{ }`** delimitan expresiones evaluadas para crear documento nuevo
- Admite expresiones condicionales del tipo **if-then-else**

En cualquier lugar del documento:

```xquery
	&b in doc("libro.xml")//libro
```

- Las consultas XQuery pueden estar formadas por hasta cinco tipos de claúsulas diferentes porque sigue **norma FLWOR**, que equivalen a For, Where, Group by, Having, Order By y Limit. 
- Si se incluyen varias consultas en el archivo `.xquery` para ejecución conjunta irán separadas por coma. 


Se trata de una **expresión que permite la unión de variables sobre conjuntos de nodos y la iteración sobre el resultado**. Las diferentes **cláusulas de una expresión FLWOR** son:

- En la sentencia FLWOR debe haber un FOR o un LET (el resto, si existen, deben seguir ese orden de palabra FLWOR)

- **For**. Permite seleccionar los nodos que se quieren consultar, guardándose su valor en una variable (identificador que comienza por $). Al conjunto de valores de la variable se le llama **tupla**.
- **Let**. (opcional). Asocia valores a variables.
- **Where** (opcional). Permite filtrar los resultados según una condición.
- **Order** (opcional). Permite ordenar la secuencia de valores o resultados.
- **Return**. Genera los valores de salida o devueltos.


```sql
for  in

let

where 

order by

return
```


- **For:** se usa para seleccionar nodos y almacenarlos en una variable, es algo parecido a la clausula **from** de SQL. A continuación hay que especificar una variable XPath que es la que se va a encargar de seleccionar los nodos. Hay que tener en cuenta que si se especifica más de una variable en el for lo que se va a realizar es el producto cartesiano de ambas. Para especificar variables estas deben ir precedidas del símbolo **$**.
- **let:** sirve para asignar valores resultantes de las expresiones XPath a variables. Es posible poner varias líneas let separadas por comas por cada variable.
- **Where**: aquí se especifican las condiciones que se quiera que cumplan los valores seleccionados.
- **Order by:** ordena los datos según el criterio que especifiquemos.
- **Return:** se utiliza para devolver el resultado. Aquí podemos especificar etiquetas XML encerrándolas entre llaves **{}.** Otra opción que presenta el return es la posibilidad de utilizar clausulas condicionales **if- then- else,**  hay que tener en cuenta que si utilizamos esta clausula es obligatorio poner siempre el **else.** Esto es debido a la naturaleza de las consultas XQuery en las que es obligatorio devolver siempre un valor. En el caso de que la consulta no devolviese ningún valor por no cumplir con las condiciones entonces devolvemos una secuencia vacía con **else()**.

Ninguna clausula FLWOR es obligatoria en la consulta XQuery. Por eso cualquier expresión XPath es XQuery válida. 

La consulta XQuery tiene:
- **Prólogo**: Lugar donde se declaran namespaces, funciones, variables...
- **Expresión**: Consulta propiamente dicha
### Funciones

##### Numéricas
- `floor()`: inferior más próximo
- `ceiling()`: superior más próximo
- `round()`: valor dado al más próximo
- `min()` `max()`: mínimo y máximo de los nodos dados
- `avg()`:valor medio
- `sum()`: suma
- `count_()`

##### Cadenas de texto
- `concat()`: unión de dos cadenas
- `string-length()`: longitud
- `startswith()`, `ends-with()`: si comienza o termina
- `upper-case()`, `lower-case()`: transforma en mayúsculas o minúsculas

##### Uso general
- `empty()`: true si no contiene elemento
- `exits()`: true si contiene elemento
- `distinct-values()`: extrae valores de secuencia de nodos y crea secuencia con valores únicos

##### Existenciales
- `some`, `every`: devuelven algún o todos los elementos...
Puede construir sus propias funciones también

```xml
declare nombre_funcion($param1 as tipo_dato1, $param2 as tipo_dato2,… $paramN as tipo_datoN)  
as tipo_dato_devuelto  
{  
...CÓDIGO DE LA FUNCIÓN...  
}
```

### Operadores
**De valores**:  eq (igual), ne (no igual), lt (menor que), le (menor o igual que), gt (mayor que), ge (mayor o igual que)

**Comparación generales**: =  != > >= < <=

**Comparación de nodos**: `is` si están ligadas al mismo nodo;  `is not` si no están ligadas al mismo nodo

**De órdenes de los nodos**: << (true si el nodo ligado al primer operando ocurre primero que el nodo ligado al segundo)

**Secuencias de nodos**: Union (suma de los dos), Intersect (en los dos), Except (primer operando y no en el segundo)

**Aritméticos**: + - \* div  y mod

(Pregunta prueba: Pertenecen a SQL y a XQuery  is, union, >=)


----------
#### Ejemplo 1 

Para el XML alumnos.xml:

```xml
<alumnos>
  <alumno dni=“93940”>
    <nombre>Jose</nombre>
    <apells>Bernardo</apells>
    <nota>7</nota>
  </alumno>
  <alumno dni=“93940”>
    <nombre>Juan</nombre>
    <apells>López</apells>
    <nota>4</nota>
  </alumno>
</alumnos>
```

Veamos un ejemplito:

```xquery
for 
  $a in doc("alumnos.xml")//alumnos
where 
  $a/nota > 5
return
  <aprobado>{$a/@dni,$a/nota}</aprobado>
```

Que nos devuelve:

```xml
<aprobado dni="93940">
	<nota>7</nota>
</aprobado>
```

#### Ejemplo 2

Para XML libro.xml:
```xml
<bib>
    <libro año="1994">
        <titulo>TCP/IP Illustrated</titulo>
        <autor>
           <apellido>Stevens</apellido>
           <nombre>W.</nombre>
       </autor>
       <editorial>Addison-Wesley</editorial>
       <precio> 65.95</precio>
    </libro>
    <libro año="1992">
       <titulo>Advan Programming for Unix environment</titulo>
       <autor>
          <apellido>Stevens</apellido>
          <nombre>W.</nombre>
      </autor>
       <editorial>Addison-Wesley</editorial>
       <precio>65.95</precio>
    </libro>
</bib>
```

Veamos un ejemplito:

```xquery
for
	&b in doc("libro.xml")//bib/libro
let
	&c := &b//autor
where 
	count(&c) > 2
order by
	&b/titulo
return
	&b/titulo
```

Busca nodos `<libro>` hijos de `<lib>` con más de dos autores, los ordena por el título y devuelve su título. 

Retorna:
```xml
<title>Data on the Web</title>
```
#### Ejemplos varios


```xml
for 
  $b in doc("libros.xml")//libro
where 
  $b/@año = "2000"
return 
  $b/titulo
```

Gráficamente:
![](LENGUAJE_MARCAS/resources/ud06-1.png)

```xml
(:1. Ejemplo de uso de la cláusula FOR. Obtener todos los títulos de los libros del fichero libros.xml.:)
    
    for $d in doc("libros.xml")/biblioteca/libros/libro/titulo
        return <titulos>{ $d }</titulos>
    
(:2. Ejemplo de uso de la cláusula LET. Obtener todos los títulos de los libros del fichero libros.xml.:)
    
    let $d := doc("libros.xml")/biblioteca/libros/libro/titulo
        return <titulos>{ $d }</titulos>
    
(:3. Ejemplo de uso de la cláusula FOR y LET juntas. Obtener todos los títulos de los libros del fichero libros.xml junto con los autores de cada libro.:)
    
    for $b in doc("libros.xml")//libro
        let $c := $b/autor
        return <libro>{ $b/titulo, <autores>{ $c }</autores>}</libro>
    
(:Otra solución posible a este ejercicio, en este caso utilizando únicamente la cláusula FOR:)
    
    for $b in doc("libros.xml")//libro
        return <libro>{ $b/titulo, <autores>{$b/autor}</autores>}</libro>
    
(:4. Ejemplo de uso de las cláusulas WHERE y ORDER BY en una consulta con dos ficheros. Obtiene los títulos de los libros prestados con sus autores y la fecha de inicio y devolución del préstamo, ordenados por la fecha de inicio del préstamo.:)
    
    for $t in doc("libros.xml")//libro,
    $e in doc("prestamos.xml")//entrada
        where $t/titulo = $e/titulo
        order by $e/prestamo/inicio
        return <prestamo>{ $t/titulo, $t/autor/*, $e/prestamo/inicio, $e/prestamo/devolucion }</prestamo>
```


```xml
(://escrutinio_sitio[convocatoria='2015']/nombre_sitio:)

(:<ul>{
for $a in /escrutinio_sitio
where $a/convocatoria='2019' and $a/votos/contabilizados/porcentaje >= '69'
order by $a/nombre_sitio
return <li>{$a/nombre_sitio/data()}</li>
}</ul>:)

(:let $contenido := (for $a in /escrutinio_sitio
where $a/convocatoria='2019' and $a/votos/contabilizados/porcentaje >= '70'
order by $a/nombre_sitio
return <li>{$a/nombre_sitio/data()}</li>)
return <ul>{$contenido}</ul>:)

(:let $p2019 := distinct-values(for $p in /escrutinio_sitio
where $p/convocatoria=2019
return $p/resultados/partido/nombre)

for $p2015 in distinct-values(for $p in /escrutinio_sitio
where $p/convocatoria=2015
return $p/resultados/partido/nombre)
where not($p2015 = $p2019)

return <partido>{$p2015}</partido>:)
(:For itera cada uno de ellos.
Let almacena conjunto de valores. A la hora de comparar, cuidado porque compara con el conjunto. A la hora de verificar no compara con el resto:)
(:<resultados>
{for $a in ('VOX','PODEMOS-IU')
let $total := sum(/escrutinio_sitio[convocatoria=2019]/
resultados/partido[nombre=$a]/electos)
return <electos partido="{$a}">{$total}</electos>}
</resultados>:)
for $provincia in /escrutinio_sitio[convocatoria=2019]
let $maximo := max($provincia//partido/votos_numero) 
let $partido := $provincia//partido[votos_numero=$maximo]/nombre
order by $provincia/nombre_sitio
return <resultado><provincia>{$provincia/nombre_sitio/data()}</provincia>
<partido>{$partido}</partido>
</resultado>
```

### 4.3. Actualización en eXist: XQuery Update Facility

Pequeña extensión que provee XQuery para insertar, eliminar y modificar nodos y elementos en documentos XML.

### Update

Todas las sentencias de actualización comienzan con la palabra **UPDATE** y a continuación:

- INSERT: para insertar nodos, seguido de:
    - **INTO**: si queremos añadir el contenido al último hijo especificado.
    - **FOLLOWING**: si queremos añadir el contenido inmediatamente después de los nodos especificados.
    - **PRECEDING**: si queremos añadir el contenido inmediatamente antes de los nodos especificados.

```

update insert CONTENIDO into EXPRESIÓN XPATH

update insert CONTENIDO following EXPRESIÓN XPATH

update insert CONTENIDO preceding EXPRESIÓN XPATH

```

```xquery
update insert
<aula id="2">
	<nombre>Aula auxiliar</nombre>
	<edificio>Aulario Severo Ochoa</edificio>
	<puestos>100</puestos>
</aula>
into /aula[@id="1"]
```


### Replace
Sustituye bien un nodo especificado con el valor nuevo que le especifiquemos. Hay que tener en cuenta que nodo debe devolver un único elemento.

```
update replace NODO with VALOR_NUEVO,

siendo NODO el nodo a remplazar que debe devolver un único valor y VALOR_NUEVO el nuevo contenido al que queremos actualizar.
```

```xquery
update replace
/aula[@id=1]/nombre with <nombre>Aula primera</nombre>
```

### Delete

elimina los nodos que le indiquemos en la expresión

```
**update delete expr xpath**
```

```xquery
update delete
/profesor [@id=2]/email
```

----

**insert**
Several modifiers are available to specify the exact insert location: insert into **as first**/**as last**, insert **before**/**after** and insert **into**.
`insert node (attribute { 'a' } { 5 }, 'text', <e/>) into /n`
**delete**
`delete node //n`
**replace**
`replace node /n with <a/>`
`replace value of node /n with 'newValue'`
**rename**
```
for $n in //originalNode
return rename node $n as 'renamedNode
```
![[BASES_DE_DATOS/resources/ud06-1.png]]

----

## 5. Trabajar con colecciones y documentos desde Java

Librerías para acceder desde Java a Sistemas XML Nativos.

**XML:DB** Librería de Java de acceso a sistemas XML más conocida. La más compatible con SGBD. Su objetivo principal es definir método común de acceso a sistemas nativos que permite realizar consultas, creación y modificaciones. Puede considerarse equivalencia de OJDBC y JDBC.

Su estructura:
- Driver: Lógica de acceso a una BD XML. Son proporcionados por proveedor. Cada sistema debe implementar el suyo.
- Collection: Contenedor de recursos y otras subcolecciones
- Resource: Recurso en sí. Se definen dos:
	- `XMLResource`: Documento XML o fragmento de documento seleccionado por una consulta XPath ejecutada previamente
	- `BinaryResource`: Secuencia binaria. Mapa de bits
	- Los recursos usados posteriormente se deben cerrar
- Service: Servicios que se solicitan para tareas especiales como ejecutar una colección XPath o administrar una colección.

eXist puede instalarse en NetBeans, por cierto.

O en Maven...

```xml
<dependencies>
    <dependency>
        <groupId>org.exist-db</groupId>
        <artifactId>exist-core</artifactId>
        <version>5.3.0</version>
    </dependency>
    <dependency>
        <groupId>org.exist-db</groupId>
        <artifactId>exist-xmldb</artifactId>
        <version>5.3.0</version>
    </dependency>
</dependencies>

```
### 5.1. Creación de BD XML. Establecer conexiones

Pasos necesarios para establecer conexión con XML:DB
- Registrar driver del proveedor del producto
- Cargar driver en memoria
- Crear instancia de la base de datos
- Registrar la instancia
- Acceder a la colección que se quiera especificando la URI ruta de acceso la servicio y ruta de la colección, usuario y contraseña. 

```java
public class ExistDBExample {
    public static void main(String[] args) {

        String driver = "org.exist.xmldb.DatabaseImpl";

        String uri = "xmldb:exist://localhost:8080/exist/xmlrpc";
        String collectionPath = "/db/mycollection";
        String username = "admin";
        String password = "password";


            // Initialize the database driver
            Class<?> cl = Class.forName(driver);
            Database database = (Database) cl.newInstance();
            database.setProperty("create-database", "true");
            DatabaseManager.registerDatabase(database);

            // Get the collection
            Collection col = DatabaseManager.getCollection(uri + collectionPath, username, password);

            if (col == null) {
                System.out.println("The collection could not be found.");
                return;
            }

            // Create a new resource
            XMLResource document = (XMLResource) col.createResource("mydocument.xml", "XMLResource");
            String xmlContent = "<root><element>Sample Content</element></root>";
            document.setContent(xmlContent);
            col.storeResource(document);

            // Retrieve the resource
            Resource res = col.getResource("mydocument.xml");
            System.out.println("Retrieved document: " + res.getContent());

            // Close the collection
            col.close();

        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```

### 5.2. Operaciones sobre colecciones

Crear y eliminar colecciones y documentos. Con `CollectionManagementService`

Una nueva colección se crea con el método `createCollection` 

```java
CollectionManagementService colserv = (CollectionManagementService)
col.getService("CollectionManagementService","1.0");
colserv.createCollection("NEW_COLLECTION");
```

Y se borra con `removeCollection`

```java
CollectionManagementService colserv = (CollectionManagementService)                col.getService("CollectionManagementService","1.0");
 colserv.removeCollection("NEW_COLLECTION");
```


### 5.3. Operaciones sobre documentos

Pueden crearse y borrarse documentos también con el `CollectionManagementService`

Creación con `createResource`

```java
import java.io.File;
File fichero= new File("NUEVO_DOC.xml");//Crea el nuevo documento.
if (!fichero.canRead())
  System.out.println("Error al leer el fichero");
else{
 Resource nuevoRecurso=col.createResource(fichero.getName(), "XMLResource");//Creamos el recurso
nuevoRecurso.setContent(fichero);//Asigno el fichero al recurso.
col.storeResource(nuevoRecurso);//Lo asigno a la coleccion
}
```

Borrado con `removeResource`

```java
try {
	Resource borrarRecurso=col.getResource("NUEVOS_CURSOS.xml");
	  col.removeResource(borrarRecurso);
} catch(NullPointerException e){
   System.out.println("No se puede borrar,no se encuentra");
}
```

### 5.4. Consultar documentos

**Pasos para procesar la consulta** 

Consulta que se encuentra en un fichero consulta.xq y almacenada en la carpeta del proyecto. El método va a recibir el nombre del fichero a ejecutar.

- Se lee el fichero
- Se recorre hasta el final y se almacena en una cadena
- Se ejecuta la consulta.

```java
import org.xmldb.api.DatabaseManager;
import org.xmldb.api.base.Collection;
import org.xmldb.api.base.Database;
import org.xmldb.api.base.ResourceSet;
import org.xmldb.api.base.ResourceIterator;
import org.xmldb.api.modules.XPathQueryService;

import java.io.BufferedReader;
import java.io.FileReader;
import java.io.IOException;

public class ExistDBQueryExecutor {

    public static void main(String[] args) {
        String driver = "org.exist.xmldb.DatabaseImpl";
        String uri = "xmldb:exist://localhost:8080/exist/xmlrpc";
        String collectionPath = "/db/mycollection";
        String username = "admin";
        String password = "password";

        if (args.length != 1) {
            System.out.println("Usage: java ExistDBQueryExecutor <query-file>");
            return;
        }

        String queryFile = args[0];

        try {
            // Read the XQuery file
            String xquery = readFile(queryFile);

            // Initialize the database driver
            Class<?> cl = Class.forName(driver);
            Database database = (Database) cl.getDeclaredConstructor().newInstance();
            database.setProperty("create-database", "true");
            DatabaseManager.registerDatabase(database);

            // Get the collection
            Collection col = DatabaseManager.getCollection(uri + collectionPath, username, password);

            if (col == null) {
                System.out.println("The collection could not be found.");
                return;
            }

            // Execute the XQuery
            XPathQueryService queryService = (XPathQueryService) col.getService("XPathQueryService", "1.0");
            ResourceSet result = queryService.query(xquery);

            // Process the results
            ResourceIterator i = result.getIterator();
            while (i.hasMoreResources()) {
                System.out.println(i.nextResource().getContent());
            }

            // Close the collection
            col.close();

        } catch (Exception e) {
            e.printStackTrace();
        }
    }

    private static String readFile(String fileName) throws IOException {
        StringBuilder content = new StringBuilder();
        try (BufferedReader br = new BufferedReader(new FileReader(fileName))) {
            String line;
            while ((line = br.readLine()) != null) {
                content.append(line).append("\n");
            }
        }
        return content.toString();
    }
}
```


Internamente, eXist no distingue entre expresiones XPath y XQuery. XQueryService por lo tanto, se asigna a la misma clase de implementación que XPathQueryService. Sin embargo, proporciona algunos métodos adicionales. Lo más importante, cuando se habla con una base de datos incrustada, es que  XQueryService permite que la expresión XQuery se compile en una representación interna, que luego se puede reutilizar.

## 6. Tratamiento de excepciones

`XMLDBException` es la excepción que se ejecuta cuando se produce excepción en la API XML:DB. Contiene dos códigos de erorres:
- Código de errores XML de API
- Código de errores definido por el proveedor.
La información puede capturarse con el método `getMessage()` que devolverá la cadena de error. 

### 6.1. Excepciones en el procesamiento de consultas

Cuando se procesa una consulta XQuery o una consulta de actualización XQuery, pueden ocurrir errores en el proceso de compilación y evaluación de la expresión de consulta, que suponen el lanzamiento de excepciones.

`CompileException` `EvaluateException`

```java
    private static void handleXMLDBException(XMLDBException e) {
        System.err.println("An XMLDBException occurred:");
        System.err.println("Error Code (XMLDB API): " + e.errorCode);
        System.err.println("Error Message: " + e.getMessage());

        // Additional checks for specific exceptions
        Throwable cause = e.getCause();
        if (cause instanceof org.exist.xmldb.CompileException) {
            System.err.println("CompileException: " + cause.getMessage());
        } else if (cause instanceof org.exist.xmldb.EvaluateException) {
            System.err.println("EvaluateException: " + cause.getMessage());
        } else {
            System.err.println("Cause: " + (cause != null ? cause.getMessage() : "Unknown"));
        }

        e.printStackTrace();
    }
```