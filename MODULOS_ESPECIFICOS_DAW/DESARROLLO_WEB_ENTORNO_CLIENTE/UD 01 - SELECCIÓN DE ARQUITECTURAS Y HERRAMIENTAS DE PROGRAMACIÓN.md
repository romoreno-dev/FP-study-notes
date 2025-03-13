(UF1)





























### Algún ejemplo

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Title</title>

  <style type="text/css">
    a{
      background-color: black;
      color: white;
      font-size: xx-large;
    }
  </style>

</head>
<body>
<script type="text/javascript" src="ejemplo1.js"></script>
  <a class="boton" onclick="eje()">PULSAME</a>
</body>
</html>

```

```javascript
function eje() {
  var a = "20";
  var b = 20.0;

  console.log("Condicionales:")
  if (a == b) {
    console.log("Son iguales")
  }
  if (a === b) {
    console.log("Son iguales y del mismo tipo")
  } else {
    console.log("Son iguales y de otro tipo")
  }
//------------------------------------------------------------------
//------------------------------------------------------------------
  console.log("operaciones del mismo tipo")
  var suma = a + 2;  // String + 2  lo asimila a String y lo concatena "202"
  console.log(suma)
  var suma = b + "patitos" // Float + String.  Lo asimila a String y lo concatena.
  console.log(suma)
  console.log("Operaciones de tistinto tipo")
  console.log(a + b) // String + Float. Lo asimila a String y lo concatena "2020"
  console.log("Comienzo del bucle")
  for (var i = 0; i < 10; i++) {
    a = a + i // Los asimila a String y los concatena. 
    console.log(a)
  }
}
```

![](resource/ud01-1.png)

#### Diferencias entre var/let

#### var
- Ámbito de **función**
- Su valor es `undefined` hasta que se asigna un valor
- Se puede declarar más de una vez en el mismo ámbito
#### let
- Ámbito de **bloque**
- Solo se puede acceder en el bloque "{}"
- No puede ser usada antes de su declaración, produce error si se usa antes
- No se puede declarar más de una vez en la misma función

```javascript
function ejemploVar() {
	var nombre = "Ana";
	if (true) {
	// Sobreescribe la original
		var nombre = "Carlos";
	}
	console.log(nombre); // Imprime "Carlos"
}


function ejemploLet() {
	let edad = 25;
	if (true) {
		// La edad solo existe dentro del bloque
		let edad = 30;
	}
	console.log(edad);
}

console.log(x); // ❌ ReferenceError: Cannot access 'x' before initialization
let x = 10;
console.log(x); // ✅ 10

console.log(y); // Undefined
var y = 10;
console.log(y); // ✅ 10
```


## Modelo de Objetos del Documento (DOM)

- Representación interna del documento HTML en el navegador como un árbol de objetos
- Cada etiqueta se considera un elemento y cada elemento se considera un objeto. Estos objetos tienen propiedades a las que se puede acceder y modificar. 
- Con JavaScript se puede acceder a métodos depe4ndendiendo del tipo de objeto. 

![](resource/ud01-3.png)

**Objeto**: `var nombreObjeto = new Object()`
**Propiedades**:  `nombreObjeto.propiedad`
**Método**: `nombreObjeto.metodo([parametros])`

## Objetos nativos de JavaScript

### String

Manipular cadenas de caracteres.
(developer.mozilla.org/es/docs/Web/JavaScript/Reference/Global_Objects/String)

**Propiedades**
- `lenght`: Devuelve el número de caracteres
**Métodos**
- `chatAt(posicion)`: Carácter en una posición
- `concat("cadenaNueva"`: Añade a continuación del string la cadena, "cadenaNueva"

```javascript
var texto = new String("Hola");
console.log(texto.length);
console.log(texto.indexOf("1"))
var otroTexto = "Hola";

//¡Atento!
console.log(typeof texto); // Object
console.log(texto instanceof String); // true
console.log(texto == "Hola"); // false

console.log(typeof otroTexto); // "string"
console.log(otroTexto instanceof String); // false
console.log(otroTexto == "Hola") // true

```

### Math

Permite realizar operaciones matemáticas

**Propiedades**
- `PI`: Valor de PI
**Métodos**
- `cos(valor)`: Valor de coseno
- `sqrt(valor)`:Valor de raíz cuadrada

### Number

Trabajar con valores numéricos a niveles absolutos de la máquina o con características específicas.

**Propiedades**
- `MAX_VALUE`: Valor más alto del que se dispone
- `MIN_VALUE`: Valor más bajo del que se dispone
**Métodos**
-` isInteger()` :  Indica si es un entero


### Date

Permite realizar operacion fechas. Se considera como fecha inicial el inicio del Timestamp (1 de enero de 1970).

**Constructor**
```javascript
new Date();
new Date(milisegundos);
new Date(cadena de Fecha);
new Date(año, mes, dia, hor, min, seg, mil);
```
**Métodos**
```javascript
getDate(); Día del mes
getMonth(); Número de mes (0-11)
setMonth(); Establecer valores...
```

```javascript
var fechaHoy = new Date();
fechaHoy.setDate(13);
fechaHoy.setMonth(9);
fechaHoy.setYear(2021);
```


**toISOString** 

```javascript
let fecha = new Date();
let fechaISO = fecha.toISOString(); 
console.log(fechaISO); // Ejemplo de salida: "2025-03-08T12:45:30.000Z"
```

**toLocaleDateString**
```javascript
let fecha = new Date();

// Formato con opciones
let opciones = { weekday: 'long', year: 'numeric', month: 'long', day: 'numeric' };
let fechaFormateada = fecha.toLocaleDateString('es-ES', opciones);
console.log(fechaFormateada);  // Ejemplo de salida: "sábado, 8 de marzo de 2025"
```

### Window

Controla la ventana del navegador. Permite crear y manejar otras ventanas.

**Propiedades**
- `document`: Accede a los elementos del documento
- `location`: URL de barra de direcciones
**Métodos**
- `alert()`: Aviso
- `confirm()`: Mensaje de aceptar/cancelar
- `open()`: Abrir nueva ventana

### Document

Acceder a todos los elementos del documento

**Métodos**
- `document.getElementById(ID)`: Nodo que corresponde con el identificador ID.
- `document.getElementByTagName('etiqueta')`: Devuelve lista con todos los elementos que tengan una etiqueta
- `document.getElementsByClassName("clase")`: Devuelve lista con todos los elementos que sean de una clase
- `document.querySelector(".miClase")`: Selecciona el primer elemento que coincide con un selector CSS dentro del documento o devuelve null si no encuentra ninguno. ( `Node)
- `document.querySelectorAll('u')`: Devuelve todos los elementos que coinciden con tag o selector CSS dentro del documento en una `NodeList`.

### Screen

Información sobre la pantalla del usuario. Solo valores fijos para consultar.

**Propiedades**
- `window.screen.height`: Altura de la pantalla
- `window.screen.availHeight`: Altura disponible en pantalla.

### Creación de clases

```javascript
class Persona(
	constructor(nombre, apellido, edad) {
		this.nombre = nombre;
		this.apellido = apellido;
		this.edad = edad;
	}

	getEdad() {
		return this.edad;
	}
)
```

```javascript
var yo = new Persona("Pepito", "Pérez", 25);
alert(yo.getEdad());
```



### Ejemplos

#### PRIMER EJEMPLO: Implementar listeners para modificar el DOM

Puedo usar **onClick**: 

```javascript
listaEnlaces[i].onclick = function() {  
  document.getElementById('eleccion').innerHTML = this.innerHTML;  
}
```

Puedo usar **addEventListener**: 

```javascript
listaEnlaces[i].addEventListener('click', actualizarValor)
```

Con `addEventListener` es mejor porque:
- puedo agregar tantos eventos como quiera al elemento
- removerlos con `removeEventListener`  

También soporta eventos adicionales en el tercer argumento como **capture**, **once**, **passive**  
 - Capture. En lugar de manejarse del abajo hacia arriba (fase burbujeo), se maneja en fase de captura, de arriba hacia abajo  
 - Once. Solo se ejecuta una vez. `,{once: true}`
 - Passive. El evento no llama a preventDefault(), puede mejorar el rendimiento en eventos scroll o toutchstart `,{passive: true}`


#### ¡Cuidado con donde lo pongo y con los estilos!

Imagina que quiero poner el script en mitad del HTML y como me de la gana:
Podría ser así. 

```javascript
var listaEnlaces = document.getElementsByTagName('u');
for (var i = 0; i < listaEnlaces.length; i++) {
  listaEnlaces[i].onclick = function() {
    document.getElementById('eleccion').innerHTML = this.innerHTML;
  }
}
```

Pero bueno, si uno pone el Script en el head y lo quiere hacer decentemente, habría que:
- prevenir que espere a que se cargue todo el DOM para asignar los listeners
- queda mejor usar `querySelectorAll` (devuelve `NodeList` estática) en lugar de `getElementsByTagName`  (devuelve `HTMLCollection` viva)  y eso permite usar  `forEach`. 
- `getElementsByTagName` solo selecciona por etiqueta, pero `querySelectorAll` soporta selectores CSS (`.class`, `#id`, `ul`, `li`, etc.)

Mira qué bien queda así:

```javascript
    document.addEventListener("DOMContentLoaded", function() {
        let listaEnlaces = document.querySelectorAll('u');

        listaEnlaces.forEach(enlace => {
            enlace.addEventListener('click', function() {
                document.getElementById('eleccion').innerHTML = this.innerHTML;
            });
        });
    });
```

```html
<!DOCTYPE html>  
<html lang="en">  
<head>  
  <meta charset="UTF-8">  
  <title>Ejemplo 1</title>  
  <script type="text/javascript" src="script.js"></script>  
</head>  
<body>  
  
<h1>Ejemplo 1</h1>  
<h2>Pulsa en cualquiera de los enlaces para actualizar el valor que se muestra por pantalla</h2>  

<!-- La etiqueta <u> se usaba antes para subrayar, aunque actualmente es desaconsejada y se aconseja hacerlo mediante CSS !-->
<u>PATATAS</u>  
<u>MACARRONES</u>  
<u>COLIFLOR</u>  
  
<p>En esta casa hoy se come: <span id="eleccion"></span></p>  
  
</body>  
</html>
```


#### SEGUNDO EJEMPLO: Implementar listeners para modificar el DOM

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Title</title>
  <script type="text/javascript" src="script.js"></script>
</head>
<body>

<h2> La fecha actual es: <span id="fecha"></span></h2>

Si multiplico el segundo actual (<span id="segundo"></span>) por el valor de PI, obtenemos un número <span id="parimpar"></span> (<span id="resultado"></span>)

</body>
</html>
```

```javascript
document.addEventListener('DOMContentLoaded',function() {  
  
  let resultado;  
  let fechaElemento = document.getElementById('fecha');  
  let segundoElemento = document.getElementById('segundo');  
  let resultadoElemento = document.getElementById('resultado');  
  let esParElemento = document.getElementById('parimpar');  
  let styleBody = document.querySelector('body').style  
  
  function actualizarFechaYResultado() {  
    let fechaActual = new Date();  
    let segundo = fechaActual.getSeconds();  
    resultado = (segundo * Math.PI).toFixed(0);  
    fechaElemento.innerHTML = fechaActual.getDate() + " de " + fechaActual.toLocaleString("es-ES", {month: "long"}) + " de " + fechaActual.getFullYear();  
    segundoElemento.innerHTML = segundo;  
    resultadoElemento.innerHTML = resultado;  
    let esPar = (resultado % 2 === 0);  
    console.log(esPar);  
    esParElemento.innerHTML =  esPar ? "par" : "impar";  
    styleBody.backgroundColor = cambiaColor(esPar);  
  }  
  
  actualizarFechaYResultado();  
  setInterval(actualizarFechaYResultado, 1000);  
})  
  
function cambiaColor(esPar) {  
  return esPar ? "red": "blue";  
}
```

#### TERCER EJEMPLO: El usuario inserta un texto y, cuando pulse insertar, debe ponerse en Texto de ejemplo. Al pulsar los botones + o - el texto debe aumentar o disminuir de tamaño. 

```html
<!DOCTYPE html>  
<html lang="en">  
<head>  
  <meta charset="UTF-8">  
  <title>Mi texto</title>  
  <script type="text/javascript" src="script.js"></script>  
</head>  
<body>  
  
<h1>Este ejemplo amplía el tamaño del texto</h1>  
  
<p><input type="text" id="texto" tabindex="1"><button id="insertar" tabindex="4">Insertar</button></p>  
  
<p></p><button id="grande" tabindex="2">+</button><button id="pequeno" tabindex="3">-</button></p>  
  
<p class="insertado" style="font-size: 200%;">Texto de ejemplo</p>  
  
</body>  
</html>
```

```javascript
document.addEventListener('DOMContentLoaded', function(){

  let btInsertar = document.getElementById('insertar');
  let btMax = document.getElementById('grande');
  let btMin = document.getElementById('pequeno');

  let inputText = document.getElementById('texto');
  let insertado = document.querySelector('.insertado');

  document.addEventListener('keydown', pulsaTecla)
  btInsertar.addEventListener('click', insertarTexto)

  btMax.addEventListener('click', ampliarTexto)
  btMin.addEventListener('click', reducirTexto)

  function insertarTexto() {
    insertado.textContent = inputText.value;
    inputText.value = "";
  }

  function ampliarTexto() {
    let size = parseFloat(window.getComputedStyle(insertado).fontSize) + 10;
    insertado.style.fontSize = `${size}px`
  }

  function reducirTexto() {
    let size = parseFloat(window.getComputedStyle(insertado).fontSize) - 10;
    insertado.style.fontSize = `${size}px`
  }

  function pulsaTecla(event) {
    console.log(event.key)
    if (event.key === 'Enter') {
      console.log("es enter");
      event.preventDefault(); //Prevenir la accion predeterminada
      insertarTexto();
    } else if (event.key === '+') {
      ampliarTexto();
    } else if (event.key === '-') {
      reducirTexto();
    }
  }

})

```