
Con frecuencia es necesario transformar la información de un documento XML en otro.

Para transformar los documentos entran en juego:
- **XSLT** (eXtensible Stylesheet Language Transformations): Definir modo de transformar un XML en otro
- **XSL-FO** (eXtensible Stylesheet Language Transformations - Formatting Objects): Transformar XML en formato legible e imprimible por una persona, como un PDF
- **Xpath**(Ruta X): Acceso a componentes de documento XML

La parte de transformaciones ganó en importancia y se llega a la terminología actual que comprende a las anteriores:  **XSL** (eXtensible Stylesheet Language).

	En 1997 se propone a W3C un lenguaje basado en XML que especificase el formato de documentos XML (como CSS a HTML), separando contenido de presentación. Se empieza a desarrollar XSL (con formato y contenido junto en el mismo documento). Para mantener la independencia se tomó como criterio que el documento con formato se generaría a partir del documento con los contenidos (se desarrolla XSLT; obteniendo por el camino XPath para localizar partes de un XML; observando el potencial de XSLT para transformar en cualquier otro contenido XML, lazando XSL-FO. XSLT y Xpath se siguen usando y se siguieron lanzando especificaciones desgajadas de XLS, que, a su vez, se renombró a XSL-FO. Este no ha tenido mucho éxito ya que es complejo y hay otros estándares CSS que hacen lo mismo.)

## 1. XPath

Lenguaje, no basado en XML, que permite localizar o acceder a una parte de un documento XML

- Se basa en una relación de parentesco entre los nodos del documento:  representación del documento XML llamada árbol de nodos o modelo de datos XPath
- Usado en XSLT, XML Schema, XQuery, Xlink, Xpointer, Xforms...
- Su notación es **similar a las rutas de los ficheros**, salvo que XPath está diseñado para selecciones múltiples.

El documento XML en primer lugar debe ser procesado por un analizador o parser XML que:
- verifica que el documento XML está bien formado
- lo valida contra el DTD / XSD correspondiente
- construye el árbol de nodos
### 1.1. Terminología

- **Nodo raíz**: Nodo que contiene en su interior al ejemplar (nodo raíz) del fichero XML. Se identifica con "/".  No es el nodo raíz del documento XML, ya que este cuelga de él.
- **Nodos elemento**: Cada uno de los elementos del documento XML. Todos tienen un elemento padre, siendo el padre del elemento raíz el nodo raíz del documento. Pueden tener identificadores únicos, siendo necesario que un atributo esté definido de ese modo en un DTD o XSD pudiendo así referenciarlo de forma más directa.
- Nodos texto: No tienen ninguna etiqueta.
- **Nodos atributo:** Son etiquetas añadidas al nodo elemento. Los atributos con valor asignado en el esquema asociado se tratarán como si se hubiesen dado al escribir documento XML. Para los que tienen la propiedad `#IMPLIED` en su DTD no se crean nodos.
- **Nodos de comentario y de instrucciones de proceso.** Se generan para elementos con comentario e instrucciones de proceso. Son hijos del elemento en el que aparezcan o del nodo raíz si están situados fuera del elemento raíz. Por estos elementos el nodo raíz del modelo no coincide con el elemento raíz del documento ya que puede haber comentarios o instrucciones fuera del raíz.
- **Nodo actual**: El que se menciona al evaluar una expresión XPath
- **Nodo contexto**: Cada expresión está formada por subexpresiones que se evalúan antes de resolver la siguiente. Los nodos obtenidos tras evaluar una expresión, usada para evaluar la siguiente son el nuevo contexto.
- **Tamaño del contexto**: Número de nodos que se evalúan en un momento dado en una expresión XPath. 

![](resources/ud05-1.png)

### 1.2. Expresiones XPath y su resultado

Las expresiones XPath son las instrucciones. Se evalúan contra el modelo de datos y devuelven un valor que puede ser:
- **Conjunto de nodos (node-set)**. Una lista de nodos. El orden en el que aparecen en la lista es el mismo en que aparecen en el documento. Se devuelve cuando los operadores usados seleccionan nodos del modelo. Se considera que todos los elementos del node-set son hermanos, independientemente de lo que fuesen originalmente. Los subárboles de un nodo no se consideran elementos del conjunto (hijos de los nodos del node-set, que son accesibles)  
	Los nodos pueden ser de 7 tipos: Elemento, Atributo, Texto, Espacio de nombres, Instrucción de procesamiento, Comentario, Raíz, Booleano, Número y Cadena.
- **boolean**: Valor verdadero o falso, devuelto con operadores lógicos o de comparación
- **number**: Generalmente entero. Se devuelve con operadores numéricos. 
- **string**: Cadena de caracteres. Cuando se seleccionan nodos de texto, comentarios o atributos. 







### Rutas de localización


### Predicados

### Funciones


### Acceso atributos

### Acceso a elementos de otro XML


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

## 2. XSLT

### Estructura de una hoja XSLT

### Elementos XSLT

### Utilización de plantillas

### Procesadores XSLT

### Depuración




