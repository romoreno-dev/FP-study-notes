
## 1. Arrays

El array (matriz, vector, arreglo) es una de las estructuras de datos más utilizadas en todos los lenguajes. Se define como una colección ordenada de datos. Es una variable (zona de almacenamiento continuo) en la que pueden introducirse varios valores.  Se introducen a partir de la versión 1.1. 

Se puede considerar que todos los arrays son de una dimensión, pero los elementos de dicha fila pueden contener otros arrays o matrices (arrays multidimensionales). 

Son adecuados para situaciones en las que el acceso a datos se realiza de forma aleatoria. Para acceso secuencial es más adecuado el uso de una lista (que tiene como ventaja que su tamaño puede cambiar fácilmente)

Los elementos de un array se pueden indexar de varias formas:
 - zero-based: Primer elemento es el 0. Es el caso de Javascript. 
 - one-based: Primer elemento es el 1
 - n-based: El índice del primer elemento se elige libremente. 

JavaScript utiliza arrays para gestionar objetos HTML en el documento, propiedades del navegador, etc. Ej.: Las colecciones dentro del objeto `document` como `anchors[]`, `forms[]`, `links[]`, `images[]`.

#### Creación e inicialización

```javascript
// Creacion de un array
var array = new Array()
var array = new Array(40)  // Se inicializa con 40 posiciones null.
// El dimensionamiento previo no presenta ninguna ventaja, ya que se puede asignar valor a cualquier posicion, esté o no definida previamente. La propiedad length se ajustará para poder almacenar la posición seteada. 
array[53] = "Desarrollo web en entorno cliente"
```

Si se accede a una posición de array no definida se obtiene el valor `undefined`

Existe la posibilidad de crear el array mediante constructor con un **array denso** en el que se le aportan los datos a cubrir separados por comas:

```javascript
sistemaSolar = new Array("Mercurio","Venus","Tierra","Marte","Jupiter","Saturno","Urano","Nepturno")
```

También puede definirse sin necesidad de constructor sino de forma literal (Desde JavaScript 1.2)

```javascript
sistemaSolar=["Mercurio","Venus","Tierra","Marte","Jupiter","Saturno","Urano","Nepturno"]
```

Puede crearse un **array mixto** u objeto literal en el que las posiciones se referencian con índices de tipo texto o números, mezclándolos de forma aleatoria. (Pares clave-valor). Se crean como `nombreArray = {"indice1":valor, indice2: "valor", ...}`

```javascript
var datos = { "numero":42, "mes":"Junio", "hola":"mundo", 69:"96"}
```

#### Otras combinaciones

```javascript
// Crear matriz vacía pero de otra forma distinta
var datos = []
// Posicion asociativa
datos[-124] = "valor"
// No asociativo ya que rendondea a 1. 
datos[1.0] = "contenido"
// Asociativo
datos["tres] = ""
```

#### Recorrer un array

```javascript
// Bucle for
for (i = 0; i < sistemaSolar.lenght; i++)
	document.write(sistemaSolar[i] + <br/>)

// Bucle while
var i = 0
while (i < sistemaSolar.length) {
	document.write(sistemaSolar[i] + <br/>)
	i++
}

// for in
for (var i in screen)
	document.write("Propiedad" + i + " y valor " + "screen[i]" + "<br/>")


```


#### Borrar elementos en un array

Para borrar cualquier dato, basta con ajustar su valor a `null` o a `""`

**Delete** El eliminar el elemento, se elimina su índice pero no se reduce la longitud del array. Se recomienda para arrays que usen texto como índices del array (así se evitan confusiones)

```javascript
delete miArray[5] // Borra esta posicion
```

**Splice** El borrado no libera la memoria ocupada por esos datos sino que el ínterprete de JavaScript, encargado de gestionar la colección de basura en memoria, liberará esa memoria ocupada cuando la necesite. 
Para tener mayor control sobre su eliminación, debe usarse el método `splice(índice, numero de elementos a eliminar)`, soportado por la mayoría de los navegadores. Este método permite eliminar elemento o secuencia de elementos, provocando que la longitud del array se ajuste al nuevo número de elementos. 

```javascript
oceanos.splice(2,1) // Elimina la posicion 2. Desplazandose a ella la posicion 3. 
```

#### Propiedades y métodos 

| Propiedad     | Descripción                                                |
| ------------- | ---------------------------------------------------------- |
| `length`      | Número de elementos del array                              |
| `constructor` | Devuelve la función que creó el prototipo del objeto array |
| `prototype`   | Permite añadir propiedades y métodos a un objeto           |

| Método       | Descripción                                                              |
| ------------ | ------------------------------------------------------------------------ |
| `concat()`   | Une dos o más arrays, devolviendo copia de la unión                      |
| `join()`     | Une todos los elementos en una cadena de texto                           |
| `reverse()`  | Invierte el orden de los elementos del array                             |
| `slice()`    | Selecciona una parte de un array y devuelve el nuevo array               |
| `sort()`     | Ordena los elementos                                                     |
| `splice()`   | Añade/elimina elementois                                                 |
| `toString()` | Convierte array a cadena                                                 |
| `valueOf()`  | Devuelve el valor primitivo de un array                                  |
|              |                                                                          |
| `unshift()`  | Añade nuevos elementos al comienzo y devuelve la nueva longitud          |
| `shift()`    | Elimina el primer elemento de un array y lo devuelve                     |
| `pop()`      | Elimina el último elemento de un array, devolviéndolo                    |
| `push()`     | Añade nuevos elementos al final del array, devolviendo la nueva longitud |

#### Ejemplillos

```javascript
var frutas = ["Plátano", "Naranja", "Manzana", "Melocotón"];

// reverse()
frutas.reverse(); // (4) ['Melocotón', 'Manzana', 'Naranja', 'Plátano']

// slice()
frutas.slice(0,1) // ['Plátano']
frutas.slice(1) // ['Naranja', 'Manzana', 'Melocotón']
frutas.slice(-2)  // ['Manzana', 'Melocotón']

// Añade y quita por la derecha LIFO (Last In, First Out)
// push() y pop()
// PILAS: Se añaden elementos a continuacion de la maxima posicion del array
var pila = ["pepe", "antonio"]
pila.push("miguel")  // Devuelve 3
pila.pop() // Devuelve 'miguel'

// Añade y quita por la izquierda FIFO (First In, First Out)
// unshift() shift() 
// COLAS: Se añaden elementos en la mínima posición del array
var pila = ["pepe", "antonio"]
cola.shift() // Devuelve 'pepe'  (lo saca de la cola)
pila.unshift("jesus") // Devuelve 4 (lo mete en la cola, ahora es (4) ['jesus', 'pepe', 'antonio', 'miguel'])
```

#### Arrays paralelos

Los **arrays paralelos** son dos o más arrays que utilizan el mismo índice para referirse a términos homólogos. Es decir, permiten almacenar diferente tipo de información en arrays que están sincronizados.

Los arrays paralelos deben tener la misma longitud para tener la consistencia de la estructura lógica creada.
Como ventajas:
- Pueden usarse en lenguajes que soportan solo arrays y no registros
- Fáciles de entender
- Ahorran gran cantidad de espacio evitando complicaciones de sincronización
- El recorrido secuencial es muy rápido en las máquinas actuales

#### Arrays multidimensionales

Es una alternativa a los arrays paralelos. En definitiva son arrays que en sus posiciones contienen otros arrays u objetos. 

```javascript
// Definimos
var datos = new Array();
datos[0] = new Array("Cristina", "Seguridad", 24)
datos[1] = new Array("Carolina", "BBDD", 18)
datos[2] = new Array("Josefa", "Redes", 29)
// O bien
var datos = [
	["Cristina", "Seguridad", 24],
	["Carolina", "BBDD", 18]
	["Josefa", "Redes", 29]
];

document.write("Alumna:" + "Nombre - " + datos[0][0] + "Asignatura - " + datos[0][1] + "Edad - " + datos[0][2]))
```

## 2. Funciones

Una **función** es la definición de un conjunto de acciones preprogramadas. Se llaman a través de eventos o mediante comandos desde el script. 
Deben diseñarse funciones que puedan reutilizarse de tal forma que se conviertan en pequeños bloques constructivos. 
En otros lenguajes se distinguen entre **procedimientos** (acciones)  y **funciones** (acciones que devuelven valores), pero esta diferencia no se hace en JavaScript. 
```
function nombreFuncion([parametro1]...[parametroN]) {
// instrucciones
}
```

Por ejemplo:
```javascript
function saludar(a,b) {
	alert("Hola " a + " y " + b)
}

function devolverMayor(a,b) {
	var devolver;
	if (a > b)
		devolver = a;
	else
		devolver = b;
	return (devolver);
}

saludar("Alice","Bob")
document.write("El número mayor entre 35 y 21 es el: " + devolverMayor(35,21) + ".");
```

#### Ámbito de variables
- Son variables **globales** aquellas definicidas fuera de funciones. El alcance de estas variables se limita al documento actual cargado en la ventana del navegador o en un frame. Todas las instrucciones (incluidas dentro de las funciones) tienen acceso directo al valor de esa variable pudiendo leerla o modificarla. Al cerrar la ventana o el frame todas las variables definidas en memoria desaparecen. Para que su valor persista deben usarse técnicas como cookies o ponerla en el documento `frameset`, etc. 

	El uso de la palabra reservada `var` realmente es opcional pero es buena práctica usarlo porque en el modo estricto de JavaScript es obligatorio. 
	También se dispone de `let` y `const`

- Son variables **locales** las definidas dentro de funciones. Aquí sí es obligatorio el uso de la palabra reservada `var` o, de lo contrario, será reconocida como una variable global. 

Un bug frecuente puede darse debido a **reutilizar el nombre de una variable global** como local. La variable local en momentos puntuales ocultará el valor de la variable global sin informar de ello. Por ello, no se considera una buena práctica. 

#### Funciones anidadas

Las **funciones anidadas** permiten encapsular la accesibilidad de una función dentro de otra y hacer que esa función sea privada o local a la función principal.
Debe tenerse cuidado y no reutilizar nombres de funciones con esta técnica para evitar confusiones posteriores. 

Las funciones anidadas pueden utilizarse cuando se tiene una secuencia de instrucciones que necesitan ser llamadas desde múltiples sitios dentro de una función y esas instrucciones solo tienen significado dentro del contexto de esa función principal. 
Así, en lugar de romper la secuencia de una función larga en varias funciones, se hará esto mismo pero con funciones locales. 

Su estructura es algo así:

```
function principalA()
{
	//instrucciones
	function internaA1()
	{
		//instrucciones
	}
	//instrucciones
}
function principalB()
{
	//instrucciones
	function internaB1()
	{
		//instrucciones
	}
	function internaB2()
	{
		//instrucciones
	}
	//instrucciones
}
```

Ejemplificado como: 

```javascript
function hipotenusa(a,b) {
	function cuadrado(x) {
		return x * x
	}
	return Math.sqrt(cuadrado(a) + cuadrado(b))
}

document.write("La hipotenusa de 1 y 2 es:" + hipotenusa(1,2));
```

#### Funciones predefinidas del lenguaje

En JavaScript existen elementos que necesitan ser tratados a escala global y que no pertenecen a ningún objeto en particular (es decir, que se pueden aplicar a cualquier objeto). 

**Propiedades globales en JavaScript**
- **infinity**: Valor numérico que representa el infinito positivo/negativo
- **NaN**: Valor no númerico ("Not a number")
- **undefined()**: A esa variable no se le ha asignado un valor

**Funciones globales en JavaScript**

| Función                | Descripción                                                               |
| ---------------------- | ------------------------------------------------------------------------- |
| `decodeURI()`          | Decodifica caracteres especiales de una URL excepto `, / ? : @ & = + $ #` |
| `decodeURIComponent()` | Decodifica todos los caracteres especiales de una URL                     |
| `encodeURI()`          | Codifica caracteres especiales de una URL excepto `, / ? : @ & = + $ #`   |
| `encodeURIComponent()` | Codifica todos los caracteres especiales de una URL                       |
| `escape()`             | Codifica caracteres especiales en una cadena excepto `* @ - _ + . /`      |
| `eval()`               | Evalúa una cadena y la ejecuta si contiene código u operaciones           |
| `isFinity()`           | Dice si un valor es un número finito válido                               |
| `isNaN()`              | Dice si un valor no es un número                                          |
| `Number()`             | Convierte el valor de un objeto a número                                  |
| `parseFloat()`         | Convierte cadena a número real                                            |
| `parseInt()`           | Convierte cadena a entero                                                 |
| `unescape()`           | Codifica caracteres especiales en una cadena excepto `* @ - _ + . /`      |

Ejemplo de `eval()`:

```html
<script>
	eval("x=50;y=30;document.write(x*y)"); // Imprime 1500
	document.write(eval("1+1")) // Imprime 2
</script>
```

## 3. Objetos





## 4. EcmaScript 6





`prototype` Permite añadir propias propiedades y métodos au n objeto???



🔹 Aquí, `ventanaCreada == false` devuelve `true` porque `""` (string vacío) es un valor **"falsy"** y JavaScript lo convierte implícitamente a `false` para hacer la comparación.



