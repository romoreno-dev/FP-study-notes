(UF1 Sintaxis del lenguaje. Objetos predefinidos del lenguaje)

Con el **modelo de objetos del documento (DOM)** se define el contenido de un documento como un conjunto de objetos sobre los que JavaScript puede interactuar.
Se define como una interfaz de programación de aplicaciones (API) para aquellos documentos HTML válidos y para los XML que estén bien construidos. El DOM puede definir la estructura lógica de estos documentos junto con la forma de acceder a ellos y manipularlos.

Un **objeto** es una colección de propiedades que, para definir un estado, utilizan una serie de funciones o métodos que hacen funcionar a esas propiedades.

- Las **propiedades** corresponden a características de dicho objeto
- Los **métodos** son acciones que el objeto puede realizar y que, por tanto, están implementadas y listas para su uso

```javascript
// Creacion de un objeto
var nombreObjeto = new Object();
// Acceder a las propiedades de un objeto con el . y el nombre de la propiedad
nombreObjeto.propiedad
// Acceder a un método concreto de un objeto
nombreObjeto.metodo([parametros])
```

Si es necesario referenciar a una propiedad por su índice, recordar que estas empiezan por 0.

## 1. Utilización de objetos. Objetos nativos del lenguaje

Los objetos nativos del lenguaje de JavaScript son:
- String
- Math
- Number
- Date
### 1.1. El objeto STRING

Permite la manipulación de cadenas de texto.

| Propiedad | Descripción                     |
| --------- | ------------------------------- |
| `length`  | Longitud de una cadena de texto |

| Método                                             | Descripción                                                                           |
| -------------------------------------------------- | ------------------------------------------------------------------------------------- |
| `charAt(index: number)`                            | Devuelve el carácter que se encuentre en la posición indicada                         |
| `concat(...strings: string[])`                     | Concatena varias cadenas                                                              |
| `fontcolor(color: string)`                         | Modifica el color de la fuente de la cadena                                           |
| `fontsize(size: string \| number)`                 | Modifica el tamaño de la fuente de la cadena                                          |
| `indexOf(searchValue: string, fromIndex?: number)` | Devuelve la posición de la primera ocurrencia del carácter que se busque en la cadena |

```javascript
// charAt(index: number)
const str = "Hola";
console.log("charAt:", str.charAt(1)); // → "o"

// concat(...strings: string[])
const saludo = "Hola";
const nombre = "Juan";
const mensaje = saludo.concat(", ", nombre, "!");
console.log("concat:", mensaje); // → "Hola, Juan!"

// fontcolor(color: string)
const textoColor = "Importante";
const coloreado = textoColor.fontcolor("red");
console.log("fontcolor:", coloreado); // → '<font color="red">Importante</font>'

// fontsize(size: string | number)
const textoTamano = "Grande";
const conTamano = textoTamano.fontsize(5);
console.log("fontsize:", conTamano); // → '<font size="5">Grande</font>'

// indexOf(searchValue: string, fromIndex?: number)
const frase = "JavaScript es genial";
console.log("indexOf 1:", frase.indexOf("Script"));    // → 4
console.log("indexOf 2:", frase.indexOf("no existe")); // → -1
console.log("indexOf 3:", frase.indexOf("a", 2));      // → 3
```

### 1.2. El objeto MATH

Permite llevar a cabo una serie de operaciones matemáticas. Math no actúa como constructor, debe llamarse anteponiendo el nombre de este objeto (llamar estáticamente)

| Propiedad | Descripción                        |
| --------- | ---------------------------------- |
| `PI`      | Devuelve el valor del número $\pi$ |
|           |                                    |

| Método     | Descripción                                                            |
| ---------- | ---------------------------------------------------------------------- |
| `abs(x)`   | Devuelve el valor absoluto de x                                        |
| `ceil(x)`  | Devuelve el valor de x redondeando al alza hasta el siguiente entero   |
| `floor(x)` | Devuelve el valor de x redondeando a la baja hasta el siguiente entero |
| `pow(x,y)` | Devuelve el resultado del número x elevado al valor indicado por y     |
| `random()` | Devuelve un valor numérico al azar entre 0 y 1                         |
| `sqrt(x)`  | Devuelve la raíz cuadrada de x                                         |
### 1.3. El objeto NUMBER

- Es poco utilizado porque JavaScript apuesta más por datos numéricos almacenados en variables
- Dispone de información más específica que puede ser utilizada por los desarrolladores
- Sus propiedades se refieren al rango de valores de números que soporta el propio lenguaje siendo el más alto **1.79 E+308** y el más bajo **2.22 E-308**. Los números más altos que el mayor se considera infinito positivo y los más pequeños que el menor se considera infinito negativo.
- Todos los números junto con sus correspondientes valores se encuentran definidos como **valores de doble precisión de 64 bits**

| Propiedad           | Descripción                                        |
| ------------------- | -------------------------------------------------- |
| `MAX_VALUE`         | Mayor número disponible en JavaScript (1.79 E+308) |
| `MIN_VALUE`         | Menor número disponible en JavaScript (2.22 E-308) |
| `NEGATIVE_INFINITY` | Infinito negativo                                  |
| `POSITIVE_INFINITY` | Infinito positivo                                  |
| `NaN`               | Valor especial "Not a number"                      |

| Método                   | Descripción                                                                                                              |
| ------------------------ | ------------------------------------------------------------------------------------------------------------------------ |
| `toExponential()`        | Convierte el número en una notación exponencial                                                                          |
| `toFixed(digits)`        | Formatea el número con la cantidad de dígitos decimales que  se pasa como parámetro. Si no se pasa nada, se considera 0. |
| `toPrecision(precision)` | Formatea el número con la longitud que se pasa como parámetro. Si no se pasa nada, se considera 0.                       |
### 1.4. El objeto DATE

Permite realizar operaciones con el tiempo, trabajando con fechas y horas.

Los objetos se crean mediante su constructor, pudiendo hacerse de cuatro formas diferentes:

```javascript
var d = new Date();
var d = new Date(milisegundos);
var d = new Date(cadenaFecha);
var d = new Date(year, month, day, hour, minuts, seconds, milliseconds);
```

No tiene ninguna propiedad.

Sí que tiene métodos que pueden dividirse en tres subconjuntos:
- **Métodos de lectura**: Tienen prefijo `get`. Consultan diferentes partes de la instancia `Date`
- **Métodos de escritura:** Tienen prefijo `set`. Inicializan diferentes partes de la instancia `Date`
- **Métodos de conversión:** Convierten objetos `Date` en cadenas de texto o en milisegundos,...

| Método             | Descripción                                                                                              |
| ------------------ | -------------------------------------------------------------------------------------------------------- |
| `getDate()`        | Devuelve número correspondiente al **día del mes (1-31)**                                                |
| `getDay()`         | Devuelve número correspondiente al **día de la semana 0(domingo) y 6(sábado)**                           |
| `getFullYear()`    | Devuelve número de 4 cifras correspondiente al **año**                                                   |
| `getHours()`       | Devuelve **hora entre 0 y 23**                                                                           |
| `getMiliseconds()` | Devuelve **milisegundos entre 0 y 9999**                                                                 |
| `getMinutes()`     | Devuelve **minutos entre 0 y 59**                                                                        |
| `getMonth()`       | Devuelve **mes entre 0(enero) y 11(diciembre)**                                                          |
| `getSeconds()`     | Devuelve **segundos entre 0 y 59**                                                                       |
| `getTime()`        | Devuelve número de **milisegundos transcurridos desde 1 de enero de 1970** (timestamp) del objeto `Date` |
| `parse()`          | Analiza una cadena de fecha y devuelve su timestamp.                                                     |
| `setDate()`        | Establece valor del día del mes (1-31)                                                                   |
| `setFullYear()`    | Establece valor del año (4 cifras)                                                                       |
| `setHours()`       | Establece valor de hora (0-23)                                                                           |
| `setMiliseconds()` | Establece milisegundos (0-9999)                                                                          |
| `setMinutes()`     | Establece minutos (0-59)                                                                                 |
| `setMonth()`       | Establece mes (0-11)                                                                                     |
| `setSeconds()`     | Establece segundos (0-59)                                                                                |
| `setTime()`        | Establece fecha, en timestamp                                                                            |
| `toDateString()`   | Convierte la fecha del objeto `Date` a cadena de caracteres                                              |
| `toTimeString()`   | Convierte la parte de tiempo de un objeto `Date` en una cadena                                           |

## 2. Objetos predefinidos asociados al navegador

### 2.1. Navigator

Contiene información **relativa al navegador que se está utilizando**

| Propiedad       | Descripción                                                |
| --------------- | ---------------------------------------------------------- |
| `appCodeName`   | Cadena con el nombre del **código del navegador**          |
| `appName`       | Cadena cuyo valor es el **nombre del cliente**             |
| `appVersion`    | Cadena con la **versión del cliente**                      |
| `cookieEnabled` | Si están habilitadas las cookies en el navegador           |
| `userAgent`     | Cabecera completa `User-Agent` de la petición HTTP enviada |
| `platform`      | Plataforma sobre la que se ejecuta el navegador            |

| Método          | Descripción                          |
| --------------- | ------------------------------------ |
| `javaEnabled()` | Si se permite la utilización de Java |

```javascript
navigator.appCodeName // Mozilla
navigator.appName // Netscape
navigator.appVersion // 5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/136.0.0.0 Safari/537.36
navigator.cookieEnabled // true
navigator.userAgent // 'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/136.0.0.0 Safari/537.36'
navigator.platform // Win32
navigator.javaEnabled() // false
```

### 2.2. Document

En la ventana del navegador se cargan los documentos. Cada documento es un objeto `Document`. Se puede acceder mediante el atributo del objeto `Window` -->  `window.document`

| Colección | Descripción                                    |
| --------- | ---------------------------------------------- |
| `anchors` | Array con todos los hiperenlaces del documento |
| `applets` | Array con todos los applets del documento      |
| `forms`   | Array con todos los formularios del documento  |
| `images`  | Array con todas las imágenes del documento     |
| `links`   | Array con todos los enlaces del documento      |


| Propiedad      | Descripción                                                     |
| -------------- | --------------------------------------------------------------- |
| `cookie`       | Devuelve todos los nombres/valores de las cookies del documento |
| `domain`       | Nombre del dominio del servidor que cargó el documento          |
| `lastModified` | Fecha y hora de la ultima modificación del documento            |
| `readyState`   | Estado de carga del documento actual (ej.: complete)            |
| `referrer`     | URL del documento desde el que se llega al actual               |
| `title`        | Devuelve o ajusta el título del documento                       |
| `URL`          | Devuelve URL completa del documento                             |

| Método                         | Descripción                                                                                       |
| ------------------------------ | ------------------------------------------------------------------------------------------------- |
| `close()`                      | Cierra el flujo abierto previamente con `document.open()`                                         |
| `getElementById(id)`           | Acceder a elemento identificado por su ID                                                         |
| `getElementByName(name)`       | Acceder a elementos identificados por Name                                                        |
| `getElementByTagName(tagName)` | Acceder a elementos identificados por tag                                                         |
| `open()`                       | Abre flujo de escritura para poder usar `document.write()` o `document.writeIn()` en el documento |
| `write(...)`                   | Escribir HTML o JavaScript dentro del documento                                                   |
| `writeIn(...)`                 | Igual que `write()` pero añadiendo salto de línea al final de cada instrucción                    |


### 2.3. Screen

Corresponde a la **pantalla que el usuario utiliza**

Tiene seis propiedades pero no cuenta con ningún método. 

| Propiedad     | Descripción                                            |
| ------------- | ------------------------------------------------------ |
| `availHeight` | Altura disponible de la pantalla para uso de ventanas  |
| `availWidth`  | Anchura disponible de la pantalla para uso de ventanas |
| `colorDepth`  | Número de colores que puede representar la pantalla    |
| `pixelDepth`  | Resolución de la pantalla expresada en bits por pixel  |
| `height`      | Altura total de la pantalla                            |
| `width`       | Anchura total de la pantalla                           |
### 2.4. Window

Es el **objeto más importante del lenguaje JavaScript**. Con él **se puede administrar las ventanas del navegador**.

Es **implícito** porque para acceder a los objetos que están ubicados en el nivel bajo su nivel de jerarquía no es necesario nombrarlo.

| Propiedad     | Descripción                                                                   |
| ------------- | ----------------------------------------------------------------------------- |
| `closed`      | Valor booleano que indica si la ventana está cerrada o no                     |
| `document`    | Documento actual de la ventana (objeto `Document`)                            |
| `frames`      | Conjunto de marcos de la ventana                                              |
| `history`     | Conjunto de elementos que representan las URL visitadas                       |
| `innerHeight` | Altura utilizable de la ventana                                               |
| `innerWidth`  | Anchura utilizable de la ventana                                              |
| `length`      | Número de marcos o iframes de la ventana                                      |
| `location`    | URL de la barra de direcciones                                                |
| `name`        | Nombre de la ventana                                                          |
| `opener`      | Referencia al objeto `Window` que abrió una ventana nueva                     |
| `parent`      | Referencia al objeto `Window` que contiene los marcos de una página de marcos |
| `self`        | Referencia al objeto `Window` de la ventana actual                            |
| `status`      | Cadena con el mensaje que contiene la barra de estado                         |
| `top`         | Ventana de nivel superior                                                     |

| Método                                 | Descripción                                                                         |
| -------------------------------------- | ----------------------------------------------------------------------------------- |
| `alert(message)`                       | Genera cuadro de diálogo con mensaje y botón Aceptar                                |
| `confirm(message)`                     | Genera cuadro de diálogo con botones Aceptar y Cancelar                             |
| `find(text)`                           | Realiza búsqueda de texto en una página (devuelve true o false)                     |
| `focus()`                              | Activa una ventana                                                                  |
| `open()`                               | Abre una nueva ventana                                                              |
| `print()`                              | Imprime una página                                                                  |
| `prompt()`                             | Genera cuadro de diálogo con cuadro de texto para que el usuario introduzca valores |
| `setTimeOut(callback, delay, ...args)` | Ejecutar una función una vez, después de que transcurre un cierto tiempo            |

```javascript
// 1. alert(message)
alert("¡Hola, mundo!"); // Muestra una alerta con el mensaje "¡Hola, mundo!"

// 2. confirm(message)
let resultado = confirm("¿Estás seguro de continuar?");
if (resultado) {
  alert("Has confirmado.");
} else {
  alert("Has cancelado.");
}

// 3. find(text) - Aunque no es un método nativo de JavaScript, usamos algo similar.
let texto = "¡Bienvenido a JavaScript!";
if (texto.includes("JavaScript")) {
  alert("Se encontró 'JavaScript' en el texto.");
}

// 4. focus()
let inputElement = document.getElementById("miInput");
inputElement.focus(); // Establece el foco en el elemento con id "miInput"

// 5. open()
let nuevaVentana = window.open("", "MiVentana", "width=400, height=300");
nuevaVentana.document.write("<h1>Esto es una nueva ventana</h1>");

// 6. print()
window.print(); // Abre el cuadro de diálogo de impresión para imprimir la página

// 7. prompt(message)
let nombre = prompt("¿Cuál es tu nombre?");
if (nombre) {
  alert("Hola, " + nombre + "!");
} else {
  alert("No ingresaste un nombre.");
}

// 8. setTimeout()
setTimeout(() => {
  alert('¡Hola! Este es un mensaje de alerta después de 3 segundos.');
}, 3000);  // 3000 ms = 3 segundos
```

### 2.5. History

**Almacena las referencia de todos los sitios web visitados**. Se guardan en una lista y sus propiedades y métodos se usan principalmente para que el usuario se pueda desplazar hacia adelante y hacia atrás.

Es una **lista de referencias**. **No se puede acceder a los nombres de las direcciones URL visitadas ya que son información privada** del usuario.

| Propiedad  | Descripción                                        |
| ---------- | -------------------------------------------------- |
| `current`  | Contiene la URL de la entrada actual del historial |
| `length`   | Número de páginas que han sido visitadas           |
| `next`     | Contiene la siguiente entrada del historial        |
| `previous` | Contiene la anterior entrada del historial         |

| Método     | Descripción                                                                                           |
| ---------- | ----------------------------------------------------------------------------------------------------- |
| `back()`   | Carga la URL del documento anterior del historial                                                     |
| `foward()` | Carga la URL del documento siguiente del historial                                                    |
| `go()`     | Carga la URL del documento especificado por el índice que pasamos como parámetro dentro del historial |

## 3. Clases

JavaScript se basa en prototipos y cada uno de los objetos tiene una propiedad interna oculta llamada `[[ Prototype ]]` que puede tener propiedades y métodos de objetos.

Las clases de JavaScript surgen como una mejora sobre la herencia basada en estos prototipos.

No es que introduzcan un nuevo modelo de herencia orientada a objetos, sino que aportan una sintaxis mucho más simple y clara.
Las clases son funciones especiales. Igual que en las funciones, la sintaxis de la clase tiene dos componentes:
- Expresiones de clases
- Declaraciones de clase

La declaración de función es izada y la de clase no. **Debe declararse la clase antes de realizar una llamada para crear objetos de esta.** En caso de no hacerlo devuelve un error `ReferenceError`

Para declararla, se usa la palabra `class` junto al nombre de la clase:

```javascript
class Alumno {
	constructor(nombre, apellido, edad) {
		this.nombre = nombre;
		this.apellido = apellido;
		this.edad = edad;
	}
}
```

Las clases pueden definirse también con una **expresión de clase,** pudiendo ser **nombradas o anónimas.** 
El nombre dado a la expresión de clase nombrada será local dentro del cuerpo de esta.

```javascript
// Anónima
var Alumno = class {
	constructor(nombre, apellido, edad) {
		this.nombre = nombre;
		this.apellido = apellido;
		this.edad = edad;
	}
};
// Nombrada
var Alumno = class Alumno {
	constructor(nombre, apellido, edad) {
		this.nombre = nombre;
		this.apellido = apellido;
		this.edad = edad;
	}
};
```

El **cuerpo de una clase** es la parte ubicada entre las llaves, donde se definen los miembros de clase, métodos o constructores y todas las funcionalidades que se quiere que se realice la clase.

El método `constructor`  es un método especial usado para crear e inicializar un objeto creado con una clase. Solo puede haber un método `constructor`. Si contiene más de uno se lanzará un error `SyntaxError`.
El constructor, para llamar al constructor de su superclase, usará la palabra super. 

```html
<!DOCTYPE html>
<html>
	<head>
		<script type=”text/javascript”>
			class Alumno {
				constructor(nombre, apellido, edad) {
					this.nombre = nombre;
					this.apellido = apellido;
					this.edad = edad;
				}
				get Nombre() {
					return this.NombreCompleto();
				}
				NombreCompleto() {
					return this.nombre + ‘ ‘ + this.apellido;
				}
			}
			function MostrarAlumno(){
				const alumno = new Alumno(‘Ilerna’, ‘Online’,
				23);
				alert(‘El nombre completo del alumno es: ‘
				+ alumno.Nombre);
			}
		</script>
	</head>
	<body>
		<h1>Clase Alumno</h1>
		</br>
		<input type=”button” value=”Mostrar valores de la clase alumno” onclick=”MostrarAlumno()” />
	</body>
</html>
```

A los **métodos estáticos** (usados muchas veces para crear funciones de utilidades) se les puede llamar sin instanciar la clase. Para definir un método estático se usa la palabra clave `static`. 

```javascript
class Calculo {
	static multiplicacion(a, b) {
		return a * b;
	}
}
```

Para crear **clases hijas de una clase genérica** se usa la palabra clave `extends`

```javascript
class Persona {
	constructor(nombre) {
		this.nombre = nombre;
	}
	Situacion() {
		return this.nombre + ‘ tiene relación con Ilerna Online.’;
	}
}
class Profesor extends Persona {
	Situacion() {
		return this.nombre + ‘ imparte clases en Ilerna Online.’;
	}
}
class Alumno extends Persona {
	Situacion() {
		return this.nombre + ‘ recibe clases en Ilerna Online.’;
	}
}
function mostrarPersona(){
	var nombre = document.getElementById(‘nombrePersona’).
	value;
	if(document.getElementById(‘profesor’).checked){
		const profesor = new Profesor(nombre);
		alert(profesor.Situacion());
	}else if(document.getElementById(‘alumno’).checked){
		const alumno = new Alumno(nombre);
		alert(alumno.Situacion());
	}else{
		const persona = new Persona(nombre);
		alert(persona.Situacion());
	}
}
```

Las clases tradicionales basadas en funciones también pueden extenderse a otras subclases.

```javascript
function Persona (nombre){
	this.nombre = nombre;
	}
	Persona.prototype.Situacion = function(){
	return this.nombre + ‘ tiene relación con
	Ilerna Online.’;
}
class Profesor extends Persona {
	Situacion() {
		super.Situacion();
		return this.nombre + ‘ imparte clases en
		Ilerna Online.’;
	}
}
class Alumno extends Persona {
	Situacion() {
		super.Situacion();
		return this.nombre + ‘ recibe clases en
		Ilerna Online.’;
	}
}
function mostrarPersona(){
	var nombre = document.getElementById(‘nombrePersona’).
	value;
	if(document.getElementById(‘profesor’).checked){
		const profesor = new Profesor(nombre);
		alert(profesor.Situacion());
	}else if(document.getElementById(‘alumno’).
		checked){
		const alumno = new Alumno(nombre);
		alert(alumno.Situacion());
	}else{
		const persona = new Persona(nombre);
		alert(persona.Situacion());
	}
}
```

La palabra `super()` será usada para llamar funciones del objeto padre.
Las clases no pueden extender objetos regulares (literales). Si se quiere heredar de un objeto regular se debe usar `Object.setPrototypeOf()`

```javascript
var Persona = {
	Situacion() {
		return this.nombre + ‘ tiene relación con
		Ilerna Online.’;
		//alert(this.nombre + ‘hace ruido.’);
	}
};
class Alumno {
		constructor(nombre) {
			this.nombre = nombre;
		}
		Situacion() {
			return this.nombre + ‘ recibe clases en
			Ilerna Online.’;
		}
}
function mostrarPersona(){
		Object.setPrototypeOf(Alumno.prototype, Persona);
		var a = new Alumno(‘Alejandro’);
		alert(a.Situacion());
}
```

El objeto **Array** de JavaScript es un objeto global usado para la construcción de arrays: objetos de tipo lista de alto nivel.
Si se quiere devolver objetos `Array` derivados de una clase array `MyArray`, se seguirá el patrón **species** que permite sobrescribir constructores por defecto. 

Por ejemplo, al usar métodos de tipo `map()` que devuelven el constructor por defecto, se devolverá el objeto padre `Array` en vez de `MyArray`. 
El símbolo **`Symbol.species`** permite hacer lo siguiente:

```java
class MyArray extends Array {
//Sobrescribe species sobre el constructor padre
	Array
		static get [Symbol.species]() { return Array; }
	}
	function mostrarArray(){
		var array = new MyArray(1,2,3);
		var mapa = array.map(x => x * x);
		alert(mapa instanceof MyArray);
		alert(mapa instanceof Array);
	}
```


## 4. Creación de nuevas ventanas

La ventana `Window` (muy presente en JavaScript) **busca trabajar con colecciones/contenedores de datos** referidos a un mismo concepto

- Es el **contenedor principal del contenido visualizado en el navegador*
- Al cargar una ventana, queda definido el objeto `Window` en la memoria. Su área de influencia abarca toda la ventana y barra de herramientas, incluyendo la barra de desplazamiento y la barra de estado.
- Los objetos que permiten manipular y gestionar las características del navegador ya se sabe que son: `location`, `navigator`, `screen`, `history`, `document` y `window`. 

### 4.1. Acceso a propiedades y métodos

- Con `self` se hace referencia al objeto `window` y, de hecho, como siempre está activo se puede omitir la referencia a él.
- Desde JavaScript no se puede crear la ventana principal del programa (lo debe crear el usuario abriendo la ventana en cualquier navegador). Pero una vez ejecutado el script, se pueden crear o abrir nuevas subventanas con el método `open` (que tiene tres parámetros: URL del documento que se abrirá, nombre de la ventana y apariencia física como color,tamaño...). Si la ventana creada se asigna a una variable, se podrá referenciar esta desde el script original a lo largo del código.
```javascript
var subVent = window.open(“new.html”,”new”,”height=800,width=600”);
subVent.close();
```
## 5. Gestión de la apariencia de ventanas

La apariencia puede parametrizarse con las siguientes propiedades:

| Propiedad     | Descripción                                   |
| ------------- | --------------------------------------------- |
| `directories` | Botones del directorio estándar del navegador |
| `height`      | Altura de la ventana (pixeles)                |
| `menubar`     | Barra de menú                                 |
| `resizable`   | Modificar el tamaño de la ventana             |
| `scrollbars`  | Barras de desplazamiento lateral              |
| `status`      | Barra de estad                                |
| `toolbar`     | Barra de herramientas                         |
| `width`       | Ancho de la ventana (pixeles)                 |
Salvo `height` y `width`, el resto de valores indican si se mostrarán o no usando 0 o 1.
   
## 6. Comunicación entre ventanas

La comunicación e interacción entre ventanas no es un proceso del todo bidireccional: La ventana principal puede abrir y cerrar ventanas secundarias pero no al revés (por motivos de seguridad). 

Las nuevas ventanas son declaradas como objetos y se les asigna un nombre gracias al cual puede mantenerse su control. Además la ventana secundaria tiene el atributo `window.opener` que referencia a la ventana principal permitiendo acceder desde la secundaria a los métodos y propiedades de esta. 

```javascript
<!DOCTYPE html>
<html>
	<head>
	<script type=”text/javascript”>
		var ventanaSecundaria = window.open(“”, “Ventana
		Sec.”, “width=500, height=500”);
	</script>
	</head>
	<body>
		<h1>Comunicación entre ventanas</h1>
		</br>
		<form name=”formulario”>
			<input type=”text” name=”url” size=”50” value=”
			http://www.” />
			<input type=”button” value=”Mostrar URL en ventana
			secundaria” onclick=”ventanaSecundaria.location =
			document.formulario.url.value;” />
		</form>
	</body>
</html>
```

## 7. Generación de texto y elementos HTML desde código JavaScript

JavaScript convierte una página estática en aplicación dinámica. 
Se puede manipular y acceder a los objetos que representan el contenido y crear documento dinámicos gracias a métodos como `document.write(...)`.
Este generador de contenido dinámico puede usarse:
- **Usando el método para mostrar resultados en la ventana actual del navegador** a través de secuencias de instrucciones JavaScript
```javascript
<script type = “text/javascript”>
	var SO = navigator.platform;
	document.write(“<h1>Se ha abierto con el navegador:” + SO + ”</h1>”);
</script>
```
- **Utilizando el método para crear documentos en nuevas ventanas** del navegador. 
```javascript
<script type = “text/javascript”>
	var texto = “Título nueva página”;
	var ventana = window.open();
	ventana.document.write(“<h1>” + texto + ”</h1>”);
</script>
```

## 8. Aplicaciones prácticas de los marcos

Un **marco** es un elemento web cuyo objetivo es independizar dentro de la misma web distintas secciones que muestran objetos HTML distintos.
El objeto `frame` representa un marco HTML. 
Cada objeto `frame` se refiere a un marco en cuestión y, por tanto, debe estar dentro de la marca `frameset` que define la esturctura de marcos HTML.

**Propiedades de `frame` e `iframe`**

| Propiedad         | Descripción                                                    |
| ----------------- | -------------------------------------------------------------- |
| `align`           | Contiene el valor del atributo `align` en el iframe            |
| `contentDocument` | Devuelve el objeto documento del frame o iframe                |
| `contentWindow`   | Devuelve el objeto window del frame o iframe                   |
| `frameBorder`     | Devuelve el valor del atributo frameborder del frame o iframe  |
| `height`          | Devuelve el valor del atributo height del frame o iframe       |
| `longDesc`        | Devuelve el valor del atributo longdesc del frame o iframe     |
| `marginHeight`    | Devuelve el valor del atributo marginHeight del frame o iframe |
| `marginWidth`     | Devuelve el valor del atributo marginWidth del frame o iframe  |
| `name`            | Devuelve el valor del atributo name del frame o iframe         |
| `noResize`        | Devuelve el valor del atributo noresize del frame o iframe     |
| `scrolling`       | Devuelve el valor del atributo scrolling del frame o iframe    |
| `src`             | Devuelve el valor del atributo src del frame o iframe          |
| `width`           | Devuelve el valor del atributo width del frame o iframe        |
El usuario así puede interactuar mediante sus marcos y ventanas, provocando cambios en otros marcos.

La **técnica del uso de marcos** está en **desuso**. Actualmente **no se recomienda el uso de los marcos** ya que supone un descontrol el dividir la página principal en tantas páginas como marcos tenga. 
## 9. Cookies

Las **cookies** son una serie de archivos de texto que las aplicaciones almacenan en el ordenador del usuario y que guardan datos que la aplicación puede recuperar.

- El protocolo HTTP no tiene estado, siendo cada petición independiente de la anterior. Las cookies se envían de forma automática en la cabecera de cada petición, permitiendo a las aplicaciones obtener peticiones anteriores gracias a los datos almacenados e nellas.

- Una cookie tiene un **tamaño máximo de 4KB de datos**, permitiéndose hasta 20 cookies por dominio.

- El manejo de cookies se hace mediante el objeto `document`
### 9.1. Lectura y grabación de las cookies

```javascript
// Guardar una nueva cookies llamada usuario con un valor
document.cookie = "usuario = ilerna"; // Cada nueva cookie puede usar este mismo formato
// Editar el valor de la cookie
document.cookie = "usuario = online";
// Leer las cookies
console.log(document.cookie)
// Se muestra algo como: 
// nombre=online; lenguaje=es; fechaUltimaSesion=15/09/2020;
```

### 9.2. Fecha de expiración

Las cookies **son eliminadas por defecto cuando el usuario finaliza la sesión** (cuando cierra el navegador)
Si se quiere que sean **persistentes** (que se mantengan los valores entre sesión y sesión) debe indicarse una fecha de expiración futura (tiempo máximo que vivirá la cookie). 

En JavaScript esto se hace obtenido la fecha actual y añadiendo el tiempo de duración de la cookie (objeto de tipo `Date` y pasarlo a UTC)

```javascript
//Crear objeto tipo fecha, variable hoy
let hoy = new Date();
//Sumar los milisegundos correspondientes a una semana
let caducidadMs = hoy.getTime() + 1000 * 60 * 60 * 24 * 7;
let caducidad = new Date(caducidadMs);
//Colocamos la fecha en formato UTC
document.cookie = “usuario=ilerna;expires=${caducidad.toUTCString()}”;
```

### 9.3. Borrar cookies

Para borrar una cookie se debe indicar una fecha de expiración del pasado. De esta forma la cookie queda caducada y el navegador la elimina automáticamente. 

```javascript
document.cookie = “usuario=ilerna; expires=Sat, 01 Jan 2000 00:00:01 GMT”;
```


