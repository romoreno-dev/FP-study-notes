
## 0. CSS. Definición.

Las **hojas de estilo en cascada** (**CSS, Cascading Style Sheets**) son la parte del diseño de las aplicaciones web.

- Permiten **ahorrar tiempo** a la hora de diseñar webs
- Consiguen **efectos potentes** que **la gran mayoría de navegadores soportan**
- Permiten **separar el contenido (información) del diseño (apariencia)**, mejorando el **mantenimiento**. En la etiqueta `<body>` del HTML se define la estructura HTML y en el `<head>` o en un archivo externo se define la apariencia.
- Se produce la **adaptación de los sitios web para diferentes dispositivos** (comportamiento **reponsive**)
## 1. Estilos en línea basados en etiquetas, en clases y en identificadores

Para definir una regla de estilo se usan selectores. Son las propias etiquetas del documento HTML.

```
selector {atributo : valor}
```
El atributo son las características que se pretenden modificar del selector.
El valor hace referencia a la instancia del atributo.

```css
h1 {color: blue;} /*un selector, un estilo*/
h1, h2{color: blue;} /*varios selectores, varios estilos*/
h1{color: blue; background-color: red;} /*varios estilos*/
```

- **background**: Establece el fondo de un elemento (color, imagen, posición, etc.).
- **background-color**: Define el color de fondo.
- **border**: Define el borde de un elemento (ancho, estilo y color).
- **border-bottom**: Configura el borde inferior.
- **border-bottom-color**: Especifica el color del borde inferior.
- **border-bottom-style**: Define el estilo del borde inferior (sólido, punteado, etc.).
- **border-bottom-width**: Especifica el grosor del borde inferior.
- **border-color**: Define el color de todos los bordes.
- **border-left**: Configura el borde izquierdo.
- **border-left-color**: Especifica el color del borde izquierdo.
- **border-left-style**: Define el estilo del borde izquierdo.
- **border-left-width**: Establece el grosor del borde izquierdo.
- **border-right**: Configura el borde derecho.
- **border-right-color**: Especifica el color del borde derecho.
- **border-right-style**: Define el estilo del borde derecho.
- **border-right-width**: Establece el grosor del borde derecho.
- **border-style**: Define el estilo de todos los bordes.
- **border-top**: Configura el borde superior.
- **border-top-color**: Especifica el color del borde superior.
- **border-top-width**: Establece el grosor del borde superior.
- **border-width**: Define el grosor de todos los bordes.
- **color**: Define el color del texto.
- **display**: Especifica cómo se muestra un elemento (block, inline, flex, etc.).
- **font**: Propiedad abreviada para configurar todas las propiedades de fuente.
- **font-family**: Define la fuente del texto.
- **font-size**: Especifica el tamaño del texto.
- **font-style**: Define el estilo de la fuente (normal, itálica, oblicua).
- **font-variant**: Controla la variación de la fuente (small-caps, normal).
- **font-weight**: Especifica el grosor de la fuente (normal, bold, valores numéricos).
- **height**: Establece la altura del elemento.
- **letter-spacing**: Define el espacio entre caracteres.
- **line-height**: Controla la altura de línea del texto.
- **list-style-type**: Especifica el estilo de viñeta de listas.
- **table-layout**: Controla el diseño de una tabla (auto, fixed).
- **text-align**: Define la alineación del texto (izquierda, centro, derecha, justificado).
- **text-decoration**: Aplica decoraciones al texto (subrayado, tachado, etc.).
- **text-indent**: Define la sangría de la primera línea del texto.
- **text-transform**: Controla la capitalización del texto (uppercase, lowercase, capitalize).
- **vertical-align**: Ajusta la alineación vertical de un elemento en línea.
- **width**: Establece el ancho del elemento.



Se pueden definir estilos directamente a las etiquetas HTML que contengan dicha clase.

Distintos tipos de clases:
- Clases asociadas directamente a una etiqueta HTML `h2.color1 {color:green}`
- Clases genéricas aplicadas a cualquier etiqueta `.color2{color:blue;}`

```
<h2 class="color1">Texto color verde</h1>
<h2>Texto color azul<h1/>
```

Las clases genéricas permiten asignar más de una clase a la misma etiqueta.

```

```

`:link` Enlaces que no se han visitado
`:visited` Enlaces que se han visitado una vez como mínimo
`:hover` Elementos marcados por el usuario
`:active` Elementos que se activan
`:focus` Elementos que tienen el foco 
`:first-line`: 
`:first-letter`: 
`:before`:
`:after`:


(Completar.......................... con aputnes y demas)

```
<head>
  <style>
    h1 {color: white; background-color: blue}
    h2.color1 {color:green} /*Solo a la clase del selector ese*/
    .color2{color:blue;}
    h2.fondobonito{background-color: red}
    #miTexto{color:pink} /*por Id*/
    h3, h4 {background-color: yellow}  /*Varios selectores*/
    h1 b {color: green} /*Anidados: Selector anidado común, afecta solo al interior*/
    h1 > b {color: pink} /*Anidados: Selector hijo anidado, afecta solo al que tiene el elemento inmediatamente como hijo*/
    :hover {color: yellow}
    
    /*
    No se aplica a elementos con fondos de colores fuertes:

Si tienes elementos con un fondo sólido (como h1 {background-color: blue} o .fondobonito {background-color: red}), el cambio de color de texto a blanco puede no ser visible.
Algunos elementos no tienen un color de texto definido antes del hover:

Por ejemplo, si un h3 no tiene una regla explícita de color de texto antes del :hover, puede que no notes el cambio.
Especificidad de los selectores:

Algunas reglas CSS más específicas pueden estar sobreescribiendo el :hover en ciertos elementos. Por ejemplo, h1 {color: white;} ya establece el color de h1, lo que podría impedir que :hover {color: white;} tenga efecto visible.
    */
    
  </style>
</head>
<body>
  <h1>Hola mundo</h1>
  <h2 class="color1 fondobonito">Texto color verde</h2>
  <h3 class="color1 fondobonito">Pero este es color negro, no esta definido</h3>
  <h2 class="color2">Texto color azul</h2>
  <h3 class="color2">También este es color azul</h2>
  <h3 id="miTexto">Texto</h3>
  <h1><li><b>Pepe</b></li></h1>
  <h1><b>Pepe</b></h1>
</body>
```

### **Diferencia entre Pseudo-clases (`:`) y Pseudo-elementos (`::`)**

|Tipo|Uso|Ejemplo|
|---|---|---|
|**Pseudo-clases (`:`)**|Se aplican a elementos en ciertos estados o condiciones.|`:hover`, `:focus`, `:nth-child()`, `:first-child`|
|**Pseudo-elementos (`::`)**|Se aplican a partes específicas de un elemento.|`::before`, `::after`, `::first-letter`, `::selection`|

**Ejemplo combinado:**



### 1.1. Selectores basados en etiquetas




### 1.2. Selectores basados en clases



### 1.3. Selectores basados en identificadores




### 1.4. Agrupación de selectores



### 1.5. Anidamiento de selectores




### 1.5.1. Selector anidado común




### 1.5.2. Selector hijo anidado



### 1.6. Atributos



### 1.7. Pseudoclases



### 1.8. Pseudoelementos



## 2. Crear y vincular hojas de estilo

## 3. Herramientas y tests de verificación

## 4. Guía de estilo

https://jigsaw.w3.org/css-validator/

w3.org/TR/css-2024


Taildwind, Bootstrap, W3CSS, Astro,... 

w3Schools