(UF1 Desarrollo web en entorno servidor)

## 1. Obtención de los lenguajes de marcas para mostrar al cliente

Cuando un cliente lanza una petición a un servidor web cuyo contenido es una página con código del servidor, implica que este sea interpretado antes de mostrarse al cliente. Si este proceso no se realiza, la información sería ilegible para el cliente.

Es necesario que a medida que se interpreta el código, se vaya generando el código resultante HTML.

**Proceso seguido:**
1. El usuario ejecuta un evento y el navegador realiza una petición al servidor correspondiente a través de la URL bajo el protocolo HTTP
2. El servidor recibe la información y la procesa: se ejecutan todos los archivos o scripts necesarios y esto genera el correspondiente código HTML
3. Cuando se obtiene el resultado, se envía el código HTML completo al navegador del lado del cliente que se encarga de mostrárselo al usuario. 

La **obtención del código HTML** es sencilla y depende de la complejidad del lenguaje de programación empleado. Ambos archivos de código tienen una serie de etiquetas que describen el tipo de elemento que es interpretado. Un controlador gestiona el código enlazando los datos obtenidos del servidor para su marcado en la web.
Las **etiquetas** permiten deducir el tipo de elemento que se representará por lo que se transforman fácilmente. La **interpretación de eventos** resulta algo más compleja. Para ella se usan lenguajes como JavaScript que permiten la creación de la estructura asociada al evento, dotando de dinamismo a la web y provocando una serie de cambios en la web ofrecida (roundtrip)

**Roundtrip** es el proceso en el que una web es modificada por la ejecución desencadenada por un evento, que puede producirse por acciones como pulsar un botón, seleccionar diferentes elementos de un desplegable, etc. 

El problema es que cada petición generaría una nueva web, cargando excesivamnte el servidor pero para paliar este problema se recurre al lenguaje AJAX.
## 2. Tecnologías asociadas: PHP; ASP, JSP, miniaplicaciones de servidores (servlets) entre otras

El proceso de obtención del HTML en el lado del cliente se repite de manera periódica en el **ciclo de vida de la página** que tiene como fases: 
- **Inicialización:** Ejecución de los scripts en cliente y servidor
- **Instanciación** de los controles de la página
- **Mantenimiento** de estado de la página
- **Ejecución de los eventos** asociados a una página
- **Envío de la página** al cliente

Según el lenguaje de programación este ciclo de vida puede suponer diferentes etapas. Cada tecnología emplea una serie de mecanismos para obtener como resultado una página web.

### 2.1. Ciclo de vida en PHP

En PHP se divide en dos etapas

1. **Proceso de inicio y cierre del motor PHP**: Esta fase se encarga de arrancar el motor PHP donde se inician todos los módulos declarados en el fichero `PHP.ini`. Esto asigna los recuross correspondientes que se usarán en todo el ciclo de vida mientras se ejecuta el motor PHP y, una vez este se ha cerrado, se liberan.
2. **Ciclo de peticiones**: Se recogen las peticiones realizadas sobre un recurso determinado. Se comunica al navegador, que realiza la petición al servidor, ejecuta los scripts y el intérprete se encarga de recoger la respuesta de la base de datos y enviarla vía URL de nuevo hasta el cliente.
### 2.2. Ciclo de vida ASP ASP.NET

Se fundamenta en los mismos principios que PHP. La única diferencia es en que ejecuta los métodos propios de ese lenguaje para gestionar las peticiones.

### 2.3. Ciclo de vida JSP

- Las peticiones en esta tecnología no son interpretadas sino compiladas.
- Se gestionan mediante pequeños programas (servlets) que procesan petición y generan la página web.
- Su **ciclo de vida** consiste en:
	- 1. **Traducción**: Cada página JSP solicitada se traduce en código del servlet. Se hace uso de las directivas propias del lenguaje para realizar la compilación de la página.
	- 2. **Compilado**: Fase propia que aplica la compilación del servlet generado.
	- 3. **Ejecución**: Ejecución del resultado de la compilación
## 3. Etiquetas para inserción de código

Cualquiera de los lenguajes de programación mencionados se basa en el uso de una serie de etiquetas para identificar los elementos que se van a representar. Así el servidor entiendo cuál es la estructura a generar.

Habitualmente se emplean `<%` y `%>` para delimitar las secciones de código que se deben interpretar. 

En **PHP** sus etiquetas son representadas en diferentes formatos a la hora de insertar fragmentos de código. Puede utilizarse las etiquetas de PHP para el HTML indicando que se trata de una representación en dicho lenguaje: `<?php` y `?>`

En **JSP** las etiquetas se distinguen por su aparición pudiendo ser:
- **Directivas**: Para indicar a JSP los pasos a seguir para llevar a cabo el procesamiento.
- **Scripting**: Porciones de código, por lo general en Java, que se ejecutan cuando la página es procesada
- **Comentarios:** Líneas de texto que no serán interpretadas. Se pueden ver en la compilación obtenida.
- **Acciones:** Interacciones que se van a realizar (redirección a otra página, especificación de ejecución de un servlet, interacción con tors componentes)
```jsp
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<%@ include file="header.jsp" %> <%-- Directiva para incluir otro archivo JSP --%>

<html>
<head>
    <title>Ejemplo JSP</title>
</head>
<body>

	<%-- Comentario JSP: Esta sección define variables y muestra un saludo --%>
	<%
	    String nombre = request.getParameter("nombre");
	    if (nombre == null) {
	        nombre = "invitado";
	    }
	%>
	
	<h2>Bienvenido, <%= nombre %>!</h2>
	
	<%-- Acción JSP para redirigir si el usuario es "admin" --%>
	<%
	    if ("admin".equals(nombre)) {
	%>
	    <jsp:forward page="admin.jsp" />
	<%
	    }
	%>
	
	<!-- Comentario HTML: Esto lo puede ver el usuario en el código fuente -->
	
	<p>Gracias por visitar nuestra página.</p>

</body>
</html>
```

En **ASP.NET** se siguen las mismas pautas que en lenguajes como PHP. Se usan símbolos `<%` `%>` para la inserción de código.

En **HTML** existen etiquetas de carácter general como `<script>`, estas permiten a través de un parámetro especificar el lenguaje de código que se empleará dentro de ellas.
## 4. Tipos de datos. Conversiones entre tipos de datos. Sintaxis del lenguaje. Sentencias

Un **tipo de dato** es un atributo de los datos que indica la forma en la que un compilador o intérprete comprenderá un dato. Cada tipo de dato permite una serie de operaciones que se pueden ejecutar sobre él.

Los **tipos de datos primitivos** son los tipos de datos originales propios de un lenguaje de programación. Permiten a los programadores construir estructuras de datos y tipos abstractos de datos más complejos. Los principales usados son:
- char (carácter)
- int (entero)
- float (real coma flotante)
Y existen otros que pueden considerarse o no primitivos pero que habitualmente lo son:
- booleano (valor lógico)
- string (cadena de caracteres)
- puntero (dirección de memoria - int)

La **conversión de un dato** consiste en cambiar el tipo de dato asociado a una variable de uno a otro. En PHP se transforma automáticamente de un tipo a otro siempre que sea posible. La función `settype()` de PHP permite hacerlo de forma permanente.

```php
$nombreVariable = 'valor inicial';
$nombreVariable = 34 // La variable $nombreVariable cambio de tipo
```

Otros lenguajes como C# o Java permiten conversiones de tipo implícitas y explícitas.

La sintaxis depende de cada lenguaje. Con la sintaxis el programador puede conocer el conjunto de reglas que posibilitan al compilador comprender el código que se está desarrollando. Para que el compilador reconozca la aplicación como válida (y compile) debe seguirla estructura marcada por el lenguaje.
La sintaxis puede llevar algo de tiempo. Por ejemplo en Java la curva de aprendizaje es elevada pero luego permite un gran campo de acciones.

Lenguajes compilados (Java): Debe seguirse la norma o no compila.
Lenguajes interpretados: Es posible que se consiga mostrar el resultado pero su visualización no aparecerá correctamente. Se producirán eventos indeseados.

Debe diferenciarse una **línea de código** de una **sentencia**. La sentencia es toda aquella parte del código escrita hasta la finalización de la misma a través de un símbolo establecido (generalmente `;`). Así, la sentencia puede estar formada por varias líneas de código. 
## 5. Variables

Una **variable** se puede definir como un espacio reservado en el sistema de almacenaje de un ordenador que está asociado a un identificador. 

Las variables pueden ser: 
- **Constantes**: Identificador para un valor simple. El tamaño de la variable no cambia durante la ejecución del programa. Por defecto la constante es `case sensitive` (distingue entre mayúsculas y minúsculas). Es buena praxis declarar los identificadores de constantes en mayúsculas.

```php
//define('nombre constante', 'valor');

define('VALOR_MAXIMO', '60');
echo VALOR_MAXIMO;
//A partir de la versión PHP 5.3.0
const PROYECTO = 'Ilerna Online';
echo PROYECTO;
//A partir de la versión PHP 5.6.0
const PROYECTO2 = PROYECTO.'; Lleida';
echo PROYECTO2;
const PERROS = array('golden', 'boxer',
'podenco');
echo PERROS[0];
//A partir de la versión PHP 7
define(= array(
'Roger Federer',
'Rafael Nadal',
'Novak Ðoković'
));
echo TENISTAS[1];
```

- **Variables:** No es posible predecir el valor que contiene y puede ser modificado durante la ejecución del programa.
```php
$nombreVariable = 'Valor';

$var = 33;
```


**Clasificación de las variables según si tiempo de vida o duración en la ejecución**
- **Globales**: Visibles dentro de todo el programa. El tiempo de vida es el tiempo que dure la ejecución del programa.
- **Locales**: Visibles en una clase o sentencia. El tiempo de vida es el tiempo de ejecución de la clase o sentencia.
- **Estáticas locales:** Visibles dentro de una clase o sentencia. El tiempo de vida es la ejecución del programa. 

Las utilizadas dentro de una función (locales) son diferentes de las usadas fuera.

```php
// 1. $var no se muestra por pantalla porque tiene un ambito local en mitad

function mitad($a){
	$var = $a / 2;
}
$num = 6;
mitad($num);
echo "El valor de la variable \$var es: $var";

----------------------------------------------------

// 2. Pero si se devuelve y se reasigna...

unction mitad($a){
	return($a / 2);
}
$var = 6;
$var = mitad($var);
echo "El valor de la variable \$var es: $var"; // Entonces si lo imprime!!!


----------------------------------------------------

// 3. O si se usan globales (Swe declara dentro del programa, sin contenerla ne ninguan funcion, ni clase y se referencia en funciones o clases con la palabra global. Asi se puede trabajar con la variable y mostrar su valor en cualquier zona del programa)

function mitad(){
	global $var;
	$var = $var / 2;
}
$var = 6;
mitad($var);
echo "El valor de la variable \$var es: $var";

----------------------------------------------------

// 4. Otra opcion es trabajar con globales usando $GLOBALS en lugar de la palabra de reserva global
function mitad(){
	$GLOBALS['var'] = $GLOBALS['var'] / 2;
}
$var = 6;
mitad($var);
echo "El valor de la variable \$var es: $var";
```

- Las variables y los tipos de datos vienen determinadas por cada lenguaje
- Para poder usar una variable primero se tiene que declarar
- El uso de variables globales no es buena praxis de programación porque pued ellevar a errores de código y mayor dificultad de mantenimiento. 
- Algunos lenguajes son fuertemente tipados (ASP.NET), pero PHP que es interpretado permite mayor flexibilidad para declarar variables, el tipo de dato es asignado en función del valor que contiene esa variable.
- Las variables se usan de forma continuada a lo largo del desarrollo. Debe hacerse un uso eficiente de ellas. Debe cuidarse porque reserva espacio de memoria que después debe ser liberado (lenguajes como Java e incluso PHP tienen un mecanismo automático), en el resto de los lenguajes es recomendable asegurarse de liberar los recursos.

---

```php
<!DOCTYPE html>
<html>
	<body>
		<?php
			define(“coche”, [
			“Renault”,
			“Fiat”,
			“Toyota”,
			“Seat”,
			“Suzuki”
			]);
			define(“color”, [
			“azul”,
			“rojo”,
			“negro”,
			“blanco”,
			“gris”
			]);
			$n = (rand(0,4));
			$c = (rand(0,4));
			echo coche[$n], “ “, color[$c];
		?>
	</body>
</html>
```