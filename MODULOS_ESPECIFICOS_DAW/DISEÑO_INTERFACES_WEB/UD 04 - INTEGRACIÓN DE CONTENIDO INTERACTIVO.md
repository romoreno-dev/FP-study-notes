
## 1. Herramientas para la inclusión de contenido multimedia interactivo

Los lenguajes de marcas tienen la facilidad de poder ser escritos en cualquier herramienta de procesado de textos. 
### 1.1. Editores simples

Los sistemas operativos instalados en equipos informáticos disponen de herramientas básicas de procesado de textos. Windows: Bloc de notas, Notepad (.txt). Pueden emplearse para escribir lenguaje de marcas HTML siempre que se guarden con su correspondiente extensión.
### 1.2. Editores avanzados

Debido a las numerosas líneas que contienen los ficheros de las páginas webs, a la interacción con otros lenguajes, incrustaciones de códigos, lenguajes externos, etc. es más complicada cada vez la identificación de las marcas para el desarrollador.

Para ello, surgen **editores de texto avanzados** que dan una interfaz amigable y sencilla de utilizar. En ellos puede diferenciarse mediante diversos colores cada elemento del lenguaje de marcas HTML, facilitando la tarea al desarrollador y a cualquiera que necesite visualizarlo. 

Además, estos editores ante cualquier incidencia proporcionan una serie de opciones para su fácil identificación. 
### 1.3. Gestores de lenguajes HTML

Una vez está diseñado todo el código HTML, este podrá ser visualizado en cualquier navegador de Internet (navegador web)
## 2. Configuración de navegadores

Los **navegadores** son herramientas destinadas a la visualización de las páginas web. A medida que los portales webs necesitan más lenguajes para su tratamiento, los navegadores deben estar configurados y preparados para su visualización. Herramientas como Flash (deprecado), Java, ... deben estar instaladas para poder visualizar las webs. 

Cada navegador tiene una ruta y distintas opciones para su configuración. 

## 3. Elementos interactivos básicos y avanzados

En el **desarrollo web** tiene elementos multimedia para multitud de funciones, permitiendo la interacción con dichos elementos.

Se define la **interacción** como el proceso que establece un usuario con un dispositivo, sistema u objeto determinado. Es una acción recíproca entre el elemento con el que se interacciona y el usuario. 

El desarrollo de las interacciones suele llevarse a cabo mediante HTML5, CSS3 y JavaScript (Flash está en desuso). 

**jQuery** es una biblioteca de JavaScript que permite realizar multitud de acciones, es libre y de código abierto.
### 3.1. Introducción a JQuery

#### Incorporar JQuery

**Descargarlo e incluirlo en los documentos web que se deseen utilizar**
Librería de jQuery (https://jquery.com/) (Versión actual es la 3.7.1.) e incluirla en el código.
```html
<!-- Recuerda que no vale poner <script/> aqui -->
<script type=”text/javascript” src=”jquery.js”></script>
```

Se puede descargar la versión comprimida o minificada (menos espacio, menor tiempo de carga para el usuario) o la descomprimida que viene mejor para el trabajo en desarrollo.

**Incluirla desde un CDN (Content Delivery Network)**
```html
<script src="https://ajax.googleapis.com/ajax/libs/jquery/3.3.1/jquery.min.js"></script>

<!-- O cualquier otro... el que mantiene Microsoft, el de jQuery, el de Bootstrap.... -->
```


Siempre que se use jQuery y este haya sido insertado en el `<header>` (si se inserta en el `<body>` da igual) debe usarse la instrucción:

```javascript
$(document).ready(function() {

});
```

O la nativa de JavaScript:

```javascript
document.addEventListener('DOMContentLoaded', function() {
    // Tu código aquí
});
```

Esto se hace para asegurarse de que el árbol DOM se ha generado. Esta instrucción indica que el código jQuery se ejecute cuando el DOM, el código se ha cargado completamente.
Si los objetos no se han cargado no debe ejecutarse ningún código jQuery ya que dará un error. 
(Ojo, es el DOM al que espera; no espera a que se cargue la imagen en el código HTML).

La **función que más se utilizará en jQuery** es `$()`, equivalente a `getElementsByTagName()`, `getElementsByName()` y `getElementsById()`

Con ella se puede:
- **Seleccionar un ID**: `$("#miId")`
- **Seleccionar todos los elementos de una cierta etiqueta en un HTML** (Ej.: `<a>` ): `$("a")`
- **Seleccionar varios elementos**, separándolos por coma: `$("#miLinea,a")`
- **Selección mediante el nombre de la clase**: `$(".miCSS")`
- **Seleccionar elementos con ciertos atributos:** `$("a[type]")`
- **Seleccionar elementos con ciertos atributos pero definiendo algún valor al atributo:** `$("input[@type-radio]")`
- **Seleccionar elementos utilizando el lenguaje XPath**: `$("/html/body/p")`

Lo habitual es realizar **$(selector).accion()** 
### 3.2. Manejo de eventos

Los **eventos** para interactuar en jQuery facilitan la programación de funcionalidades. 

Se pueden usar de dos formas:
- **Pasándole una función** que especifique cómo se comportará cuando se active
```javascript
$("p").click(function(){
	alert($(this).text());
});
```

- **Sin pasarle una función** por lo que se genera un evento estándar de JavaScript. No hay que usar el prefijo `on`. Esto simula que se ha hecho un click en todos los `<p>` de la página aunque el usuario no haya interactuado. JavaScript "fuerza" a que se ejecuten todos los eventos `click` asociados a los párrafos. Es útil para activar eventos de forma programática sin que el usuario lo haga.

	Invoca el manejador de eventos `click`directamente pero sin disparar el elemento en sí. Si tienes un evento `click` previamente vinculado, este método simplemente ejecutará ese manejador de eventos. 
```javascript
$("p").click();
```

El método **`.trigger()`** en jQuery se usa para **desencadenar un evento** en un elemento de manera programática, es decir, para **simular** que un evento ha ocurrido, aunque el usuario no lo haya hecho realmente.

Dispara el evento y además ejecuta todos los manejadores de eventos registrados, como si un usuario hubiese hecho cli en ellos. No solo ejecuta el manejador sino que también puede hacer que otros eventos o eventos adicionales se propaguen. 

```javascript
$(selector).trigger(eventName, [extraParameters]);
```

### 3.2.1. Eventos importantes

**on() y off()**
- Aparecen en versión 1.7. de jQuery sustituyendo a `bind()` y `unbind()`
- Con `on()` los eventos buscan asociarse al conjunto de eventos seleccionados. Es posible seleccionar más de un evento separándolo con espacios. (Novedad respecto a `bind()`)  Además produce un enlace dinámico en el que pueden añadirse y eliminarse. 

```javascript
$(elements).on(events [, selector] [, data], manejador);

$("#btn").on("click", function() {
                $("#mensaje").text("¡Botón clickeado!");
            });
```

Por su parte `off()`  si se utiliza sin ningún parámetro, eliminará todos los eventos
asociados a dicho elemento. De lo contrario, todos los eventos asociados a un elemento:

```javascript
$(elements).off( [ events ] [, selector] [, manejador] );

$("#btn").off("click", primeraFuncion); // Solo elimina la primera función

$("#btn").off("click"); // Se desactiva el evento de clic

```


**toggle()** 
- Realiza dos acciones: La primera se ejecuta cada vez que hacemos un clic sobre el elemento o todas las veces impares. La segunda al pulsar por segunda vez o todas las veces pares. Al usarlo deben pasarse ambas funciones a través de variables. 

```javascript
$(“p”).toggle(variable1, variable2);
```

## 4. Ejecución de secuencias

Las sentencias JavaScript se ejecutan línea por línea. Al trabajar con eventos, la siguiente línea de código se puede ejecutar aunque el evento no haya finalizado lo que puede generar errores.

Una **función callback** es aquella que se ejecuta después de que el efecto haya terminado de ejecutarse. 
Se emplea la sintaxis parecida a esta: `$(selector). hide(speed, callback);`
Aquí el selector se oculta y durará `speed` la animación de ocultarse, llamándose después a la `callback`.

```javascript
$(“button”).click(function(){
	$(“p”).hide(“slow”, function(){ 
		alert(“The paragraph is now hidden”);
	});
});
```

## 5. Comportamientos interactivos. Comportamientos de los elementos

### 5.1. Comportamientos de los elementos

**Eventos capaces de transformar los elementos para realizar efectos visuales y conseguir animaciones.**
Eventos que pueden realizarse con jQuery.
#### Efectos básicos

`.show ([duración] [,easing] [,callback])`
Muestra el elemento que estaba oculto.
- **Duración**: Puuede ser `slow` o `fast` o un número en milisegundos
- **Easing**: Tipo de transición. Se necesitará un plugin para hacer más funciones de transición. ( `swing` suave, `linear` velocidad constante...)
- **Callback**

`.hide ([duración] [,easing] [callback])`
Método similar pero que realiza la acción de ocultar el elemento. Mismos parámetro que `show()`

#### Efectos fading (opacidad-transparencia)

Se llama **fading** al efecto de desvanecimiento de los elementos. Se juega con la opacidad y la transparencia.

`.fadeIn ([duración] [,easing] [,callback])`
Muestra el elemento con opacidad gradual (hasta llegar a 1)

`.fadeOut ([duración] [,easing] [,callback])`
Oculta el elemento con opacidad gradual (hasta llegar a 0)

`.fadeToggle ([duración] [,easing] [,callback])`
Alterna entre aparecer y desaparecer el elemento según se haga clic sobre él (como `toggle()`)

`.fadeTo(duración, opacidad, [,easing] [,callback])`
Ajusta la opacidad del elemento según el valor que se le pase, que debe ser entre 0 y 1. Lo hará durante el tiempo que se le indique.

#### Efectos sliding (desplazamiento)

Se llama **sliding** al efecto de desplazar los elementos realizando efectos de plegado odespliegue.

`.slideUp ([duración] [,easing] [,callback])`
Recoge los elementos en altura de forma gradual.

`.slideDown ([duración] [,easing] [,callback])`
Despliega los elementos en altura de forma gradual.

`.slideToggle ([duración] [,easing] [,callback])`
Alterna el proceso de plegar y desplegar el elemento según los clics realizados (como `toggle()`)

#### Otros efectos

Para aumentar las prestaciones de las animaciones:
`.animate (propiedades, [duración], [,easing],[,callback])`
Anima el elemento según lo que se indique en propiedades. 
Este método es más simple que el método `.css()` ya que en `animate()` se tienen que pasar valores numéricos en el parámetro propiedades. No se puede animar con propiedades que no sean valores numéricos.

`.delay(duración [,NombreCola])`
Retrasa la animación de los elementos en una estructura cola según la duración que se indique.
- Duración: Tiempo que se retrasará
- NombreCola: Cadena que contendrá los elementos que se retrasarán

`stop()` Parará la animación si está en proceso.

### 5.2. Comportamientos interactivos

Eventos que se tiene disponibles para realizar con ratón, teclado y asociados a las ventanas.
#### Eventos de ratón

Tendrán siempre una estructura básica `elemento.evento(funcion (handler))`

- **.click()**: Cuando el usuario se coloca sobre un elemento y presiona clic izquierdo sobre el ratón y lo levante todo ello en el mismo objeto. Todos los HTML pueden recibir este evento.
- **.dbiclick()**: Tras hacer doble clic
- **.focusin()**: Cuando un objeto recibe el foco
- **.focusout()**: Cuando un objeto pierde el foco
- **.mousedown()**: Cuando se hace clic sobre el objeto, aunque no hace falta levantarlo para que se ejecute
- **.mouseup()**: Después de levantar el botón del ratón
- **.mouseenter()**: Cuando el puntero entra en el objeto, sin necesidad de hacer clic sobre él
- **.mouseleave()**: Cuando sale el puntero del objeto
- **.mousemove()**: Siempre que se mueva el puntero dentro del objeto
- **.mouseover()**: Parecido a mouseenter() pero se ejecuta incluso cuando el ratón entra en elementos anidados dentro del elemento
- **.mouseout()**: Opuesto a mouseover. Parecido a mouseleave pero se ejecuta incluso cuando el ratón sale del área de elementos anidados.

#### Eventos de teclado
- **.focusin()**: Cuando un objeto recibe el foco.
- **.focusout()**: Cuando un objeto pierde el foco
- **.keydown()**: Cuando se presiona una tecla y el elemento posee el foco. Si se quiere saber qué tecla se ha presionado se examina el objeto `event` que se le pasa a la función. Con la propiedad `.which` de event se puede recuperar el código de la letra que se presiona. Si se quiere recuperar el texto que se introduce, se usa `.keypress()`
- **.keyup()**: Se ejecuta cuando se deja de presionar una tecla y el elemento pose el foco
- **.keypress()**: Se ejecuta cuando se presiona una tecla pero este registrará cada carácter que se introduzca (keydown() solo lo hace una vez aunque se deje presionado)

#### Eventos de ventana
- **.scroll()**: Propiedad para visualizar la barra de desplazamiento en la aplicación.
- **.resize()**: Se ejecutará cuando a una ventana se le cambia el tamaño. 


```javascript
        // 5.1. Comportamientos de los elementos - Efectos básicos
        // Mostrar el elemento con un fadeIn
        $("#miElemento").click(function() {
            $(this).fadeIn("slow", function() {
                alert("Elemento mostrado con fadeIn.");
            });
        });

        // Ocultar el elemento con fadeOut
        $("#miElemento").dblclick(function() {
            $(this).fadeOut("slow", function() {
                alert("Elemento ocultado con fadeOut.");
            });
        });

        // 5.1. Comportamientos de los elementos - Efectos sliding
        // Slide up y slide down
        $("#miElemento2").mouseenter(function() {
            $(this).slideUp("slow", function() {
                alert("Elemento recogido con slideUp.");
            });
        }).mouseleave(function() {
            $(this).slideDown("slow", function() {
                alert("Elemento desplegado con slideDown.");
            });
        });

        // 5.1. Comportamientos de los elementos - Efectos de animación
        $("#miElemento3").click(function() {
            $(this).animate({
                width: "400px", 
                height: "400px"
            }, 1000, "swing", function() {
                alert("Elemento animado (cambio de tamaño).");
            });
        });

        // 5.2. Comportamientos interactivos - Eventos de ratón
        // Click
        $("#miElemento").click(function() {
            alert("Clic realizado sobre el elemento.");
        });

        // Double click
        $("#miElemento2").dblclick(function() {
            alert("Doble clic realizado sobre el elemento.");
        });

        // Mouseenter y mouseleave
        $("#miElemento").mouseenter(function() {
            $(this).css("background-color", "orange");
        }).mouseleave(function() {
            $(this).css("background-color", "lightblue");
        });

        // 5.2. Comportamientos interactivos - Eventos de teclado
        // keydown, keyup
        $(document).keydown(function(event) {
            console.log("Tecla presionada: " + event.key);
        });

        $(document).keyup(function(event) {
            console.log("Tecla liberada: " + event.key);
        });

        // 5.2. Comportamientos interactivos - Eventos de ventana
        // Resize
        $(window).resize(function() {
            console.log("La ventana ha sido redimensionada.");
        });

        // Scroll
        $(window).scroll(function() {
            console.log("Se está desplazando por la página.");
        });
```

## 6. Modificar página con jQuery

### 6.1. Contenido

**text()**: Establece o devuelve el contenido de texto de los elementos seleccionados
**html()**: Establece o devuelve el contenido de los elementos seleccionados
**val()**: Establece o devuelve el valor de los campos de un formulario

### 6.2. Atributos

**attr()**: Establece o cambia los valores de los atributos

### 6.3. Añadir/Eliminar elementos

**append()**: Inserta contenido al final de los elementos HTML seleccionados
**prepend()**: Inserta contenido al principio de los elementos HTML seleccionados
Ambos admiten un número infinito de nuevos elementos como parámetros.

**after()**: Inserta contenido después de elementos HTML seleccionados
**before()**: Inserta contenido antes de elementos HTML seleccionados
**remove()**: Elimina el elemento seleccionado (y sus elementos hijos). Acepta un parámetro que le permite filtrar los elementos a eliminar
**empty()**: Elimina elementos hijos del elemento seleccionado

### 6.4. Manipulación de CSS

**addClass()**: Añade una o más clases a los elementos seleccionados
**removeClass()**: Elimina una o más clases de los elementos seleccionados
**toggleClass()** Cambia entre adición/eliminación de las clases de los elementos seleccionados
**css()** Establece o devuelve el atributo de estilo

`$('#h').css('fontSize')`
`$("p").css("background-color","yellow");`
`$("p").css("background-color":"yellow","color":"red);`
### 6.5. Definir eventos de forma dinámica

Insertar elemento de forma dinámica y se quiere asignar un comportamiento determinado a un evento:

```javascript
$(".informacion").on("dblclic","p",function(){
	$(this).css("border","red 10px solid");
})
```


```javascript
        // **Contenido**
        $("#textButton").click(function() {
            $("#parrafo").text("Texto cambiado con .text()");
        });

        $("#htmlButton").click(function() {
            $("#parrafo").html("<strong>Texto HTML cambiado con .html()</strong>");
        });

        $("#valButton").click(function() {
            let val = $("#inputField").val();  // Obtiene el valor actual del campo de texto
            alert("Valor del campo de texto: " + val);
            $("#inputField").val("Nuevo texto");
        });

        // **Atributos**
        $("#attrButton").click(function() {
            $("#myLink").attr("href", "https://www.google.com");  // Cambia el atributo href
            alert("El atributo href ha sido cambiado a Google.");
        });

        // **Añadir/Eliminar elementos**
        $("#appendButton").click(function() {
            $("#lista").append("<li>Elemento añadido al final</li>");
        });

        $("#prependButton").click(function() {
            $("#lista").prepend("<li>Elemento añadido al principio</li>");
        });

        $("#afterButton").click(function() {
            $("#lista").after("<p>Este párrafo se ha añadido después de la lista.</p>");
        });

        $("#beforeButton").click(function() {
            $("#lista").before("<p>Este párrafo se ha añadido antes de la lista.</p>");
        });

        $("#removeButton").click(function() {
            $("#lista li").last().remove();  // Elimina el último elemento de la lista
        });

        $("#emptyButton").click(function() {
            $("#lista").empty();  // Vacía la lista eliminando todos sus elementos hijos
        });

        // **Manipulación de CSS**
        $("#addClassButton").click(function() {
            $(".rojo").addClass("verde");  // Añade la clase 'verde' al texto
        });

        $("#removeClassButton").click(function() {
            $(".rojo").removeClass("rojo");  // Elimina la clase 'rojo' del texto
        });

        $("#toggleClassButton").click(function() {
            $(".rojo").toggleClass("amarillo");  // Alterna la clase 'amarillo' del texto
        });

        $("#cssButton").click(function() {
            $(".rojo").css("fontSize", "20px");  // Cambia el tamaño de la fuente a 20px
            $(".rojo").css("background-color", "pink");  // Cambia el color de fondo
        });
```
## 7. Reemplazo de jQuery actualmente

✅ **JavaScript puro (ES6+)** – Ya tiene todo lo necesario sin jQuery.  
✅ **React.js / Vue.js / Angular** – Para aplicaciones interactivas modernas.  
✅ **CSS moderno** – Para animaciones y efectos sin jQuery.  
✅ **Fetch API** – Para peticiones AJAX sin necesidad de `$.ajax()`.  
✅ **Librerías especializadas** – En lugar de usar jQuery para todo, ahora hay pequeñas librerías para casos específicos (ejemplo: GSAP para animaciones).