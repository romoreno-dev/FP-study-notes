
## 1. Introducción.

### 1.1. ECMAScript y DOM

El subconjunto definido en el estándar **ECMAScript** permite homogeneizar los métodos y propiedades de cada navegador (que en principio no tendría por qué ser igual). 
Si bien son iguales, su implementación podría tener diferencias sutiles a la hora de ser implementados.

El **Modelo de Objetos del Documento (DOM)** permite ver el contenido de un documento HTML como un conjunto de objetos sobre los que un programa de JavaScript puede interactuar. 

Se trata, en palabras del W3C de _una interfaz de programación de aplicaciones (API) para documento válidos HTML y bien construidos XML_. Define la estructura lógica de los documentos y el modo en el que se acceden y manipulan.

### 1.2. Breve noción de objeto

**Objeto**: Entidad con una serie de **propiedades** que definen su estado y de **métodos** que actúan sobre esas propiedades. 
Se accede a propiedad: `nombreobjeto.propiedad`
Se accede a método: `nombreobjeto.metodo(...)`
También la propiedad puede ser referenciada por su índice en la creación (son zero-index, comienzan en 0).

## 2. Objetos de más alto nivel u objetos globales del navegador

Los objetos de más alto nivel que se encuentran en Javascript son:
- **window**: La ventana o pestaña del navegador. Contiene todos los demás objetos y métodos para controlar la página.
	- **location**: Información sobre la URL actual, permite redireccionar a otras páginas.
	- **navigator**: Información sobre el navegador del usuario, tipo de dispositivo, sistema operativo
	- **document**: Contenido de la página web y permite manipular el DOM. 
	- **screen**: Información sobre la pantalla del dispositivo
	- **history**: Navegar entre páginas visitadas en la sesión actual. 

### 2.1. Objeto window

- Se encuentra en la **parte superior de la jerarquía**
- Es el **contenedor principal de todo el contenido que se visualiza en el navegador**.
- Tan pronto como se abre una ventana o pestaña, incluso aunque no se cargue ningún documento en ella, este objeto ya está instanciado. Abarca también las dimensiones de la ventana y todo lo que rodea al área del contenido (barras de desplazamiento, de herramientas,de estado,...)
- Si un documento contiene marcos (`iframe`) , el navegador crea un objeto `window` para el documento HTML y objetos adicionales para cada marco.

- Se puede acceder a sus propiedades y métodos de la forma habitual, utilizando la palabra `self` cuando se hace referencia desde el documento contenido en esa ventana (mejor reservarla para scripts más complejos) u omitirlo ya que el objeto `window` siempre estará presente y se asumirá que son del objeto de mayor jerarquía en el que nos encontramos. 

```javascript
// 
window.nombrePropiedad
window.nombreMetodo()
//
self.nombrePropiedad
self.nombreMetodo()
//
nombrePropiedad
nombreMetodo()
```

| Propiedad       | Descripción                                                           |
| --------------- | --------------------------------------------------------------------- |
| `closed`        | Saber si ha sido cerrada  o no                                        |
| `defaultStatus` | Valor por defecto de la barra de estado de una ventana                |
| `frames`        | Array con todos los marcos (incluidos `iframes`) de la ventana actual |
| `length`        | Número de marcos (incluidos `iframes`) de la ventana                  |
| `name`          | Nombre de la ventana. Puede ajustarse                                 |
| `opener`        | Referencia a la ventana que abrió la actual                           |
| `parent`        | Ventana padre de la actual                                            |
| `self`          | Ventana actual                                                        |
| `status`        | Texto de la barra de estado de una ventana                            |
| `location`      | Localización del objeto `window` (URL del fichero)                    |
| `document`      | Objeto `document`                                                     |
| `history`       | Objeto `history`                                                      |
| `navigator`     | Objeto `navigator`                                                    |

| Método            | Descripción                                                                          |
| ----------------- | ------------------------------------------------------------------------------------ |
| `alert()`         | Ventana emergente de alerta y botón de aceptar                                       |
| `blur()`          | Elimina el foco de la ventana actual                                                 |
| `clearInterval()` | Resetea el cronómetro de `setInterval()`                                             |
| `setInterval()`   | Llama a una función o evalúa una expresión en un intervalo específico (milisegundos) |
| `confirm()`       | Ventana emergente con mensaje y botones de aceptar o cancelar                        |
| `focus()`         | Coloca el foco en la ventana actual                                                  |
| `prompt()`        | Ventana de diálogo para introducir datos                                             |

**Método `open()`**
El script no crea la ventana principal del navegador (eso lo hace el usuario). Pero sí que puede crear o abrir nuevas subventanas. 

EL método  `open(...)` tiene tres parámetros:
- URL del documento a abrir
- Nombre de la ventana
- Apariencia física

```javascript
var subVentana = window.open("nueva.html", "nueva", "height=800,width=600");
```

**Método `close()`**
Permite cerrar la ventana. 
```javascript
// La propia ventana, tras pedir confirmación
window.close()
self.close()
close()
// Una subventana
subventana.close()
```

### 2.2. Objeto location

Contiene información sobre la URL actual.

| Propiedad  | Descripción                                  |
| ---------- | -------------------------------------------- |
| `hash`     | Contiene el nombre del enlace                |
| `host`     | Nombre del servidor y número del puerto      |
| `hostname` | Nombre de dominio (o IP)                     |
| `href`     | URL completa                                 |
| `pathname` | Camino al recurso                            |
| `port`     | Puerto del servidor                          |
| `protocol` | Protocolo usado                              |
| `search`   | Contiene la información pasada en la llamada |

| Método      | Descripción                                            |
| ----------- | ------------------------------------------------------ |
| `assign()`  | Carga un nuevo documento                               |
| `reload()`  | Vuelve a carga la URL especificada en href de location |
| `replace()` | Reemplaza el historial actual                          |

### 2.3. Objeto navigator 

Contiene información sobre el navegador.

| Propiedad       | Descripción                                                                                  |
| --------------- | -------------------------------------------------------------------------------------------- |
| `appCodeName`   | Nombre en código del navegador                                                               |
| `appName`       | Nombre del cliente                                                                           |
| `appVersion`    | Versión del cliente                                                                          |
| `cookieEnabled` | Cookies habilitadas o no                                                                     |
| `language`      | Idioma                                                                                       |
| `onLine`        | Si está offline u online                                                                     |
| `platform`      | Plataforma (SO) sobre la que se ejecuta el cliente                                           |
| `userAgent`     | Cabecera completa del agente enviada en petición HTTP. Contiene `appCodeName` y `appVersion` |

| Método        | Descripción          |
| ------------- | -------------------- |
| `javaEnabled` | Si permite usar Java |

### 2.4. Objeto document 

Documento cargado en la ventana del navegador. Permite el acceso a todos los elementos HTML de la página. 

| Colleción   | Descripción                          |
| ----------- | ------------------------------------ |
| `anchors[]` | Todos los hiperenlaces del documento |
| `forms[]`   | Todos los formularios del documento  |
| `images[]`  | Todas las imágenes del documento     |
| `links[]`   | Todos los enlaces del documento      |

| Propiedad  | Descripción                                                 |
| ---------- | ----------------------------------------------------------- |
| `cookie`   | Nombres/Valores de las cookies en el documento              |
| `domain`   | Nombre de dominio del servidor que cargó el documento       |
| `referrer` | URL del documento desde el que se llega al documento actual |
| `title`    | Título del documento                                        |
| `URL`      | URL completa del documento                                  |

| Método                      | Descripción                                                                     |
| --------------------------- | ------------------------------------------------------------------------------- |
| `open()`                    | Abre flujo de escritura                                                         |
| `close()`                   | Cierra flujo de escritura                                                       |
| `write()`                   | Permite escribir expresiones HTML o código de JavaScript dentro de un documento |
| `writeIn()`                 | Como `write()` pero añadiendo un salto de línea al final de cada instrucción    |
| `getElementById(..)`        | Acceder a elemento identificado por el id                                       |
| `getElementsByName(...)`    | Acceder a elemento identificado por name                                        |
| `getElementsByTagName(...)` | Acceder a elemento identificado por tag o etiqueta                              |

## 3. Marcos

Permiten introducir una web dentro de otra. 

La etiqueta `<frame>` identifica una ventana particular dentro de un conjunto de marcos `frameset`.  Para cada etiqueta, se crea un objeto `frame` que representa al marco HTML. 

Esto también se aplica a `<iframe>` , `iframe`. Actualmente HTML 5 no soporta `frame` pero sí `iframe`

(Muy absurda esta tablita de abajo, lo sé. Pero es lo que hay)

| Propiedad         | Descripción                                        |
| ----------------- | -------------------------------------------------- |
| `align`           | Valor del `align` (alineación) en el frame         |
| `contentDocument` | Objeto document contenido por frame                |
| `contentWindow`   | Objeto window generado por frame                   |
| `frameBorder`     | Valor del atributo `frameborder` (borde del marco) |
| `heigth`          | Valor del atributo `height` del frame              |
| `longDesc`        | Valor de descripción larga                         |
| `marginHeight`    | Valor de alto del margen                           |
| `marginWidth`     | Valor de ancho del margen                          |
| `name`            | Valor del nombre                                   |
| `noResize`        | Valor de noResize                                  |
| `scrolling`       | Valor de scrolling                                 |
| `src`             | Valor del origen (src)                             |
| `width`           | Valor del width                                    |

| Evento   | Descripción                                          |
| -------- | ---------------------------------------------------- |
| `onload` | Se ejecutará inmediatamente una vez cargado el frame |

Los marcos se encuentran completamente desfasados ya que las páginas incrustadas en ellos no son completamente accesibles (la URL del navegador no cambia, por lo que no se tiene una referencia directa de la página en la que uno se encuentra). Además los buscadores no indexan bien los frames ya que al registrar su contenido lo toman como si fuese la página principal de ese portal. 
### 3.1. Jerarquías

Cuando se trabaja con marcos se puede referenciar a las ventanas como: 
- frame
- top
- parent

**Ejemplo de frameset**

La ventana del navegador se divide en dos marcos de igual tamaño (el frameset establece las relaciones entre marcos, cargándose en la ventana principal o padre). Cada uno de los frames es un marco hijo (ventanas hijas).

Se forma una jerarquía en la que la ventana padre que contiene el frameset no tiene ningún objeto document sino que son los frames hijos los que lo tienen. (El frameset no puede contener objetos típicos de HTML). En realidad, cada frame, es un objeto window independiente. 

```html
<!DOCTYPE html>
<html>

<head>
	<title>Frames con iframes</title>
</head>

<body>
	<frameset cols="50%,50%">
		<frame name="frame_izq" src="documento1.html" title="Frame 1"></iframe>
		<frame name="frame_drc" src="documento2.html" title="Frame 2"></iframe>
		<noframes></noframes>
	</frameset>
</body>


</html>
```

Los iframes en cambio pueden encontrarse dentro del body y son un poco más flexibles.

`<iframe class="iframe_terra" src="http://terra.es"></iframe>`

### 3.2. Comunicación entre marcos

#### Referencias Padre-Hijos

El documento padre mantiene un array con sus marcos hijos. Se puede acceder al marco a través de la sintaxis de array, por su nombre o por su atributo. 
```javascript
window.frames[n].metodo  // Basado en orden en el que aparecen en frameset
frames["nombreMarco"].metodo
nombreMarco.metodo
```

#### Referencias Hijo-Padre

Es común enlazar scripts al documento padre (frameset) que se carga una vez y permanece cargado con los mismos datos.
El hijo puede acceder al padre simplemente con `parent` o, como está en el top de la jerarquía, con `top`
```javascript
parent.metodo
top.metodo
```

#### Referencias Hijos-Hijos

Deben ser referenciados a través del padre (hijo-padre-hijo)

```javascript
parent.frames[n].metodo  // Basado en orden en el que aparecen en frameset
parent.frames["nombreMarco"].metodo
parent.nombreMarco.metodo
```

### 3.3. Comunicación entre múltiples ventanas

Cada objeto `window` dispone de la propiedad `opener` que tiene referencia al marco que la ha abierto usando `open()`.  La ventana principal tiene `opener = null`
Se puede usar para referenciar a objetos de la ventana padre desde la ventana hija. (Similar a lo que se vio con los frames pero entre ventanas independientes del ordenador)

## 4. Objetos nativos en Javascript

### 4.1. Objeto String

- Pueden emplearse **comillas dobles o simples** para definir el String. Las comillas empleadas que aparezcan de nuevo durante la cadena deberán ser escapadas con `\`
- La concatenación puede realizarse mediante `+=`

```javascript
var nombre = prompt("¿Cómo te llamas?")
var message = "¡¡Hola " + nombre + "!!"
alert(message)
```

`\"` Comilla doble
`\'` Comilla simple
`\\` Barra inclinada
`\b` Retroceso
`\t` Tabulador
`\n` Nueva línea
`\r` Retorno de carro
`\f` Avance de página

| Propiedad | Descripción |
| --------- | ----------- |
| `lenght`  | Longitud    |

| Método              | Descripción                                                                           |
| ------------------- | ------------------------------------------------------------------------------------- |
| `charAt(int)`       | Caracter en posición indicada                                                         |
| `charCodeAt(int)`   | Unicode en posición indicada                                                          |
| concat()            | Une cadenas                                                                           |
| `fromCharCode()`    | Convierte Unicode a caracteres                                                        |
| `indexOf(char)`     | Posición de la primera ocurrencia de un carácter buscado                              |
| `lastIndexOf(char)` | Posición de la última ocurrencia de un carácter                                       |
| `match()`           | Coincidencia entre expresión regular y cadena. Devuelve coincidencias o null          |
| `replace(str, str)` | Reemplaza cadena buscada por nueva cadena especificada                                |
| `search()`          | Encuentra subcadena en cadena devolviendo posición donde se encontró                  |
| `slice()`           | Extrae parte de la cadena y devuelve nueva cadena                                     |
| `split()`           | Divide cadena en array de subcadenas                                                  |
| `substr()`          | Extrae caracteres de cadena comenzando en una posición y con los caracteres indicados |
| `substring()`       | Extrae caracteres de cadena entre dos índices                                         |
| `toLowerCase()`     | Convierte cadena en minúsculas                                                        |
| `toUpperCase()`     | Convierte cadena en mayúscula                                                         |

### 4.2. Objeto Math

Permite realizar cálculos matemáticos. No es instanciable. 

| Propiedad | Descripción               |
| --------- | ------------------------- |
| `E`       | Número de Euler (2.718)   |
| `LN2`     | Logaritmo neperiano de 2  |
| `LN10`    | Logaritmo neperiano de 10 |
| `LOG2E`   | Logaritmo en base 2 de E  |
| `LOG10E`  | Logaritmo decimal de E    |
| `PI`      | Número PI                 |
| `SQRT2`   | Raíz cuadrada de 2        |

| Método           | Descripción                                |
| ---------------- | ------------------------------------------ |
| `abs(x)`         | Valor absoluto                             |
| `acos(x)`        | Arcocoseno                                 |
| `asin(x)`        | Arcoseno                                   |
| `atan(x)`        | Arcotangente de x en radianes              |
| `atan2(y,x)`     | Arcotagente del cociente de los argumentos |
| `ceil(x)`        | Número x redondeado hacia arriba           |
| `floor(x)`       | Número x redondeado hacia abajo            |
| `cos(x)`         | Coseno                                     |
| `log(x)`         | Logaritmo neperiano                        |
| `max(x,y,z,...)` | Máximo                                     |
| `min(x,y,z,...)` | Mínimo                                     |
| `pow(x,y)`       | Potencia de x elevado a y                  |
| `random()`       | Número al azar entre 0 y 1                 |
| `round(x)`       | Redondeo al entero más próximo             |
| `sin(x)`         | Seno                                       |
| `sqrt(x)`        | Raíz cuadrada                              |
| `tan(x)`         | Tangente de un ángulo                      |

### 4.3. Objeto Number

Este objeto no es muy usado pero tiene: 
- Propiedades que indican el rango de números soportados por el lenguaje
- Es envoltorio (wrapper) para valores numéricos primitivos

| Propiedad           | Descripción                                              |
| ------------------- | -------------------------------------------------------- |
| `MAX_VALUE`         | Valor más alto                                           |
| `MIN_VALUE`         | Valor más bajo                                           |
| `NEGATIVE_INFINITY` | Representa a infinitivo negativo (en overflow)           |
| `POSITIVE_INFINITY` | Representa a infinito positivo (en overflow)             |
| `prototype`         | Permite añadir propiedades y métodos propios a un objeto |

| Método             | Descripción                                                                                                       |
| ------------------ | ----------------------------------------------------------------------------------------------------------------- |
| `toExponential(x)` | Convierte número a notación exponencial                                                                           |
| `toFixed(x)`       | Formatea número con x digitos decimales                                                                           |
| `toPrecision(x)`   | Formatea número a cierta longitud                                                                                 |
| `toString(x)`      | Convierte objeto `Number` a una cadena. Si se pone 2 (binario), si se pone 8 (octal), si se pone 16 (hexadecimal) |
| `valueOf()`        | Valor primitivo de objeto `Number`                                                                                |

### 4.4. Objeto Boolean 

Nada reseñable más allá de recordar que posee
- `constructor`
- `prototype`
- `toString()`
- `valueOf()`

### 4.5. Objeto Date

Para gestionar fechas.

Sus constructores posibles son:
```javascript
var d = new Date()
var d = new Date(milisegundos)
var d = new Date(cadena de Fecha)
var d = new Date(año, mes, dia, hora, minuto, segundo, milisegundo)
// El mes comienza en 0
```

| Método                | Descripción                                            |
| --------------------- | ------------------------------------------------------ |
| `getDate()`           | Día del mes (1-31)                                     |
| `getDay()`            | Día de la semana (0-6)                                 |
| `getFullYear()`       | Año (4 dígitos)                                        |
| `getHours()`          | Hora (0-23)                                            |
| `getMilliseconds()`   | Milisegundos (0-999)                                   |
| `getMinutes()`        | Minutos (0-59)                                         |
| `getMonth()`          | Mes (0-11)                                             |
| `getSeconds()`        | Segundos (0-59)                                        |
| `getTime()`           | Milisegundos desde inicio del Timestamp (1-01-1970)    |
| `getTimezoneOffset()` | Diferencia de tiempo entre GMT y hora local en minutos |
| `getUTCDate()`        | Día del mes en base a UTC                              |
| `getUTCDay()`         | Día de la semana en base a UTC                         |
| `getUTCFullYear()`    | Año en base a UTC                                      |
| `setDay()`            | Ajustar día del mes del objeto (1-31)                  |
| `setFullYear()`       | Ajustar año del objeto                                 |
| `setHours()`          | Ajustar hora del objeto                                |
