(UF2 Estructuras definidas por el programador. Objetos)

Los **arrays** de datos se conocen también como listas, vectores o matrices. Y son el tipo de variable que todo lenguaje tiene capaz de gestionar conjuntos de datos. 
Son variables que permiten almacenar en una misma estructura un conjunto de valores. (Permiten controlar múltiples variables)

Para poder acceder a un dato dentro el array es necesario indicar su posición (número entero conocido como **índice**)

**Declaración e inicialización de arrays**

```javascript
var marca = []; //Declarar un array vacío
var marca = new Array(); //Declarar un array con
el operador new con longitud 0
var marca = new Array(100); //Declarar un array
con el operador new de tamaño 100
//Colocar un valor en la primera posición
marca[0] = “Seat”;
marca[1] = “BMW”;
marca[2] = “Audi”;
marca[3] = “Ford”;
console.log(marca[1]); //Muestra: BMW

```

Es posible añadirlos en la misma declaración del array

```javascript
var marca = [“Seat”, “BMW”, “Audi”, “Ford”];
```

**Uso de los arrays mediante bucles**

Es muy útil mezclar las características de los bucles y los arrays para observar cómo trabajar con múltiples variables.

```javascript
var codigos = new Array();
for (var i=0; i<10; i++) {
	codigos[i] = “Código” + i;
}
```

```javascript
for (var i=0; i<10; i++) {
	document.write( codigos[i] + “<br>);
}
```
 
 **Propiedades de los arrays**

| Propiedad   | Descripción                                                     |
| ----------- | --------------------------------------------------------------- |
| `lenght`    | Devuelve el número de elementos que contiene el array           |
| `prototype` | Es posible agregar nuevas propiedades y métodos al objeto array |
`nombreArray.length;`

**Métodos de los arrays**

`array.metodo()`

| Método                                                     | Descripción                                                                                  |
| ---------------------------------------------------------- | -------------------------------------------------------------------------------------------- |
| `push(valor1, valor2,...)`                                 | Añadir nuevos elementos y devolver la lognitud del array                                     |
| `concat(valor1, valor2,...)`                               | Concatenar elementos de un array en un nuevo array                                           |
| `join([separador])`                                        | Concatenar elementos de un array en una cadena de texto separada por un carácter (opcional). |
| `reserse()`                                                | Invertir el orden de los elementos de un array                                               |
| `unshift(valor1, valor2,...)`                              | Añadir nuevos elementos al inicio y devolver el número de elemento del array                 |
| `shift()`                                                  | Eliminar el primer elemento de un array                                                      |
| `pop()`                                                    | Eliminar el último elemento de un array                                                      |
| `sort([funcion])`                                          | Ordenar alfabéticamente los elementos de un array                                            |
| `splice(inicio, [num_elem_borrar], [valor1, valor2, ...])` | Eliminar, sustituir o añadir elementos a un array dependiendo de los argumentos del método   |
## 1. Funciones predefinidas del lenguaje

JavaScript tiene una serie de funciones predefinidas (integradas en el propio lenguaje). Pueden ser utilizadas sin necesidad de ser declaradas. Basta con saber el nombre de la función y el resultado que se va a obtener.

Muchas de estas funciones funcionan sin necesidad de información extra. Aunque la mayor parte de estas funciones requieren acceder a los valores de las variables para producir sus resultados (estas variables que reciben las funciones se denominan **argumentos** o **parámetros** de la función).

| Función predefinida | Descripción                                                                                                                                                                                                                                                                                                      |
| ------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `escape()`          | Recibe una cadena de caracteres como argumento y devuelve esa misma cadena sustituida con codificación de caracteres ASCII.<br>`Unscape()` es la función opuesta, decodifica los caracteres que estén codificados.                                                                                               |
| `eval()`            | Convierte una cadena pasada como argumento en código JavaScript ejecutable. Puede usarse por ejemplo para ingresar una operación numérica y ver el resultado.                                                                                                                                                    |
| `isFinite()`        | Verifica si el número pasado como argumento es o no un número finito. ±1.7976931348623157 10^308                                                                                                                                                                                                                 |
| `isNaN()`           | Comprueba si el valor pasado es de tipo númerico                                                                                                                                                                                                                                                                 |
| `Number()`          | Convierte el objeto pasado por argumento en un número que representa el valor del argumento                                                                                                                                                                                                                      |
| `String()`          | Convierte el objeto pasado como argumento en una cadena que representa el valor del objeto                                                                                                                                                                                                                       |
| `parseInt()`        | Convierte la cadena que se pasa como argumento en un valor numérico entero. Si no se especifica la base se supone base decimal. Puede ser  base binaria, octal, decimal o hexadecimal. Si el valor no es numérico devuelve el valor encontrado hasta ese punto y si el primer valor no es numérico devuelve NaN. |
| `parseFloat()`      | Convierte la cadena que se pasa como argumento en un valor numérico flotante                                                                                                                                                                                                                                     |

```javascript
var input = prompt(“Introduce una cadena de texto:“);
var inputCodigo = escape(input);
alert(“Cadena codificada: “) + inputCodigo;

var input = prompt(“Introduce una operación numérica:“);
var resultado = eval(input);
alert(“El resultado de la operación es: “ + resultado);

if(isFinite(argumento)){
	//instrucciones si el argumento es un número finito
}else{
	//instrucciones si el argumento no es un número
}

var input = prompt(“Introduce un valor numérico:“);
if(isNaN(input)){
	alert(“El dato introducido es numérico”);
}else{
	alert(“El dato introducido no es numérico”);
}

var input = prompt(“Introduce un valor:”);
var inputNumber = Number(input);
alert(“El valor introducido: “ + inputNumber);

var fecha = new Date();
var fechaString = String(fecha);
alert(“La fecha actual es: “ + fechaString);

var input = prompt(“Introduce un valor: “);
var inputParsed = parseInt(input);
alert(“parseInt (“ + input + “): “ + inputParsed);

var input = prompt(“Introduce un valor: “);
var inputParsed = parseFloat(input);
alert(“parseFloat (“ + input + “): “ + inputParsed);
```

## 2. Definición y llamadas de funciones

Las **funciones** son un conjunto de instrucciones relacionadas para realizar una tarea específica.

- Es conveniente que sean **diseñadas de forma que puedan ser reutilizadas** en otras aplicaciones. Así serán **pequeños bloques constructivos** que permitirán desarrollar los nuevos programas de forma más rápida. 
- Se usa en otros lenguajes el término de **procedimiento o subrutina** (los que ejecutan acciones) o **funciones** (los que ejecutan acciones y devuelven algún valor). En JavaScript, sin embargo, todo son funciones.
- La función siempre va desarrollada entre llaves `{ }`
- Para invocarla se hace a través de su identificador seguido de los parámetros de entrada y también debe llevar paréntesis a la hora de realizar su llamada. Puede ser llamada en HTML dentro de `<script>` o dentro de las etiquetas de los elementos HTML.
- Siempre devuelven respuesta mediante `return` y si devuelve un valor no especificado devuelve `undefined`. Todo código que existiese detrás del return no se llegará ejecutar nunca. 

### 2.1. Argumentos

- No existe ninguna regla sobre el número de parámetros que se debe representar. Si una función espera tres argumentos se puede facilitar uno, cinco,... puesto que **los parámetros se gestionan de forma interna como un array**
- Los **parámetros en JavaScript siempre se pasan por valor**: Se crea una copia en memoria del valor o conjunto de valores. ¡Cuidado! Hay un comportamiento diferente según se reciba un tipo primitivo o un tipo de referencia. Por eso es conveniente tener un paso por valor y otro por referencia aunque JavaScript solo lo realice por valor. 

- **Valores por valor**: Primitivo. Copia en una variable local el parámetro recibido. Apunta a una dirección de memoria distinta. Los cambios del interior de la función no se trasladan fuera de esta.
- **Valores por referencia**: Referencia. Copia en una variable local el parámetro recibido. Apunta a la misma dirección de memoria. Los cambios en el interior de la función sí se trasladan fuera de esta. 

### 2.2. Otras declaraciones

**Declaración de funciones mediante una expresión**

No se le llamará usando el identificador dado a `function` (ejemplo) sino la variable (`mifuncion`)

```javascript
var mifuncion = function ejemplo (texto){
	return texto + texto;
};
function llamadaFuncion (){
	alert(mifuncion(‘Hola Mundo ‘));
};
```

**Objeto función**
Se pueden crear funciones dinámicas con la palabra reservada function junto con su declaración utilizando una cadena de texto de las diferentes sentencias y valores que devuelve. 
Esta forma hacer uso del objeto `Function`. Su constructor tiene dos parámetros: Uno para definir los atributos y otro para definir el cuerpo de la función o bloque de sentencias.

```html
<html>
	<head>
		<script type=”text/javascript”>
			//Objeto función
			var miFuncion = new Function(‘texto,lugar’,’alert(texto
			+ “ “ + lugar)’);
			function llamada(){
			miFuncion(‘Prueba de ejecucción función objeto en:’,
			window.location.pathname);
			}
		</script>
	</head>
	<body>
		<h1>Objeto Función</h1>
		</br>
		<input type=’button’ onclick=’llamada();’ value=’
		Pulsar’ />
	</body>
</html>
```

### 2.3. Funciones anidadas

Son **funciones que tengan en su contenido otra función**. Es fundamental que se tenga clara la importancia que tiene el ámbito de una variable. Es posible que cualquier función interna tenga acceso a todo el contenido de ejecución externa pero no sucede lo mismo en caso contrario ya que la externa solo puede llamar a la interna por su nombre. 

```html
<!DOCTYPE html>
<html>
	<head>
		<script type=”text/javascript”>
			//Funciones Anidadas
			function calcular(){
			var x = 7;
			//Función anidada
			function incrementar(valor){
				return ++valor;
			}
				return incrementar(numero) + x;
			}
		</script>
	</head>
	<body>
		<h1>Funciones Anidadas</h1>
		<input type=’button’ onclick=’alert(calcular(5));’ value=’Pulsar’ />
	</body>
</html>
```

## 3. Objetos definidos por el usuario

### 3.1. Declaración e inicialización de objetos

El **objeto** se puede definir como entidad que prosee propiedades y métodos que actúan sobre estas propiedades.

Se declaran como una función empleando la clase `function` mediante la sintaxis siguiente:
```javascript
function mi_objeto (valor1, valor2, valorx) {
	this.propiedad1 = valor1;
	this.propiedad2 = valor2;
	this.propiedadx = valorx;
}
```
Puede darse un nombre a este nuevo objeto y asignarle unos valores iniciales a cada una de sus propiedades definidas:
```javascript
function Coche (marca_in, modelo_in, año_in) {
	this.marca = marca_in;
	this.modelo = modelo_in;
	this.anyo = año_in;
}
```

Una vez declarado el objeto, se pueden crear instancias de este con la palabra clave `new`

```javascript
var coches = new Array(3);
coches[0] = new Coche(“Seat”, “León”, “2018”);
coches[1] = new Coche(“Ford”, “Focus”, “2019”);
coches[2] = new Coche(“Hyundai”, “i30”, “2019”);
```

### 3.2. Definición de propiedades y métodos

Para crear las propiedades se emplea la palabra clave `this` seguida del nombre de la propiedad y su valor. Esta palabra hace referencia al objeto en el que se utiliza la palabra aunque se puede también crear nuevas propiedades sin que hayan sido declaradasne un mismo objeto. 

```javascript
function Coche (marca_in, modelo_in, año_in) {
	this.marca = marca_in;
	this.modelo = modelo_in;
	this.anyo = año_in;
}
var mi_coche1 = new Coche(“Volkswagen”, “Golf”,
“2007”);
mi_coche1.color = “Gris”;
```

La instancia `mi_coche1` tiene una nueva propiedad que informa del color y que solo afectará a este objeto. 

También, como resulta obvio, se pueden establecer objetos como propiedad de otro objeto (que tendrá sus propias características, claro)

Por ejemplo también podríamos crear una función que imprimiese por pantalla los datos del coche:

````javascript
function imprimirDatos() {
  document.write("<p> Marca: " + this.marca + "</p>");
  document.write("<p> Modelo: " + this.modelo + "</p>");
  document.write("<p> Año: " + this.año + "</p>");
}

function Coche(marca_in, modelo_in, año_in) {
  this.marca = marca_in;
  this.modelo = modelo_in;
  this.año = año_in;
  this.imprimirDatos = imprimirDatos;
}

var mi_coche1 = new Coche("Volkswagen", "Golf", "2007");
mi_coche1.imprimirDatos();
```
