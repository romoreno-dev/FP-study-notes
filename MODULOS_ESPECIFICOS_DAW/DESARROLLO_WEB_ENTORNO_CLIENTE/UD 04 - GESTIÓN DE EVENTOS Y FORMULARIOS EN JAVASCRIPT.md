
## 1. Objeto Form

Los **formularios** son el principal medio de introducción de datos en una aplicación web y el principal punto de interactividad con el usuario.
JavaScript permite aportar interactividad a los elementos estáticos del formulario HTML. 

Los formularios y sus controles son objetos del DOM con propiedades únicas que otros objetos no poseen. Con JavaScript:
- Se pueden **examinar y validar las entradas del usuario** directamente en el lado del cliente
- Se pueden emitir **mensajes instantáneos** con información de la entrada del usuario. 
Podemos mencionar como elementos el Formulario, Campo de texto, Campo oculto, Área de texto, Casilla de verificación, Grupo de casillas de verificación, Botón de opción, Grupo de opción, Seleccionar Lista, Menú de salto, Campo de imagen, Campo de archivo, Botón, Etiqueta, Juego de campos.

El objeto `form` es una propiedad del objeto `document` que se corresponde con la etiqueta `<form>` del HTML.

El formulario puede ser enviado:
- Haciendo clic en el botón submit del formulario
- Llamando al método `form.submit()` de JavaScript. 

### 1.1. Formas de selección del objeto Form

```html
<div id="menulateral">
	<form id="contactar" name="contactar" action="...">...</form>
</div>
```

```javascript
// 1. Con el método getElementById()
var formulario = document.getElementById("contactar")

// 2. Con el método getElementsByTagName()
var formularios = document.getElementsByTagName("form")[0]

var menu = document.getElementById("menulateral")
var formularios=menu.getElementsByTagName("form")[0]

// 3. A través de la colección forms[]
var formulario = document.forms[0]
var formulario = document.forms["contactar"] // Formulario con name "contactar"
```

### 1.2. El formulario como objeto y contenedor

Al cargar la información HTML por el navegador, se realiza estructura en árbol del documento en la que se generan nodos que cuelgan de un árbol raíz.

Netscape inventó el **DOM nivel 0**: Especificación contenida en documentos ECMAScript que definen el lenguaje JavaScript pero mucho más detallado que el modelo BOM desarrollado por Microsoft en el que nunca hubo documentación. La aparición de XML W3C estandarizo el modelo en tres niveles: 1,2 y 3. Cada nivel ha ido añadiendo nuevas posibilidades y características. `getElementById()` surge a partir de la versión 2.0. 

El objeto `Form` está dentro de dos árboles al mismo tiempo.
En nuevas definiciones del DOM se especifica que el `Form` es el padre de todos sus nodos hijos, incluidos objetos y textos. En versiones antiguas solo era padre de `input`, `select`, `button` y `textarea`.

**Jerarquía de nivel 0 (DOM 0)**
Hace muchísimo más fácil leer y escribir los controles del formulario. En sus hijos `p` no se encuentra entre la lista de los posibles hijos, por ejemplo. 
![[Pasted image 20250203225829.png]]

**Jerarquía de nivel 2 (DOM 2)** 
Puede ser usado para leer y escribir en todo el documento con un nivel muy fino de granularidad. 

Se use una u otra, los objetos siguen siendo los mismos.

Para: 

```html
<form action="buscar.php" name="formulario" id="miFormu" method="post">
	<p>
		<label for="busqueda">Buscar por:</label>
		<input id="busqueda" name="busqueda" type="text" value="">
		<input id="submit" type="submit" value="Buscar">
	</p>
</form>
```

```javascript
var formulario = document.getElementById("miFormu")
var control = formulario.busqueda
```

### 1.3. Acceso a propiedades y métodos del formulario



## 2. Objetos relacionados con formularios


### 2.1. Objeto input de tipo texto

### 2.2. Objeto input de tipo checkbox

### 2.3. Objeto input de tipo radio
### 2.4. Objeto select

### 2.5. Paso de objetos a funciones



## 3. Eventos

### 3.1. Modelo de registro de eventos en línea

### 3.2. Modelo de registro de eventos tradicional


### 3.3. Modelo de registro avanzado de eventos según W3C



### 3.4. Modelo de registro de eventos según Microsoft


### 3.5. Orden de disparo de los eventos


## 4. Envío y validación de formularios

### 4.1. Ejemplo sencillo de validación de un formulario


## 5. Expresiones regulares y objetos RegExp

### 5.1. Caracteres especiales en expresiones regulares

### 5.2. Objeto RegExp

### 5.3. Ejemplos


## 6. Las cookies

### 6.1. Gestión y uso de cookies




## 7. HTML 5












